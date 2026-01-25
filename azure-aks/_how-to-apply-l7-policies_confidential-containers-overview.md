---
merged_at: 2026-01-25T12:25:33.942276
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: how-to-apply-l7-policies.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/how-to-apply-l7-policies -->

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

<!-- DOCUMENTO FUSIONADO: confidential-containers-overview.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/confidential-containers-overview -->

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
