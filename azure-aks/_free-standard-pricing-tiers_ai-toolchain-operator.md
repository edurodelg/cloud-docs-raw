---
merged_at: 2026-01-25T12:25:33.941689
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: free-standard-pricing-tiers.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/free-standard-pricing-tiers -->

# Free, Standard, and Premium pricing tiers for Azure Kubernetes Service (AKS) cluster management

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Manage your Azure Kubernetes Service (AKS) clusters using AKS pricing tiers. This article explains the differences between these tiers, when to use each tier, and how to create or update AKS clusters using Azure CLI.

## About AKS pricing tiers

AKS offers three pricing tiers for cluster management: the **Free tier**, the **Standard tier**, and the **Premium tier**.

**SKU and tier relationship**:

**Base SKU clusters**: Can use any of the three pricing tiers (Free, Standard, or Premium).**Automatic SKU clusters**: Must use the Standard tier (automatically selected during cluster creation).

## AKS pricing tiers comparison

The following table compares the Free, Standard, and Premium pricing tiers for AKS cluster management:

| Tier | When to use | Supported cluster types | Pricing | Feature comparison |
|---|---|---|---|---|
| Free | • Development/testing environments. • Learning and evaluation scenarios. • Non-production workloads. |
• Development clusters or small scale testing environments. • Clusters with fewer than 10 nodes. |
• Free cluster management. • Pay-as-you-go for resources you consume. |
• Recommended for clusters with fewer than 10 nodes, but can support up to 1,000 nodes. • Includes all current AKS features. |
| Standard | • Production workloads requiring 99.9-99.95% API server uptime. • Workloads needing financial service level agreement (SLA) coverage. |
• Default tier for Automatic SKU clusters. • Enterprise-grade or production workloads. • Clusters with up to 5,000 nodes. |
• Pay-as-you-go for resources you consume. •
|
• Uptime SLA is enabled by default. • Greater cluster reliability. • Supports up to 5,000 nodes in a cluster. • Includes all current AKS features. |
| Premium | • Production workloads requiring 99.9-99.95% API server uptime. • Workloads requiring 24-month
• Regulated environments requiring extended maintenance. |
• Enterprise-grade or production workloads. • Clusters with up to 5,000 nodes. |
• Pay-as-you-go for resources you consume. •
|
• Includes all current AKS features. •
|

## Uptime SLA terms and conditions

Standard and Premium tiers include Uptime SLA by default:

**With availability zones**: 99.95% availability of the Kubernetes API server**Without availability zones**: 99.9% availability of the Kubernetes API server**Free tier**: Best-effort uptime (no SLA guarantee)

For more information, see the [SLA](https://azure.microsoft.com/support/legal/sla/kubernetes-service/v1_1/).

## Region availability

The following tables outline the availability of AKS pricing tiers by region:

| Region type | Available pricing tiers |
|---|---|
| Public regions and Azure Government regions where
|

- Standard tier

- Premium tier

[Private AKS clusters](private-clusters)in all public regions where AKS is supported- Standard tier

- Premium tier

## Prerequisites

- You need
[Azure CLI](/en-us/cli/azure/install-azure-cli)version 2.47.0 or later. Find the current version using the`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You can create your cluster in an existing resource group or create a new one. To learn more about resource groups and working with them, see
[managing resource groups using the Azure CLI](/en-us/azure/azure-resource-manager/management/manage-resource-groups-cli).

## Create a resource group

Create a resource group using the

command.`az group create`

`# Set environment variables export REGION=<your-region> export RESOURCE_GROUP=<your-resource-group-name> # Create the resource group az group create --name $RESOURCE_GROUP --location $REGION`

Results:

`{ "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/"<your-resource-group-name>", "location": "<your-region>", "managedBy": null, "name": "<your-resource-group-name>", "properties": { "provisioningState": "Succeeded" }, "tags": null, "type": "Microsoft.Resources/resourceGroups" }`


## Create an AKS cluster in the Free tier

Create an AKS cluster in the Free tier using the

command with the`az aks create`

`--tier`

parameter set to`free`

.`# Set environment variables export RESOURCE_GROUP=<your-resource-group-name> export CLUSTER_NAME=<your-aks-cluster-name> # Create the AKS cluster az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --tier free \ --generate-ssh-keys`

Results:

`{ ... "sku": { "name": "Base", "tier": "Free" }, ... }`


## Create an AKS cluster in the Standard tier

Create an AKS cluster in the Standard tier using the

command with the`az aks create`

`--tier`

parameter set to`standard`

.`# Set environment variables export RESOURCE_GROUP=<your-resource-group-name> export CLUSTER_NAME=<your-aks-cluster-name> # Create the AKS cluster az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --tier standard \ --generate-ssh-keys`

Results:

`{ ... "sku": { "name": "Base", "tier": "Standard" }, ... }`


## Create an AKS cluster in the Premium tier

Important

When creating a cluster in the Premium tier, you must also enable the [LTS plan](long-term-support) by setting the `--k8s-support-plan`

parameter to `AKSLongTermSupport`

. You should enable/disable LTS and the Premium tier together.

Create an AKS cluster in the Premium tier using the

command with the`az aks create`

`--tier`

parameter set to`premium`

and the`--k8s-support-plan`

parameter set to`AKSLongTermSupport`

.`# Set environment variables export RESOURCE_GROUP=<your-resource-group-name> export CLUSTER_NAME=<your-aks-cluster-name> # Create the AKS cluster az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --tier premium \ --k8s-support-plan AKSLongTermSupport \ --generate-ssh-keys`

Results:

`{ ... "sku": { "name": "Base", "tier": "Premium" }, "supportPlan": "AKSLongTermSupport", ... }`


## Update an existing cluster from the Standard tier to the Free tier

Update an existing cluster from the Standard tier to the Free tier using the

command with the`az aks update`

`--tier`

parameter set to`free`

.`# Set environment variables export RESOURCE_GROUP=<your-resource-group-name> export CLUSTER_NAME=<your-aks-cluster-name> # Update the AKS cluster az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --tier free`

Results:

`{ ... "sku": { "name": "Base", "tier": "Free" }, ... }`


## Update an existing cluster from the Free tier to the Standard tier

Update an existing cluster from the Free tier to the Standard tier using the

command with the`az aks update`

`--tier`

parameter set to`standard`

.`# Set environment variables export RESOURCE_GROUP=<your-resource-group-name> export CLUSTER_NAME=<your-aks-cluster-name> # Update the AKS cluster az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --tier standard`

Results:

`{ ... "sku": { "name": "Base", "tier": "Standard" }, ... }`


## Update an existing cluster to or from the Premium tier

Important

[Updating existing clusters to or from the Premium tier](long-term-support#enable-lts-on-an-existing-cluster) requires changing the support plan.

### Update an existing cluster to the Premium tier

Update an existing cluster to the Premium tier using the

command with the`az aks update`

`--tier`

parameter set to`premium`

and the`--k8s-support-plan`

parameter set to`AKSLongTermSupport`

.`# Set environment variables export RESOURCE_GROUP=<your-resource-group-name> export CLUSTER_NAME=<your-aks-cluster-name> # Update the AKS cluster az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --tier premium --k8s-support-plan AKSLongTermSupport`

Results:

`{ ... "sku": { "name": "Base", "tier": "Premium" }, "supportPlan": "AKSLongTermSupport", ... }`


### Update an existing cluster from the Premium tier to the Free or Standard tier

Update an existing cluster from the Premium tier to the Free or Standard tier using the

command with the`az aks update`

`--tier`

parameter set to`free`

or`standard`

and the`--k8s-support-plan`

parameter set to`KubernetesOfficial`

. The following example shows updating to the Free tier.`# Set environment variables export RESOURCE_GROUP=<your-resource-group-name> export CLUSTER_NAME=<your-aks-cluster-name> # Update the AKS cluster az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --tier free --k8s-support-plan KubernetesOfficial`

Results:

`{ ... "sku": { "name": "Base", "tier": "Free" }, "supportPlan": "KubernetesOfficial", ... }`


## Update an existing cluster from the Base SKU to the Automatic SKU

Important

Make sure all the [AKS Automatic features](intro-aks-automatic) are enabled on your cluster before updating.

Update an existing cluster from the Base SKU to the Automatic SKU using the

command with the`az aks update`

`--sku`

parameter set to`Automatic`

.`# Set environment variables export RESOURCE_GROUP=<your-resource-group-name> export CLUSTER_NAME=<your-aks-cluster-name> # Update the AKS cluster az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --sku Automatic`

Results:

`{ ... "sku": { "name": "Automatic", "tier": "Standard" }, ... }`


## Update an existing cluster from the Automatic SKU to the Base SKU

Update an existing cluster from the Automatic SKU to the Base SKU using the

command with the`az aks update`

`--sku`

parameter set to`Base`

.`# Set environment variables export RESOURCE_GROUP=<your-resource-group-name> export CLUSTER_NAME=<your-aks-cluster-name> # Update the AKS cluster az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --sku Base`

Results:

`{ ... "sku": { "name": "Base", "tier": "Standard" }, ... }`


## Related content

- Use
[availability zones](availability-zones)to increase high availability with your AKS cluster workloads. [Limit egress traffic](limit-egress-traffic)on AKS clusters to meet security and compliance requirements.


---

<!-- DOCUMENTO FUSIONADO: ai-toolchain-operator.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/ai-toolchain-operator -->

# Deploy an AI model on Azure Kubernetes Service (AKS) with the AI toolchain operator add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to use the AI toolchain operator add-on to efficiently self-host large language models on Kubernetes, reducing costs and resource complexity, enhancing customization, and maintaining full control over your data.

## About KAITO

Self-hosting large language models (LLMs) on Kubernetes is gaining momentum among organizations with inference workloads at scale, such as batch processing, chatbots, agents, and AI-driven applications. These organizations often have access to commercial-grade GPUs and are seeking alternatives to costly per-token API pricing models, which can quickly scale out of control. Many also require the ability to fine-tune or customize their models, a capability typically restricted by closed-source API providers. Additionally, companies handling sensitive or proprietary data - especially in regulated sectors such as finance, healthcare, or defense - prioritize self-hosting to maintain strict control over data and prevent exposure through third-party systems.

To address these needs and more, the [Kubernetes AI Toolchain Operator (KAITO)](https://github.com/kaito-project/kaito), a Cloud Native Computing Foundation (CNCF) Sandbox project, simplifies the process of deploying and managing open-source LLM workloads on Kubernetes. KAITO integrates with vLLM, a high-throughput inference engine designed to serve large language models efficiently. vLLM as an inference engine helps reduce memory and GPU requirements without significantly compromising accuracy.

Built on top of the open-source KAITO project, the AI toolchain operator managed add-on offers a modular, plug-and-play setup that allows teams to quickly deploy models and expose them via production-ready APIs. It includes built-in features like OpenAI-compatible APIs, prompt formatting, and streaming response support. When deployed on an AKS cluster, KAITO ensures data stays within your organization’s controlled environment, providing a secure, compliant alternative to cloud-hosted LLM APIs.

## Before you begin

- This article assumes a basic understanding of Kubernetes concepts. For more information, see
[Kubernetes core concepts for AKS](concepts-clusters-workloads). - For
and default resource configuration, see the**all hosted model preset images**[KAITO GitHub repository](https://github.com/kaito-project/kaito/tree/main/presets). - The AI toolchain operator add-on currently supports KAITO
**version 0.6.0**, please make a note of this in considering your choice of model from the KAITO model repository.

## Limitations

`AzureLinux`

and`Windows`

OS SKU are not currently supported.- AMD GPU VM sizes are not supported
`instanceType`

in a KAITO workspace. - AI toolchain operator add-on is supported in
**public**Azure regions.

## Prerequisites

If you don't have an Azure subscription, create a

[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.If you have multiple Azure subscriptions, make sure you select the correct subscription in which the resources will be created and charged using the

[az account set](/en-us/cli/azure/account#az-account-set)command.Note

Your Azure subscription must have GPU VM quota recommended for your model deployment in the same Azure region as your AKS resources.


Azure CLI version 2.76.0 or later installed and configured. Run

`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).The Kubernetes command-line client, kubectl, installed and configured. For more information, see

[Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

### Export environment variables

To simplify the configuration steps in this article, you can define environment variables using the following commands. Make sure to replace the placeholder values with your own.

`export AZURE_SUBSCRIPTION_ID="mySubscriptionID" export AZURE_RESOURCE_GROUP="myResourceGroup" export AZURE_LOCATION="myLocation" export CLUSTER_NAME="myClusterName"`


## Enable the AI toolchain operator add-on on an AKS cluster

The following sections describe how to create an AKS cluster with the AI toolchain operator add-on enabled and deploy a default hosted AI model.

### Create an AKS cluster with the AI toolchain operator add-on enabled

Create an Azure resource group using the

[az group create](/en-us/cli/azure/group#az-group-create)command.`az group create --name $AZURE_RESOURCE_GROUP --location $AZURE_LOCATION`

Create an AKS cluster with the AI toolchain operator add-on enabled using the

[az aks create](/en-us/cli/azure/aks#az-aks-create)command with the`--enable-ai-toolchain-operator`

and`--enable-oidc-issuer`

flags.`az aks create --location $AZURE_LOCATION \ --resource-group $AZURE_RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-ai-toolchain-operator \ --enable-oidc-issuer \ --generate-ssh-keys`

On an existing AKS cluster, you can enable the AI toolchain operator add-on using the

[az aks update](/en-us/cli/azure/aks#az-aks-update)command.`az aks update --name $CLUSTER_NAME \ --resource-group $AZURE_RESOURCE_GROUP \ --enable-ai-toolchain-operator \ --enable-oidc-issuer`


## Connect to your cluster

Configure

`kubectl`

to connect to your cluster using the[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command.`az aks get-credentials --resource-group $AZURE_RESOURCE_GROUP --name $CLUSTER_NAME`

Verify the connection to your cluster using the

`kubectl get`

command.`kubectl get nodes`


## Deploy a default hosted AI model

KAITO offers a range of small to large language models hosted as public container images, which can be deployed in one step using a KAITO workspace. You can browse the preset LLM images available in the [KAITO model registry](https://github.com/kaito-project/kaito/tree/main/presets). In this section, we'll use the high-performant multimodal [Microsoft Phi-4-mini](https://techcommunity.microsoft.com/blog/educatordeveloperblog/welcome-to-the-new-phi-4-models---microsoft-phi-4-mini--phi-4-multimodal/4386037) language model as an example:

Deploy the

[Phi-4-mini instruct](https://huggingface.co/microsoft/Phi-4-mini-instruct)model preset for inference from the KAITO model repository using the`kubectl apply`

command.`kubectl apply -f https://raw.githubusercontent.com/kaito-project/kaito/refs/heads/main/examples/inference/kaito_workspace_phi_4_mini.yaml`

Track the live resource changes in your workspace using the

`kubectl get`

command.`kubectl get workspace workspace-phi-4-mini -w`

Note

As you track the KAITO workspace deployment, note that machine readiness can take up to 10 minutes, and workspace readiness up to 20 minutes depending on the size of your model.

Check your inference service and get the service IP address using the

`kubectl get svc`

command.`export SERVICE_IP=$(kubectl get svc workspace-phi-4-mini -o jsonpath='{.spec.clusterIP}')`

Test the Phi-4-mini instruct inference service with a sample input of your choice using the

[OpenAI chat completions API format](https://platform.openai.com/docs/api-reference/chat):`kubectl run -it --rm --restart=Never curl --image=curlimages/curl -- curl -X POST http://$SERVICE_IP/v1/completions -H "Content-Type: application/json" \ -d '{ "model": "phi-4-mini-instruct", "prompt": "How should I dress for the weather today?", "max_tokens": 10 }'`


## Deploy a custom or domain-specific LLM

Open-source LLMs are often trained in different contexts and domains, and the hosted model presets may not always fit the requirements of your application or data. In this case, KAITO also supports inference deployment of newer or domain-specific language models from [HuggingFace](https://huggingface.co/). Try out a custom model inference deployment with KAITO by following [this article](kaito-custom-inference-model).

## Clean up resources

If you no longer need these resources, you can delete them to avoid incurring extra Azure compute charges.

Delete the KAITO workspace using the

`kubectl delete workspace`

command.`kubectl delete workspace workspace-phi-4-mini`

You need to manually delete the GPU node pools provisioned by the KAITO deployment. Use the node label created by

[Phi-4-mini instruct workspace](https://raw.githubusercontent.com/kaito-project/kaito/refs/heads/main/examples/inference/kaito_workspace_phi_4_mini.yaml)to get the node pool name using thecommand. In this example, the node label is "kaito.sh/workspace": "workspace-phi-4-mini".`az aks nodepool list`

`az aks nodepool list --resource-group $AZURE_RESOURCE_GROUP --cluster-name $CLUSTER_NAME`

[Delete the node pool](delete-node-pool)with this name from your AKS cluster and repeat the steps in this section for each KAITO workspace that will be removed.

## Common troubleshooting scenarios

After applying the KAITO model inference workspace, your resource readiness and workspace conditions might not update to `True`

for the following reasons:

- Your Azure subscription doesn't have quota for the minimum GPU instance type specified in your KAITO workspace. You'll need to
[request a quota increase](/en-us/azure/quotas/quickstart-increase-quota-portal)for the GPU VM family in your Azure subscription. - The GPU instance type isn't available in your AKS region. Confirm the
[GPU instance availability in your specific region](https://azure.microsoft.com/explore/global-infrastructure/products-by-region/?regions=&products=virtual-machines)and switch the Azure region if your GPU VM family isn't available.

## Next steps

Learn more about KAITO model deployment options below:

- Deploy LLMs with your application on AKS using
[KAITO in Visual Studio Code](aks-extension-kaito). [Monitor your KAITO inference workload](ai-toolchain-operator-monitoring).[Fine tune a model](ai-toolchain-operator-fine-tune)with the AI toolchain operator add-on on AKS.- Configure and test
[tool calling with KAITO inference](ai-toolchain-operator-tool-calling). - Integrate an
[MCP server with the AI toolchain operator](ai-toolchain-operator-mcp)add-on on AKS.
