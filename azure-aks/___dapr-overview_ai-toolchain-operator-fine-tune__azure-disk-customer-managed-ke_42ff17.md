---
merged_at: 2026-01-26T23:04:05.988430
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/dapr-overview -->

# Dapr extension for Azure Kubernetes Service (AKS) and Arc-enabled Kubernetes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Distributed Application Runtime (Dapr)](https://docs.dapr.io/) offers APIs that help you write and implement simple, portable, resilient, and secured microservices. Dapr APIs run as a sidecar process in tandem with your applications and abstract away common complexities you may encounter when building distributed applications, such as:

- Service discovery
- Message broker integration
- Encryption
- Observability
- Secret management

Dapr is incrementally adoptable. You can use any of the API building blocks as needed. [Learn the support level Microsoft offers for the Dapr extension.](#issue-handling)

## Capabilities and features

[Using the Dapr extension to provision Dapr on your AKS or Arc-enabled Kubernetes cluster](dapr) eliminates the overhead of:

- Downloading Dapr tooling
- Manually installing and managing the Dapr runtime on your AKS cluster

Additionally, the extension offers support for all [native Dapr configuration capabilities](dapr-settings) through simple command-line arguments.

Dapr provides the following set of capabilities to help with your microservice development on AKS:

- Easy provisioning of Dapr on AKS through
[cluster extensions](cluster-extensions) - Portability enabled through HTTP and gRPC APIs which abstract underlying technologies choices
- Reliable, secure, and resilient service-to-service calls through HTTP and gRPC APIs
- Publish and subscribe messaging made easy with support for CloudEvent filtering and "at-least-once" semantics for message delivery
- Pluggable observability and monitoring through Open Telemetry API collector
- Independent of language, while also offering language specific software development kits (SDKs)
- Integration with Visual Studio Code through the Dapr extension
[More APIs for solving distributed application challenges](https://docs.dapr.io/concepts/building-blocks-concept/)

## Issue handling

Microsoft categorizes issues raised against the Dapr extension into two parts:

- Extension operations
- Dapr runtime (including APIs and components)

The following table breaks down support priority levels for each of these categories.

| Description | Security risks/Regressions | Functional issues | |
|---|---|---|---|
Extension operations |
Issues encountered during extension operations, such as installing/uninstalling or upgrading the Dapr extension. | Microsoft prioritizes for immediate resolution. | Microsoft investigates and addresses as needed. |
Dapr runtime |
Issues encountered when using the Dapr runtime, APIs, and components via the extension, like cert expiration and unexpected component behavior. |
|

[Discuss issues with the Dapr open source project](https://github.com/dapr/dapr/issues/new/choose)to resolve in a hotfix or future Dapr open source release. Known open source functional issues won't be investigated by Microsoft at this time.### Clouds/regions

Global Azure cloud is supported with AKS and Arc support on the following regions:

| Region | AKS support | Arc for Kubernetes support |
|---|---|---|
`australiaeast` |
✔️ | ✔️ |
`australiasoutheast` |
✔️ | ❌ |
`brazilsouth` |
✔️ | ❌ |
`canadacentral` |
✔️ | ✔️ |
`canadaeast` |
✔️ | ✔️ |
`centralindia` |
✔️ | ✔️ |
`centralus` |
✔️ | ✔️ |
`eastasia` |
✔️ | ✔️ |
`eastus` |
✔️ | ✔️ |
`eastus2` |
✔️ | ✔️ |
`eastus2euap` |
❌ | ✔️ |
`francecentral` |
✔️ | ✔️ |
`francesouth` |
✔️ | ❌ |
`germanywestcentral` |
✔️ | ✔️ |
`japaneast` |
✔️ | ✔️ |
`japanwest` |
✔️ | ❌ |
`koreacentral` |
✔️ | ✔️ |
`koreasouth` |
✔️ | ❌ |
`northcentralus` |
✔️ | ✔️ |
`northeurope` |
✔️ | ✔️ |
`norwayeast` |
✔️ | ❌ |
`southafricanorth` |
✔️ | ❌ |
`southcentralus` |
✔️ | ✔️ |
`southeastasia` |
✔️ | ✔️ |
`southindia` |
✔️ | ❌ |
`swedencentral` |
✔️ | ✔️ |
`switzerlandnorth` |
✔️ | ✔️ |
`uaenorth` |
✔️ | ❌ |
`uksouth` |
✔️ | ✔️ |
`ukwest` |
✔️ | ❌ |
`westcentralus` |
✔️ | ✔️ |
`westeurope` |
✔️ | ✔️ |
`westus` |
✔️ | ✔️ |
`westus2` |
✔️ | ✔️ |
`westus3` |
✔️ | ✔️ |

## Frequently asked questions

### How do Dapr and Service meshes compare?

While Dapr and service meshes do offer some overlapping capabilities, a service mesh is focused on networking concerns, whereas Dapr is focused on providing building blocks that make building applications as microservices easier. Dapr is developer-centric, while service meshes are infrastructure-centric.

Some common capabilities that Dapr shares with service meshes include:

- Secure service-to-service communication with mTLS encryption
- Service-to-service metric collection
- Service-to-service distributed tracing
- Resiliency through retries

Dapr provides other application-level building blocks for state management, pub/sub messaging, actors, and more. However, Dapr doesn't provide capabilities for traffic behavior, such as routing or traffic splitting. If your solution would benefit from the traffic splitting a service mesh provides, consider using [Open Service Mesh](open-service-mesh-about).

For more information on Dapr and service meshes, and how they can be used together, visit the [Dapr documentation](https://docs.dapr.io/).

### How does the Dapr secrets API compare to the Secrets Store CSI driver?

Both the Dapr secrets API and the managed Secrets Store CSI driver allow for the integration of secrets held in an external store, abstracting secret store technology from application code.

The Secrets Store CSI driver mounts secrets held in Azure Key Vault as a CSI volume for consumption by an application.

Dapr exposes secrets via a RESTful API that can be:

- Called by application code
- Configured with assorted secret stores

The following table lists the capabilities of each offering:

| Dapr secrets API | Secrets Store CSI driver | |
|---|---|---|
Supported secrets stores |
Local environment variables (for Development); Local file (for Development); Kubernetes Secrets; AWS Secrets Manager; Azure Key Vault secret store; Azure Key Vault with Managed Identities on Kubernetes; GCP Secret Manager; HashiCorp Vault | Azure Key Vault secret store |
Accessing secrets in application code |
Call the Dapr secrets API | Access the mounted volume or sync mounted content as a Kubernetes secret and set an environment variable |
Secret rotation |
New API calls obtain the updated secrets | Polls for secrets and updates the mount at a configurable interval |
Logging and metrics |
The Dapr sidecar generates logs, which can be configured with collectors such as Azure Monitor, emits metrics via Prometheus, and exposes an HTTP endpoint for health checks | Emits driver and Azure Key Vault provider metrics via Prometheus |

For more information on the secret management in Dapr, see the [secrets management overview](https://docs.dapr.io/developing-applications/building-blocks/secrets/secrets-overview/).

For more information on the Secrets Store CSI driver and Azure Key Vault provider, see the [Secrets Store CSI driver overview](csi-secrets-store-driver).

### How does the managed Dapr cluster extension compare to the open source Dapr offering?

The managed Dapr cluster extension is the easiest method to provision Dapr on an AKS cluster. With the extension, you're able to offload management of the Dapr runtime version by opting into automatic upgrades. Additionally, the extension installs Dapr with smart defaults (for example, provisioning the Dapr control plane in high availability mode).

When installing Dapr open source via helm or the Dapr CLI, developers and cluster maintainers are also responsible for runtime versions and configuration options.

Lastly, the Dapr extension is an extension of AKS, therefore you can expect the same support policy as other AKS features.

[Learn more about migrating from Dapr open source to the Dapr extension for AKS](dapr-migration).

### How can I authenticate Dapr components with Microsoft Entra ID using managed identities?

- Learn how
[Dapr components authenticate with Microsoft Entra ID](https://docs.dapr.io/developing-applications/integrations/azure/azure-authentication). - Learn about
[using managed identities with AKS](use-managed-identity).

### How can I switch to using the Dapr extension if I've already installed Dapr via a method, such as Helm?

Recommended guidance is to completely uninstall Dapr from the AKS cluster and reinstall it via the cluster extension. [You can also check for the existing Dapr installation and migrate it to AKS.](dapr-migration)

If you install Dapr through the AKS extension, our recommendation is to continue using the extension for future management of Dapr instead of the Dapr CLI. Combining the two tools can cause conflicts and result in undesired behavior.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ai-toolchain-operator-fine-tune -->

# Fine-tune and deploy an AI model for inferencing on Azure Kubernetes Service (AKS) with the AI toolchain operator add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to fine-tune and deploy a language model inferencing workload on AKS with the AI toolchain operator add-on. You learn how to accomplish the following tasks:

[Set environment variables](#export-environmental-variables)to reference your Azure Container Registry (ACR) and repository details.[Create your container registry image push/pull secret](#create-a-new-secret-for-your-private-registry)to store and retrieve private fine-tuning adapter images.[Select a supported model and fine-tune it to your data](#fine-tune-an-ai-model).[Test the inference service endpoint](#test-the-model-inference-service-endpoint).[Clean up resources](#clean-up-resources).

The AI toolchain operator (KAITO) is a managed add-on for AKS that simplifies the deployment and operations for AI models on your AKS clusters. Starting with [KAITO version 0.3.1](https://github.com/kaito-project/kaito/releases/tag/v0.3.1) and above, you can use the AKS managed add-on to fine-tune supported foundation models with new data and enhance the accuracy of your AI models. To learn more about parameter efficient fine-tuning methods and their use cases, see [Concepts - Fine-tuning language models for AI and machine learning workflows on AKS](concepts-fine-tune-language-models).

## Before you begin

- This article assumes you have an existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Azure CLI version 2.47.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Prerequisites

- The Kubernetes command-line client, kubectl, installed and configured. For more information, see
[Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/). - Configure
[Azure Container Registry (ACR) integration](aks-extension-attach-azure-container-registry)of a new or existing ACR with your AKS cluster. - Install the
[AI toolchain operator add-on](ai-toolchain-operator)on your AKS cluster. - If you already have the AI toolchain operator add-on installed, update your AKS cluster to the latest version to run KAITO v0.3.1+ and ensure that the AI toolchain operator add-on feature flag is enabled.

## Export environmental variables

To simplify the configuration steps in this article, you can define environment variables using the following commands. Make sure to replace the placeholder values with your own.

```
ACR_NAME="myACRname"
ACR_USERNAME="myACRusername"
REPOSITORY="myRepository"
VERSION="repositoryVersion'
ACR_PASSWORD=$(az acr token create --name $ACR_USERNAME --registry $ACR_NAME --expiration-in-days 10 --repository $REPOSITORY content/write content/read --query "credentials.passwords[0].value" --output tsv)
```


## Create a new secret for your private registry

In this example, your KAITO fine-tuning deployment produces a containerized adapter output, and the KAITO workspace requires a new push secret as authorization to push the adapter image to your ACR.

Generate a new secret to provide the KAITO fine-tuning workspace access to push the model fine-tuning output image to your ACR using the `kubectl create secret docker-registry`

command.

```
kubectl create secret docker-registry myregistrysecret --docker-server=$ACR_NAME.azurecr.io --docker-username=$ACR_USERNAME --docker-password=$ACR_PASSWORD
```


## Fine-tune an AI model

In this example, you fine-tune the [Phi-3-mini small language model](https://huggingface.co/docs/transformers/main/en/model_doc/phi3) using the qLoRA tuning method by applying the following Phi-3-mini KAITO fine-tuning workspace CRD:

```
apiVersion: kaito.sh/v1alpha1
kind: Workspace
metadata:
name: workspace-tuning-phi-3-mini
resource:
instanceType: "Standard_NC24ads_A100_v4"
labelSelector:
matchLabels:
apps: tuning-phi-3-mini-pycoder
tuning:
preset:
name: phi3mini128kinst
method: qlora
input:
urls:
- “myDatasetURL”
output:
image: “$ACR_NAME.azurecr.io/$REPOSITORY:$VERSION”
imagePushSecret: myregistrysecret
```


This example uses a public dataset specified by a URL in the input. If choosing an image as the source of your fine-tuning data, please refer to the [KAITO fine-tuning API](https://github.com/kaito-project/kaito/tree/main) specification to adjust the input to pull an image from your ACR.

Note

The choice of GPU SKU is critical since model fine-tuning normally requires more GPU memory compared to model inference. To avoid GPU Out-Of-Memory errors, we recommend using NVIDIA A100 or higher tier GPUs.

Apply the KAITO fine-tuning workspace CRD using the

`kubectl apply`

command.`kubectl apply workspace-tuning-phi-3-mini.yaml`

Track the readiness of your GPU resources, fine-tuning job, and workspace using the

`kubectl get workspace`

command.`kubectl get workspace -w`

Your output should look similar to the following example output:

`NAME INSTANCE RESOURCE READY INFERENCE READY JOB STARTED WORKSPACE SUCCEEDED AGE workspace-tuning-phi-3-mini Standard_NC24ads_A100_v4 True True 3m 45s`

Check the status of your fine-tuning job pods using the

`kubectl get pods`

command.`kubectl get pods`


Note

You can store the adapter to your specific output location as a container image or any storage type supported by Kubernetes.

## Deploy the fine-tuned model for inferencing

Now, you use the Phi-3-mini adapter image created in the previous section for a new inferencing deployment with this model.

The KAITO inference workspace CRD below consists of the following resources and adapter(s) to deploy on your AKS cluster:

```
apiVersion: kaito.sh/v1alpha1
kind: Workspace
metadata:
name: workspace-phi-3-mini-adapter
resource:
instanceType: "Standard_NC6s_v3"
labelSelector:
matchLabels:
apps: phi-3-adapter
inference:
preset:
name: “phi-3-mini-128k-instruct“
adapters:
-source:
name: kubernetes-adapter
image: $ACR_NAME.azurecr.io/$REPOSITORY:$VERSION
imagePullSecrets:
- myregistrysecret
strength: “1.0”
```


Note

Optionally, you can pull in several adapters created from fine-tuning deployments with the same model on different data sets by defining additional "source" fields. Inference with different adapters to compare the performance of your fine-tuned model in varying contexts.

Apply the KAITO inference workspace CRD using the

`kubectl apply`

command.`kubectl apply -f workspace-phi-3-mini-adapter.yaml`

Track the readiness of your GPU resources, inference server, and workspace using the

`kubectl get workspace`

command.`kubectl get workspace -w`

Your output should look similar to the following example output:

`NAME INSTANCE RESOURCE READY INFERENCE READY JOB STARTED WORKSPACE SUCCEEDED AGE workspace-phi-3-mini-adapter Standard_NC6s_v3 True True True 5m 47s`

Check the status of your inferencing workload pods using the

`kubectl get pods`

command.`kubectl get pods`

It might take several minutes for your pods to show the

`Running`

status.

## Test the model inference service endpoint

Check your model inferencing service and retrieve the service IP address using the

`kubectl get svc`

command.`export SERVICE_IP=$(kubectl get svc workspace-phi-3-mini-adapter -o jsonpath=’{.spec.clusterIP}’)`

Run your fine-tuned Phi-3-mini model with a sample input of your choice using the

`kubectl run`

command. The following example asks the generative AI model,*"What is AKS?"*:`kubectl run -it --rm --restart=Never curl --image=curlimages/curl -- curl -X POST http://$SERVICE_IP/chat -H "accept: application/json" -H "Content-Type: application/json" -d "{\"prompt\":\"What is AKS?\"}"`

Your output might look similar to the following example output:

`"Kubernetes on Azure" is the official name. https://learn.microsoft.com/en-us/azure/aks/ ...`


## Clean up resources

If you no longer need these resources, you can delete them to avoid incurring extra Azure charges. To calculate the estimated cost of your resources, you can use the [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?service=kubernetes-service).

Delete the KAITO workspaces and their allocated resources on your AKS cluster using the `kubectl delete workspace`

command.

```
kubectl delete workspace workspace-tuning-phi-3-mini
kubectl delete workspace workspace-phi-3-mini-adapter
```


## Next steps

- Learn more about fine-tuning language models with KAITO in this
[AKS Engineering Blog](https://blog.aks.azure.com/2024/08/23/fine-tuning-language-models-with-kaito)! - Explore
[MLOps for AI and machine learning workflows](concepts-machine-learning-ops)and best practices on AKS - Learn about supported families of
[GPUs on Azure Kubernetes Service](gpu-cluster)

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-disk-customer-managed-keys -->

# Bring your own keys (BYOK) with Azure managed disks in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure encrypts all data in a managed disk at rest. By default, data is encrypted with Microsoft-managed keys. For more control over encryption keys, you can supply customer-managed keys to use for encryption at rest for both the OS and data disks for your AKS clusters.

Learn more about customer-managed keys on [Linux](/en-us/azure/virtual-machines/disk-encryption#customer-managed-keys) and [Windows](/en-us/azure/virtual-machines/disk-encryption#customer-managed-keys).

## Prerequisites

- You must enable soft delete and purge protection for
*Azure Key Vault*when using Key Vault to encrypt managed disks. - You need the Azure CLI version 2.11.1 or later.
- Data disk encryption and customer-managed keys are supported on Kubernetes versions 1.24 and higher.
- If you choose to rotate (change) your keys periodically, see
[Customer-managed keys and encryption of Azure managed disk](/en-us/azure/virtual-machines/disk-encryption)for more information.

## Limitations

Encryption of an OS disk with customer-managed keys can only be enabled when creating an AKS cluster.

Virtual nodes are not supported.

When encrypting an ephemeral OS disk-enabled node pool with customer-managed keys, if you want to rotate the key in Azure Key Vault, there are two options to consider:

Immediate usage of new CMK

- Scale down the node pool count to 0.
- Rotate the key.
- Scale up the node pool to the original count.

Gradual usage of new CMK

- Allow AKS node image upgrades or version upgrades to naturally adopt the new CMK over time.
- Until all nodes in the pool are upgraded, the existing CMK will continue to function without disruption.
- Once the upgrade process is complete across all nodes, the new CMK takes effect seamlessly.


## Create an Azure Key Vault instance

Use an Azure Key Vault instance to store your keys. You can optionally use the Azure portal to [Configure customer-managed keys with Azure Key Vault](/en-us/azure/storage/common/customer-managed-keys-configure-key-vault)

Create a new *resource group*, then create a new *Key Vault* instance and enable soft delete and purge protection. Ensure you use the same region and resource group names for each command.

```
# Optionally retrieve Azure region short names for use on upcoming commands
az account list-locations
```


```
# Create new resource group in a supported Azure region
az group create --location myAzureRegionName --name myResourceGroup
# Create an Azure Key Vault resource in a supported Azure region
az keyvault create --name myKeyVaultName --resource-group myResourceGroup --location myAzureRegionName --enable-purge-protection true
```


## Create an instance of a DiskEncryptionSet

Replace *myKeyVaultName* with the name of your key vault. You also need a *key* stored in Azure Key Vault to complete the following steps. Either store your existing Key in the Key Vault you created on the previous steps, or [generate a new key](/en-us/azure/key-vault/general/manage-with-cli2) and replace *myKeyName* with the name of your key.

Note

For cross-account access support for customer-managed encryption keys, you need to create the DiskEncryptionSet for cross-tenant customer-managed keys as detailed in [this guide](/en-us/azure/virtual-machines/disks-cross-tenant-customer-managed-keys?tabs=azure-cli#create-a-disk-encryption-set). The remaining storage class configuration is the same as normal customer managed keys.

```
# Retrieve the Key Vault Id and store it in a variable
keyVaultId=$(az keyvault show --name myKeyVaultName --query "[id]" -o tsv)
# Retrieve the Key Vault key URL and store it in a variable
keyVaultKeyUrl=$(az keyvault key show --vault-name myKeyVaultName --name myKeyName --query "[key.kid]" -o tsv)
# Create a DiskEncryptionSet
az disk-encryption-set create --name myDiskEncryptionSetName --location myAzureRegionName --resource-group myResourceGroup --source-vault $keyVaultId --key-url $keyVaultKeyUrl
```


Important

Make sure that the DiskEncryptionSet is located in the same region as your AKS cluster and that the AKS cluster identity has **read** access to the DiskEncryptionSet.

## Grant the DiskEncryptionSet access to key vault

Use the DiskEncryptionSet and resource groups you created on the prior steps, and grant the DiskEncryptionSet resource access to the Azure Key Vault.

```
# Retrieve the DiskEncryptionSet value and set a variable
desIdentity=$(az disk-encryption-set show --name myDiskEncryptionSetName --resource-group myResourceGroup --query "[identity.principalId]" -o tsv)
# Update security policy settings
az keyvault set-policy --name myKeyVaultName --resource-group myResourceGroup --object-id $desIdentity --key-permissions wrapkey unwrapkey get
```


## Create a new AKS cluster and encrypt the OS disk

Either create a new resource group, or select an existing resource group hosting other AKS clusters, then use your key to encrypt either using network-attached OS disks or ephemeral OS disk. By default, a cluster uses ephemeral OS disk when possible in conjunction with VM size and OS disk size.

Run the following command to retrieve the DiskEncryptionSet value and set a variable:

```
diskEncryptionSetId=$(az disk-encryption-set show --name mydiskEncryptionSetName --resource-group myResourceGroup --query "[id]" -o tsv)
```


If you want to create a new resource group for the cluster, run the following command:

```
az group create --name myResourceGroup --location myAzureRegionName
```


To create a regular cluster using network-attached OS disks encrypted with your key, you can do so by specifying the `--node-osdisk-type=Managed`

argument.

```
az aks create --name myAKSCluster --resource-group myResourceGroup --node-osdisk-diskencryptionset-id $diskEncryptionSetId --generate-ssh-keys --node-osdisk-type Managed
```


To create a cluster with ephemeral OS disk encrypted with your key, you can do so by specifying the `--node-osdisk-type=Ephemeral`

argument. You also need to specify the argument `--node-vm-size`

because the default vm size is too small and doesn't support ephemeral OS disk.

```
az aks create --name myAKSCluster --resource-group myResourceGroup --node-osdisk-diskencryptionset-id $diskEncryptionSetId --generate-ssh-keys --node-osdisk-type Ephemeral --node-vm-size Standard_DS3_v2
```


When new node pools are added to the cluster, the customer-managed key provided during the create process is used to encrypt the OS disk. The following example shows how to deploy a new node pool with an ephemeral OS disk.

```
az aks nodepool add --cluster-name $CLUSTER_NAME --resource-group $RG_NAME --name $NODEPOOL_NAME --node-osdisk-type Ephemeral
```


Important

The DiskEncryptionSet we previously applied to the storage class only encrypts new PVCs. Encrypting existing PVCs requires detaching first before using the Azure Disks API/CLI to update the underlying disks, as shown in [this related guide](/en-us/azure/virtual-machines/linux/disks-enable-customer-managed-keys-cli#encrypt-existing-managed-disks).

## Encrypt your AKS cluster data disk

If you have already provided a disk encryption set during cluster creation, encrypting data disks with the same disk encryption set is the default option. Therefore, this step is optional. However, if you want to encrypt data disks with a different disk encryption set, you can follow these steps.

Important

Ensure you have the proper AKS credentials. The managed identity needs to have contributor access to the resource group where the diskencryptionset is deployed. Otherwise, you'll get an error suggesting that the managed identity does not have permissions.

To assign the AKS cluster identity the Contributor role for the diskencryptionset, execute the following commands:

```
aksIdentity=$(az aks show --resource-group $RG_NAME --name $CLUSTER_NAME --query "identity.principalId")
az role assignment create --role "Contributor" --assignee $aksIdentity --scope $diskEncryptionSetId
```


Create a file called **byok-azure-disk.yaml** that contains the following information. Replace *myAzureSubscriptionId*, *myResourceGroup*, and *myDiskEncrptionSetName* with your values, and apply the yaml. Make sure to use the resource group where your DiskEncryptionSet is deployed.

```
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
name: byok
provisioner: disk.csi.azure.com # replace with "kubernetes.io/azure-disk" if aks version is less than 1.21
parameters:
skuname: StandardSSD_LRS
kind: managed
diskEncryptionSetID: "/subscriptions/{myAzureSubscriptionId}/resourceGroups/{myResourceGroup}/providers/Microsoft.Compute/diskEncryptionSets/{myDiskEncryptionSetName}"
```


Next, run the following commands to update your AKS cluster:

```
# Get credentials
az aks get-credentials --name myAksCluster --resource-group myResourceGroup --output table
# Update cluster
kubectl apply -f byok-azure-disk.yaml
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-node-pools -->

# Configure node pools for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to configure node pools for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS), including SKU selectors, resource limits, and priority weights. It also provides examples to help you get started.

## Overview of node pools in NAP

NAP uses virtual machine (VM) SKU requirements to decide the best VMs for pending workloads. You can configure:

- SKU families and specific instance types.
- Resource limits and priorities.
- Spot or On-demand instances.
- Architecture and capabilities requirements.

The `NodePool`

resource sets constraints on the nodes that NAP creates and the pods that run on those nodes. When you first install NAP, it creates a [default NodePool](#review-default-node-pool-configuration). You can modify this node pool or create extra node pools to suit your workload requirements.

## Key behaviors of `NodePools`

in NAP

When configuring `NodePools`

for NAP, keep the following behaviors in mind:

- NAP requires at least one
`NodePool`

to function. - NAP evaluates each configured
`NodePool`

. - NAP skips
`NodePools`

with taints not tolerated by a pod. - NAP applies startup taints to provisioned nodes but doesn't require pod toleration.
- NAP works best with mutually exclusive
`NodePools`

. When multiple`NodePools`

match, it uses the one with highest weight.

## Review default node pool configuration

The configuration of the default [Karpenter NodePool](https://karpenter.sh/docs/concepts/nodepools/) named

`default`

created by NAP is as follows:```
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
name: default
spec:
disruption:
consolidationPolicy: WhenEmptyOrUnderutilized
template:
spec:
nodeClassRef:
name: default
expireAfter: Never
# Requirements that constrain the parameters of provisioned nodes.
# These requirements are combined with pod.spec.affinity.nodeAffinity rules.
# Operators { In, NotIn, Exists, DoesNotExist, Gt, and Lt } are supported.
# https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#operators
requirements:
- key: kubernetes.io/arch
operator: In
values:
- amd64
- key: kubernetes.io/os
operator: In
values:
- linux
- key: karpenter.sh/capacity-type
operator: In
values:
- on-demand
- key: karpenter.azure.com/sku-family
operator: In
values:
- D
```


It also creates a `system-surge`

node pool, which helps to autoscale system pool nodes.

## Control configuration of default node pool during cluster creation

When you [create a new AKS cluster enabled with NAP using the Azure CLI](use-node-auto-provisioning#enable-nap-on-a-new-cluster), you can include the `--node-provisioning-default-pools`

flag to control the configuration of the default NAP `NodePool`

.

The `--node-provisioning-default-pools`

flag controls the default NAP `NodePool`

configuration and accepts the following values:

(default): Creates two standard`Auto`

`NodePools`

for immediate use.: Doesn't create any`None`

`NodePools`

. You must define your own.

Warning

**Changing from Auto to None**: If you change the setting from


`Auto`

to `None`

on an existing cluster, the default `NodePools`

aren't deleted automatically. You must delete them manually if you no longer need them.## Node pool configuration options

The following sections outline various configuration options for `NodePools`

in NAP, including [well-known labels and SKU selectors](#well-known-labels-and-sku-selectors), [node pool limits](#node-pool-limits), and [node pool weights](#node-pool-weights).

### Well-known labels and SKU selectors

Kubernetes defines [well-known labels](https://kubernetes.io/docs/reference/labels-annotations-taints/) that Azure implements. You can define these labels in the `spec.requirements`

section of the `NodePool`

API. NAP also supports Azure-specific labels for more advanced scheduling.

`karpenter.azure.com`

SKU selectors

The following table lists the `karpenter.azure.com`

SKU selectors you can use in the `spec.requirements`

section of your `NodePool`

API to define VM characteristics for your nodes:

| Selector | Description | Example |
|---|---|---|
`karpenter.azure.com/sku-family` |
VM SKU family | D, F, L, etc. |
`karpenter.azure.com/sku-name` |
Explicit SKU name | Standard_A1_v2 |
`karpenter.azure.com/sku-version` |
SKU version (without "v", can use 1) | 1, 2 |
`karpenter.sh/capacity-type` |
VM allocation type (Spot / On-demand) | Spot |
`karpenter.azure.com/sku-cpu` |
Number of CPUs in VM | 16 |
`karpenter.azure.com/sku-memory` |
Memory in VM in MiB | 131072 |
`kubernetes.azure.com/sku-cpu` |
Number of CPUs in VM | 16 |
`kubernetes.azure.com/sku-memory` |
Memory in VM in MiB | 131072 |
`karpenter.azure.com/sku-gpu-name` |
GPU name | A100 |
`karpenter.azure.com/sku-gpu-manufacturer` |
GPU manufacturer | nvidia |
`karpenter.azure.com/sku-gpu-count` |
GPU count per VM | 2 |
`karpenter.azure.com/sku-networking-accelerated` |
Whether the VM has accelerated networking | [true, false] |
`karpenter.azure.com/sku-storage-premium-capable` |
Whether the VM supports Premium IO storage | [true, false] |
`karpenter.azure.com/sku-storage-ephemeralos-maxsize` |
Size limit for the Ephemeral operating system (OS) disk in Gb | 92 |

`kubernetes.io`

well-known labels

The following table lists the `kubernetes.io`

well-known labels you can use in the `spec.requirements`

section of your `NodePool`

API to define node characteristics for your nodes:

| Label | Description | Example |
|---|---|---|
`topology.kubernetes.io/zone` |
Availability zone(s) | [uksouth-1,uksouth-2,uksouth-3] |
`kubernetes.io/os` |
Operating system | linux |
`kubernetes.io/arch` |
CPU architecture (AMD64 or ARM64) | [amd64, arm64] |

#### SKU family examples

The `karpenter.azure.com/sku-family`

selector allows you to target specific VM families.

| Family | Description |
|---|---|
| D-series | General-purpose VMs with balanced CPU-to-memory ratio |
| F-series | Compute-optimized VMs with high CPU-to-memory ratio |
| E-series | Memory-optimized VMs for memory-intensive applications |
| L-series | Storage-optimized VMs with high disk throughput |
| N-series | GPU-enabled VMs for compute-intensive workloads |

Example configuration using SKU family:

```
requirements:
- key: karpenter.azure.com/sku-family
operator: In
values:
- D
- F
```


#### SKU name examples

The `karpenter.azure.com/sku-name`

selector allows you to specify the exact VM instance type.

```
requirements:
- key: karpenter.azure.com/sku-name
operator: In
values:
- Standard_D4s_v3
- Standard_F8s_v2
```


#### SKU version examples

The `karpenter.azure.com/sku-version`

selector targets specific generations of VM SKUs.

```
requirements:
- key: karpenter.azure.com/sku-version
operator: In
values:
- "3" # v3 generation
- "5" # v5 generation
```


#### Availability zone example

The `topology.kubernetes.io/zone`

selector allows you to specify the availability zones for your nodes.

```
requirements:
- key: topology.kubernetes.io/zone
operator: In
values:
- eastus-1
- eastus-2
```


Note

You can find available zones for your region using the `az account list-locations --output table`

Azure CLI command.

#### Architecture example

The `kubernetes.io/arch`

selector allows you to specify the CPU architecture for your nodes. NAP supports both `amd64`

and `arm64`

nodes.

```
requirements:
- key: kubernetes.io/arch
operator: In
values:
- amd64
- arm64
```


#### OS example

The `kubernetes.io/os`

selector allows you to specify the operating system for your nodes.

```
requirements:
- key: kubernetes.io/os
operator: In
values:
- linux
```


#### Capacity type example

The `karpenter.sh/capacity-type`

selector allows you to specify whether to use Spot or On-demand instances.

Note

NAP prioritizes Spot instances when both Spot and On-demand are specified.

```
requirements:
- key: karpenter.sh/capacity-type
operator: In
values:
- spot
- on-demand
```


### Node pool limits

By default, NAP attempts to schedule your workloads within the Azure quota you have available. You can also specify the upper limit of resources that a node pool uses by specifying limits within the node pool spec. For example:

```
spec:
# Resource limits constrain the total size of the cluster.
# Limits prevent Node Auto Provisioning from creating new instances once the limit is exceeded.
limits:
cpu: "1000"
memory: 1000Gi
```


### Node pool weights

When you have multiple node pools defined, you can set a preference of where a workload should be scheduled by defining the relative weight in your node pool definitions. For example:

```
spec:
# Priority given to the node pool when the scheduler considers which to select.
# Higher weights indicate higher priority when comparing node pools.
# Specifying no weight is equivalent to specifying a weight of 0.
weight: 10
```


## Next steps

For more information on node auto-provisioning in AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-virtual-machine-sizes -->

# Virtual machine (VM) sizes, generations, and features for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) supports various virtual machine (VM) sizes, generations, and features to accommodate different workloads and performance requirements. This article provides an overview of available VM sizes and generations for AKS, how to check for available VM sizes in your region, reasons why certain VM sizes might not be available, and what happens when a VM size retires.

## VM support on AKS

Azure supports both Generation 1 (Gen 1) and [Generation 2 (Gen 2) virtual machines (VMs)](/en-us/azure/virtual-machines/generation-2). With some [exceptions](/en-us/windows-server/virtualization/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v), we generally recommend [migrating to Generation 2 VMs](#gen-2-vms-on-aks) to take advantage of the newest features and functionalities in Azure VMs.

The VM size and operating system (OS) you select when creating an AKS node pool determines the VM generation and [node image](node-images) used. Check the [list of supported sizes](/en-us/azure/virtual-machines/generation-2#generation-2-vm-sizes) to see if your SKU supports or requires Gen 2.

### Limitations

There are some limitations to take into account when choosing a VM generation and/or OS:

- Trusted Launch can only be enabled on VM sizes that support Gen 2.
- Confidential VM sizes always use Gen 2 on AKS.
- Arm64 VM sizes always use Gen 2 on AKS.
- Windows Server 2019 node pools don't support Gen 2 VM sizes.
- Windows Server 2022 node pools require use of a custom header to use Gen 2.

To use Gen 2 VMs on AKS, see [Use Gen 2 VMs](#gen-2-vms-on-aks).

## Available VM features

AKS supports various VM features that enhance security, performance, and functionality. Some key features include:

uses pending pod resource requirements to decide the optimal VM configuration to run your workloads efficiently and cost-effectively.**Node autoprovisioning (NAP)**provide a better experience for dynamic workloads and high availability requirements. Virtual Machines node pools enable you to set up multiple similar-family VMs in a single node pool. Your workloads are automatically scheduled on the available resources you configure.**Virtual Machines node pools**

## Supported VM sizes

For in-depth information about VM sizes available in Azure, see [Azure VM sizes](/en-us/azure/virtual-machines/sizes/overview?tabs=breakdownseries%2Cgeneralsizelist%2Ccomputesizelist%2Cmemorysizelist%2Cstoragesizelist%2Cgpusizelist%2Cfpgasizelist%2Chpcsizelist). To view supported Gen 2 VM sizes, see [Generation 2 VM sizes](/en-us/azure/virtual-machines/generation-2).

AKS also supports the following VM types and features:

[Confidential VMs (CVMs)](use-cvm)[Arm-based processor (Arm64) VMs](use-arm64-vms)[GPU-optimized VMs](/en-us/azure/virtual-machines/sizes/overview?tabs=breakdownseries%2Cgeneralsizelist%2Ccomputesizelist%2Cmemorysizelist%2Cstoragesizelist%2Cgpusizelist%2Cfpgasizelist%2Chpcsizelist#gpu-accelerated)[Trusted Launch](use-trusted-launch)[Federal Information Process Standard (FIPS)](enable-fips-nodes)

### Default behavior for supported VM sizes

There are three scenarios when creating a node pool with a supported VM size:

- If the VM size supports only Gen 1, the default behavior for both Linux and Windows node pools is to use the Gen 1 node image.
- If the VM size supports only Gen 2, the default behavior for both Linux and Windows node pools is to use the Gen 2 node image. Windows Server 2022 node pools require a custom header to use a VM size that only supports Gen 2. For more information, see
[Create a Windows node pool with a Gen 2 VM](generation-2-vms#create-a-node-pool-with-a-gen-2-vm). - If the VM size supports both Gen 1 and Gen 2, the default behavior for both Linux and Windows (in Windows Server 2025+) nodes pools is to use the Gen 2 node image. To use the Gen 2 node image for Windows Server 2022, see
[Create a Windows node pool with a Gen 2 VM](generation-2-vms#create-a-node-pool-with-a-gen-2-vm).

## Check available VM sizes

Check available VM sizes using the [ az vm list-skus](/en-us/cli/azure/vm#az-vm-list-skus) command.

```
az vm list-skus --location <your-location> --output table
```


## Why certain VM sizes might not be available

There are several reasons why certain VM sizes might not be available, including:

**Quota limits**: All Azure services set default limits and quotas for resources and features. For more information, see the following resources:[Quotas and regional limits for Azure Kubernetes Service (AKS)](quotas-skus-regions)[Check your quota usage](/en-us/azure/virtual-machines/quotas)[Request a quota increase through an Azure support request](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest)(for**Issue type**, select**Quota**)

Note

- For
, VM sizes with**user node pools***fewer than two vCPUs and two GBs of memory (RAM)*might not be used by default. - For
, VM sizes with**system node pools***fewer than two vCPUs and four GBs of memory (RAM)*might not be used by default. To ensure that you can reliably schedule the required`kube-system`

pods and your applications, we recommend that you**do not use any**.[B series VMs](/en-us/azure/virtual-machines/sizes/general-purpose/bv1-series)or[Av1 series VMs](/en-us/azure/virtual-machines/sizes/retirement/av1-series-retirement)

**VM sizes in preview**: VM sizes in preview might not be available to you if you haven't registered the preview flag for the VM size.**Blocked by AKS**: Some VM sizes might not be available by default in AKS. These sizes might require extra testing or validation to ensure compatibility with AKS. If you need a specific VM size that isn't available to you, you can[submit a GitHub issue request](https://github.com/Azure/AKS/issues).

Make sure you understand which features your workloads need and choose a VM size that meets those requirements. Later VM versions typically have better performance and improved features. For example, [Gen 2 VMs](#gen-2-vms-on-aks) have increased security and performance benefits over Gen 1 VMs.

## What happens when a VM size retires?

When a VM size or series reaches its retirement date, the VM is deallocated. VM deallocation causes your AKS node pools to break. To check the retirement status of a VM size, see [Retired Azure VM size series](/en-us/azure/virtual-machines/sizes/retirement/retired-sizes-list) or perform a search in [Azure Updates](https://azure.microsoft.com/updates). To check the VM size of your node pools, use the [`az aks nodepool list`

][az-aks-nodepool-list] command and query for the `vmSize`

property:

```
az aks nodepool list --resource-group <your-resource-group> --cluster-name <your-cluster-name> --query "[].{Name:name, VMSize:vmSize}" --output table
```


If you're using a VM size that's retiring/retired, we recommend [migrating your node pools to a supported VM size](#migrate-node-pools-to-a-supported-vm-size) to prevent any potential disruption to your service. Currently, AKS *doesn't support* transitioning to a new VM size within the same node pool.

## Migrate node pools to a supported VM size

Once you determine the appropriate node pools to take action on, you can [resize your node pools](resize-node-pool). During the resizing process, a new node pool is created and workloads are migrated to the new node pool.

For more information on migrating to a new VM size, see the following resources:

[Migrate from Gen 1 to Gen 2 VMs](#gen-2-vms-on-aks)[General-purpose sizes migration guide](/en-us/azure/virtual-machines/migration/sizes/d-ds-dv2-dsv2-ls-series-migration-guide)[Storage-optimized sizes migration guide](/en-us/azure/virtual-machines/migration/sizes/d-ds-dv2-dsv2-ls-series-migration-guide)[GPU-accelerated sizes migration guide](/en-us/azure/virtual-machines/migration/sizes/n-series-migration)[Azure Dedicated Host SKU migration guide](/en-us/azure/virtual-machines/migration/dedicated-host-migration-guide)

## Gen 2 VMs on AKS

Gen 2 VMs are generally Azure's newer offerings and have exclusive features over Gen 1 VMs like increased memory, improved CPU performance, support for NVMe disks, and support for [Trusted Launch](use-trusted-launch).

While we generally recommend running Gen 2 VMs, you should make sure that the generation you choose supports your requirements. To learn more about the differences between generations, and when one might make more sense than the other, see [Should I create a Gen 1 or 2 VM in Hyper-V?](/en-us/windows-server/virtualization/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)

To use Gen 2 VMs on AKS, see [Use generation 2 VMs on AKS](generation-2-vms).

## Next steps

- To learn more about Gen 2 VMs, see
[Support for Generation 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2) - To learn more about supported Gen 2 node images, see
[Node images](node-images)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/devops-pipeline -->

# Build and deploy to Azure Kubernetes Service with Azure Pipelines

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Azure DevOps Services**

Use [Azure Pipelines](/en-us/azure/devops/pipelines/) to automatically deploy to Azure Kubernetes Service (AKS). Azure Pipelines lets you build, test, and deploy with continuous integration (CI) and continuous delivery (CD) using [Azure DevOps](/en-us/azure/devops/).

In this article, you'll learn how to create a pipeline that continuously builds and deploys your app. Every time you change your code in a repository that contains a Dockerfile, the images are pushed to your Azure Container Registry, and the manifests are then deployed to your AKS cluster.

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - An Azure Resource Manager service connection.
[Create an Azure Resource Manager service connection](/en-us/azure/devops/pipelines/library/connect-to-azure#create-an-azure-resource-manager-service-connection-using-automated-security). - A GitHub account. Create a free
[GitHub account](https://github.com/join)if you don't have one already.

## Get the code

Fork the following repository containing a sample application and a Dockerfile:

```
https://github.com/MicrosoftDocs/pipelines-javascript-docker
```


## Create the Azure resources

Sign in to the [Azure portal](https://portal.azure.com/), and then select the [Cloud Shell](/en-us/azure/cloud-shell/overview) button in the upper-right corner. Use Azure CLI or PowerShell to create an AKS cluster.

### Create a container registry

```
# Create a resource group
az group create --name myapp-rg --location eastus
# Create a container registry
az acr create --resource-group myapp-rg --name mycontainerregistry --sku Basic
# Create a Kubernetes cluster
az aks create \
--resource-group myapp-rg \
--name myapp \
--node-count 1 \
--enable-addons monitoring \
--generate-ssh-keys
```


## Sign in to Azure Pipelines

Sign in to [Azure Pipelines](https://azure.microsoft.com/services/devops/pipelines). After you sign in, your browser goes to `https://dev.azure.com/my-organization-name`

and displays your Azure DevOps dashboard.

Within your selected organization, create a *project*. If you don't have any projects in your organization, you see a **Create a project to get started** screen. Otherwise, select the **Create Project** button in the upper-right corner of the dashboard.

## Create the pipeline

### Connect and select your repository

Sign in to your Azure DevOps organization and go to your project.

Go to

**Pipelines**, and then select**New pipeline**.Do the steps of the wizard by first selecting

**GitHub**as the location of your source code.You might be redirected to GitHub to sign in. If so, enter your GitHub credentials.

When you see the list of repositories, select your repository.

You might be redirected to GitHub to install the Azure Pipelines app. If so, select

**Approve & install**.Select

**Deploy to Azure Kubernetes Service**.If you're prompted, select the subscription in which you created your registry and cluster.

Select the

`myapp`

cluster.For

**Namespace**, select**Existing**, and then select**default**.Select the name of your container registry.

You can leave the image name set to the default.

Set the service port to 8080.

Set the

**Enable Review App for Pull Requests**checkbox for[review app](/en-us/azure/devops/pipelines/process/environments-kubernetes)related configuration to be included in the pipeline YAML autogenerated in subsequent steps.Select

**Validate and configure**.As Azure Pipelines creates your pipeline, the process will:

Create a

*Docker registry service connection*to enable your pipeline to push images into your container registry.Create an

*environment*and a Kubernetes resource within the environment. For an RBAC-enabled cluster, the created Kubernetes resource implicitly creates ServiceAccount and RoleBinding objects in the cluster so that the created ServiceAccount can't perform operations outside the chosen namespace.Generate an

*azure-pipelines.yml*file, which defines your pipeline.Generate Kubernetes manifest files. These files are generated by hydrating the

[deployment.yml](https://github.com/Microsoft/azure-pipelines-yaml/blob/master/templates/resources/k8s/deployment.yml)and[service.yml](https://github.com/Microsoft/azure-pipelines-yaml/blob/master/templates/resources/k8s/service.yml)templates based on selections you made. When you're ready, select**Save and run**.

Select

**Save and run**.You can change the

**Commit message**to something like*Add pipeline to our repository*. When you're ready, select**Save and run**to commit the new pipeline into your repo, and then begin the first run of your new pipeline!

## See your app deploy

As your pipeline runs, watch as your build stage, and then your deployment stage, go from blue (running) to green (completed). You can select the stages and jobs to watch your pipeline in action.

Note

If you're using a Microsoft-hosted agent, you must add the IP range of the Microsoft-hosted agent to your firewall. Get the weekly list of IP ranges from the [weekly JSON file](https://www.microsoft.com/download/details.aspx?id=56519), which is published every Wednesday. The new IP ranges become effective the following Monday. For more information, see [Microsoft-hosted agents](/en-us/azure/devops/pipelines/agents/hosted?tabs=yaml&view=azure-devops&preserve-view=true#networking).
To find the IP ranges that are required for your Azure DevOps organization, learn how to [identify the possible IP ranges for Microsoft-hosted agents](/en-us/azure/devops/pipelines/agents/hosted?tabs=yaml&view=azure-devops&preserve-view=true#to-identify-the-possible-ip-ranges-for-microsoft-hosted-agents).

After the pipeline run is finished, explore what happened and then go see your app deployed. From the pipeline summary:

Select the

**Environments**tab.Select

**View environment**.Select the instance of your app for the namespace you deployed to. If you used the defaults, then it is the

**myapp**app in the**default**namespace.Select the

**Services**tab.Select and copy the external IP address to your clipboard.

Open a new browser tab or window and enter <IP address>:8080.


If you're building our sample app, then *Hello world* appears in your browser.

## How the pipeline builds

When you finished selecting options and then proceeded to validate and configure the pipeline Azure Pipelines created a pipeline for you, using the *Deploy to Azure Kubernetes Service* template.

The build stage uses the [Docker task](/en-us/azure/devops/pipelines/tasks/build/docker) to build and push the image to the Azure Container Registry.

```
- stage: Build
displayName: Build stage
jobs:
- job: Build
displayName: Build job
pool:
vmImage: $(vmImageName)
steps:
- task: Docker@2
displayName: Build and push an image to container registry
inputs:
command: buildAndPush
repository: $(imageRepository)
dockerfile: $(dockerfilePath)
containerRegistry: $(dockerRegistryServiceConnection)
tags: |
$(tag)
- task: PublishPipelineArtifact@1
inputs:
artifactName: 'manifests'
path: 'manifests'
```


The deployment job uses the *Kubernetes manifest task* to create the `imagePullSecret`

required by Kubernetes cluster nodes to pull from the Azure Container Registry resource. Manifest files are then used by the Kubernetes manifest task to deploy to the Kubernetes cluster. The manifest files, `service.yml`

and `deployment.yml`

, were generated when you used the **Deploy to Azure Kubernetes Service** template.

```
- stage: Deploy
displayName: Deploy stage
dependsOn: Build
jobs:
- deployment: Deploy
displayName: Deploy job
pool:
vmImage: $(vmImageName)
environment: 'myenv.aksnamespace' #customize with your environment
strategy:
runOnce:
deploy:
steps:
- task: DownloadPipelineArtifact@2
inputs:
artifactName: 'manifests'
downloadPath: '$(System.ArtifactsDirectory)/manifests'
- task: KubernetesManifest@1
displayName: Create imagePullSecret
inputs:
action: 'createSecret'
connectionType: 'kubernetesServiceConnection'
kubernetesServiceConnection: 'myapp-default' #customize for your Kubernetes service connection
secretType: 'dockerRegistry'
secretName: '$(imagePullSecret)'
dockerRegistryEndpoint: '$(dockerRegistryServiceConnection)'
- task: KubernetesManifest@1
displayName: Deploy to Kubernetes cluster
inputs:
action: 'deploy'
connectionType: 'kubernetesServiceConnection'
kubernetesServiceConnection: 'myapp-default' #customize for your Kubernetes service connection
manifests: |
$(Pipeline.Workspace)/manifests/deployment.yml
$(Pipeline.Workspace)/manifests/service.yml
containers: '$(containerRegistry)/$(imageRepository):$(tag)'
imagePullSecrets: '$(imagePullSecret)'
```


## Clean up resources

Whenever you're done with the resources you created, you can use the following command to delete them:

```
az group delete --name myapp-rg
```


Enter `y`

when you're prompted.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/support-policies -->

# Support policies for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes technical support policies and limitations for Azure Kubernetes Service (AKS). It also details agent node management, managed control plane components, third-party open-source components, and security or patch management.

## Service updates and releases

- For release information, see
[AKS release notes](https://github.com/Azure/AKS/releases). - For information on preview features, see the
[AKS roadmap](https://github.com/Azure/AKS/projects/1).

## Managed features in AKS

Base infrastructure as a service (IaaS) cloud components, such as compute or networking components, allow you access to low-level controls and customization options. By contrast, AKS provides a turnkey Kubernetes deployment that gives you a common set of configurations and capabilities you need for your cluster. As an AKS user, you have limited customization and deployment options. In exchange, you don't need to worry about or manage Kubernetes clusters directly.

With AKS, you get a fully managed *control plane*. The control plane contains all of the components and services you need to operate and deliver Kubernetes clusters to end users. Microsoft maintains and operates all Kubernetes components.

Microsoft manages and monitors the following components through the control plane:

- Kubelet or Kubernetes API servers
- Etcd or a compatible key-value store, providing Quality of Service (QoS), scalability, and runtime
- DNS services (for example, kube-dns or CoreDNS)
- Kubernetes proxy or networking, except when
[BYOCNI](use-byo-cni)is used - Any other
[add-ons](integrations#add-ons)or system component running in the kube-system namespace.

AKS isn't a Platform-as-a-Service (PaaS) solution. Some components, such as agent nodes, have *shared responsibility*, where you must help maintain the AKS cluster. User input is required, for example, to apply an agent node operating system (OS) security patch.

The services are *managed* in the sense that Microsoft and the AKS team deploys, operates, and is responsible for service availability and functionality. Customers can't alter these managed components. Microsoft limits customization to ensure a consistent and scalable user experience.

## Shared responsibility

When a cluster is created, you define the Kubernetes agent nodes that AKS creates. Your workloads are executed on these nodes.

Because your agent nodes execute private code and store sensitive data, Microsoft Support can access them only in a limited way. Microsoft Support can't sign in to, execute commands in, or view logs for these nodes without your express permission or assistance.

Any modification made directly to the agent nodes using any one of the IaaS APIs renders the cluster unsupportable. Any modification applied to the agent nodes must be done using kubernetes-native mechanisms such as `Daemon Sets`

.

Similarly, while you might add any metadata to the cluster and nodes, such as tags and labels, changing any of the system created metadata renders the cluster unsupported.

## AKS support coverage

### Supported scenarios

Microsoft provides technical support for the following examples:

- Connectivity to all Kubernetes components that the Kubernetes service provides and supports, such as the API server.
- Management, uptime, QoS, and operations of Kubernetes control plane services (For example, Kubernetes control plane, API server, etcd, and coreDNS).
- Etcd data store. Support includes automated, transparent backups of all etcd data every 30 minutes for disaster planning and cluster state restoration. These backups aren't directly available to you or anyone else. They ensure data reliability and consistency. On-demand rollback or restore isn't supported as a feature.
- Any integration points in the Azure cloud provider driver for Kubernetes. These include integrations into other Azure services such as load balancers, persistent volumes, or networking (Kubernetes and Azure CNI, except when
[BYOCNI](use-byo-cni)is in use). - Questions or issues about customization of control plane components such as the Kubernetes API server, etcd, and coreDNS.
- Issues about networking, such as Azure CNI, kubenet, or other network access and functionality issues, except when
[BYOCNI](use-byo-cni)is in use. Issues could include DNS resolution, packet loss, routing, and so on. Microsoft supports various networking scenarios:- Kubenet and Azure CNI using managed VNETs or with custom (bring your own) subnets.
- Connectivity to other Azure services and applications
- Microsoft-managed ingress controllers or load balancer configurations
- Network performance and latency
- Microsoft-managed
[network policies](use-network-policies#differences-between-network-policy-engines-cilium-azure-npm-and-calico)components and functionalities


Note

Any cluster actions taken by Microsoft/AKS are made with your consent under a built-in Kubernetes role `aks-service`

and built-in role binding `aks-service-rolebinding`

. This role enables AKS to troubleshoot and diagnose cluster issues, but can't modify permissions nor create roles or role bindings, or other high privilege actions. Role access is only enabled under active support tickets with just-in-time (JIT) access.

### Unsupported scenarios

Microsoft doesn't provide technical support for the following scenarios:

Questions about how to use Kubernetes. For example, Microsoft Support doesn't provide advice on how to create custom ingress controllers, use application workloads, or apply third-party or open-source software packages or tools.

Note

Microsoft Support can advise on AKS cluster functionality, customization, and tuning (for example, Kubernetes operations issues and procedures).

Third-party open-source projects that aren't provided as part of the Kubernetes control plane or deployed with AKS clusters. These projects might include Istio, Helm, Envoy, or others.

Note

Microsoft can provide best-effort support for third-party open-source projects such as Helm. Where the third-party open-source tool integrates with the Kubernetes Azure cloud provider or other AKS-specific bugs, Microsoft supports examples and applications from Microsoft documentation.

Third-party closed-source software. This software can include security scanning tools and networking devices or software.

Configuring or troubleshooting application-specific code or behavior of third-party applications or tools running within the AKS cluster. This includes application deployment issues not related to the AKS platform itself.

Issuance, renewal, or management of certificates for applications running on AKS.

Network customizations other than the ones listed in the

[AKS documentation](./). For example, Microsoft Support can't configure devices or virtual appliances meant to provide[outbound traffic](outbound-rules-control-egress)for the AKS cluster, such as VPNs or firewalls.Note

On a best-effort basis, Microsoft Support might advise on the

[configuration needed](outbound-rules-control-egress)for Azure Firewall, but not for other third-party devices.Custom or third-party CNI plugins used in

[BYOCNI](use-byo-cni)mode.Configuring or troubleshooting non-Microsoft-managed network policies. While using network policies is supported, Microsoft Support can't investigate issues stemming from custom network policy configurations.

Configuring or troubleshooting non-Microsoft-managed ingress controllers, such as nginx, kong, traefik, etc. This includes addressing functionality issues that arise after AKS-specific operations, like an ingress controller ceasing to work following a Kubernetes version upgrade. Such issues might stem from incompatibilities between the ingress controller version and the new Kubernetes version. For a fully supported option, consider leveraging a

[Microsoft-managed ingress controller option](concepts-network-ingress#compare-ingress-options).Configuring or troubleshooting DaemonSets (including scripts) used to customize node configurations. Although using DaemonSets is the recommended approach to tune, modify, or install third-party software on cluster agent nodes when

[configuration file parameters](custom-node-configuration)are insufficient, Microsoft Support can't troubleshoot issues arising from the custom scripts used in DaemonSets due to their custom nature.Stand-by and proactive scenarios. Microsoft Support provides reactive support to help solve active issues in a timely and professional manner. However, standby or proactive support to help you eliminate operational risks, increase availability, and optimize performance aren't covered.

[Eligible customers](https://www.microsoft.com/unifiedsupport)can contact their account team to get nominated for[Azure Event Management service](https://devblogs.microsoft.com/premier-developer/proactively-plan-for-your-critical-event-in-azure-with-enhanced-support-and-engineering-services/). It's a paid service delivered by Microsoft support engineers that includes a proactive solution risk assessment and coverage during the event.Vulnerabilities / CVEs with a vendor fix that is less than 30 days old. As long as you're running the updated VHD, you shouldn't be running any container image vulnerabilities / CVEs with a vendor fix that is over 30 days old. It's customer responsibility to update the VHD and provide filtered lists to Microsoft support. Once you updated your VHD, it is customer responsibility to filter the vulnerabilities / CVEs report and provide a list only with vulnerabilities/CVEs with a vendor fix that is over 30 days old. If that will be the case, Microsoft support will make sure to work internally and address components with a vendor fix released more than 30 days ago. Additionally, Microsoft provide vulnerability / CVE-related support only for Microsoft-managed components (i.e., AKS node images, managed container images for applications that get deploy during cluster creation or via the installation of a managed add-on). For more details about vulnerability management for AKS, visit

[this page](concepts-vulnerability-management).Custom code samples or scripts. While Microsoft Support

*can*provide small code samples and reviews of small code samples within a support case to demonstrate how to use features of a Microsoft product, Microsoft Support*can't*provide custom code samples that are specific to your environment or application.

## AKS support coverage for agent nodes

### Microsoft responsibilities for AKS agent nodes

Microsoft and you share responsibility for Kubernetes agent nodes where:

- The base OS image has required additions (such as monitoring and networking agents).
- The agent nodes receive OS patches automatically.
- Issues with the Kubernetes control plane components that run on the agent nodes are automatically remediated. These components include the below:
`Kube-proxy`

- Networking tunnels that provide communication paths to the Kubernetes master components
`Kubelet`

`containerd`


Note

If an agent node isn't operational, AKS might restart individual components or the entire agent node. These restart operations are automated and provide auto-remediation for common issues. If you want to know more about the auto-remediation mechanisms, see [Node Auto-Repair](node-auto-repair)

### Customer responsibilities for AKS agent nodes

Microsoft provides patches and new images for your image nodes weekly. To keep your agent node OS and runtime components up to date, you should apply these patches and updates regularly either manually or automatically. For more information, see:

Similarly, AKS regularly releases new Kubernetes patches and minor versions. These updates can contain security or functionality improvements to Kubernetes. You're responsible to keep your clusters' Kubernetes version updated and according to the [AKS Kubernetes support version policy](supported-kubernetes-versions).

#### User customization of agent nodes

Note

AKS agent nodes appear in the Azure portal as standard Azure IaaS resources. However, these virtual machines are deployed into a custom Azure resource group (prefixed with MC_*). You can't change the base OS image or make any direct customizations to these nodes using the IaaS APIs or resources. Any custom changes that aren't performed from the AKS API won't persist through an upgrade, scale, update or reboot. Also, any change to the nodes' extensions like the **CustomScriptExtension** can lead to unexpected behavior and should be prohibited.
Avoid performing changes to the agent nodes unless Microsoft Support directs you to make changes.

AKS manages the lifecycle and operations of agent nodes on your behalf and modifying the IaaS resources associated with the agent nodes is **not supported**. An example of an unsupported operation is customizing a node pool virtual machine scale set by manually changing configurations in the Azure portal or from the API.

For workload-specific configurations or packages, AKS recommends using [Kubernetes daemon sets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/).

Using Kubernetes privileged `daemon sets`

and init containers enables you to tune/modify or install third party software on cluster agent nodes. Examples of such customizations include adding custom security scanning software or updating sysctl settings.

While this path is recommended if the above requirements apply, AKS engineering and support can't help troubleshoot or diagnose modifications that render the node unavailable due to a custom deployed `daemon set`

.

### Security issues and patching

If a security flaw is found in one or more of the managed components of AKS, the AKS team patches all affected clusters to mitigate the issue. Alternatively, the AKS team provides you with upgrade guidance.

For agent nodes affected by a security flaw, Microsoft notifies you with details on the impact and the steps to fix or mitigate the security issue.

### Node maintenance and access

Although you can sign in to and change agent nodes, doing this operation is discouraged because changes can make a cluster unsupportable.

## Network ports, access, and NSGs

You might only customize the NSGs on custom subnets. You might not customize NSGs on managed subnets or at the NIC level of the agent nodes. AKS has egress requirements to specific endpoints, to control egress and ensure the necessary connectivity, see [limit egress traffic](limit-egress-traffic). For ingress, the requirements are based on the applications you have deployed to cluster.

## Stopped, deallocated, and Not Ready nodes

If you don't need your AKS workloads to run continuously, you can [stop the AKS cluster](start-stop-cluster#stop-an-aks-cluster), which stops all nodepools and the control plane. You can start it again when needed. When you stop a cluster using the `az aks stop`

command, the cluster state is preserved for up to 12 months. After 12 months, the cluster state and all of its resources are deleted.

Manually deallocating all cluster nodes from the IaaS APIs, the Azure CLI, or the Azure portal isn't supported to stop an AKS cluster or nodepool. The cluster will be considered out of support and stopped by AKS after 30 days. The clusters are then subject to the same 12 month preservation policy as a correctly stopped cluster.

Clusters with zero **Ready** nodes (or all **Not Ready**) and zero **Running** VMs will be stopped after 30 days.

AKS reserves the right to archive control planes that have been configured out of support guidelines for extended periods equal to and beyond 30 days. AKS maintains backups of cluster etcd metadata and can readily reallocate the cluster. This reallocation is initiated by any PUT operation bringing the cluster back into support, such as an upgrade or scale to active agent nodes.

All clusters in a suspended subscription will be stopped immediately and deleted after 90 days. All clusters in a deleted subscription will be deleted immediately.

## Unsupported alpha and beta Kubernetes features

AKS only supports stable and beta features within the upstream Kubernetes project. Unless otherwise documented, AKS doesn't support any alpha feature that is available in the upstream Kubernetes project.

## Preview features or feature flags

For features and functionality that requires extended testing and user feedback, Microsoft releases new preview features or features behind a feature flag. Consider these features as prerelease or beta features.

Preview features or feature-flag features aren't meant for production. Ongoing changes in APIs and behavior, bug fixes, and other changes can result in unstable clusters and downtime.

Features in public preview fall under **best effort** support, as these features are in preview and aren't meant for production. The AKS technical support teams provides support during business hours only. For more information, see [Azure Support FAQ](https://azure.microsoft.com/support/faq/).

## Upstream bugs and issues

Given the speed of development in the upstream Kubernetes project, bugs invariably arise. Some of these bugs can't be patched or worked around within the AKS system. Instead, bug fixes require larger patches to upstream projects (such as Kubernetes, node or agent operating systems, and kernel). For components that Microsoft owns (such as the Azure cloud provider), AKS and Azure personnel are committed to fixing issues upstream in the community.

When the root cause of a technical support issue is due to one or more upstream bugs, AKS support and engineering teams will:

Identify and link the upstream bugs with any supporting details to help explain why this issue affects your cluster or workload. Customers receive links to the required repositories so they can watch the issues and see when a new release will provide fixes.

Provide potential workarounds or mitigation. If the issue can be mitigated, a

[known issue](https://github.com/Azure/AKS/issues?q=is%3Aissue+is%3Aopen+label%3Aknown-issue)is filed in the AKS repository. The known-issue filing explains:- The issue, including links to upstream bugs.
- The workaround and details about an upgrade or another persistence of the solution.
- Rough timelines for the issue's inclusion, based on the upstream release cadence.
