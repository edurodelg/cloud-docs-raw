---
merged_at: 2026-01-26T23:04:05.994873
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deploy-confidential-containers-default-policy -->

# Deploy an AKS cluster with Confidential Containers and an automatically generated policy

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you use the Azure CLI to deploy an Azure Kubernetes Service (AKS) cluster and configure Confidential Containers (preview) with an automatically generated security policy. You then deploy an application as a Confidential container. To learn more, read the [overview of AKS Confidential Containers](confidential-containers-overview).

In general, getting started with AKS Confidential Containers involves the following steps.

- Deploy or upgrade an AKS cluster using the Azure CLI
- Add an annotation to your pod YAML manifest to mark the pod as using confidential containers
- Add a security policy to your pod YAML manifest
- Deploy your application in confidential computing

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Prerequisites

The Azure CLI version 2.44.1 or later. Run

`az --version`

to find the version, and run`az upgrade`

to upgrade the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).The

`aks-preview`

Azure CLI extension version 0.5.169 or later.The

`confcom`

Confidential Container Azure CLI extension 0.3.3 or later.`confcom`

is required to generate a[security policy](/en-us/azure/confidential-computing/confidential-containers-aks-security-policy).Register the

`Preview`

feature in your Azure subscription.AKS supports Confidential Containers (preview) on version 1.25.0 and higher.

A workload identity and a federated identity credential. The workload identity credential enables Kubernetes applications access to Azure resources securely with a Microsoft Entra ID based on annotated service accounts. If you aren't familiar with Microsoft Entra Workload ID, see the

[Microsoft Entra Workload ID overview](/en-us/azure/active-directory/workload-identities/workload-identities-overview)and review how[Workload Identity works with AKS](workload-identity-overview).The identity you're using to create your cluster has the appropriate minimum permissions. For more information about access and identity for AKS, see

[Access and identity options for Azure Kubernetes Service (AKS)](concepts-identity).To manage a Kubernetes cluster, use the Kubernetes command-line client

[kubectl](https://kubernetes.io/docs/reference/kubectl/). Azure Cloud Shell comes with`kubectl`

. You can install kubectl locally using the[az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli)command.Confidential containers on AKS provide a sidecar open source container for attestation and secure key release. The sidecar integrates with a Key Management Service (KMS), like Azure Key Vault, for releasing a key to the container group after validation is completed. Deploying an

[Azure Key Vault Managed HSM](/en-us/azure/key-vault/managed-hsm/overview)(Hardware Security Module) is optional but recommended to support container-level integrity and attestation. See[Provision and activate a Managed HSM](/en-us/azure/key-vault/managed-hsm/quick-create-cli)to deploy Managed HSM.

### Install the aks-preview Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

To install the aks-preview extension, run the following command:

```
az extension add --name aks-preview
```


Run the following command to update to the latest version of the extension:

```
az extension update --name aks-preview
```


### Install the confcom Azure CLI extension

To install the confcom extension, run the following command:

```
az extension add --name confcom
```


Run the following command to update to the latest version of the extension:

```
az extension update --name confcom
```


### Register the KataCcIsolationPreview feature flag

Register the `KataCcIsolationPreview`

feature flag by using the [az feature register](/en-us/cli/azure/feature#az-feature-register) command, as shown in the following example:

```
az feature register --namespace "Microsoft.ContainerService" --name "KataCcIsolationPreview"
```


It takes a few minutes for the status to show *Registered*. Verify the registration status by using the [az feature show](/en-us/cli/azure/feature#az-feature-show) command:

```
az feature show --namespace "Microsoft.ContainerService" --name "KataCcIsolationPreview"
```


When the status reflects *Registered*, refresh the registration of the *Microsoft.ContainerService* resource provider by using the [az provider register](/en-us/cli/azure/provider#az-provider-register) command:

```
az provider register --namespace "Microsoft.ContainerService"
```


## Deploy a new cluster

Create an AKS cluster using the

[az aks create](/en-us/cli/azure/aks#az-aks-create)command and specifying the following parameters:**--os-sku**:*AzureLinux*. Only the Azure Linux os-sku supports this feature in this preview release.**--node-vm-size**: Any Azure VM size that supports AMD SEV-SNP protected child VMs works. For example,[Standard_DC8as_cc_v5](/en-us/azure/virtual-machines/dcasccv5-dcadsccv5-series)VMs.**--enable-workload-identity**: Enables creating a Microsoft Entra Workload ID enabling pods to use a Kubernetes identity.**--enable-oidc-issuer**: Enables OpenID Connect (OIDC) Issuer. It allows a Microsoft Entra ID or other cloud provider identity and access management platform the ability to discover the API server's public signing keys.**--workload-runtime**: Specify*KataCcIsolation*to enable the Confidential Containers feature on the node pool.

`az aks create --resource-group myResourceGroup --name myAKSCluster --kubernetes-version <1.25.0 and above> --os-sku AzureLinux --node-vm-size Standard_DC8as_cc_v5 --workload-runtime KataCcIsolation --node-count 1 --enable-oidc-issuer --enable-workload-identity --generate-ssh-keys`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

When the cluster is ready, get the cluster credentials using the

[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Deploy to an existing cluster

To use this feature with an existing AKS cluster, the following requirements must be met:

- Follow the steps to
[register the KataCcIsolationPreview](#register-the-kataccisolationpreview-feature-flag)feature flag. - Verify the cluster is running Kubernetes version 1.25.0 and higher.
[Enable workload identity](workload-identity-deploy-cluster#deploy-and-configure-microsoft-entra-workload-id-on-an-azure-kubernetes-service-aks-cluster)on the cluster if it isn't already.

Use the following command to enable Confidential Containers (preview) by creating a node pool to host it.

Add a node pool to your AKS cluster using the

[az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add)command. Specify the following parameters:**--resource-group**: Enter the name of an existing resource group to create the AKS cluster in.**--cluster-name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**--name**: Enter a unique name for your clusters node pool, such as*nodepool2*.**--workload-runtime**: Specify*KataCcIsolation*to enable the feature on the node pool. Along with the`--workload-runtime`

parameter, these other parameters shall satisfy the following requirements. Otherwise, the command fails and reports an issue with the corresponding parameter(s).**--os-sku**:*AzureLinux*. Only the Azure Linux os-sku supports this feature in this preview release.**--node-vm-size**: Any Azure VM size that supports AMD SEV-SNP protected child VMs nested virtualization works. For example,[Standard_DC8as_cc_v5](/en-us/azure/virtual-machines/dcasccv5-dcadsccv5-series)VMs.

The following example adds a user node pool to

*myAKSCluster*with two nodes in*nodepool2*in the*myResourceGroup*:`az aks nodepool add --resource-group myResourceGroup --name nodepool2 –-cluster-name myAKSCluster --node-count 2 --os-sku AzureLinux --node-vm-size Standard_DC8as_cc_v5 --workload-runtime KataCcIsolation`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

Run the

[az aks update](/en-us/cli/azure/aks#az-aks-update)command to enable Confidential Containers (preview) on the cluster.`az aks update --name myAKSCluster --resource-group myResourceGroup`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

When the cluster is ready, get the cluster credentials using the

[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Configure container

Before you configure access to the Azure Key Vault and secret, and deploy an application as a Confidential container, you need to complete the configuration of the workload identity.

To configure the workload identity, perform the following steps described in the [Deploy and configure workload identity](workload-identity-deploy-cluster) article:

- Retrieve the OIDC Issuer URL
- Create a managed identity
- Create Kubernetes service account
- Establish federated identity credential

Important

You need to set the *environment variables* from the section **Export environmental variables** in the [Deploy and configure workload identity](workload-identity-deploy-cluster) article to continue completing this tutorial. Remember to set the variable `SERVICE_ACCOUNT_NAMESPACE`

to `kafka`

, and execute the command `kubectl create namespace kafka`

before configuring workload identity.

## Deploy a trusted application with kata-cc and attestation container

The following steps configure end-to-end encryption for Kafka messages using encryption keys managed by [Azure Managed Hardware Security Modules](/en-us/azure/key-vault/managed-hsm/overview) (mHSM). The key is only released when the Kafka consumer runs within a Confidential Container with an Azure attestation secret provisioning container injected in to the pod.

This configuration is based on the following four components:

- Kafka Cluster: A simple Kafka cluster deployed in the Kafka namespace on the cluster.
- Kafka Producer: A Kafka producer running as a vanilla Kubernetes pod that sends encrypted user-configured messages using a public key to a Kafka topic.
- Kafka Consumer: A Kafka consumer pod running with the kata-cc runtime, equipped with a secure key release container to retrieve the private key for decrypting Kafka messages and render the messages to web UI.

For this preview release, we recommend for test and evaluation purposes to either create or use an existing Azure Key Vault Premium tier resource to support storing keys in a hardware security module (HSM). We don't recommend using your production key vault. If you don't have an Azure Key Vault, see [Create a key vault using the Azure CLI](/en-us/azure/key-vault/general/quick-create-cli).

Grant the managed identity you created earlier, and your account, access to the key vault.

[Assign](/en-us/azure/key-vault/general/rbac-guide#assign-role)both identities the**Key Vault Crypto Officer**and**Key Vault Crypto User**Azure RBAC roles.Note

The managed identity is the value you assign to the

`USER_ASSIGNED_IDENTITY_NAME`

variable.To add role assignments, you must have

`Microsoft.Authorization/roleAssignments/write`

and`Microsoft.Authorization/roleAssignments/delete`

permissions, such as[Key Vault Data Access Administrator](/en-us/azure/role-based-access-control/built-in-roles#key-vault-data-access-administrator),[User Access Administrator](/en-us/azure/role-based-access-control/built-in-roles#user-access-administrator), or[Owner](/en-us/azure/role-based-access-control/built-in-roles#owner).You must use the Key Vault Premium SKU to support HSM-protected keys.


Run the following command to set the scope:

`AKV_SCOPE=$(az keyvault show --name <AZURE_AKV_RESOURCE_NAME> --query id --output tsv)`

Run the following command to assign the

**Key Vault Crypto Officer**role.`az role assignment create --role "Key Vault Crypto Officer" --assignee "${USER_ASSIGNED_IDENTITY_NAME}" --scope $AKV_SCOPE`

Run the following command to assign the

**Key Vault Crypto User**role.`az role assignment create --role "Key Vault Crypto User" --assignee "${USER_ASSIGNED_IDENTITY_NAME}" --scope $AKV_SCOPE`

Install the Kafka cluster in the kafka namespace by running the following command:

`kubectl create -f 'https://strimzi.io/install/latest?namespace=kafka' -n kafka`

Run the following command to apply the

`kafka`

cluster CR file.`kubectl apply -f https://strimzi.io/examples/latest/kafka/kafka-persistent-single.yaml -n kafka`

Prepare the RSA Encryption/Decryption key using the

[bash script](https://github.com/microsoft/confidential-container-demos/raw/main/kafka/setup-key.sh)for the workload from GitHub. Save the file as`setup-key.sh`

.Set the

`MAA_ENDPOINT`

environment variable with the FQDN of Attest URI by running the following command.`export MAA_ENDPOINT="$(az attestation show --name "myattestationprovider" --resource-group "MyResourceGroup" --query 'attestUri' -o tsv | cut -c 9-)"`

Check if the FQDN of Attest URI is in correct format (the MAA_ENDPOINT should not include the prefix "https://"):

`echo $MAA_ENDPOINT`

Note

To set up Microsoft Azure Attestation, see

[Quickstart: Set up Azure Attestation with Azure CLI](/en-us/azure/attestation/quickstart-azure-cli).Copy the following YAML manifest and save it as

`consumer.yaml`

.`apiVersion: v1 kind: Pod metadata: name: kafka-golang-consumer namespace: kafka labels: azure.workload.identity/use: "true" app.kubernetes.io/name: kafka-golang-consumer spec: serviceAccountName: workload-identity-sa runtimeClassName: kata-cc-isolation containers: - image: "mcr.microsoft.com/aci/skr:2.7" imagePullPolicy: Always name: skr env: - name: SkrSideCarArgs value: ewogICAgImNlcnRjYWNoZSI6IHsKCQkiZW5kcG9pbnRfdHlwZSI6ICJMb2NhbFRISU0iLAoJCSJlbmRwb2ludCI6ICIxNjkuMjU0LjE2OS4yNTQvbWV0YWRhdGEvVEhJTS9hbWQvY2VydGlmaWNhdGlvbiIKCX0gIAp9 command: - /bin/skr volumeMounts: - mountPath: /opt/confidential-containers/share/kata-containers/reference-info-base64 name: endor-loc - image: "mcr.microsoft.com/acc/samples/kafka/consumer:1.0" imagePullPolicy: Always name: kafka-golang-consumer env: - name: SkrClientKID value: kafka-encryption-demo - name: SkrClientMAAEndpoint value: sharedeus2.eus2.test.attest.azure.net - name: SkrClientAKVEndpoint value: "myKeyVault.vault.azure.net" - name: TOPIC value: kafka-demo-topic command: - /consume ports: - containerPort: 3333 name: kafka-consumer resources: limits: memory: 1Gi cpu: 200m volumes: - name: endor-loc hostPath: path: /opt/confidential-containers/share/kata-containers/reference-info-base64 --- apiVersion: v1 kind: Service metadata: name: consumer namespace: kafka spec: type: LoadBalancer selector: app.kubernetes.io/name: kafka-golang-consumer ports: - protocol: TCP port: 80 targetPort: kafka-consumer`

Note

Update the value for the pod environment variable

`SkrClientAKVEndpoint`

to match the URL of your Azure Key Vault, excluding the protocol value`https://`

. The current value placeholder value is`myKeyVault.vault.azure.net`

. Update the value for the pod environment variable`SkrClientMAAEndpoint`

with the value of`MAA_ENDPOINT`

. You can find the value of`MAA_ENDPOINT`

by running the command`echo $MAA_ENDPOINT`

or the command`az attestation show --name "myattestationprovider" --resource-group "MyResourceGroup" --query 'attestUri' -o tsv | cut -c 9-`

.Generate the security policy for the Kafka consumer YAML manifest and obtain the hash of the security policy stored in the

`WORKLOAD_MEASUREMENT`

variable by running the following command:`export WORKLOAD_MEASUREMENT=$(az confcom katapolicygen -y consumer.yaml --print-policy | base64 -d | sha256sum | cut -d' ' -f1)`

To generate an RSA asymmetric key pair (public and private keys), run the

`setup-key.sh`

script using the following command. The`<Azure Key Vault URL>`

value should be`<your-unique-keyvault-name>.vault.azure.net`

`export MANAGED_IDENTITY=${USER_ASSIGNED_CLIENT_ID} bash setup-key.sh "kafka-encryption-demo" <Azure Key Vault URL>`

Note

The envionment variable

`MANAGED_IDENTITY`

is required by the bash script`setup-key.sh`

.The public key will be saved as

`kafka-encryption-demo-pub.pem`

after executing the bash script.

Important

If you receive the error

`ForbiddenByRbac`

,you might need to wait up to 24 hours as the backend services for managed identities maintain a cache per resource URI for up to 24 hours. See also:[Troubleshoot Azure RBAC](/en-us/azure/role-based-access-control/troubleshooting#symptom---role-assignment-changes-are-not-being-detected).To verify the keys have been successfully uploaded to the key vault, run the following commands:

`az account set --subscription <Subscription ID> az keyvault key list --vault-name <KeyVault Name> -o table`

Copy the following YAML manifest and save it as

`producer.yaml`

.`apiVersion: v1 kind: Pod metadata: name: kafka-producer namespace: kafka spec: containers: - image: "mcr.microsoft.com/acc/samples/kafka/producer:1.0" name: kafka-producer command: - /produce env: - name: TOPIC value: kafka-demo-topic - name: MSG value: "Azure Confidential Computing" - name: PUBKEY value: |- -----BEGIN PUBLIC KEY----- MIIBojAN***AE= -----END PUBLIC KEY----- resources: limits: memory: 1Gi cpu: 200m`

Note

Update the value which begin with

`-----BEGIN PUBLIC KEY-----`

and ends with`-----END PUBLIC KEY-----`

strings with the content from`kafka-encryption-demo-pub.pem`

which was created in the previous step.Deploy the

`consumer`

and`producer`

YAML manifests using the files you saved earlier.`kubectl apply -f consumer.yaml`

`kubectl apply -f producer.yaml`

Get the IP address of the web service using the following command:

`kubectl get svc consumer -n kafka`

Copy and paste the external IP address of the consumer service into your browser and observe the decrypted message.

The following example resembles the output of the command:

`Welcome to Confidential Containers on AKS! Encrypted Kafka Message: Msg 1: Azure Confidential Computing`

You should also attempt to run the consumer as a regular Kubernetes pod by removing the

`skr container`

and`kata-cc runtime class`

spec. Since you aren't running the consumer with kata-cc runtime class, you no longer need the policy.Remove the entire policy and observe the messages again in the browser after redeploying the workload. Messages appear as base64-encoded ciphertext because the private encryption key can't be retrieved. The key can't be retrieved because the consumer is no longer running in a confidential environment, and the

`skr container`

is missing, preventing decryption of messages.

## Cleanup

When you're finished evaluating this feature, to avoid Azure charges, clean up your unnecessary resources. If you deployed a new cluster as part of your evaluation or testing, you can delete the cluster using the [az aks delete](/en-us/cli/azure/aks#az-aks-delete) command.

```
az aks delete --resource-group myResourceGroup --name myAKSCluster
```


If you enabled Confidential Containers (preview) on an existing cluster, you can remove the pod(s) using the [kubectl delete pod](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#delete) command.

```
kubectl delete pod pod-name
```


## Next steps

- Learn more about
[Azure Dedicated hosts](/en-us/azure/virtual-machines/dedicated-hosts)for nodes with your AKS cluster to use hardware isolation and control over Azure platform maintenance events.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/how-to-apply-l7-policies -->

# Set up Layer 7(L7) policies with Advanced Container Networking Services

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article demonstrates how to set up L7 policies with Advanced Container Networking Services in AKS clusters. Continue only after you have reviewed the limitations and considerations listed on the [Layer 7 Policy Overview](container-network-security-l7-policy-concepts) page.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


The minimum version of Azure CLI required for the steps in this article is 2.79.0. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Install the `aks-preview`

Azure CLI extension

Install or update the Azure CLI preview extension using the [ az extension add](/en-us/cli/azure/extension#az-extension-add) or

[command.](/en-us/cli/azure/extension#az-extension-update)

`az extension update`

The minimum version of the aks-preview Azure CLI extension is `14.0.0b6`


```
# Install the aks-preview extension
az extension add --name aks-preview
# Update the extension to make sure you have the latest version installed
az extension update --name aks-preview
```


### Register the `AdvancedNetworkingL7PolicyPreview`

feature flag

Register the `AdvancedNetworkingL7PolicyPreview`

feature flag using the [ az feature register](/en-us/cli/azure/feature#az-feature-register) command.

```
az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingL7PolicyPreview"
```


Verify successful registration using the [ az feature show](/en-us/cli/azure/feature#az-feature-show) command. It takes a few minutes for the registration to complete.

```
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingL7PolicyPreview"
```


Once the feature shows `Registered`

, refresh the registration of the `Microsoft.ContainerService`

resource provider using the [ az provider register](/en-us/cli/azure/provider#az-provider-register) command.

### Enable Advanced Container Networking Services

To proceed, you must have an AKS cluster with [Advanced Container Networking Services](advanced-container-networking-services-overview) enabled.

The `az aks create`

command with the Advanced Container Networking Services flag, `--enable-acns`

, creates a new AKS cluster with all Advanced Container Networking Services features. These features encompass:

**Container Network Observability:**Provides insights into your network traffic. To learn more visit[Container Network Observability](advanced-container-networking-services-overview?tabs=cilium#container-network-observability).**Container Network Security:**Offers security features like Fully Qualified Domain Name (FQDN) filtering. To learn more visit[Container Network Security](advanced-container-networking-services-overview?tabs=cilium#container-network-security).

Note

Clusters with the Cilium data plane support Container Network Observability and Container Network security starting with Kubernetes version 1.29.

For this demo, the `--acns-advanced-networkpolicies`

parameter must be set to "L7" to enable L7 policies. Setting this parameter to "L7" also enables FQDN filtering. If you only want to enable FQDN filtering, set the parameter to "FQDN". To disable both features, you can follow the instructions provided in [Disable Container Network Security](advanced-container-networking-services-overview).

```
export CLUSTER_NAME="<aks-cluster-name>"
# Create an AKS cluster
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--generate-ssh-keys \
--network-plugin azure \
--network-dataplane cilium \
--enable-acns \
--acns-advanced-networkpolicies L7
```


### Enable Advanced Container Networking Services on an existing cluster

The [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the Advanced Container Networking Services flag,

`--enable-acns`

, updates an existing AKS cluster with all Advanced Container Networking Services features which includes [Container Network Observability](advanced-container-networking-services-overview?tabs=cilium#container-network-observability)and the

[Container Network Security](advanced-container-networking-services-overview?tabs=cilium#container-network-security)feature.

Note

Only clusters with the Cilium data plane support Container Network Security features of Advanced Container Networking Services.

For this demo, the `--acns-advanced-networkpolicies`

parameter must be set to "L7" to enable L7 policies. Setting this parameter to "L7" also enables FQDN filtering. If you only want to enable FQDN filtering, set the parameter to "FQDN". To disable both features, you can follow the instructions provided in [Disable Container Network Security](advanced-container-networking-services-overview).

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns \
--acns-advanced-networkpolicies L7
```


## Get cluster credentials

Get your cluster credentials using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command.

```
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


## Set up http-server application on your AKS cluster

Apply the below YAML to your AKS cluster to set up the `http-server`

application.

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: http-server
labels:
app: http-server
spec:
replicas: 1
selector:
matchLabels:
app: http-server
template:
metadata:
labels:
app: http-server
spec:
containers:
- name: http-server
image: nginx:latest
ports:
- containerPort: 8080
volumeMounts:
- name: config-volume
mountPath: /etc/nginx/conf.d
volumes:
- name: config-volume
configMap:
name: nginx-config
---
apiVersion: v1
kind: Service
metadata:
name: http-server
spec:
selector:
app: http-server
ports:
- protocol: TCP
port: 80
targetPort: 8080
---
apiVersion: v1
kind: ConfigMap
metadata:
name: nginx-config
data:
default.conf: |
server {
listen 8080;
location / {
return 200 "Hello from the server root!\n";
}
location /products {
return 200 "Listing products...\n";
}
}
```


## Set up http-client application on your AKS Cluster

Apply the below YAML to your AKS cluster to set up the `http-client`

application.

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: http-client
labels:
app: http-client
spec:
replicas: 1
selector:
matchLabels:
app: http-client
template:
metadata:
labels:
app: http-client
spec:
containers:
- name: http-client
image: curlimages/curl:latest
command: ["sleep", "infinity"]
```


## Test connectivity with a policy

Next, apply the following Layer 7 policy to allow only `GET`

requests from the `http-client`

application to the `/products`

endpoint on the `http-server`

:

```
apiVersion: cilium.io/v2
kind: CiliumNetworkPolicy
metadata:
name: allow-get-products
spec:
description: "Allow only GET requests to /products from http-client to http-server"
endpointSelector:
matchLabels:
app: http-server
ingress:
- fromEndpoints:
- matchLabels:
app: http-client
toPorts:
- ports:
- port: "8080"
protocol: TCP
rules:
http:
- method: "GET"
path: "/products"
```


### Verify policy

To verify the policy's enforcement, execute these commands from the `http-client`

pod:

```
kubectl exec -it <your-http-client-pod-name> -n default -- curl -v http://http-server:80/products
```


You should expect an output like `Listing products...`

when you run the above command

```
kubectl exec -it <your-http-client-pod-name> -n default -- curl -v -XPOST http://http-server:80/products -d "test=data"
```


You should expect an output like `Access Denied`

when you run the above command

### Observing L7 metrics

If you have Advanced Container Network Service's container network observability enabled, you can visualize the traffic on Grafana.

To simplify the analysis of these L7 metrics, we provide preconfigured Azure Managed Grafana dashboards. You can find them under the **Dashboards > Azure Managed Prometheus** folder, with filenames like **"Kubernetes/Networking/L7 (Namespace)"** and **"Kubernetes/Networking/L7 (Workload)"**.

You should see metrics similar to the following:

## Clean up resources

If you don't plan on using this application, delete the other resources you created in this article using the [ az group delete](/en-us/cli/azure/#az-group-delete) command.

```
az group delete --name $RESOURCE_GROUP
```


## Next steps

In this how-to article, you learned how to enable and apply L7 Policies with Advanced Container Networking Services for your AKS cluster.

- For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see
[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/confidential-containers-overview -->

# Confidential Containers (preview) with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Confidential Containers preview is set to sunset in **March 2026**. After this date, customers with existing Confidential Container node pools should expect to see reduced functionality, and you won't be able to spin up any new nodes with the `KataCcIsolation`

runtime. Customers currently using Confidential Container node pools can continue using them as normal. If you want to move off Confidential Containers, consider the following alternatives:

[Confidential VMs on AKS](/en-us/azure/confidential-computing/confidential-node-pool-aks): Offers a similar hardware-based TEE that leverages AMD SEV-SNP security features, without the addition of per-VM isolation for workloads seen in Confidential Containers.[Application enclave support](/en-us/azure/confidential-computing/confidential-nodes-aks-overview): Provides users with Intel SGX confidential computing VM nodes that support hardware-based, process-level container isolation through the Intel SGX trusted execution environment.[Confidential Containers on Azure Container Instances](/en-us/azure/confidential-computing/confidential-containers): Allows for lift-and-shift deployments on containers backed by AMD SEV-SNP. Functionality includes performing full guest attestation, access to toolings to generate policies, and utilizing sidecar containers for secure key releases. ACI nodes can be run on AKS via[virtual nodes](/en-us/azure/container-instances/container-instances-virtual-nodes).[Azure RedHat OpenShift Confidential Containers](/en-us/azure/openshift/confidential-containers-overview): Offers a similar AMD SEV-SNP backed TEE and utilizes the Kata runtime for per-container level isolation.[Open source Confidential Containers](https://github.com/confidential-containers): Gives a similar AMD SEV-SNP backed TEE that comes with per-container isolation through Kata.

If you have additional questions, please create a [support request](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest) or post an issue in [AKS issues](https://github.com/Azure/AKS/issues).

Confidential Containers provide a set of features and capabilities to further secure your standard container workloads to achieve higher data security, data privacy and runtime code integrity goals. Azure Kubernetes Service (AKS) includes Confidential Containers (preview) on AKS.

Confidential Containers builds on Kata Confidential Containers and hardware-based encryption to encrypt container memory. It establishes a new level of data confidentiality by preventing data in memory during computation from being in clear text, readable format. Trust is earned in the container through hardware attestation, allowing access to the encrypted data by trusted entities.

Together with [Pod Sandboxing](use-pod-sandboxing), you can run sensitive workloads isolated in Azure to protect your data and workloads. What makes a container confidential:

- Transparency: The confidential container environment where your sensitive application is shared, you can see and verify if it's safe. All components of the Trusted Computing Base (TCB) are to be open sourced.
- Auditability: You have the ability to verify and see what version of the CoCo environment package including Linux Guest OS and all the components are current. Microsoft signs to the guest OS and container runtime environment for verifications through attestation. It also releases a secure hash algorithm (SHA) of guest OS builds to build a string audibility and control story.
- Full attestation: Anything that is part of the TEE shall be fully measured by the CPU with ability to verify remotely. The hardware report from AMD SEV-SNP processor shall reflect container layers and container runtime configuration hash through the attestation claims. Application can fetch the hardware report locally including the report that reflects Guest OS image and container runtime.
- Code integrity: Runtime enforcement is always available through customer defined policies for containers and container configuration, such as immutable policies and container signing.
- Isolation from operator: Security designs that assume least privilege and highest isolation shielding from all untrusted parties including customer/tenant admins. It includes hardening existing Kubernetes control plane access (kubelet) to confidential pods.

With other security measures or data protection controls, as part of your overall architecture, these capabilities help you meet regulatory, industry, or governance compliance requirements for securing sensitive information.

This article helps you understand the Confidential Containers feature, and how to implement and configure the following:

- Deploy or upgrade an AKS cluster using the Azure CLI
- Add an annotation to your pod YAML to mark the pod as being run as a confidential container
- Add a
[security policy](/en-us/azure/confidential-computing/confidential-containers-aks-security-policy)to your pod YAML - Deploy your application in confidential computing

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Supported scenarios

Confidential Containers (preview) are appropriate for deployment scenarios that involve sensitive data. For example, personally identifiable information (PII) or any data with strong security needed for regulatory compliance. Some common scenarios with containers are:

- Run big data analytics using Apache Spark for fraud pattern recognition in the financial sector.
- Running self-hosted GitHub runners to securely sign code as part of Continuous Integration and Continuous Deployment (CI/CD) DevOps practices.
- Machine Learning inferencing and training of ML models using an encrypted data set from a trusted source. It only decrypts inside a confidential container environment to preserve privacy.
- Building big data clean rooms for ID matching as part of multi-party computation in industries like retail with digital advertising.
- Building confidential computing Zero Trust landing zones to meet privacy regulations for application migrations to cloud.

## Considerations

The following are considerations with this preview of Confidential Containers:

- An increase in pod startup time compared to runc pods and kernel-isolated pods.
- Version 1 container images aren't supported.
- Ephemeral containers and other troubleshooting methods like
`exec`

into a container, log outputs from containers, and`stdio`

require a policy modification and redeployment to enable ExecProcessRequest, ReadStreamRequest, WriteStreamRequest, and CloseStdinRequest. - Due to container image layer measurements being encoded in the security policy, we don't recommend using the
`latest`

tag when specifying containers. - Services, Load Balancers, and EndpointSlices only support the TCP protocol.
- The policy generator only supports pods that use IPv4 addresses.
- Pod environment variables based on ConfigMaps and Secrets can't be changed after the pod is deployed.
- Pod termination logs aren't supported. While pods write termination logs to
`/dev/termination-log`

or to a custom location if specified in the pod manifest, the host/kubelet can't read those logs. Changes from the pod to that file aren't reflected on the host. - Confidential Containers currently only supports Azure Linux.

## Resource allocation overview

It's important you understand the memory and processor resource allocation behavior in this release.

- CPU: The shim assigns one vCPU to the base OS inside the pod. If no resource
`limits`

are specified, the workloads don't have separate CPU shares assigned, the vCPU is then shared with that workload. If CPU limits are specified, CPU shares are explicitly allocated for workloads. - Memory: The Kata-CC handler uses 2 GB memory for the UVM OS and X MB additional memory where X is the resource
`limits`

if specified in the YAML manifest (resulting in a 2-GB VM when no limit is given, without implicit memory for containers). The[Kata](https://katacontainers.io/docs/)handler uses 256 MB base memory for the UVM OS and X MB additional memory when resource`limits`

are specified in the YAML manifest. If limits are unspecified, an implicit limit of 1,792 MB is added resulting in a 2 GB VM and 1,792 MB implicit memory for containers.

In this release, specifying resource requests in the pod manifests isn't supported. containerd doesn't pass the requests to the Kata Shim, and as a result, reserving resources based on the pod manifest resource requests is not implemented. Use resource `limits`

instead of resource `requests`

to allocate memory or CPU resources for workloads or containers.

With the local container filesystem backed by VM memory, writing to the container filesystem (including logging) can fill up the available memory provided to the pod. This condition can result in potential pod crashes.

## Next steps

- See the overview of
[Confidential Containers security policy](/en-us/azure/confidential-computing/confidential-containers-aks-security-policy)to learn about how workloads and their data in a pod is protected. [Deploy Confidential Containers on AKS](deploy-confidential-containers-default-policy)with an automatically generated security policy.- Learn more about
[Azure Dedicated hosts](/en-us/azure/virtual-machines/dedicated-hosts)for nodes with your AKS cluster to use hardware isolation and control over Azure platform maintenance events.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/configure-kubenet -->

# Use kubenet networking with your own IP address ranges in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

On **31 March 2028**, kubenet networking for Azure Kubernetes Service (AKS) will be retired.

To avoid service disruptions, **you'll need to** [upgrade to Azure Container Networking Interface (CNI) overlay](/en-us/azure/aks/upgrade-aks-ipam-and-dataplane#upgrade-an-existing-cluster-to-azure-cni-overlay) **before that date**, when workloads running on kubenet for AKS will no longer be supported.

AKS clusters use kubenet and create an Azure virtual network and subnet for you by default. With kubenet, nodes get an IP address from the Azure virtual network subnet. Pods receive an IP address from a logically different address space to the Azure virtual network subnet of the nodes. Network address translation (NAT) is then configured so the pods can reach resources on the Azure virtual network. The source IP address of the traffic is NAT'd to the node's primary IP address. This approach greatly reduces the number of IP addresses you need to reserve in your network space for pods to use.

With [Azure Container Networking Interface (CNI)](https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md), every pod gets an IP address from the subnet and can be accessed directly. These IP addresses must be planned in advance and unique across your network space. Each node has a configuration parameter for the maximum number of pods it supports. The equivalent number of IP addresses per node are then reserved up front for that node. This approach requires more planning, and often leads to IP address exhaustion or the need to rebuild clusters in a larger subnet as your application demands grow. You can configure the maximum pods deployable to a node at cluster creation time or when creating new node pools. If you don't specify `maxPods`

when creating new node pools, you receive a default value of *110* for kubenet.

This article shows you how to use kubenet networking to create and use a virtual network subnet for an AKS cluster. For more information on network options and considerations, see [Network concepts for Kubernetes and AKS](concepts-network).

## Prerequisites

- The virtual network for the AKS cluster must allow outbound internet connectivity.
- Don't create more than one AKS cluster in the same subnet.
- AKS clusters can't use
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

for the Kubernetes service address range, pod address range, or cluster virtual network address range. The range can't be updated after you create your cluster. - The cluster identity used by the AKS cluster must at least have the
[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)role on the subnet within your virtual network. CLI helps set the role assignment automatically. If you're using an ARM template or other clients, you need to manually set the role assignment. You must also have the appropriate permissions, such as the subscription owner, to create a cluster identity and assign it permissions. If you want to define a[custom role](/en-us/azure/role-based-access-control/custom-roles)instead of using the built-in Network Contributor role, you need the following permissions:`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Network/virtualNetworks/subnets/read`


Warning

To use Windows Server node pools, you must use Azure CNI. The kubenet network model isn't available for Windows Server containers.

## Before you begin

You need the Azure CLI version 2.0.65 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Overview of kubenet networking with your own subnet

In many environments, you have defined virtual networks and subnets with allocated IP address ranges, and you use these resources to support multiple services and applications. To provide network connectivity, AKS clusters can use *kubenet* (basic networking) or Azure CNI (*advanced networking*).

With *kubenet*, only the nodes receive an IP address in the virtual network subnet. Pods can't communicate directly with each other. Instead, User Defined Routing (UDR) and IP forwarding handle connectivity between pods across nodes. UDRs and IP forwarding configuration is created and maintained by the AKS service by default, but you can [bring your own route table for custom route management](#bring-your-own-subnet-and-route-table-with-kubenet) if you want. You can also deploy pods behind a service that receives an assigned IP address and load balances traffic for the application. The following diagram shows how the AKS nodes receive an IP address in the virtual network subnet, but not the pods:

Azure supports a maximum of *400* routes in a UDR, so you can't have an AKS cluster larger than 400 nodes. AKS [virtual nodes](virtual-nodes-cli) and Azure Network Policies aren't supported with *kubenet*. [Calico Network Policies](https://docs.projectcalico.org/v3.9/security/calico-network-policy) are supported.

With *Azure CNI*, each pod receives an IP address in the IP subnet and can communicate directly with other pods and services. Your clusters can be as large as the IP address range you specify. However, you must plan the IP address range in advance, and all the IP addresses are consumed by the AKS nodes based on the maximum number of pods they can support. Advanced network features and scenarios such as [virtual nodes](virtual-nodes-cli) or Network Policies (either Azure or Calico) are supported with *Azure CNI*.

### Limitations & considerations for kubenet

- An additional hop is required in the design of kubenet, which adds minor latency to pod communication.
- Route tables and user-defined routes are required for using kubenet, which adds complexity to operations.
- For more information, see
[Customize cluster egress with a user-defined routing table in AKS](egress-udr)and[Customize cluster egress with outbound types in AKS](egress-outboundtype).

- For more information, see
- Direct pod addressing isn't supported for kubenet due to kubenet design.
- Unlike Azure CNI clusters, multiple kubenet clusters can't share a subnet.
- AKS doesn't apply Network Security Groups (NSGs) to its subnet and doesn't modify any of the NSGs associated with that subnet. If you provide your own subnet and add NSGs associated with that subnet, you must ensure the security rules in the NSGs allow traffic between the node and pod CIDR. For more details, see
[Network security groups](concepts-network#network-security-groups). - Features
**not supported on kubenet**include:

Note

Some of the system pods such as **konnectivity** within the cluster use the host node IP address rather than an IP from the overlay address space. The system pods will only use the node IP and not an IP address from the virtual network.

### IP address availability and exhaustion

A common issue with *Azure CNI* is that the assigned IP address range is too small to then add more nodes when you scale or upgrade a cluster. The network team also might not be able to issue a large enough IP address range to support your expected application demands.

As a compromise, you can create an AKS cluster that uses *kubenet* and connect to an existing virtual network subnet. This approach lets the nodes receive defined IP addresses without the need to reserve a large number of IP addresses up front for any potential pods that could run in the cluster. With *kubenet*, you can use a much smaller IP address range and support large clusters and application demands. For example, with a */27* IP address range on your subnet, you can run a 20-25 node cluster with enough room to scale or upgrade. This cluster size can support up to *2,200-2,750* pods (with a default maximum of 110 pods per node). The maximum number of pods per node that you can configure with *kubenet* in AKS is 250.

The following basic calculations compare the difference in network models:

**kubenet**: A simple*/24*IP address range can support up to*251*nodes in the cluster. Each Azure virtual network subnet reserves the first three IP addresses for management operations. This node count can support up to*27,610*pods, with a default maximum of 110 pods per node.**Azure CNI**: That same basic*/24*subnet range can only support a maximum of*eight*nodes in the cluster. This node count can only support up to*240*pods, with a default maximum of 30 pods per node.

Note

These maximums don't take into account upgrade or scale operations. In practice, you can't run the maximum number of nodes the subnet IP address range supports. You must leave some IP addresses available for scaling or upgrading operations.

### Virtual network peering and ExpressRoute connections

To provide on-premises connectivity, both *kubenet* and *Azure-CNI* network approaches can use [Azure virtual network peering](/en-us/azure/virtual-network/virtual-network-peering-overview) or [ExpressRoute connections](/en-us/azure/expressroute/expressroute-introduction). Plan your IP address ranges carefully to prevent overlap and incorrect traffic routing. For example, many on-premises networks use a *10.0.0.0/8* address range that's advertised over the ExpressRoute connection. We recommend creating your AKS clusters in Azure virtual network subnets outside this address range, such as *172.16.0.0/16*.

### Choose a network model to use

The following considerations help outline when each network model may be the most appropriate:

**Use kubenet when**:

- You have limited IP address space.
- Most of the pod communication is within the cluster.
- You don't need advanced AKS features, such as virtual nodes or Azure Network Policy.

**Use Azure CNI when**:

- You have available IP address space.
- Most of the pod communication is to resources outside of the cluster.
- You don't want to manage user defined routes for pod connectivity.
- You need AKS advanced features, such as virtual nodes or Azure Network Policy.

For more information to help you decide which network model to use, see [Compare network models and their support scope](concepts-network-cni-overview).

## Create a virtual network and subnet

Create a resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus`

If you don't have an existing virtual network and subnet to use, create these network resources using the

command. The following example command creates a virtual network named`az network vnet create`

*myAKSVnet*with the address prefix of*192.168.0.0/16*and a subnet named*myAKSSubnet*with the address prefix*192.168.1.0/24*:`az network vnet create \ --resource-group myResourceGroup \ --name myAKSVnet \ --address-prefixes 192.168.0.0/16 \ --subnet-name myAKSSubnet \ --subnet-prefix 192.168.1.0/24 \ --location eastus`

Get the subnet resource ID using the

command and store it as a variable named`az network vnet subnet show`

`SUBNET_ID`

for later use.`SUBNET_ID=$(az network vnet subnet show --resource-group myResourceGroup --vnet-name myAKSVnet --name myAKSSubnet --query id -o tsv)`


## Create an AKS cluster in the virtual network

### Create an AKS cluster with system-assigned managed identities

Note

When using system-assigned identity, the Azure CLI grants the Network Contributor role to the system-assigned identity after the cluster is created. If you're using an ARM template or other clients, you need to use the [user-assigned managed identity](configure-kubenet#create-an-aks-cluster-with-user-assigned-managed-identity) instead.

Create an AKS cluster with system-assigned managed identities using the

command.`az aks create`

`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --network-plugin kubenet \ --service-cidr 10.0.0.0/16 \ --dns-service-ip 10.0.0.10 \ --pod-cidr 10.244.0.0/16 \ --vnet-subnet-id $SUBNET_ID \ --generate-ssh-keys`

Deployment parameters:

*--service-cidr*is optional. This address is used to assign internal services in the AKS cluster an IP address. This IP address range should be an address space that isn't in use elsewhere in your network environment, including any on-premises network ranges if you connect, or plan to connect, your Azure virtual networks using Express Route or a Site-to-Site VPN connection. The default value is 10.0.0.0/16.*--dns-service-ip*is optional. The address should be the*.10*address of your service IP address range. The default value is 10.0.0.10.*--pod-cidr*is optional. This address should be a large address space that isn't in use elsewhere in your network environment. This range includes any on-premises network ranges if you connect, or plan to connect, your Azure virtual networks using Express Route or a Site-to-Site VPN connection. The default value is 10.244.0.0/16.- This address range must be large enough to accommodate the number of nodes that you expect to scale up to. You can't change this address range once the cluster is deployed.
- The pod IP address range is used to assign a
*/24*address space to each node in the cluster. In the following example, the*--pod-cidr*of*10.244.0.0/16*assigns the first node*10.244.0.0/24*, the second node*10.244.1.0/24*, and the third node*10.244.2.0/24*. - As the cluster scales or upgrades, the Azure platform continues to assign a pod IP address range to each new node.


### Create an AKS cluster with user-assigned managed identity

#### Create a managed identity

Create a managed identity using the

command. If you have an existing managed identity, find the principal ID using the`az identity`

`az identity show --ids <identity-resource-id>`

command instead.`az identity create --name myIdentity --resource-group myResourceGroup`

Your output should resemble the following example output:

`{ "clientId": "<client-id>", "clientSecretUrl": "<clientSecretUrl>", "id": "/subscriptions/<subscriptionid>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/myIdentity", "location": "westus2", "name": "myIdentity", "principalId": "<principal-id>", "resourceGroup": "myResourceGroup", "tags": {}, "tenantId": "<tenant-id>", "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`


#### Add role assignment for managed identity

If you're using the Azure CLI, the role is automatically added and you can skip this step. If you're using an ARM template or other clients, you need to use the Principal ID of the cluster managed identity to perform a role assignment.

Get the virtual network resource ID using the

command and store it as a variable named`az network vnet show`

`VNET_ID`

.`VNET_ID=$(az network vnet show --resource-group myResourceGroup --name myAKSVnet --query id -o tsv)`

Assign the managed identity for your AKS cluster

*Network Contributor*permissions on the virtual network using thecommand and provide the`az role assignment create`

*<principalId>*.`az role assignment create --assignee <control-plane-identity-principal-id> --scope $VNET_ID --role "Network Contributor" # Example command az role assignment create --assignee 22222222-2222-2222-2222-222222222222 --scope "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myAKSVnet" --role "Network Contributor"`


Note

Permission granted to your cluster's managed identity used by Azure may take up 60 minutes to populate.

#### Create an AKS cluster

Create an AKS cluster using the

command and provide the control plane's managed identity resource ID for the`az aks create`

`assign-identity`

argument to assign the user-assigned managed identity.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --node-count 3 \ --network-plugin kubenet \ --vnet-subnet-id $SUBNET_ID \ --assign-identity <identity-resource-id> \ --generate-ssh-keys`


When you create an AKS cluster, a network security group and route table are automatically created. These network resources are managed by the AKS control plane. The network security group is automatically associated with the virtual NICs on your nodes. The route table is automatically associated with the virtual network subnet. Network security group rules and route tables are automatically updated as you create and expose services.

## Bring your own subnet and route table with kubenet

With kubenet, a route table must exist on your cluster subnet(s). AKS supports bringing your own existing subnet and route table. If your custom subnet doesn't contain a route table, AKS creates one for you and adds rules throughout the cluster lifecycle. If your custom subnet contains a route table when you create your cluster, AKS acknowledges the existing route table during cluster operations and adds/updates rules accordingly for cloud provider operations.

Warning

You can add/update custom rules on the custom route table. However, rules are added by the Kubernetes cloud provider which can't be updated or removed. Rules such as *0.0.0.0/0* generally exist on a given route table (unless the egress outbound type is `none`

) and map to the target of your internet gateway, such as an NVA or other egress gateway. Take caution when updating rules.

Learn more about setting up a [custom route table](/en-us/azure/virtual-network/manage-route-table).

Kubenet networking requires organized route table rules to successfully route requests. Due to this design, route tables must be carefully maintained for each cluster that relies on it. Multiple clusters can't share a route table because pod CIDRs from different clusters might overlap which causes unexpected and broken routing scenarios. When configuring multiple clusters on the same virtual network or dedicating a virtual network to each cluster, consider the following limitations:

- A custom route table must be associated to the subnet before you create the AKS cluster.
- The associated route table resource can't be updated after cluster creation. However, custom rules can be modified on the route table.
- Each AKS cluster must use a single, unique route table for all subnets associated with the cluster. You can't reuse a route table with multiple clusters due to the potential for overlapping pod CIDRs and conflicting routing rules.
- For system-assigned managed identity, it's only supported to provide your own subnet and route table via Azure CLI because Azure CLI automatically adds the role assignment. If you're using an ARM template or other clients, you must use a
[user-assigned managed identity](configure-kubenet#create-an-aks-cluster-with-user-assigned-managed-identity), assign permissions before cluster creation, and ensure the user-assigned identity has write permissions to your custom subnet and custom route table. - Using the same route table with multiple AKS clusters isn't supported.

Note

When you create and use your own VNet and route table with the kubenet network plugin, you must configure a [user-assigned managed identity](use-managed-identity#create-a-user-assigned-managed-identity) for the cluster. With a system-assigned managed identity, you can't retrieve the identity ID before creating a cluster, which causes a delay during role assignment.

Both system-assigned and user-assigned managed identities are supported when you create and use your own VNet and route table with the Azure network plugin. We highly recommend using a user-assigned managed identity for BYO scenarios.

### Add a route table with a user-assigned managed identity to your AKS cluster

After creating a custom route table and associating it with a subnet in your virtual network, you can create a new AKS cluster specifying your route table with a user-assigned managed identity. You need to use the subnet ID for where you plan to deploy your AKS cluster. This subnet also must be associated with your custom route table.

Get the subnet ID using the

command.`az network vnet subnet list`

`az network vnet subnet list --resource-group myResourceGroup --vnet-name myAKSVnet [--subscription]`

Create an AKS cluster with a custom subnet pre-configured with a route table using the

command and providing your values for the`az aks create`

`--vnet-subnet-id`

and`--assign-identity`

parameters.`az aks create \ --resource-group myResourceGroup \ --name myManagedCluster \ --vnet-subnet-id mySubnetIDResourceID \ --assign-identity controlPlaneIdentityResourceID \ --generate-ssh-keys`


## Next steps

This article showed you how to deploy your AKS cluster into your existing virtual network subnet. Now, you can start [creating new apps using Helm](quickstart-helm) or [deploying existing apps using Helm](kubernetes-helm).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/migrate-from-npm-to-cilium-network-policy -->

# Migrate from Network Policy Manager (NPM) to Cilium Network Policy

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, we provide a comprehensive guide to plan, execute, and validate the migration from Network Policy Manager (NPM) to Cilium Network Policy. The goal is to ensure policy parity, minimize service disruption, and align with Azure CNI's strategic direction toward eBPF-based networking and enhanced observability.

Important

This guide applies exclusively to AKS clusters running Linux nodes. Cilium Network Policy isn't currently supported for Windows nodes in AKS.

## Key considerations before you begin

- Policy Compatibility: NPM and Cilium differ in enforcement models. Before migration you need to validate that existing policies are compatible or identify required changes. Refer to the Pre-Migration Validation section for guidance.
- Downtime Expectations: Policy enforcement might be temporarily inconsistent during node reimaging.
- Windows Node Pools: Cilium Network Policy isn't currently supported for Windows nodes in AKS.

## Pre-migration validation

Before migrating from Network Policy Manager (NPM) to Cilium Network Policy, it's important to assess the compatibility of your existing network policies. While most policies continue to function as expected post-migration, there are specific scenarios where behavior might differ between NPM and Cilium. These differences could require updates to your policies either before or after the migration to ensure consistent enforcement and avoid unintended traffic drops. In this section, we outline known scenarios where policy adjustments might be necessary. We explain why it matters, and provide guidance on what actions—if any—are required to make your policies Cilium-compatible.

### NetworkPolicy with endPort

Note

Cilium started supporting the `endPort`

field in Kubernetes NetworkPolicy in version 1.17.

The endPort field allows you to define a range of ports in a single rule, rather than specifying individual ports.

Here's an example of a Kubernetes NetworkPolicy that uses the endPort field:

```
egress:
- to:
- ipBlock:
cidr: 10.0.0.0/24
ports:
- protocol: TCP
port: 32000
endPort: 32768
```


**Action Required:**

- If your AKS cluster is running Cilium version 1.17 or later, no changes are needed as endPort is fully supported.
- If your cluster is running a Cilium version earlier than 1.17, remove the endPort field from any policies before migrating. Use explicit single-port entries instead.

### NetworkPolicy with ipBlock

The ipBlock field in Kubernetes NetworkPolicy allows you to define CIDR ranges for ingress sources or egress destinations. These ranges can include external IPs, Pod IPs, or Node IPs. However, Cilium doesn't allow egress to Pod or Node IPs using ipBlock, even if those IPs fall within the specified CIDR range.

For example, the following NetworkPolicy uses an ipBlock to allow all egress traffic to 0.0.0.0/0:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: example-ipblock
spec:
podSelector: {}
policyTypes:
- Egress
egress:
- to:
- ipBlock:
cidr: 0.0.0.0/0
```


- Under NPM, this policy would allow egress to all destinations, including Pods and Nodes.
- After migrating to Cilium, egress to Pod and Node IPs will be blocked, even though they fall within the 0.0.0.0/0 range.

**Action Required:**

- To allow traffic to Pod IPs, before migration replace the ipBlock with a combination of namespaceSelector and podSelector.

Here's an example of using namespaceSelector and podSelector:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: example-ipblock
spec:
podSelector: {}
policyTypes:
- Egress
egress:
- to:
- ipBlock:
cidr: 0.0.0.0/0
- namespaceSelector: {}
- podSelector: {}
```


- For Node IPs, there's no pre-migration workaround. After migration, you must create a CiliumNetworkPolicy that explicitly allows egress to the host and/or remote-node entities. Until this policy is in place, egress traffic to Node IPs is blocked.

Here's an example of CiliumNetworkPolicy to allow traffic from/to local and remote nodes:

```
apiVersion: "cilium.io/v2"
kind: CiliumNetworkPolicy
metadata:
name: allow-node-egress
namespace: ipblock-test
spec:
endpointSelector: {} # Applies to all pods in the namespace
egress:
- toEntities:
- host # host allows traffic from/to the local node's host network namespace
- remote-node # remote-node allows traffic from/to the remote node's host network namespace
```


### NetworkPolicy with named Ports

Kubernetes NetworkPolicy allows you to reference ports by name instead of number. If you're using named ports in your NetworkPolicies, Cilium might fail to enforce rules correctly and lead to unexpected traffic being blocked. This issue happens when the same port name is used for different ports.
For more information, see [Cilium GitHub issue #30003](https://github.com/cilium/cilium/issues/30003).

Here's an example of NetworkPolicy uses Named port to allow egress traffic:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
annotations:
name: allow-egress
namespace: default
spec:
podSelector:
matchLabels:
network-rules-egress: cilium-np-test
egress:
- ports:
- port: http-test # Named port
protocol: TCP
policyTypes:
- Egress
```


**Action Required:**

- Before migration, replace all named ports in your policies with their corresponding numeric values.

### NetworkPolicy with Egress Policies

Kubernetes NetworkPolicy on NPM doesn't block egress traffic from a pod to its own node's IP, this traffic is implicitly allowed. After you migrate to Cilium, this behavior will change, and traffic to local nodes that was previously allowed will be blocked unless explicitly allowed.

For example, the following policy allows egress only to an internal API subnet:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: allow-egress
namespace: default
spec:
podSelector: {}
policyTypes:
- Egress
egress:
- to:
- ipBlock:
cidr: 10.20.30.0/24
```


- With NPM: Egress traffic to 10.20.30.0/24 is allowed explicitly, and egress traffic to the local node is allowed implicitly.
- With Cilium: Only traffic to 10.20.30.0/24 is allowed; egress to the node IP is blocked unless you permit it explicitly.

**Action Required:**

- Review all existing egress policies for your workloads.
- If your applications rely on NPM's implicit allow behavior for egress to the local node, you must add explicit egress rules to maintain connectivity after migration.
- You can add a CiliumNetworkPolicy after migration to explicitly allow egress traffic to the local host.

### Ingress policy behavior changes

Under Network Policy Manager (NPM), ingress traffic arriving via a LoadBalancer or NodePort service with "externalTrafficPolicy=Cluster" - which is the default setting - isn't subject to ingress policy enforcement. This behavior means that even if a pod has a restrictive ingress policy, traffic from external sources might still reach it via loadbalancer or nodeport services.

In contrast, Cilium enforces ingress policies on all traffic, including traffic routed internally due to externalTrafficPolicy=Cluster. As a result, after migration, traffic that was previously allowed might be dropped if the appropriate ingress rules aren't explicitly defined.

For example, Customer creates a network policy to deny all in ingress traffic

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: default-deny-ingress
spec:
podSelector: {}
policyTypes:
- Ingress
```


- With NPM: Direct connection to the pod or via ClusterIP service is blocked. However, access through NodePort or LoadBalancer is still allowed despite the deny-all policy.
- With Cilium: All ingress traffic is blocked, including traffic via NodePort or LoadBalancer, unless explicitly allowed.

**Action Required:**

- Review all ingress policies for workloads behind LoadBalancer or NodePort services using externalTrafficPolicy=Cluster.
- Ensure that ingress rules explicitly allow traffic from the expected external sources (for example, IP ranges, namespaces, or labels).
- If your policy currently relies on the implicit allow behavior under NPM, you must add explicit ingress rules to maintain connectivity after migration.

## Upgrade to Azure CNI Powered by Cilium

To use Cilium Network Policy, your AKS cluster must be running Azure CNI powered by Cilium. When you enable Cilium in a cluster currently using NPM, the existing NPM engine is automatically uninstalled and replaced with Cilium.

Warning

The upgrade process triggers each node pool to be reimaged simultaneously. Upgrading each node pool separately isn't supported. Any disruptions to cluster networking are similar to a node image upgrade or [Kubernetes version upgrade](upgrade-cluster) where each node in a node pool is reimaged. Cilium will begin enforcing network policies only after all nodes are reimaged.

Important

These instructions apply to clusters upgrading from Azure CNI to Azure CNI with the Cilium dataplane. Upgrades from bring-your-own CNIs or changes the IPAM mode aren't covered here. For more information, see [Upgrade Azure CNI documentation](update-azure-cni).

To perform the upgrade, you need Azure CLI version 2.52.0 or later. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Use the following command to upgrade an existing cluster to Azure CNI Powered by Cilium. Replace the values for `clusterName`

and `resourceGroupName`

:

```
az aks update --name <clusterName> --resource-group <resourceGroupName> --network-dataplane cilium
```


## Next steps

For more information about using Cilium FQDN network policy on AKS, see

[Set up FQDN filtering feature for Container Network Security in Advanced Container Networking Services](how-to-apply-fqdn-filtering-policies).For more information about using Cilium L7 network policy on AKS, see

[Set up Layer 7(L7) policies with Advanced Container Networking Services](how-to-apply-l7-policies).For more information about network policy best practices on aks, see

[Best practices for network policies in Azure Kubernetes Service (AKS)](network-policy-best-practices)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/core-aks-concepts -->

# Core concepts for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes core concepts of Azure Kubernetes Service (AKS), a managed Kubernetes service that you can use to deploy and operate containerized applications at scale on Azure.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## What is Kubernetes?

Kubernetes is an open-source container orchestration platform for automating the deployment, scaling, and management of containerized applications. For more information, see the official [Kubernetes documentation](https://kubernetes.io/docs/home/).

## What is AKS?

AKS is a managed Kubernetes service that simplifies deploying, managing, and scaling containerized applications that use Kubernetes. For more information, see [What is Azure Kubernetes Service (AKS)?](what-is-aks).

## Cluster components

An AKS cluster is divided into two main components:

**Control plane**: The control plane provides the core Kubernetes services and orchestration of application workloads.**Nodes**: Nodes are the underlying virtual machines (VMs) that run your applications.

Note

AKS managed components have the label `kubernetes.azure.com/managedby`

: `aks`

.

AKS manages the Helm releases with the prefix `aks-managed`

. Continuously increasing revisions on these releases are expected and safe.

### Control plane

The Azure managed control plane is composed of several components that help manage the cluster:

| Component | Description |
|---|---|
`kube-apiserver` |
The API server (
|

`etcd`

[etcd](https://kubernetes.io/docs/concepts/overview/components/#etcd)helps to maintain the state of your Kubernetes cluster and configuration.`kube-scheduler`

[kube-scheduler](https://kubernetes.io/docs/concepts/overview/components/#kube-scheduler)) helps to make scheduling decisions. It watches for new pods with no assigned node and selects a node for them to run on.`kube-controller-manager`

[kube-controller-manager](https://kubernetes.io/docs/concepts/overview/components/#kube-controller-manager)) runs controller processes, such as noticing and responding when nodes go down.`cloud-controller-manager`

[cloud-controller-manager](https://kubernetes.io/docs/concepts/overview/components/#cloud-controller-manager)) embeds cloud-specific control logic to run controllers specific to the cloud provider.### Nodes

Each AKS cluster has at least one node, which is an Azure VM that runs Kubernetes node components. The following components run on each node:

| Component | Description |
|---|---|
`kubelet` |
The
|

`kube-proxy`

[kube-proxy](https://kubernetes.io/docs/concepts/overview/components/#kube-proxy)is a network proxy that maintains network rules on nodes.`container runtime`

[container runtime](https://kubernetes.io/docs/concepts/overview/components/#container-runtime)manages the execution and lifecycle of containers.## Node configuration

Configure the following settings for nodes.

### VM size and image

The *Azure VM size* for your nodes defines CPUs, memory, size, and the storage type available, such as a high-performance solid-state drive or a regular hard-disk drive. The VM size you choose depends on the workload requirements and the number of pods that you plan to run on each node. As of May 2025, the default VM SKU and size will be dynamically selected by AKS based on available capacity and quota if the parameter is left blank during deployment. For more information, see [Supported VM sizes in Azure Kubernetes Service (AKS)](quotas-skus-regions#supported-vm-sizes).

In AKS, the *VM image* for your cluster's nodes is based on Ubuntu Linux, [Azure Linux](use-azure-linux), or Windows Server 2022. When you create an AKS cluster or scale out the number of nodes, the Azure platform automatically creates and configures the requested number of VMs. Agent nodes are billed as standard VMs. Any VM size discounts, including [Azure reservations](/en-us/azure/cost-management-billing/reservations/save-compute-costs-reservations), are automatically applied.

### OS disks

Default OS disk sizing is used on new clusters or node pools only when a default OS disk size isn't specified. This behavior applies to both managed and ephemeral OS disks. For more information, see [Default OS disk sizing](concepts-storage#default-os-disk-sizing).

### Resource reservations

AKS uses node resources to help the nodes function as part of the cluster. This usage can cause a discrepancy between the node's total resources and the allocatable resources in AKS. To maintain node performance and functionality, AKS reserves two types of resources, CPU and memory, on each node. For more information, see [Resource reservations in AKS](node-resource-reservations).

### OS

AKS supports two linux distros: Ubuntu and Azure Linux. Ubuntu is the default Linux distro on AKS. Windows node pools are also supported on AKS with the [Long Term Servicing Channel (LTSC)](/en-us/windows-server/get-started/servicing-channels-comparison) as the default channel on AKS. For more information on default OS versions, see documentation on [node images](node-images).

### Container runtime

A container runtime is software that executes containers and manages container images on a node. The runtime helps abstract away system calls or OS-specific functionality to run containers on Linux or Windows. For Linux node pools, [containerd](https://containerd.io/) is used on Kubernetes version 1.19 and higher. For Windows Server 2019 and 2022 node pools, [containerd](https://containerd.io/) is generally available and is the only runtime option on Kubernetes version 1.23 and higher.

## Pods

A *pod* is a group of one or more containers that share the same network and storage resources and a specification for how to run the containers. Pods typically have a 1:1 mapping with a container, but you can run multiple containers in a pod.

## Node pools

In AKS, nodes of the same configuration are grouped together into *node pools*. These node pools contain the underlying virtual machine scale sets and virtual machines (VMs) that run your applications.

When you create an AKS cluster, you define the initial number of nodes and their size (version), which creates a [system node pool](use-system-pools). System node pools serve the primary purpose of hosting critical system pods, such as CoreDNS and `konnectivity`

.

To support applications that have different compute or storage demands, you can create *user node pools*. User node pools serve the primary purpose of hosting your application pods.

For more information, see [Create node pools in AKS](create-node-pools) and [Manage node pools in AKS](manage-node-pools).

## Node resource group

When you create an AKS cluster in an Azure resource group, the AKS resource provider automatically creates a second resource group called the *node resource group*. This resource group contains all the infrastructure resources associated with the cluster, including VMs, virtual machine scale sets, and storage.

For more information, see the following resources:

[Why are two resource groups created with AKS?](faq)[Can I provide my own name for the AKS node resource group?](faq)[Can I modify tags and other properties of the resources in the AKS node resource group?](faq)

## Namespaces

Kubernetes resources, such as pods and deployments, are logically grouped into *namespaces* to divide an AKS cluster and create, view, or manage access to resources.

The following namespaces are created by default in an AKS cluster:

| Namespace | Description |
|---|---|
`default` |
The
|

`kube-node-lease`

[kube-node-lease](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace enables nodes to communicate their availability to the control plane.`kube-public`

[kube-public](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace isn't typically used, but you can use it so that resources are visible across the whole cluster by any user.`kube-system`

[kube-system](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace is used by Kubernetes to manage cluster resources, such as`coredns`

, `konnectivity-agent`

, and `metrics-server`

. It is not recommended to deploy your own applications to this namespace. For rare cases where deploying your own applications to this namespace is necessary, see the [FAQ](faq#can-admission-controller-webhooks-affect-kube-system-and-internal-aks-namespaces-)to learn how.## Cluster modes

In AKS, you can create a cluster with the Automatic or Standard mode. AKS Automatic provides a more fully managed experience. You can manage cluster configuration, including nodes, scaling, security, and other preconfigured settings. AKS Standard provides more control over the cluster configuration, including the ability to manage node pools, scaling, and other settings.

For more information, see [AKS Automatic and Standard feature comparison](intro-aks-automatic#aks-automatic-and-standard-feature-comparison).

## Pricing tiers

AKS offers three pricing tiers for cluster management: Free, Standard, and Premium. The pricing tier you choose determines the features that are available for managing your cluster.

For more information, see [Pricing tiers for AKS cluster management](free-standard-pricing-tiers).

## Supported Kubernetes versions

For more information, see [Supported Kubernetes versions in AKS](supported-kubernetes-versions).

## Related content

For information on more core concepts for AKS, see the following resources:
