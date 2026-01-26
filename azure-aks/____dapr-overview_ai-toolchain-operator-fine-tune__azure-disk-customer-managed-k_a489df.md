---
merged_at: 2026-01-26T20:54:26.144168
merged_files: 2
---


---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/how-to-configure-container-network-logs -->

# Set up container network logs with Advanced Container Networking Services (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Component renaming (starting November 11, 2025)

We are renaming components in the Container Network Logs feature to improve clarity and consistency:

What's changing

**CRD**:`RetinaNetworkFlowLogs`

→`ContainerNetworkLog`

**CLI flag**:`--enable-retinanetworkflowlog`

→`--enable-container-network-logs`

**Log Analytics table**:`RetinaNetworkFlowLogs`

→`ContainerNetworkLog`


Action items for existing users to enable new naming

**Update Azure CLI**(MUST - First step!):`az upgrade`

**Update Preview CLI Extension**(MUST):`az extension update --name aks-preview`

**Disable Monitoring**:`az aks disable-addons -a monitoring -n <cluster-name> -g <resource-group>`

**Re-enable Monitoring**:`az aks enable-addons -a monitoring --enable-high-log-scale-mode -g <resource-group> -n <cluster-name>`

**Re-enable ACNS Container Network Logs**:`az aks update --enable-acns --enable-container-network-logs -g <resource-group> -n <cluster-name>`

**Apply new ContainerNetworkLog CRD**: Apply your updated CRD configuration with the new naming.**Reimport Grafana Dashboards**: Import the updated dashboards to reflect the new table names.

Note

- Previously collected data stays in your workspace in old table RetinaNetworkFlowLogs.
- After re-enabling, allow a short delay before new data appears in new table ContainerNetworkLog.

In this article, you complete the steps to configure and use the container network logs feature in Advanced Container Networking Services for Azure Kubernetes Service (AKS). These logs offer persistent network flow monitoring tailored to enhance visibility in containerized environments.

By capturing container network logs, you can effectively track network traffic, detect anomalies, optimize performance, and ensure compliance with established policies. Follow the detailed instructions provided to set up and integrate container network logs for your system. For more information about the container network logs feature, see [Overview of container network logs](container-network-observability-logs).

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


The minimum version of the Azure CLI required to complete the steps in this article is 2.75.0. To find your version, run

`az --version`

in the Azure CLI. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).Container network logs in stored logs mode work only for Cilium data planes.

Container network logs in on-demand mode work for both Cilium and non-Cilium data planes.

If your existing cluster is version 1.33 or earlier, upgrade the cluster to the latest available Kubernetes version.

The minimum version of the

`aks-preview`

Azure CLI extension to complete the steps in this article is`19.0.07`

.

### Install the aks-preview Azure CLI extension

Install or update the Azure CLI preview extension by using the [ az extension add](/en-us/cli/azure/extension#az-extension-add) or

[command.](/en-us/cli/azure/extension#az-extension-update)

`az extension update`

```
# Install the aks-preview extension
az extension add --name aks-preview
# Update the extension to make sure you have the latest version installed
az extension update --name aks-preview
```


### Register the AdvancedNetworkingFlowLogsPreview feature flag

First, register the AdvancedNetworkingFlowLogsPreview feature flag by using the [ az feature register](/en-us/cli/azure/feature#az-feature-register) command:

```
az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingFlowLogsPreview"
```


Verify successful registration by using the [ az feature show](/en-us/cli/azure/feature#az-feature-show) command. It takes a few minutes for registration to complete.

```
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingFlowLogsPreview"
```


When the feature shows **Registered**, refresh the registration of the `Microsoft.ContainerService`

resource provider by using the [ az provider register](/en-us/cli/azure/provider#az-provider-register) command.

## Limitations

- Layer 7 flow data is captured only when Layer 7 policy support is enabled. For more information, see
[Configure a Layer 7 policy](how-to-apply-l7-policies). - Domain Name System (DNS) flows and related metrics are captured only when a Cilium Fully Qualified Domain (FQDN) network policy is applied. For more information, see
[Configure an FQDN policy](how-to-apply-fqdn-filtering-policies). - Onboarding by using Terraform isn't supported at this time.
- When Log Analytics isn't configured for log storage, container network logs are limited to a maximum of 50 MB of storage. When this limit is reached, new entries overwrite older logs.
- If the log table plan is set to Basic logs, the prebuilt Grafana dashboards don't function as expected.
- The Auxiliary logs table plan isn't supported.

## Configure stored logs mode for container network logs

### Deployment methods

You can onboard to container network logs using different deployment methods:

This section provides two paths for setting up container network logs based on your current situation:

: Complete setup for new AKS clusters[New clusters](#new-clusters): Enable container network logs on existing AKS clusters[Existing clusters](#existing-clusters)

## New clusters

This section guides you through setting up container network logs on a new AKS cluster from start to finish.

### Create a new AKS cluster with Advanced Container Networking Services

Use the `az aks create`

command with the `--enable-acns`

flag to create a new AKS cluster that has all Advanced Container Networking Services features. These features include:

**Container Network Observability:**Provides insight into your network traffic. To learn more, see[Container Network Observability](advanced-container-networking-services-overview#container-network-observability).**Container Network Security:**Offers security features like FQDN filtering. To learn more, see[Container Network Security](advanced-container-networking-services-overview#container-network-security).

```
# Set an environment variable for the AKS cluster name. Make sure you replace the placeholder with your own value.
export CLUSTER_NAME="<aks-cluster-name>"
export RESOURCE_GROUP="<aks-resource-group>"
export LOCATION="<location>"
# Create the resource group if it doesn't already exist
az group create --name $RESOURCE_GROUP --location $LOCATION
# Create an AKS cluster
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--generate-ssh-keys \
--location $LOCATION \
--max-pods 250 \
--network-plugin azure \
--network-plugin-mode overlay \
--network-dataplane cilium \
--node-count 2 \
--pod-cidr 192.168.0.0/16 \
--kubernetes-version 1.33 or later \
--enable-acns
```


### Configure custom resources for log filtering

To configure container network logs in stored logs mode, you must define specific custom resources to set filters for log collection. When at least one custom resource is defined, logs are collected and stored on the host node at `/var/log/acns/hubble/events.log`

.

To configure logging, you must define and apply the `ContainerNetworkLog`

type of custom resource. You set filters like namespace, pod, service, port, protocol, and verdict. Multiple custom resources can exist in a cluster simultaneously. If no custom resource is defined with nonempty filters, no logs are saved in the designated location.

The following sample definition demonstrates how to configure the `ContainerNetworkLog`

type of custom resource.

### ContainerNetworkLog CRD template

```
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkLog
metadata:
name: sample-containernetworklog # Cluster scoped
spec:
includefilters: # List of filters
- name: sample-filter # Filter name
from:
namespacedPod: # List of source namespace/pods. Prepend namespace with /
- sample-namespace/sample-pod
labelSelector: # Standard k8s label selector
matchLabels:
app: frontend
k8s.io/namespace: sample-namespace
matchExpressions:
- key: environment
operator: In
values:
- production
- staging
ip: # List of source IPs; can be CIDR
- "192.168.1.10"
- "10.0.0.1"
to:
namespacedPod:
- sample-namespace2/sample-pod2
labelSelector:
matchLabels:
app: backend
k8s.io/namespace: sample-namespace2
matchExpressions:
- key: tier
operator: NotIn
values:
- dev
ip:
- "192.168.1.20"
- "10.0.1.1"
protocol: # List of protocols; can be tcp, udp, dns
- tcp
- udp
- dns
verdict: # List of verdicts; can be forwarded, dropped
- forwarded
- dropped
```


The following table describes the fields in the custom resource definition:

| Field | Type | Description | Required |
|---|---|---|---|
`includefilters` |
[]filter | A list of filters that define network flows to include. Each filter specifies the source, destination, protocol, and other matching criteria. Include filters can't be empty and must have at least one filter. | Mandatory |
`filters.name` |
String | The name of the filter. | Optional |
`filters.protocol` |
[]string | The protocols to match for this filter. Valid values are `tcp` , `udp` , and `dns` . This parameter is optional. If not specified, logs with all protocols are included. |
Optional |
`filters.verdict` |
[]string | The verdict of the flow to match. Valid values are `forwarded` and `dropped` . This parameter is optional. If not specified, logs with all verdicts are included. |
Optional |
`filters.from` |
Endpoint | Specifies the source of the network flow. Can include IP addresses, label selectors, and namespace/pod pairs. | Optional |
`Endpoint.ip` |
[]string | It can be a single IP or a CIDR. | Optional |
`Endpoint.labelSelector` |
Object | A label selector is a mechanism to filter and query resources based on labels, so you can identify specific subsets of resources. A label selector can include two components: `matchLabels` and `matchExpressions` . Use `matchLabels` for straightforward matching by specifying a key/value pair (for example, `{"app": "frontend"}` ). For more advanced criteria, use `matchExpressions` , where you define a label key, an operator (such as `In` , `NotIn` , `Exists` , or `DoesNotExist` ), and an optional list of values. Ensure that the conditions in both `matchLabels` and `matchExpressions` are met, because they're logically combined by `AND` . If no conditions are specified, the selector matches all resources. To match none, leave the selector null. Carefully define your label selector to target the correct set of resources. |
Optional |
`Endpoint.namespacedPod` |
[]string | A list of namespace and pod pairs (formatted as `namespace/pod` ) for matching the source. `name` should match the RegEx pattern `^.+$` . |
Optional |
`filters.to` |
Endpoint | Specifies the destination of the network flow. Can include IP addresses, label selectors, or namespace/pod pairs. | Optional |
`Endpoint.ip` |
[]string | It can be a single IP or a CIDR. | Optional |
`Endpoint.labelSelector` |
Object | A label selector to match resources based on their labels. | Optional |
`Endpoint.namespacedPod` |
[]string | A list of namespace and pod pairs (formatted as `namespace/pod` ) to match the destination. |
Optional |

Apply the

`ContainerNetworkLog`

custom resource to enable log collection at the cluster:`kubectl apply -f <crd.yaml>`

Tip

For a practical example of a ContainerNetworkLog custom resource configuration, see the

[sample CRD in the AKS Labs documentation](https://azure-samples.github.io/aks-labs/docs/networking/acns-lab/#enable-flow-logs-for-the-pets-namespace).

Logs stored locally on host nodes are temporary because the host or node itself isn't a persistent storage solution. Logs on host nodes are also rotated when their size reaches 50 MB. For longer-term storage and analysis, we recommend that you configure the Azure Monitor Agent on the cluster to collect and retain logs in the Log Analytics workspace.

Alternatively, you can integrate a partner logging service like an OpenTelemetry collector for more log management options.

### Configure Azure Monitor for managed storage (recommended)

For persistent storage and advanced analytics, configure the Azure Monitor Agent to collect and store logs in a Log Analytics workspace:

```
# Set an environment variable for the AKS cluster name. Make sure you replace the placeholder with your own value.
export CLUSTER_NAME="<aks-cluster-name>"
export RESOURCE_GROUP="<aks-resource-group>"
# Enable azure monitor with high log scale mode
### To use the default Log Analytics workspace
az aks enable-addons -a monitoring --enable-high-log-scale-mode -g $RESOURCE_GROUP -n $CLUSTER_NAME
### To use an existing Log Analytics workspace
az aks enable-addons -a monitoring --enable-high-log-scale-mode -g $RESOURCE_GROUP -n $CLUSTER_NAME --workspace-resource-id <workspace-resource-id>
# Update the AKS cluster with the enable-container-network-logs flag
az aks update --enable-acns \
--enable-container-network-logs \
-g $RESOURCE_GROUP \
-n $CLUSTER_NAME
```


Note

When enabled, container network flow logs are written to `/var/log/acns/hubble/events.log`

when the `ContainerNetworkLog`

custom resource is applied. If Log Analytics integration is enabled later, the Azure Monitor Agent begins collecting logs at that point. Logs older than two minutes aren't ingested. Only new entries that are appended after monitoring begins are collected in a Log Analytics workspace.

## Existing clusters

Note

If your cluster already has Advanced Container Networking Services (ACNS) enabled, you can start collecting flow logs on the host node by simply applying a ContainerNetworkLog CRD. However, if you want to enable flow logs with Log Analytics workspace integration for persistent storage and advanced analytics, follow the steps in the [Configure integration with log analytics on existing cluster](#configure-integration-with-log-analytics-on-existing-cluster) section.

```
# Set environment variables for your existing cluster. Make sure you replace the placeholders with your own values.
export CLUSTER_NAME="<aks-cluster-name>"
export RESOURCE_GROUP="<aks-resource-group>"
```


### Configure integration with log analytics on existing cluster

To enable container network logs on an existing cluster:

Check whether monitoring add-ons are already enabled on that cluster:

`az aks addon list -g $RESOURCE_GROUP -n $CLUSTER_NAME`

If monitoring add-ons are enabled, disable monitoring add-ons:

`az aks disable-addons -a monitoring -g $RESOURCE_GROUP -n $CLUSTER_NAME`

Complete this step because monitoring add-ons might already be enabled, but not for high scale. For more information, see

[High-scale mode](/en-us/azure/azure-monitor/containers/container-insights-high-scale).Set Azure Monitor to

`enable-high-log-scale-mode`

:`### Use default Log Analytics workspace az aks enable-addons -a monitoring --enable-high-log-scale-mode -g $RESOURCE_GROUP -n $CLUSTER_NAME ### Use existing Log Analytics workspace az aks enable-addons -a monitoring --enable-high-log-scale-mode -g $RESOURCE_GROUP -n $CLUSTER_NAME --workspace-resource-id <workspace-resource-id>`

Update the AKS cluster with the

`enable-container-network-logs`

flag:`az aks update --enable-acns \ --enable-container-network-logs \ -g $RESOURCE_GROUP \ -n $CLUSTER_NAME`

Create the CRD as per the

[ContainerNetworkLog template](#containernetworklog-crd-template)mentioned above and apply it to start log collection in log analytics workspace.Tip

For a practical example of a ContainerNetworkLog custom resource configuration, see the

[sample CRD in the AKS Labs documentation](https://azure-samples.github.io/aks-labs/docs/networking/acns-lab/#enable-flow-logs-for-the-pets-namespace).

**Viewing L7 flows and DNS errors**

To capture Layer 7 (L7) flow data and DNS errors/flows in your container network logs, you must apply Cilium network policies with FQDN filtering and L7 policy support enabled. Without these policies, L7 and DNS-related flow information won't be captured.

Example of a Cilium network policy with FQDN filtering and L7 support:

```
apiVersion: cilium.io/v2
kind: CiliumNetworkPolicy
metadata:
name: l7-dns-policy
namespace: default
spec:
endpointSelector:
matchLabels:
app: myapp
egress:
- toEndpoints:
- matchLabels:
"k8s:io.kubernetes.pod.namespace": kube-system
"k8s:k8s-app": kube-dns
toPorts:
- ports:
- port: "53"
protocol: UDP
rules:
dns:
- matchPattern: "*.example.com"
- toFQDNs:
- matchPattern: "*.example.com"
toPorts:
- ports:
- port: "443"
protocol: TCP
rules:
http:
- method: "GET"
path: "/1"
```


Apply the policy using:

```
kubectl apply -f l7-dns-policy.yaml
```


For more information, see [Configure a Layer 7 policy](how-to-apply-l7-policies) and [Configure an FQDN policy](how-to-apply-fqdn-filtering-policies)

## Common post-setup steps to verify configuration

The following steps apply to both new and existing cluster setups.

### Get cluster credentials

Get your cluster credentials by using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command:

```
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


### Validate the setup

Validate that the retina network flow log capability is enabled:

```
az aks show -g $RESOURCE_GROUP -n $CLUSTER_NAME
```


Expected output:

```
"networkProfile":{
"advancedNetworking": {
"enabled": true,
"observability":{
"enabled": true
}
}
}
----------------------------
"osmagent":{
"config":{
"enableContainerNetworkLogs": "True"
}
}
```


Check which custom resource definitions are installed for flow logs:

```
kubectl get containernetworklog
```


This command lists all the `ContainerNetworkLog`

custom resources created in the cluster.

Validate that the `ContainerNetworkLog`

custom resource is applied:

```
k describe containernetworklog <cr-name>
```


Expect to see a `Spec`

node that contains `Include filters`

and a `Status`

node. The value for `Status`

> `State`

should be `CONFIGURED`

(not `FAILED`

).

```
Spec:
Includefilters:
From:
Namespaced Pod:
namespace/pod-
Name: sample-filter
Protocol:
tcp
To:
Namespaced Pod:
namespace/pod-
Verdict:
dropped
Status:
State: CONFIGURED
Timestamp: 2025-05-01T11:24:48Z
```


Users can apply multiple `ContainerNetworkLog`

custom resources in the cluster. Each custom resource has its own status.

### Querying Container Network Flow Logs in Log Analytics dashboard

When Container Network Flow Logs are enabled with a Log Analytics workspace, you have access to historical logs that allow you to analyze network traffic patterns over time. You can query these logs using the `ContainerNetworkLog`

table to perform detailed forensic analysis and troubleshooting.

Customers can use Kusto Query Language (KQL) to analyze network data in Log Analytics. This historical data is invaluable for understanding network behavior patterns, identifying security incidents, troubleshooting connectivity issues, and performing root cause analysis over extended periods. The ability to correlate network events across time helps detect intermittent issues and understand traffic flows that may not be apparent in real-time monitoring.

To see sample queries that can be applied for troubleshooting connectivity issues, refer to the [progressive diagnosis using flow logs](https://azure-samples.github.io/aks-labs/docs/networking/acns-lab/#progressive-diagnosis-using-flow-logs) in the AKS Labs documentation.

### Azure Managed Grafana

You can access prebuilt Grafana dashboards through the Azure portal. Navigate to either the Azure Monitor resource or your Azure Kubernetes Service (AKS) cluster to view and interact with these dashboards. But before that:

Make sure that the Azure logs pods are running:

`kubectl get pods -o wide -n kube-system | grep ama-logs`

Your output should look similar to the following example:

`ama-logs-9bxc6 3/3 Running 1 (39m ago) 44m ama-logs-fd568 3/3 Running 1 (40m ago) 44m ama-logs-rs-65bdd98f75-hqnd2 2/2 Running 1 (43m ago) 22h`

Ensure that your Managed Grafana workspace can access and search all monitoring data in the relevant subscription. This step is required to access prebuilt dashboards for network flow logs.

**Use case 1**: If you're a subscription Owner or a User Access Administrator, when a Managed Grafana workspace is created, it comes with the Monitoring Reader role granted on all Azure Monitor data and Log Analytics resources in the subscription. The new Managed Grafana workspace can access and search all monitoring data in the subscription. It can view the Azure Monitor metrics and logs from all resources and view any logs stored in Log Analytics workspaces in the subscription.**Use case 2**: If you're not a subscription Owner or User Access Administrator, or if your Log Analytics and Managed Grafana workspaces are in different subscriptions, Grafana can't access Log Analytics and the subscription. The Grafana workspace must have the Monitoring Reader role in the relevant subscription to access prebuilt Grafana dashboards. In this scenario, complete these steps to provide access:In your Managed Grafana workspace, go to

**Settings**>**Identity**.Select

**Azure role assignments**>**Add role assignments**.For

**Scope**, enter**Subscription**. Select your subscription. Set**Role**to**Monitoring Reader**, and then select**Save**.Verify the data source for the Managed Grafana instance. To verify the subscription for the data source for the Grafana dashboards, check the

**Data source**tab in the Managed Grafana instance:


#### Visualization in Grafana dashboards

Azure Monitor dashboards with Grafana enable you to use Grafana's query, transformation, and visualization capabilities on metrics and logs collected in Azure Monitor. You can use this option as an alternative to visualize container network flow logs.

- Navigate to the left pane of the Kubernetes cluster in the Azure portal.
- Select
**Dashboards with Grafana (Preview)**. - Browse the list of available dashboards in the Azure Monitor or Azure Managed Prometheus listings.
- Select a dashboard, for example
**Azure | Insights | Containers | Networking | Flow Logs**.

You can visualize container network flow logs for analysis by using two prebuilt Grafana dashboards. You can access the dashboards either through Azure Managed Grafana or in the Azure portal.

To simplify log analysis, we provide two preconfigured Azure Managed Grafana dashboards:

Go to

**Azure**>**Insights**>**Containers**>**Networking**>**Flow Logs**. This dashboard provides visualizations in which AKS workloads communicate with each other, including network requests, responses, drops, and errors. Currently, you must use[ID 23155](https://grafana.com/grafana/dashboards/23155-azure-insights-containers-networking-flow-logs//)to import these dashboards.Go to

**Azure**>**Insights**>**Containers**>**Networking**>**Flow Logs (External Traffic)**. This dashboard provides visualizations in which AKS workloads send and receive communications from outside an AKS cluster, including network requests, responses, drops, and errors. Use[ID 23156](https://grafana.com/grafana/dashboards/23156-azure-insights-containers-networking-flow-logs-external-traffic//).

For more information about how to use this dashboard, see the [overview of container network logs](container-network-observability-logs).

## Configure on-demand logs mode

On-demand logs mode for network flows works with both Cilium and non-Cilium data planes.

To proceed, you must have an AKS cluster with [Advanced Container Networking Services](advanced-container-networking-services-overview) enabled.

The `az aks create`

command with the Advanced Container Networking Services flag, `--enable-acns`

, creates a new AKS cluster with all Advanced Container Networking Services features. The features include:

**Container Network Observability:**Provides insights into your network traffic. To learn more, visit[Container Network Observability](advanced-container-networking-services-overview#container-network-observability).**Container Network Security:**Offers security features like FQDN filtering. To learn more, visit[Container Network Security](advanced-container-networking-services-overview#container-network-security).

Note

Clusters that have the Cilium data plane support the Container Network Observability and Container Network Security features in Kubernetes version 1.29 and later.

```
# Set an environment variable for the AKS cluster name. Make sure you replace the placeholder with your own value.
export CLUSTER_NAME="<aks-cluster-name>"
# Create an AKS cluster
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--generate-ssh-keys \
--location eastus \
--max-pods 250 \
--network-plugin azure \
--network-plugin-mode overlay \
--network-dataplane cilium \
--node-count 2 \
--pod-cidr 192.168.0.0/16 \
--kubernetes-version 1.33 \
--enable-acns
```


### Enable Advanced Container Networking Services on an existing cluster

The [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`--enable-acns`

flag updates an existing AKS cluster with all Advanced Container Networking Services features. The features include [Container Network Observability](advanced-container-networking-services-overview#container-network-observability)and

[Container Network Security](advanced-container-networking-services-overview#container-network-security).

Note

Only clusters that have the Cilium data plane support the Container Network Security features of Advanced Container Networking Services.

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns
```


Next, get your cluster credentials by using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command:

```
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


### Install the Hubble CLI

Install the Hubble CLI to access the data it collects. Run the following commands:

```
# Set environment variables
export HUBBLE_VERSION=v1.16.3
export HUBBLE_ARCH=amd64
#Install the Hubble CLI
if [ "$(uname -m)" = "aarch64" ]; then HUBBLE_ARCH=arm64; fi
curl -L --fail --remote-name-all https://github.com/cilium/hubble/releases/download/$HUBBLE_VERSION/hubble-linux-${HUBBLE_ARCH}.tar.gz{,.sha256sum}
sha256sum --check hubble-linux-${HUBBLE_ARCH}.tar.gz.sha256sum
sudo tar xzvfC hubble-linux-${HUBBLE_ARCH}.tar.gz /usr/local/bin
rm hubble-linux-${HUBBLE_ARCH}.tar.gz{,.sha256sum}
```


### Visualize the Hubble flows

Make sure that the Hubble pods are running:

`kubectl get pods -o wide -n kube-system -l k8s-app=hubble-relay`

Your output should look similar to the following example:

`hubble-relay-7ddd887cdb-h6khj 1/1 Running 0 23h`

Port-forward the Hubble Relay server:

`kubectl port-forward -n kube-system svc/hubble-relay --address 127.0.0.1 4245:443`

Mutual TLS (mTLS) ensures the security of the Hubble Relay server. To enable the Hubble client to retrieve flows, you must get the appropriate certificates and configure the client with them. Apply the certificates by using the following commands:

`#!/usr/bin/env bash set -euo pipefail set -x # Directory where certificates will be stored CERT_DIR="$(pwd)/.certs" mkdir -p "$CERT_DIR" declare -A CERT_FILES=( ["tls.crt"]="tls-client-cert-file" ["tls.key"]="tls-client-key-file" ["ca.crt"]="tls-ca-cert-files" ) for FILE in "${!CERT_FILES[@]}"; do KEY="${CERT_FILES[$FILE]}" JSONPATH="{.data['${FILE//./\\.}']}" # Retrieve the secret and decode it kubectl get secret hubble-relay-client-certs -n kube-system \ -o jsonpath="${JSONPATH}" | \ base64 -d > "$CERT_DIR/$FILE" # Set the appropriate hubble CLI config hubble config set "$KEY" "$CERT_DIR/$FILE" done hubble config set tls true hubble config set tls-server-name instance.hubble-relay.cilium.io`

Confirm that the secrets were generated:

`kubectl get secrets -n kube-system | grep hubble-`

Your output should look similar to the following example:

`kube-system hubble-relay-client-certs kubernetes.io/tls 3 9d kube-system hubble-relay-server-certs kubernetes.io/tls 3 9d kube-system hubble-server-certs kubernetes.io/tls 3 9d`

Verify that the Hubble Relay pod is running:

`hubble observe --pod hubble-relay-7ddd887cdb-h6khj`


### Visualize by using the Hubble UI

To use the Hubble UI, save the following script in the

`hubble-ui.yaml`

file:`apiVersion: v1 kind: ServiceAccount metadata: name: hubble-ui namespace: kube-system --- kind: ClusterRole apiVersion: rbac.authorization.k8s.io/v1 metadata: name: hubble-ui labels: app.kubernetes.io/part-of: retina rules: - apiGroups: - networking.k8s.io resources: - networkpolicies verbs: - get - list - watch - apiGroups: - "" resources: - componentstatuses - endpoints - namespaces - nodes - pods - services verbs: - get - list - watch - apiGroups: - apiextensions.k8s.io resources: - customresourcedefinitions verbs: - get - list - watch - apiGroups: - cilium.io resources: - "*" verbs: - get - list - watch --- apiVersion: rbac.authorization.k8s.io/v1 kind: ClusterRoleBinding metadata: name: hubble-ui labels: app.kubernetes.io/part-of: retina roleRef: apiGroup: rbac.authorization.k8s.io kind: ClusterRole name: hubble-ui subjects: - kind: ServiceAccount name: hubble-ui namespace: kube-system --- apiVersion: v1 kind: ConfigMap metadata: name: hubble-ui-nginx namespace: kube-system data: nginx.conf: | server { listen 8081; server_name localhost; root /app; index index.html; client_max_body_size 1G; location / { proxy_set_header Host $host; proxy_set_header X-Real-IP $remote_addr; # CORS add_header Access-Control-Allow-Methods "GET, POST, PUT, HEAD, DELETE, OPTIONS"; add_header Access-Control-Allow-Origin *; add_header Access-Control-Max-Age 1728000; add_header Access-Control-Expose-Headers content-length,grpc-status,grpc-message; add_header Access-Control-Allow-Headers range,keep-alive,user-agent,cache-control,content-type,content-transfer-encoding,x-accept-content-transfer-encoding,x-accept-response-streaming,x-user-agent,x-grpc-web,grpc-timeout; if ($request_method = OPTIONS) { return 204; } # /CORS location /api { proxy_http_version 1.1; proxy_pass_request_headers on; proxy_hide_header Access-Control-Allow-Origin; proxy_pass http://127.0.0.1:8090; } location / { try_files $uri $uri/ /index.html /index.html; } # Liveness probe location /healthz { access_log off; add_header Content-Type text/plain; return 200 'ok'; } } } --- kind: Deployment apiVersion: apps/v1 metadata: name: hubble-ui namespace: kube-system labels: k8s-app: hubble-ui app.kubernetes.io/name: hubble-ui app.kubernetes.io/part-of: retina spec: replicas: 1 selector: matchLabels: k8s-app: hubble-ui template: metadata: labels: k8s-app: hubble-ui app.kubernetes.io/name: hubble-ui app.kubernetes.io/part-of: retina spec: serviceAccountName: hubble-ui automountServiceAccountToken: true containers: - name: frontend image: mcr.microsoft.com/oss/cilium/hubble-ui:v0.12.2 imagePullPolicy: Always ports: - name: http containerPort: 8081 livenessProbe: httpGet: path: /healthz port: 8081 readinessProbe: httpGet: path: / port: 8081 resources: {} volumeMounts: - name: hubble-ui-nginx-conf mountPath: /etc/nginx/conf.d/default.conf subPath: nginx.conf - name: tmp-dir mountPath: /tmp terminationMessagePolicy: FallbackToLogsOnError securityContext: {} - name: backend image: mcr.microsoft.com/oss/cilium/hubble-ui-backend:v0.12.2 imagePullPolicy: Always env: - name: EVENTS_SERVER_PORT value: "8090" - name: FLOWS_API_ADDR value: "hubble-relay:443" - name: TLS_TO_RELAY_ENABLED value: "true" - name: TLS_RELAY_SERVER_NAME value: ui.hubble-relay.cilium.io - name: TLS_RELAY_CA_CERT_FILES value: /var/lib/hubble-ui/certs/hubble-relay-ca.crt - name: TLS_RELAY_CLIENT_CERT_FILE value: /var/lib/hubble-ui/certs/client.crt - name: TLS_RELAY_CLIENT_KEY_FILE value: /var/lib/hubble-ui/certs/client.key livenessProbe: httpGet: path: /healthz port: 8090 readinessProbe: httpGet: path: /healthz port: 8090 ports: - name: grpc containerPort: 8090 resources: {} volumeMounts: - name: hubble-ui-client-certs mountPath: /var/lib/hubble-ui/certs readOnly: true terminationMessagePolicy: FallbackToLogsOnError securityContext: {} nodeSelector: kubernetes.io/os: linux volumes: - configMap: defaultMode: 420 name: hubble-ui-nginx name: hubble-ui-nginx-conf - emptyDir: {} name: tmp-dir - name: hubble-ui-client-certs projected: defaultMode: 0400 sources: - secret: name: hubble-relay-client-certs items: - key: tls.crt path: client.crt - key: tls.key path: client.key - key: ca.crt path: hubble-relay-ca.crt --- kind: Service apiVersion: v1 metadata: name: hubble-ui namespace: kube-system labels: k8s-app: hubble-ui app.kubernetes.io/name: hubble-ui app.kubernetes.io/part-of: retina spec: type: ClusterIP selector: k8s-app: hubble-ui ports: - name: http port: 80 targetPort: 8081`

Apply the

`hubble-ui.yaml`

manifest to your cluster:`kubectl apply -f hubble-ui.yaml`

Set up port forwarding for the Hubble UI:

`kubectl -n kube-system port-forward svc/hubble-ui 12000:80`

In your web browser, enter

`http://localhost:12000/`

to access the Hubble UI.

### Basic troubleshooting

Advanced Container Networking Services is a prerequisite to turn on the Azure Monitor Agent log collection feature.

Trying to enable the container network flow logs capability on a cluster without enabling Advanced Container Networking Services, for example:

`az aks update -g test-rg -n test-cluster --enable-container-network-logs`

Results in an error message:

`Flow logs requires '--enable-acns', advanced networking to be enabled, and the monitoring addon to be enabled.`

If the cluster Kubernetes version is earlier than version 1.33.0, trying to run

`--enable-container-network-logs`

results in an error message:`The specified orchestrator version %s is not valid. Advanced Networking Flow Logs is only supported on Kubernetes version 1.33.0 or later.`

where

`%s`

is your Kubernetes version.If you try to run

`--enable-container-network-logs`

on a subscription where the Azure Feature Exposure Control (AFEC) flag isn't enabled, an error message appears:`Feature Microsoft.ContainerService/AdvancedNetworkingFlowLogsPreview is not enabled. Please see https://aka.ms/aks/previews for how to enable features.`

If you try to apply a

`ContainerNetworkLog`

custom resource on a cluster where Advanced Container Networking Services isn't enabled, an error message appears:`error: resource mapping not found for <....>": no matches for kind "ContainerNetworkLog" in version "acn.azure.com/v1alpha1"`

Ensure that you install custom resources first.


### Disable container network logs: Stored logs mode on existing cluster

If all custom resources are deleted, flow log collection stops because no filters are defined for collection.

To disable container network log collection by the Azure Monitor Agent, run:

```
az aks update -n $CLUSTER_NAME -g $RESOURCE_GROUP --disable-container-network-logs
```


## Clean up resources

If you don't plan to use this example application, delete the resources you created in this article by using the [ az group delete](/en-us/cli/azure/#az-group-delete) command.

```
az group delete --name $RESOURCE_GROUP
```


## Related content

- Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview). - Explore the
[Container Network Observability feature](advanced-container-networking-services-overview#container-network-observability)in Advanced Container Networking Services.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deploy-postgresql-ha -->

# Deploy a highly available PostgreSQL database on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you deploy a highly available PostgreSQL database on AKS.

- If you still need to create the required infrastructure for this deployment, follow the steps in
[Create infrastructure for deploying a highly available PostgreSQL database on AKS](create-postgresql-ha)to get set up, and then return to this article.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Create secret for bootstrap app user

- Generate a secret to validate the PostgreSQL deployment by interactive login for a bootstrap app user using the
command.`kubectl create secret`


Important

Microsoft recommends that you use the most secure authentication flow available. The authentication flow described in this procedure requires a high degree of trust in the application and carries risks that are not present in other flows. You should only use this flow when other more secure flows, such as managed identities, aren't viable.

```
PG_DATABASE_APPUSER_SECRET=$(echo -n | openssl rand -base64 16)
kubectl create secret generic db-user-pass \
--from-literal=username=app \
--from-literal=password="${PG_DATABASE_APPUSER_SECRET}" \
--namespace $PG_NAMESPACE \
--context $AKS_PRIMARY_CLUSTER_NAME
```


Validate that the secret was successfully created using the

command.`kubectl get`

`kubectl get secret db-user-pass --namespace $PG_NAMESPACE --context $AKS_PRIMARY_CLUSTER_NAME`


## Set environment variables for the PostgreSQL cluster

Deploy a ConfigMap to configure the CNPG operator using the following

command. These values replace the legacy`kubectl apply`

`ENABLE_AZURE_PVC_UPDATES`

toggle, which is no longer required, and help stagger upgrades and speed up replica reconnections. Before rolling this configuration into production, validate that any existing`DRAIN_TAINTS`

settings you rely on remain compatible with your Azure environment.`cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME -n $PG_NAMESPACE -f - apiVersion: v1 kind: ConfigMap metadata: name: cnpg-controller-manager-config data: CLUSTERS_ROLLOUT_DELAY: '120' STANDBY_TCP_USER_TIMEOUT: '10' EOF`


## Install the Prometheus PodMonitors

Prometheus scrapes CNPG using the recording rules stored in the CNPG GitHub samples repo. Because the operator-managed PodMonitor is being deprecated, create and manage the PodMonitor resource yourself so you can tailor it to your monitoring stack.

Add the Prometheus Community Helm repo using the

command.`helm repo add`

`helm repo add prometheus-community \ https://prometheus-community.github.io/helm-charts`

Upgrade the Prometheus Community Helm repo and install it on the primary cluster using the

command with the`helm upgrade`

`--install`

flag.`helm upgrade --install \ --namespace $PG_NAMESPACE \ -f https://raw.githubusercontent.com/cloudnative-pg/cloudnative-pg/main/docs/src/samples/monitoring/kube-stack-config.yaml \ prometheus-community \ prometheus-community/kube-prometheus-stack \ --kube-context=$AKS_PRIMARY_CLUSTER_NAME`

Create a PodMonitor for the cluster. The CNPG team is deprecating the operator-managed PodMonitor, so you now manage it directly:

`cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE -f - apiVersion: monitoring.coreos.com/v1 kind: PodMonitor metadata: name: $PG_PRIMARY_CLUSTER_NAME namespace: ${PG_NAMESPACE} labels: cnpg.io/cluster: ${PG_PRIMARY_CLUSTER_NAME} spec: selector: matchLabels: cnpg.io/cluster: ${PG_PRIMARY_CLUSTER_NAME} podMetricsEndpoints: - port: metrics EOF`


## Create a federated credential

In this section, you create a federated identity credential for PostgreSQL backup to allow CNPG to use AKS workload identity to authenticate to the storage account destination for backups. The CNPG operator creates a Kubernetes service account with the same name as the cluster named used in the CNPG Cluster deployment manifest.

Get the OIDC issuer URL of the cluster using the

command.`az aks show`

`export AKS_PRIMARY_CLUSTER_OIDC_ISSUER="$(az aks show \ --name $AKS_PRIMARY_CLUSTER_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --query "oidcIssuerProfile.issuerUrl" \ --output tsv)"`

Create a federated identity credential using the

command.`az identity federated-credential create`

`az identity federated-credential create \ --name $AKS_PRIMARY_CLUSTER_FED_CREDENTIAL_NAME \ --identity-name $AKS_UAMI_CLUSTER_IDENTITY_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --issuer "${AKS_PRIMARY_CLUSTER_OIDC_ISSUER}" \ --subject system:serviceaccount:"${PG_NAMESPACE}":"${PG_PRIMARY_CLUSTER_NAME}" \ --audience api://AzureADTokenExchange`


## Deploy a highly available PostgreSQL cluster

In this section, you deploy a highly available PostgreSQL cluster using the [CNPG Cluster custom resource definition (CRD)](https://cloudnative-pg.io/documentation/1.23/cloudnative-pg.v1/#postgresql-cnpg-io-v1-ClusterSpec).

### Cluster CRD parameters

The following table outlines the key properties set in the YAML deployment manifest for the Cluster CRD:

| Property | Definition |
|---|---|
`imageName` |
Points to the CloudNativePG operand container image. Use `ghcr.io/cloudnative-pg/postgresql:18-system-trixie` with the in-core backup integration shown in this guide, or switch to `18-standard-trixie` when you adopt the Barman Cloud plugin. |
`inheritedMetadata` |
Specific to the CNPG operator. The CNPG operator applies the metadata to every object related to the cluster. |
`annotations` |
Includes the DNS label required when exposing the cluster endpoints and enables
`alpha.cnpg.io/failoverQuorum` |

`labels: azure.workload.identity/use: "true"`

`topologySpreadConstraints`

`"workload=postgres"`

.`resources`

*Guaranteed*. In a production environment, these values are key for maximizing usage of the underlying node VM and vary based on the Azure VM SKU used.`probes`

`startDelay`

configuration. Streaming startup and readiness probes help ensure replicas are healthy before serving traffic.`smartShutdownTimeout`

`bootstrap`

`storage`

`postgresql.synchronous`

`minSyncReplicas`

/`maxSyncReplicas`

and lets you specify synchronous replication behavior using the newer schema.`postgresql.parameters`

`postgresql.conf`

, `pg_hba.conf`

, and `pg_ident.conf`

. The sample emphasizes observability and WAL retention defaults that suit the AKS workload identity scenario but should be tuned per workload.`serviceAccountTemplate`

`barmanObjectStore`

To further isolate PostgreSQL workloads, you can add a taint (for example, `node-role.kubernetes.io/postgres=:NoSchedule`

) to your data plane nodes and replace the sample `nodeSelector`

/`tolerations`

with the values recommended by CloudNativePG. If you take this approach, label the nodes accordingly and confirm the AKS autoscaler policies align with your topology.

### PostgreSQL performance parameters

PostgreSQL performance heavily depends on your cluster's underlying resources and workload. The following table provides baseline guidance for a three-node cluster running on Standard D4s v3 nodes (16-GiB memory). Treat these values as a starting point and adjust them once you understand your workload profile:

| Property | Recommended value | Definition |
|---|---|---|
`wal_compression` |
lz4 | Compresses full-page writes written in WAL file with specified method |
`max_wal_size` |
6 GB | Sets the WAL size that triggers a checkpoint |
`checkpoint_timeout` |
15 min | Sets the maximum time between automatic WAL checkpoints |
`checkpoint_completion_target` |
0.9 | Balances checkpoint work across the checkpoint window |
`checkpoint_flush_after` |
2 MB | Number of pages after which previously performed writes are flushed to disk |
`wal_writer_flush_after` |
2 MB | Amount of WAL written out by WAL writer that triggers a flush |
`min_wal_size` |
2 GB | Sets the minimum size to shrink the WAL to |
`max_slot_wal_keep_size` |
10 GB | Upper bound for WAL left to service replication slots |
`shared_buffers` |
4 GB | Sets the number of shared memory buffers used by the server (25% of node memory in this example) |
`effective_cache_size` |
12 GB | Sets the planner's assumption about the total size of the data caches |
`work_mem` |
1/256th of node memory | Sets the maximum memory to be used for query workspaces |
`maintenance_work_mem` |
6.25% of node memory | Sets the maximum memory to be used for maintenance operations |
`autovacuum_vacuum_cost_limit` |
2400 | Vacuum cost amount available before napping, for autovacuum |
`random_page_cost` |
1.1 | Sets the planner's estimate of the cost of a nonsequentially fetched disk page |
`effective_io_concurrency` |
64 | Sets how many simultaneous requests the disk subsystem can handle efficiently |
`maintenance_io_concurrency` |
64 | A variant of "effective_io_concurrency" that is used for maintenance work |

### Deploying PostgreSQL

Deploy the PostgreSQL cluster with the Cluster CRD using the

command.`kubectl apply`

`cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME -n $PG_NAMESPACE -v 9 -f - apiVersion: postgresql.cnpg.io/v1 kind: Cluster metadata: name: $PG_PRIMARY_CLUSTER_NAME annotations: alpha.cnpg.io/failoverQuorum: "true" spec: imageName: ghcr.io/cloudnative-pg/postgresql:18-system-trixie inheritedMetadata: annotations: service.beta.kubernetes.io/azure-dns-label-name: $AKS_PRIMARY_CLUSTER_PG_DNSPREFIX labels: azure.workload.identity/use: "true" instances: 3 smartShutdownTimeout: 30 probes: startup: type: streaming maximumLag: 32Mi periodSeconds: 5 timeoutSeconds: 3 failureThreshold: 120 readiness: type: streaming maximumLag: 0 periodSeconds: 10 failureThreshold: 6 topologySpreadConstraints: - maxSkew: 1 topologyKey: topology.kubernetes.io/zone whenUnsatisfiable: DoNotSchedule labelSelector: matchLabels: cnpg.io/cluster: $PG_PRIMARY_CLUSTER_NAME affinity: nodeSelector: workload: postgres resources: requests: memory: '8Gi' cpu: 2 limits: memory: '8Gi' cpu: 2 bootstrap: initdb: database: appdb owner: app secret: name: db-user-pass dataChecksums: true storage: storageClass: $POSTGRES_STORAGE_CLASS size: 64Gi postgresql: synchronous: method: any number: 1 parameters: wal_compression: lz4 max_wal_size: 6GB max_slot_wal_keep_size: 10GB checkpoint_timeout: 15min checkpoint_completion_target: '0.9' checkpoint_flush_after: 2MB wal_writer_flush_after: 2MB min_wal_size: 2GB shared_buffers: 4GB effective_cache_size: 12GB work_mem: 62MB maintenance_work_mem: 1GB autovacuum_vacuum_cost_limit: "2400" random_page_cost: "1.1" effective_io_concurrency: "64" maintenance_io_concurrency: "64" log_checkpoints: 'on' log_lock_waits: 'on' log_min_duration_statement: '1000' log_statement: 'ddl' log_temp_files: '1024' log_autovacuum_min_duration: '1s' pg_stat_statements.max: '10000' pg_stat_statements.track: 'all' hot_standby_feedback: 'on' pg_hba: - host all all all scram-sha-256 serviceAccountTemplate: metadata: annotations: azure.workload.identity/client-id: "$AKS_UAMI_WORKLOAD_CLIENTID" labels: azure.workload.identity/use: "true" backup: barmanObjectStore: destinationPath: "https://${PG_PRIMARY_STORAGE_ACCOUNT_NAME}.blob.core.windows.net/backups" azureCredentials: inheritFromAzureAD: true retentionPolicy: '7d' EOF`


Note

The sample manifest uses the `ghcr.io/cloudnative-pg/postgresql:18-system-trixie`

image because it works with the in-core Barman Cloud integration shown later. When you're ready to switch to the Barman Cloud plugin, update `spec.imageName`

to `ghcr.io/cloudnative-pg/postgresql:18-standard-trixie`

and follow the [plugin configuration guidance](https://cloudnative-pg.io/plugin-barman-cloud/docs/intro/) before redeploying the cluster.

Important

The example `pg_hba`

entry allows non-TLS access. If you keep this configuration, document the security implications for your team and prefer encrypted connections wherever possible.

Validate that the primary PostgreSQL cluster was successfully created using the

command. The CNPG Cluster CRD specified three instances, which can be validated by viewing running pods once each instance is brought up and joined for replication. Be patient as it can take some time for all three instances to come online and join the cluster.`kubectl get`

`kubectl get pods --context $AKS_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE -l cnpg.io/cluster=$PG_PRIMARY_CLUSTER_NAME`

Example output

`NAME READY STATUS RESTARTS AGE pg-primary-cnpg-r8c7unrw-1 1/1 Running 0 4m25s pg-primary-cnpg-r8c7unrw-2 1/1 Running 0 3m33s pg-primary-cnpg-r8c7unrw-3 1/1 Running 0 2m49s`


Important

If you use local NVMe with Azure Container Storage and a pod remains in the init state with a multi-attach error, the pod is still searching for the volume on a lost node. After the pod starts running, it enters a `CrashLoopBackOff`

state because CNPG creates a new replica on a new node without data and can't find the `pgdata`

directory. To resolve this issue, destroy the affected instance and bring up a new one. Run the following command:

```
kubectl cnpg destroy [cnpg-cluster-name] [instance-number]
```


## Validate the Prometheus PodMonitor is running

The manually created PodMonitor ties the kube-prometheus-stack scrape configuration to the CNPG pods you deployed earlier.

Validate the PodMonitor is running using the [ kubectl get](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_get/) command.

```
kubectl --namespace $PG_NAMESPACE \
--context $AKS_PRIMARY_CLUSTER_NAME \
get podmonitors.monitoring.coreos.com \
$PG_PRIMARY_CLUSTER_NAME \
--output yaml
```


Example output

```
kind: PodMonitor
metadata:
labels:
cnpg.io/cluster: pg-primary-cnpg-r8c7unrw
name: pg-primary-cnpg-r8c7unrw
namespace: cnpg-database
spec:
podMetricsEndpoints:
- port: metrics
selector:
matchLabels:
cnpg.io/cluster: pg-primary-cnpg-r8c7unrw
```


If you're using Azure Monitor for Managed Prometheus, you need to add another pod monitor using the custom group name. Managed Prometheus doesn't pick up the custom resource definitions (CRDs) from the Prometheus community. Aside from the group name, the CRDs are the same. That design lets pod monitors for Managed Prometheus run alongside pod monitors that use the community CRD. If you're not using Managed Prometheus, you can skip this section. Create a new pod monitor:

```
cat <<EOF | kubectl apply --context $AKS_PRIMARY_CLUSTER_NAME --namespace $PG_NAMESPACE -f -
apiVersion: azmonitoring.coreos.com/v1
kind: PodMonitor
metadata:
name: cnpg-cluster-metrics-managed-prometheus
namespace: ${PG_NAMESPACE}
labels:
azure.workload.identity/use: "true"
cnpg.io/cluster: ${PG_PRIMARY_CLUSTER_NAME}
spec:
selector:
matchLabels:
azure.workload.identity/use: "true"
cnpg.io/cluster: ${PG_PRIMARY_CLUSTER_NAME}
podMetricsEndpoints:
- port: metrics
EOF
```


Verify that the pod monitor is created (note the difference in the group name).

```
kubectl --namespace $PG_NAMESPACE \
--context $AKS_PRIMARY_CLUSTER_NAME \
get podmonitors.azmonitoring.coreos.com \
-l cnpg.io/cluster=$PG_PRIMARY_CLUSTER_NAME \
-o yaml
```


### Option A - Azure Monitor workspace

After you deploy the Postgres cluster and the pod monitor, you can view the metrics using the Azure portal in an Azure Monitor workspace.

### Option B - Managed Grafana

Alternatively, after you deploy the Postgres cluster and pod monitors, you can create a metrics dashboard on the Managed Grafana instance created by the deployment script to visualize the metrics exported to the Azure Monitor workspace. You can access the Managed Grafana via the Azure portal. Navigate to the Managed Grafana instance created by the deployment script and select the Endpoint link as shown here:

Selecting the Endpoint link opens a new browser window where you can create dashboards on the Managed Grafana instance. Following the instructions to [configure an Azure Monitor data source](/en-us/azure/azure-monitor/visualize/grafana-plugin#configure-an-azure-monitor-data-source-plug-in), you can then add visualizations to create a dashboard of metrics from the Postgres cluster. After setting up the data source connection, from the main menu, select the Data sources option. You should see a set of data source options for the data source connection as shown here:

On the Managed Prometheus option, select the option to build a dashboard to open the dashboard editor. After the editor window opens, select the Add visualization option then select the Managed Prometheus option to browse the metrics from the Postgres cluster. After you select the metric you want to visualize, select the Run queries button to fetch the data for the visualization as shown here:

Select the Save icon to add the panel to your dashboard. You can add other panels by selecting the Add button in the dashboard editor and repeating this process to visualize other metrics. Adding the metrics visualizations, you should have something that looks like this:

Select the Save icon to save your dashboard.

## Next steps

## Contributors

*Microsoft maintains this article. The following contributors originally wrote it:*

- Ken Kilty | Principal TPM
- Russell de Pina | Principal TPM
- Adrian Joian | Senior Customer Engineer
- Jenny Hayes | Senior Content Developer
- Carol Smith | Senior Content Developer
- Erin Schaffer | Content Developer 2
- Adam Sharif | Customer Engineer 2

## Acknowledgment

This documentation was jointly developed with EnterpriseDB, the maintainers of the CloudNativePG operator. We thank [Gabriele Bartolini](https://cloudnative-pg.io/authors/gbartolini/) for reviewing earlier drafts of this document and offering technical improvements.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-cluster-security -->

# Best practices for cluster security and upgrades in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you manage clusters in Azure Kubernetes Service (AKS), workload and data security is a key consideration. When you run multi-tenant clusters using logical isolation, you especially need to secure resource and workload access. Minimize the risk of attack by applying the latest Kubernetes and node OS security updates.

This article focuses on how to secure your AKS cluster. You learn how to:

- Use Microsoft Entra ID and Kubernetes role-based access control (Kubernetes RBAC) to secure API server access.
- Secure container access to node resources.
- Upgrade an AKS cluster to the latest Kubernetes version.
- Keep nodes up to date and automatically apply security patches.

You can also read the best practices for [container image management](operator-best-practices-container-image-management) and for [pod security](developer-best-practices-pod-security).

## Enable threat protection


Best practice guidanceYou can enable

[Defender for Containers]to help secure your containers. Defender for Containers can assess cluster configurations and provide security recommendations, run vulnerability scans, and provide real-time protection and alerting for Kubernetes nodes and clusters.

## Secure access to the API server and cluster nodes


Best practice guidanceOne of the most important ways to secure your cluster is to secure access to the Kubernetes API server. To control access to the API server, integrate Kubernetes RBAC with Microsoft Entra ID. With these controls,you secure AKS the same way that you secure access to your Azure subscriptions.


The Kubernetes API server provides a single connection point for requests to perform actions within a cluster. To secure and audit access to the API server, limit access and provide the lowest possible permission levels. while this approach isn't unique to Kubernetes, it's especially important when you've logically isolated your AKS cluster for multi-tenant use.

Microsoft Entra ID provides an enterprise-ready identity management solution that integrates with AKS clusters. Since Kubernetes doesn't provide an identity management solution, you may be hard-pressed to granularly restrict access to the API server. With Microsoft Entra integrated clusters in AKS, you use your existing user and group accounts to authenticate users to the API server.

Using Kubernetes RBAC and Microsoft Entra ID-integration, you can secure the API server and provide the minimum permissions required to a scoped resource set, like a single namespace. You can grant different Microsoft Entra users or groups different Kubernetes roles. With granular permissions, you can restrict access to the API server and provide a clear audit trail of actions performed.

The recommended best practice is to use *groups* to provide access to files and folders instead of individual identities. For example, use a Microsoft Entra ID *group* membership to bind users to Kubernetes roles rather than individual *users*. As a user's group membership changes, their access permissions on the AKS cluster change accordingly.

Meanwhile, let's say you bind the individual user directly to a role and their job function changes. While the Microsoft Entra group memberships update, their permissions on the AKS cluster would not. In this scenario, the user ends up with more permissions than they require.

For more information about Microsoft Entra integration, Kubernetes RBAC, and Azure RBAC, see [Best practices for authentication and authorization in AKS](concepts-identity).

## Restrict access to Instance Metadata API


Best practice guidanceAdd a network policy in all user namespaces to block pod egress to the metadata endpoint.


Note

To implement Network Policy, include the attribute `--network-policy azure`

when creating the AKS cluster. Use the following command to create the cluster:
`az aks create -g myResourceGroup -n myManagedCluster --network-plugin azure --network-policy azure --generate-ssh-keys`


```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: restrict-instance-metadata
spec:
podSelector:
matchLabels: {}
policyTypes:
- Egress
egress:
- to:
- ipBlock:
cidr: 10.10.0.0/0#example
except:
- 169.254.169.254/32
```


## Secure container access to resources


Best practice guidanceLimit access to actions that containers can perform. Provide the least number of permissions, and avoid the use of root access or privileged escalation.


In the same way that you should grant users or groups the minimum privileges required, you should also limit containers to only necessary actions and processes. To minimize the risk of attack, avoid configuring applications and containers that require escalated privileges or root access.

Using user-namespaces, you improve the host isolation and limit the lateral movement in case of container breakouts. These improvements are significant whether the pod is running as root or not.

For even more granular control of container actions, you can also use built-in Linux security features such as *AppArmor* and *seccomp*.

For more information, see [Secure container access to resources](secure-container-access).

## Regularly update to the latest version of Kubernetes


Best practice guidanceTo stay current on new features and bug fixes, regularly upgrade the Kubernetes version in your AKS cluster.


Kubernetes releases new features at a quicker pace than more traditional infrastructure platforms. Kubernetes updates include:

- New features
- Bug or security fixes

New features typically move through *alpha* and *beta* status before they become *stable*. Once stable, are generally available and recommended for production use. Kubernetes new feature release cycle allows you to update Kubernetes without regularly encountering breaking changes or adjusting your deployments and templates.

AKS supports three minor versions of Kubernetes. Once a new minor patch version is introduced, the oldest minor version and patch releases supported are retired. Minor Kubernetes updates happen on a periodic basis. To stay within support, ensure you have a governance process to check for necessary upgrades. For more information, see [Supported Kubernetes versions AKS](supported-kubernetes-versions).

To check the versions that are available for your cluster, use the [az aks get-upgrades](/en-us/cli/azure/aks#az-aks-get-upgrades) command as shown in the following example:

```
az aks get-upgrades --resource-group myResourceGroup --name myAKSCluster --output table
```


You can then upgrade your AKS cluster using the [az aks upgrade](/en-us/cli/azure/aks#az-aks-upgrade) command. The upgrade process safely:

- Cordons and drains one node at a time.
- Schedules pods on remaining nodes.
- Deploys a new node running the latest OS and Kubernetes versions.

Important

Test new minor versions in a dev test environment and validate that your workload remains healthy with the new Kubernetes version.

Kubernetes may deprecate APIs (like in version 1.16) that your workloads rely on. When bringing new versions into production, consider using [multiple node pools on separate versions](create-node-pools) and upgrade individual pools one at a time to progressively roll the update across a cluster. If running multiple clusters, upgrade one cluster at a time to progressively monitor for impact or changes.

```
az aks upgrade --resource-group myResourceGroup --name myAKSCluster --kubernetes-version KUBERNETES_VERSION
```


For more information about upgrades in AKS, see [Supported Kubernetes versions in AKS](supported-kubernetes-versions) and [Upgrade an AKS cluster](upgrade-cluster).

## Process Linux node updates

Each evening, Linux nodes in AKS get security patches through their distro update channel. This behavior is automatically configured as the nodes are deployed in an AKS cluster. To minimize disruption and potential impact to running workloads, nodes are not automatically rebooted if a security patch or kernel update requires it. For more information about how to handle node reboots, see [Apply security and kernel updates to nodes in AKS](node-updates-kured).

### Node image upgrades

Unattended upgrades apply updates to the Linux node OS, but the image used to create nodes for your cluster remains unchanged. If a new Linux node is added to your cluster, the original image is used to create the node. This new node will receive all the security and kernel updates available during the automatic check every night but will remain unpatched until all checks and restarts are complete. You can use node image upgrade to check for and update node images used by your cluster. For more information on node image upgrade, see [Azure Kubernetes Service (AKS) node image upgrade](node-image-upgrade).

## Process Windows Server node updates

For Windows Server nodes, regularly perform a node image upgrade operation to safely cordon and drain pods and deploy updated nodes.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/windows-vs-linux-containers -->

# Windows container considerations with Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create deployments that use Windows Server containers on Azure Kubernetes Service (AKS), there are a few differences relative to Linux deployments you should keep in mind. For a detailed comparison of the differences between Windows and Linux in upstream Kubernetes, see [Windows containers in Kubernetes](https://kubernetes.io/docs/concepts/windows/intro/).

Some of the major differences include:

**Identity**: Windows Server uses a larger binary security identifier (SID) that's stored in the Windows Security Access Manager (SAM) database. This database isn't shared between the host and containers or between containers.**File permissions**: Windows Server uses an access control list based on SIDs rather than a bitmask of permissions and UID+GID.**File paths**: The convention on Windows Server is to use \ instead of /. In pod specs that mount volumes, specify the path correctly for Windows Server containers. For example, rather than a mount point of*/mnt/volume*in a Linux container, specify a drive letter and location such as*/K/Volume*to mount as the*K:*drive.

Note

[Windows Server 2019 retires on March 1, 2026](https://github.com/Azure/AKS/issues/4091). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2019 on any Kubernetes version. All existing node pools with Windows Server 2019 will be unsupported. Windows Server 2019 is not supported in Kubernetes version 1.33 and above. Starting on April 1, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail.[Windows Server 2022 retires on March 15, 2027](https://github.com/Azure/AKS/issues/4168). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2022 on any Kubernetes version. All existing node pools with Windows Server 2022 will be unsupported. Windows Server 2022 is not supported in Kubernetes version 1.36 and above. Starting on April 1, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail.

For more information, see [AKS release notes](https://github.com/Azure/AKS/releases). To stay up to date on the latest Windows Server OS versions and learn more about our roadmap of what's planned for support on AKS, see our [AKS public roadmap](https://github.com/azure/aks/projects/1).

This article covers important considerations to keep in mind when using Windows containers instead of Linux containers in Kubernetes. For an in-depth comparison of Windows and Linux containers, see [Comparison with Linux](https://kubernetes.io/docs/concepts/windows/intro/#compatibility-linux-similarities).

## Considerations

| Feature | Windows considerations |
|---|---|
|

*must*be Linux.• The maximum number of nodes per cluster is 5000.

• The Windows Server node pool name has a limit of six characters.

[Privileged containers](use-windows-hpc#limitations)**HostProcess Containers (HPC) containers**.[HPC containers](use-windows-hpc#limitations)[Create a Windows HostProcess pod](https://kubernetes.io/docs/tasks/configure-pod-container/create-hostprocess-pod/).[Azure Network Policy Manager (Azure)](use-network-policies#overview-of-network-policy)• Named ports

• SCTP protocol

• Negative match labels or namespace selectors (all labels except "debug=true")

• "except" CIDR blocks (a CIDR with exceptions)

• Windows Server 2019

[Node upgrade](manage-node-pools#upgrade-a-single-node-pool)[node image upgrade](node-image-upgrade). These upgrades deploy new nodes with the latest Window Server 2019 and Windows Server 2022 base node image and security patches.[AKS Image Cleaner](image-cleaner#limitations)[BYOCNI](use-byo-cni)[Open Service Mesh](open-service-mesh-about)[GPU](use-windows-gpu)[Multi-instance GPU](gpu-multi-instance)[Generation 2 VMs](generation-2-vms)[Custom node config](custom-node-configuration)•

[kubelet](custom-node-configuration#kubelet-configuration): Supported.• OS config: Not supported.

## Next steps

For more information on Windows containers, see the [Windows Server containers FAQ](windows-faq).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-cni-overlay-pod-expand -->

# Expand pod CIDR space in Azure CNI Overlay Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can expand your pod Classless Inter-Domain Routing (CIDR) space on Azure CNI Overlay clusters in Azure Kubernetes Service with Linux nodes only. The operation uses the [ az aks update](/en-us/cli/azure/aks#az_aks_update) command and allows expansions without the need to re-create your AKS cluster.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Requirements and parameters

| Requirement or parameter | Supported versions or values | Description |
|---|---|---|
| Feature flag | `EnableAzureCNIOverlayPodCIDRExpansion` |
This feature flag must be registered in your subscription to enable pod CIDR expansion in Azure CNI Overlay AKS clusters. |
| Azure CLI version | 2.48.0 or later | The Azure CLI version must be 2.48.0 or later to support the pod CIDR expansion feature. |
| Kubernetes version | 1.33 | Pod CIDR expansion is supported only on AKS clusters running Kubernetes version 1.33. |
| Node operating system | Linux | Pod CIDR expansion is supported only on Azure CNI Overlay AKS clusters with Linux nodes. |
| Networking mode | Azure CNI Overlay | Pod CIDR expansion is supported only on AKS clusters that use Azure CNI Overlay networking. |
| Example original pod CIDR | `10.244.0.0/18` |
This is an example of a starting pod CIDR block. |
| Example expanded pod CIDR | `10.244.0.0/16` |
This is an example of a target expanded pod CIDR block. |

## Limitations

- Windows nodes and hybrid node scenarios aren't supported.
- Shrinking or changing the pod CIDR isn't supported.
- Adding a discontinuous pod CIDR isn't supported. The new pod CIDR must be a larger superset that contains the complete original range.
- IPv6 pod CIDR expansion isn't supported.
- Changing multiple pod CIDR blocks via
`--pod-cidrs`

isn't supported. - If an
[Azure availability zone](availability-zones)is down during the expansion operation, new nodes might appear as`unready`

. You can expect these nodes to reconcile after the availability zone is up.

## Prerequisites

- You need an Azure subscription. If you don't have an Azure subscription, create a
[free account](https://azure.microsoft.com/free/)before you begin. - Ensure that you meet the requirements listed in the
[Requirements and parameters](#requirements-and-parameters)section.

## Register the `EnableAzureCNIOverlayPodCIDRExpansion`

feature flag

Register the

`EnableAzureCNIOverlayPodCIDRExpansion`

feature flag by using thecommand:`az feature register`

`az feature register --namespace Microsoft.ContainerService --name EnableAzureCNIOverlayPodCIDRExpansion`

Verify successful registration by using the

command. It takes a few minutes for the registration to finish.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "EnableAzureCNIOverlayPodCIDRExpansion"`

After the feature shows

`Registered`

, refresh the registration of the`Microsoft.ContainerService`

resource provider by using thecommand:`az provider register`

`az provider register --namespace Microsoft.ContainerService`


## Update an Azure CNI Overlay AKS cluster to expand the pod CIDR space

Starting from a pod CIDR block of

`10.244.0.0/18`

, you can expand the pod CIDR space by using thecommand. For example:`az aks update`

`az aks update \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --pod-cidr 10.244.0.0/16`

Note

Although the update operation might successfully finish and show the new pod CIDR in the network profile, be sure to validate the new cluster state through

`NodeNetworkConfig`

(`nnc`

).Verify the state of the upgrade operation by checking

`NodeNetworkConfig`

(`nnc`

) via the`kubectl get nnc`

command. In the output, all node pools should match your new pod CIDR block (for example,`10.244.0.0/16`

).`kubectl get nnc -A -o jsonpath='{range .items[*]}{.metadata.name}{" "}{.status.networkContainers[0].subnetAddressSpace}{"\n"}{end}'`


## Related content

To learn more about Azure CNI Overlay networking on AKS, see the following articles:
