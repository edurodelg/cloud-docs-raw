---
merged_at: 2026-02-04T00:17:48.863054
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-fine-tune-language-models -->

# Concepts - Fine-tuning language models for AI and machine learning workflows

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn about fine-tuning [language models](concepts-ai-ml-language-models), including some common methods and how applying the tuning results can improve the performance of your AI and machine learning workflows on Azure Kubernetes Service (AKS).

## Pre-trained language models

*Pre-trained language models (PLMs)* offer an accessible way to get started with AI inferencing and are widely used in natural language processing (NLP). PLMs are trained on large-scale text corpora from the internet using deep neural networks and can be fine-tuned on smaller datasets for specific tasks. These models typically consist of billions of parameters, or *weights*, that are learned during the pre-training process.

PLMs can learn universal language representations that capture the statistical properties of natural language, such as the probability of words or sequences of words occurring in a given context. These representations can be transferred to downstream tasks, such as text classification, named entity recognition, and question answering, by fine-tuning the model on task-specific datasets.

### Pros and cons

The following table lists some pros and cons of using PLMs in your AI and machine learning workflows:

| Pros | Cons |
|---|---|
| • Get started quickly with deployment in your machine learning lifecycle. • Avoid heavy compute costs associated with model training. • Reduces the need to store large, labeled datasets. |
• Might provide generalized or outdated responses based on pre-training data sources. • Might not be suitable for all tasks or domains. • Performance can vary depending on inferencing context. |

## Fine-tuning methods

### Parameter efficient fine-tuning

*Parameter efficient fine-tuning (PEFT)* is a method for fine-tuning PLMs on relatively small datasets with limited compute resources. PEFT uses a combination of techniques, like additive and selective methods to update weights, to improve the performance of the model on specific tasks. PEFT requires minimal compute resources and flexible quantities of data, making it suitable for low-resource settings. This method retains most of the weights of the original pre-trained model and updates the remaining weights to fit context-specific, labeled data.

### Low rank adaptation

*Low rank adaptation (LoRA)* is a PEFT method commonly used to customize large language models for new tasks. This method tracks changes to model weights and efficiently stores smaller weight matrices that represent only the model's trainable parameters, reducing memory usage and the compute power needed for fine-tuning. LoRA creates fine-tuning results, known as *adapter layers*, that can be temporarily stored and pulled into the model's architecture for new inferencing jobs.

*Quantized low rank adaptation (QLoRA)* is an extension of LoRA that further reduces memory usage by introducing quantization to the adapter layers. For more information, see [Making LLMs even more accessible with bitsandbites, 4-bit quantization, and QLoRA](https://huggingface.co/blog/4bit-transformers-bitsandbytes#:%7E:text=We%20present%20QLoRA%2C%20an%20efficient%20finetuning%20approach%20that,pretrained%20language%20model%20into%20Low%20Rank%20Adapters%7E%20%28LoRA%29.).

## Experiment with fine-tuning language models on AKS

Kubernetes AI Toolchain Operator (KAITO) is an open-source operator that automates small and large language model deployments in Kubernetes clusters. The AI toolchain operator add-on leverages KAITO to simplify onboarding, save on infrastructure costs, and reduce the time-to-inference for open-source models on an AKS cluster. The add-on automatically provisions right-sized GPU nodes and sets up the associated inference server as an endpoint server to your chosen model.

With KAITO version 0.3.0 or later, you can efficiently fine-tune supported MIT and Apache 2.0 licensed models with the following features:

- Store your retraining data as a container image in a private container registry.
- Host the new adapter layer image in a private container registry.
- Efficiently pull the image for inferencing with adapter layers in new scenarios.

For guidance on getting started with fine-tuning on KAITO, see the [Kaito Tuning Workspace API documentation][kaito-fine-tuning]. To learn more about deploying language models with KAITO in your AKS clusters, see the [KAITO model GitHub repository](https://github.com/Azure/kaito/tree/main/presets).

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Next steps

To learn more about containerized AI and machine learning workloads on AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-network-services -->

# Kubernetes Services in AKS

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can use Kubernetes Services to logically group pods and provide network connectivity by allowing direct access to them through a specific IP address or DNS name on a designated port. This allows you to expose your application workloads to other services within the cluster or to external clients without having to manually manage the network configuration for each pod hosting a workload.

You can specify what kind of service you want using Kubernetes *Service type values*. For more information, see the

[Kubernetes Service documentation](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types).

The following Service types are available in AKS: [ ClusterIP](#clusterip),

[,](#nodeport)

`NodePort`

[, and](#loadbalancer)

`LoadBalancer`

[.](#externalname)

`ExternalName`

## ClusterIP

`ClusterIP`

creates an internal IP address for use within the AKS cluster. The `ClusterIP`

Service is good for *internal-only applications* that support other workloads within the cluster. ClusterIP is used by default if you don't explicitly specify a type for a Service.


## NodePort

`NodePort`

creates a port mapping on the underlying node that allows the application to be accessed directly with the node IP address and port.


## LoadBalancer

`LoadBalancer`

creates an Azure load balancer resource, configures an external IP address, and connects the requested pods to the load balancer backend pool. To allow customer traffic to reach the application, load balancing rules are created on the desired ports.


For HTTP load balancing of inbound traffic, you can also use an [Ingress controller](concepts-network-ingress#ingress-controllers).

You can also use the `LoadBalancer`

type to create multiple public load balancers in a single AKS cluster. This is useful for large clusters or port-heavy workloads that can quickly exhaust the limits of a single load balancer. For more information, see [Use multiple public load balancers in Azure Kubernetes Service (preview)](use-multiple-standard-load-balancer).

## ExternalName

`ExternalName`

creates a specific DNS entry for easier application access. You can dynamically assign the load balancers and service IP address, or you can specify an existing static IP address. You can assign both internal and external static IP addresses. Existing static IP addresses are often tied to a DNS entry.

You can create both *internal* and *external* load balancers. Internal load balancers are only assigned a private IP address, so they can't be accessed from the Internet.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-hybrid-benefit -->

# What is Azure Hybrid Benefit for Azure Kubernetes Service?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Hybrid Benefit is a program that enables you to significantly reduce the costs of running workloads in the cloud. With Azure Hybrid Benefit for Azure Kubernetes Service (AKS), you can maximize the value of your on-premises licenses and modernize your applications at no extra cost. Azure Hybrid Benefit enables you to use your on-premises licenses that also have either active Software Assurance (SA) or a qualifying subscription to get Windows virtual machines (VMs) on Azure at a reduced cost.

For more information on qualifications for Azure Hybrid Benefit, what is included with it, how to stay compliant, and more, check out [Azure Hybrid Benefit for Windows Server](/en-us/azure/virtual-machines/windows/hybrid-use-benefit-licensing).

Note

Azure Hybrid Benefit for Azure Kubernetes Service follows the same licensing guidance as Azure Hybrid Benefit for Windows Server VMs on Azure.

## Enable Azure Hybrid Benefit for Azure Kubernetes Service

Azure Hybrid Benefit for Azure Kubernetes Service can be enabled at cluster creation or on an existing AKS cluster. You can enable and disable Azure Hybrid Benefit using either the Azure CLI or Azure PowerShell. In the following examples, be sure to replace the variable definitions with values matching your own cluster.

To create a new AKS cluster with Azure Hybrid Benefit enabled:

```
PASSWORD='' # replace with your own password value
RG_NAME='myResourceGroup'
CLUSTER='myAKSCluster'
az aks create \
--resource-group $RG_NAME \
--name $CLUSTER \
--load-balancer-sku Standard \
--network-plugin azure \
--windows-admin-username azure \
--windows-admin-password $PASSWORD \
--enable-ahub \
--generate-ssh-keys
```


To enable Azure Hybrid Benefit on an existing AKS cluster:

```
RG_NAME='myResourceGroup'
CLUSTER='myAKSCluster'
az aks update --resource-group $RG_NAME --name $CLUSTER--enable-ahub
```


## Disable Azure Hybrid Benefit for Azure Kubernetes Service

To disable Azure Hybrid Benefit for an AKS cluster:

```
RG_NAME='myResourceGroup'
CLUSTER='myAKSCluster'
az aks update --resource-group $RG_NAME --name $CLUSTER --disable-ahub
```


## Next steps

To learn more about Windows containers on AKS, see the following resources:

[Learn how to deploy, manage, and monitor Windows containers on AKS](/en-us/training/paths/deploy-manage-monitor-wincontainers-aks).- Open an issue or provide feedback in the
[Windows containers GitHub repository](https://github.com/microsoft/Windows-Containers/issues). - Review the
[third-party partner solutions for Windows on AKS](windows-aks-partner-solutions).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-multi-region -->

# Multi-region deployment models for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) provides a managed Kubernetes environment for deploying, managing, and scaling containerized applications. To provide resiliency to regional outages for your applications running on AKS, you can implement various multi-region deployment models. This article provides an overview of these models, their pros and cons, and best practices for maintaining application uptime.

AKS provides a range of capabilities that support both high availability (HA) and disaster recovery (DR) for your cluster and the applications running on AKS. For more information on how AKS supports reliability requirements, see [Reliability in AKS](/en-us/azure/reliability/reliability-aks#multi-region-support).

## Considerations

Below are some important considerations when implementing multi-region deployment models in AKS:

### Regional and global resources

**Regional resources** are provisioned as part of a *deployment stamp* to a single Azure region. These resources share nothing with resources in other regions, and they can be independently removed or replicated to other regions. For more information, see [Regional resources](/en-us/azure/architecture/reference-architectures/containers/aks-mission-critical/mission-critical-intro#regional-resources).

**Global resources** share the lifetime of the system, and they can be globally available within the context of a multi-region deployment. For more information, see [Global resources](/en-us/azure/architecture/reference-architectures/containers/aks-mission-critical/mission-critical-intro#global-resources).

### Global load balancing

Global load balancing services distribute traffic across regional backends, clouds, or hybrid on-premises services. These services route end-user traffic to the closest available backend. They also react to changes in service reliability or performance to maximize availability and performance. The following Azure services provide global load balancing:

[Azure Front Door](/en-us/azure/frontdoor/front-door-overview)[Azure Traffic Manager](/en-us/azure/traffic-manager/traffic-manager-overview)[Cross-region Azure Load Balancer](/en-us/azure/load-balancer/cross-region-overview)[Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/overview)

### Scope definition

Application uptime becomes important as you manage AKS clusters. By default, AKS provides high availability by using multiple nodes in a [Virtual Machine Scale Set](/en-us/azure/virtual-machine-scale-sets/overview), but these nodes don’t protect your system from a region failure. To maximize your uptime, plan ahead to maintain business continuity and prepare for disaster recovery using the following best practices:

- Plan for AKS clusters in multiple regions.
- Route traffic across multiple clusters using Azure Traffic Manager.
- Use geo-replication for your container image registries.
- Plan for application state across multiple clusters.
- Replicate storage across multiple regions.

## Multi-region deployment model implementations

The following table summarizes the three main multi-region deployment models in AKS, along with their pros and cons:

| Deployment model | Pros | Cons |
|---|---|---|
|

• High resiliency

• Better utilization of resources with higher performance

• Higher cost

• Requires a load balancer and form of traffic routing

[Active-passive](#active-passive-disaster-recovery-deployment-model)• Lower cost

• Doesn't require a load balancer or traffic manager

• Longer recovery time and downtime

• Underutilization of resources

[Passive-cold](#passive-cold-failover-deployment-model)• Doesn't require synchronization, replication, load balancer, or traffic manager

• Suitable for low-priority, non-critical workloads

• Longest recovery time and downtime

• Requires manual intervention to activate cluster and trigger backup

### Active-active high availability deployment model

In the active-active high availability (HA) deployment model, you have two independent AKS clusters deployed in two different Azure regions (typically paired regions, such as Canada Central and Canada East or US East 2 and US Central) that actively serve traffic.

With this example architecture:

- You deploy two AKS clusters in separate Azure regions.
- During normal operations, network traffic routes between both regions. If one region becomes unavailable, traffic automatically routes to a region closest to the user who issued the request.
- There's a deployed hub-spoke pair for each regional AKS instance. Azure Firewall Manager policies manage the firewall rules across the regions.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Azure Front Door load balances and routes traffic to a regional Azure Application Gateway instance, which sits in front of each AKS cluster.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs.
- The container images for the workload are stored in a managed container registry. A single Azure Container Registry is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables replicating images to the selected Azure regions and provides continued access to images, even if a region experiences an outage.

To create an active-active deployment model in AKS, you perform the following steps:

Create two identical deployments in two different Azure regions.

Create two instances of your web app.

Create an Azure Front Door profile with the following resources:

- An endpoint.
- Two origin groups, each with a priority of
*one*. - A route.

Limit network traffic to the web apps only from the Azure Front Door instance. 5. Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.

Deploy code to both web apps with continuous deployment.


For more information, see the [ Recommended active-active high availability solution overview for AKS](active-active-solution).

### Active-passive disaster recovery deployment model

In the active-passive disaster recovery (DR) deployment model, you have two independent AKS clusters deployed in two different Azure regions (typically paired regions, such as Canada Central and Canada East or US East 2 and US Central) that actively serve traffic. Only one of the clusters actively serves traffic at any given time. The other cluster contains the same configuration and application data as the active cluster, but doesn't accept traffic unless directed by a traffic manager.

With this example architecture:

- You deploy two AKS clusters in separate Azure regions.
- During normal operations, network traffic routes to the primary AKS cluster, which you set in the Azure Front Door configuration.
- Priority needs to be set between
*1-5*with 1 being the highest and 5 being the lowest. - You can set multiple clusters to the same priority level and can specify the weight of each.

- Priority needs to be set between
- If the primary cluster becomes unavailable (disaster occurs), traffic automatically routes to the next region selected in the Azure Front Door.
- All traffic must go through the Azure Front Door traffic manager for this system to work.

- Azure Front Door routes traffic to the Azure App Gateway in the primary region (cluster must be marked with priority 1). If this region fails, the service redirects traffic to the next cluster in the priority list.
- Rules come from Azure Front Door.

- A hub-spoke pair is deployed for each regional AKS instance. Azure Firewall Manager policies manage the firewall rules across the regions.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs.
- The container images for the workload are stored in a managed container registry. A single Azure Container Registry is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables replicating images to the selected Azure regions and provides continued access to images, even if a region experiences an outage.

To create an active-passive deployment model in AKS, you perform the following steps:

Create two identical deployments in two different Azure regions.

Configure autoscaling rules for the secondary application so it scales to the same instance count as the primary when the primary region becomes inactive. While inactive, it doesn't need to be scaled up. This helps reduce costs.

Create two instances of your web application, with one on each cluster.

Create an Azure Front Door profile with the following resources:

- An endpoint.
- An origin group with a priority of
*one*for the primary region. - A second origin group with a priority of
*two*for the secondary region. - A route.

Limit network traffic to the web applications from only the Azure Front Door instance.

Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.

Deploy code to both the web applications with continuous deployment.


For more information, see the [ Recommended active-passive disaster recovery solution overview for AKS](active-passive-solution).

### Passive-cold failover deployment model

The passive-cold failover deployment model is configured in the same way as the [active-passive disaster recovery deployment model](#active-passive-disaster-recovery-deployment-model), except the clusters remain inactive until a user activates them in the event of a disaster. We consider this approach *out-of-scope* because it involves a similar configuration to active-passive, but with the added complexity of manual intervention to activate the cluster and trigger a backup.

With this example architecture:

- You create two AKS clusters, preferably in different regions or zones for better resiliency.
- When you need to fail over, you activate the deployment to take over the traffic flow.
- In the case the primary passive cluster goes down, you need to manually activate the cold cluster to take over the traffic flow.
- This condition needs to be set either by a manual input every time or a certain event as specified by you.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs for each cluster.

To create a passive-cold failover deployment model in AKS, you perform the following steps:

- Create two identical deployments in different zones/regions.
- Configure autoscaling rules for the secondary application so it scales to the same instance count as the primary when the primary region becomes inactive. While inactive, it doesn't need to be scaled up, which helps reduce costs.
- Create two instances of your web application, with one on each cluster.
- Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.
- Set a condition when the cold cluster should be triggered. You can use a load balancer if you need.

For more information, see the [ Recommended passive-cold failover solution overview for AKS](passive-cold-solution).

For more information, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/csi-secrets-store-identity-access -->

# Connect your Azure identity provider to the Azure Key Vault Secrets Store CSI Driver in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Secrets Store Container Storage Interface (CSI) Driver on Azure Kubernetes Service (AKS) provides various methods of identity-based access to your Azure Key Vault. This article outlines these methods and best practices for when to use Azure role-based access control (Azure RBAC) or OpenID Connect (OIDC) security models to access your key vault and AKS cluster.

You can use one of the following access methods:

- Service Connector with managed identity
- Workload ID
- User-assigned managed identity

Learn how to connect to Azure Key Vault with the Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster using Service Connector. In this article, you complete the following tasks:

- Create an AKS cluster and an Azure Key Vault.
- Create a connection between the AKS cluster and the Azure Key Vault with Service Connector.
- Create a
`SecretProviderClass`

CRD and a`Pod`

that consumes the CSI provider to test the connection. - Clean up resources.

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - The
[Azure CLI](/en-us/cli/azure/install-azure-cli). Sign in using thecommand.`az login`

[Docker](https://docs.docker.com/get-docker/)and[kubectl](https://kubernetes.io/docs/tasks/tools/). To install kubectl locally, use thecommand.`az aks install-cli`

- A basic understanding of containers and AKS. Get started by
[preparing an application for AKS](/en-us/azure/aks/tutorial-kubernetes-prepare-app). - Before you begin, make sure you finish the steps in
[Use the Azure Key Vault provider for Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster](csi-secrets-store-driver)to enable the Azure Key Vault Secrets Store CSI Driver in your AKS cluster.

## Initial set-up

If you're using Service Connector for the first time, start by running the command

[az provider register](/en-us/cli/azure/provider#az-provider-register)to register the Service Connector and Kubernetes Configuration resource providers.`az provider register -n Microsoft.ServiceLinker`

`az provider register -n Microsoft.KubernetesConfiguration`

Tip

You can check if these resource providers have already been registered by running the commands

`az provider show -n "Microsoft.ServiceLinker" --query registrationState`

and`az provider show -n "Microsoft.KubernetesConfiguration" --query registrationState`

.Optionally, use the Azure CLI command to get a list of supported target services for AKS cluster.

`az aks connection list-support-types --output table`


## Create Azure resources

Create a resource group using the

command.`az group create`

`az group create \ --name <resource-group-name> \ --location <location>`

Create an AKS cluster using the

command. The following example creates a single-node AKS cluster with managed identity enabled.`az aks create`

`az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --enable-managed-identity \ --node-count 1`

Connect to the cluster using the

command.`az aks get-credentials`

`az aks get-credentials \ --resource-group <resource-group-name> \ --name <cluster-name>`

Create an Azure key vault using the

command.`az keyvault create`

`az keyvault create \ --resource-group <resource-group-name> \ --name <key-vault-name> \ --location <location>`

Create a secret in the key vault using the

command.`az keyvault secret set`

`az keyvault secret set \ --vault-name <key-vault-name> \ --name <secret-name> \ --value <secret-value>`


## Create a service connection in AKS with Service Connector

You can create a service connection to Azure Key Vault using the Azure portal or Azure CLI.

In the Azure portal, navigate to your AKS cluster resource.

From the service menu, under

**Settings**, select**Service Connector**>**Create**.On the

**Create connection**page, configure the following settings in the**Basics**tab:**Kubernetes namespace**: Select**default**.**Service type**: Select**Key Vault**and select the checkbox to enable the Azure Key Vault CSI Provider.**Connection name**: Enter a name for the connection.**Subscription**: Select the subscription that contains the key vault.**Key vault**: Select the key vault you created.**Client type**: Select**None**.

Select

**Review + create**, and then select**Create**to create the connection.

## Test the connection

### Clone the sample repo and deploy manifest files

Clone the sample repository using the

`git clone`

command.`git clone https://github.com/Azure-Samples/serviceconnector-aks-samples.git`

Change directories to the Azure Key Vault CSI provider sample.

`cd serviceconnector-aks-samples/azure-keyvault-csi-provider`

In the

`secret_provider_class.yaml`

file, replace the following placeholders with your Azure Key Vault information:- Replace
`<AZURE_KEYVAULT_NAME>`

with the name of the key vault you created and connected. - Replace
`<AZURE_KEYVAULT_TENANTID>`

with the tenant ID of the key vault. - Replace
`<AZURE_KEYVAULT_CLIENTID>`

with identity client ID of the`azureKeyvaultSecretsProvider`

addon. - Replace
`<KEYVAULT_SECRET_NAME>`

with the key vault secret you created. For example,`ExampleSecret`

.

- Replace
Deploy the

`SecretProviderClass`

CRD using the`kubectl apply`

command.`kubectl apply -f secret_provider_class.yaml`

Deploy the

`Pod`

manifest file using the`kubectl apply`

command.The command creates a pod named

`sc-demo-keyvault-csi`

in the default namespace of your AKS cluster.`kubectl apply -f pod.yaml`


### Verify the connection

Verify the pod was created successfully using the

`kubectl get`

command.`kubectl get pod/sc-demo-keyvault-csi`

After the pod starts, the mounted content at the volume path specified in your deployment YAML is available.

Show the secrets held in the secrets store using the

`kubectl exec`

command.`kubectl exec sc-demo-keyvault-csi -- ls /mnt/secrets-store/`

Display a secret using the

`kubectl exec`

command.This example command shows a test secret named

`ExampleSecret`

.`kubectl exec sc-demo-keyvault-csi -- cat /mnt/secrets-store/ExampleSecret`


## Prerequisites for CSI Driver

- Before you begin, make sure you finish the steps in
[Use the Azure Key Vault provider for Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster](csi-secrets-store-driver)to enable the Azure Key Vault Secrets Store CSI Driver in your AKS cluster. - Microsoft Entra Workload ID supports both Windows and Linux clusters.

## Access with a Microsoft Entra Workload ID

A [Microsoft Entra Workload ID](workload-identity-overview) is an identity that an application running on a pod uses to authenticate itself against other Azure services, such as workloads in software. The Secret Store CSI Driver integrates with native Kubernetes capabilities to federate with external identity providers.

In this security model, the AKS cluster acts as token issuer. Microsoft Entra ID then uses OIDC to discover public signing keys and verify the authenticity of the service account token before exchanging it for a Microsoft Entra token. For your workload to exchange a service account token projected to its volume for a Microsoft Entra token, you need the Azure Identity client library in the Azure SDK or the Microsoft Authentication Library (MSAL)

Note

- This authentication method replaces Microsoft Entra pod-managed identity (preview). The open source Microsoft Entra pod-managed identity (preview) in Azure Kubernetes Service was deprecated as of October 24, 2022.
- Microsoft Entra Workload ID supports both Windows and Linux clusters.

### Configure workload identity

Set your subscription using the

command.`az account set`

`export SUBSCRIPTION_ID=<subscription id> export RESOURCE_GROUP=<resource group name> export UAMI=<name for user assigned identity> export KEYVAULT_NAME=<existing keyvault name> export CLUSTER_NAME=<aks cluster name> az account set --subscription $SUBSCRIPTION_ID`

Create a managed identity using the

command.`az identity create`

Note

This step assumes you have an existing AKS cluster with workload identity enabled. If workload identity isn't enabled, see

[Enable workload identity on an existing AKS cluster](workload-identity-deploy-cluster#enable-oidc-issuer-and-microsoft-entra-workload-id-on-an-aks-cluster)to enable it.`az identity create --name $UAMI --resource-group $RESOURCE_GROUP export USER_ASSIGNED_CLIENT_ID="$(az identity show --resource-group $RESOURCE_GROUP --name $UAMI --query 'clientId' -o tsv)" export IDENTITY_TENANT=$(az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query identity.tenantId -o tsv)`

Create a role assignment that grants the workload identity permission to access the key vault secrets, access keys, and certificates using the

command.`az role assignment create`

Important

- If your key vault is set with
`--enable-rbac-authorization`

and you're using`key`

or`certificate`

type, assign therole to give permissions.`Key Vault Certificate User`

- If your key vault is set with
`--enable-rbac-authorization`

and you're using`secret`

type, assign therole.`Key Vault Secrets User`

- If your key vault isn't set with
`--enable-rbac-authorization`

, you can use thecommand with the`az keyvault set-policy`

`--key-permissions get`

,`--certificate-permissions get`

, or`--secret-permissions get`

parameter to create a key vault policy to grant access for keys, certificates, or secrets. For example:

`az keyvault set-policy --name $KEYVAULT_NAME --key-permissions get --object-id <identity-object-id>`

`export KEYVAULT_SCOPE=$(az keyvault show --name $KEYVAULT_NAME --query id -o tsv) # Example command for key vault with Azure RBAC enabled using `key` type az role assignment create --role "Key Vault Certificate User" --assignee $USER_ASSIGNED_CLIENT_ID --scope $KEYVAULT_SCOPE`

- If your key vault is set with
Get the AKS cluster OIDC Issuer URL using the

command.`az aks show`

Note

This step assumes you have an existing AKS cluster with the OIDC Issuer URL enabled. If the OIDC Issuer URL isn't enabled, see

[Update an AKS cluster with OIDC Issuer](use-oidc-issuer#enable-the-oidc-issuer-on-an-existing-aks-cluster)to enable it.`export AKS_OIDC_ISSUER="$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query "oidcIssuerProfile.issuerUrl" -o tsv)" echo $AKS_OIDC_ISSUER`

Establish a federated identity credential between the Microsoft Entra application, service account issuer, and subject. Get the object ID of the Microsoft Entra application using the following commands. Make sure to update the values for

`serviceAccountName`

and`serviceAccountNamespace`

with the Kubernetes service account name and its namespace.`export SERVICE_ACCOUNT_NAME="workload-identity-sa" # sample name; can be changed export SERVICE_ACCOUNT_NAMESPACE="default" # can be changed to namespace of your workload cat <<EOF | kubectl apply -f - apiVersion: v1 kind: ServiceAccount metadata: annotations: azure.workload.identity/client-id: ${USER_ASSIGNED_CLIENT_ID} name: ${SERVICE_ACCOUNT_NAME} namespace: ${SERVICE_ACCOUNT_NAMESPACE} EOF`

Create the federated identity credential between the managed identity, service account issuer, and subject using the

command.`az identity federated-credential create`

`export FEDERATED_IDENTITY_NAME="aksfederatedidentity" # can be changed as needed az identity federated-credential create --name $FEDERATED_IDENTITY_NAME --identity-name $UAMI --resource-group $RESOURCE_GROUP --issuer ${AKS_OIDC_ISSUER} --subject system:serviceaccount:${SERVICE_ACCOUNT_NAMESPACE}:${SERVICE_ACCOUNT_NAME}`

Deploy a

`SecretProviderClass`

using the`kubectl apply`

command and the following YAML script.`cat <<EOF | kubectl apply -f - # This is a SecretProviderClass example using workload identity to access your key vault apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: azure-kvname-wi # needs to be unique per namespace spec: provider: azure parameters: usePodIdentity: "false" clientID: "${USER_ASSIGNED_CLIENT_ID}" # Setting this to use workload identity keyvaultName: ${KEYVAULT_NAME} # Set to the name of your key vault cloudName: "" # [OPTIONAL for Azure] if not provided, the Azure environment defaults to AzurePublicCloud objects: | array: - | objectName: secret1 # Set to the name of your secret objectType: secret # object types: secret, key, or cert objectVersion: "" # [OPTIONAL] object versions, default to latest if empty - | objectName: key1 # Set to the name of your key objectType: key objectVersion: "" tenantId: "${IDENTITY_TENANT}" # The tenant ID of the key vault EOF`

Note

If you use

`objectAlias`

instead of`objectName`

, update the YAML script to account for it.Note

In order for the

`SecretProviderClass`

to function properly, make sure to populate your Azure Key Vault with secrets, keys, or certificates before referencing them in the`objects`

section.Deploy a sample pod using the

`kubectl apply`

command and the following YAML script.`cat <<EOF | kubectl apply -f - # This is a sample pod definition for using SecretProviderClass and workload identity to access your key vault kind: Pod apiVersion: v1 metadata: name: busybox-secrets-store-inline-wi labels: azure.workload.identity/use: "true" spec: serviceAccountName: "workload-identity-sa" containers: - name: busybox image: registry.k8s.io/e2e-test-images/busybox:1.29-4 command: - "/bin/sleep" - "10000" volumeMounts: - name: secrets-store01-inline mountPath: "/mnt/secrets-store" readOnly: true volumes: - name: secrets-store01-inline csi: driver: secrets-store.csi.k8s.io readOnly: true volumeAttributes: secretProviderClass: "azure-kvname-wi" EOF`


## Prerequisites for CSI Driver

- Before you begin, make sure you finish the steps in
[Use the Azure Key Vault provider for Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster](csi-secrets-store-driver)to enable the Azure Key Vault Secrets Store CSI Driver in your AKS cluster.

## Access with managed identity

A [Microsoft Entra Managed ID](/en-us/entra/identity/managed-identities-azure-resources/overview) is an identity that an administrator uses to authenticate themselves against other Azure services. The managed identity uses Azure RBAC to federate with external identity providers.

In this security model, you can grant access to your cluster's resources to team members or tenants sharing a managed role. The role is checked for scope to access the keyvault and other credentials. When you [enabled the Azure Key Vault provider for Secrets Store CSI Driver on your AKS Cluster](csi-secrets-store-driver#create-an-aks-cluster-with-azure-key-vault-provider-for-secrets-store-csi-driver-support), it created a user identity.

### Configure managed identity

Access your key vault using the

command and the user-assigned managed identity created by the add-on. You should also retrieve the identity's`az aks show`

`clientId`

, which you use in later steps when creating a`SecretProviderClass`

.`az aks show --resource-group <resource-group> --name <cluster-name> --query addonProfiles.azureKeyvaultSecretsProvider.identity.objectId -o tsv az aks show --resource-group <resource-group> --name <cluster-name> --query addonProfiles.azureKeyvaultSecretsProvider.identity.clientId -o tsv`

Alternatively, you can create a new managed identity and assign it to your virtual machine (VM) scale set or to each VM instance in your availability set using the following commands.

`az identity create --resource-group <resource-group> --name <identity-name> az vmss identity assign --resource-group <resource-group> --name <agent-pool-vmss> --identities <identity-resource-id> az vm identity assign --resource-group <resource-group> --name <agent-pool-vm> --identities <identity-resource-id> az identity show --resource-group <resource-group> --name <identity-name> --query 'clientId' -o tsv`

Create a role assignment that grants the identity permission to access the key vault secrets, access keys, and certificates using the

command.`az role assignment create`

Important

- If your key vault is set with
`--enable-rbac-authorization`

and you're using`key`

or`certificate`

type, assign therole.`Key Vault Certificate User`

- If your key vault is set with
`--enable-rbac-authorization`

and you're using`secret`

type, assign therole.`Key Vault Secrets User`

- If your key vault isn't set with
`--enable-rbac-authorization`

, you can use thecommand with the`az keyvault set-policy`

`--key-permissions get`

,`--certificate-permissions get`

, or`--secret-permissions get`

parameter to create a key vault policy to grant access for keys, certificates, or secrets. For example:

`az keyvault set-policy --name $KEYVAULT_NAME --key-permissions get --object-id <identity-object-id>`

`export IDENTITY_OBJECT_ID="$(az identity show --resource-group <resource-group> --name <identity-name> --query 'principalId' -o tsv)" export KEYVAULT_SCOPE=$(az keyvault show --name <key-vault-name> --query id -o tsv) # Example command for key vault with Azure RBAC enabled using `key` type az role assignment create --role "Key Vault Certificate User" --assignee $IDENTITY_OBJECT_ID --scope $KEYVAULT_SCOPE`

- If your key vault is set with
Create a

`SecretProviderClass`

using the following YAML. Make sure to use your own values for`userAssignedIdentityID`

,`keyvaultName`

,`tenantId`

, and the objects to retrieve from your key vault.`# This is a SecretProviderClass example using user-assigned identity to access your key vault apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: azure-kvname-user-msi spec: provider: azure parameters: usePodIdentity: "false" useVMManagedIdentity: "true" # Set to true for using managed identity userAssignedIdentityID: <client-id> # Set the clientID of the user-assigned managed identity to use keyvaultName: <key-vault-name> # Set to the name of your key vault cloudName: "" # [OPTIONAL for Azure] if not provided, the Azure environment defaults to AzurePublicCloud objects: | array: - | objectName: secret1 objectType: secret # object types: secret, key, or cert objectVersion: "" # [OPTIONAL] object versions, default to latest if empty - | objectName: key1 objectType: key objectVersion: "" tenantId: <tenant-id> # The tenant ID of the key vault`

Note

If you use

`objectAlias`

instead of`objectName`

, make sure to update the YAML script.Note

In order for the

`SecretProviderClass`

to function properly, make sure to populate your Azure Key Vault with secrets, keys, or certificates before referencing them in the`objects`

section.Apply the

`SecretProviderClass`

to your cluster using the`kubectl apply`

command.`kubectl apply -f secretproviderclass.yaml`

Create a pod using the following YAML.

`# This is a sample pod definition for using SecretProviderClass and the user-assigned identity to access your key vault kind: Pod apiVersion: v1 metadata: name: busybox-secrets-store-inline-user-msi spec: containers: - name: busybox image: registry.k8s.io/e2e-test-images/busybox:1.29-4 command: - "/bin/sleep" - "10000" volumeMounts: - name: secrets-store01-inline mountPath: "/mnt/secrets-store" readOnly: true volumes: - name: secrets-store01-inline csi: driver: secrets-store.csi.k8s.io readOnly: true volumeAttributes: secretProviderClass: "azure-kvname-user-msi"`

Apply the pod to your cluster using the

`kubectl apply`

command.`kubectl apply -f pod.yaml`


## Validate Key Vault secrets

After the pod starts, the mounted content at the volume path specified in your deployment YAML is available. Use the following commands to validate your secrets and print a test secret.

Show secrets held in the secrets store using the following command.

`kubectl exec busybox-secrets-store-inline-user-msi -- ls /mnt/secrets-store/`

Display a secret in the store using the following command. This example command shows the test secret

`ExampleSecret`

.`kubectl exec busybox-secrets-store-inline-user-msi -- cat /mnt/secrets-store/ExampleSecret`


## Obtain certificates and keys

The Azure Key Vault design makes sharp distinctions between keys, secrets, and certificates. The certificate features of the Key Vault service are designed to make use of key and secret capabilities. When you create a key vault certificate, it creates an addressable key and secret with the same name. This key allows authentication operations, and the secret allows the retrieval of the certificate value as a secret.

A key vault certificate also contains public x509 certificate metadata. The key vault stores both the public and private components of your certificate in a secret. You can obtain each individual component by specifying the `objectType`

in `SecretProviderClass`

. The following table shows which objects map to the various resources associated with your certificate:

| Object | Return value | Returns entire certificate chain |
|---|---|---|
`key` |
The public key, in Privacy Enhanced Mail (PEM) format. | N/A |
`cert` |
The certificate, in PEM format. | No |
`secret` |
The private key and certificate, in PEM format. | Yes |

## Disable the addon on existing clusters

Note

Before you disable the add-on, ensure that *no* `SecretProviderClass`

is in use. Trying to disable the add-on while a `SecretProviderClass`

exists results in an error.

Disable the Azure Key Vault provider for Secrets Store CSI Driver capability in an existing cluster using the [ az aks disable-addons](/en-us/cli/azure/aks#az-aks-disable-addons) command with the

`azure-keyvault-secrets-provider`

add-on.```
az aks disable-addons --addons azure-keyvault-secrets-provider --resource-group myResourceGroup --name myAKSCluster
```


Note

When you disable the add-on, existing workloads should have no issues or see any updates in the mounted secrets. If the pod restarts or a new pod is created as part of scale-up event, the pod fails to start because the driver is no longer running.

## Next steps

In this article, you learned how to create and provide an identity to access your Azure Key Vault. The [Service Connector](/en-us/azure/service-connector/overview) integration helps simplify the connection configuration for AKS workloads and Azure backing services. It securely handles authentication and network configurations and follows best practices for connecting to Azure services. For more information, see [Use the Azure Key Vault provider for Secrets Store CSI Driver in an AKS cluster](/en-us/azure/service-connector/tutorial-python-aks-keyvault-csi-driver) and the [Service Connector introduction](https://blog.aks.azure.com/2024/05/23/service-connector-intro).

If you want to configure extra configuration options or perform troubleshooting, see [Configuration options and troubleshooting resources for Azure Key Vault provider with Secrets Store CSI Driver in AKS](csi-secrets-store-configuration-options).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deployment-safeguards -->

# Use Deployment Safeguards to enforce best practices in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use Deployment Safeguards to enforce best practices on an Azure Kubernetes Service (AKS) cluster.

## Overview

Note

Deployment Safeguards is turned on by default in AKS Automatic.

Throughout the development lifecycle, it is common for bugs, issues, and other problems to arise if the initial deployment of your Kubernetes resources includes misconfigurations. To ease the burden of Kubernetes development, Azure Kubernetes Service (AKS) offers Deployment Safeguards. Deployment Safeguards enforce Kubernetes best practices in your AKS cluster through Azure Policy controls.

Deployment Safeguards offer two levels of configuration:

`Warn`

: Displays warning messages in the code terminal to alert you of any noncompliant cluster configurations but still allows the request to go through.`Enforce`

: Enforces compliant configurations by denying and mutating deployments if they don't follow best practices.

After you configure Deployment Safeguards for 'Warn' or 'Enforce', Deployment Safeguards programmatically assess your Kubernetes resources at creation or update time for compliance. Deployment Safeguards also display aggregated compliance information across your workloads at a per resource level via Azure Policy's compliance dashboard in the [Azure portal](https://portal.azure.com/#view/Microsoft_Azure_Policy/PolicyMenuBlade/%7E/Compliance) or in your CLI or terminal. Running a noncompliant workload indicates that your cluster is not following best practices and that workloads on your cluster are at risk of experiencing issues caused by your cluster configuration.

## Prerequisites

Note

Cluster admins don't need Azure Policy permissions to enable or disable Deployment Safeguards. However, it's required to have the Azure Policy add-on installed.

- You need to enable the Azure Policy add-on for AKS. For more information, see
[Enable Azure Policy on your AKS cluster](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#install-azure-policy-add-on-for-aks). This includes registering the`Microsoft.PolicyInsights`

resource provider in your subscription.

## Deployment Safeguards policies

The following table lists the policies that become active and the Kubernetes resources they target when you enable Deployment Safeguards. You can view the [currently available Deployment Safeguards](https://portal.azure.com/#view/Microsoft_Azure_Policy/InitiativeDetail.ReactView/id/%2Fproviders%2FMicrosoft.Authorization%2FpolicySetDefinitions%2Fc047ea8e-9c78-49b2-958b-37e56d291a44/scopes/) in the Azure portal as an Azure Policy definition or at [Azure Policy built-in definitions for Azure Kubernetes Service](/en-us/azure/aks/policy-reference#policy-definitions). The intention behind this collection is to create a common and generic list of best practices applicable to most users and use cases.

| Deployment safeguard policy | Mutation outcome if available |
|---|---|
| Cannot Edit Individual Nodes | N/A |
| Kubernetes cluster containers CPU and memory resource requests must be defined | Sets default CPU and memory requests and enforces minimums. For more information, see
|

[Anti-affinity and topology spread mutator](#anti-affinity-and-topology-spread-mutator).`CriticalAddonsOnly`

taint from a user node pool if not set. AKS uses the `CriticalAddonsOnly`

taint to keep customer pods away from the system pool. This configuration ensures a clear separation between AKS components and customer pods and prevents eviction of customer pods that don't tolerate the `CriticalAddonsOnly`

taint.If you want to submit an idea or request for Deployment Safeguards, open an issue in the [AKS GitHub repository](https://github.com/Azure/AKS) and add `[Deployment Safeguards request]`

to the beginning of the title.

## Resource requests mutator

When Deployment Safeguards is set to the `Enforce`

level, the resource requests mutator automatically sets CPU and memory requests and limits for containers that don't have them defined or have values below minimum thresholds.

### Default values

When no resources are specified, the mutator sets the following default values:

| Resource | Request | Limit |
|---|---|---|
| CPU | 500m | 500m |
| Memory | 2048Mi (2Gi) | 2048Mi (2Gi) |

### Minimum enforcement

When resources are specified but they're below thresholds, the mutator enforces the following minimum values:

| Resource | Minimum value |
|---|---|
| CPU | 100m |
| Memory | 100Mi |

### Understanding resource units

**CPU units**:

`m`

= millicores (`1m`

= 1/1,000th of a CPU core)`1000m`

= 1 full CPU core`500m`

= 0.5 CPU cores (half a core)`100m`

= 0.1 CPU cores (10% of a core)

**Memory units**:

`Mi`

= Mebibytes (binary: 1 Mi = 1,024 × 1,024 bytes)`Gi`

= Gibibytes (binary: 1 Gi = 1,024 Mi)`2048Mi`

=`2Gi`

`100Mi`

≈ 105 MB

### CPU mutation rules

The mutator applies the following logic for CPU resources:

| Scenario | Action |
|---|---|
| Both CPU request and limit are missing | Set both to `500m` (default) |
CPU request exists but is less than `100m` |
Set request to `100m` (minimum) |
CPU limit exists but is less than `100m` |
Set limit to `100m` (minimum) |
| Only CPU request exists | Set request equal to limit |
| Only CPU limit exists | Set request equal to limit |

### Memory mutation rules

The mutator applies the following logic for memory resources:

| Scenario | Action |
|---|---|
| Both memory request and limit are missing | Set both to `2048Mi` (default) |
Memory request exists but is less than `100Mi` |
Set request to `100Mi` (minimum) |
Memory limit exists but is less than `100Mi` |
Set limit to `100Mi` (minimum) |
| Only memory request exists | Leave as-is (no limit added) |
| Only memory limit exists | Leave as-is (no request added) |

### Kubernetes Quality of Service (QoS) class fix

After CPU and memory mutations are applied, if the request value exceeds the limit for the same resource type, the mutator caps the request to match the limit. This fix maintains valid Kubernetes Quality of Service (QoS) class configurations.

### Cases that are mutated

The resource requests mutator applies changes in the following scenarios:

**Empty resources**: Containers with no CPU or memory requests or limits receive default values (`500m`

CPU,`2048Mi`

memory).**Below minimum thresholds**: CPU requests or limits below`100m`

are increased to`100m`

. Memory requests or limits below`100Mi`

are increased to`100Mi`

.**Invalid QoS scenarios**: When requests exceed limits, requests are lowered to match limits.**Partial resource specifications**: Containers with only requests or only limits (but not both) have minimums enforced where specified.**Multiple containers**: All containers in a pod are processed and mutated appropriately.**Enabled namespaces**: Only workloads in namespaces where the safeguard is enabled are mutated.

### Cases that aren't mutated

The resource requests mutator doesn't apply changes in the following scenarios:

**Excluded namespaces**: Workloads in namespaces where the safeguard is excluded remain unchanged.**Already compliant resources**: Containers that already have requests and limits above minimum thresholds remain unchanged.**Valid QoS configurations**: When requests are less than or equal to limits and both values are above minimums, no changes occur.

## Anti-affinity and topology spread mutator

When Deployment Safeguards is set to the `Enforce`

level, the anti-affinity and topology spread mutator automatically adds pod anti-affinity rules and topology spread constraints to improve workload distribution across nodes.

### When the mutator runs

The mutator runs only when all of the following conditions are met:

- Both pod anti-affinity and topology spread constraints don't already exist on the workload.
- The namespace isn't excluded from Deployment Safeguards.
- Deployment Safeguards is in
`Enforce`

mode. - The workload doesn't have the
`kubernetes.azure.com/managedby=aks`

label.

### What the mutator adds

**Label identification**: The mutator identifies pods using the following label priority:

`app`

label (first priority)`app.kubernetes.io/name`

label (second priority)- Creates a
`default-antiaffinity-applabel=<workload-name>`

label (fallback)

**Pod anti-affinity**: Adds a preferred pod anti-affinity rule with weight 100 that prefers to schedule pods with matching labels on different nodes. Uses topology key `kubernetes.io/hostname`

.

**Topology spread constraints**: Adds a constraint with the following settings:

| Setting | Value |
|---|---|
| MaxSkew | 1 (allows maximum difference of 1 pod per node) |
| WhenUnsatisfiable | ScheduleAnyway (best-effort, doesn't block scheduling) |
| Topology key | `kubernetes.io/hostname` |

### Cases that are mutated

The anti-affinity and topology spread mutator applies changes in the following scenarios:

**Workloads with**: Uses the`app`

label`app`

label value for anti-affinity and topology spread selectors.**Workloads with**: When no`app.kubernetes.io/name`

label`app`

label exists, uses this label for selectors.**Workloads with no app labels**: Creates a default label using the workload name and adds anti-affinity and topology spread rules.**Clean workloads**: Workloads with no existing affinity or topology spread constraints receive both configurations.**Partial affinity**: Workloads with existing node affinity (but no pod anti-affinity) receive pod anti-affinity and topology spread rules.**Enabled namespaces**: Mutations only occur in namespaces where the safeguard is enabled.

### Cases that aren't mutated

The anti-affinity and topology spread mutator doesn't apply changes in the following scenarios:

**Existing topology spread constraints**: Workloads that already have any topology spread constraints are skipped entirely.**Existing pod anti-affinity**: Workloads with existing required or preferred pod anti-affinity rules are skipped entirely.**Excluded namespaces**: Workloads in namespaces where the safeguard is excluded remain unchanged.**Workloads without identifiable names or labels**: Edge cases where no app name can be determined are skipped gracefully.

## Deployment Safeguards error messages

This section describes the error messages you might encounter when Deployment Safeguards detects noncompliant configurations, along with recommended fixes.

### General safeguard error messages

The following table lists error messages for general Deployment Safeguards policies:

| Policy | Error message | Fix |
|---|---|---|
| Enforce Probes | `Container <container_name> in your Pod <pod_name> has no livenessProbe. Required probes: readinessProbe, livenessProbe` |
Add liveness and readiness probes to each container. |
| No "Latest" Image | `Please specify an explicit, versioned image tag such as '1.0' for container %v. Using explicit version tags is a best practice to ensure reproducibility, prevent unintended updates, and facilitate easier debugging and rollbacks. Avoid using the 'latest' tag because it can change over time without notice.` |
Use an explicit image tag other than `latest` or blank. For example, `nginx` isn't allowed, but `nginx:v1.0.0` is allowed. |
| Enforce CSI Driver | `Storage class <class_name> use intree provisioner kubernetes.io/azure-file is not allowed` or `Storage class <class_name> use intree provisioner kubernetes.io/azure-disk is not allowed` |
Use `disk.csi.azure.com` or `file.csi.azure.com` instead. For more information, see
|
| Resource Requests | `container <container_name> has no resource requests` |
Add CPU and memory requests to your container. |
| AntiAffinity Rules | `Deployment with 2 replicas should have either podAntiAffinity or topologySpreadConstraints set to avoid disruptions due to nodes crashing` |
Define `podAntiAffinity` or `topologySpreadConstraints` on the workload. |
| Restricted Labels | `Label kubernetes.azure.com is reserved for AKS use only` |
Remove the label from your workload. |
| Restricted Node Edits | `Tainting or labeling individual nodes is not recommended. Please use Azure CLI to taint/label node pools instead` |
Use the Azure CLI to taint or label node pools instead of individual nodes. |
| Restricted Taints | `Taint with key CriticalAddonsOnly is reserved for the system pool only` |
Don't taint the user node pool with `CriticalAddonsOnly` . |

### Pod Security Standards error messages

Note

Baseline Pod Security Standards are now turned on by default in AKS Automatic. The baseline Pod Security Standards in AKS Automatic can't be turned off.

Deployment Safeguards also supports the ability to turn on [Baseline, Restricted and Privileged Pod Security Standards](https://kubernetes.io/docs/concepts/security/pod-security-standards/). To ensure your workloads deploy successfully, make sure each manifest complies with the Baseline or Restricted Pod Security requirements. By default, Azure Kubernetes Service uses Privileged Pod Security Standards.

| Policy | Error message | Fix |
|---|---|---|
| AppArmor | `AppArmor annotation values must be undefined/nil, runtime/default, or localhost/*` or `AppArmor profile type must be one of: undefined/nil, RuntimeDefault, or Localhost` |
Remove any specification of AppArmor. Kubernetes by default applies AppArmor settings. On supported hosts, the RuntimeDefault AppArmor profile is applied by default. |
| Host Namespaces | `Host network namespaces are disallowed: spec.hostNetwork is set to true` or `Host PID namespaces are disallowed: spec.hostPID is set to true` or `Host IPC namespaces are disallowed: spec.hostIPC is set to true` |
Set those values to `false` , or remove specifying the fields. |
| Privileged Containers | `Privileged [ephemeral\|init\|N/A] containers are disallowed: spec.containers[*].securityContext.privileged is set to true` |
Set the appropriate `securityContext.privileged` field to `false` , or remove the field. |
| Capabilities | Message starts with `Disallowed capabilities detected` |
Remove the capability shown from the container's manifest. |
| HostPath Volumes | `HostPath volumes are forbidden under restricted security policy unless containers mounting them are from allowed images` |
Remove the HostPath volume and volume mount. |
| Host Ports | `HostPorts are forbidden under baseline security policy` |
Remove the host port specification from the offending container. |
| SELinux | `SELinux type must be one of: undefined/empty, container_t, container_init_t, container_kvm_t, or container_engine_t` |
Set the container's `securityContext.seLinuxOptions.type` field to one of the allowed values. |
| /proc Mount Type | `ProcMount must be undefined/nil or 'Default' in spec.containers[*].securityContext.procMount` |
Set `spec.containers[*].securityContext.procMount` to `Default` or leave it undefined. |
| Seccomp | `Seccomp profile must not be explicitly set to Unconfined. Allowed values are: undefined/nil, RuntimeDefault, or Localhost` |
Set `securityContext.seccompProfile.type` on the pod or containers to one of the allowed values. |
| Sysctls | `Disallowed sysctl detected. Only baseline Kubernetes pod security standard sysctls are permitted` |
Remove the disallowed sysctls. For the specific list, see the
|

`Only the following volume types are allowed under restricted policy: configMap, csi, downwardAPI, emptyDir, ephemeral, persistentVolumeClaim, projected, secret`

`Privilege escalation must be set to false under restricted policy`

`spec.containers[*].securityContext.allowPrivilegeEscalation`

to `false`

for each container, initContainer, and ephemeralContainer.`Containers must not run as root user in spec.containers[*].securityContext.runAsNonRoot`

`spec.containers[*].securityContext.runAsNonRoot`

to `true`

for each container, initContainer, and ephemeralContainer.`Containers must not run as root user: spec.securityContext.runAsUser is set to 0`

`securityContext.runAsUser`

to a nonzero value, or leave it undefined for the pod level and each container, initContainer, and ephemeralContainer.`Seccomp profile must be "RuntimeDefault" or "Localhost" under restricted policy`

`securityContext.seccompProfile.type`

on the pod or containers to one of the allowed values. This differs from the baseline because the restricted policy doesn't allow an undefined value.`All containers must drop ALL capabilities under restricted policy`

or `Only NET_BIND_SERVICE may be added to capabilities under restricted policy`

`ALL`

capabilities and are only permitted to add `NET_BIND_SERVICE`

.## Enable Deployment Safeguards

Note

Using the Deployment Safeguards `Enforce`

level means you're opting in to deployments being blocked and mutated. Consider how these policies might work with your AKS cluster before enabling `Enforce`

.

### Enable Deployment Safeguards on an existing cluster

Enable Deployment Safeguards on an existing cluster that has the Azure Policy add-on enabled using the `az aks safeguard create`

command with the `--level`

flag. If you want to receive noncompliance warnings, set the `--level`

to `Warn`

. If you want to deny or mutate all noncompliant deployments, set it to `Enforce`

.

```
az aks safeguards create --resource-group <resource-group-name> --name <cluster-name> --level Enforce
```


You can also enable Deployment Safeguards by using the `--cluster`

flag and specifying the cluster resource ID.

```
az aks safeguards create --cluster <ID> --level Enforce
```


If you want to update the Deployment Safeguards level of an existing cluster, run the following command with the new value for `--level`

.

```
az aks safeguards update --resource-group <resource-group-name> --name <cluster-name> --level Warn
```


### Excluding namespaces

You can also exclude certain namespaces from Deployment Safeguards. When you exclude a namespace, activity in that namespace is unaffected by Deployment Safeguards warnings or enforcement.

For example, to exclude the namespaces `ns1`

and `ns2`

, use a space separated list of namespaces with the `--excluded-ns`

flag, as shown in the following example:

```
az aks safeguards update --resource-group <resource-group-name> --name <cluster-name> --level Warn --excluded-ns ns1 ns2
```


### Turn on Pod Security Standards

Note

Azure Kubernetes Service (AKS) uses `Privileged`

Pod Security Standards by default. If you want to revert to the default configuration, set the `--pss-level`

flag to `Privileged`

.

To enable Pod Security Standards in Deployment Safeguards, use the `--pss-level`

flag to select one of the following levels: `Baseline`

, `Restricted`

, or `Privileged`

.

```
az aks safeguards update --resource-group <resource-group-name> --name <cluster-name> --level Warn --pss-level <Baseline|Restricted|Privileged>
```


### Update your Deployment Safeguard version

Deployment Safeguards adhere to the [AKS addon versioning scheme](supported-kubernetes-versions). Each new version of a Deployment Safeguard will be released as a new minor version in AKS. These updates will be communicated through the [AKS GitHub release notes](https://github.com/Azure/AKS/releases) and reflected in the "Deployment Safeguards Policies" table in our documentation.

To learn more about AKS versioning and addons, refer to the following documentation: [aks-component-versions](supported-kubernetes-versions) and [aks-versioning-for-addons](integrations#add-ons).

## Verify compliance across clusters

After deploying your Kubernetes manifest, you see warnings or a potential denial message in your CLI or terminal if the cluster isn't compliant with Deployment Safeguards, as shown in the following examples:

**Warn**

```
$ kubectl apply -f deployment.yaml
Warning: [azurepolicy-k8sazurev1antiaffinityrules-ceffa082711831ebffd1] Deployment with 2 replicas should have either podAntiAffinity or topologySpreadConstraints set to avoid disruptions due to nodes crashing
deployment.apps/simple-web created
```


**Enforce**

With Deployment Safeguard mutations, the `Enforce`

level mutates your Kubernetes resources when applicable. However, your Kubernetes resources still need to pass all safeguards to deploy successfully. If any safeguard policies fail, your resource is denied and won't be deployed.

```
$ kubectl apply -f deployment.yaml
Error from server (Forbidden): error when creating "deployment.yaml": admission webhook "validation.gatekeeper.sh" denied the request: [azurepolicy-k8sazurev1antiaffinityrules-ceffa082711831ebffd1] Deployment with 2 replicas should have either podAntiAffinity or topologySpreadConstraints set to avoid disruptions due to nodes crashing
```


If your Kubernetes resources comply with the applicable mutation safeguards and meet all other safeguard requirements, they'll be successfully deployed, as shown in the following example:

```
$ kubectl apply -f deployment.yaml
deployment.apps/simple-web created
```


## Verify compliance across clusters using the Azure Policy dashboard

To verify Deployment Safeguards have been applied and to check on your cluster's compliance, navigate to the Azure portal page for your cluster and select **Policies**, then select **go to Azure Policy**.

From the list of policies and initiatives, select the initiative associated with Deployment Safeguards. You see a dashboard showing compliance state across your AKS cluster.

Note

To properly assess compliance across your AKS cluster, the Azure Policy initiative must be scoped to your cluster's resource group.

## Disable Deployment Safeguards

To disable Deployment Safeguards on your cluster, use the `delete`

command.

```
az aks safeguards delete --resource-group <resource-group-name> --name <cluster-name>
```


## FAQ

#### Can I create my own mutations?

No. If you have an idea for a safeguard, open an issue in the [AKS GitHub repository](https://github.com/Azure/AKS) and add `[Deployment Safeguards request]`

to the beginning of the title.

#### Can I pick and choose which mutations I want in Enforcement?

No. Deployment Safeguards is all or nothing. Once you turn on Warn or Enforce, all safeguards are active.

#### Why did my deployment resource get admitted even though it wasn't following best practices?

Deployment Safeguards enforce best practice standards through Azure Policy controls and has policies that validate against Kubernetes resources. To evaluate and enforce cluster components, Azure Policy extends [Gatekeeper](https://open-policy-agent.github.io/gatekeeper/website/). Gatekeeper enforcement also currently operates in a [ fail-open model](https://open-policy-agent.github.io/gatekeeper/website/docs/failing-closed/#considerations). As there's no guarantee that Gatekeeper responds to our networking call, we make sure that in that case, the validation is skipped so that the deny doesn't block your deployments.

To learn more, see [workload validation in Gatekeeper](https://open-policy-agent.github.io/gatekeeper/website/docs/workload-resources/).

## Next steps

- Learn more about
[best practices](best-practices)for operating an AKS cluster.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/dapr -->

# Install the Dapr extension for Azure Kubernetes Service (AKS) and Arc-enabled Kubernetes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Dapr](dapr-overview) simplifies building resilient, stateless, and stateful applications that run on the cloud and edge and embrace the diversity of languages and developer frameworks. With Dapr's sidecar architecture, you can keep your code platform agnostic while tackling challenges around building microservices, like:

- Calling other services reliably and securely
- Building event-driven apps with pub/sub
- Building applications that are portable across multiple cloud services and hosts (for example, Kubernetes vs. a virtual machine)

Note

If you plan on installing Dapr in a Kubernetes production environment, see the [Dapr guidelines for production usage](https://docs.dapr.io/operations/hosting/kubernetes/kubernetes-production) documentation page.

## How it works

The Dapr extension uses the Azure CLI or a Bicep template to provision the Dapr control plane on your AKS or Arc-enabled Kubernetes cluster, creating the following Dapr services:

| Dapr service | Description |
|---|---|
`dapr-operator` |
Manages component updates and Kubernetes services endpoints for Dapr (state stores, pub/subs, etc.) |
`dapr-sidecar-injector` |
Injects Dapr into annotated deployment pods and adds the environment variables `DAPR_HTTP_PORT` and `DAPR_GRPC_PORT` to enable user-defined applications to easily communicate with Dapr without hard-coding Dapr port values. |
`dapr-placement` |
Used for actors only. Creates mapping tables that map actor instances to pods. |
`dapr-sentry` |
Manages mTLS between services and acts as a certificate authority. For more information, read the
|

Once Dapr is installed on your cluster, you can begin to develop using the Dapr building block APIs by [adding a few annotations](https://docs.dapr.io/operations/hosting/kubernetes/kubernetes-overview/#adding-dapr-to-a-kubernetes-deployment) to your deployments. For a more in-depth overview of the building block APIs and how to best use them, see the [Dapr building blocks overview](https://docs.dapr.io/developing-applications/building-blocks/).

Warning

If you install Dapr through the AKS or Arc-enabled Kubernetes extension, our recommendation is to continue using the extension for future management of Dapr instead of the Dapr CLI. Combining the two tools can cause conflicts and result in undesired behavior.

## Prerequisites

- An Azure subscription.
[Don't have one? Create a free account.](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) - The latest version of the
[Azure CLI](/en-us/cli/azure/install-azure-cli). - An existing
[AKS cluster](tutorial-kubernetes-deploy-cluster)or connected[Arc-enabled Kubernetes cluster](/en-us/azure/azure-arc/kubernetes/quickstart-connect-cluster). [An Azure Kubernetes Service Role-Based Access Control Admin role](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-rbac-admin)

Select how you'd like to install, deploy, and configure the Dapr extension.

## Before you begin

### Add the Azure CLI extension for cluster extensions

Install the `k8s-extension`

Azure CLI extension by running the following commands:

```
az extension add --name k8s-extension
```


If the `k8s-extension`

extension is already installed, you can update it to the latest version using the following command:

```
az extension update --name k8s-extension
```


### Register the `KubernetesConfiguration`

resource provider

If you aren't already using cluster extensions, you may need to register the resource provider with your subscription. You can check the status of the provider registration using the [az provider list](/en-us/cli/azure/provider#az-provider-list) command, as shown in the following example:

```
az provider list --query "[?contains(namespace,'Microsoft.KubernetesConfiguration')]" -o table
```


The *Microsoft.KubernetesConfiguration* provider should report as *Registered*, as shown in the following example output:

```
Namespace RegistrationState RegistrationPolicy
--------------------------------- ------------------- --------------------
Microsoft.KubernetesConfiguration Registered RegistrationRequired
```


If the provider shows as *NotRegistered*, register the provider using the [az provider register](/en-us/cli/azure/provider#az-provider-register) as shown in the following example:

```
az provider register --namespace Microsoft.KubernetesConfiguration
```


### Register the `ExtensionTypes`

feature to your Azure subscription

The `ExtensionTypes`

feature needs to be registered to your Azure subscription. In the terminal, verify you're in the correct subscription:

```
az account set --subscription <YOUR-AZURE-SUBSCRIPTION-ID>
```


Register the `ExtensionTypes`

feature.

```
az feature registration create --namespace Microsoft.KubernetesConfiguration --name ExtensionTypes
```


Feature registration may take some time. After a few minutes, check the registration status using the following command:

```
az feature show --namespace Microsoft.KubernetesConfiguration --name ExtensionTypes
```


## Create the extension and install Dapr on your AKS or Arc-enabled Kubernetes cluster

When installing the Dapr extension, use the flag value that corresponds to your cluster type:

**AKS cluster**:`--cluster-type managedClusters`

.**Arc-enabled Kubernetes cluster**:`--cluster-type connectedClusters`

.

Note

If you're using Dapr OSS on your AKS cluster and would like to install the Dapr extension for AKS, read more about [how to successfully migrate to the Dapr extension](dapr-migration).

Create the Dapr extension, which installs Dapr on your AKS or Arc-enabled Kubernetes cluster.

For example, install the latest version of Dapr via the Dapr extension on your AKS cluster:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name <myAKSCluster> \
--resource-group <myResourceGroup> \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version false
```


### Keep your managed AKS cluster updated to the latest version

Based on your environment (dev, test, or production), you can keep up-to-date with the latest stable Dapr versions.

#### Choosing a release train

When configuring the extension, you can choose to install Dapr from a particular release train. Specify one of the two release train values:

| Value | Description |
|---|---|
`stable` |
Default. |
`dev` |
Early releases that can contain experimental features. Not suitable for production. |

For example:

```
--release-train stable
```


#### Configuring automatic updates to Dapr control plane

Warning

Auto-upgrade is not suitable for production environments. Only enable automatic updates to the Dapr control plane in dev or test environments. [Learn how to manually upgrade to the latest Dapr version for production environments.](#viewing-the-latest-stable-dapr-versions-available)

If you install Dapr without specifying a version, `--auto-upgrade-minor-version`

*is automatically enabled*, configuring the Dapr control plane to automatically update its minor version on new releases.

You can disable auto-update by specifying the `--auto-upgrade-minor-version`

parameter and setting the value to `false`

.

[Dapr versioning is in MAJOR.MINOR.PATCH format](https://docs.dapr.io/operations/support/support-versioning/#versioning), which means

`1.11.0`

to `1.12.0`

is a *minor*version upgrade.

```
--auto-upgrade-minor-version true
```


#### Viewing the latest stable Dapr versions available

To upgrade to the latest Dapr version in a production environment, you need to manually upgrade. Start by viewing a list of the stable Dapr versions available to your managed AKS cluster. Run the following command:

```
az k8s-extension extension-types list-versions-by-cluster --resource-group <myResourceGroup> --cluster-name <myCluster> --cluster-type managedClusters --extension-type microsoft.dapr --release-train stable
```


To see the latest stable Dapr version available to your managed AKS cluster, run the following command:

```
az k8s-extension extension-types list-versions-by-cluster --resource-group <myResourceGroup> --cluster-name <myCluster> --cluster-type managedClusters --extension-type microsoft.dapr --release-train stable --show-latest
```


To view a list of the stable Dapr versions available *by location*:

[Make sure you've registered the](dapr#register-the-extensiontypes-feature-to-your-azure-subscription)`ExtensionTypes`

feature to your Azure subscription.- Run the following command.

```
az k8s-extension extension-types list-versions-by-location --location westus --extension-type microsoft.dapr
```


[Next, manually update Dapr to the latest stable version.](#targeting-a-specific-dapr-version)

#### Targeting a specific Dapr version

Note

Dapr is supported with a rolling window, including only the current and previous versions. It is your operational responsibility to remain up to date with these supported versions. If you have an older version of Dapr, you may have to do intermediate upgrades to get to a supported version.

The same command-line argument is used for installing a specific version of Dapr or rolling back to a previous version. Set `--auto-upgrade-minor-version`

to `false`

and `--version`

to the version of Dapr you wish to install. If the `version`

parameter is omitted, the extension installs the latest version of Dapr. The following example command installs Dapr version `1.14.4-msft.10`

on your AKS cluster:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name <myAKSCluster> \
--resource-group <myResourceGroup> \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version false \
--version 1.14.4-msft.10
```


## Troubleshooting

### Troubleshooting extension management errors

If the extension fails to create or update, try suggestions and solutions in the [Dapr extension troubleshooting guide](dapr-troubleshooting).

### Troubleshooting Dapr functional errors

Troubleshoot Dapr open source errors unrelated to the extension via the [common Dapr issues and solutions guide](https://docs.dapr.io/operations/troubleshooting/common_issues/).

## Support

Note

Learn more about [how Microsoft handles issues raised for the Dapr extension](dapr-overview#issue-handling).

If you're experiencing Dapr runtime security risks and regressions while using the extension, open an issue with the [Dapr open source project](https://github.com/dapr/dapr/issues/new/choose).

You could also start a discussion in the Dapr project Discord:

## Delete the Dapr extension from your cluster

The process of uninstalling the Dapr extension from AKS does not delete the CRDs created during installation. These CRDs remain in the cluster as residual components, essential for the reconciler during the installation and uninstallation of the extension.

To clean the cluster of these CRDs, you can manually delete them **after** the Dapr extension has been completely uninstalled from AKS.

### Uninstalling the extension

Delete the extension from your AKS cluster using the following command:

```
az k8s-extension delete --resource-group <myResourceGroup> --cluster-name <myAKSCluster> --cluster-type managedClusters --name dapr
```


Or, if using a Bicep template, you can delete the template.

### Listing the CRDs in your cluster

To find the CRDs you'd like to remove, run the following command:

```
kubectl get crds | findstr dapr.io
```

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kms-data-encryption-concepts -->

# Data encryption at rest concepts for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) stores sensitive data such as Kubernetes secrets in etcd, the distributed key-value store used by Kubernetes. For enhanced security and compliance requirements, AKS supports encryption of Kubernetes secrets at rest using the Kubernetes Key Management Service (KMS) provider integrated with Azure Key Vault.

This article explains the key concepts, encryption models, and key management options available for protecting Kubernetes secrets at rest in AKS.

## Understanding data encryption at rest

Data encryption at rest protects your data when it's stored on disk. Without encryption at rest, an attacker who gains access to the underlying storage could potentially read sensitive data like Kubernetes secrets.

AKS provides encryption for Kubernetes secrets stored in etcd:

| Layer | Description |
|---|---|
Azure platform encryption |
Azure Storage automatically encrypts all data at rest using 256-bit AES encryption. This encryption is always enabled and transparent to users. |
KMS provider encryption |
An optional layer that encrypts Kubernetes secrets before they're written to etcd using keys stored in Azure Key Vault. |

For more information about Azure's encryption at rest capabilities, see [Azure data encryption at rest](/en-us/azure/security/fundamentals/encryption-atrest) and [Azure encryption models](/en-us/azure/security/fundamentals/encryption-models).

## KMS provider for data encryption

The [Kubernetes KMS provider](https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/) is a mechanism that enables encryption of Kubernetes secrets at rest using an external key management system. AKS integrates with Azure Key Vault to provide this capability, giving you control over encryption keys while maintaining the security benefits of a managed Kubernetes service.

### How KMS encryption works

When you enable KMS for an AKS cluster:

**Secret creation**: When a secret is created, the Kubernetes API server sends the secret data to the KMS provider plugin.**Encryption**: The KMS plugin encrypts the secret data using a Data Encryption Key (DEK), which is itself encrypted using a Key Encryption Key (KEK) stored in Azure Key Vault.**Storage**: The encrypted secret is stored in etcd.**Secret retrieval**: When a secret is read, the KMS plugin decrypts the DEK using the KEK from Azure Key Vault, then uses the DEK to decrypt the secret data.

This envelope encryption approach provides both security and performance benefits. The DEK handles frequent encryption operations locally while the KEK in Azure Key Vault provides the security of a hardware-backed key management system.

## Key management options

AKS offers two key management options for KMS encryption:

### Platform-managed keys (PMK)

With platform-managed keys, AKS automatically manages the encryption keys for you:

- AKS creates and manages the encryption keys.
- Key rotation is handled automatically by the platform.
- No additional configuration or key vault setup is required.

**When to use platform-managed keys:**

- You want the simplest setup with minimal configuration.
- You don't have specific regulatory requirements that mandate customer-managed keys.
- You want automatic key rotation without manual intervention.

### Customer-managed keys (CMK)

With customer-managed keys, you have full control over the encryption keys:

- You create and manage your own Azure Key Vault and encryption keys.
- You control key rotation schedules and policies.

**When to use customer-managed keys:**

- You have regulatory or compliance requirements that mandate customer-managed keys.
- You need to control the key lifecycle, including rotation schedules and key versions.
- You require audit logs for all key operations.

### Key vault network access options

When using customer-managed keys, you can configure the network access for your Azure Key Vault:

| Network access | Description | Use case |
|---|---|---|
Public |
Key vault is accessible over the public internet with authentication. | Development environments, simpler setup |
Private |
Key vault has public network access disabled. AKS accesses the key vault through the
|

## Comparing encryption key options

| Feature | Platform-managed keys | Customer-managed keys (Public) | Customer-managed keys (Private) |
|---|---|---|---|
Key ownership |
Microsoft manages | Customer manages | Customer manages |
Key rotation |
Automatic |
|

[User configurable](/en-us/azure/key-vault/keys/how-to-configure-key-rotation)**Key vault creation****Network isolation**## Requirements

- The new
[KMS encryption with platform-managed keys or customer-managed keys with automatic key rotation](kms-data-encryption)experience requires**Kubernetes version 1.33 or later**. - The new
[KMS encryption with platform-managed keys or customer-managed keys with automatic key rotation](kms-data-encryption)experience is only supported on AKS clusters where[managed identity is used for the cluster's identity](use-managed-identity).

## Limitations

**No downgrade**: After enabling the new KMS encryption experience, you can't disable the feature.**Key deletion**: Deleting the encryption key or key vault makes your secrets unrecoverable.**Private endpoint access**: Key vault access using[private link/endpoint](/en-us/azure/key-vault/general/private-link-service)isn't yet supported. For private key vaults, use the[trusted services firewall exception](/en-us/azure/key-vault/general/network-security#key-vault-firewall-enabled-trusted-services-only).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/dapr-workflow -->

# Deploy and run workflows with the Dapr extension for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

With Dapr Workflow, you can easily orchestrate messaging, state management, and failure-handling logic across various microservices. Dapr Workflow can help you create long-running, fault-tolerant, and stateful applications.

In this guide, you use the [provided order processing workflow example](https://github.com/Azure-Samples/dapr-workflows-aks-sample) to:

- Create an Azure Container Registry and an AKS cluster for this sample.
- Install the Dapr extension on your AKS cluster.
- Deploy the sample application to AKS.
- Start and query workflow instances using HTTP API calls.

The workflow example is an ASP.NET Core project with:

- A
that contains the setup of the app, including the registration of the workflow and workflow activities.`Program.cs`

file - Workflow definitions found in the
.`Workflows`

directory - Workflow activity definitions found in the
.`Activities`

directory

## Prerequisites

- An
[Azure subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)with Owner or Admin role. [An Azure Kubernetes Service Role-Based Access Control Admin role](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-rbac-admin)- The latest version of the
[Azure CLI](/en-us/cli/azure/install-azure-cli) - The latest version of
[Dapr](https://docs.dapr.io/getting-started/install-dapr-cli/) - Latest
[Docker](https://docs.docker.com/get-docker/) - Latest
[Helm](https://helm.sh/docs/intro/install/)

## Set up the environment

### Clone the sample project

Clone the example workflow application.

```
git clone https://github.com/Azure-Samples/dapr-workflows-aks-sample.git
```


Navigate to the sample's root directory.

```
cd dapr-workflows-aks-sample
```


### Create a Kubernetes cluster

Create a resource group to hold the AKS cluster.

```
az group create --name myResourceGroup --location eastus
```


Create an AKS cluster.

```
az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 2 --generate-ssh-keys
```


[Make sure kubectl is installed and pointed to your AKS cluster.](tutorial-kubernetes-deploy-cluster#connect-to-cluster-using-kubectl) If you use the Azure Cloud Shell,

`kubectl`

is already installed.For more information, see the [Deploy an AKS cluster](tutorial-kubernetes-deploy-cluster) tutorial.

## Deploy the application to AKS

### Install Dapr on your AKS cluster

Install the Dapr extension on your AKS cluster. Before you start, make sure you have:

[Installed or updated the](dapr#add-the-azure-cli-extension-for-cluster-extensions).`k8s-extension`

[Registered the](dapr#register-the-kubernetesconfiguration-resource-provider)`Microsoft.KubernetesConfiguration`

service provider

```
az k8s-extension create --cluster-type managedClusters --cluster-name myAKSCluster --resource-group myResourceGroup --name dapr --extension-type Microsoft.Dapr
```


After a few minutes, you'll see output showing the Dapr connection to your AKS cluster. Next, initialize Dapr on your cluster.

```
dapr init -k
```


Verify Dapr is installed:

```
kubectl get pods -A
```


### Deploy the Redis Actor state store component

Navigate to the `Deploy`

directory in your forked version of the sample:

```
cd Deploy
```


Deploy the Redis component:

```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install redis bitnami/redis
kubectl apply -f redis.yaml
```


### Run the application

Once Redis is deployed, deploy the application to AKS:

```
kubectl apply -f deployment.yaml
```


Expose the Dapr sidecar and the sample app:

```
kubectl apply -f service.yaml
export APP_URL=$(kubectl get svc/workflows-sample -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
export DAPR_URL=$(kubectl get svc/workflows-sample-dapr -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
```


Verify that the above commands were exported:

```
echo $APP_URL
echo $DAPR_URL
```


## Start the workflow

Now that the application and Dapr are deployed to the AKS cluster, you can now start and query workflow instances. Restock items in the inventory using the following API call to the sample app:

```
curl -X GET $APP_URL/stock/restock
```


Start the workflow:

```
curl -i -X POST $DAPR_URL/v1.0/workflows/dapr/OrderProcessingWorkflow/start \
-H "Content-Type: application/json" \
-H "dapr-app-id: dwf-app" \
-d '{"Name": "Paperclips", "TotalCost": 99.95, "Quantity": 1}'
```


Expected output includes an auto-generated instance ID:

```
HTTP/1.1 202 Accepted
Content-Type: application/json
Traceparent: 00-00000000000000000000000000000000-0000000000000000-00
Date: Tue, 23 Apr 2024 15:35:00 GMT
Content-Length: 21
{"instanceID":"<generated-id>"}
```


Check the workflow status:

```
curl -i -X GET $DAPR_URL/v1.0/workflows/dapr/OrderProcessingWorkflow/<instance-id> \
-H "dapr-app-id: dwf-app"
```


Expected output:

```
HTTP/1.1 200 OK
Content-Type: application/json
Traceparent: 00-00000000000000000000000000000000-0000000000000000-00
Date: Tue, 23 Apr 2024 15:51:02 GMT
Content-Length: 580
```


Monitor the application logs:

```
kubectl logs -l run=workflows-sample -c workflows-sample --tail=20
```


Expected output:

```
{
"instanceID":"1234",
"workflowName":"OrderProcessingWorkflow",
"createdAt":"2024-04-23T15:35:00.156714334Z",
"lastUpdatedAt":"2024-04-23T15:35:00.176459055Z",
"runtimeStatus":"COMPLETED",
"dapr.workflow.input":"{ \"input\" : {\"Name\": \"Paperclips\", \"TotalCost\": 99.95, \"Quantity\": 1}}",
"dapr.workflow.output":"{\"Processed\":true}"
}
```


Notice that the workflow status is marked as completed.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-metrics-server-vertical-pod-autoscaler -->

# Configure Metrics Server VPA in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Metrics Server](https://kubernetes-sigs.github.io/metrics-server/) is a scalable, efficient source of container resource metrics for Kubernetes built-in autoscaling pipelines. With Azure Kubernetes Service (AKS), vertical pod autoscaling is enabled for the Metrics Server. The Metrics Server is commonly used by other Kubernetes add-ons, like the [Horizontal Pod Autoscaler](concepts-scale#horizontal-pod-autoscaler).

Vertical Pod Autoscaler (VPA) enables you to adjust the resource limit when the Metrics Server is experiencing consistent CPU and memory resource constraints.

## Prerequisites

- An AKS cluster with Kubernetes version 1.24 or higher.
- The Kubernetes command-line tool
`kubectl`

installed on your computer or use Azure Cloud Shell to run`kubectl`

commands.

## Get credentials

To run the `kubectl`

commands, you need your AKS credentials merged into your profile's `.kube/config`

file. Replace `<resourceGroupName>`

and `<clusterName>`

with your cluster's values.

```
az aks get-credentials --resource-group <resourceGroupName> --name <clusterName>
```


## Metrics server throttling

If the Metrics Server throttling rate is high, and the memory usage of its two pods is unbalanced, it's an indication that the Metrics Server needs more resources than the default values.

To update the coefficient values, create a `ConfigMap`

in the overlay `kube-system`

namespace to override the values in the Metrics Server specification. Perform the following steps to update the metrics server.

Create a

`ConfigMap`

file named*metrics-server-config.yaml*and copy the manifest code into the file.`apiVersion: v1 kind: ConfigMap metadata: name: metrics-server-config namespace: kube-system labels: kubernetes.io/cluster-service: "true" addonmanager.kubernetes.io/mode: EnsureExists data: NannyConfiguration: |- apiVersion: nannyconfig/v1alpha1 kind: NannyConfiguration baseCPU: 100m cpuPerNode: 1m baseMemory: 100Mi memoryPerNode: 8Mi`

In the

`ConfigMap`

example, the resource limit and request are changed to the following values where`n`

is the number of nodes:- cpu: (100+1n) millicores
- memory: (100+8n) mebibytes

If you're using Cloud Shell, use

**Manage files**and select**Upload**so the file is available in your Bash session.Create the

`ConfigMap`

using the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify the name of your YAML manifest:`kubectl apply -f metrics-server-config.yaml`

Restart the two Metrics Server pods using

[kubectl rollout restart](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#rollout). The following command deletes both pods and new pods are created.`kubectl rollout restart -n kube-system deployment metrics-server`

The new Metrics Server pods are created before the old pods are terminated so there isn't downtime.

List the pods using

[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)to get the new Metrics Server pod names that are used in the next command.`kubectl get pods --namespace kube-system`

`NAME READY STATUS RESTARTS AGE metrics-server-1a2b333c44-wxyz5 2/2 Running 0 15s metrics-server-1a2b333c44-abcd6 2/2 Running 0 15s`

If you notice a third Metrics Server pod with a longer age value, it's because the termination occurs after the new pods are available.

To verify the updated resources took effect for each pod, run the following command to review the Metrics Server VPA log. Replace

`<metrics-server-pod-name>`

with the name of each of your metrics server pods.`kubectl -n kube-system logs <metrics-server-pod-name> -c metrics-server-vpa`

The following example output resembles the results showing the updated throttling settings were applied.

`I0811 19:08:34.930865 1 pod_nanny.go:86] Invoked by [/pod_nanny --config-dir=/etc/config --cpu=150m --extra-cpu=0.5m --memory=100Mi --extra-memory=4Mi --poll-period=180000 --threshold=5 --deployment=metrics-server --container=metrics-server] I0811 19:08:34.931128 1 pod_nanny.go:87] Version: 1.8.23 I0811 19:08:34.931200 1 pod_nanny.go:109] Watching namespace: kube-system, pod: <metrics-server-pod-name>, container: metrics-server. I0811 19:08:34.931249 1 pod_nanny.go:110] storage: MISSING, extra_storage: 0Gi I0811 19:08:34.932085 1 pod_nanny.go:144] cpu: 100m, extra_cpu: 1m, memory: 100Mi, extra_memory: 8Mi I0811 19:08:34.932177 1 pod_nanny.go:278] Resources: [{Base:{i:{value:100 scale:-3} d:{Dec:<nil>} s:100m Format:DecimalSI} ExtraPerResource:{i:{value:1 scale:-3} d:{Dec:<nil>} s:1m Format:DecimalSI} Name:cpu} {Base:{i:{value:104857600 scale:0} d:{Dec:<nil>} s:100Mi Format:BinarySI} ExtraPerResource:{i:{value:8388608 scale:0} d:{Dec:<nil>} s: Format:BinarySI} Name:memory}]`


Be cautious of the `baseCPU`

, `cpuPerNode`

, `baseMemory`

, and the `memoryPerNode`

, because AKS doesn't validate the `ConfigMap`

. As a recommended practice, increase the value gradually to avoid unnecessary resource consumption. Proactively monitor resource usage when updating or creating the `ConfigMap`

. A large number of resource requests could negatively affect the node.

## Manually configure Metrics Server resource usage

The Metrics Server VPA adjusts resource usage by the number of nodes. If the cluster scales up or down often, the Metrics Server might restart frequently. In this case, you can bypass VPA and manually control its resource usage. This method to configure VPA isn't to be performed in addition to the steps described in the previous section.

If you would like to bypass VPA for Metrics Server and manually control its resource usage, perform the following steps.

Create a

`ConfigMap`

file named*metrics-server-config.yaml*and copy in the following manifest.`apiVersion: v1 kind: ConfigMap metadata: name: metrics-server-config namespace: kube-system labels: kubernetes.io/cluster-service: "true" addonmanager.kubernetes.io/mode: EnsureExists data: NannyConfiguration: |- apiVersion: nannyconfig/v1alpha1 kind: NannyConfiguration baseCPU: 100m cpuPerNode: 0m baseMemory: 100Mi memoryPerNode: 0Mi`

In this

`ConfigMap`

example, the resource limit and request are changed to the following values that don't trigger autoscaling:- cpu: 100 millicores
- memory: 100 mebibytes

If you're using Cloud Shell, use

**Manage files**and select**Upload**so the file is available in your Bash session.Create the

`ConfigMap`

using the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify the name of your YAML manifest:`kubectl apply -f metrics-server-config.yaml`

Restart the two Metrics Server pods using

[kubectl rollout restart](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#rollout). The following command deletes both pods and new pods are created.`kubectl rollout restart -n kube-system deployment metrics-server`

The new Metrics Server pods are created before the old pods are terminated so there isn't downtime.

List the pods using

[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)to get the new Metrics Server pod names that are used in the next command.`kubectl get pods --namespace kube-system`

`NAME READY STATUS RESTARTS AGE metrics-server-1a2b333c44-wxyz5 2/2 Running 0 15s metrics-server-1a2b333c44-abcd6 2/2 Running 0 15s`

If you notice a third Metrics Server pod with a longer age value, it's because the termination occurs after the new pods are available.

To verify the updated resources took effect for each pod, run the following command to review the Metrics Server VPA log. Replace

`<metrics-server-pod-name>`

with the name of each of your metrics server pods.`kubectl -n kube-system logs <metrics-server-pod-name> -c metrics-server-vpa`

The following example output resembles the results showing the updated throttling settings were applied.

`I0811 19:19:06.235018 1 pod_nanny.go:86] Invoked by [/pod_nanny --config-dir=/etc/config --cpu=150m --extra-cpu=0.5m --memory=100Mi --extra-memory=4Mi --poll-period=180000 --threshold=5 --deployment=metrics-server --container=metrics-server] I0811 19:19:06.235105 1 pod_nanny.go:87] Version: 1.8.23 I0811 19:19:06.235136 1 pod_nanny.go:109] Watching namespace: kube-system, pod: <metrics-server-pod-name>, container: metrics-server. I0811 19:19:06.235171 1 pod_nanny.go:110] storage: MISSING, extra_storage: 0Gi I0811 19:19:06.235899 1 pod_nanny.go:144] cpu: 100m, extra_cpu: 0m, memory: 100Mi, extra_memory: 0Mi I0811 19:19:06.235917 1 pod_nanny.go:278] Resources: [{Base:{i:{value:100 scale:-3} d:{Dec:<nil>} s:100m Format:DecimalSI} ExtraPerResource:{i:{value:0 scale:-3} d:{Dec:<nil>} s: Format:DecimalSI} Name:cpu} {Base:{i:{value:104857600 scale:0} d:{Dec:<nil>} s:100Mi Format:BinarySI} ExtraPerResource:{i:{value:0 scale:0} d:{Dec:<nil>} s: Format:BinarySI} Name:memory}]`


## Troubleshooting

### ConfigMap error

If you apply the following `ConfigMap`

, the Metrics Server VPA customizations aren't applied. You need add a unit for `baseCPU`

like `baseCPU: 100m`

that includes the `m`

unit.

```
apiVersion: v1
kind: ConfigMap
metadata:
name: metrics-server-config
namespace: kube-system
labels:
kubernetes.io/cluster-service: "true"
addonmanager.kubernetes.io/mode: EnsureExists
data:
NannyConfiguration: |-
apiVersion: nannyconfig/v1alpha1
kind: NannyConfiguration
baseCPU: 100
cpuPerNode: 1m
baseMemory: 100Mi
memoryPerNode: 8Mi
```


The following example output resembles the results showing the updated throttling settings aren't applied.

```
I0811 19:25:33.992691 1 pod_nanny.go:86] Invoked by [/pod_nanny --config-dir=/etc/config --cpu=150m --extra-cpu=0.5m --memory=100Mi --extra-memory=4Mi --poll-period=180000 --threshold=5 --deployment=metrics-server --container=metrics-server]
I0811 19:25:33.992890 1 pod_nanny.go:87] Version: 1.8.23
I0811 19:25:33.992918 1 pod_nanny.go:109] Watching namespace: kube-system, pod: <metrics-server-pod-name>, container: metrics-server.
I0811 19:25:33.992937 1 pod_nanny.go:110] storage: MISSING, extra_storage: 0Gi
I0811 19:25:33.993586 1 pod_nanny.go:217] Unable to decode Nanny Configuration from config map, using default parameters
I0811 19:25:33.993602 1 pod_nanny.go:144] cpu: 150m, extra_cpu: 0.5m, memory: 100Mi, extra_memory: 4Mi
I0811 19:25:33.993610 1 pod_nanny.go:278] Resources: [{Base:{i:{value:150 scale:-3} d:{Dec:<nil>} s:150m Format:DecimalSI} ExtraPerResource:{i:{value:5 scale:-4} d:{Dec:<nil>} s: Format:DecimalSI} Name:cpu} {Base:{i:{value:104857600 scale:0} d:{Dec:<nil>} s:100Mi Format:BinarySI} ExtraPerResource:{i:{value:4194304 scale:0} d:{Dec:<nil>} s:4Mi Format:BinarySI} Name:memory}]
```


### PodDisruptionBudget

For Kubernetes version 1.23 and higher clusters, Metrics Server has a `PodDisruptionBudget`

. It ensures the number of available Metrics Server pods is at least one. If you get something like this after running `kubectl get pods --namespace kube-system`

, it's possible that the customized resource usage is small. Increase the coefficient values to resolve it.

```
metrics-server-1a2b333c44-wxyz5 1/2 CrashLoopBackOff 6 (36s ago) 6m33s
metrics-server-1a2b333c44-abcd6 1/2 CrashLoopBackOff 6 (54s ago) 6m33s
metrics-server-5d69966543-hcrff 2/2 Running 0 37m
```


## Next steps

Metrics Server is a component in the core metrics pipeline. For more information, see [Metrics Server API design](https://kubernetes.io/docs/tasks/debug/debug-cluster/resource-metrics-pipeline/).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/release-tracker -->

# AKS release tracker

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS releases weekly rounds of fixes and feature and component updates that affect all clusters and customers. It's important for you to know when a particular AKS release is hitting your region, and the AKS release tracker provides these details in real time by versions and regions.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Overview

With AKS release tracker, you can follow specific component updates present in an AKS version release, such as fixes shipped to a core add-on, and node image updates for Azure Linux, Ubuntu, and Windows. The tracker provides links to the specific version of the AKS [release notes](https://github.com/Azure/AKS/releases) to help you identify relevant release instances. Real time data updates allow you to track the release order and status of each region.

## Use the release tracker

To view the release tracker, visit the [AKS release status webpage](https://releases.aks.azure.com/webpage/index.html).

### AKS releases

The top half of the tracker shows the current latest version and three previously available release versions for each region and links to the corresponding release notes entries. This view is helpful when you want to track the available versions by region.


The bottom half of the tracker shows the release order. The table has two views: *By Region* and *By Version*.


### AKS node image updates

The top half of the tracker shows the current latest node image version and three previously available node image versions for each region. This view is helpful when you want to track the available node image versions by region.


The bottom half of the tracker shows the node image update order. The table has two views: *By Region* and *By Version*.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/update-kms-key-vault -->

# Update the key vault mode for an Azure Kubernetes Service (AKS) cluster with Key Management Service (KMS) etcd encryption (legacy)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to update the key vault mode from public to private or private to public for an Azure Kubernetes Service (AKS) cluster with Key Management Service (KMS) etcd encryption.

## Prerequisites

- An AKS cluster with KMS etcd encryption enabled. For more information, see
[Add Key Management Service (KMS) etcd encryption to an Azure Kubernetes Service (AKS) cluster](use-kms-etcd-encryption). - Azure CLI version 2.39.0 or later. Find your version using the
`az --version`

command. If you need to install or upgrade, see[Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

## Update a key vault mode

Note

To change a different key vault with a different mode (whether public or private), you can run [ az aks update](/en-us/cli/azure/aks#az-aks-update) directly. To change the mode of an attached key vault, you must first turn off KMS, then turn it on again using the new key vault IDs.

Turn off KMS on the existing cluster and release the key vault using the

command with the`az aks update`

`--disable-azure-keyvault-kms`

parameter.`az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --disable-azure-keyvault-kms`

Warning

After you turn off KMS, the encryption key vault key is still needed. You can't delete or expire it.

Update all secrets using the

`kubectl get secrets`

command to ensure the secrets created earlier are no longer encrypted. For larger clusters, you might want to subdivide the secrets by namespace or create an update script. If the previous command to update KMS fails, still run the following command to avoid unexpected state for KMS plugin.`kubectl get secrets --all-namespaces -o json | kubectl replace -f -`

When you run the command, the following error is safe to ignore:

`The object has been modified; please apply your changes to the latest version and try again.`

Update the key vault from public to private using the

command with the`az keyvault update`

`--public-network-access`

parameter set to`Disabled`

.`az keyvault update --name $KEY_VAULT --resource-group $RESOURCE_GROUP --public-network-access Disabled`

Turn on KMS with the updated private key vault using the

command with the`az aks update`

`--azure-keyvault-kms-key-vault-network-access`

parameter set to`Private`

.`az aks update \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --enable-azure-keyvault-kms \ --azure-keyvault-kms-key-id $KEY_ID \ --azure-keyvault-kms-key-vault-network-access "Private" \ --azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-capacity-reservation-groups -->

# Assign capacity reservation groups to Azure Kubernetes Service (AKS) node pools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As your workload demands change, you can associate existing [capacity reservation groups (CRGs)](/en-us/azure/virtual-machines/capacity-reservation-associate-virtual-machine-scale-set) to your Azure Kubernetes Service (AKS) node pools to guarantee allocated capacity for them. Capacity reservation groups allow you to reserve compute capacity in an Azure region or availability zone for any duration of time. This feature is useful for workloads that require guaranteed capacity, such as those with predictable traffic patterns or those that need to meet specific performance requirements.

In this article, you learn how to use capacity reservation groups with node pools in AKS.

Note

Deleting a node pool implicitly dissociates that node pool from any associated capacity reservation group before the node pool is deleted. Deleting a cluster implicitly dissociates all node pools in that cluster from their associated capacity reservation groups.

## Prerequisites for using capacity reservation groups with AKS node pools

- You need the Azure CLI version 2.56 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You need an existing
[capacity reservation group](/en-us/azure/virtual-machines/capacity-reservation-associate-virtual-machine-scale-set)with at least one capacity reservation. If not, the node pool is added to the cluster with a warning and no capacity reservation group gets associated. - You need to
[create a user-assigned managed identity with the](#create-a-user-assigned-managed-identity-and-assign-it-to-an-aks-cluster)for the resource group that contains the capacity reservation group and assign the identity to your AKS cluster. System-assigned managed identities don't work for this feature.`Contributor`

role

### Create a user-assigned managed identity and assign it to an AKS cluster

Create a user-assigned managed identity using the

command.`az identity create`

`az identity create --name <identity-name> --resource-group <resource-group-name> --location <location>`

Get the ID of the user-assigned managed identity using the

command and set it to an environment variable.`az identity show`

`IDENTITY_ID=$(az identity show --name <identity-name> --resource-group <resource-group-name> --query identity.id -o tsv)`

Assign the

`Contributor`

role to the user-assigned identity using thecommand.`az role assignment create`

`az role assignment create --assignee $IDENTITY_ID --role "Contributor" --scope /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>`

It can take up to

*60 minutes*for the role assignment to propagate.Assign the user-assigned managed identity to a new or existing AKS cluster using the

`--assign-identity`

flag with theor`az aks create`

command.`az aks update`

`# Create a new AKS cluster with the user-assigned managed identity az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --location <location> \ --node-vm-size <vm-size> --node-count <node-count> \ --assign-identity $IDENTITY_ID \ --generate-ssh-keys # Update an existing AKS cluster to use the user-assigned managed identity az aks update \ --resource-group <resource-group-name> \ --name <cluster-name> \ --location <location> \ --node-vm-size <vm-size> \ --node-count <node-count> \ --enable-managed-identity \ --assign-identity $IDENTITY_ID`


## Limitations for using capacity reservation groups with AKS node pools

You can't update an existing node pool with a capacity reservation group. Instead, you need to create a new node pool with the `--crg-id`

flag to associate it with the capacity reservation group. You can also associate an existing capacity reservation group with a system node pool during cluster creation.

## Get the ID of an existing capacity reservation group

Get the ID of an existing capacity reservation group using the

command and set it to an environment variable.`az capacity reservation group show`

`CRG_ID=$(az capacity reservation group show --capacity-reservation-group <crg-name> --resource-group <resource-group-name> --query id -o tsv)`


## Associate an existing capacity reservation group with a node pool

Associate an existing capacity reservation group with a node pool using the

command with the`az aks nodepool add`

`--crg-id`

flag. The following example assumes you have a CRG named "myCRG".`az aks nodepool add --resource-group <resource-group-name> --cluster-name <cluster-name> --name <node-pool-name> --crg-id $CRG_ID`


## Associate an existing capacity reservation group with a system node pool

To associate an existing capacity reservation group with a system node pool, you need to assign the user-assigned managed identity with the `Contributor`

role to the cluster during cluster creation. You can then use the `--crg-id`

flag to associate the capacity reservation group with the system node pool.

Create a new AKS cluster with the user-assigned managed identity and associate it with the capacity reservation group using the

`--assign-identity`

and`--crg-id`

flags with thecommand.`az aks create`

`az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --location <location> \ --node-vm-size <vm-size> --node-count <node-count> \ --assign-identity $IDENTITY_ID \ --crg-id $CRG_ID \ --generate-ssh-keys`


## Next steps: Manage node pools in AKS

To learn more about managing node pools in AKS, see [Manage node pools in Azure Kubernetes Service (AKS)](manage-node-pools).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/best-practices-performance-scale -->

# Best practices for performance and scaling for small to medium workloads in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This article focuses on general best practices for **small to medium workloads**. For best practices specific to **large workloads**, see [Performance and scaling best practices for large workloads in Azure Kubernetes Service (AKS)](best-practices-performance-scale-large).

As you deploy and maintain clusters in AKS, you can use the following best practices to help you optimize performance and scaling.

In this article, you learn about:

- Tradeoffs and recommendations for autoscaling your workloads.
- Managing node scaling and efficiency based on your workload demands.
- Networking considerations for ingress and egress traffic.
- Monitoring and troubleshooting control plane and node performance.
- Capacity planning, surge scenarios, and cluster upgrades.
- Storage and networking considerations for data plane performance.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Application autoscaling vs. infrastructure autoscaling

### Application autoscaling

Application autoscaling is useful when dealing with cost optimization or infrastructure limitations. A well-configured autoscaler maintains high availability for your application while also minimizing costs. You only pay for the resources required to maintain availability, regardless of the demand.

For example, if an existing node has space but not enough IPs in the subnet, it might be able to skip the creation of a new node and instead immediately start running the application on a new pod.

#### Horizontal Pod autoscaling

Implementing [horizontal pod autoscaling](concepts-scale#horizontal-pod-autoscaler) is useful for applications with a steady and predictable resource demand. The Horizontal Pod Autoscaler (HPA) dynamically scales the number of pod replicas, which effectively distributes the load across multiple pods and nodes. This scaling mechanism is typically most beneficial for applications that can be decomposed into smaller, independent components capable of running in parallel.

The HPA provides resource utilization metrics by default. You can also integrate custom metrics or leverage tools like the [Kubernetes Event-Driven Autoscaler (KEDA) (Preview)](keda-about). These extensions allow the HPA to make scaling decisions based on multiple perspectives and criteria, providing a more holistic view of your application's performance. This is especially helpful for applications with varying complex scaling requirements.

Note

If maintaining high availability for your application is a top priority, we recommend leaving a slightly higher buffer for the minimum pod number for your HPA to account for scaling time.

#### Vertical Pod autoscaling

Implementing [vertical pod autoscaling](vertical-pod-autoscaler) is useful for applications with fluctuating and unpredictable resource demands. The Vertical Pod Autoscaler (VPA) allows you to fine-tune resource requests, including CPU and memory, for individual pods, enabling precise control over resource allocation. This granularity minimizes resource waste and enhances the overall efficiency of cluster utilization. The VPA also streamlines application management by automating resource allocation, freeing up resources for critical tasks.

Warning

You shouldn't use the VPA in conjunction with the HPA on the same CPU or memory metrics. This combination can lead to conflicts, as both autoscalers attempt to respond to changes in demand using the same metrics. However, you can use the VPA for CPU or memory in conjunction with the HPA for custom metrics to prevent overlap and ensure that each autoscaler focuses on distinct aspects of workload scaling.

Note

The VPA works based on historical data. We recommend waiting at least *24 hours* after deploying the VPA before applying any changes to give it time to collect recommendation data.

### Infrastructure autoscaling

#### Cluster autoscaling

Implementing cluster autoscaling is useful if your existing nodes lack sufficient capacity, as it helps with scaling up and provisioning new nodes.

When considering cluster autoscaling, the decision of when to remove a node involves a tradeoff between optimizing resource utilization and ensuring resource availability. Eliminating underutilized nodes enhances cluster utilization but might result in new workloads having to wait for resources to be provisioned before they can be deployed. It's important to find a balance between these two factors that aligns with your cluster and workload requirements and [configure the cluster autoscaler profile settings accordingly](cluster-autoscaler#update-the-cluster-autoscaler-settings).

The Cluster Autoscaler profile settings apply universally to all autoscaler-enabled node pools in your cluster. This means that any scaling actions occurring in one autoscaler-enabled node pool might impact the autoscaling behavior in another node pool. It's important to apply consistent and synchronized profile settings across all relevant node pools to ensure that the autoscaler behaves as expected.

##### Overprovisioning

Overprovisioning is a strategy that helps mitigate the risk of application pressure by ensuring there's an excess of readily available resources. This approach is especially useful for applications that experience highly variable loads and cluster scaling patterns that show frequent scale ups and scale downs.

To determine the optimal amount of overprovisioning, you can use the following formula:

```
1-buffer/1+traffic
```


For example, let's say you want to avoid hitting 100% CPU utilization in your cluster. You might opt for a 30% buffer to maintain a safety margin. If you anticipate an average traffic growth rate of 40%, you might consider overprovisioning by 50%, as calculated by the formula:

```
1-30%/1+40%=50%
```


An effective overprovisioning method involves the use of *pause pods*. Pause pods are low-priority deployments that can be easily replaced by high-priority deployments. You create low priority pods that serve the sole purpose of reserving buffer space. When a high-priority pod requires space, the pause pods are removed and rescheduled on another node or a new node to accommodate the high priority pod.

The following YAML shows an example pause pod manifest:

```
apiVersion: scheduling.k8s.io/v1
kind: PriorityClass
metadata:
name: overprovisioning
value: -1
globalDefault: false
description: "Priority class used by overprovisioning."
---
apiVersion: apps/v1
kind: Deployment
metadata:
name: overprovisioning
namespace: kube-system
spec:
replicas: 1
selector:
matchLabels:
run: overprovisioning
template:
metadata:
labels:
run: overprovisioning
spec:
priorityClassName: overprovisioning
containers:
- name: reserve-resources
image: your-custome-pause-image
resources:
requests:
cpu: 1
memory: 4Gi
```


## Node scaling and efficiency


Best practice guidance:Carefully monitor resource utilization and scheduling policies to ensure nodes are being used efficiently.


Node scaling allows you to dynamically adjust the number of nodes in your cluster based on workload demands. It's important to understand that adding more nodes to a cluster isn't always the best solution for improving performance. To ensure optimal performance, you should carefully monitor resource utilization and scheduling policies to ensure nodes are being used efficiently.

### Node images


Best practice guidance:Use the latest node image version to ensure that you have the latest security patches and bug fixes.


Using the latest node image version provides the best performance experience. AKS ships performance improvements within the weekly image releases. The latest daemonset images are cached on the latest VHD image, which provide lower latency benefits for node provisioning and bootstrapping. Falling behind on updates might have a negative impact on performance, so it's important to avoid large gaps between versions.

#### Azure Linux

The [Azure Linux Container Host on AKS](/en-us/azure/azure-linux/intro-azure-linux) uses a native AKS image and provides a single place for Linux development. Every package is built from source and validated, ensuring your services run on proven components.

Azure Linux is lightweight, only including the necessary set of packages to run container workloads. It provides a reduced attack surface and eliminates patching and maintenance of unnecessary packages. At its base layer, it has a Microsoft-hardened kernel tuned for Azure. This image is ideal for performance-sensitive workloads and platform engineers or operators that manage fleets of AKS clusters.

#### Ubuntu 2204

The [Ubuntu 2204 image](https://github.com/Azure/AKS/blob/master/CHANGELOG.md) is the default node image for AKS. It's a lightweight and efficient operating system optimized for running containerized workloads. This means that it can help reduce resource usage and improve overall performance. The image includes the latest security patches and updates, which help ensure that your workloads are protected from vulnerabilities.

The Ubuntu 2204 image is fully supported by Microsoft, Canonical, and the Ubuntu community and can help you achieve better performance and security for your containerized workloads.

### Virtual machines (VMs)


Best practice guidance:When selecting a VM, ensure the size and performance of the OS disk and VM SKU don't have a large discrepancy. A discrepancy in size or performance can cause performance issues and resource contention.


Application performance is closely tied to the VM SKUs you use in your workloads. Larger and more powerful VMs, generally provide better performance. For *mission critical or product workloads*, we recommend using VMs with at least an 8-core CPU. VMs with newer hardware generations, like v4 and v5, can also help improve performance. Keep in mind that create and scale latency might vary depending on the VM SKUs you use.

### Use dedicated system node pools

For scaling performance and reliability, we recommend using a dedicated system node pool. With this configuration, the dedicated system node pool reserves space for critical system resources such as system OS daemons. Your application workload can then run in a user node pool to increase the availability of allocatable resources for your application. This configuration also helps mitigate the risk of resource competition between the system and application.

### Create operations

Review the extensions and add-ons you have enabled during create provisioning. Extensions and add-ons can add latency to overall duration of create operations. If you don't need an extension or add-on, we recommend removing it to improve create latency.

You can also use availability zones to provide a higher level of availability to protect against potential hardware failures or planned maintenance events. AKS clusters distribute resources across logical sections of underlying Azure infrastructure. Availability zones physically separate nodes from other nodes to help ensure that a single failure doesn't impact the availability of your application. Availability zones are only available in certain regions. For more information, see [Availability zones in Azure](/en-us/azure/reliability/availability-zones-overview).

## Kubernetes API server

### LIST and WATCH operations

Kubernetes uses the LIST and WATCH operations to interact with the Kubernetes API server and monitor information about cluster resources. These operations are fundamental to how Kubernetes performs resource management.

**The LIST operation retrieves a list of resources that fit within certain criteria**, such as all pods in a specific namespace or all services in the cluster. This operation is useful when you want to get an overview of your cluster resources or you need to operator on multiple resources at once.

The LIST operation can retrieve large amounts of data, especially in large clusters with multiple resources. Be mindful of the fact that making unbounded or frequent LIST calls puts a significant load on the API server and can close down response times.

**The WATCH operation performs real-time resource monitoring**. When you set up a WATCH on a resource, the API server sends you updates whenever there are changes to that resource. This is important for controllers, like the ReplicaSet controller, which rely on WATCH to maintain the desired state of resources.

Be mindful of the fact that watching too many mutable resources or making too many concurrent WATCH requests can overwhelm the API server and cause excessive resource consumption.

To avoid potential issues and ensure the stability of the Kubernetes control plane, you can use the following strategies:

**Resource quotas**

Implement resource quotas to limit the number of resources that can be listed or watched by a particular user or namespace to prevent excessive calls.

**API Priority and Fairness**

Kubernetes introduced the concept of API Priority and Fairness (APF) to prioritize and manage API requests. You can use APF in Kubernetes to protect the cluster's API server and reduce the number of `HTTP 429 Too Many Requests`

responses seen by client applications.

| Custom resource | Key features |
|---|---|
| PriorityLevelConfigurations | * Define different priority levels for API requests. * Specifies a unique name and assigns an integer value representing the priority level. Higher priority levels have lower integer values, indicating they're more critical. * Can use multiple to categorize requests into different priority levels based on their importance. * Allow you to specify whether requests at a particular priority level should be subject to rate limits. |
| FlowSchemas | * Define how API requests should be routed to different priority levels based on request attributes. * Specify rules that match requests based on criteria like API groups, versions, and resources. * When a request matches a given rule, the request is directed to the priority level specified in the associated PriorityLevelConfiguration. * Can use to set the order of evaluation when multiple FlowSchemas match a request to ensure that certain rules take precedence. |

Configuring API with PriorityLevelConfigurations and FlowSchemas enables the prioritization of critical API requests over less important requests. This ensures that essential operations don't starve or experience delays because of lower priority requests.

**Optimize labeling and selectors**

When using LIST operations, optimize label selectors to narrow down the scope of the resources you want to query to reduce the amount of data returned and the load on the API server.

In Kubernetes CREATE and UPDATE operations refer to actions that manage and modify cluster resources.

### CREATE and UPDATE operations

**The CREATE operation creates new resources in the Kubernetes cluster**, such as pods, services, deployments, configmaps, and secrets. During a CREATE operation, a client, such as `kubectl`

or a controller, sends a request to the Kubernetes API server to create the new resource. The API server validates the request, ensures compliance with any admission controller policies, and then creates the resource in the cluster's desired state.

**The UPDATE operation modifies existing resources in the Kubernetes cluster**, including changes to resources specifications, like number of replicas, container images, environment variables, or labels. During an UPDATE operation, a client sends a request to the API server to update an existing resource. The API server validates the request, applies the changes to the resource definition, and updates the cluster resource.

CREATE and UPDATE operations can impact the performance of the Kubernetes API server under the following conditions:

**High concurrency**: When multiple users or applications make concurrent CREATE or UPDATE requests, it can lead to a surge in API requests arriving at the server at the same time. This can stress the API server's processing capacity and cause performance issues.**Complex resource definitions**: Resource definitions that are overly complex or involve multiple nested objects can increase the time it takes for the API server to validate and process CREATE and UPDATE requests, which can lead to performance degradation.**Resource validation and admission control**: Kubernetes enforces various admission control policies and validation checks on incoming CREATE and UPDATE requests. Large resource definitions, like ones with extensive annotations or configurations, might require more processing time.**Custom controllers**: Custom controllers that watch for changes in resources, like Deployments or StatefulSet controllers, can generate a significant number of updates when scaling or rolling out changes. These updates can strain the API server's resources.

For more information, see [Troubleshoot API server and etcd problems in AKS](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-apiserver-etcd).

## Data plane performance

The Kubernetes data plane is responsible for managing network traffic between containers and services. Issues with the data plane can lead to slow response times, degraded performance, and application downtime. It's important to carefully monitor and optimize data plane configurations, such as network latency, resource allocation, container density, and network policies, to ensure your containerized applications run smoothly and efficiently.

### Storage types

AKS recommends and defaults to using ephemeral OS disks. Ephemeral OS disks are created on local VM storage and aren't saved to remote Azure storage like managed OS disks. They have faster reimaging and boot times, enabling faster cluster operations, and they provide lower read/write latency on the OS disk of AKS agent nodes. Ephemeral OS disks work well for stateless workloads, where applications are tolerant of individual VM failures but not of VM deployment time or individual VM reimaging instances. Only certain VM SKUs support ephemeral OS disks, so you need to ensure that your desired SKU generation and size is compatible. For more information, see [Ephemeral OS disks in Azure Kubernetes Service (AKS)](cluster-configuration#use-ephemeral-os-on-new-clusters).

If your workload is unable to use ephemeral OS disks, AKS defaults to using Premium SSD OS disks. If Premium SSD OS disks aren't compatible with your workload, AKS defaults to Standard SSD disks. Currently, the only other available OS disk type is Standard HDD. For more information, see [Storage options in Azure Kubernetes Service (AKS)](concepts-storage).

The following table provides a breakdown of suggested use cases for OS disks supported in AKS:

| OS disk type | Key features | Suggested use cases |
|---|---|---|
| Ephemeral OS disks | * Faster reimaging and boot times. * Lower read/write latency on OS disk of AKS agent nodes. * High performance and availability. |
* Demanding enterprise workloads, such as SQL Server, Oracle, Dynamics, Exchange Server, MySQL, Cassandra, MongoDB, SAP Business Suite, etc. * Stateless production workloads that require high availability and low latency. |
| Premium SSD OS disks | * Consistent performance and low latency. * High availability. |
* Demanding enterprise workloads, such as SQL Server, Oracle, Dynamics, Exchange Server, MySQL, Cassandra, MongoDB, SAP Business Suite, etc. * Input/output (IO) intensive enterprise workloads. |
| Standard SSD OS disks | * Consistent performance. * Better availability and latency compared to Standard HDD disks. |
* Web servers. * Low input/output operations per second (IOPS) application servers. * Lightly used enterprise applications. * Dev/test workloads. |
| Standard HDD disks | * Low cost. * Exhibits variability in performance and latency. |
* Backup storage. * Mass storage with infrequent access. |

#### IOPS and throughput

Input/output operations per second (IOPS) refers to the number of read and write operations that a disk can perform in a second. Throughput refers to the amount of data that can be transferred in a given time period.

OS disks are responsible for storing the operating system and its associated files, and the VMs are responsible for running the applications. When selecting a VM, ensure the size and performance of the OS disk and VM SKU don't have a large discrepancy. A discrepancy in size or performance can cause performance issues and resource contention. For example, if the OS disk is significantly smaller than the VMs, it can limit the amount of space available for application data and cause the system to run out of disk space. If the OS disk has lower performance than the VMs, it can become a bottleneck and limit the overall performance of the system. Make sure the size and performance are balanced to ensure optimal performance in Kubernetes.

You can use the following steps to monitor IOPS and bandwidth meters on OS disks in the Azure portal:

- Navigate to the
[Azure portal](https://portal.azure.com/). - Search for
**Virtual machine scale sets**and select your virtual machine scale set. - Under
**Monitoring**, select**Metrics**.

Ephemeral OS disks can provide dynamic IOPS and throughput for your application, whereas managed disks have capped IOPS and throughput. For more information, see [Ephemeral OS disks for Azure VMs](/en-us/azure/virtual-machines/ephemeral-os-disks).

[Azure Premium SSD v2](/en-us/azure/virtual-machines/disks-types#premium-ssd-v2) is designed for IO-intense enterprise workloads that require sub-millisecond disk latencies and high IOPS and throughput at a low cost. It's suited for a broad range of workloads, such as SQL server, Oracle, MariaDB, SAP, Cassandra, MongoDB, big data/analytics, gaming, and more. This disk type is the highest performing option currently available for persistent volumes.

### Pod scheduling

The memory and CPU resources allocated to a VM have a direct impact on the performance of the pods running on the VM. When a pod is created, it's assigned a certain amount of memory and CPU resources, which are used to run the application. If the VM doesn't have enough memory or CPU resources available, it can cause the pods to slow down or even crash. If the VM has too much memory or CPU resources available, it can cause the pods to run inefficiently, wasting resources and increasing costs. We recommend monitoring the total pod requests across your workloads against the total allocatable resources for best scheduling predictability and performance. You can also set the maximum pods per node based on your capacity planning using `--max-pods`

.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-network-isolated -->

# Network isolated Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Organizations typically have strict security and compliance requirements to regulate egress (outbound) network traffic from a cluster to eliminate risks of data exfiltration. By default, standard SKU Azure Kubernetes Service (AKS) clusters have unrestricted outbound internet access. This level of network access allows nodes and services you run to access external resources as needed. If you wish to restrict egress traffic, a limited number of ports and addresses must be accessible to maintain healthy cluster maintenance tasks. The conceptual document on [outbound network and fully qualified domain name (FQDN) rules for AKS clusters](outbound-rules-control-egress) provides a list of required endpoints for the AKS cluster and its optional add-ons and features.

One common solution to restricting outbound traffic from the cluster is to use a [firewall device](limit-egress-traffic) to restrict traffic based on firewall rules. Firewall is applicable when your application requires outbound access, but when outbound requests have to be inspected and secured. Configuring a firewall manually with required egress rules and *FQDNs* is a cumbersome process especially if your only requirement is to create an isolated AKS cluster with no outbound dependencies for the cluster bootstrapping.

To reduce risk of data exfiltration, network isolated cluster allows for bootstrapping the AKS cluster without any outbound network dependencies, even for fetching cluster components/images from Microsoft Artifact Registry (MAR). The cluster operator could incrementally set up allowed outbound traffic for each scenario they want to enable.

## How a network isolated cluster works

The following diagram shows the network communication between dependencies for a network isolated cluster.


AKS clusters fetch artifacts required for the cluster and its features or add-ons from the Microsoft Artifact Registry (MAR). This image pull allows AKS to provide newer versions of the cluster components and to also address critical security vulnerabilities. A network isolated cluster attempts to pull those images and binaries from a private Azure Container Registry (ACR) instance connected to the cluster instead of pulling from MAR. If the images aren't present, the private ACR pulls them from MAR and serves them via its private endpoint, eliminating the need to enable egress from the cluster to the public MAR endpoint.

The following two options are supported for a private ACR associated with network isolated clusters:

**AKS-managed ACR**- AKS creates, manages, and reconciles an ACR resource in this option. There's nothing you need to do.Note

The AKS-managed ACR resource is created in your subscription. If you delete the cluster with AKS-managed ACR for bootstrap artifact source. Related resources such as the AKS-managed ACR, private link, and private endpoint are also automatically deleted. If you change outbound type on a cluster to any type other than

`none`

or`block`

with`--bootstrap-artifact-source`

retained as`Cache`

. Then the related resources are not deleted.**Bring your own (BYO) ACR**- The BYO ACR option requires creating an ACR with a private link between the ACR resource and the AKS cluster. See[Connect privately to an Azure container registry using Azure Private Link](/en-us/azure/container-registry/container-registry-private-link)to understand how to configure a private endpoint for your registry. You also need to assign permissions and manage the cache rules, private link, and private endpoint used in the cluster.Note

When you delete the AKS cluster or after you disable the feature. The BYO ACR, private link, and private endpoint aren't deleted automatically. If you add customized images and cache rules to the BYO ACR, they persist after cluster reconciliation.


To create a network isolated cluster, you need to first ensure network traffic between your API server and your node pools remains only on the private network, you can choose one of the following private cluster modes:

[Private link-based cluster](private-clusters)- The control plane or API server is in an AKS-managed Azure resource group, and your node pool is in your resource group. The server and the node pool can communicate with each other through the Azure Private Link service in the API server virtual network and a private endpoint which is exposed on the subnet of your AKS cluster.[API Server VNet Integration configured cluster](api-server-vnet-integration)- A cluster configured with API Server VNet Integration projects the API server endpoint directly into a delegated subnet in the virtual network where AKS is deployed. API Server VNet Integration enables network communication between the API server and the cluster nodes without requiring a private link or tunnel.

You also need to ensure the egress path for your AKS cluster are controlled and limited, you can choose one of the following network outbound types:

[Outbound type of](/en-us/azure/aks/egress-outboundtype#outbound-type-of-none)- If`none`

`none`

is set. AKS doesn't automatically configure egress paths and a default route is not required. It is supported in both bring-your-own (BYO) virtual network scenarios and managed virtual network scenarios. For bring your own virtual network scenario, you must establish explicit egress paths if needed.[Outbound type of](/en-us/azure/aks/egress-outboundtype#outbound-type-of-block-preview)-If`block`

(preview)`block`

is set. AKS configures network rules to actively block all egress traffic from the cluster. This option is useful for highly secure environments where outbound connectivity must be restricted. It is supported in managed virtual network scenario. You can also achieve similar effect by blocking all egress traffic by adding[network security group (NSG)](/en-us/azure/virtual-network/network-security-groups-overview)rules with`none`

in bring-your-own virtual network scenario.

Note

Outbound type of `none`

is generally available.
Outbound type `block`

is in preview.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Limitations

`Unmanaged`

channel is not supported.- Windows node pools are not yet supported.
- kubenet networking is not supported.
- BYO ACR
[Domain Name Label (DNL)](/en-us/azure/container-registry/container-registry-get-started-portal?tabs=azure-cli#configure-domain-name-label-dnl-option)is not supported.

Caution

If you are using [Node Public IP](use-node-public-ips) in network isolated AKS clusters, it will allow outbound traffic with outbound type `none`

.

## Using features, add-ons, and extensions requiring egress

For network isolated clusters with BYO ACR:

- If you want to use any AKS feature or add-on that requires outbound network access in network isolated clusters with outbound type
`none`

,[this document](outbound-rules-control-egress)contains the outbound network requirements for each feature. Also, this doc enumerates the features or add-ons that support private link integration for secure connection from within the cluster's virtual network. It is recommended to set up private endpoints to access these features. For example, you can set up[private endpoint based ingestion](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-private-link)to use Managed Prometheus (Azure Monitor workspace) and Container insights (Log Analytics workspace) in network isolated clusters. If a private link integration is not available for any of these features. Then you can set up the cluster with a[user-defined routing table and an Azure Firewall](limit-egress-traffic)based on the network rules and application rules that required for that feature. - If you are using
[Azure Container Storage Interface (CSI) driver](azure-files-csi)for Azure Files and Blob storage, you must create a custom storage class with "networkEndpointType: privateEndpoint", see examples in[Azure Files storage classes](/en-us/azure/aks/azure-csi-files-storage-provision#dynamically-provision-a-volume)and[Azure Blob storage classes](/en-us/azure/aks/azure-csi-blob-storage-provision?tabs=mount-nfs%2Csecret#storage-class-parameters-for-dynamic-persistent-volumes). - The following AKS cluster extensions aren't supported yet on network isolated clusters:

## Frequently asked questions

### What's the difference between network isolated cluster and Azure Firewall?

A network isolated cluster doesn't require any egress traffic beyond the VNet throughout the cluster bootstrapping process. A network isolated cluster has outbound type as either `none`

or `block`

. If the outbound type is set to `none`

, then AKS doesn't set up any outbound connections for the cluster, allowing the user to configure them on their own. If the outbound type is set to `block`

, then all outbound connections are blocked.

A firewall typically establishes a barrier between a trusted network and an untrusted network, such as the Internet. Azure Firewall, for example, can restrict outbound HTTP and HTTPS traffic that's based on the destination. It gives you fine-grained control of egress traffic, but at the same time allows you to provide access to the FQDNs encompassing an AKS cluster’s outbound dependencies. This is something that NSGs can't do. For example, you can set outbound type of the cluster to `userDefinedRouting`

to force outbound traffic through the firewall and then configure FQDN restrictions on outbound traffic. There are many cases where you still want a firewall. Such as you have outbound traffic anyway from your application or you want to control, inspect, and secure the cluster traffic both egress and ingress.

In summary, while Azure Firewall can be used to define egress restrictions on clusters with outbound requests, network isolated clusters go further on secure-by-default posture by eliminating or blocking the outbound requests altogether.

### Do I need to set up any allowlist endpoints for the network isolated cluster to work?

The cluster creation and bootstrapping stages don't require any outbound traffic from the network isolated cluster. Images required for AKS components and addons are pulled from the private ACR connected to the cluster instead of pulling from Microsoft Artifact Registry (MAR) over public endpoints.

After setting up a network isolated cluster. If you want to enable features or add-ons that need to make outbound requests to their service endpoints, you can set up private endpoints to the services powered by Azure Private Link.

### Can I manually upgrade packages to upgrade node pool image?

Manually upgrading packages based on egress to package repositories is not recommended. Instead, you can [manually upgrade](node-image-upgrade) or [autoupgrade your node OS images](auto-upgrade-node-os-image). Only `NodeImage`

and `None`

upgrade channels are currently supported for network isolated clusters.

### What if I change the outbound type other than `none`

or `block`

, does that still make a network isolated cluster?

The only supported outbound types for a network isolated cluster are outbound type `none`

and `block`

. If you use any other outbound type, the cluster may still pull artifacts from the private ACR associated, however that may generate egress traffic.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-deploy-ingress -->

# Deploy ingress gateways for Istio service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to deploy external or internal ingresses for the Istio service mesh add-on for Azure Kubernetes Service (AKS) cluster.

Note

When you perform a [minor revision upgrade](istio-upgrade#minor-revision-upgrades-with-ingress-and-egress-gateways) of the Istio add-on, another deployment for the external / internal gateways will be created for the new control plane revision.

## Prerequisites

This guide assumes you followed the [documentation](istio-deploy-addon) to enable the Istio add-on on an AKS cluster, deploy a sample application, and set environment variables.

## Enable external ingress gateway

Note

If you need the ingress gateway pods scheduled onto particular nodes, you can use [AKS system nodes](/en-us/azure/aks/use-system-pools) or the `azureservicemesh/istio.replica.preferred`

node label. The pods have node affinities with a weighted preference of `100`

for AKS system nodes (labeled `kubernetes.azure.com/mode: system`

), and a weighted preference of `50`

for nodes labeled `azureservicemesh/istio.replica.preferred: true`

.

Use `az aks mesh enable-ingress-gateway`

to enable an externally accessible Istio ingress on your AKS cluster:

```
az aks mesh enable-ingress-gateway --resource-group $RESOURCE_GROUP --name $CLUSTER --ingress-gateway-type external
```


Use `kubectl get svc`

to check the service mapped to the ingress gateway:

```
kubectl get svc aks-istio-ingressgateway-external -n aks-istio-ingress
```


Observe from the output that the external IP address of the service is a publicly accessible one:

```
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE
aks-istio-ingressgateway-external LoadBalancer 10.0.10.249 <EXTERNAL_IP> 15021:30705/TCP,80:32444/TCP,443:31728/TCP 4m21s
```


Applications aren't accessible from outside the cluster by default after enabling the ingress gateway. To make an application accessible, map the sample deployment's ingress to the Istio ingress gateway using the following manifest:

```
kubectl apply -f - <<EOF
apiVersion: networking.istio.io/v1beta1
kind: Gateway
metadata:
name: bookinfo-gateway-external
spec:
selector:
istio: aks-istio-ingressgateway-external
servers:
- port:
number: 80
name: http
protocol: HTTP
hosts:
- "*"
---
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
name: bookinfo-vs-external
spec:
hosts:
- "*"
gateways:
- bookinfo-gateway-external
http:
- match:
- uri:
exact: /productpage
- uri:
prefix: /static
- uri:
exact: /login
- uri:
exact: /logout
- uri:
prefix: /api/v1/products
route:
- destination:
host: productpage
port:
number: 9080
EOF
```


Note

The selector used in the Gateway object points to `istio: aks-istio-ingressgateway-external`

, which can be found as label on the service mapped to the external ingress that was enabled earlier.

Set environment variables for external ingress host and ports:

```
export INGRESS_HOST_EXTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-external -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
export INGRESS_PORT_EXTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-external -o jsonpath='{.spec.ports[?(@.name=="http2")].port}')
export GATEWAY_URL_EXTERNAL=$INGRESS_HOST_EXTERNAL:$INGRESS_PORT_EXTERNAL
```


Retrieve the external address of the sample application:

```
echo "http://$GATEWAY_URL_EXTERNAL/productpage"
```


Navigate to the URL from the output of the previous command and confirm that the sample application's product page is displayed. Alternatively, you can also use `curl`

to confirm the sample application is accessible. For example:

```
curl -s "http://${GATEWAY_URL_EXTERNAL}/productpage" | grep -o "<title>.*</title>"
```


Confirm that the sample application's product page is accessible. The expected output is:

```
<title>Simple Bookstore App</title>
```


## Enable internal ingress gateway

Use `az aks mesh enable-ingress-gateway`

to enable an internal Istio ingress on your AKS cluster:

```
az aks mesh enable-ingress-gateway --resource-group $RESOURCE_GROUP --name $CLUSTER --ingress-gateway-type internal
```


Use `kubectl get svc`

to check the service mapped to the ingress gateway:

```
kubectl get svc aks-istio-ingressgateway-internal -n aks-istio-ingress
```


Observe from the output that the external IP address of the service isn't a publicly accessible one and is instead only locally accessible:

```
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE
aks-istio-ingressgateway-internal LoadBalancer 10.0.182.240 <IP> 15021:30764/TCP,80:32186/TCP,443:31713/TCP 87s
```


After enabling the ingress gateway, applications need to be exposed through the gateway, and routing rules need to be configured accordingly. Use the following manifest to map the sample deployment's ingress to the Istio ingress gateway:

```
kubectl apply -f - <<EOF
apiVersion: networking.istio.io/v1beta1
kind: Gateway
metadata:
name: bookinfo-internal-gateway
spec:
selector:
istio: aks-istio-ingressgateway-internal
servers:
- port:
number: 80
name: http
protocol: HTTP
hosts:
- "*"
---
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
name: bookinfo-vs-internal
spec:
hosts:
- "*"
gateways:
- bookinfo-internal-gateway
http:
- match:
- uri:
exact: /productpage
- uri:
prefix: /static
- uri:
exact: /login
- uri:
exact: /logout
- uri:
prefix: /api/v1/products
route:
- destination:
host: productpage
port:
number: 9080
EOF
```


Note

The selector used in the Gateway object points to `istio: aks-istio-ingressgateway-internal`

, which can be found as label on the service mapped to the internal ingress that was enabled earlier.

Set environment variables for internal ingress host and ports:

```
export INGRESS_HOST_INTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-internal -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
export INGRESS_PORT_INTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-internal -o jsonpath='{.spec.ports[?(@.name=="http2")].port}')
export GATEWAY_URL_INTERNAL=$INGRESS_HOST_INTERNAL:$INGRESS_PORT_INTERNAL
```


Retrieve the address of the sample application:

```
echo "http://$GATEWAY_URL_INTERNAL/productpage"
```


Navigate to the URL from the output of the previous command and confirm that the sample application's product page is **NOT** displayed. Alternatively, you can also use `curl`

to confirm the sample application is **NOT** accessible. For example:

```
curl -s "http://${GATEWAY_URL_INTERNAL}/productpage" | grep -o "<title>.*</title>"
```


Use `kubectl exec`

to confirm application is accessible from inside the cluster's virtual network:

```
kubectl exec "$(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}')" -c ratings -- curl -sS "http://$GATEWAY_URL_INTERNAL/productpage" | grep -o "<title>.*</title>"
```


Confirm that the sample application's product page is accessible. The expected output is:

```
<title>Simple Bookstore App</title>
```


## Ingress gateway service customizations

### Annotations

The following annotations can be added to the Kubernetes service for the external and internal ingress gateways. See the [document on configuring public load balancers](configure-load-balancer-standard#customizations-via-kubernetes-annotations) for more information about these annotations.

`external-dns.alpha.kubernetes.io/hostname`

: for specifying the domain for resource's DNS records. For more information, see[external-dns](https://kubernetes-sigs.github.io/external-dns/latest/docs/annotations/annotations/#external-dnsalphakubernetesiohostname).`service.beta.kubernetes.io/azure-allowed-ip-ranges`

: for specifying a list of allowed IP ranges separated by commas.`service.beta.kubernetes.io/azure-allowed-service-tags`

: for specifying which[service tags](/en-us/azure/virtual-network/service-tags-overview)the ingress gateway can receive requests from.`service.beta.kubernetes.io/azure-disable-load-balancer-floating-ip`

: set to`true`

to disable floating IP address in load balancer rule.`service.beta.kubernetes.io/azure-load-balancer-internal-subnet`

: name of subnet to bind internal ingress gateway to. This subnet must exist in the same virtual network as the mesh.`service.beta.kubernetes.io/azure-load-balancer-ipv4`

: for configuring a static IPv4 address.`service.beta.kubernetes.io/azure-load-balancer-disable-tcp-reset`

: for controlling whether Azure Load Balancer enables TCP Reset.`service.beta.kubernetes.io/azure-load-balancer-resource-group`

: for specifying the resource group of a public IP in a different resource group from the cluster.`service.beta.kubernetes.io/azure-load-balancer-tcp-idle-timeout`

: for configuring the TCP idle timeout in minutes for connections through the Azure Load Balancer.`service.beta.kubernetes.io/azure-pip-ip-tags`

: for specifying a list of IpTags separated by commas.`service.beta.kubernetes.io/azure-pip-name`

: for specifying the name of a public IP address.`service.beta.kubernetes.io/azure-shared-securityrule`

: for exposing the ingress gateway through an[augmented security rule](/en-us/azure/virtual-network/network-security-groups-overview#augmented-security-rules).

The add-on supports the following health probe annotations for ports `80`

and `443`

:

`service.beta.kubernetes.io/port_{port}_no_lb_rule`

`service.beta.kubernetes.io/port_{port}_no_probe_rule`

`service.beta.kubernetes.io/port_{port}_health-probe_protocol`

`service.beta.kubernetes.io/port_{port}_health-probe_port`

`service.beta.kubernetes.io/port_{port}_health-probe_interval`

`service.beta.kubernetes.io/port_{port}_health-probe_num-of-probe`

`service.beta.kubernetes.io/port_{port}_health-probe_request-path`


### External traffic policy

The add-on supports customization of `.spec.externalTrafficPolicy`

in the Kubernetes service for the ingress gateway. Setting `.spec.externalTrafficPolicy`

to `Local`

preserves the client source IP at the Istio ingress gateway and avoids a second hop in the traffic path to the backend ingress gateway pods.

```
kubectl patch service aks-istio-ingressgateway-external -n aks-istio-ingress --type merge --patch '{"spec": {"externalTrafficPolicy": "Local"}}'
```


Note

Modifying the `.spec.externalTrafficPolicy`

to `Local`

risks potentially imbalanced traffic spreading. Before applying this change, it is recommended to read the [Kubernetes docs](https://kubernetes.io/docs/tasks/access-application-cluster/create-external-load-balancer/#preserving-the-client-source-ip) to understand the tradeoffs between the different `externalTrafficPolicy`

settings.

## Delete resources

If you want to clean up the Istio external or internal ingress gateways, but leave the mesh enabled on the cluster, run the following command:

```
az aks mesh disable-ingress-gateway --ingress-gateway-type <external/internal> --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


If you want to clean up the Istio service mesh and the ingresses (leaving behind the cluster), run the following command:

```
az aks mesh disable --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


If you want to clean up all the resources created from the Istio how-to guidance documents, run the following command:

```
az group delete --name ${RESOURCE_GROUP} --yes --no-wait
```


## Next steps

Note

If there are any issues encountered with deploying the Istio ingress gateway or configuring ingress traffic routing, refer to [article on troubleshooting Istio add-on ingress gateways](/en-us/troubleshoot/azure/azure-kubernetes/extensions/istio-add-on-ingress-gateway)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deploy-marketplace -->

# Deploy and manage a Kubernetes application from Azure Marketplace

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to deploy and manage a Kubernetes application from Azure Marketplace.

[Azure Marketplace](/en-us/marketplace/azure-marketplace-overview) is an online store that contains thousands of IT software applications and services built by industry-leading technology companies. In Azure Marketplace, you can find, try, buy, and deploy the software and services that you need to build new solutions and manage your cloud infrastructure. The catalog includes solutions for different industries and technical areas, free trials, and consulting services from Microsoft partners.

## Limitations

- This feature is currently supported only in the following regions:
- Australia East, Australia Southeast, Brazil South, Canada Central, Canada East, Central India, Central US, East Asia, East US, East US 2, East US 2 EAUP, France Central, France South, Germany North, Germany West Central, Japan East, Japan West, Jio India West, Korea Central, Korea South, North Central Us, North Europe, Norway East, Norway West, South Africa North, South Central US, South India, Southeast Asia, Sweden Central, Switzerland North, UAE North, UK South, UK West, West Central US, West Europe, West US, West US 2, West US 3

- You can't deploy Kubernetes application-based container offers on AKS for Azure Stack HCI or AKS Edge Essentials.

## Select and deploy a Kubernetes application

### From an AKS cluster

In the Azure portal, navigate to your AKS cluster resource.

From the service menu, under

**Settings**, select**Extensions + applications**>**Add**.You can search for an offer or publisher directly by name, or you can browse all offers. To view Kubernetes application offers, select

**Containers**under**Categories**.After you decide on an application, select the offer. The following example uses the

**TrilioVault for Kubernetes - BYOL**offer.Select

**Plans + Pricing**to ensure the terms are acceptable, and then select**Create**.Follow each page in the application creation process, filling in information for your resource group, your cluster, and any configuration options that the application requires. You can decide to deploy on a new AKS cluster or use an existing cluster.

Once you've filled in all the required information, select

**Review + create**>**Create**.It might take a few minutes for the application to deploy. You can monitor the deployment status from the

**Extensions + applications**page.

### Search in the Azure portal

From the Azure portal home page, search for and select

**Marketplace**.You can search for an offer or publisher directly by name, or you can browse all offers. To find Kubernetes application offers, on the left side under

**Categories**select**Containers**.After you decide on an application, select the offer. The following example uses the

**TrilioVault for Kubernetes - BYOL**offer.Select

**Plans + Pricing**to ensure the terms are acceptable, and then select**Create**.Follow each page in the application creation process, filling in information for your resource group, your cluster, and any configuration options that the application requires. You can decide to deploy on a new AKS cluster or use an existing cluster.

Once you've filled in all the required information, select

**Review + create**>**Create**.It might take a few minutes for the application to deploy. You can monitor the deployment status from the

**Extensions + applications**page.

## Verify the deployment

- Navigate to the cluster where you recently installed the application.
- From the service menu, under
**Settings**, select**Extensions + applications**. - Verify that the extension is listed and the
*Provisioning State*shows**Succeeded**.

## Manage the offer lifecycle

For lifecycle management, a Kubernetes offer is represented as a cluster extension for AKS. For more information, see [Cluster extensions for AKS](cluster-extensions). Purchasing an offer from Azure Marketplace creates a new instance of the extension on your AKS cluster.

- In the Azure portal, navigate to the cluster where you recently installed the application.
- From the service menu, under
**Settings**, select**Extensions + applications**. - Select an extension name to navigate to a properties view where you're able to disable autoupgrades, check the provisioning state, delete the extension instance, or modify configuration settings as needed.

## Monitor billing and usage information

- In the Azure portal, navigate to your cluster's resource group.
- From the service menu, under
**Cost Management**, select**Cost analysis**. Under**Product**, you can see a cost breakdown for the plan that you selected.

## Remove an offer

You can delete a purchased plan for an Azure container offer by deleting the extension instance on the cluster.

- Navigate to the cluster where you recently installed the application.
- From the service menu, under
**Settings**, select**Extensions + applications**. - Select an application, then select
**Uninstall**.

## Troubleshooting

If you experience issues, see the [troubleshooting checklist for failed deployments of a Kubernetes offer](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-failed-kubernetes-deployment-offer).

## Next steps

- Learn more about
[exploring and analyzing costs](/en-us/azure/cost-management-billing/costs/quick-acm-cost-analysis). - Learn more about
[deploying a Kubernetes application programmatically using Azure CLI](/en-us/azure/aks/deploy-application-az-cli). - Learn more about
[deploying a Kubernetes application using an ARM template](/en-us/azure/aks/deploy-application-template).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/quickstart-event-grid -->

# Quickstart: Subscribe to Azure Kubernetes Service (AKS) events with Azure Event Grid

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Event Grid is a fully managed event routing service that provides uniform event consumption using a publish-subscribe model.

In this quickstart, you create an AKS cluster and subscribe to AKS events.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). [Azure CLI](/en-us/cli/azure/install-azure-cli)or[Azure PowerShell](/en-us/powershell/azure/install-az-ps)installed.

Note

AKS operations are independent of Azure Event Grid availability and aren't impacted during Event Grid [Service Outages](https://azure.status.microsoft/status).

## Create an AKS cluster

Create an AKS cluster using the [az aks create](/en-us/cli/azure/aks#az-aks-create) command. The following example creates a resource group *MyResourceGroup* and a cluster named *MyAKS* with one node in the *MyResourceGroup* resource group:

```
az group create --name MyResourceGroup --location eastus
az aks create --resource-group yResourceGroup --name MyAKS --location eastus --node-count 1 --generate-ssh-keys
```


## Subscribe to AKS events

Create a namespace and event hub using [az eventhubs namespace create](/en-us/cli/azure/eventhubs/namespace#az-eventhubs-namespace-create) and [az eventhubs eventhub create](/en-us/cli/azure/eventhubs/eventhub#az-eventhubs-eventhub-create). The following example creates a namespace *MyNamespace* and an event hub *MyEventGridHub* in *MyNamespace*, both in the *MyResourceGroup* resource group.

```
az eventhubs namespace create --location eastus --name MyNamespace --resource-group MyResourceGroup
az eventhubs eventhub create --name MyEventGridHub --namespace-name MyNamespace --resource-group MyResourceGroup
```


Note

The *name* of your namespace must be unique.

Subscribe to the AKS events using [az eventgrid event-subscription create](/en-us/cli/azure/eventgrid/event-subscription#az-eventgrid-event-subscription-create):

```
SOURCE_RESOURCE_ID=$(az aks show --resource-group MyResourceGroup --name MyAKS --query id --output tsv)
ENDPOINT=$(az eventhubs eventhub show --resource-group MyResourceGroup --name MyEventGridHub --namespace-name MyNamespace --query id --output tsv)
az eventgrid event-subscription create --name MyEventGridSubscription \
--source-resource-id $SOURCE_RESOURCE_ID \
--endpoint-type eventhub \
--endpoint $ENDPOINT
```


Verify your subscription to AKS events using `az eventgrid event-subscription list`

:

```
az eventgrid event-subscription list --source-resource-id $SOURCE_RESOURCE_ID
```


The following example output shows you're subscribed to events from the *MyAKS* cluster and those events are delivered to the *MyEventGridHub* event hub:

```
[
{
"deadLetterDestination": null,
"deadLetterWithResourceIdentity": null,
"deliveryWithResourceIdentity": null,
"destination": {
"deliveryAttributeMappings": null,
"endpointType": "EventHub",
"resourceId": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/MyResourceGroup/providers/Microsoft.EventHub/namespaces/MyNamespace/eventhubs/MyEventGridHub"
},
"eventDeliverySchema": "EventGridSchema",
"expirationTimeUtc": null,
"filter": {
"advancedFilters": null,
"enableAdvancedFilteringOnArrays": null,
"includedEventTypes": [
"Microsoft.ContainerService.NewKubernetesVersionAvailable","Microsoft.ContainerService.ClusterSupportEnded","Microsoft.ContainerService.ClusterSupportEnding","Microsoft.ContainerService.NodePoolRollingFailed","Microsoft.ContainerService.NodePoolRollingStarted","Microsoft.ContainerService.NodePoolRollingSucceeded"
],
"isSubjectCaseSensitive": null,
"subjectBeginsWith": "",
"subjectEndsWith": ""
},
"id": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/MyResourceGroup/providers/Microsoft.ContainerService/managedClusters/MyAKS/providers/Microsoft.EventGrid/eventSubscriptions/MyEventGridSubscription",
"labels": null,
"name": "MyEventGridSubscription",
"provisioningState": "Succeeded",
"resourceGroup": "MyResourceGroup",
"retryPolicy": {
"eventTimeToLiveInMinutes": 1440,
"maxDeliveryAttempts": 30
},
"systemData": null,
"topic": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/MyResourceGroup/providers/microsoft.containerservice/managedclusters/MyAKS",
"type": "Microsoft.EventGrid/eventSubscriptions"
}
]
```


When AKS events occur, you see those events appear in your event hub. For example, when the list of available Kubernetes versions for your clusters changes, you see a `Microsoft.ContainerService.NewKubernetesVersionAvailable`

event. There are also new events available now for upgrades and cluster within support. For more information on the events AKS emits, see [Azure Kubernetes Service (AKS) as an Event Grid source](/en-us/azure/event-grid/event-schema-aks).

## Delete the cluster and subscriptions

Use the [az group delete](/en-us/cli/azure/group#az-group-delete) command to remove the resource group, the AKS cluster, namespace, and event hub, and all related resources.

```
az group delete --name MyResourceGroup --yes --no-wait
```


Note

When you delete the cluster, the Microsoft Entra service principal used by the AKS cluster isn't removed. For steps on how to remove the service principal, see [AKS service principal considerations and deletion](kubernetes-service-principal#considerations-when-using-a-service-principal).

If you used a managed identity, the identity is managed by the platform and doesn't require removal.

## Next steps

In this quickstart, you deployed a Kubernetes cluster and then subscribed to AKS events in Azure Event Hubs.

To learn more about AKS, and walk through a complete code to deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/spot-node-pool -->

# Add an Azure Spot node pool to an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you add a secondary Spot node pool to an existing Azure Kubernetes Service (AKS) cluster.

A Spot node pool is a node pool backed by an [Azure Spot Virtual Machine scale set](/en-us/azure/virtual-machine-scale-sets/use-spot). With Spot VMs in your AKS cluster, you can take advantage of unutilized Azure capacity with significant cost savings. The amount of available unutilized capacity varies based on many factors, such as node size, region, and time of day.

When you deploy a Spot node pool, Azure allocates the Spot nodes if there's capacity available and deploys a Spot scale set that backs the Spot node pool in a single default domain. There's no SLA for the Spot nodes. There are no high availability guarantees. If Azure needs capacity back, the Azure infrastructure evicts the Spot nodes.

Spot nodes are great for workloads that can handle interruptions, early terminations, or evictions. For example, workloads such as batch processing jobs, development and testing environments, and large compute workloads might be good candidates to schedule on a Spot node pool.

## Before you begin

- This article assumes a basic understanding of Kubernetes and Azure Load Balancer concepts. For more information, see
[Kubernetes core concepts for Azure Kubernetes Service (AKS)](concepts-clusters-workloads). - If you don't have an Azure subscription, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - When you create a cluster to use a Spot node pool, the cluster must use Virtual Machine Scale Sets for node pools and the
*Standard*SKU load balancer. You must also add another node pool after you create your cluster, which is covered in this tutorial. - This article requires that you're running the Azure CLI version 2.14 or later. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Limitations

The following limitations apply when you create and manage AKS clusters with a Spot node pool:

- A Spot node pool can't be a default node pool, it can only be used as a secondary pool.
- You can't upgrade the control plane and node pools at the same time. You must upgrade them separately or remove the Spot node pool to upgrade the control plane and remaining node pools at the same time.
- A Spot node pool must use Virtual Machine Scale Sets.
- You can't change
`ScaleSetPriority`

or`SpotMaxPrice`

after creation. - When setting
`SpotMaxPrice`

, the value must be*-1*or a*positive value with up to five decimal places*. - A Spot node pool has the
`kubernetes.azure.com/scalesetpriority:spot`

label, the`kubernetes.azure.com/scalesetpriority=spot:NoSchedule`

taint, and the system pods have anti-affinity. - You must add a
[corresponding toleration](#verify-the-spot-node-pool)and affinity to schedule workloads on a Spot node pool.

## Add a Spot node pool to an AKS cluster

When adding a Spot node pool to an existing cluster, it must be a cluster with multiple node pools enabled. When you create an AKS cluster with multiple node pools enabled, you create a node pool with a `priority`

of `Regular`

by default. To add a Spot node pool, you must specify `Spot`

as the value for `priority`

. For more details on creating an AKS cluster with multiple node pools, see [use multiple node pools](create-node-pools).

- Create a node pool with a
`priority`

of`Spot`

using thecommand.`az aks nodepool add`


```
export SPOT_NODEPOOL="spotnodepool"
az aks nodepool add \
--resource-group $RESOURCE_GROUP \
--cluster-name $AKS_CLUSTER \
--name $SPOT_NODEPOOL \
--priority Spot \
--eviction-policy Delete \
--spot-max-price -1 \
--enable-cluster-autoscaler \
--min-count 1 \
--max-count 3 \
--no-wait
```


In the previous command, the `priority`

of `Spot`

makes the node pool a Spot node pool. The `eviction-policy`

parameter is set to `Delete`

, which is the default value. When you set the [eviction policy](/en-us/azure/virtual-machine-scale-sets/use-spot#eviction-policy) to `Delete`

, nodes in the underlying scale set of the node pool are deleted when they're evicted.

You can also set the eviction policy to `Deallocate`

, which means that the nodes in the underlying scale set are set to the *stopped-deallocated* state upon eviction. Nodes in the *stopped-deallocated* state count against your compute quota and can cause issues with cluster scaling or upgrading. The `priority`

and `eviction-policy`

values can only be set during node pool creation. Those values can't be updated later.

The previous command also enables the [cluster autoscaler](cluster-autoscaler), which we recommend using with Spot node pools. Based on the workloads running in your cluster, the cluster autoscaler scales the number of nodes up and down. For Spot node pools, the cluster autoscaler will scale up the number of nodes after an eviction if more nodes are still needed. If you change the maximum number of nodes a node pool can have, you also need to adjust the `maxCount`

value associated with the cluster autoscaler. If you don't use a cluster autoscaler, upon eviction, the Spot pool will eventually decrease to *0* and require manual operation to receive any additional Spot nodes.

Important

Only schedule workloads on Spot node pools that can handle interruptions, such as batch processing jobs and testing environments. We recommend you set up [taints and tolerations](operator-best-practices-advanced-scheduler#provide-dedicated-nodes-using-taints-and-tolerations) on your Spot node pool to ensure that only workloads that can handle node evictions are scheduled on a Spot node pool. For example, the above command adds a taint of `kubernetes.azure.com/scalesetpriority=spot:NoSchedule`

, so only pods with a corresponding toleration are scheduled on this node.

## Verify the Spot node pool

- Verify your node pool was added using the
command and confirming the`az aks nodepool show`

`scaleSetPriority`

is`Spot`

.

```
az aks nodepool show --resource-group $RESOURCE_GROUP --cluster-name $AKS_CLUSTER --name $SPOT_NODEPOOL
```


Results:

```
{
"artifactStreamingProfile": null,
"availabilityZones": null,
"capacityReservationGroupId": null,
"count": 3,
"creationData": null,
"currentOrchestratorVersion": "1.30.10",
"eTag": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"enableAutoScaling": true,
"enableCustomCaTrust": false,
"enableEncryptionAtHost": false,
"enableFips": false,
"enableNodePublicIp": false,
"enableUltraSsd": false,
"gatewayProfile": null,
"gpuInstanceProfile": null,
"gpuProfile": null,
"hostGroupId": null,
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/xxxxxxxxxxxxxxxx/providers/Microsoft.ContainerService/managedClusters/xxxxxxxxxxxxxxxx/agentPools/xxxxxxxxxxxx",
"kubeletConfig": null,
"kubeletDiskType": "OS",
"linuxOsConfig": null,
"maxCount": 3,
"maxPods": 30,
"messageOfTheDay": null,
"minCount": 1,
"mode": "User",
"name": "xxxxxxxxxxxx",
"networkProfile": {
"allowedHostPorts": null,
"applicationSecurityGroups": null,
"nodePublicIpTags": null
},
"nodeImageVersion": "AKSUbuntu-2204gen2containerd-xxxxxxxx.xx.x",
"nodeInitializationTaints": null,
"nodeLabels": {
"kubernetes.azure.com/scalesetpriority": "spot"
},
"nodePublicIpPrefixId": null,
"nodeTaints": [
"kubernetes.azure.com/scalesetpriority=spot:NoSchedule"
],
"orchestratorVersion": "x.xx.xx",
"osDiskSizeGb": 128,
"osDiskType": "Managed",
"osSku": "Ubuntu",
"osType": "Linux",
"podIpAllocationMode": null,
"podSubnetId": null,
"powerState": {
"code": "Running"
},
"provisioningState": "Creating",
"proximityPlacementGroupId": null,
"resourceGroup": "xxxxxxxxxxxxxxxx",
"scaleDownMode": "Delete",
"scaleSetEvictionPolicy": "Delete",
"scaleSetPriority": "Spot",
"securityProfile": {
"enableSecureBoot": false,
"enableVtpm": false,
"sshAccess": "LocalUser"
},
"spotMaxPrice": -1.0,
"status": null,
"tags": null,
"type": "Microsoft.ContainerService/managedClusters/agentPools",
"typePropertiesType": "VirtualMachineScaleSets",
"upgradeSettings": {
"drainTimeoutInMinutes": null,
"maxSurge": null,
"maxUnavailable": null,
"nodeSoakDurationInMinutes": null,
"undrainableNodeBehavior": null
},
"virtualMachineNodesStatus": null,
"virtualMachinesProfile": null,
"vmSize": "Standard_DS2_v2",
"vnetSubnetId": null,
"windowsProfile": null,
"workloadRuntime": "OCIContainer"
}
```


## Schedule a pod to run on the Spot node

To schedule a pod to run on a Spot node, you can add a toleration and node affinity that corresponds to the taint applied to your Spot node.

The following example shows a portion of a YAML file that defines a toleration corresponding to the `kubernetes.azure.com/scalesetpriority=spot:NoSchedule`

taint and a node affinity corresponding to the `kubernetes.azure.com/scalesetpriority=spot`

label used in the previous step with `requiredDuringSchedulingIgnoredDuringExecution`

and `preferredDuringSchedulingIgnoredDuringExecution`

node affinity rules:

```
spec:
containers:
- name: spot-example
tolerations:
- key: "kubernetes.azure.com/scalesetpriority"
operator: "Equal"
value: "spot"
effect: "NoSchedule"
affinity:
nodeAffinity:
requiredDuringSchedulingIgnoredDuringExecution:
nodeSelectorTerms:
- matchExpressions:
- key: "kubernetes.azure.com/scalesetpriority"
operator: In
values:
- "spot"
preferredDuringSchedulingIgnoredDuringExecution:
- weight: 1
preference:
matchExpressions:
- key: another-node-label-key
operator: In
values:
- another-node-label-value
```


When you deploy a pod with this toleration and node affinity, Kubernetes successfully schedules the pod on the nodes with the taint and label applied. In this example, the following rules apply:

- The node
*must*have a label with the key`kubernetes.azure.com/scalesetpriority`

, and the value of that label*must*be`spot`

. - The node
*preferably*has a label with the key`another-node-label-key`

, and the value of that label*must*be`another-node-label-value`

.

For more information, see [Assigning pods to nodes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity).

## Upgrade a Spot node pool

When you upgrade a Spot node pool, AKS internally issues a cordon and an eviction notice, but no drain is applied. There are no surge nodes available for Spot node pool upgrades. Outside of these changes, the behavior when upgrading Spot node pools is consistent with that of other node pool types.

For more information on upgrading, see [Upgrade an AKS cluster](upgrade-cluster).

## Max price for a Spot pool

[Pricing for Spot instances is variable](/en-us/azure/virtual-machine-scale-sets/use-spot#pricing), based on region and SKU. For more information, see pricing information for [Linux](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/linux/) and [Windows](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/windows/).

With variable pricing, you have the option to set a max price, in US dollars (USD) using up to five decimal places. For example, the value *0.98765* would be a max price of *$0.98765 USD per hour*. If you set the max price to *-1*, the instance won't be evicted based on price. As long as there's capacity and quota available, the price for the instance will be the lower price of either the current price for a Spot instance or for a standard instance.

## Next steps

In this article, you learned how to add a Spot node pool to an AKS cluster. For more information about how to control pods across node pools, see [Best practices for advanced scheduler features in AKS](operator-best-practices-advanced-scheduler).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-identity -->

# Access and identity options for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can authenticate, authorize, secure, and control access to Kubernetes clusters in a variety of ways:

- Using Kubernetes role-based access control (Kubernetes RBAC), you can grant users, groups, and service accounts access to only the resources they need.
- With Azure Kubernetes Service (AKS), you can further enhance the security and permissions structure using Microsoft Entra ID and Azure RBAC.

Kubernetes RBAC and AKS help you secure your cluster access and provide only the minimum required permissions to developers and operators.

This article introduces the core concepts that help you authenticate and assign permissions in AKS.

## Kubernetes RBAC

Kubernetes RBAC provides granular filtering of user actions. With this control mechanism:

- You assign users or user groups permission to create and modify resources or view logs from running application workloads.
- You can scope permissions to a single namespace or across the entire AKS cluster.
- You create
*roles*to define permissions, and then assign those roles to users with*role bindings*.

For more information, see [Using Kubernetes RBAC authorization](https://kubernetes.io/docs/reference/access-authn-authz/rbac/).

### Roles and ClusterRoles

#### Roles

Before assigning permissions to users with Kubernetes RBAC, you'll define user permissions as a *Role*. Grant permissions within a namespace using roles.

Note

Kubernetes roles *grant* permissions; they don't *deny* permissions.

To grant permissions across the entire cluster or to cluster resources outside a given namespace, you can instead use *ClusterRoles*.

#### ClusterRoles

A ClusterRole grants and applies permissions to resources across the entire cluster, not a specific namespace.

### RoleBindings and ClusterRoleBindings

Once you've defined roles to grant permissions to resources, you assign those Kubernetes RBAC permissions with a *RoleBinding*. If your AKS cluster [integrates with Microsoft Entra ID](#azure-ad-integration), RoleBindings grant permissions to Microsoft Entra users to perform actions within the cluster. See how in [Control access to cluster resources using Kubernetes role-based access control and Microsoft Entra identities](azure-ad-rbac).

#### RoleBindings

Assign roles to users for a given namespace using RoleBindings. With RoleBindings, you can logically segregate a single AKS cluster, only enabling users to access the application resources in their assigned namespace.

To bind roles across the entire cluster, or to cluster resources outside a given namespace, you instead use *ClusterRoleBindings*.

#### ClusterRoleBinding

With a ClusterRoleBinding, you bind roles to users and apply to resources across the entire cluster, not a specific namespace. This approach lets you grant administrators or support engineers access to all resources in the AKS cluster.

Note

Microsoft/AKS performs any cluster actions with user consent under a built-in Kubernetes role `aks-service`

and built-in role binding `aks-service-rolebinding`

.

This role enables AKS to troubleshoot and diagnose cluster issues, but can't modify permissions nor create roles or role bindings, or other high privilege actions. Role access is only enabled under active support tickets with just-in-time (JIT) access. Read more about [AKS support policies](support-policies).

### Kubernetes service accounts

*Service accounts* are one of the primary user types in Kubernetes. The Kubernetes API holds and manages service accounts. Service account credentials are stored as Kubernetes secrets, allowing them to be used by authorized pods to communicate with the API Server. Most API requests provide an authentication token for a service account or a normal user account.

Normal user accounts allow more traditional access for human administrators or developers, not just services and processes. While Kubernetes doesn't provide an identity management solution to store regular user accounts and passwords, you can integrate external identity solutions into Kubernetes. For AKS clusters, this integrated identity solution is Microsoft Entra ID.

For more information on the identity options in Kubernetes, see [Kubernetes authentication](https://kubernetes.io/docs/reference/access-authn-authz/authentication).

## Azure role-based access control

Azure role-based access control (RBAC) is an authorization system built on [Azure Resource Manager](/en-us/azure/azure-resource-manager/management/overview) that provides fine-grained access management of Azure resources.

| RBAC system | Description |
|---|---|
| Kubernetes RBAC | Designed to work on Kubernetes resources within your AKS cluster. |
| Azure RBAC | Designed to work on resources within your Azure subscription. |

With Azure RBAC, you create a *role definition* that outlines the permissions to be applied. You then assign a user or group this role definition via a *role assignment* for a particular *scope*. The scope can be an individual resource, a resource group, or across the subscription.

For more information, see [What is Azure role-based access control (Azure RBAC)?](/en-us/azure/role-based-access-control/overview)

There are two levels of access needed to fully operate an AKS cluster:

[Access the AKS resource in your Azure subscription](#azure-rbac-to-authorize-access-to-the-aks-resource).- Control scaling or upgrading your cluster using the AKS APIs.
- Pull your
`kubeconfig`

.

- Access to the Kubernetes API. This access is controlled by either:
[Kubernetes RBAC](#kubernetes-rbac)(traditionally).[Integrating Azure RBAC with AKS for Kubernetes authorization](#azure-rbac-for-kubernetes-authorization).


### Azure RBAC to authorize access to the AKS resource

With Azure RBAC, you can provide your users (or identities) with granular access to AKS resources across one or more subscriptions. For example, you could use the [Azure Kubernetes Service Contributor role](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-contributor-role) to scale and upgrade your cluster. Meanwhile, another user with the [Azure Kubernetes Service Cluster Admin role](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-cluster-admin-role) only has permission to pull the Admin `kubeconfig`

.

[Use Azure RBAC to define access to the Kubernetes configuration file in AKS](control-kubeconfig-access).

### Azure RBAC for Kubernetes Authorization

With the Azure RBAC integration, AKS will use a Kubernetes Authorization webhook server so you can manage Microsoft Entra integrated Kubernetes cluster resource permissions and assignments using Azure role definition and role assignments.

As shown in the above diagram, when using the Azure RBAC integration, all requests to the Kubernetes API will follow the same authentication flow as explained on the [Microsoft Entra integration section](#azure-ad-integration).

If the identity making the request exists in Microsoft Entra ID, Azure will team with Kubernetes RBAC to authorize the request. If the identity exists outside of Microsoft Entra ID (i.e., a Kubernetes service account), authorization will defer to the normal Kubernetes RBAC.

In this scenario, you use Azure RBAC mechanisms and APIs to assign users built-in roles or create custom roles, just as you would with Kubernetes roles.

With this feature, you not only give users permissions to the AKS resource across subscriptions, but you also configure the role and permissions for inside each of those clusters controlling Kubernetes API access. For example, you can grant the `Azure Kubernetes Service RBAC Reader`

role on the subscription scope. The role recipient will be able to list and get all Kubernetes objects from all clusters without modifying them.

Important

You need to enable Azure RBAC for Kubernetes authorization before using this feature. For more details and step by step guidance, follow our [Use Azure RBAC for Kubernetes Authorization](manage-azure-rbac) how-to guide.

#### Built-in roles

AKS provides the following four built-in roles. They are similar to the [Kubernetes built-in roles](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#user-facing-roles) with a few differences, like supporting CRDs. See the full list of actions allowed by each [Azure built-in role](/en-us/azure/role-based-access-control/built-in-roles).

| Role | Description |
|---|---|
| Azure Kubernetes Service RBAC Reader | Allows read-only access to see most objects in a namespace. Doesn't allow viewing roles or role bindings. Doesn't allow viewing `Secrets` . Reading the `Secrets` contents enables access to `ServiceAccount` credentials in the namespace, which would allow API access as any `ServiceAccount` in the namespace (a form of privilege escalation). |
| Azure Kubernetes Service RBAC Writer | Allows read/write access to most objects in a namespace. Doesn't allow viewing or modifying roles, or role bindings. Allows accessing `Secrets` and running pods as any ServiceAccount in the namespace, so it can be used to gain the API access levels of any ServiceAccount in the namespace. |
| Azure Kubernetes Service RBAC Admin | Allows admin access, intended to be granted within a namespace. Allows read/write access to most resources in a namespace (or cluster scope), including the ability to create roles and role bindings within the namespace. Doesn't allow write access to resource quota or to the namespace itself. |
| Azure Kubernetes Service RBAC Cluster Admin | Allows super-user access to perform any action on any resource. Gives full control over every resource in the cluster and in all namespaces. |

## Microsoft Entra integration

Enhance your AKS cluster security with Microsoft Entra integration. Built on decades of enterprise identity management, Microsoft Entra ID is a multi-tenant, cloud-based directory and identity management service that combines core directory services, application access management, and identity protection. With Microsoft Entra ID, you can integrate on-premises identities into AKS clusters to provide a single source for account management and security.

With Microsoft Entra integrated AKS clusters, you can grant users or groups access to Kubernetes resources within a namespace or across the cluster.

- To obtain a
`kubectl`

configuration context, a user runs the[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command. - When a user interacts with the AKS cluster with
`kubectl`

, they're prompted to sign in with their Microsoft Entra credentials.

This approach provides a single source for user account management and password credentials. The user can only access the resources as defined by the cluster administrator.

Microsoft Entra authentication is provided to AKS clusters with OpenID Connect. OpenID Connect is an identity layer built on top of the OAuth 2.0 protocol. For more information on OpenID Connect, see the [OpenID Connect documentation](/en-us/azure/active-directory/develop/v2-protocols-oidc). From inside of the Kubernetes cluster, [Webhook Token Authentication](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#webhook-token-authentication) is used to verify authentication tokens. Webhook token authentication is configured and managed as part of the AKS cluster.

### Webhook and API server

As shown in the graphic above, the API server calls the AKS webhook server and performs the following steps:

`kubectl`

uses the Microsoft Entra client application to sign in users with[OAuth 2.0 device authorization grant flow](/en-us/azure/active-directory/develop/v2-oauth2-device-code).- Microsoft Entra ID provides an access_token, id_token, and a refresh_token.
- The user makes a request to
`kubectl`

with an access_token from`kubeconfig`

. `kubectl`

sends the access_token to API Server.- The API Server is configured with the Auth WebHook Server to perform validation.
- The authentication webhook server confirms the JSON Web Token signature is valid by checking the Microsoft Entra public signing key.
- If the user is a member of more than 200 groups, the server application uses user-provided credentials to query group memberships of the logged-in user from the MS Graph API. For users with group memberships of 200 or fewer the groups claim already exists in the client token. No query will be performed.
- A response is sent to the API Server with user information such as the user principal name (UPN) claim of the access token, and the group membership of the user based on the object ID.
- The API performs an authorization decision based on the Kubernetes Role/RoleBinding.
- Once authorized, the API server returns a response to
`kubectl`

. `kubectl`

provides feedback to the user.

Learn how to integrate AKS with Microsoft Entra ID with our [AKS-managed Microsoft Entra integration how-to guide](managed-azure-ad).

## AKS service permissions

When creating a cluster, AKS generates or modifies resources it needs (like VMs and NICs) to create and run the cluster on behalf of the user. This identity is distinct from the cluster's identity permission, which is created during cluster creation.

### Identity creating and operating the cluster permissions

The following permissions are needed by the identity creating and operating the cluster.

| Permission | Reason |
|---|---|
`Microsoft.Compute/diskEncryptionSets/read` |
Required to read disk encryption set ID. |
`Microsoft.Compute/proximityPlacementGroups/write` |
Required for updating proximity placement groups. |
`Microsoft.Network/applicationGateways/read` `Microsoft.Network/applicationGateways/write` `Microsoft.Network/virtualNetworks/subnets/join/action` |
Required to configure application gateways and join the subnet. |
`Microsoft.Network/virtualNetworks/subnets/join/action` |
Required to configure the Network Security Group for the subnet when using a custom VNET. |
`Microsoft.Network/publicIPAddresses/join/action` `Microsoft.Network/publicIPPrefixes/join/action` |
Required to configure the outbound public IPs on the Standard Load Balancer. |
`Microsoft.OperationalInsights/workspaces/sharedkeys/read` `Microsoft.OperationalInsights/workspaces/read` `Microsoft.OperationsManagement/solutions/write` `Microsoft.OperationsManagement/solutions/read` `Microsoft.ManagedIdentity/userAssignedIdentities/assign/action` |
Required to create and update Log Analytics workspaces and Azure monitoring for containers. |
`Microsoft.Network/virtualNetworks/joinLoadBalancer/action` |
Required to configure the IP-based Load Balancer Backend Pools. |

### AKS cluster identity permissions

The following permissions are used by the AKS cluster identity, which is created and associated with the AKS cluster. Each permission is used for the reasons below:

| Permission | Reason |
|---|---|
`Microsoft.ContainerService/managedClusters/*` |
Required for creating users and operating the cluster |
`Microsoft.Network/loadBalancers/delete` `Microsoft.Network/loadBalancers/read` `Microsoft.Network/loadBalancers/write` |
Required to configure the load balancer for a LoadBalancer service. |
`Microsoft.Network/publicIPAddresses/delete` `Microsoft.Network/publicIPAddresses/read` `Microsoft.Network/publicIPAddresses/write` |
Required to find and configure public IPs for a LoadBalancer service. |
`Microsoft.Network/publicIPAddresses/join/action` |
Required for configuring public IPs for a LoadBalancer service. |
`Microsoft.Network/networkSecurityGroups/read` `Microsoft.Network/networkSecurityGroups/write` |
Required to create or delete security rules for a LoadBalancer service. |
`Microsoft.Compute/disks/delete` `Microsoft.Compute/disks/read` `Microsoft.Compute/disks/write` `Microsoft.Compute/locations/DiskOperations/read` |
Required to configure AzureDisks. |
`Microsoft.Storage/storageAccounts/delete` `Microsoft.Storage/storageAccounts/listKeys/action` `Microsoft.Storage/storageAccounts/read` `Microsoft.Storage/storageAccounts/write` `Microsoft.Storage/operations/read` |
Required to configure storage accounts for AzureFile or AzureDisk. |
`Microsoft.Network/routeTables/read` `Microsoft.Network/routeTables/routes/delete` `Microsoft.Network/routeTables/routes/read` `Microsoft.Network/routeTables/routes/write` `Microsoft.Network/routeTables/write` |
Required to configure route tables and routes for nodes. |
`Microsoft.Compute/virtualMachines/read` |
Required to find information for virtual machines in a VMAS, such as zones, fault domain, size, and data disks. |
`Microsoft.Compute/virtualMachines/write` |
Required to attach AzureDisks to a virtual machine in a VMAS. |
`Microsoft.Compute/virtualMachineScaleSets/read` `Microsoft.Compute/virtualMachineScaleSets/virtualMachines/read` `Microsoft.Compute/virtualMachineScaleSets/virtualmachines/instanceView/read` |
Required to find information for virtual machines in a virtual machine scale set, such as zones, fault domain, size, and data disks. |
`Microsoft.Network/networkInterfaces/write` |
Required to add a virtual machine in a VMAS to a load balancer backend address pool. |
`Microsoft.Compute/virtualMachineScaleSets/write` |
Required to add a virtual machine scale set to a load balancer backend address pools and scale out nodes in a virtual machine scale set. |
`Microsoft.Compute/virtualMachineScaleSets/delete` |
Required to delete a virtual machine scale set to a load balancer backend address pools and scale down nodes in a virtual machine scale set. |
`Microsoft.Compute/virtualMachineScaleSets/virtualmachines/write` |
Required to attach AzureDisks and add a virtual machine from a virtual machine scale set to the load balancer. |
`Microsoft.Network/networkInterfaces/read` |
Required to search internal IPs and load balancer backend address pools for virtual machines in a VMAS. |
`Microsoft.Compute/virtualMachineScaleSets/virtualMachines/networkInterfaces/read` |
Required to search internal IPs and load balancer backend address pools for a virtual machine in a virtual machine scale set. |
`Microsoft.Compute/virtualMachineScaleSets/virtualMachines/networkInterfaces/ipconfigurations/publicipaddresses/read` |
Required to find public IPs for a virtual machine in a virtual machine scale set. |
`Microsoft.Network/virtualNetworks/read` `Microsoft.Network/virtualNetworks/subnets/read` |
Required to verify if a subnet exists for the internal load balancer in another resource group. |
`Microsoft.Compute/snapshots/delete` `Microsoft.Compute/snapshots/read` `Microsoft.Compute/snapshots/write` |
Required to configure snapshots for AzureDisk. |
`Microsoft.Compute/locations/vmSizes/read` `Microsoft.Compute/locations/operations/read` |
Required to find virtual machine sizes for finding AzureDisk volume limits. |

### Additional cluster identity permissions

When creating a cluster with specific attributes, you will need the following additional permissions for the cluster identity. Since these permissions are not automatically assigned, you must add them to the cluster identity after it's created.

| Permission | Reason |
|---|---|
`Microsoft.Network/networkSecurityGroups/write` `Microsoft.Network/networkSecurityGroups/read` |
Required if using a network security group in another resource group. Required to configure security rules for a LoadBalancer service. |
`Microsoft.Network/virtualNetworks/subnets/read` `Microsoft.Network/virtualNetworks/subnets/join/action` |
Required if using a subnet in another resource group such as a custom VNET. |
`Microsoft.Network/routeTables/routes/read` `Microsoft.Network/routeTables/routes/write` |
Required if using a subnet associated with a route table in another resource group such as a custom VNET with a custom route table. Required to verify if a subnet already exists for the subnet in the other resource group. |
`Microsoft.Network/virtualNetworks/subnets/read` |
Required if using an internal load balancer in another resource group. Required to verify if a subnet already exists for the internal load balancer in the resource group. |
`Microsoft.Network/privatednszones/*` |
Required if using a private DNS zone in another resource group such as a custom privateDNSZone. |

## AKS Node Access

By default Node Access is not required for AKS. The following access is needed for the node if a specific component is leveraged.

| Access | Reason |
|---|---|
`kubelet` |
Required to grant MSI access to ACR. |
`http app routing` |
Required for write permission to "random name".aksapp.io. |
`container insights` |
Required to grant permission to the Log Analytics workspace. |

## Summary

View the table for a quick summary of how users can authenticate to Kubernetes when Microsoft Entra integration is enabled. In all cases, the user's sequence of commands is:

Run

`az login`

to authenticate to Azure.Run

`az aks get-credentials`

to download credentials for the cluster into`.kube/config`

.Run

`kubectl`

commands.- The first command may trigger browser-based authentication to authenticate to the cluster, as described in the following table.


In the Azure portal, you can find:

- The
*Role Grant*(Azure RBAC role grant) referred to in the second column is shown on the**Access Control**tab. - The Cluster Admin Microsoft Entra group is shown on the
**Configuration**tab.- Also found with parameter name
`--aad-admin-group-object-ids`

in the Azure CLI.

- Also found with parameter name

| Description | Role grant required | Cluster admin Microsoft Entra group(s) | When to use |
|---|---|---|---|
| Legacy admin login using client certificate | Azure Kubernetes Service Cluster Admin Role. This role allows `az aks get-credentials` to be used with the `--admin` flag, which downloads a
`.kube/config` . This is the only purpose of "Azure Kubernetes Service Cluster Admin Role". |
n/a | If you're permanently blocked by not having access to a valid Microsoft Entra group with access to your cluster. |
| Microsoft Entra ID with manual (Cluster)RoleBindings | Azure Kubernetes Service Cluster User Role. The "User" role allows `az aks get-credentials` to be used without the `--admin` flag. (This is the only purpose of "Azure Kubernetes Service Cluster User Role".) The result, on a Microsoft Entra ID-enabled cluster, is the download of
`.kube/config` , which triggers browser-based authentication when it's first used by `kubectl` . |
User is not in any of these groups. Because the user is not in any Cluster Admin groups, their rights will be controlled entirely by any RoleBindings or ClusterRoleBindings that have been set up by cluster admins. The (Cluster)RoleBindings
`subjects` . If no such bindings have been set up, the user will not be able to excute any `kubectl` commands. |

`cluster-admin`

Kubernetes role. So users in these groups can run all `kubectl`

commands as `cluster-admin`

.*not*using Azure RBAC for Kubernetes authorization.First,

**Azure Kubernetes Service Cluster User Role**(as above).Second, one of the "Azure Kubernetes Service

**RBAC**..." roles listed above, or your own custom alternative.## Next steps

- To get started with Microsoft Entra ID and Kubernetes RBAC, see
[Integrate Microsoft Entra ID with AKS](managed-azure-ad). - For associated best practices, see
[Best practices for authentication and authorization in AKS](operator-best-practices-identity). - To get started with Azure RBAC for Kubernetes Authorization, see
[Use Azure RBAC to authorize access within the Azure Kubernetes Service (AKS) Cluster](manage-azure-rbac). - To get started securing your
`kubeconfig`

file, see[Limit access to cluster configuration file](control-kubeconfig-access). - To get started with managed identities in AKS, see
[Use a managed identity in AKS](use-managed-identity).

For more information on core Kubernetes and AKS concepts, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-cni-overlay -->

# Configure Azure CNI Overlay networking in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains the setup process, dual-stack networking configuration, and an example workload deployment for Azure CNI Overlay in Azure Kubernetes Service (AKS) clusters. For an overview of Azure CNI Overlay networking, see [Overview of Azure CNI Overlay networking in Azure Kubernetes Service (AKS)](concepts-network-azure-cni-overlay).

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, create a
[free account](https://azure.microsoft.com/free/)before you begin. - Azure CLI version 2.48.0 or later. To install or upgrade the Azure CLI, see
[Install the Azure CLI](/en-us/cli/azure/install-azure-cli). - An existing Azure resource group. If you need to create one, see
[Create resource groups](/en-us/azure/azure-resource-manager/management/manage-resource-groups-cli#create-resource-groups).

For dual-stack networking, you need Kubernetes version 1.26.3 or later.

## Key parameters for Azure CNI Overlay AKS clusters

The following table describes the key parameters for configuring Azure CNI Overlay networking in AKS clusters:

| Parameter | Description |
|---|---|
`--network-plugin` |
Set to `azure` to use Azure Container Networking Interface (CNI) networking. |
`--network-plugin-mode` |
Set to `overlay` to enable Azure CNI Overlay networking. This setting applies only when `--network-plugin=azure` . |
`--pod-cidr` |
Specify a custom pod Classless Inter-Domain Routing (CIDR) block for the cluster. The default is `10.244.0.0/16` . |

The default behavior for network plugins depends on whether you explicitly set `--network-plugin`

:

- If you don't specify
`--network-plugin`

, AKS defaults to Azure CNI Overlay. - If you specify
`--network-plugin=azure`

and omit`--network-plugin-mode`

, AKS intentionally uses virtual network (node subnet) mode for backward compatibility.

## Create an Azure CNI Overlay AKS cluster

Create an Azure CNI Overlay AKS cluster by using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command with

`--network-plugin=azure`

and `--network-plugin-mode=overlay`

. If you don't specify a value for `--pod-cidr`

, AKS assigns the default value of `10.244.0.0/16`

.```
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--location $REGION \
--network-plugin azure \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16 \
--generate-ssh-keys
```


## Add a new node pool to a dedicated subnet

Add a node pool to a different subnet within the same virtual network to control virtual machine (VM) node IP addresses for network traffic to virtual network or peered virtual network resources.

Add a new node pool to the cluster by using the [ az aks nodepool add](/en-us/cli/azure/aks#az_aks_nodepool_add) command and specify the subnet resource ID with the

`--vnet-subnet-id`

parameter. For example:```
az aks nodepool add \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--name $NODE_POOL_NAME \
--node-count 1 \
--mode system \
--vnet-subnet-id $SUBNET_RESOURCE_ID
```


## About Azure CNI Overlay AKS clusters with dual-stack networking

You can deploy your Azure CNI Overlay AKS clusters in a dual-stack mode with an Azure virtual network. In this configuration, nodes receive both an IPv4 and IPv6 address from the Azure virtual network subnet. Pods receive an IPv4 and IPv6 address from a different address space to the Azure virtual network subnet of the nodes. Network address translation (NAT) is then configured so that the pods can reach resources on the Azure virtual network. The source IP address of the traffic is NAT'd to the node's primary IP address of the same family (*IPv4 to IPv4* and *IPv6 to IPv6*).

Note

You can also deploy dual-stack networking clusters by using Azure CNI Powered by Cilium. For more information, see [Dual-stack networking with Azure CNI Powered by Cilium](azure-cni-powered-by-cilium#dual-stack-networking-with-azure-cni-powered-by-cilium).

## Dual-stack networking limitations

The following features aren't supported with dual-stack networking:

## Key parameters for dual-stack networking

The following table describes the key parameters for configuring dual-stack networking in Azure CNI Overlay AKS clusters:

| Parameter | Description |
|---|---|
`--ip-families` |
Takes a comma-separated list of IP families to enable on the cluster. Only `ipv4` and `ipv4,ipv6` are supported. |
`--pod-cidrs` |
Takes a comma-separated list of Classless Inter-Domain Routing (CIDR) notation IP ranges to assign pod IPs from. The count and order of ranges in this list must match the value provided to `--ip-families` . If you don't supply any values, the parameter uses the default value of `10.244.0.0/16,fd12:3456:789a::/64` . |
`--service-cidrs` |
Takes a comma-separated list of CIDR notation IP ranges to assign service IPs from. The count and order of ranges in this list must match the value provided to `--ip-families` . If you don't supply any values, the parameter uses the default value of `10.0.0.0/16,fd12:3456:789a:1::/108` . The IPv6 subnet assigned to `--service-cidrs` can be no larger than `/108` . |

## Create an Azure CNI Overlay AKS cluster with dual-stack networking (Linux)

Create an Azure resource group for the cluster by using the

command:`az group create`

`az group create --location $REGION --name $RESOURCE_GROUP`

Create a dual-stack AKS cluster by using the

command with the`az aks create`

`--ip-families`

parameter set to`ipv4,ipv6`

:`az aks create \ --location $REGION \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --network-plugin azure \ --network-plugin-mode overlay \ --ip-families ipv4,ipv6 \ --generate-ssh-keys`


## Create an Azure CNI Overlay AKS cluster with dual-stack networking (Windows)

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Before you create an Azure CNI Overlay AKS cluster with dual-stack networking with Windows node pools, you need to install the `aks-preview`

Azure CLI extension and register the `AzureOverlayDualStackPreview`

feature flag in your subscription.

### Install the `aks-preview`

Azure CLI extension

Install the

`aks-preview`

extension by using thecommand:`az extension add`

`az extension add --name aks-preview`

Update to the latest version of the extension by using the

command:`az extension update`

`az extension update --name aks-preview`


### Register the `AzureOverlayDualStackPreview`

feature flag

Register the

`AzureOverlayDualStackPreview`

feature flag by using thecommand:`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AzureOverlayDualStackPreview"`

It takes a few minutes for the status to show

`Registered`

.Verify the registration status by using the

command:`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "AzureOverlayDualStackPreview"`

When the status reflects

`Registered`

, refresh the registration of the`Microsoft.ContainerService`

resource provider by using thecommand:`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Create a dual-stack Azure CNI Overlay AKS cluster and add a Windows node pool

Create a cluster with Azure CNI Overlay by using the

command:`az aks create`

`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --location $REGION \ --network-plugin azure \ --network-plugin-mode overlay \ --ip-families ipv4,ipv6 \ --generate-ssh-keys`

Add a Windows node pool to the cluster by using the

command:`az aks nodepool add`

`az aks nodepool add \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --os-type Windows \ --name $WINDOWS_NODE_POOL_NAME \ --node-count 2`


## Deploy an example workload to the Azure CNI Overlay AKS cluster

Deploy dual-stack AKS CNI Overlay clusters with IPv4/IPv6 addresses on virtual machine nodes. This example deploys an NGINX web server and exposes it by using a `LoadBalancer`

service with both IPv4 and IPv6 addresses.

Note

We recommend using the application routing add-on for ingress in AKS clusters. However, for demonstration purposes, this example deploys an NGINX web server without the application routing add-on. For more information about the add-on, see [Managed NGINX ingress with the application routing add-on](app-routing).

### Expose the workload by using a `LoadBalancer`

service

Expose the NGINX deployment by using either `kubectl`

commands or YAML manifests.

Important

There are currently *two limitations* that pertain to IPv6 services in AKS:

- Azure Load Balancer sends health probes to IPv6 destinations from a link-local address. In
*Azure Linux node pools*, you can't route this traffic to a pod, so traffic flowing to IPv6 services deployed with`externalTrafficPolicy: Cluster`

fails. - You must deploy IPv6 services with
`externalTrafficPolicy: Local`

, which causes`kube-proxy`

to respond to the probe on the node.

Expose the NGINX deployment by using the

`kubectl expose deployment nginx`

command:`kubectl expose deployment nginx --name=nginx-ipv4 --port=80 --type=LoadBalancer kubectl expose deployment nginx --name=nginx-ipv6 --port=80 --type=LoadBalancer --overrides='{"spec":{"ipFamilies": ["IPv6"]}}'`

Your output should show the exposed services. For example:

`service/nginx-ipv4 exposed service/nginx-ipv6 exposed`

After the deployment is exposed and the

`LoadBalancer`

services are fully provisioned, get the IP addresses of the services by using the`kubectl get services`

command:`kubectl get services`

Your output should show the services with their assigned IP addresses. For example:

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE nginx-ipv4 LoadBalancer 10.0.88.78 20.46.24.24 80:30652/TCP 97s nginx-ipv6 LoadBalancer fd12:3456:789a:1::981a 2603:1030:8:5::2d 80:32002/TCP 63s`

Get the service IP by using the

`kubectl get services`

command and set it to an environment variable:`SERVICE_IP=$(kubectl get services nginx-ipv6 -o jsonpath='{.status.loadBalancer.ingress[0].ip}')`

Verify functionality by using a

`curl`

request from an IPv6-capable host. (*Azure Cloud Shell isn't IPv6 capable*.)`curl -s "http://[${SERVICE_IP}]" | head -n5`

Your output should show the HTML for the NGINX welcome page. For example:

`<!DOCTYPE html> <html> <head> <title>Welcome to nginx!</title> <style>`


## Related content

To learn more about Azure CNI Overlay networking on AKS, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-disruption -->

# Configure node disruption policies for node auto-provisioning (NAP) nodes in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to configure node disruption policies for Azure Kubernetes Service (AKS) node auto-provisioning (NAP) nodes and details how disruption works to optimize resource utilization and cost efficiency.

NAP optimizes your cluster by:

- Removing or replacing underutilized nodes.
- Consolidating workloads to reduce costs.
- Respecting disruption budgets and maintenance windows.
- Providing manual control when needed.

## Before you begin

- Read the
[Overview of node auto-provisioning (NAP) in AKS](node-auto-provisioning)article, which details[how NAP works](node-auto-provisioning#how-does-node-auto-provisioning-work). - Read the
[Overview of networking configurations for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)](node-auto-provisioning-networking).

## How does node disruption work for NAP nodes?

Karpenter sets a Kubernetes [finalizer](https://kubernetes.io/docs/concepts/overview/working-with-objects/finalizers/) on each node and node claim it provisions. The finalizer blocks the deletion of the node object, while the Termination Controller taints and drains the node before removing the underlying node claim.

When the workloads on your nodes scale down, NAP uses disruption rules on the node pool specification to decide when and how to remove those nodes and potentially reschedule your workloads for efficiency.

## Node disruption methods

NAP automatically discovers nodes eligible for disruption and spins up replacements when needed. You can trigger disruption through automated methods like *Expiration*, *Consolidation*, and *Drift*, manual methods, or external systems.

## Expiration

Expiration allows you to set a maximum age for your NAP nodes. Nodes are marked as expired and disrupted after reaching the age you specify for the node pool's `spec.disruption.expireAfter`

value.

### Example expiration configuration

The following example shows how to set the expiration time for NAP nodes to 24 hours:

```
spec:
disruption:
expireAfter: 24h # Expire nodes after 24 hours
```


## Consolidation

NAP works to actively reduce cluster cost by identifying when nodes can be removed because they're empty or underutilized, or when nodes can be replaced with lower priced variants. This process is called *Consolidation*. NAP primarily uses Consolidation to delete or replace nodes for optimal pod placement.

NAP performs the following types of consolidation in order to optimize resource utilization:

**Empty node consolidation**: Deletes any empty nodes in parallel.**Multi-node consolidation**: Deletes multiple nodes, possibly launching a single replacement.**Single-node consolidation**: Deletes any single node, possibly launching a replacement.

You can trigger consolidation through the `spec.disruption.consolidationPolicy`

field in the node pool specification using the `WhenEmpty`

, or `WhenEmptyOrUnderUtilized`

settings. You can also set the `consolidateAfter`

field, which is a time-based condition that determines how long NAP waits after discovering a consolidation opportunity before disrupting the node.

### Example consolidation configuration

The following example shows how to configure NAP to consolidate nodes when they're empty, and to wait 30 seconds after discovering a consolidation opportunity before disrupting the node:

```
disruption:
# Describes which types of nodes NAP should consider for consolidation
# `WhenEmptyOrUnderUtilized`: NAP considers all nodes for consolidation and attempts to remove or replace nodes when it discovers that the node is empty or underutilized and could be changed to reduce cost
# `WhenEmpty`: NAP only considers nodes for consolidation that don't contain any workload pods
consolidationPolicy: WhenEmpty
# The amount of time NAP should wait after discovering a consolidation decision
# Currently, you can only set this value when the consolidation policy is `WhenEmpty`
# You can choose to disable consolidation entirely by setting the string value `Never`
consolidateAfter: 30s
```


## Drift

Drift handles changes to the `NodePool`

/`AKSNodeClass`

resources. Values in the `NodeClaimTemplateSpec`

/`AKSNodeClassSpec`

are reflected in the same way that they're set. A `NodeClaim`

is detected as *drifted* if the values in the associated `NodePool`

/`AKSNodeClass`

don't match the values in the `NodeClaim`

. Similar to the upstream `deployment.spec.template`

relationship to pods, Karpenter annotates the associated `NodePool`

/`AKSNodeClass`

with a hash of the `NodeClaimTemplateSpec`

to check for drift. Karpenter removes the `Drifted`

status condition in the following scenarios:

- The
`Drift`

feature gate isn't enabled but the`NodeClaim`

is drifted. - The
`NodeClaim`

isn't drifted, but has the status condition.

Karpenter or the cloud provider interface might discover [special cases](#special-cases-on-drift) triggered by `NodeClaim`

/`Instance`

/`NodePool`

/`AKSNodeClass`

changes.

### Special cases on drift

In special cases, drift can correspond to multiple values and must be handled differently. Drift on resolved fields can create cases where drift occurs without changes to Custom Resource Definitions (CRDs), or where CRD changes don't result in drift.

For example, if a `NodeClaim`

has `node.kubernetes.io/instance-type: Standard_D2s_v3`

, and requirements change from `node.kubernetes.io/instance-type In [Standard_D2s_v3]`

to `node.kubernetes.io/instance-type In [Standard_D2s_v3, Standard_D4s_v3]`

, the `NodeClaim`

isn't drifted because its value is still compatible with the new requirements. Conversely, if a `NodeClaim`

uses a `NodeClaim`

`imageFamily`

, but the `spec.imageFamily`

field changes, Karpenter detects the `NodeClaim`

as *drifted* and rotates the node to meet that specification.

Important

Karpenter monitors subnet configuration changes and detects drift when the `vnetSubnetID`

in an `AKSNodeClass`

is modified. Understanding this behavior is critical when managing custom networking configurations. For more information, see [Subnet drift behavior](node-auto-provisioning-networking#subnet-drift-behavior).

For more information, see [Drift Design](https://github.com/aws/karpenter-core/blob/main/designs/drift.md).

## Termination grace period

You can set a termination grace period for NAP nodes using the `spec.template.spec.terminationGracePeriod`

field in the node pool specification. This setting allows you to configure how long Karpenter waits for pods to terminate gracefully. This setting takes precedence over a pod's `terminationGracePeriodSeconds`

and bypasses `PodDisruptionBudgets`

and the `karpenter.sh/do-not-disrupt`

annotation.

### Example termination grace period configuration

The following example shows how to set a termination grace period of 30 seconds for NAP nodes:

```
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
name: default
spec:
template:
spec:
terminationGracePeriod: 30s
```


## Disruption budgets

You can rate limit Karpenter's disruption by modifying the `spec.disruption.budgets`

field in the node pool specification. If you leave this setting undefined, Karpenter defaults to one budget with `nodes: 10%`

. Budgets consider nodes that are being deleted for any reason, and they only block Karpenter from voluntary disruptions through expiration, drift, emptiness, and consolidation.

When calculating if a budget blocks nodes from disruption, Karpenter counts the total nodes owned by a node pool and then subtracts nodes that are being deleted and nodes that are `NotReady`

. If the budget is configured with a percentage value, such as `20%`

, Karpenter calculates the number of allowed disruptions as `allowed_disruptions = roundup(total * percentage) - total_deleting - total_notready`

. For multiple budgets in a node pool, Karpenter takes the minimum (most restrictive) value of each of the budgets.

### Schedule and duration fields

When using budgets, you can optionally set the `schedule`

and `duration`

fields to create time-based budgets. These fields allow you to define maintenance windows or specific timeframes when disruption limits are stricter.

**Schedule**uses cron job syntax with special macros like`@yearly`

,`@monthly`

,`@weekly`

,`@daily`

,`@hourly`

.**Duration**allows compound durations like`10h5m`

,`30m`

, or`160h`

. Duration and Schedule must be defined together.

#### Schedule and duration examples

##### Maintenance window budget

Prevent disruptions during business hours:

```
budgets:
- nodes: "0"
schedule: "0 9 * * 1-5" # 9 AM Monday-Friday
duration: 8h # For 8 hours
```


##### Weekend-only disruptions

Only allow disruptions on weekends:

```
budgets:
- nodes: "50%"
schedule: "0 0 * * 6" # Saturday midnight
duration: 48h # All weekend
- nodes: "0" # Block all other times
```


##### Gradual rollout budget

Allow increasing disruption rates:

```
budgets:
- nodes: "1"
schedule: "0 2 * * *" # 2 AM daily
duration: 2h
- nodes: "3"
schedule: "0 4 * * *" # 4 AM daily
duration: 4h
```


### Budget configuration examples

The following `NodePool`

specification has three budgets configured:

- The first budget allows 20% of nodes owned by the node pool to be disrupted at once.
- The second budget acts as a ceiling, only allowing five disruptions when there are more than 25 nodes.
- The last budget blocks disruptions during the first 10 minutes of each day.

```
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
name: default
spec:
disruption:
consolidationPolicy: WhenEmptyOrUnderutilized
expireAfter: 720h # 30 * 24h = 720h
budgets:
- nodes: "20%" # Allow 20% of nodes to be disrupted
- nodes: "5" # Cap at maximum 5 nodes
- nodes: "0" # Block all disruptions during maintenance window
schedule: "@daily" # Scheduled daily
duration: 10m # Duration of 10 minutes
```


## Manual node disruption

You can manually disrupt NAP nodes using `kubectl`

or by deleting `NodePool`

resources.

### Remove nodes with kubectl

You can manually remove nodes using the `kubectl delete node`

command. You can delete specific nodes, all NAP-managed nodes, or nodes from a specific node pool by using labels, for example:

```
# Delete a specific node
kubectl delete node $NODE_NAME
# Delete all NAP-managed nodes
kubectl delete nodes -l karpenter.sh/nodepool
# Delete nodes from a specific nodepool
kubectl delete nodes -l karpenter.sh/nodepool=$NODEPOOL_NAME
```


### Delete `NodePool`

resources

The `NodePool`

owns `NodeClaims`

through an owner reference. NAP gracefully terminates nodes through cascading deletion when you delete the associated `NodePool`

.

## Control disruption using annotations

You can block or disable disruption for specific pods, nodes, or entire node pools using annotations.

### Pod controls

Block NAP from disrupting certain pods by setting the `karpenter.sh/do-not-disrupt: "true"`

annotation:

```
apiVersion: apps/v1
kind: Deployment
spec:
template:
metadata:
annotations:
karpenter.sh/do-not-disrupt: "true"
```


This annotation prevents voluntary disruption for Expiration, Consolidation, and Drift. However, it doesn't prevent disruption from external systems or manual disruption through `kubectl`

or `NodePool`

deletion.

### Node controls

Block NAP from disrupting specific nodes:

```
apiVersion: v1
kind: Node
metadata:
annotations:
karpenter.sh/do-not-disrupt: "true"
```


### Node pool controls

Disable disruption for all nodes in a `NodePool`

:

```
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
name: default
spec:
template:
metadata:
annotations:
karpenter.sh/do-not-disrupt: "true"
```


## Next steps

For more information on node auto-provisioning in AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ssh -->

# Connect to Azure Kubernetes Service (AKS) cluster nodes for maintenance or troubleshooting

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Throughout the lifecycle of your Azure Kubernetes Service (AKS) cluster, you eventually need to directly access an AKS node. This access could be for maintenance, log collection, or troubleshooting operations.

You access a node through authentication, which methods vary depending on your Node OS and method of connection. You securely authenticate against AKS Linux and Windows nodes through two options discussed in this article. One requires that you have Kubernetes API access, and the other is through the AKS ARM API, which provides direct private IP information. For security reasons, AKS nodes aren't exposed to the internet. Instead, to connect directly to any AKS nodes, you need to use either `kubectl debug`

or the host's private IP address.

## Access nodes using the Kubernetes API

This method requires usage of `kubectl debug`

command.

### Before you begin

This guide shows you how to create a connection to an AKS node and update the SSH key of your AKS cluster. To follow along the steps, you need to use Azure CLI that supports version 2.0.64 or later. Run `az --version`

to check the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Complete these steps if you don't have an SSH key. Create an SSH key depending on your Node OS Image, for [macOS and Linux](/en-us/azure/virtual-machines/linux/mac-create-ssh-keys), or [Windows](/en-us/azure/virtual-machines/linux/ssh-from-windows). Make sure you save the key pair in the OpenSSH format, avoid unsupported formats such as `.ppk`

. Next, refer to [Manage SSH configuration](manage-ssh-node-access) to add the key to your cluster.

### Linux and macOS

Linux and macOS users can access their node using `kubectl debug`

or their private IP Address. Windows users should skip to the Windows Server Proxy section for a workaround to SSH via proxy.

#### Connect using kubectl debug

To create an interactive shell connection, use the `kubectl debug`

command to run a privileged container on your node.

To list your nodes, use the

`kubectl get nodes`

command:`kubectl get nodes -o wide`

Sample output:

`NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE aks-nodepool1-37663765-vmss000000 Ready agent 166m v1.25.6 10.224.0.33 <none> Ubuntu 22.04.2 LTS aks-nodepool1-37663765-vmss000001 Ready agent 166m v1.25.6 10.224.0.4 <none> Ubuntu 22.04.2 LTS aksnpwin000000 Ready agent 160m v1.25.6 10.224.0.62 <none> Windows Server 2022 Datacenter`

Use the

`kubectl debug`

command to start a privileged container on your node and connect to it.`kubectl debug node/aks-nodepool1-37663765-vmss000000 -it --image=mcr.microsoft.com/cbl-mariner/busybox:2.0`

Sample output:

`Creating debugging pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx with container debugger on node aks-nodepool1-37663765-vmss000000. If you don't see a command prompt, try pressing enter. root@aks-nodepool1-37663765-vmss000000:/#`

You now have access to the node through a privileged container as a debugging pod.

Note

You can interact with the node session by running

`chroot /host`

from the privileged container.

#### Exit kubectl debug mode

When you're done with your node, enter the `exit`

command to end the interactive shell session. After the interactive container session closes, delete the debugging pod used with `kubectl delete pod`

.

```
kubectl delete pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx
```


### Windows Server proxy connection for SSH

Follow these steps as a workaround to connect with SSH on a Windows Server node.

#### Create a proxy server

At this time, you can't connect to a Windows Server node directly by using `kubectl debug`

. Instead, you need to first connect to another node in the cluster with `kubectl`

, then connect to the Windows Server node from that node using SSH.

To connect to another node in the cluster, use the `kubectl debug`

command. For more information, follow the above steps in the kubectl section. Create an SSH connection to the Windows Server node from another node using the SSH keys provided when you created the AKS cluster and the internal IP address of the Windows Server node.

Important

The following steps for creating the SSH connection to the Windows Server node from another node can only be used if you created your AKS cluster using the Azure CLI with the `--generate-ssh-keys`

parameter. If you want to use your own SSH keys instead, you can use the `az aks update`

to manage SSH keys on an existing AKS cluster. For more information, see [manage SSH node access](manage-ssh-node-access).

Note

If your Linux proxy node is down or unresponsive, use the [Azure Bastion](/en-us/azure/bastion/bastion-overview) method to connect instead.

Use the

`kubectl debug`

command to start a privileged container on your proxy (Linux) node and connect to it.`kubectl debug node/aks-nodepool1-37663765-vmss000000 -it --image=mcr.microsoft.com/cbl-mariner/busybox:2.0`

Sample output:

`Creating debugging pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx with container debugger on node aks-nodepool1-37663765-vmss000000. If you don't see a command prompt, try pressing enter. root@aks-nodepool1-37663765-vmss000000:/#`

Open a new terminal window and use the

`kubectl get pods`

command to get the name of the pod started by`kubectl debug`

.`kubectl get pods`

Sample output:

`NAME READY STATUS RESTARTS AGE node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx 1/1 Running 0 21s`

In the sample output,

*node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx*is the name of the pod started by`kubectl debug`

.Use the

`kubectl port-forward`

command to open a connection to the deployed pod:`kubectl port-forward node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx 2022:22`

Sample output:

`Forwarding from 127.0.0.1:2022 -> 22 Forwarding from [::1]:2022 -> 22`

The previous example begins forwarding network traffic from port

`2022`

on your development computer to port`22`

on the deployed pod. When using`kubectl port-forward`

to open a connection and forward network traffic, the connection remains open until you stop the`kubectl port-forward`

command.Open a new terminal and run the command

`kubectl get nodes`

to show the internal IP address of the Windows Server node:`kubectl get no -o custom-columns=NAME:metadata.name,'INTERNAL_IP:status.addresses[?(@.type == \"InternalIP\")].address'`

Sample output:

`NAME INTERNAL_IP aks-nodepool1-19409214-vmss000003 10.224.0.8`

In the previous example,

*10.224.0.62*is the internal IP address of the Windows Server node.Create an SSH connection to the Windows Server node using the internal IP address, and connect to port

`22`

through port`2022`

on your development computer. The default username for AKS nodes is*azureuser*. Accept the prompt to continue with the connection. You're then provided with the bash prompt of your Windows Server node:`ssh -o 'ProxyCommand ssh -p 2022 -W %h:%p azureuser@127.0.0.1' azureuser@10.224.0.62`

Sample output:

`The authenticity of host '10.224.0.62 (10.224.0.62)' can't be established. ECDSA key fingerprint is SHA256:1234567890abcdefghijklmnopqrstuvwxyzABCDEFG. Are you sure you want to continue connecting (yes/no)? yes`

Note

If you prefer to use password authentication, include the parameter

`-o PreferredAuthentications=password`

. For example:`ssh -o 'ProxyCommand ssh -p 2022 -W %h:%p azureuser@127.0.0.1' -o PreferredAuthentications=password azureuser@10.224.0.62`


## Use a host process container to access Windows node

Run the following script to create

`hostprocess.yaml`

. In the script, replace`AKSWINDOWSNODENAME`

with the AKS Windows node name.This specification uses the nanoserver base image. The base image doesn't have PowerShell, but because it runs as a host process container (HPC), PowerShell is available in the underlying VM.

`apiVersion: v1 kind: Pod metadata: labels: pod: hpc name: hpc spec: securityContext: windowsOptions: hostProcess: true runAsUserName: "NT AUTHORITY\\SYSTEM" hostNetwork: true containers: - name: hpc image: mcr.microsoft.com/windows/nanoserver:ltsc2022 # Use nanoserver:1809 for WS2019 command: - powershell.exe - -Command - "Start-Sleep 2147483" imagePullPolicy: IfNotPresent nodeSelector: kubernetes.io/os: windows kubernetes.io/hostname: AKSWINDOWSNODENAME tolerations: - effect: NoSchedule key: node.kubernetes.io/unschedulable operator: Exists - effect: NoSchedule key: node.kubernetes.io/network-unavailable operator: Exists - effect: NoExecute key: node.kubernetes.io/unreachable operator: Exists`

Run

`kubectl apply -f hostprocess.yaml`

to deploy the Windows HPC in the specified Windows node.Use

`kubectl exec -it [HPC-POD-NAME] -- powershell`

.You can run any PowerShell commands inside the HPC container to access the Windows node.


Note

You need to switch the root folder to `C:\`

inside the HPC container to access the files in the Windows node.

## SSH using Azure Bastion for Windows

If your Linux proxy node isn't reachable, using Azure Bastion as a proxy is an alternative. This method requires that you set up an Azure Bastion host for the virtual network in which the cluster resides. See [Connect with Azure Bastion](/en-us/azure/bastion/bastion-overview) for more details.

## SSH using private IPs from the AKS API

If you don't have access to the Kubernetes API, you can get access to properties such as `Node IP`

and `Node Name`

through the [AKS agent pool API ](/en-us/rest/api/aks/agent-pools/get#agentpool), (available on stable versions `07-01-2024`

or above) to connect to AKS nodes.

### Create an interactive shell connection to a node using the IP address

For convenience, AKS nodes are exposed on the cluster's virtual network through private IP addresses. However, you need to be in the cluster's virtual network to SSH into the node. If you don't already have an environment configured, you can use [Azure Bastion](/en-us/azure/bastion/bastion-connect-vm-ssh-linux) to establish a proxy from which you can SSH to cluster nodes. Make sure the Azure Bastion is deployed in the same virtual network as the cluster.

Obtain private IPs using the

`az aks machine list`

command, targeting all the VMs in a specific node pool with the`--nodepool-name`

flag.`az aks machine list --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name nodepool1 -o table`

The following example output shows the internal IP addresses of all the nodes in the node pool:

`Name Ip Family --------------------------------- ----------- ----------- aks-nodepool1-33555069-vmss000000 10.224.0.5 IPv4 aks-nodepool1-33555069-vmss000001 10.224.0.6 IPv4 aks-nodepool1-33555069-vmss000002 10.224.0.4 IPv4`

To target a specific node inside the node pool, use the

`--machine-name`

flag:`az aks machine show --cluster-name myAKScluster --nodepool-name nodepool1 -g myResourceGroup --machine-name aks-nodepool1-33555069-vmss000000 -o table`

The following example output shows the internal IP address of all the specified node:

`Name Ip Family --------------------------------- ----------- ----------- aks-nodepool1-33555069-vmss000000 10.224.0.5 IPv4`

SSH to the node using the private IP address you obtained in the previous step. This step is applicable for Linux machines only. For Windows machines, see

[Connect with Azure Bastion](/en-us/azure/bastion/bastion-overview).`ssh -i /path/to/private_key.pem azureuser@10.224.0.33`


## Next steps

If you need more troubleshooting data, you can [view the kubelet logs](kubelet-logs) or [view the Kubernetes control plane logs](monitor-aks-reference#resource-logs).

To learn about managing your SSH keys, see [Manage SSH configuration](manage-ssh-node-access).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-access -->

# Connect to Azure Kubernetes Service (AKS) cluster nodes for maintenance or troubleshooting

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Throughout the lifecycle of your Azure Kubernetes Service (AKS) cluster, you eventually need to directly access an AKS node. This access could be for maintenance, log collection, or troubleshooting operations.

You access a node through authentication, which methods vary depending on your Node OS and method of connection. You securely authenticate against AKS Linux and Windows nodes through two options discussed in this article. One requires that you have Kubernetes API access, and the other is through the AKS ARM API, which provides direct private IP information. For security reasons, AKS nodes aren't exposed to the internet. Instead, to connect directly to any AKS nodes, you need to use either `kubectl debug`

or the host's private IP address.

## Access nodes using the Kubernetes API

This method requires usage of `kubectl debug`

command.

### Before you begin

This guide shows you how to create a connection to an AKS node and update the SSH key of your AKS cluster. To follow along the steps, you need to use Azure CLI that supports version 2.0.64 or later. Run `az --version`

to check the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Complete these steps if you don't have an SSH key. Create an SSH key depending on your Node OS Image, for [macOS and Linux](/en-us/azure/virtual-machines/linux/mac-create-ssh-keys), or [Windows](/en-us/azure/virtual-machines/linux/ssh-from-windows). Make sure you save the key pair in the OpenSSH format, avoid unsupported formats such as `.ppk`

. Next, refer to [Manage SSH configuration](manage-ssh-node-access) to add the key to your cluster.

### Linux and macOS

Linux and macOS users can access their node using `kubectl debug`

or their private IP Address. Windows users should skip to the Windows Server Proxy section for a workaround to SSH via proxy.

#### Connect using kubectl debug

To create an interactive shell connection, use the `kubectl debug`

command to run a privileged container on your node.

To list your nodes, use the

`kubectl get nodes`

command:`kubectl get nodes -o wide`

Sample output:

`NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE aks-nodepool1-37663765-vmss000000 Ready agent 166m v1.25.6 10.224.0.33 <none> Ubuntu 22.04.2 LTS aks-nodepool1-37663765-vmss000001 Ready agent 166m v1.25.6 10.224.0.4 <none> Ubuntu 22.04.2 LTS aksnpwin000000 Ready agent 160m v1.25.6 10.224.0.62 <none> Windows Server 2022 Datacenter`

Use the

`kubectl debug`

command to start a privileged container on your node and connect to it.`kubectl debug node/aks-nodepool1-37663765-vmss000000 -it --image=mcr.microsoft.com/cbl-mariner/busybox:2.0`

Sample output:

`Creating debugging pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx with container debugger on node aks-nodepool1-37663765-vmss000000. If you don't see a command prompt, try pressing enter. root@aks-nodepool1-37663765-vmss000000:/#`

You now have access to the node through a privileged container as a debugging pod.

Note

You can interact with the node session by running

`chroot /host`

from the privileged container.

#### Exit kubectl debug mode

When you're done with your node, enter the `exit`

command to end the interactive shell session. After the interactive container session closes, delete the debugging pod used with `kubectl delete pod`

.

```
kubectl delete pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx
```


### Windows Server proxy connection for SSH

Follow these steps as a workaround to connect with SSH on a Windows Server node.

#### Create a proxy server

At this time, you can't connect to a Windows Server node directly by using `kubectl debug`

. Instead, you need to first connect to another node in the cluster with `kubectl`

, then connect to the Windows Server node from that node using SSH.

To connect to another node in the cluster, use the `kubectl debug`

command. For more information, follow the above steps in the kubectl section. Create an SSH connection to the Windows Server node from another node using the SSH keys provided when you created the AKS cluster and the internal IP address of the Windows Server node.

Important

The following steps for creating the SSH connection to the Windows Server node from another node can only be used if you created your AKS cluster using the Azure CLI with the `--generate-ssh-keys`

parameter. If you want to use your own SSH keys instead, you can use the `az aks update`

to manage SSH keys on an existing AKS cluster. For more information, see [manage SSH node access](manage-ssh-node-access).

Note

If your Linux proxy node is down or unresponsive, use the [Azure Bastion](/en-us/azure/bastion/bastion-overview) method to connect instead.

Use the

`kubectl debug`

command to start a privileged container on your proxy (Linux) node and connect to it.`kubectl debug node/aks-nodepool1-37663765-vmss000000 -it --image=mcr.microsoft.com/cbl-mariner/busybox:2.0`

Sample output:

`Creating debugging pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx with container debugger on node aks-nodepool1-37663765-vmss000000. If you don't see a command prompt, try pressing enter. root@aks-nodepool1-37663765-vmss000000:/#`

Open a new terminal window and use the

`kubectl get pods`

command to get the name of the pod started by`kubectl debug`

.`kubectl get pods`

Sample output:

`NAME READY STATUS RESTARTS AGE node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx 1/1 Running 0 21s`

In the sample output,

*node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx*is the name of the pod started by`kubectl debug`

.Use the

`kubectl port-forward`

command to open a connection to the deployed pod:`kubectl port-forward node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx 2022:22`

Sample output:

`Forwarding from 127.0.0.1:2022 -> 22 Forwarding from [::1]:2022 -> 22`

The previous example begins forwarding network traffic from port

`2022`

on your development computer to port`22`

on the deployed pod. When using`kubectl port-forward`

to open a connection and forward network traffic, the connection remains open until you stop the`kubectl port-forward`

command.Open a new terminal and run the command

`kubectl get nodes`

to show the internal IP address of the Windows Server node:`kubectl get no -o custom-columns=NAME:metadata.name,'INTERNAL_IP:status.addresses[?(@.type == \"InternalIP\")].address'`

Sample output:

`NAME INTERNAL_IP aks-nodepool1-19409214-vmss000003 10.224.0.8`

In the previous example,

*10.224.0.62*is the internal IP address of the Windows Server node.Create an SSH connection to the Windows Server node using the internal IP address, and connect to port

`22`

through port`2022`

on your development computer. The default username for AKS nodes is*azureuser*. Accept the prompt to continue with the connection. You're then provided with the bash prompt of your Windows Server node:`ssh -o 'ProxyCommand ssh -p 2022 -W %h:%p azureuser@127.0.0.1' azureuser@10.224.0.62`

Sample output:

`The authenticity of host '10.224.0.62 (10.224.0.62)' can't be established. ECDSA key fingerprint is SHA256:1234567890abcdefghijklmnopqrstuvwxyzABCDEFG. Are you sure you want to continue connecting (yes/no)? yes`

Note

If you prefer to use password authentication, include the parameter

`-o PreferredAuthentications=password`

. For example:`ssh -o 'ProxyCommand ssh -p 2022 -W %h:%p azureuser@127.0.0.1' -o PreferredAuthentications=password azureuser@10.224.0.62`


## Use a host process container to access Windows node

Run the following script to create

`hostprocess.yaml`

. In the script, replace`AKSWINDOWSNODENAME`

with the AKS Windows node name.This specification uses the nanoserver base image. The base image doesn't have PowerShell, but because it runs as a host process container (HPC), PowerShell is available in the underlying VM.

`apiVersion: v1 kind: Pod metadata: labels: pod: hpc name: hpc spec: securityContext: windowsOptions: hostProcess: true runAsUserName: "NT AUTHORITY\\SYSTEM" hostNetwork: true containers: - name: hpc image: mcr.microsoft.com/windows/nanoserver:ltsc2022 # Use nanoserver:1809 for WS2019 command: - powershell.exe - -Command - "Start-Sleep 2147483" imagePullPolicy: IfNotPresent nodeSelector: kubernetes.io/os: windows kubernetes.io/hostname: AKSWINDOWSNODENAME tolerations: - effect: NoSchedule key: node.kubernetes.io/unschedulable operator: Exists - effect: NoSchedule key: node.kubernetes.io/network-unavailable operator: Exists - effect: NoExecute key: node.kubernetes.io/unreachable operator: Exists`

Run

`kubectl apply -f hostprocess.yaml`

to deploy the Windows HPC in the specified Windows node.Use

`kubectl exec -it [HPC-POD-NAME] -- powershell`

.You can run any PowerShell commands inside the HPC container to access the Windows node.


Note

You need to switch the root folder to `C:\`

inside the HPC container to access the files in the Windows node.

## SSH using Azure Bastion for Windows

If your Linux proxy node isn't reachable, using Azure Bastion as a proxy is an alternative. This method requires that you set up an Azure Bastion host for the virtual network in which the cluster resides. See [Connect with Azure Bastion](/en-us/azure/bastion/bastion-overview) for more details.

## SSH using private IPs from the AKS API

If you don't have access to the Kubernetes API, you can get access to properties such as `Node IP`

and `Node Name`

through the [AKS agent pool API ](/en-us/rest/api/aks/agent-pools/get#agentpool), (available on stable versions `07-01-2024`

or above) to connect to AKS nodes.

### Create an interactive shell connection to a node using the IP address

For convenience, AKS nodes are exposed on the cluster's virtual network through private IP addresses. However, you need to be in the cluster's virtual network to SSH into the node. If you don't already have an environment configured, you can use [Azure Bastion](/en-us/azure/bastion/bastion-connect-vm-ssh-linux) to establish a proxy from which you can SSH to cluster nodes. Make sure the Azure Bastion is deployed in the same virtual network as the cluster.

Obtain private IPs using the

`az aks machine list`

command, targeting all the VMs in a specific node pool with the`--nodepool-name`

flag.`az aks machine list --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name nodepool1 -o table`

The following example output shows the internal IP addresses of all the nodes in the node pool:

`Name Ip Family --------------------------------- ----------- ----------- aks-nodepool1-33555069-vmss000000 10.224.0.5 IPv4 aks-nodepool1-33555069-vmss000001 10.224.0.6 IPv4 aks-nodepool1-33555069-vmss000002 10.224.0.4 IPv4`

To target a specific node inside the node pool, use the

`--machine-name`

flag:`az aks machine show --cluster-name myAKScluster --nodepool-name nodepool1 -g myResourceGroup --machine-name aks-nodepool1-33555069-vmss000000 -o table`

The following example output shows the internal IP address of all the specified node:

`Name Ip Family --------------------------------- ----------- ----------- aks-nodepool1-33555069-vmss000000 10.224.0.5 IPv4`

SSH to the node using the private IP address you obtained in the previous step. This step is applicable for Linux machines only. For Windows machines, see

[Connect with Azure Bastion](/en-us/azure/bastion/bastion-overview).`ssh -i /path/to/private_key.pem azureuser@10.224.0.33`


## Next steps

If you need more troubleshooting data, you can [view the kubelet logs](kubelet-logs) or [view the Kubernetes control plane logs](monitor-aks-reference#resource-logs).

To learn about managing your SSH keys, see [Manage SSH configuration](manage-ssh-node-access).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/certificate-rotation -->

# Certificate rotation in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) uses certificates for authentication with many of its components. You need to periodically rotate those certificates for security or policy reasons. This article shows you how certificate rotation works in your AKS cluster.

Important

Starting on **March 30, 2026** Azure Kubernetes Service (AKS) no longer supports the `aks-disable-kubelet-serving-certificate-rotation=true`

node pool tag to disable Kubelet Serving Certificate Rotation (KSCR). You can create new node pools using this tag, but AKS won't respect it. This behavior means that the node pools will be created with KSCR enabled. For existing node pools, KSCR will be automatically enabled on their next reimage operation. Before this date you can update your node pools using the [`az aks nodepool update`

][az-aks-nodepool-update] command with the `aks-disable-kubelet-serving-certificate-rotation=true`

tag. To prepare for the removal, you should update your workloads with the correct cert path. For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/5539). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Prerequisites

This article requires the Azure CLI version 2.0.77 or later. Check your version using the

`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).Configure

`kubectl`

to connect to your AKS cluster using thecommand:`az aks get-credentials`

`az aks get-credentials --resource-group <resource-group> --name <cluster-name>`


## AKS certificates, Certificate Authorities, and Service Accounts

AKS generates and uses the following certificates, Certificate Authorities (CA), and Service Accounts (SA):

- The AKS API server creates a CA called the
*Cluster CA*, which signs certificates for one-way communication from the API server to kubelet. - Each kubelet creates a Certificate Signing Request (CSR), which the Cluster CA signs, for communication from the kubelet to the API server.
- The API aggregator uses the Cluster CA to issue certificates for communication with other APIs. The API aggregator can also have its own CA for issuing those certificates, but it currently uses the Cluster CA.
- Each agent node uses an SA token, which the Cluster CA signs.
- The
`kubectl`

client has a certificate for communicating with the AKS cluster.

Microsoft maintains all certificates mentioned in this section, except for the cluster certificate.

## Certificate expiration dates

Important

The expiration date for your certificates depends on when your AKS cluster was created:

**AKS clusters created**have certificates that expire after two years.*before*May 2019**AKS clusters created**have Cluster CA certificates that expire after 30 years.*after*May 2019

You can verify when your cluster was created using the `kubectl get nodes`

command, which shows you the `Age`

of your agent nodes.

## Check cluster certificate expiration date

Check the expiration date of the cluster certificate using the

`kubectl config view`

command.`kubectl config view --raw -o jsonpath="{.clusters[?(@.name == '')].cluster.certificate-authority-data}" | base64 -d | openssl x509 -text | grep -A2 Validity`


## Check API server certificate expiration date

Check the expiration date of the API server certificate using the following

`curl`

command:`curl https://{apiserver-fqdn} -k -v 2>&1 | grep expire`


## Check virtual machine (VM) agent node certificate expiration date

Check the expiration date of the VM agent node certificate using the

command.`az vm run-command invoke`

**Key parameters in this command**: -`--resource-group <node-resource-group>`

: The resource group that contains the VM agent node. -`--name <vm-name>`

: The name of the VM agent node. -`--scripts "openssl x509 -in /etc/kubernetes/certs/apiserver.crt -noout -enddate"`

: The script that retrieves the expiration date of the API server certificate located at`/etc/kubernetes/certs/apiserver.crt`

.`az vm run-command invoke --resource-group <node-resource-group> --name <vm-name> --command-id RunShellScript --query 'value[0].message' -otsv --scripts "openssl x509 -in /etc/kubernetes/certs/apiserver.crt -noout -enddate"`


## Check certificate expiration for the Azure Virtual Machine Scale Set agent node

Check the expiration date of the Azure Virtual Machine Scale Set agent node certificate using the

command.`az vmss run-command invoke`

**Key parameters in this command**: -`--resource-group <node-resource-group>`

: The resource group that contains the Azure Virtual Machine Scale Set agent node. -`--name <vmss-name>`

: The name of the Azure Virtual Machine Scale Set. -`--instance-id 1`

: The instance ID of the Azure Virtual Machine Scale Set agent node. -`--scripts "openssl x509 -in /var/lib/kubelet/pki/kubelet-client-current.pem -noout -enddate"`

: The script that retrieves the expiration date of the kubelet client certificate located at`/var/lib/kubelet/pki/kubelet-client-current.pem`

.`az vmss run-command invoke --resource-group <node-resource-group> --name <vmss-name> --command-id RunShellScript --instance-id 1 --scripts "openssl x509 -in /var/lib/kubelet/pki/kubelet-client-current.pem -noout -enddate" --query "value[0].message"`


## Manually rotate your cluster certificates

Rotate all certificates, CAs, and SAs on your cluster using the

command.`az aks rotate-certs`

`az aks rotate-certs --resource-group <resource-group> --name <cluster-name>`

Important

The

command recreates all of your agent nodes, Azure Virtual Machine Scale Sets, and disks. This command can also cause up to`az aks rotate-certs`

*30 minutes of downtime*for your AKS cluster. If the command fails before completing, use the [`az aks show`

][az-aks-show] command to verify the status of the cluster is`Certificate Rotating`

. If the cluster is in a failed state, rerun thecommand to rotate your certificates again.`az aks rotate-certs`

Verify the old certificates are no longer valid using any

`kubectl`

command. The following example uses the`kubectl get nodes`

command:`kubectl get nodes`

If you didn't update the certificates used by

`kubectl`

, you see an error similar to the following example output:`Unable to connect to the server: x509: certificate signed by unknown authority (possibly because of "crypto/rsa: verification error" while trying to verify candidate authority certificate "ca")`

Update the certificate used by

`kubectl`

using thecommand with the`az aks get-credentials`

`--overwrite-existing`

flag.`az aks get-credentials --resource-group <resource-group> --name <cluster-name> --overwrite-existing`

Verify the certificates are updated using the

command.`kubectl get`

`kubectl get nodes`


If you have any services that run on top of AKS, you might need to update their certificates as well.

## Rotate the kubelet serving certificate

When you rotate the kubelet serving certificate, AKS allows kubelet server Transport Layer Security (TLS) Bootstrapping for both bootstrapping and rotating serving certificates signed by the Cluster CA.

### Limitations for kubelet serving certificate rotation

- Supported on Kubernetes version 1.27 and above.
- Not supported when the node pool is using a node pool snapshot based on any node image older than
`202501.12.0`

. - You can't manually enable this feature. Kubelet serving certificate rotation is enabled by default on existing node pools when they perform their first upgrade to any Kubernetes version 1.27 or higher. Kubelet serving certificate rotation is enabled by default on new node pools using Kubernetes version 1.27 or higher. To see if kubelet serving certificate rotation is enabled in your region, check the
[AKS releases](https://github.com/Azure/AKS/releases).

## Verify kubelet serving certificate rotation is enabled

Each node with the feature enabled is automatically given the label `kubernetes.azure.com/kubelet-serving-ca=cluster`

.

Verify the labels are set using the

`kubectl get nodes -L kubernetes.azure.com/kubelet-serving-ca`

command.`kubectl get nodes -L kubernetes.azure.com/kubelet-serving-ca`

The output should show the label

`kubernetes.azure.com/kubelet-serving-ca`

with the value`cluster`

for each agent node.

## Verify kubelet TLS Bootstrapping is working

Verify the bootstrapping process is taking place using the

command.`kubectl get`

`kubectl get csr --field-selector=spec.signerName=kubernetes.io/kubelet-serving`

In the output, all serving CSRs should be in the

`Approved,Issued`

state, which indicates the CSR was approved and issued a signed certificate. Serving CSRs have a signer name of`kubernetes.io/kubelet-serving`

. For example:`NAME AGE SIGNERNAME REQUESTOR REQUESTEDDURATION CONDITION csr-1ab2c 113s kubernetes.io/kube-apiserver-client-kubelet system:bootstrap:uoxr9r none Approved,Issued csr-defgh 111s kubernetes.io/kubelet-serving system:node:akswinp7000000 none Approved,Issued csr-ij3kl 46m kubernetes.io/kubelet-serving system:node:akswinp6000000 none Approved,Issued csr-mn4op 46m kubernetes.io/kube-apiserver-client-kubelet system:bootstrap:ho7zyu none Approved,Issued`


## Verify kubelet is using a certificate obtained from server TLS Bootstrapping

Confirm the kubelet is using a serving certificate signed by the Cluster CA using the

command.`kubectl debug`

`kubectl debug node/<node> -ti --image=mcr.microsoft.com/azurelinux/base/core:3.0 -- ls -l /host/var/lib/kubelet/kubelet-server-current.pem`

If a

`kubelet-server-current.pem`

symlink exists, then the kubelet bootstrapped/rotated its own serving certificate, and the Cluster CA signed it.

## Disable kubelet serving certificate rotation

Disable kubelet serving certificate rotation by updating the node pool using the

command with the`az aks nodepool update`

`aks-disable-kubelet-serving-certificate-rotation=true`

tag.`az aks nodepool update --cluster-name <cluster-name> --resource-group <resource-group> --name <node-pool-name> --tags aks-disable-kubelet-serving-certificate-rotation=true`


- Reimage your nodes using a
[node image upgrade](node-image-upgrade)or by scaling the pool to*zero*instances and then back up to the desired value.

## Certificate autorotation

Keep the following considerations in mind when using certificate autorotation:

- If you have an existing cluster, you have to upgrade that cluster to enable certificate autorotation.
- Don't disable TLS Bootstrap to keep certificate autorotation enabled.
- If the cluster is in a stopped state during certificate autorotation, only the control plane certificates are rotated. In this case, you should recreate the node pool after certificate rotation to initiate the node pool certificate rotation.
- For any AKS clusters created or upgraded after March 2022, AKS automatically rotates non-CA certificates on both the control plane and agent nodes within 80% of the client certificate valid time before they expire with no downtime for the cluster.

## Verify TLS Bootstrapping is enabled on current agent node pool

Verify your cluster has TLS Bootstrapping enabled by browsing to one to the following paths:

**On a Linux node**:`/var/lib/kubelet/bootstrap-kubeconfig`

or`/host/var/lib/kubelet/bootstrap-kubeconfig`

**On a Windows node**:`C:\k\bootstrap-config`


For more information, see

[Connect to Azure Kubernetes Service (AKS) cluster nodes for maintenance or troubleshooting](node-access).Note

The file path might change as Kubernetes versions evolve.

Once a region is configured, create a new cluster or upgrade an existing cluster to set certificate autorotation for the cluster certificate. You need to upgrade the control plane and node pool to enable this feature.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/csi-secrets-store-configuration-options -->

# Azure Key Vault provider for Secrets Store CSI Driver for Azure Kubernetes Service (AKS) configuration options

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes configuration options for the Azure Key Vault provider for Secrets Store CSI Driver in Azure Kubernetes Service (AKS), including how to enable and customize autorotation of secrets, sync mounted content with a Kubernetes secret, and access metrics.

## Prerequisites

Before you begin, complete the steps in [Use the Azure Key Vault provider for Secrets Store CSI Driver in an AKS cluster](csi-secrets-store-driver) and [Provide an identity to access the Azure Key Vault provider for Secrets Store CSI Driver in AKS](csi-secrets-store-identity-access).

## Autorotation and secret sync overview

Once you enable autorotation, the Azure Key Vault provider for Secrets Store CSI Driver updates the pod mount and the Kubernetes secret defined in the `secretObjects`

field of the `SecretProviderClass`

. It does so by polling for changes periodically, based on the rotation poll interval you defined. The default rotation poll interval is *two minutes*.

When you update a secret in an external secrets store after initial pod deployment, the Kubernetes Secret and the pod mount periodically update depending on how the application consumes the secret data.

**Mount the Kubernetes Secret as a volume**: Use the autorotation and sync K8s secrets features of Secrets Store CSI Driver. The application needs to watch for changes from the mounted Kubernetes Secret volume. When the CSI Driver updates the Kubernetes Secret, the corresponding volume contents automatically update as well.**Application reads the data from the container filesystem**: Use the rotation feature of Secrets Store CSI Driver. The application needs to watch for the file change from the volume mounted by the CSI driver.**Use the Kubernetes Secret for an environment variable**: Restart the pod to get the latest secret as an environment variable. Use a tool such as[Reloader](https://github.com/stakater/Reloader)to watch for changes on the synced Kubernetes Secret and perform rolling upgrades on pods.

## Enable autorotation on a new AKS cluster

Enable autorotation of secrets on a new cluster using the

command and with the`az aks create`

`--enable-secret-rotation`

flag and the`--enable-addons`

flat set to`azure-keyvault-secrets-provider`

. The following example creates a new AKS cluster named`myAKSCluster`

in the resource group`myResourceGroup`

:`az aks create \ --name myAKSCluster \ --resource-group myResourceGroup \ --enable-addons azure-keyvault-secrets-provider \ --enable-secret-rotation \ --generate-ssh-keys`

Condensed example output:

`{ "aadProfile": null, "addonProfiles": { "azureKeyvaultSecretsProvider": { "config": { "enableSecretRotation": "true", "rotationPollInterval": "2m" }, "enabled": true, ...`


## Enable autorotation on an existing AKS cluster

Update an existing cluster to enable secret autorotation using the

command with the`az aks addon update`

`enable-secret-rotation`

parameter and the`--addon`

flag set to`azure-keyvault-secrets-provider`

. The following example updates an existing AKS cluster named`myAKSCluster`

in the resource group`myResourceGroup`

:`az aks addon update --resource-group myResourceGroup --name myAKSCluster --addon azure-keyvault-secrets-provider --enable-secret-rotation`


## Customize rotation interval

Specify a custom rotation interval using the

command with the`az aks addon update`

`rotation-poll-interval`

parameter. The following example sets the rotation poll interval to five minutes for an existing AKS cluster named`myAKSCluster`

in the resource group`myResourceGroup`

:`az aks addon update --resource-group myResourceGroup --name myAKSCluster --addon azure-keyvault-secrets-provider --enable-secret-rotation --rotation-poll-interval 5m`

Condensed example output:

`... "rotationPollInterval": "5m" ...`


## Disable autorotation on an existing AKS cluster

Tip

If you're already using a `SecretProviderClass`

, you can update the add-on without disabling it first using the `az aks addon enable`

command without the `--enable-secret-rotation`

parameter.

Disable the Azure Key Vault provider for Secrets Store Driver add-on using the

command. The following example disables the add-on for an existing AKS cluster named`az aks addon disable`

`myAKSCluster`

in the resource group`myResourceGroup`

:`az aks addon disable --resource-group myResourceGroup --name myAKSCluster --addon azure-keyvault-secrets-provider`

Condensed example output:

`... "azureKeyvaultSecretsProvider": { "config": null, "enabled": false, "identity": null ...`

Re-enable the Azure Key Vault provider for Secrets Store Driver add-on without the

`enable-secret-rotation`

parameter using thecommand. The following example re-enables the add-on for the existing AKS cluster named`az aks addon enable`

`myAKSCluster`

in the resource group`myResourceGroup`

:`az aks addon enable --resource-group myResourceGroup --name myAKSCluster --addon azure-keyvault-secrets-provider`

Condensed example output:

`... "enableSecretRotation": "false", "rotationPollInterval": "2m" }, "enabled": true, ...`


## Sync mounted content with a Kubernetes secret

Note

Before using the YAML example in this section, you need to modify them to support your chosen method of access to your key vault identity. For more information, see [Provide an identity to access the Azure Key Vault provider for Secrets Store CSI Driver](csi-secrets-store-identity-access).

You might want to create a Kubernetes secret to mirror your mounted secrets content. Your secrets sync after you start a pod to mount them. When you delete the pods that consume the secrets, your Kubernetes secret is also deleted.

Sync mounted content with a Kubernetes secret using the

`secretObjects`

field when creating a`SecretProviderClass`

to define the desired state of the Kubernetes secret, as shown in the following example YAML.`apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: azure-sync spec: provider: azure secretObjects: # [OPTIONAL] SecretObjects defines the desired state of synced Kubernetes secret objects - data: - key: username # data field to populate objectName: foo1 # name of the mounted content to sync; this could be the object name or the object alias secretName: foosecret # name of the Kubernetes secret object type: Opaque # type of Kubernetes secret object (for example, Opaque, kubernetes.io/tls)`

Note

Make sure the

`objectName`

in the`secretObjects`

field matches the file name of the mounted content. If you use`objectAlias`

instead, it should match the object alias.

## Set an environment variable to reference Kubernetes secrets

Note

The example YAML demonstrates access to a secret through env variables and volume/volumeMount. A typical application would use one method or the other. Keep in mind that a secret needs to be mounted by at least one pod in order to become available through env variables.

Reference your newly created Kubernetes secret by setting an environment variable in your pod, as shown in the following example YAML:

`kind: Pod apiVersion: v1 metadata: name: busybox-secrets-store-inline spec: containers: - name: busybox image: registry.k8s.io/e2e-test-images/busybox:1.29-1 command: - "/bin/sleep" - "10000" volumeMounts: - name: secrets-store01-inline mountPath: "/mnt/secrets-store" readOnly: true env: - name: SECRET_USERNAME valueFrom: secretKeyRef: name: foosecret key: username volumes: - name: secrets-store01-inline csi: driver: secrets-store.csi.k8s.io readOnly: true volumeAttributes: secretProviderClass: "azure-sync"`


## Access Azure Key Vault provider and Secrets Store CSI Driver metrics

You can access metrics provided by both the Azure Key Vault provider for Secrets Store CSI Driver and the Secrets Store CSI Driver itself. These metrics can help you monitor the performance and health of your secrets management solution.

### Azure Key Vault provider metrics

The Azure Key Vault provider exposes the following metrics:

| Metric | Description | Tags |
|---|---|---|
`keyvault_request` |
The distribution of how long it took to get from the key vault. | `os_type=<runtime os>` , `provider=azure` , `object_name=<keyvault object name>` , `object_type=<keyvault object type>` , `error=<error if failed>` |
`grpc_request` |
The distribution of how long it took for the gRPC requests. | `os_type=<runtime os>` , `provider=azure` , `grpc_method=<rpc full method>` , `grpc_code=<grpc status code>` , `grpc_message=<grpc status message>` |

Metrics are served via Prometheus from port 8898, but this port isn't exposed outside the pod by default.

Access the Azure Key Vault provider metrics over localhost using the

`kubectl port-forward`

command.`kubectl port-forward -n kube-system ds/aks-secrets-store-provider-azure 8898:8898 & curl localhost:8898/metrics`


### Secrets Store CSI Driver metrics

The Secrets Store CSI Driver exposes the following metrics:

| Metric | Description | Tags |
|---|---|---|
`total_node_publish` |
The total number of successful volume mount requests. | `os_type=<runtime os>` , `provider=<provider name>` |
`total_node_unpublish` |
The total number of successful volume unmount requests. | `os_type=<runtime os>` |
`total_node_publish_error` |
The total number of errors with volume mount requests. | `os_type=<runtime os>` , `provider=<provider name>` , `error_type=<error code>` |
`total_node_unpublish_error` |
The total number of errors with volume unmount requests. | `os_type=<runtime os>` |
`total_sync_k8s_secret` |
The total number of Kubernetes secrets synced. | `os_type=<runtime os>` , `provider=<provider name>` |
`sync_k8s_secret_duration_sec` |
The distribution of how long it took to sync the Kubernetes secret. | `os_type=<runtime os>` |
`total_rotation_reconcile` |
The total number of rotation reconciles. | `os_type=<runtime os>` , `rotated=<true or false>` |
`total_rotation_reconcile_error` |
The total number of rotation reconciles with errors. | `os_type=<runtime os>` , `rotated=<true or false>` , `error_type=<error code>` |
`rotation_reconcile_duration_sec` |
The distribution of how long it took to rotate secrets-store content for pods. | `os_type=<runtime os>` |

Metrics are served from port 8095, but this port isn't exposed outside the pod by default.

Access the Secrets Store CSI Driver metrics over localhost using the

`kubectl port-forward`

command.`kubectl port-forward -n kube-system ds/aks-secrets-store-csi-driver 8095:8095 & curl localhost:8095/metrics`


## Migrate from open-source to AKS-managed Secrets Store CSI Driver

Uninstall the open-source Secrets Store CSI Driver using the following

`helm delete`

command.`helm delete <release name>`

Note

If you installed the driver and provider using deployment YAMLs, you can delete the components using the following

`kubectl delete`

commands:`# Delete AKV provider pods from Linux nodes kubectl delete -f https://raw.githubusercontent.com/Azure/secrets-store-csi-driver-provider-azure/master/deployment/provider-azure-installer.yaml # Delete AKV provider pods from Windows nodes kubectl delete -f https://raw.githubusercontent.com/Azure/secrets-store-csi-driver-provider-azure/master/deployment/provider-azure-installer-windows.yaml`

Upgrade your existing AKS cluster with the feature using the

command with the`az aks enable-addons`

`--addons`

parameter set to`azure-keyvault-secrets-provider`

. The following example enables the add-on for an existing AKS cluster named`myAKSCluster`

in the resource group`myResourceGroup`

:`az aks enable-addons --addons azure-keyvault-secrets-provider --name myAKSCluster --resource-group myResourceGroup`


## Related content

To learn more about or troubleshoot issues with the Azure Key Vault provider for Secrets Store CSI Driver, see the following resources:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-production-upgrade-strategies -->

# AKS production upgrade strategies

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Upgrade your production Azure Kubernetes Service (AKS) clusters safely by using these proven patterns. Each strategy is optimized for specific business constraints and risk tolerance.

## What this article covers

This article provides tested upgrade patterns for production AKS clusters and focuses on:

- Blue-green deployments for zero-downtime upgrades.
- Staged fleet upgrades across multiple environments.
- Safe Kubernetes version adoption with validation gates.
- Emergency security patching for rapid common vulnerabilities and exposures (CVE) response.
- Application resilience patterns for seamless upgrades.

These patterns are best for production environments, site reliability engineers, and platform teams that require minimal downtime and maximum safety.

For more information, see these related articles:

- To get upgrade patterns for AKS clusters with stateful workloads, see
[Stateful workload upgrade patterns](stateful-workload-upgrades). - To check for and apply basic upgrades to your AKS cluster, see
[Upgrade an Azure Kubernetes Service cluster](upgrade-aks-cluster). - To use the scenario hub to help you choose the right AKS upgrade approach, see
[AKS upgrade scenarios: Choose your path](upgrade-scenarios-hub).

For a quick start, select a link for instructions:

## Choose your strategy

| Your priority | Best pattern | Downtime | Time to complete |
|---|---|---|---|
| Zero downtime |
|

[Staged fleet upgrades](#scenario-2-stage-upgrades-across-environments)[Canary with validation](#scenario-3-safe-kubernetes-version-intake)[Automated patching](#scenario-4-fastest-security-patch-deployment)[Resilient architecture](#scenario-5-application-architecture-for-seamless-upgrades)#### Role-based quick start

| Role | Start here |
|---|---|
| Site reliability engineer/Platform |
|

[Stateful workload patterns](stateful-workload-upgrades)[Scenario 5](#scenario-5-application-architecture-for-seamless-upgrades)[Scenario 4](#scenario-4-fastest-security-patch-deployment)## Scenario 1: Minimal downtime production upgrades

**Challenge:** "I need to upgrade my production cluster with less than 2 minutes of downtime during business hours."

**Strategy:** Use blue-green deployment with intelligent traffic shifting.

To learn more, see [Blue-green deployment patterns](/en-us/azure/architecture/guide/aks/blue-green-deployment-for-aks) and [Azure Traffic Manager configuration](/en-us/azure/traffic-manager/traffic-manager-configure-weighted-routing-method).

### Quick implementation (15 minutes)

```
# 1. Create green cluster (parallel to blue)
az aks create --name myaks-green --resource-group myRG \
--kubernetes-version 1.29.0 --enable-cluster-autoscaler \
--min-count 3 --max-count 10
# 2. Deploy application to green cluster
kubectl config use-context myaks-green
kubectl apply -f ./production-manifests/
# 3. Validate green cluster
# Run your application-specific health checks here
# Examples: API endpoint tests, database connectivity, dependency checks
# 4. Switch traffic (<30-second downtime)
az network traffic-manager endpoint update \
--profile-name prod-tm --name green-endpoint --weight 100
az network traffic-manager endpoint update \
--profile-name prod-tm --name blue-endpoint --weight 0
```


** Detailed step-by-step guide**

#### Prerequisites

- Secondary cluster capacity planned.
- Application supports horizontal scaling.
- Database connections use connection pooling.
- Health checks configured (
`/health`

,`/ready`

). - Rollback procedure tested in staging.

#### Step 1: Prepare the blue-green infrastructure

```
# Create resource group for green cluster
az group create --name myRG-green --location eastus2
# Create green cluster with same configuration as blue
az aks create \
--resource-group myRG-green \
--name myaks-green \
--kubernetes-version 1.29.0 \
--node-count 3 \
--enable-cluster-autoscaler \
--min-count 3 \
--max-count 10 \
--enable-addons monitoring \
--generate-ssh-keys
```


#### Step 2: Deploy and validate the green environment

```
# Get green cluster credentials
az aks get-credentials --resource-group myRG-green --name myaks-green
# Deploy application stack
# Apply your Kubernetes manifests in order:
kubectl apply -f ./your-manifests/namespace.yaml # Create namespace
kubectl apply -f ./your-manifests/secrets/ # Deploy secrets
kubectl apply -f ./your-manifests/configmaps/ # Deploy config maps
kubectl apply -f ./your-manifests/deployments/ # Deploy applications
kubectl apply -f ./your-manifests/services/ # Deploy services
# Wait for all pods to be ready
kubectl wait --for=condition=ready pod --all --timeout=300s
# Validate application health
kubectl get pods -A
kubectl logs -l app=my-app --tail=50
```


#### Step 3: Traffic switching (critical 30-second window)

```
# Pre-switch validation
curl -f https://myapp-green.eastus2.cloudapp.azure.com/health
if [ $? -ne 0 ]; then echo "Green health check failed!"; exit 1; fi
# Execute traffic switch
az network dns record-set cname set-record \
--resource-group myRG-dns \
--zone-name mycompany.com \
--record-set-name api \
--cname myapp-green.eastus2.cloudapp.azure.com
# Immediate validation
sleep 30
curl -f https://api.mycompany.com/health
```


#### Step 4: Monitor and validate

```
# Monitor traffic and errors for 15 minutes
kubectl top nodes
kubectl top pods
kubectl logs -l app=my-app --since=15m | grep ERROR
# Check application metrics
curl https://api.mycompany.com/metrics | grep http_requests_total
```


### Common pitfalls and FAQs

**Expand for quick troubleshooting and tips**

**Domain Name System (DNS) propagation is slow:**Use low time-to-live values before upgrade, and validate the DNS cache flush.**Pods stuck terminating:**Check for finalizers, long shutdown hooks, or pod disruption budgets (PDBs) with`maxUnavailable: 0`

.**Traffic not shifting:**Validate Azure Load Balancer/Azure Traffic Manager configuration and health probes.**Rollback fails:**Always keep the blue cluster ready until the green cluster is fully validated.**Q: Can I use open-source software tools for validation?****A:**Yes. Use[kube-no-trouble](https://github.com/doitintl/kube-no-trouble)for API checks and[Trivy](https://aquasecurity.github.io/trivy/)for image scanning.

**Q: What's unique to AKS?****A:**Native integration with Traffic Manager, Azure Kubernetes Fleet Manager, and node image patching for zero-downtime upgrades.


### Advanced configuration

For applications that require <30-second downtime:

```
# Use session affinity during transition
apiVersion: v1
kind: Service
metadata:
name: my-app
spec:
sessionAffinity: ClientIP
sessionAffinityConfig:
clientIP:
timeoutSeconds: 300
```


### Success validation

To validate your progress, use the following checklist:

- Application responds within two seconds.
- No 5xx errors are in logs.
- Database connections are stable.
- User sessions are preserved.

### Emergency rollback (if needed)

```
# Immediate rollback to blue cluster
az network dns record-set cname set-record \
--resource-group myRG-dns \
--zone-name mycompany.com \
--record-set-name api \
--cname myapp-blue.eastus2.cloudapp.azure.com
```


**Expected outcome:** Less than 2-minute total downtime, zero data loss, and full rollback capability.

```
az aks create \
--resource-group production-rg \
--name aks-green-cluster \
--kubernetes-version 1.29.0 \
--node-count 3 \
--tier premium \
--auto-upgrade-channel patch \
--planned-maintenance-config ./maintenance-window.json
```


## Verify cluster readiness

```
az aks get-credentials --resource-group production-rg --name aks-green-cluster
kubectl get nodes
```


### Implementation steps

#### Step 1: Deploy the application to a green cluster

```
# Deploy application stack
kubectl apply -f ./k8s-manifests/
kubectl apply -f ./monitoring/
# Wait for all pods to be ready
kubectl wait --for=condition=ready pod --all --timeout=300s
# Validate application health
curl -f http://green-cluster-ingress/health
```


#### Step 2: Run traffic shift

```
# Update DNS or load balancer to point to green cluster
az network dns record-set a update \
--resource-group dns-rg \
--zone-name contoso.com \
--name api \
--set aRecords[0].ipv4Address="<green-cluster-ip>"
# Monitor traffic shift (should complete in 60-120 seconds)
watch kubectl top pods -n production
```


#### Step 3: Validate and clean up

```
# Verify zero errors in application logs
kubectl logs -l app=api --tail=100 | grep -i error
# Monitor key metrics for 15 minutes
kubectl get events --sort-by='.lastTimestamp' | head -20
# After validation, decommission blue cluster
az aks delete --resource-group production-rg --name aks-blue-cluster --yes
```


### Success metrics

**Downtime:**<2 minutes (DNS propagation time)**Error rate:**0% during transition**Recovery time:**<5 minutes if rollback needed

## Scenario 2: Stage upgrades across environments

**Challenge:** "I need to safely test upgrades through dev/test/production with proper validation gates."

**Strategy:** Use Azure Kubernetes Fleet Manager with staged rollouts.

To learn more, see the [Azure Kubernetes Fleet Manager overview](/en-us/azure/kubernetes-fleet/overview) and [Update orchestration](/en-us/azure/kubernetes-fleet/update-orchestration).

### Prerequisites

```
# Install Fleet extension
az extension add --name fleet
az extension update --name fleet
# Create Fleet resource
az fleet create \
--resource-group fleet-rg \
--name production-fleet \
--location eastus
```


### Implementation steps

#### Step 1: Define stage configuration

Create `upgrade-stages.json`

:

```
{
"stages": [
{
"name": "development",
"groups": [{ "name": "dev-clusters" }],
"afterStageWaitInSeconds": 1800
},
{
"name": "testing",
"groups": [{ "name": "test-clusters" }],
"afterStageWaitInSeconds": 3600
},
{
"name": "production",
"groups": [{ "name": "prod-clusters" }],
"afterStageWaitInSeconds": 0
}
]
}
```


#### Step 2: Add clusters to a fleet

```
# Add development clusters
az fleet member create \
--resource-group fleet-rg \
--fleet-name production-fleet \
--name dev-east \
--member-cluster-id "/subscriptions/.../clusters/aks-dev-east" \
--group dev-clusters
# Add test clusters
az fleet member create \
--resource-group fleet-rg \
--fleet-name production-fleet \
--name test-east \
--member-cluster-id "/subscriptions/.../clusters/aks-test-east" \
--group test-clusters
# Add production clusters
az fleet member create \
--resource-group fleet-rg \
--fleet-name production-fleet \
--name prod-east \
--member-cluster-id "/subscriptions/.../clusters/aks-prod-east" \
--group prod-clusters
```


#### Step 3: Create and run a staged update

```
# Create staged update run
az fleet updaterun create \
--resource-group fleet-rg \
--fleet-name production-fleet \
--name k8s-1-29-upgrade \
--upgrade-type Full \
--kubernetes-version 1.29.0 \
--node-image-selection Latest \
--stages upgrade-stages.json
# Start the staged rollout
az fleet updaterun start \
--resource-group fleet-rg \
--fleet-name production-fleet \
--name k8s-1-29-upgrade
```


#### Step 4: Validation gates between stages

After dev stage (30-minute soak):

```
# Run automated test suite
./scripts/run-e2e-tests.sh dev-cluster
./scripts/performance-baseline.sh dev-cluster
# Check for any regressions
kubectl get events --sort-by='.lastTimestamp' | grep -i warn
```


After test stage (60-minute soak):

```
# Extended testing with production-like load
./scripts/load-test.sh test-cluster 1000-users 15-minutes
./scripts/chaos-engineering.sh test-cluster
# Manual approval gate
echo "Approve production deployment? (y/n)"
read approval
```


### Common pitfalls and FAQs

**Expand for quick troubleshooting and tips**

**Stage fails because of quota:**Precheck regional quotas for all clusters in the fleet.**Validation scripts fail:**Ensure that test scripts are idempotent and have clear pass/fail output.**Manual approval delays:**Use automation for nonproduction. Require manual only for production.**Q: Can I use open-source software tools for validation?****A:**Yes. Integrate[Sonobuoy](https://sonobuoy.io/)for conformance and[kube-bench](https://github.com/aquasecurity/kube-bench)for security.

**Q: What's unique to AKS?****A:**Azure Kubernetes Fleet Manager enables true staged rollouts and validation gates natively.


## Scenario 3: Safe Kubernetes version intake

**Challenge:** "I need to adopt Kubernetes 1.30 without breaking existing workloads or APIs."

**Strategy:** Use multiphase validation with canary deployment.

To learn more, see [Canary deployments](/en-us/azure/architecture/reference-architectures/containers/aks-microservices/aks-microservices-advanced#deployment-strategies) and [API deprecation policies](https://kubernetes.io/docs/reference/using-api/deprecation-policy/).

### Implementation steps

#### Step 1: API deprecation analysis

```
# Install and run API deprecation scanner
kubectl apply -f https://github.com/doitintl/kube-no-trouble/releases/latest/download/knt-full.yaml
# Scan for deprecated APIs
kubectl run knt --image=doitintl/knt:latest --rm -it --restart=Never -- \
-c /kubeconfig -o json > api-deprecation-report.json
# Review and remediate findings
cat api-deprecation-report.json | jq '.[] | select(.deprecated==true)'
```


To learn more, see the [Kubernetes API deprecation guide](https://kubernetes.io/docs/reference/using-api/deprecation-guide/) and [kube-no-trouble documentation](https://github.com/doitintl/kube-no-trouble).

#### Step 2: Create a canary environment

```
# Create canary cluster with target version
az aks create \
--resource-group canary-rg \
--name aks-canary-k8s130 \
--kubernetes-version 1.30.0 \
--node-count 2 \
--tier premium \
--enable-addons monitoring
# Deploy subset of workloads
kubectl apply -f ./canary-manifests/
```


#### Step 3: Progressive workload migration

```
# Phase 1: Stateless services (20% traffic)
kubectl patch service api-service -p '{"spec":{"selector":{"version":"canary"}}}'
./scripts/monitor-error-rate.sh 15-minutes
# Phase 2: Background jobs (50% traffic)
kubectl scale deployment batch-processor --replicas=3
./scripts/validate-job-completion.sh
# Phase 3: Critical services (100% traffic)
kubectl patch deployment critical-api -p '{"spec":{"template":{"metadata":{"labels":{"cluster":"canary"}}}}}'
```


#### Step 4: Feature gate validation

```
# Test new Kubernetes 1.30 features
apiVersion: v1
kind: ConfigMap
metadata:
name: feature-validation
data:
test-script: |
# Test new security features
kubectl auth can-i create pods --as=service-account:default:test-sa
# Validate performance improvements
kubectl top nodes --use-protocol-buffers=true
# Check new API versions
kubectl api-versions | grep "v1.30"
```


### Success metrics

**API compatibility:**100% (zero breaking changes)**Performance:**≤5% regression in key metrics**Feature adoption:**New features validated in canary

## Scenario 4: Fastest security patch deployment

**Challenge:** "A critical CVE was announced. I need patches deployed across all clusters within 4 hours."

**Strategy:** Use automated node image patching with minimal disruption.

To learn more, see [Node image upgrade strategies](node-image-upgrade), [Auto-upgrade channels](auto-upgrade-cluster), and [Security patching best practices](/en-us/azure/aks/operator-best-practices-cluster-security).

### Implementation steps

#### Step 1: Emergency response preparation

```
# Set up automated monitoring for security updates
az aks nodepool update \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--auto-upgrade-channel SecurityPatch
# Configure maintenance window for emergency patches
az aks maintenance-configuration create \
--resource-group production-rg \
--cluster-name aks-prod \
--config-name emergency-security \
--week-index First,Second,Third,Fourth \
--day-of-week Monday,Tuesday,Wednesday,Thursday,Friday \
--start-hour 0 \
--duration 4
```


To learn more, see [Planned maintenance configuration](planned-maintenance) and [Autoupgrade channels](auto-upgrade-cluster#cluster-autoupgrade-channels).

#### Step 2: Automated security scanning

```
# security-scan-cronjob.yaml
apiVersion: batch/v1
kind: CronJob
metadata:
name: security-scanner
spec:
schedule: "0 */6 * * *" # Every 6 hours
jobTemplate:
spec:
template:
spec:
containers:
- name: scanner
image: aquasec/trivy:latest
command:
- trivy
- k8s
- --report
- summary
- cluster
```


#### Step 3: Rapid patch deployment

```
# Trigger immediate node image upgrade for security patches
az aks nodepool upgrade \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--node-image-only \
--max-surge 50% \
--drain-timeout 5
# Monitor patch deployment
watch az aks nodepool show \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--query "upgradeSettings"
```


#### Step 4: Compliance validation

```
# Verify patch installation
kubectl get nodes -o wide
kubectl describe node | grep "Kernel Version"
# Generate compliance report
./scripts/generate-security-report.sh > security-compliance-$(date +%Y%m%d).json
# Notify security team
curl -X POST "$SLACK_WEBHOOK" -d "{\"text\":\"Security patches deployed to production cluster. Compliance report attached.\"}"
```


### Success metrics

**Deployment time:**<4 hours from common vulnerabilities and exposures announcement**Coverage:**100% of nodes patched**Downtime:**<5 minutes per node pool

## Scenario 5: Application architecture for seamless upgrades

**Challenge:** "I want my applications to handle cluster upgrades gracefully without affecting users."

**Strategy:** Use resilient application patterns with graceful degradation.

To learn more, see [Application reliability patterns](/en-us/azure/architecture/framework/resiliency/reliability-patterns), [Pod disruption budgets](https://kubernetes.io/docs/tasks/run-application/configure-pdb/), and [Health check best practices](/en-us/azure/architecture/patterns/health-endpoint-monitoring).

### Implementation steps

#### Step 1: Implement robust health checks

```
# robust-health-checks.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
name: resilient-api
spec:
replicas: 3
template:
spec:
containers:
- name: api
image: myapp:latest
readinessProbe:
httpGet:
path: /health/ready
port: 8080
initialDelaySeconds: 10
periodSeconds: 5
timeoutSeconds: 3
successThreshold: 1
failureThreshold: 3
livenessProbe:
httpGet:
path: /health/live
port: 8080
initialDelaySeconds: 30
periodSeconds: 10
timeoutSeconds: 5
failureThreshold: 3
lifecycle:
preStop:
exec:
command: ["/bin/sh", "-c", "sleep 15"]
```


#### Step 2: Configure pod disruption budgets

```
# optimal-pdb.yaml
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
name: api-pdb
spec:
selector:
matchLabels:
app: api
maxUnavailable: 1
# Ensures at least 2 pods remain available during upgrades
---
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
name: database-pdb
spec:
selector:
matchLabels:
app: database
minAvailable: 2
# Critical: Always keep majority of database pods running
```


#### Step 3: Implement a circuit breaker pattern

```
// circuit-breaker.js
const CircuitBreaker = require('opossum');
const options = {
timeout: 3000,
errorThresholdPercentage: 50,
resetTimeout: 30000,
fallback: () => 'Service temporarily unavailable'
};
const breaker = new CircuitBreaker(callExternalService, options);
// Monitor circuit breaker state during upgrades
breaker.on('open', () => console.log('Circuit breaker opened'));
breaker.on('halfOpen', () => console.log('Circuit breaker half-open'));
```


To learn more, see [Circuit breaker pattern](/en-us/azure/architecture/patterns/circuit-breaker), [Retry pattern](/en-us/azure/architecture/patterns/retry), and [Application resilience](/en-us/azure/well-architected/reliability/).

#### Step 4: Database connection resilience

```
# connection-pool-config.yaml
apiVersion: v1
kind: ConfigMap
metadata:
name: db-config
data:
database.yml: |
production:
adapter: postgresql
pool: 25
timeout: 5000
retry_attempts: 3
retry_delay: 1000
connection_validation: true
validation_query: "SELECT 1"
test_on_borrow: true
```


### Success metrics

**Error rate:**<0.01% during upgrades**Response time:**<10% degradation**Recovery time:**<30 seconds after node replacement

## Monitoring and alerting setup

To learn more, see the [AKS monitoring overview](monitor-aks), [Container Insights](/en-us/azure/azure-monitor/containers/container-insights-overview), and [Prometheus metrics](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview).

### Essential metrics to monitor

```
# upgrade-monitoring.yaml
apiVersion: monitoring.coreos.com/v1
kind: PrometheusRule
metadata:
name: upgrade-monitoring
spec:
groups:
- name: upgrade.rules
rules:
- alert: UpgradeInProgress
expr: kube_node_spec_unschedulable > 0
for: 1m
annotations:
summary: "Node upgrade in progress"
- alert: HighErrorRate
expr: rate(http_requests_total{status=~"5.."}[5m]) > 0.01
for: 2m
annotations:
summary: "High error rate during upgrade"
- alert: PodEvictionFailed
expr: increase(kube_pod_container_status_restarts_total[5m]) > 5
for: 1m
annotations:
summary: "Multiple pod restarts detected"
```


### Dashboard configuration

```
{
"dashboard": {
"title": "AKS Upgrade Dashboard",
"panels": [
{
"title": "Upgrade Progress",
"targets":
[
"kube_node_info",
"kube_node_status_condition"
]
},
{
"title": "Application Health",
"targets":
[
"up{job='kubernetes-pods'}",
"http_request_duration_seconds"
]
}
]
}
}
```


## Troubleshooting guide

To learn more, see the [AKS troubleshooting guide](/en-us/azure/aks/troubleshooting), [Node and pod troubleshooting](node-access), and [Upgrade error messages](upgrade-aks-cluster#troubleshoot-aks-cluster-upgrade-error-messages).

### Common issues and solutions

| Issue | Symptoms | Solution |
|---|---|---|
| Stuck node drain | Pods won't evict. | Check PDB configuration, increase drain timeout. |
| High error rates | 5xx responses are increasing. | Verify health checks, check resource limits. |
| Slow upgrades | Takes >2 hours. | Increase `maxSurge` , optimize container startup. |
| DNS resolution | Service discovery is failing. | Verify `CoreDNS` pods, check service endpoints. |

### Emergency rollback procedures

```
# Quick rollback script
#!/bin/bash
echo "Initiating emergency rollback..."
# Switch traffic back to previous cluster
az network traffic-manager endpoint update \
--resource-group traffic-rg \
--profile-name production-tm \
--name current-endpoint \
--target-resource-id "/subscriptions/.../clusters/aks-previous"
# Verify rollback success
curl -f https://api.production.com/health
echo "Rollback completed in $(date)"
```


## Related resources

### Specialized scenarios

[Stateful workloads](stateful-workload-upgrades): Use PostgreSQL, Redis, and MongoDB upgrade patterns.[Upgrade scenarios hub](upgrade-scenarios-hub): Choose your upgrade path.[Basic AKS upgrades](upgrade-aks-cluster): Find simple cluster version upgrades.

### Supporting tools

[Auto-upgrade configuration](auto-upgrade-cluster): Use automated upgrade channels.[Maintenance windows](planned-maintenance): Schedule upgrade windows.[Upgrade monitoring](aks-communication-manager): Use real-time upgrade alerts.

### Best practices

[Cluster reliability](best-practices-app-cluster-reliability): Design for upgrades.[Security guidelines](operator-best-practices-cluster-security): Use secure upgrade practices.[Support policies](support-policies): Understand upgrade support windows.

## Next tasks

**Set up monitoring:**Configure[upgrade notifications](aks-communication-manager)before your first upgrade.**Practice safely:**Test scenarios in staging by using[cluster snapshots](node-pool-snapshot).**Automate gradually:**Start with[auto-upgrade channels](auto-upgrade-cluster)for nonproduction.**Handle stateful data:**Review[stateful workload patterns](stateful-workload-upgrades)if you run databases.

## Related content

- For more help, see
[AKS support options](aks-support-help)or review[common upgrade scenarios](upgrade-cluster#common-upgrade-scenarios-and-recommendations).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-gateway-api -->

# Configure Istio ingress with the Kubernetes Gateway API for Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

The Istio service mesh add-on supports both [Istio's own ingress traffic management API](istio-deploy-ingress) and the Kubernetes Gateway API for ingress traffic management. You can use the Istio Gateway API [automated deployment model](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#automated-deployment) or the [manual deployment model](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#manual-deployment). This article describes how to configure ingress traffic management for the Istio service mesh add-on using the Kubernetes Gateway API with the [automated deployment model](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#automated-deployment).

## Limitations and considerations

- Using the Kubernetes Gateway API for
[egress traffic management](istio-deploy-egress)with the Istio service mesh add-on is only supported for the[manual deployment model](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#manual-deployment). - ConfigMap customizations for
`Gateway`

resources must fall within the Resource customization allow list. Fields not on the allow list are disallowed and blocked via add-on managed webhooks. For more information, see the[Istio service mesh add-on support policy](istio-support-policy#allowed-supported-and-blocked-customizations).

## Prerequisites

- Enable the
[Managed Gateway API](managed-gateway-api)on your AKS cluster. - Install the Istio service mesh add-on revision
`asm-1-26`

or higher. Follow the[installation guide](istio-deploy-addon)if you don't have the Istio service mesh add-on installed yet, or the[upgrade guide](istio-upgrade)if you're on a lower minor revision.

## Set environment variables

Set the following environment variables to use throughout this article:

| Variable | Description |
|---|---|
`RESOURCE_GROUP` |
The name of the resource group containing your AKS cluster. |
`CLUSTER_NAME` |
The name of your AKS cluster. |
`LOCATION` |
The Azure region where your AKS cluster is deployed. |
`KEY_VAULT_NAME` |
The name of the Azure Key Vault resource to be created for storing TLS secrets. If you have an existing resource, use that name. |

## Deploy sample application

Deploy the sample

`httpbin`

application in the`default`

namespace using thecommand.`kubectl apply`

`kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.26/samples/httpbin/httpbin.yaml`


## Create Kubernetes Gateway and HTTPRoute

The example manifest creates an external ingress load balancer service that's accessible from outside the cluster. You can add [annotations](#annotation-customizations) to create an internal load balancer and customize other load balancer settings.

Deploy a Gateway API configuration in the

`default`

namespace with the`gatewayClassName`

set to`istio`

and an`HTTPRoute`

that routes traffic to the`httpbin`

service using the following manifest:`kubectl apply -f - <<EOF apiVersion: gateway.networking.k8s.io/v1 kind: Gateway metadata: name: httpbin-gateway spec: gatewayClassName: istio listeners: - name: http port: 80 protocol: HTTP allowedRoutes: namespaces: from: Same --- apiVersion: gateway.networking.k8s.io/v1 kind: HTTPRoute metadata: name: http namespace: default spec: parentRefs: - name: httpbin-gateway hostnames: ["httpbin.example.com"] rules: - matches: - path: type: PathPrefix value: /get backendRefs: - name: httpbin port: 8000 EOF`

Note

If you're performing a

[minor revision upgrade](istio-upgrade)and have two Istio service mesh add-on revisions installed on your cluster simultaneously, the control plane for the higher minor revision takes ownership of the`Gateways`

by default. You can add the`istio.io/rev`

label to the`Gateway`

to control which control plane revision owns it. If you add the revision label, make sure that you update it accordingly to the appropriate control plane revision before rolling back or completing the upgrade operation.

## Verify resource creation

Verify the

`Deployment`

,`Service`

,`HorizontalPodAutoscaler`

, and`PodDisruptionBudget`

resources were created using the following`kubectl get`

commands:`kubectl get deployment httpbin-gateway-istio kubectl get service httpbin-gateway-istio kubectl get hpa httpbin-gateway-istio kubectl get pdb httpbin-gateway-istio`

Example output:

`# Deployment resource NAME READY UP-TO-DATE AVAILABLE AGE httpbin-gateway-istio 2/2 2 2 31m # Service resource NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE httpbin-gateway-istio LoadBalancer 10.0.65.45 <external-ip> 15021:32053/TCP,80:31587/TCP 33m # HPA resource NAME REFERENCE TARGETS MINPODS MAXPODS REPLICAS AGE httpbin-gateway-istio Deployment/httpbin-gateway-istio cpu: 3%/80% 2 5 3 34m # PDB resource NAME MIN AVAILABLE MAX UNAVAILABLE ALLOWED DISRUPTIONS AGE httpbin-gateway-istio 1 N/A 2 36m`


## Send request to sample application

Try sending a

`curl`

request to the`httpbin`

application. First, set the`INGRESS_HOST`

environment variable:`kubectl wait --for=condition=programmed gateways.gateway.networking.k8s.io httpbin-gateway export INGRESS_HOST=$(kubectl get gateways.gateway.networking.k8s.io httpbin-gateway -ojsonpath='{.status.addresses[0].value}')`

Try sending an HTTP request to

`httpbin`

.`curl -s -I -HHost:httpbin.example.com "http://$INGRESS_HOST/get"`

In the output, you should see an

`HTTP 200`

response.

## Secure Istio ingress traffic with the Kubernetes Gateway API

The Istio service mesh add-on supports syncing secrets from Azure Key Vault for securing Gateway API-based ingress traffic with [Transport Layer Security (TLS) termination](https://istio.io/latest/docs/tasks/traffic-management/ingress/secure-ingress/) or [Server Name Indication (SNI) passthrough](https://istio.io/latest/docs/tasks/traffic-management/ingress/ingress-sni-passthrough/). In the following sections, you sync secrets from Azure Key Vault onto your AKS cluster using the [Azure Key Vault provider for Secrets Store Container Storage Interface (CSI) Driver add-on](csi-secrets-store-driver) and terminate TLS at the ingress gateway.

## Create client/server certificates and keys

Create a root certificate and private key for signing the certificates for sample services:

`mkdir httpbin_certs openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -subj '/O=example Inc./CN=example.com' -keyout httpbin_certs/example.com.key -out httpbin_certs/example.com.crt`

Generate a certificate and a private key for

`httpbin.example.com`

:`openssl req -out httpbin_certs/httpbin.example.com.csr -newkey rsa:2048 -nodes -keyout httpbin_certs/httpbin.example.com.key -subj "/CN=httpbin.example.com/O=httpbin organization" openssl x509 -req -sha256 -days 365 -CA httpbin_certs/example.com.crt -CAkey httpbin_certs/example.com.key -set_serial 0 -in httpbin_certs/httpbin.example.com.csr -out httpbin_certs/httpbin.example.com.crt`


## Set up Azure Key Vault and create secrets

Create an Azure Key Vault instance to supply the certificate and key inputs to the Istio service mesh add-on using the

command. If you already have an Azure Key Vault instance, you can skip this step.`az keyvault create`

`az keyvault create --name $KEY_VAULT_NAME --resource-group $RESOURCE_GROUP --location $LOCATION`

Enable the

[Azure Key Vault provider for Secrets Store (CSI) Driver add-on](csi-secrets-store-driver)on your cluster using thecommand.`az aks enable-addons`

`az aks enable-addons --addons azure-keyvault-secrets-provider --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`

If your key vault uses Azure role-based access control (RBAC) for the permissions model, follow the instructions in

[Provide access to Azure Key Vault keys, certificates, and secrets with Azure role-based access control](/en-us/azure/key-vault/general/rbac-guide)to assign an Azure role of*Key Vault Secrets User*for the add-on's user-assigned managed identity. Alternatively, if your key vault uses the vault access policy permissions model, authorize the user-assigned managed identity of the add-on to access Azure Key Vault resource using access policy using thecommand.`az keyvault set-policy`

`OBJECT_ID=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query 'addonProfiles.azureKeyvaultSecretsProvider.identity.objectId' -o tsv | tr -d '\r') CLIENT_ID=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query 'addonProfiles.azureKeyvaultSecretsProvider.identity.clientId') TENANT_ID=$(az keyvault show --resource-group $RESOURCE_GROUP --name $KEY_VAULT_NAME --query 'properties.tenantId') az keyvault set-policy --name $KEY_VAULT_NAME --object-id $OBJECT_ID --secret-permissions get list`

Create secrets in Azure Key Vault using the certificates and keys using the following

commands:`az keyvault secret set`

`az keyvault secret set --vault-name $KEY_VAULT_NAME --name test-httpbin-key --file httpbin_certs/httpbin.example.com.key az keyvault secret set --vault-name $KEY_VAULT_NAME --name test-httpbin-crt --file httpbin_certs/httpbin.example.com.crt`


## Deploy SecretProviderClass and sample pod

Deploy the SecretProviderClass to provide Azure Key Vault specific parameters to the CSI driver using the following manifest. In this example,

`test-httpbin-key`

and`test-httpbin-crt`

are the names of the secret objects in Azure Key Vault.`cat <<EOF | kubectl apply -f - apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: httpbin-credential-spc spec: provider: azure secretObjects: - secretName: httpbin-credential type: kubernetes.io/tls data: - objectName: test-httpbin-key key: tls.key - objectName: test-httpbin-crt key: tls.crt parameters: useVMManagedIdentity: "true" userAssignedIdentityID: $CLIENT_ID keyvaultName: $KEY_VAULT_NAME cloudName: "" objects: | array: - | objectName: test-httpbin-key objectType: secret objectAlias: "test-httpbin-key" - | objectName: test-httpbin-crt objectType: secret objectAlias: "test-httpbin-crt" tenantId: $TENANT_ID EOF`

Note

Alternatively, to reference a certificate object type directly from Azure Key Vault, use the following manifest to deploy SecretProviderClass. In this example,

`test-httpbin-cert-pxf`

is the name of the certificate object in Azure Key Vault.`cat <<EOF | kubectl apply -f - apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: httpbin-credential-spc spec: provider: azure secretObjects: - secretName: httpbin-credential type: kubernetes.io/tls data: - objectName: test-httpbin-key key: tls.key - objectName: test-httpbin-crt key: tls.crt parameters: useVMManagedIdentity: "true" userAssignedIdentityID: $CLIENT_ID keyvaultName: $KEY_VAULT_NAME cloudName: "" objects: | array: - | objectName: test-httpbin-cert-pfx #certificate object name from keyvault objectType: secret objectAlias: "test-httpbin-key" - | objectName: test-httpbin-cert-pfx #certificate object name from keyvault objectType: cert objectAlias: "test-httpbin-crt" tenantId: $TENANT_ID EOF`

Deploy a sample pod using the following manifest. The Azure Key Vault provider for Secrets Store (CSI) Driver add-on requires a pod to reference the SecretProviderClass resource to ensure secrets sync from Azure Key Vault to the cluster.

`cat <<EOF | kubectl apply -f - apiVersion: v1 kind: Pod metadata: name: secrets-store-sync-httpbin spec: containers: - name: busybox image: mcr.microsoft.com/oss/busybox/busybox:1.33.1 command: - "/bin/sleep" - "10" volumeMounts: - name: secrets-store01-inline mountPath: "/mnt/secrets-store" readOnly: true volumes: - name: secrets-store01-inline csi: driver: secrets-store.csi.k8s.io readOnly: true volumeAttributes: secretProviderClass: "httpbin-credential-spc" EOF`


## Verify TLS secret creation

Verify the

`httpbin-credential`

secret was created in the`default`

namespace as defined in the SecretProviderClass resource using the`kubectl describe secret`

command.`kubectl describe secret/httpbin-credential`

Example output:

`Name: httpbin-credential Namespace: default Labels: secrets-store.csi.k8s.io/managed=true Annotations: <none> Type: kubernetes.io/tls Data ==== tls.crt: 1180 bytes tls.key: 1675 bytes`


## Deploy TLS Gateway

Create a Kubernetes Gateway that references the

`httpbin-credential`

secret under the TLS configuration using the following manifest:`cat <<EOF | kubectl apply -f - apiVersion: gateway.networking.k8s.io/v1 kind: Gateway metadata: name: httpbin-gateway spec: gatewayClassName: istio listeners: - name: https hostname: "httpbin.example.com" port: 443 protocol: HTTPS tls: mode: Terminate certificateRefs: - name: httpbin-credential allowedRoutes: namespaces: from: Selector selector: matchLabels: kubernetes.io/metadata.name: default EOF`

Note

In the gateway definition,

`tls.certificateRefs.name`

must match the`secretName`

in SecretProviderClass resource.Create a corresponding

`HTTPRoute`

to configure ingress traffic routing to the`httpbin`

service over HTTPS using the following manifest:`cat <<EOF | kubectl apply -f - apiVersion: gateway.networking.k8s.io/v1 kind: HTTPRoute metadata: name: httpbin spec: parentRefs: - name: httpbin-gateway hostnames: ["httpbin.example.com"] rules: - matches: - path: type: PathPrefix value: /status - path: type: PathPrefix value: /delay backendRefs: - name: httpbin port: 8000 EOF`

Get the ingress gateway's external IP address and secure port using the following commands:

`kubectl wait --for=condition=programmed gateways.gateway.networking.k8s.io httpbin-gateway export INGRESS_HOST=$(kubectl get gateways.gateway.networking.k8s.io httpbin-gateway -o jsonpath='{.status.addresses[0].value}') export SECURE_INGRESS_PORT=$(kubectl get gateways.gateway.networking.k8s.io httpbin-gateway -o jsonpath='{.spec.listeners[?(@.name=="https")].port}')`

Send an HTTPS request to access the

`httpbin`

service:`curl -v -HHost:httpbin.example.com --resolve "httpbin.example.com:$SECURE_INGRESS_PORT:$INGRESS_HOST" \ --cacert httpbin_certs/example.com.crt "https://httpbin.example.com:$SECURE_INGRESS_PORT/status/418"`

The output should show the

`httpbin`

service return the*418 I’m a Teapot*code.Note

To configure HTTPS ingress access to an HTTPS service, update the TLS mode in the gateway definition to

`Passthrough`

. This configuration instructs the gateway to pass the ingress traffic*as is*, without terminating TLS.

## Annotation customizations

You can add annotations under `spec.infrastructure.annotations`

to [configure load balancer settings](configure-load-balancer-standard#customizations-via-kubernetes-annotations) for the `Gateway`

. For instance, to create an internal load balancer attached to a specific subnet, you can create a `Gateway`

with the following annotations:

```
spec:
# ... existing spec content ...
infrastructure:
annotations:
service.beta.kubernetes.io/azure-load-balancer-internal: "true"
service.beta.kubernetes.io/azure-load-balancer-internal-subnet: "my-subnet"
```


## ConfigMap customizations

The Istio service mesh add-on supports [customizations of the resources](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#automated-deployment) generated for the `Gateways`

, including:

- Service
- Deployment
- Horizontal Pod Autoscaler (HPA)
- Pod Disruption Budget (PDB)

The [default settings for these resources](https://istio.io/latest/docs/tasks/traffic-management/ingress/gateway-api/#gatewayclass-defaults) are set in the `istio-gateway-class-defaults`

ConfigMap in the `aks-istio-system`

namespace. This ConfigMap must have the `gateway.istio.io/defaults-for-class`

label set to `istio`

for the customizations to take effect for all `Gateways`

with `spec.gatewayClassName: istio`

. The `GatewayClass`

-level ConfigMap is installed by default in the `aks-istio-system`

namespace when the [Managed Gateway API installation](managed-gateway-api) is enabled. It could take up to five minutes for the `istio-gateway-class-defaults`

ConfigMap to get deployed after installing the Managed Gateway API CRDs.

```
kubectl get configmap istio-gateway-class-defaults -n aks-istio-system -o yaml
```


```
...
data:
horizontalPodAutoscaler: |
spec:
minReplicas: 2
maxReplicas: 5
podDisruptionBudget: |
spec:
minAvailable: 1
...
```


You can modify these settings for all Istio `Gateways`

at a `GatewayClass`

level by updating the `istio-gateway-class-defaults`

ConfigMap, or you can set them for individual `Gateway`

resources. For both the `GatewayClass`

-level and `Gateway`

-level `ConfigMaps`

, you must add fields to the allow list for the given resource. If there are customizations both for the `GatewayClass`

and an individual `Gateway`

, the `Gateway`

-level configuration takes precedence.

## Deployment customization allow list fields

| Field path | Description |
|---|---|
`metadata.labels` |
Deployment labels |
`metadata.annotations` |
Deployment annotations |
`spec.replicas` |
Deployment replica count |
`spec.template.metadata.labels` |
Pod labels |
`spec.template.metadata.annotations` |
Pod annotations |
`spec.template.spec.affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms` |
Node affinity |
`spec.template.spec.affinity.nodeAffinity.preferredDuringSchedulingIgnoredDuringExecution` |
Node affinity |
`spec.template.spec.affinity.podAffinity.requiredDuringSchedulingIgnoredDuringExecution` |
Pod affinity |
`spec.template.spec.affinity.podAffinity.preferredDuringSchedulingIgnoredDuringExecution` |
Pod affinity |
`spec.template.spec.affinity.podAntiAffinity.requiredDuringSchedulingIgnoredDuringExecution` |
Pod anti-affinity |
`spec.template.spec.affinity.podAntiAffinity.preferredDuringSchedulingIgnoredDuringExecution` |
Pod anti-affinity |
`spec.template.spec.containers.resizePolicy` |
Container resource utilization |
`spec.template.spec.containers.resources.limits` |
Container resource utilization |
`spec.template.spec.containers.resources.requests` |
Container resource utilization |
`spec.template.spec.containers.stdin` |
Container debugging |
`spec.template.spec.containers.stdinOnce` |
Container debugging |
`spec.template.spec.nodeSelector` |
Pod scheduling |
`spec.template.spec.nodeName` |
Pod scheduling |
`spec.template.spec.tolerations` |
Pod scheduling |
`spec.template.spec.topologySpreadConstraints` |
Pod scheduling |

## Service customization allow list fields

| Field path | Description |
|---|---|
`metadata.labels` |
Service labels |
`metadata.annotations` |
Service annotations |
`spec.type` |
Service type |
`spec.loadBalancerSourceRanges` |
Service load balancer settings |
`spec.loadBalancerClass` |
Service load balancer settings |
`spec.externalTrafficPolicy` |
Service traffic policy |
`spec.internalTrafficPolicy` |
Service traffic policy |

## HorizontalPodAutoscaler (HPA) customization allow list fields

| Field path | Description |
|---|---|
`metadata.labels` |
HPA labels |
`metadata.annotations` |
HPA annotations |
`spec.behavior.scaleUp.stabilizationWindowSeconds` |
HPA scale-up behavior |
`spec.behavior.scaleUp.selectPolicy` |
HPA scale-up behavior |
`spec.behavior.scaleUp.policies` |
HPA scale-up behavior |
`spec.behavior.scaleDown.stabilizationWindowSeconds` |
HPA scale-down behavior |
`spec.behavior.scaleDown.selectPolicy` |
HPA scale-down behavior |
`spec.behavior.scaleDown.policies` |
HPA scale-down behavior |
`spec.metrics` |
HPA scaling resource metrics |
`spec.minReplicas` |
HPA minimum replica count. Must not be below 2. |
`spec.maxReplicas` |
HPA maximum replica count |

## PodDisruptionBudget (PDB) customization allow list fields

| Field path | Description |
|---|---|
`metadata.labels` |
PDB labels |
`metadata.annotations` |
PDB annotations |
`spec.minAvailable` |
PDB minimum availability |
`spec.unhealthyPodEvictionPolicy` |
PDB eviction policy |

Note

Modifying the `PDB`

minimum availability and eviction policy can lead to potential errors during cluster/node upgrade and deletion operations. Follow the [PDB troubleshooting guide](/en-us/troubleshoot/azure/azure-kubernetes/create-upgrade-delete/error-code-poddrainfailure) to address *UpgradeFailed* errors due to `PDB`

eviction failures.

## Configure GatewayClass-level settings

Update the

`GatewayClass`

-level ConfigMap in the`aks-istio-system`

namespace using the`kubectl edit configmap`

command:`kubectl edit cm istio-gateway-class-defaults -n aks-istio-system`

Edit the resource settings in the

`data`

section as needed. For example, to update the HPA min/max replicas and add a label to the`Deployment`

, modify the ConfigMap as follows:`... data: deployment: | metadata: labels: test.azureservicemesh.io/deployment-config: "updated" horizontalPodAutoscaler: | spec: minReplicas: 3 maxReplicas: 6 podDisruptionBudget: | spec: minAvailable: 1 ...`

Note

Only one ConfigMap per

`GatewayClass`

is allowed.Now, you should see the

`HPA`

for`httpbin-gateway`

that you created earlier get updated with the new min/max values. Verify the`HPA`

settings using the`kubectl get hpa`

command.`kubectl get hpa httpbin-gateway-istio`

Example output:

`NAME REFERENCE TARGETS MINPODS MAXPODS REPLICAS AGE httpbin-gateway-istio Deployment/httpbin-gateway-istio cpu: 3%/80% 3 6 3 36m`

Verify the

`Deployment`

is updated with the new label using the`kubectl get deployment`

command.`kubectl get deployment httpbin-gateway-istio -ojsonpath='{.metadata.labels.test\.azureservicemesh\.io\/deployment-config}'`

Example output:

`updated`


## Configure settings for a specific gateway

Create a ConfigMap with resource customizations for the

`httpbin`

Gateway using the following manifest:`kubectl apply -f - <<EOF apiVersion: v1 kind: ConfigMap metadata: name: gw-options data: horizontalPodAutoscaler: | spec: minReplicas: 2 maxReplicas: 4 deployment: | metadata: labels: test.azureservicemesh.io/deployment-config: "updated-per-gateway" EOF`

Update the

`httpbin`

`Gateway`

to reference the ConfigMap:`spec: # ... existing spec content ... infrastructure: parametersRef: group: "" kind: ConfigMap name: gw-options`

Apply the update using the

`kubectl apply`

command.`kubectl apply -f httpbin-gateway-updated.yaml`

Verify the

`HPA`

is updated with the new min/max values using the`kubectl get hpa`

command. If you also configured the`GatewayClass`

-level ConfigMap, the`Gateway`

-level settings should take precedence.`kubectl get hpa httpbin-gateway-istio`

Example output:

`NAME REFERENCE TARGETS MINPODS MAXPODS REPLICAS AGE httpbin-gateway-istio Deployment/httpbin-gateway-istio cpu: 3%/80% 2 4 2 4h14m`

Inspect the

`Deployment`

labels to ensure that the`test.azureservicemesh.io/deployment-config`

is updated to the new value using the`kubectl get deployment`

command.`kubectl get deployment httpbin-gateway-istio -ojsonpath='{.metadata.labels.test\.azureservicemesh\.io\/deployment-config}'`

Example output:

`updated-per-gateway`


## Clean up resources

If you no longer need the resources created in this article, you can delete them to avoid incurring any charges.

Delete the Gateway and HTTPRoute resources using the following

`kubectl delete`

commands:`kubectl delete gateways.gateway.networking.k8s.io httpbin-gateway kubectl delete httproute httpbin`

If you created a ConfigMap to customize your Gateway resources, delete it using the

`kubectl delete configmap`

command.`kubectl delete configmap gw-options`

If you created a SecretProviderClass and secret to use for TLS termination delete the resources using the following

`kubectl delete`

commands:`kubectl delete secret httpbin-credential kubectl delete pod secrets-store-sync-httpbin kubectl delete secretproviderclass httpbin-credential-spc`

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-windows-gpu -->

# Use Windows GPUs for compute-intensive workloads on Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Graphical processing units (GPUs) are often used for compute-intensive workloads, such as graphics and visualization workloads. AKS supports GPU-enabled Windows and [Linux](gpu-cluster) node pools to run compute-intensive Kubernetes workloads.

This article helps you provision Windows nodes with schedulable GPUs on new and existing AKS clusters (preview).

## Supported GPU-enabled virtual machines (VMs)

To view supported GPU-enabled VMs, see [GPU-optimized VM sizes in Azure](/en-us/azure/virtual-machines/sizes-gpu). For AKS node pools, we recommend a minimum size of *Standard_NC6s_v3*. The NVv4 series (based on AMD GPUs) aren't supported on AKS.

Note

GPU-enabled VMs contain specialized hardware subject to higher pricing and region availability. For more information, see the [pricing](https://azure.microsoft.com/pricing/) tool and [region availability](https://azure.microsoft.com/global-infrastructure/services/).

## Limitations

- Updating an existing Windows node pool to add GPU isn't supported.
- Not supported on Kubernetes version 1.28 and below.

## Before you begin

- This article assumes you have an existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-windows-container-deploy-cli),[Azure PowerShell](learn/quick-windows-container-deploy-powershell), or the[Azure portal](learn/quick-windows-container-deploy-portal). - You need the Azure CLI version 2.72.2 or later installed and configured to use the
`--gpu-driver`

field with the`az aks nodepool add`

command. Run`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you have the
`aks-preview`

Azure CLI extension installed, please update the version to 18.0.0b2 or later.

## Get the credentials for your cluster

Get the credentials for your AKS cluster using the

command. The following example command gets the credentials for the`az aks get-credentials`

*myAKSCluster*in the*myResourceGroup*resource group:`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Using Windows GPU with automatic driver installation

Using NVIDIA GPUs involves the installation of various NVIDIA software components such as the [DirectX device plugin for Kubernetes](https://github.com/aarnaud/k8s-directx-device-plugin), GPU driver installation, and more. When you create a Windows node pool with a supported GPU-enabled VM, these components and the appropriate NVIDIA CUDA or GRID drivers are installed. For NC and ND series VM sizes, the CUDA driver is installed. For NV series VM sizes, the GRID driver is installed.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

### Install the `aks-preview`

Azure CLI extension

Register or update the aks-preview extension using the

or`az extension add`

command.`az extension update`

`# Register the aks-preview extension az extension add --name aks-preview # Update the aks-preview extension az extension update --name aks-preview`


### Register the `WindowsGPUPreview`

feature flag

Register the

`WindowsGPUPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "WindowsGPUPreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "WindowsGPUPreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Create a Windows GPU-enabled node pool (preview)

To create a Windows GPU-enabled node pool, you need to use a supported GPU-enabled VM size and specify the `os-type`

as `Windows`

. The default Windows `os-sku`

is `Windows2022`

, but all Windows `os-sku`

options are supported.

Create a Windows GPU-enabled node pool using the

command.`az aks nodepool add`

`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name gpunp \ --node-count 1 \ --os-type Windows \ --kubernetes-version 1.29.0 \ --node-vm-size Standard_NC6s_v3`

Check that your

[GPUs are schedulable](#confirm-that-gpus-are-schedulable).Once you confirm that your GPUs are schedulable, you can run your GPU workload.


#### Specify GPU Driver Type (preview)

By default, AKS specifies a default GPU driver type for each supported GPU-enabled VM. Because workload and driver compatibility are important for functioning GPU workloads, you can specify the driver type for your Windows GPU node. This feature is not supported for Linux GPU node pools.

When creating a Windows agent pool with GPU support, you have the option to specify the type of GPU driver using the `--driver-type`

flag.

The available options are:

- GRID: For applications requiring virtualization support.
- CUDA: Optimized for computational tasks in scientific computing and data-intensive applications.

Note

When you set the `--driver-type`

flag, you assume responsibility for ensuring that the selected driver type is compatible with the specific VM size and configuration of your node pool. While AKS attempts to validate compatibility, there are scenarios where the node pool creation might fail due to incompatibilities between the specified driver type and the underlying VM or hardware.

To create a Windows GPU-enabled node pool with a specific GPU Driver type, use the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) command.

```
az aks nodepool add \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name gpunp \
--node-count 1 \
--os-type Windows \
--kubernetes-version 1.29.0 \
--node-vm-size Standard_NC6s_v3 \
--driver-type GRID
```


For example, the above command creates a GPU-enabled node pool using the `GRID`

GPU driver type. Selecting this driver type overrides the default of `CUDA`

driver type for NC series VM skus.

## Using Windows GPU with manual driver installation

When creating a Windows node pool with N-series (NVIDIA GPU) VM sizes in AKS, the GPU driver and Kubernetes DirectX device plugin are installed automatically. To bypass this automatic installation, use the following steps:

[Skip GPU driver installation](#skip-gpu-driver-installation)by setting the configuration`--gpu-driver none`

at node pool create time.[Manual installation of the Kubernetes DirectX device plugin](#manually-install-the-kubernetes-directx-device-plugin).

### Skip GPU driver installation

AKS has automatic GPU driver installation enabled by default. In some cases, such as installing your own drivers, you may want to skip GPU driver installation.

Important

Starting on **August 14, 2025**, Azure Kubernetes Service (AKS) no longer supports the `--skip-gpu-driver-install`

node pool tag. After this date, you'll be unable to provision GPU-enabled node pools using this tag to bypass automatic GPU driver installation. You can achieve the same behavior by setting the `--gpu-driver`

field to `none`

. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4925) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=496440). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Create a node pool using the

command and setting the API field`az aks nodepool add`

`--gpu-driver`

to`none`

to skip automatic GPU driver installation.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name gpunp \ --node-count 1 \ --os-type windows \ --os-sku windows2022 \ --gpu-driver none`


Note

If the `--node-vm-size`

that you're using isn't yet onboarded on AKS, you can't use GPUs and the `--gpu-driver`

field doesn't work.

### Manually install the Kubernetes DirectX device plugin

You can deploy a DaemonSet for the Kubernetes DirectX device plugin, which runs a pod on each node to provide the required drivers for the GPUs.

Add a node pool to your cluster using the

command.`az aks nodepool add`

`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name gpunp \ --node-count 1 \ --os-type windows \ --os-sku windows2022`


## Create a namespace and deploy the Kubernetes DirectX device plugin

Create a namespace using the

command.`kubectl create namespace`

`kubectl create namespace gpu-resources`

Create a file named

*k8s-directx-device-plugin.yaml*and paste the following YAML manifest provided as part of the[NVIDIA device plugin for Kubernetes project](https://github.com/NVIDIA/k8s-device-plugin):`apiVersion: apps/v1 kind: DaemonSet metadata: name: nvidia-device-plugin-daemonset namespace: gpu-resources spec: selector: matchLabels: name: nvidia-device-plugin-ds updateStrategy: type: RollingUpdate template: metadata: # Mark this pod as a critical add-on; when enabled, the critical add-on scheduler # reserves resources for critical add-on pods so that they can be rescheduled after # a failure. This annotation works in tandem with the toleration below. annotations: scheduler.alpha.kubernetes.io/critical-pod: "" labels: name: nvidia-device-plugin-ds spec: tolerations: # Allow this pod to be rescheduled while the node is in "critical add-ons only" mode. # This, along with the annotation above marks this pod as a critical add-on. - key: CriticalAddonsOnly operator: Exists - key: nvidia.com/gpu operator: Exists effect: NoSchedule - key: "sku" operator: "Equal" value: "gpu" effect: "NoSchedule" containers: - image: mcr.microsoft.com/aks/aks-windows-gpu-device-plugin:0.0.17 name: nvidia-device-plugin-ctr securityContext: allowPrivilegeEscalation: false capabilities: drop: ["ALL"] volumeMounts: - name: device-plugin mountPath: /var/lib/kubelet/device-plugins volumes: - name: device-plugin hostPath: path: /var/lib/kubelet/device-plugins`

Create the DaemonSet and confirm the NVIDIA device plugin is created successfully using the

command.`kubectl apply`

`kubectl apply -f nvidia-device-plugin-ds.yaml`

Now that you successfully installed the NVIDIA device plugin, you can check that your

[GPUs are schedulable](#confirm-that-gpus-are-schedulable).

## Confirm that GPUs are schedulable

After creating your cluster, confirm that GPUs are schedulable in Kubernetes.

List the nodes in your cluster using the

command.`kubectl get nodes`

`kubectl get nodes`

Your output should look similar to the following example output:

`NAME STATUS ROLES AGE VERSION aks-gpunp-28993262-0 Ready agent 13m v1.20.7`

Confirm the GPUs are schedulable using the

command.`kubectl describe node`

`kubectl describe node aks-gpunp-28993262-0`

Under the

*Capacity*section, the GPU should list as`microsoft.com/directx: 1`

. Your output should look similar to the following condensed example output:`Capacity: [...] microsoft.com.directx/gpu: 1 [...]`


## Clean up resources

Remove the associated Kubernetes objects you created in this article using the

command.`kubectl delete job`

`kubectl delete jobs windows-gpu-workload`


## Next steps

- To run Apache Spark jobs, see
[Run Apache Spark jobs on AKS](spark-job). - For more information on features of the Kubernetes scheduler, see
[Best practices for advanced scheduler features in AKS](operator-best-practices-advanced-scheduler). - For more information on Azure Kubernetes Service and Azure Machine Learning, see:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-aks-node-pools-rolling -->

# Configure rolling upgrades for Azure Kubernetes Service (AKS) node pools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

A rolling upgrade strategy upgrades nodes one at a time (or a few at a time), minimizing workload disruption while ensuring the node pool remains available throughout the upgrade process. This article explains how to configure rolling upgrades for AKS node pools, including surge settings, drain timeout, and soak time.

## Before you begin

- Ensure your control plane is already upgraded to the target Kubernetes version. You can't upgrade node pools to a version higher than the control plane. For more information, see
[Upgrade the AKS cluster control plane](upgrade-aks-control-plane). - If you're using the Azure CLI, this article requires Azure CLI version 2.34.1 or later. Use the
`az --version`

command to find the version. If you need to install or upgrade, see [Install Azure CLI][azure-cli-install]. - You need the
`Microsoft.ContainerService/managedClusters/agentPools/write`

RBAC role permission to configure rolling upgrades for AKS node pools.

## Overview of rolling upgrade behavior

During a rolling upgrade, AKS performs the following operations for each node in the node pool:

**Add surge nodes**: Add new buffer nodes based on max surge (`--max-surge`

) settings to maintain capacity during the upgrade.**Cordon and drain nodes**:[Cordon and drain](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/)the old nodes one at a time to minimize disruption to running applications. If you're using max surge, it cordons and drains as many nodes at the same time as the number of buffer nodes specified.**Wait for soak time**(optional): Wait for a configured[soak duration](#set-node-soak-time-value)before proceeding to allow workloads to stabilize on the new nodes before continuing the upgrade.**Reimage old nodes**: When the old nodes are drained, they're reimaged to receive the new version. The reimaged nodes become the buffer nodes for the next set of nodes to be upgraded.**Repeat**: The process repeats until all nodes in the node pool are upgraded.**Remove surge nodes**: After all nodes are upgraded, any remaining buffer nodes are removed, maintaining the original node pool size and balance.

## Configure rolling upgrade settings

### Customize node surge

Important

- Node surges require subscription quota for the requested max surge count for each upgrade operation. For example, a cluster that has five node pools, each with a count of four nodes, has a total of 20 nodes. If each node pool has a max surge value of 50%, extra compute and IP quota of 10 nodes (
*two*nodes ×*five*pools) is required to complete the upgrade. - The max surge setting on a node pool is persistent. Subsequent Kubernetes upgrades or node version upgrades use this setting. You can change the max surge value for your node pools at any time. For production node pools, we recommend a max surge setting of 33%.
- If you're using Azure CNI, validate there are available IPs in the subnet to
[satisfy IP requirements of Azure CNI](configure-azure-cni).

AKS configures upgrades to surge with one extra node by default. A default value of *one* for the max surge setting enables AKS to minimize workload disruption by creating an extra node before the cordon/drain of existing applications to replace an older versioned node. You can customize the max surge value per node pool. When you increase the max surge value, the upgrade process completes faster, but you might experience more disruptions during the upgrade process.

For example, a max surge value of `100%`

provides the fastest possible upgrade process but also causes all nodes in the node pool to be drained simultaneously. You might want to use a higher value like this for testing environments. For production node pools, we recommend a max surge setting of `33%`

.

AKS accepts both integer values and a percentage value for max surge. For example:

| Value type | Example | Description |
|---|---|---|
| Integer | `5` |
Five extra nodes to surge |
| Percentage | `50%` |
Surge value of half the current node count in the pool |

Max surge percent values can be a minimum of `1%`

and a maximum of `100%`

. A percent value is rounded up to the nearest node count. If the max surge value is higher than the required number of nodes to be upgraded, the number of nodes to be upgraded is used for the max surge value.

#### Set max surge value

Set max surge values for new or existing node pools using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) or

[command with the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)

`az aks nodepool update`

`--max-surge`

parameter. For example:```
# Set max surge for a new node pool
az aks nodepool add \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 33%
# Update max surge for an existing node pool
az aks nodepool update \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 5
```


### Customize unavailable nodes

Important

- You must set max surge to
`0`

in order to set a max unavailable value. The two values can't both be active at the same time. - Max unavailable doesn't create surge nodes during the upgrade process. Instead, AKS cordons
*n*nodes (the max unavailable value) at a time and evicts the pods to other nodes in the agent pool. This might cause workload disruptions if the pods can't be scheduled. - Max unavailable might cause more failures due to unsatisfied Pod Disruption Budgets (PDBs) since there are fewer resources for pods to be scheduled on. For more information, see
[Troubleshooting for Pod Disruption Budgets](/en-us/troubleshoot/azure/azure-kubernetes/create-upgrade-delete/error-code-poddrainfailure). - You can't set max unavailable on system node pools.

AKS can also configure upgrades to not use a surge node and upgrade the nodes in place. The max unavailable value determines how many nodes can be simultaneously cordoned and drained from the existing node pool nodes.

AKS accepts both integer values and a percentage value for max unavailable. For example:

| Value type | Example | Description |
|---|---|---|
| Integer | `5` |
Five nodes are cordoned from the existing nodes |
| Percentage | `50%` |
Half the current node count in the pool will be unavailable |

Max unavailable percent values can be a minimum of `1%`

and a maximum of `100%`

. A percent value is rounded up to the nearest node count.

#### Set max unavailable value

Set max unavailable values for new or existing node pools using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add),

[, or the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)

`az aks nodepool update`

[command with the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-upgrade)

`az aks nodepool upgrade`

`--max-unavailable`

parameter. For example:```
# Set max unavailable for a new node pool
az aks nodepool add \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 0 \
--max-unavailable 5
# Update max unavailable for an existing node pool
az aks nodepool update \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 0 \
--max-unavailable 5
# Set max unavailable at upgrade time
az aks nodepool upgrade \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 0 \
--max-unavailable 5
```


### Customize node drain timeout

You might have long-running workloads on certain pods that you can't reschedule to another node during runtime. For example, a memory-intensive stateful workload that must finish running. In these cases, you can configure a node drain timeout that AKS respects in the upgrade workflow.

The default node drain timeout value is 30 minutes. Node drain timeout values can be a minimum of 5 minutes and a maximum of 24 hours.

If the drain timeout value elapses and pods are still running, the upgrade operation stops. Any subsequent `PUT`

operation resumes the stopped upgrade.

Tip

For long-running pods, you should also configure the [ terminationGracePeriodSeconds](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/) in your pod spec.

#### Set node drain timeout value

Set node drain timeout (in minutes) for new or existing node pools using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) or

[command with the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)

`az aks nodepool update`

`--drain-time-out`

parameter.```
# Set drain timeout for a new node pool
az aks nodepool add \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--drain-time-out 100
# Update drain timeout for an existing node pool
az aks nodepool update \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--drain-time-out 45
```


### Customize node soak time

To enable a waiting period for a specified duration of time between draining a node and proceeding to reimage it and move on to the next node, you can set the soak time. This soak time gives you the opportunity to perform other tasks during the upgrade process, such as checking application health from a monitoring dashboard.

The default node soak time is 0 minutes. Node soak time values can be a minimum of 0 minutes and a maximum of 30 minutes. We recommend keeping soak time as short as reasonably possible. A higher node soak time increases the total upgrade duration and delays discovery of issues.

#### Set node soak time value

Set node soak time (in minutes) for new or existing node pools using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add),

[, or](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)

`az aks nodepool update`

[command with the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-upgrade)

`az aks nodepool upgrade`

`--node-soak-duration`

flag.```
# Set node soak time for a new node pool
az aks nodepool add \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--node-soak-duration 10
# Update node soak time for an existing node pool
az aks nodepool update \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 33% \
--node-soak-duration 5
# Set node soak time when upgrading an existing node pool
az aks nodepool upgrade \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 33% \
--node-soak-duration 20
```


## View AKS node upgrade events

View upgrade events using the `kubectl get events`

command to monitor the rolling upgrade progress.

```
kubectl get events --field-selector reason=Drain,reason=Surge,reason=Upgrade
```


Example output during an upgrade event:

```
default 2m1s Normal Drain node/aks-nodepool1-12345678-vmss000001 Draining node: [aks-nodepool1-12345678-vmss000001]
default 9m22s Normal Surge node/aks-nodepool1-12345678-vmss000002 Created a surge node [aks-nodepool1-12345678-vmss000002 nodepool1] for agentpool nodepool1
default 1m45s Normal Upgrade node/aks-nodepool1-12345678-vmss000001 Soak duration 5m0s after draining node: aks-nodepool1-12345678-vmss000001
```


## Recommended AKS node pool upgrade settings for production workloads

The following table outlines recommended node pool upgrade settings for production workloads:

| Setting | Recommendation |
|---|---|
Max surge |
Set to 33% for production node pools |
Drain timeout |
Configure based on your longest-running pod's requirements |
Soak time |
Use a short duration (0-5 minutes) unless you need manual verification |
Pod Disruption Budgets |
Configure PDBs for critical workloads to control pod eviction |
Upgrade order |
Upgrade non-production node pools first to validate the new version |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-upgrade-image -->

# Node image updates for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of node image updates for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS), including how it works, recommended maintenance windows, and examples to get started.

## How do node image updates work for node auto-provisioning nodes?

By default, NAP node pool virtual machines (VMs) are automatically updated when a new image version is available. You can configure an [AKS-managed node operating system (OS) upgrade schedule maintenance window](#node-os-upgrade-maintenance-windows-for-nap) to control when new images are picked up and applied to your NAP nodes, or [use Karpenter Node Disruption Budgets and Pod Disruption Budgets](#karpenter-node-disruption-budgets-and-pod-disruption-budgets-for-nap) to control how and when disruption occurs during upgrades.

Note

NAP forces the latest image version to be picked up if the existing node image version is older than 90 days. This bypasses any existing maintenance window.

## Node OS upgrade maintenance windows for NAP

You can use the [AKS planned maintenance feature](planned-maintenance) with a [node OS auto-upgrade channel](auto-upgrade-node-os-image) to configure a `aksManagedNodeOSUpgradeSchedule`

maintenance window that controls when to perform node OS security patching scheduled by your designated node OS auto-upgrade channel.

### Node OS upgrade maintenance window behavior and considerations

Keep the following information in mind when configuring a node OS upgrade maintenance window for NAP:

- The
`aksManagedNodeOSUpgradeSchedule`

maintenance configuration determines the window during which NAP picks up a new image. This configuration doesn't necessarily determine when existing nodes are disrupted. - The upgrade mechanism and decision criteria are specific to NAP/Karpenter and are evaluated by NAP's drift logic. NAP respects Karpenter Node Disruption Budgets and Pod Disruption Budgets. For more information about drift, see the
[Karpenter drift documentation](https://karpenter.sh/docs/concepts/disruption/#drift). - These NAP upgrade decisions are separate from the cluster
`NodeImage`

and`SecurityPatch`

channels. However, the`aksManagedNodeOSUpgradeSchedule`

maintenance configuration applies them as well. - We recommend using a maintenance window of four hours or more for reliable operation.
- If no maintenance configuration exists, AKS might use a fallback schedule to pick up new images, which can cause images to be picked up at unexpected times. You can avoid unexpected timing of new images and upgrades by defining an explicit
`aksManagedNodeOSUpgradeSchedule`

. - Allow at least 30 minutes between creating or updating a maintenance configuration and the scheduled start time to ensure AKS has time to reconcile the new configuration.

### Recommended schedule pattern for NAP-managed nodes

We recommend the following schedule pattern for NAP-managed nodes:

**Weekly cadence**: Recommended for routine node image roll outs (for example:*Every week on Sunday*).

## Create a node OS maintenance schedule example

The following sections show you how to create a weekly maintenance window for NAP-managed nodes using the Azure CLI and a JSON configuration file and how to update, view, list, and delete the maintenance configuration.

### Create a maintenance configuration

Create a JSON file named

`nodeosMaintenance.json`

with a weekly maintenance window (for example:*Sunday at 01:00 UTC for 4 hours*).`{ "properties": { "maintenanceWindow": { "durationHours": 4, "schedule": { "weekly": { "intervalWeeks": 1, "dayOfWeek": "Sunday" } }, "startDate": "2025-01-01", "startTime": "01:00", "utcOffset": "+00:00" } } }`

Add the maintenance configuration to your cluster using the

command.`az aks maintenanceconfiguration add`

`az aks maintenanceconfiguration add \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --name aksManagedNodeOSUpgradeSchedule \ --config-file ./nodeosMaintenance.json`


### Update, view, list, or delete a maintenance configuration

You can use the following commands to update, view, list, or delete a maintenance configuration for NAP-managed nodes:

Update a maintenance configuration by modifying the JSON file and then running the

command.`az aks maintenanceconfiguration update`

`az aks maintenanceconfiguration update \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --name aksManagedNodeOSUpgradeSchedule \ --config-file ./nodeosMaintenance.json`

View the details of a maintenance configuration using the

command.`az aks maintenanceconfiguration show`

`az aks maintenanceconfiguration show \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --name aksManagedNodeOSUpgradeSchedule`

List all maintenance configurations for your cluster using the

command.`az aks maintenanceconfiguration list`

`az aks maintenanceconfiguration list \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME`

Delete a maintenance configuration using the

command.`az aks maintenanceconfiguration delete`

`az aks maintenanceconfiguration delete \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --name aksManagedNodeOSUpgradeSchedule`


For complete details, examples, and advanced scenarios, see [Use Planned Maintenance to schedule maintenance windows for your AKS cluster](planned-maintenance).

## Karpenter Node Disruption Budgets and Pod Disruption Budgets for NAP

For more information on configuring Karpenter Node Disruption Budgets and Pod Disruption Budgets for NAP, see the following resources from the official Karpenter documentation:

## Next steps

For more information on node auto-provisioning in AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/generation-2-vm -->

# Use Generation 2 (Gen 2) virtual machines (VMs) on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to use Generation 2 (Gen 2) virtual machines (VMs) on Azure Kubernetes Service (AKS), including how to check available Gen 2 VM sizes, create AKS node pools with Gen 2 VMs, migrate from Gen 1 to Gen 2 VMs on AKS, and verify the VM generation of your AKS nodes.

## Before you begin

- Review the
[Virtual machine (VM) sizes, generations, and features for Azure Kubernetes Service (AKS)](aks-virtual-machine-sizes)article to understand VM generations and features supported on AKS.

## Check available Gen 2 VM sizes

Check available Gen 2 VM sizes using the [ az vm list-skus](/en-us/cli/azure/vm#az-vm-list-skus) command.

```
# Set environment variables
export LOCATION=<your-region>
export VM_SIZE=<vm-size-to-check>
# Check if the VM size is available in the specified location
az vm list-skus --location $LOCATION --size $VM_SIZE --output table
```


For a breakdown of what VM sizes support Gen 2, see [Support for Gen 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2).

## Create a node pool with a Gen 2 VM

By default, Linux uses the Gen 2 node image unless the VM size doesn't support Gen 2.

Create a Linux node pool with a Gen 2 VM using the default [node pool creation](create-node-pools) process.

## Migrate an existing node pool to Gen 2

If you're using a VM size that only supports Gen 1, you can update your node pool to a VM size that supports Gen 2 using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command. This update changes your node image from Gen 1 to Gen 2.

```
# Set environment variables
export RESOURCE_GROUP=<resource-group-name>
export CLUSTER_NAME=<cluster-name>
export NODE_POOL_NAME=<node-pool-name>
export VM_SIZE=<supported-generation-2-vm-size>
# Update a Linux node pool to use a Gen 2 VM
az aks nodepool update --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name $NODE_POOL_NAME --node-vm-size $VM_SIZE --os-type Linux
```


## Check if you're using a Gen 2 node image

Verify a successful node pool creation using the [ az aks nodepool show](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-show) command and check that the

`nodeImageVersion`

contains `gen2`

in the output.```
# Set environment variables
export RESOURCE_GROUP=<resource-group-name>
export CLUSTER_NAME=<cluster-name>
export NODE_POOL_NAME=<node-pool-name>
# Show node pool details
az aks nodepool show --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name $NODE_POOL_NAME --output table
```


## Next steps

- To learn more about Gen 2 VMs, see
[Support for Generation 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2) - To learn more about supported Gen 2 node images, see
[Node images](node-images)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/generation-2-vms -->

# Use Generation 2 (Gen 2) virtual machines (VMs) on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to use Generation 2 (Gen 2) virtual machines (VMs) on Azure Kubernetes Service (AKS), including how to check available Gen 2 VM sizes, create AKS node pools with Gen 2 VMs, migrate from Gen 1 to Gen 2 VMs on AKS, and verify the VM generation of your AKS nodes.

## Before you begin

- Review the
[Virtual machine (VM) sizes, generations, and features for Azure Kubernetes Service (AKS)](aks-virtual-machine-sizes)article to understand VM generations and features supported on AKS.

## Check available Gen 2 VM sizes

Check available Gen 2 VM sizes using the [ az vm list-skus](/en-us/cli/azure/vm#az-vm-list-skus) command.

```
# Set environment variables
export LOCATION=<your-region>
export VM_SIZE=<vm-size-to-check>
# Check if the VM size is available in the specified location
az vm list-skus --location $LOCATION --size $VM_SIZE --output table
```


For a breakdown of what VM sizes support Gen 2, see [Support for Gen 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2).

## Create a node pool with a Gen 2 VM

By default, Linux uses the Gen 2 node image unless the VM size doesn't support Gen 2.

Create a Linux node pool with a Gen 2 VM using the default [node pool creation](create-node-pools) process.

## Migrate an existing node pool to Gen 2

If you're using a VM size that only supports Gen 1, you can update your node pool to a VM size that supports Gen 2 using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command. This update changes your node image from Gen 1 to Gen 2.

```
# Set environment variables
export RESOURCE_GROUP=<resource-group-name>
export CLUSTER_NAME=<cluster-name>
export NODE_POOL_NAME=<node-pool-name>
export VM_SIZE=<supported-generation-2-vm-size>
# Update a Linux node pool to use a Gen 2 VM
az aks nodepool update --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name $NODE_POOL_NAME --node-vm-size $VM_SIZE --os-type Linux
```


## Check if you're using a Gen 2 node image

Verify a successful node pool creation using the [ az aks nodepool show](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-show) command and check that the

`nodeImageVersion`

contains `gen2`

in the output.```
# Set environment variables
export RESOURCE_GROUP=<resource-group-name>
export CLUSTER_NAME=<cluster-name>
export NODE_POOL_NAME=<node-pool-name>
# Show node pool details
az aks nodepool show --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name $NODE_POOL_NAME --output table
```


## Next steps

- To learn more about Gen 2 VMs, see
[Support for Generation 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2) - To learn more about supported Gen 2 node images, see
[Node images](node-images)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-vulnerability-management -->

# Vulnerability management for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Vulnerability management involves detecting, assessing, mitigating, and reporting on any security vulnerabilities that exist in an organization's systems and software. Vulnerability management is a shared responsibility between you and Microsoft.

This article describes how Microsoft manages security vulnerabilities and security updates (also referred to as patches), for Azure Kubernetes Service (AKS) clusters.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## How vulnerabilities are discovered

Microsoft identifies and patches vulnerabilities and missing security updates for the following components:

AKS Container Images

Ubuntu operating system 18.04 and 22.04 worker nodes: Canonical provides Microsoft with OS builds that have all available security updates applied.

Windows Server 2022 OS worker nodes: The Windows Server operating system is patched on the second Tuesday of every month. SLAs should be the same as per their support contract and severity.

Azure Linux OS Nodes: Azure Linux provides AKS with OS builds that have all available security updates applied.


## AKS Container Images

While the [Cloud Native Computing Foundation](https://www.cncf.io/) (CNCF) owns and maintains most of the code AKS runs, Microsoft takes responsibility for building the open-source packages we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, as well as control over the binaries in container images. Having responsibility for building the open-source packages deployed on AKS enables us to establish a software supply chain over the binary, and to patch the software as needed.

Microsoft is active in the broader Kubernetes ecosystem to help build the future of cloud-native compute in the wider CNCF community. This work not only ensures the quality of every Kubernetes release for the world, but also enables AKS quickly get new Kubernetes releases out into production for several years. In some cases, ahead of other cloud providers by several months. Microsoft collaborates with other industry partners in the Kubernetes security organization. For example, the Security Response Committee (SRC) receives, prioritizes, and patches embargoed security vulnerabilities before they're announced to the public. This commitment ensures Kubernetes is secure for everyone, and enables AKS to patch and respond to vulnerabilities faster to keep our customers safe. In addition to Kubernetes, Microsoft has signed up to receive pre-release notifications for software vulnerabilities for products such as Envoy, container runtimes, and many other open-source projects.

Microsoft scans container images using static analysis to discover vulnerabilities and missing updates in Kubernetes and Microsoft-managed containers. If fixes are available, the scanner automatically begins the update and release process.

In addition to automated scanning, Microsoft discovers and updates vulnerabilities unknown to scanners in the following ways:

Microsoft performs its own audits, penetration testing, and vulnerability discovery across all AKS platforms. Specialized teams inside Microsoft and trusted third-party security vendors conduct their own attack research.

Microsoft actively engages with the security research community through multiple vulnerability reward programs. A dedicated

[Microsoft Azure Bounty program](https://www.microsoft.com/msrc/bounty-microsoft-azure)provides significant bounties for the best cloud vulnerability found each year.Microsoft collaborates with other industry and open source software partners who share vulnerabilities, security research, and updates before the public release of the vulnerability. The goal of this collaboration is to update large pieces of Internet infrastructure before the vulnerability is announced to the public. In some cases, Microsoft contributes vulnerabilities found to this community.

Microsoft's security collaboration happens on many levels. Sometimes it occurs formally through programs where organizations sign up to receive pre-release notifications about software vulnerabilities for products such as Kubernetes and Docker. Collaboration also happens informally due to our engagement with many open source projects such as the Linux kernel, container runtimes, virtualization technology, and others.


## Worker Nodes

### Linux nodes

The nightly canonical OS security updates are turned off by default in AKS. In order to enable them explicitly, use the `unmanaged`

[channel](node-image-upgrade).

If you are using the `unmanaged`

[channel](node-image-upgrade), then nightly canonical security updates are applied to the OS on the node. The node image used to create nodes for your cluster remains unchanged. If a new Linux node is added to your cluster, the original image is used to create the node. This new node receives all the security and kernel updates available during the automatic assessment performed every night, but remains unpatched until all checks and restarts are complete. You can use node image upgrade to check for and update node images used by your cluster. For more information on node image upgrade, see [Azure Kubernetes Service (AKS) node image upgrade](node-image-upgrade).

For AKS clusters using a [channel](node-image-upgrade) other than `unmanaged`

, the unattended upgrade process is disabled.

### Windows Server nodes

For Windows Server nodes, Windows Update doesn't automatically run and apply the latest updates. Schedule Windows Server node pool upgrades in your AKS cluster around the regular Windows Update release cycle and your own update management process. This upgrade process creates nodes that run the latest Windows Server image and patches, then removes the older nodes. For more information on this process, see [Upgrade a node pool in AKS](manage-node-pools#upgrade-a-single-node-pool).

## How vulnerabilities are classified

Microsoft makes large investments in security hardening the entire stack, including the OS, container, Kubernetes, and network layers, in addition to setting good defaults and providing security-hardened configurations and managed components. Combined, these efforts help to reduce the impact and likelihood of vulnerabilities.

The AKS team classifies vulnerabilities according to the Kubernetes vulnerability scoring system. Classifications consider many factors including AKS configuration and security hardening. As a result of this approach, and the investments AKS make in security, AKS vulnerability classifications might differ from other classification sources.

The following table describes vulnerability severity categories:

| Severity | Description |
|---|---|
| Critical | A vulnerability easily exploitable in all clusters by an unauthenticated remote attacker that leads to full system compromise. |
| High | A vulnerability easily exploitable for many clusters that leads to loss of confidentiality, integrity, or availability. |
| Medium | A vulnerability exploitable for some clusters where loss of confidentiality, integrity, or availability is limited by common configurations, difficulty of the exploit itself, required access, or user interaction. |
| Low | All other vulnerabilities. Exploitation is unlikely or consequences of exploitation are limited. |

## How vulnerabilities are updated

AKS patches Common Vulnerabilities and Exposures (CVEs) that have a *vendor fix* every week. Any CVEs without a fix are waiting on a vendor fix before they can be remediated. The fixed container images are cached in the next corresponding virtual hard disk (VHD) build, which also contains the updated Ubuntu/Azure Linux/Windows patched CVEs. As long as you're running the updated VHD, you shouldn't be running any container image CVEs with a vendor fix that is over 30 days old.

For the OS-based vulnerabilities in the VHD, AKS also relies on node image vhd updates by default, so any security updates will come with weekly node image releases. Unattended upgrades is disabled unless you switch to unmanaged which is not recommended as its release is global.

## Update release timelines

Microsoft's goal is to mitigate detected vulnerabilities within a time period appropriate for the risks they represent. The [Microsoft Azure FedRAMP High](/en-us/azure/azure-government/compliance/azure-services-in-fedramp-auditscope#azure-government-services-by-audit-scope) Provisional Authorization to Operate (P-ATO) includes AKS in audit scope and has been authorized. FedRAMP Continuous Monitoring Strategy Guide and the FedRAMP Low, Moderate, and High Security Control baselines requires remediation of known vulnerabilities within a specific time period according to their severity level. As specified in FedRAMP RA-5d.

## How vulnerabilities and updates are communicated

In general, Microsoft doesn't broadly communicate the release of new patch versions for AKS. However, Microsoft constantly monitors and validates available CVE patches to support them in AKS in a timely manner. If a critical patch is found or user action is required, Microsoft [posts and updates CVE issue details on GitHub](https://github.com/Azure/AKS/issues?q=is%3Aissue+is%3Aopen+cve).

## Security Reporting

You can report a security issue to the Microsoft Security Response Center (MSRC), by [creating a vulnerability report](https://aka.ms/opensource/security/create-report).

If you prefer to submit a report without logging in to the tool, send email to [secure@microsoft.com](mailto:secure@microsoft.com). If possible, encrypt your message with our PGP key by downloading it from the [Microsoft Security Response Center PGP Key page](https://aka.ms/opensource/security/pgpkey).

You should receive a response within 24 hours. If for some reason you don't, follow up with an email to ensure we received your original message. For more information, go to the [Microsoft Security Response Center](https://aka.ms/opensource/security/msrc).

Include the following requested information (as much as you can provide) to help us better understand the nature and scope of the possible issue:

- Type of issue (for example, buffer overflow, SQL injection, cross-site scripting, etc.)
- Full paths of source file(s) related to the manifestation of the issue
- The location of the affected source code (tag/branch/commit or direct URL)
- Any special configuration required to reproduce the issue
- Step-by-step instructions to reproduce the issue
- Proof-of-concept or exploit code (if possible)
- Impact of the issue, including how an attacker might exploit the issue

This information helps us triage your reported security issue quicker.

If you're reporting for a bug bounty, more complete reports can contribute to a higher bounty award. For more information about our active programs, see [Microsoft Bug Bounty Program](https://aka.ms/opensource/security/bounty).

### Policy

Microsoft follows the principle of [Coordinated Vulnerability Disclosure](https://aka.ms/opensource/security/cvd).

## Next steps

See the overview about [Upgrading Azure Kubernetes Service clusters and node pools](upgrade).
