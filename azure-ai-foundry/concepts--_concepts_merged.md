---
merged_at: 2026-01-26T23:20:36.746281
merged_files: 35
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/concept-synthetic-data -->

# Synthetic data generation in Microsoft Foundry portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

In Microsoft Foundry portal, you can use synthetic data generation to efficiently produce predictions for your datasets. This article introduces you to the concept of synthetic data generation and how you can use it in machine learning.

## What is synthetic data generation?

Synthetic data generation involves creating artificial data that mimics the statistical properties of real-world data. This data is generated through algorithms and machine learning techniques. You can use the data in various ways, such as computer simulations or modeling real-world events.

## Benefits

In machine learning, synthetic data is valuable for:

**Data augmentation**: It helps in expanding the size of training datasets, which is crucial for training robust machine learning models. This expansion technique is especially useful when real-world data is scarce or expensive to obtain.**Testing and validation**: It allows for extensive testing and validation of machine learning models under various scenarios without the need for real-world data.

## Sample notebook

To see how to generate synthetic data, you can use the [sample notebook](https://aka.ms/meta-llama-3.1-datagen).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/management-center -->

# Management center overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

The management center is part of the Microsoft Foundry portal that streamlines governance and management activities. From the management center, you can manage:

Foundry hubs and hub-based projects

Azure AI Foundry projects

Quotas for models and virtual machines (VMs)

Note

VMs and VM quotas are only available for hub-based projects.

User management and role assignment


To access the management center, sign in to [Foundry](https://ai.azure.com/?cid=learnDocs), select a project, and then select **Management center** from the bottom of the left menu. (You might have to scroll down to find it.)


## Manage Foundry projects

Use the management center to create and configure Foundry projects. Use **All resources** to view all Foundry projects that you have access to, or to create new projects. Use the **Project** section (Project = Foundry project) of the left menu to manage and create individual Foundry projects on the Foundry resource.

For more information, see [Create a Foundry project](../how-to/create-projects?view=foundry-classic).

### Manage Foundry hubs and hub-based projects

You can also manage hub-based projects from the management center. The management center lists them in the **All resources** section. When you select a hub, the portal displays it in the left menu.

For more information, see [Create a hub-based project](../how-to/hub-create-projects?view=foundry-classic).

## Manage resource utilization

View and manage quotas and usage metrics across multiple projects and Azure subscriptions. Use the **Quota** link from the left menu to view and manage quotas. VM quotas apply to hub-based projects only.

For more information, see [Manage and increase quotas for resources](../how-to/quota?view=foundry-classic).

## Govern access

With a project selected, use the **Users** entry in the left menu to view and manage users and their roles.

Note

You can only assign built-in roles for Foundry here.

For more information, see [Role-based access control](rbac-foundry?view=foundry-classic#built-in-roles).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/resource-types -->

# Choose an Azure resource type for Foundry

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

Microsoft Foundry portal and SDK clients support multiple Azure resource types, each designed for different development and operational needs. This article helps you choose the right resource type for your AI development scenario.

## Resource types supported with Foundry portal and SDK clients

**Foundry**– An Azure resource that scopes design, deployment, governance, and runtime access for generative AI applications and agents, including agent service, Microsoft‑ and partner‑provided models, evaluations, Foundry Tools, and Azure OpenAI–compatible APIs. It is the default resource type for projects built in the Foundry portal.[Create your first Foundry resource](../../ai-services/multi-service-resource?view=foundry-classic&toc=/azure/ai-foundry/toc.json&bc=/azure/ai-foundry/breadcrumb/toc.json).**Azure AI Search**– A resource you use to index and retrieve data for grounding AI applications. You can[connect](../how-to/connections-add?view=foundry-classic)it to Foundry agents to enable retrieval-augmented generation (RAG) and semantic search experiences.**Azure OpenAI**– A specialized resource type that provides access to OpenAI models and APIs only. For most use cases, use the Foundry resource, which offers backward compatibility with all Azure OpenAI APIs.Note

If your IT security team doesn't enable the superset of Foundry capabilities in your environment, you might need the standalone Azure OpenAI resource.

[An upgrade option from Azure OpenAI to Foundry](../how-to/upgrade-azure-openai?view=foundry-classic)is available to access all Foundry capabilities and models while keeping your existing Azure OpenAI API endpoint, state of work, and security configurations.

**Azure AI Hub**- In June 2025, Microsoft started to move most of Hub's capabilities under "Foundry" resource type. This change brings agents, models, and their tools together for development, management and governance, under a dedicated Azure resource type for Foundry.New features primarily land on Foundry resource type. To learn more, see

[migrate from hub-based to Foundry projects](../how-to/migrate-project?view=foundry-classic).[Select use cases](../what-is-foundry?view=foundry-classic#which-type-of-project-do-i-need), including open source model deployments, currently still require a hub resource.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/hub-encryption-keys-portal -->

# Customer-managed keys for hub projects

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

This article provides legacy support for hub-based projects. It will not work for **Foundry projects**. See [How do I know which type of project I have?](../what-is-foundry?view=foundry-classic#how-do-i-know-which-type-of-project-i-have)

**SDK compatibility note**: Code examples require a specific Microsoft Foundry SDK version. If you encounter compatibility issues, consider [migrating from a hub-based to a Foundry project](../how-to/migrate-project?view=foundry-classic).

Tip

An alternate Foundry project article is available: [Customer-managed keys for encryption with Microsoft Foundry (Foundry projects)](encryption-keys-portal?view=foundry-classic).

Hub-based projects require configuring CMK on each underlying service (Azure AI Hub, Storage) for end-to-end encryption control.

## Architecture

Azure AI Hub resource acts as a gateway to multiple Azure services. Configure CMK per service:

- Azure AI Hub / hub project (Machine Learning workspace) – see ML data encryption docs.
- Foundry resources – AES-256 FIPS 140-2 compliant.
- Azure Storage accounts – store uploaded data (configure CMK in Storage).

## Data storage options

Two options when using CMK with hubs:

- Service-side encrypted data stored in Microsoft subscription (recommended). Document-level CMK, dedicated per-customer Azure AI Search instance for isolation.
- Legacy managed resource group in your subscription (Cosmos DB, Storage, Azure AI Search). Backward compatibility only.

Managed resource group naming: `azureml-rg-hubworkspacename_GUID`

. Deleted when hub deleted.

### Managed resource data

| Service | Use | Example |
|---|---|---|
| Azure Cosmos DB | Metadata for projects/tools | Flow creation timestamps |
| Azure AI Search | Indices for querying content | Index of model deployment names |
| Azure Storage | Orchestration instructions | JSON flow representations |

## Key Vault usage

Store CMKs in Azure Key Vault (same region & tenant). Enable soft-delete & purge protection. Allow trusted services if firewalling.

Grant hub system-assigned managed identity: Get, Wrap, Unwrap permissions.

Supported keys: RSA / RSA-HSM 2048.

## Create a hub with customer-managed keys

For customers in highly regulated industries, creating a hub with customer-managed keys (CMK) is a critical requirement.

### Prerequisites

Before creating your hub with CMK:

**Create and configure Azure Key Vault**in the same region and tenant as your planned hub:- Enable soft-delete
- Enable purge protection
- If using firewall, allow trusted Microsoft services
- Prepare an RSA or RSA-HSM 2048-bit key

**Plan your data storage approach**:- Service-side encryption (recommended): Data stored in Microsoft subscription
- Legacy approach: Managed resource group in your subscription

**Ensure proper permissions**: You need permissions to create the hub and assign Key Vault access policies

### Configure CMK during hub creation

To create a hub with CMK enabled, follow these steps in the Azure portal:

- Start the
**Create an Azure AI Hub**wizard. - On the
**Basics**tab, fill in the required details. - Navigate to the
**Encryption**tab. - Select
**Customer-managed keys**. - Select
**Select a key vault and key**. - Choose your existing Key Vault and the key you created in the prerequisites.
- (Optional) Configure the
**Service-side encryption**setting if needed. - Continue through the remaining tabs (Networking, Tags) and select
**Review + create**. - Select
**Create**to finish the hub creation.

After the hub is created, the system assigns a managed identity that receives Get, Wrap, and Unwrap permissions for the specified key.

## Customer-managed key constraints (permanent)

- CMK must be configured at hub creation time; you cannot add CMK to an existing hub.
- You cannot switch between customer-managed keys and Microsoft-managed keys after creation.
- Key rotation is supported only within the same Azure Key Vault; changing Key Vaults is not supported.

## Rotation

Rotate within the same Key Vault by updating the hub to a new key URI. Existing data isn't re-encrypted; new data uses the new key.

## Revocation

Remove access policy or delete key versions. Revocation halts new fine-tunes or downloads, but existing deployments continue to serve until deleted.

## Cost considerations

Dedicated hosting of certain back-end services under CMK results in extra subline items in Cost Management.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/disable-preview-features-with-rbac -->

# Disable preview features in Microsoft Foundry by using role-based access control

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

In Microsoft Foundry projects, some features are in preview. You can block access to these features by excluding specific data actions from a custom role, and then assigning that role to users.

This article lists the data actions for each preview feature so you can block features individually. Because you can't modify built-in roles in Foundry projects, you need to create a custom role.

## Prerequisites

- A Microsoft Foundry project.
- Permissions to create custom roles at the scope where you want the role to be assignable (for example, Owner or User Access Administrator).
- Permissions to assign roles at the scope where you assign access (for example, Role Based Access Control Administrator or User Access Administrator).

## Example: Create a custom role that blocks a preview feature

This example shows the JSON shape for a custom role definition and where to put the preview feature data actions.

If you clone an existing role or use wildcard permissions, add the preview feature data actions to `notDataActions`

so the role excludes them.

```
{
"properties": {
"roleName": "Foundry custom role (preview features blocked)",
"description": "Custom role that excludes specific Foundry preview features.",
"assignableScopes": [
"/subscriptions/<subscription-id>"
],
"permissions": [
{
"actions": [],
"notActions": [],
"dataActions": [],
"notDataActions": [
"Microsoft.CognitiveServices/accounts/AIServices/agents/write",
"Microsoft.CognitiveServices/accounts/AIServices/agents/read",
"Microsoft.CognitiveServices/accounts/AIServices/agents/delete"
]
}
]
}
}
```


Reference: [Create or update Azure custom roles using the Azure portal](/en-us/azure/role-based-access-control/custom-roles-portal)

Reference: [Assign Azure roles using the Azure portal](/en-us/azure/role-based-access-control/role-assignments-portal)

## Agent Service data actions

Use these data actions in a custom role definition:

`Microsoft.CognitiveServices/accounts/AIServices/agents/write`

`Microsoft.CognitiveServices/accounts/AIServices/agents/read`

`Microsoft.CognitiveServices/accounts/AIServices/agents/delete`


## Content understanding (multimodal intelligence)

Add these data actions to your custom role definition:

`Microsoft.CognitiveServices/accounts/MultiModalIntelligence/analyzers/read`

`Microsoft.CognitiveServices/accounts/MultiModalIntelligence/analyzers/write`

`Microsoft.CognitiveServices/accounts/MultiModalIntelligence/analyzers/delete`

`Microsoft.CognitiveServices/accounts/MultiModalIntelligence/classifiers/read`

`Microsoft.CognitiveServices/accounts/MultiModalIntelligence/classifiers/write`

`Microsoft.CognitiveServices/accounts/MultiModalIntelligence/classifiers/delete`

`Microsoft.CognitiveServices/accounts/MultiModalIntelligence/batchAnalysisJobs/*`


If your team labels documents in Foundry, search for `labelingProjects`

under the **Microsoft.CognitiveServices** resource provider and include the matching data actions.

## Fine-tuning

Add these data actions to your custom role definition:

`Microsoft.CognitiveServices/accounts/OpenAI/fine-tunes/*`

, includes`/files/*`

,`/uploads/*`

,`/stored-completions/*`

,`/evals/*`

,`/models/*`

- (optional, if you run RLHF jobs)
`Microsoft.CognitiveServices/accounts/OpenAI/1p-jobs/*`


## Tracing

Allow or deny the following data actions in the custom role definition.

Foundry's Tracing pane uses Azure Monitor. In the custom role wizard, set the provider to `Microsoft.Insights`

, then add or remove only the read actions you need:

`Microsoft.Insights/alertRules/read`

`Microsoft.Insights/diagnosticSettings/read`

`Microsoft.Insights/logDefinitions/read`

`Microsoft.Insights/metricdefinitions/read`

`Microsoft.Insights/metrics/read`


## Evaluation data actions

Add these data actions to your custom role definition:

`Microsoft.CognitiveServices/accounts/AIServices/evaluations/write`

`Microsoft.CognitiveServices/accounts/AIServices/evaluations/read`

`Microsoft.CognitiveServices/accounts/AIServices/evaluations/delete`


## Content safety risks and alerts

Add these data actions to your custom role definition:

`Microsoft.CognitiveServices/accounts/ContentSafety/*`


To allow only specific Content Safety operations, search for `ContentSafety`

in the Azure portal custom role editor and select the specific data actions you need.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/deployments-overview -->

# Deployment overview for Microsoft Foundry Models

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

The model catalog in Microsoft Foundry is the hub to discover and use a wide range of Foundry Models for building generative AI applications. You need to deploy models to make them available for receiving inference requests. Foundry offers a comprehensive suite of deployment options for Foundry Models, depending on your needs and model requirements.

## Deployment options

Foundry provides several deployment options depending on the type of models and resources you need to provision. The following deployment options are available:

- Standard deployment in Foundry resources
- Deployment to serverless API endpoints
- Deployment to managed computes

Foundry portal might automatically pick a deployment option based on your environment and configuration. Use Foundry resources for deployment whenever possible. Models that support multiple deployment options default to Foundry resources for deployment. To access other deployment options, use the Azure CLI or Azure Machine Learning SDK for deployment.

### Standard deployment in Foundry resources

Foundry resources (formerly referred to as Azure AI Services resources), is **the preferred deployment option** in Foundry. It offers the widest range of capabilities, including regional, data zone, or global processing, and it offers standard and [provisioned throughput (PTU)](../../ai-services/openai/concepts/provisioned-throughput?view=foundry-classic) options. Flagship models in Foundry Models support this deployment option.

This deployment option is available in:

- Foundry resources
- Azure OpenAI resources
1 - Azure AI hub, when connected to a Foundry resource

1If you use Azure OpenAI resources, the model catalog shows only Azure OpenAI in Foundry Models for deployment. You can get the full list of Foundry Models by upgrading to a Foundry resource.

To get started with standard deployment in Foundry resources, see [How-to: Deploy models to Foundry Models](../foundry-models/how-to/create-model-deployments?view=foundry-classic).

### Serverless API endpoint

This deployment option is available **only in** [Azure AI hub resources](ai-resources?view=foundry-classic). It allows you to create dedicated endpoints to host the model, accessible through an API. Foundry Models support serverless API endpoints with pay-as-you-go billing, and you can create only regional deployments for serverless API endpoints.

To get started with deployment to a serverless API endpoint, see [Deploy models as serverless API deployments](../how-to/deploy-models-serverless?view=foundry-classic).

### Managed compute

This deployment option is available **only in** [Azure AI hub resources](ai-resources?view=foundry-classic). It allows you to create a dedicated endpoint to host the model in a **dedicated compute**. You need to have compute quota in your subscription to host the model, and you're billed per compute uptime.

Managed compute deployment is required for model collections that include:

- Hugging Face
- NVIDIA inference microservices (NIMs)
- Industry models (Saifr, Rockwell, Bayer, Cerence, Sight Machine, Page AI, SDAIA)
- Databricks
- Custom models

To get started, see [How to deploy and inference a managed compute deployment](../how-to/deploy-models-managed?view=foundry-classic) and [Deploy Foundry Models to managed compute with pay-as-you-go billing](../how-to/deploy-models-managed-pay-go?view=foundry-classic).

## Capabilities for the deployment options

Use [Standard deployments in Foundry resources](#standard-deployment-in-foundry-resources) whenever possible. This deployment option provides the most capabilities among the available deployment options. The following table lists details about specific capabilities for each deployment option:

| Capability | Standard deployment in Foundry resources | Serverless API Endpoint | Managed compute |
|---|---|---|---|
| Which models can be deployed? |
|

[Foundry Models with pay-as-you-go billing](../how-to/model-catalog-overview?view=foundry-classic)[Open and custom models](../how-to/model-catalog-overview?view=foundry-classic#availability-of-models-for-deployment-as-managed-compute)Data-zone

Global

[provisioned throughput units](../../ai-services/openai/concepts/provisioned-throughput?view=foundry-classic)232 A minimal endpoint infrastructure is billed per minute. You aren't billed for the infrastructure that hosts the model in serverless deployment. After you delete the endpoint, no further charges accrue.

3 Billing is on a per-minute basis, depending on the product tier and the number of instances used in the deployment since the moment of creation. After you delete the endpoint, no further charges accrue.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/model-catalog-content-safety -->

# Guardrails & controls for Models Sold Directly by Azure

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

In this article, learn about content safety capabilities for models from the model catalog deployed using serverless API deployments.

## Content filter defaults

Azure AI uses a default configuration of [Azure AI Content Safety](/en-us/azure/ai-services/content-safety/overview) content filters to detect harmful content across four categories including hate and fairness, self-harm, sexual, and violence for models deployed via [serverless API deployments](deployments-overview?view=foundry-classic#serverless-api-endpoint). To learn more about content filtering, see [Understand harm categories](#understand-harm-categories).

The default content filtering configuration for text models is set to filter at the medium severity threshold, filtering any detected content at this level or higher. For image models, the default content filtering configuration is set at the low configuration threshold, filtering at this level or higher. For models deployed using the [Microsoft Foundry Models](../model-inference/how-to/configure-content-filters?view=foundry-classic), you can create configurable filters by selecting the **Content filters** tab within the **Guardrails & controls** page of the Foundry portal.

Tip

Content filtering isn't available for certain model types that are deployed via serverless API deployments. These model types include embedding models and time series models.

Content filtering occurs synchronously as the service processes prompts to generate content. You might be billed separately according to [Azure AI Content Safety pricing](https://azure.microsoft.com/pricing/details/cognitive-services/content-safety/) for such use. You can disable content filtering for individual serverless endpoints either:

- When you first deploy a language model
- Later, by selecting the content filtering toggle on the deployment details page

Suppose you decide to use an API other than the [Model Inference API](/en-us/azure/ai-studio/reference/reference-model-inference-api) to work with a model that is deployed via a serverless API deployment. In such a situation, content filtering (preview) isn't enabled unless you implement it separately by using Azure AI Content Safety. To get started with Azure AI Content Safety, see [Quickstart: Analyze text content](/en-us/azure/ai-services/content-safety/quickstart-text). You run a higher risk of exposing users to harmful content if you don't use content filtering (preview) when working with models that are deployed via serverless API deployments.

## Understand harm categories

### Harm categories

| Category | Description | API term |
|---|---|---|
| Hate and Fairness | Hate and fairness harms refer to any content that attacks or uses discriminatory language with reference to a person or identity group based on certain differentiating attributes of these groups. This includes, but isn't limited to:
|
`Hate` |
| Sexual | Sexual describes language related to anatomical organs and genitals, romantic relationships and sexual acts, acts portrayed in erotic or affectionate terms, including those portrayed as an assault or a forced sexual violent act against one's will. This includes but isn't limited to:
|
`Sexual` |
| Violence | Violence describes language related to physical actions intended to hurt, injure, damage, or kill someone or something; describes weapons, guns, and related entities. This includes, but isn't limited to:
|
`Violence` |
| Self-Harm | Self-harm describes language related to physical actions intended to purposely hurt, injure, damage one's body or kill oneself. This includes, but isn't limited to:
|
`SelfHarm` |

### Severity levels

| Level | Description |
|---|---|
| Safe | Content might be related to violence, self-harm, sexual, or hate categories. However, the terms are used in general, journalistic, scientific, medical, and similar professional contexts, which are appropriate for most audiences. |
| Low | Content that expresses prejudiced, judgmental, or opinionated views, includes offensive use of language, stereotyping, use-cases exploring a fictional world (for example, gaming, literature) and depictions at low intensity. |
| Medium | Content that uses offensive, insulting, mocking, intimidating, or demeaning language towards specific identity groups, includes depictions of seeking and executing harmful instructions, fantasies, glorification, promotion of harm at medium intensity. |
| High | Content that displays explicit and severe harmful instructions, actions, damage, or abuse; includes endorsement, glorification, or promotion of severe harmful acts, extreme or illegal forms of harm, radicalization, or nonconsensual power exchange or abuse. |

## How charges are calculated

Pricing details are viewable at [Azure AI Content Safety pricing](https://azure.microsoft.com/pricing/details/cognitive-services/content-safety/). Charges are incurred when the Azure AI Content Safety validates the prompt or completion. If Azure AI Content Safety blocks the prompt or completion, you're charged for both the evaluation of the content and the inference calls.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/encryption-keys-portal -->

# Customer-managed keys (CMK) for Microsoft Foundry

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

Tip

An alternate hub-focused CMK article is available: [Customer-managed keys for hub projects](hub-encryption-keys-portal?view=foundry-classic).

Customer-managed key (CMK) encryption in [Microsoft Foundry](https://ai.azure.com/?cid=learnDocs) gives you control over encryption of your data. Use CMKs to add an extra protection layer and help meet compliance requirements with Azure Key Vault integration.

Customer-managed key (CMK) encryption in [Microsoft Foundry](https://ai.azure.com/?cid=learnDocs) gives you control over encryption of your data. Use CMKs to add an extra protection layer and help meet compliance requirements with Azure Key Vault integration.

Microsoft Foundry provides robust encryption capabilities, including the ability to use **customer-managed keys (CMKs)** stored in **Azure Key Vault** to secure your sensitive data. This article explains the concept of encryption with CMKs and provides step-by-step guidance for configuring CMK using Azure Key Vault. It also discusses encryption models and access control methods like **Azure Role-Based Access Control (RBAC)** and **Vault Access Policies** and ensuring compatibility with **system-assigned managed identities** and **user-assigned managed identities (UAI)**.

## Why use customer-managed keys?

With CMK, you gain full control over encryption keys, providing enhanced protection for sensitive data and helping meet compliance requirements. The key benefits of using CMKs include:

Using your own keys to encrypt data at rest.

Integration with organizational security and compliance policies.

The ability to rotate or revoke keys for enhanced control over access to encrypted data.


Microsoft Foundry supports encryption with your CMKs stored in **Azure Key Vault**, leveraging industry-leading security features.

## Prerequisites

To configure CMK for Microsoft Foundry, ensure the following prerequisites are met:

**Azure Subscription**:

You need an active Azure subscription to create and manage Azure resources.**Azure Key Vault**:- You need an existing Azure Key Vault to store your keys.
- You must deploy the Key Vault and the Microsoft Foundry resource in the same Azure region.
- Enable Soft Delete and Purge Protection on Key Vault to safeguard customer-managed keys from accidental or malicious deletion (required by Azure)
- Follow this guide to create a Key Vault:
[Quickstart: Create a Key Vault using Azure portal](/en-us/azure/key-vault/general/quick-create-portal).

**Managed Identity Configuration**:**System-assigned managed identity**: Ensure your Microsoft Foundry resource has enabled a system-assigned managed identity.**User-assigned managed identity**: You can use the following link to create a[User-Assigned Managed Identity](/en-us/entra/identity/managed-identities-azure-resources/manage-user-assigned-managed-identities-azure-portal?pivots=identity-mi-methods-azp#create-a-user-assigned-managed-identity)

**Key Vault Permissions**:- If you're using
**Azure RBAC**, assign Key Vault Crypto User role to the managed identity. - If you're using
**Vault Access Policies**, grant key-specific permissions to the managed identity, such as**unwrap key**and**wrap key**.

- If you're using

Before configuring CMK, make sure you deploy your resources in a supported region. Refer to [Microsoft Foundry feature availability across cloud regions](../reference/region-support?view=foundry-classic) for more details on regional support for Microsoft Foundry features.

## Steps to Configure CMK

### Step 1. Create or Import a Key in Azure Key Vault

You store Customer-Managed Keys (CMKs) in **Azure Key Vault**. You can either generate a new key within the Key Vault or import an existing key. Follow the steps in the following sections:

**Generate a Key**

- Go to your Azure Key Vault in the Azure portal.
- Under
**Settings**, select**Keys**. - Select
**+ Generate/Import**. - Enter a key name, choose the key type (such as RSA or HSM-backed), and configure key size and expiration details.
- Select
**Create**to save the new key.

- Projects can be updated from Microsoft-managed keys to CMKs but not reverted.
- Project CMK can be updated only to keys in the same Key Vault instance.
- Storage-related charges for CMK encryption continue during soft-deleted retention.
For more information, see
[Create and Manage Keys in Azure Key Vault](/en-us/azure/key-vault/keys/about-keys).

**Import a Key**

- Go to the
**Keys**section in your Key Vault. - Select
**+ Generate/Import**and choose the**Import**option. - Upload the key material and provide the necessary key configuration details.
- Follow the prompts to complete the import process.

### Step 2. Grant Key Vault permissions to managed identities

Configure appropriate permissions for the **system-assigned** or **user-assigned managed identity** to access the Key Vault.

**System-assigned managed identity**

- Go to the Key Vault in the Azure portal.
- Select
**Access Control (IAM)**. - Select
**+ Add role assignment**. - Assign the Key Vault Crypto User role to the
**system-assigned managed identity**of the Microsoft Foundry resource or the**User-assigned managed identity**

### Step 3. Enable CMK in Microsoft Foundry

You can enable Customer-Managed Keys (CMK) either during the creation of a Microsoft Foundry resource or by updating an existing resource. During resource creation, the wizard will guide you to use either user-assigned or system-assigned managed identity, select a user-assigned managed identity, and select a key vault where your key is stored.

You can follow the steps below if you're updating an existing Microsoft Foundry resource to enable CMK:

- Open the Microsoft Foundry resource in the Azure portal.
- Go to the
**Encryption**under**Resource Management**section. - Select
**Customer-Managed Keys**as the encryption type. - Enter the
**Key Vault URL**and the key name.

**Key Vault Access Design: Azure RBAC vs. Vault Access Policies**

Azure Key Vault supports two models for managing access permissions:

**Azure RBAC (Recommended)**:- Provides centralized access control using Azure AD roles.
- Simplifies permission management for resources across Azure.
- Use Key Vault Crypto User role.

**Vault Access Policies**:- Allows granular access control specific to Key Vault resources.
- Suitable for configurations where legacy or isolated permission settings are necessary.


Choose the model that aligns with your organizational requirements.

**Monitoring and Rotating Keys**

To maintain optimal security and compliance, implement the following practices:

**Enable Key Vault Diagnostics**:

Monitor key usage and access activity by enabling diagnostic logging in Azure Monitor or Log Analytics.**Rotate Keys Regularly**:

Periodically create a new version of your key in Azure Key Vault.

Update the Microsoft Foundry resource to reference the latest key version in its**Encryption Settings**.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/retrieval-augmented-generation -->

# Retrieval augmented generation (RAG) and indexes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Retrieval augmented generation (RAG) is a pattern that combines search with large language models (LLMs) so responses are grounded in your data. This article explains how RAG works in Microsoft Foundry, what role indexes play, and how agentic retrieval changes classic RAG patterns.

## Overview

LLMs are trained on public data available at training time. If you need answers based on your private data, or on frequently changing information, RAG helps you:

- Retrieve relevant information from your data (often through an index).
- Provide that information to the model as grounding data.
- Generate a response that can include citations back to source content.

## Key concepts

**Grounding data**: Retrieved content you provide to the model to reduce guessing.**Index**: A data structure optimized for retrieval (keyword, semantic, vector, or hybrid search).**Embeddings**: Numeric representations of content used for vector similarity search. See[Understand embeddings](../openai/concepts/understand-embeddings?view=foundry-classic).**System message and prompts**: Instructions that guide how the model uses retrieved content. See[Prompt engineering](../openai/concepts/prompt-engineering?view=foundry-classic)and[Safety system messages](../openai/concepts/system-message?view=foundry-classic).

## What is RAG?

Large language models (LLMs) like ChatGPT are trained on public internet data that was available when the model was trained. The public data might not be sufficient for your needs. For example, you might want answers based on private documents, or you might need up-to-date information.

RAG addresses this by retrieving relevant content from your data and including it in the model input. The model can then generate responses grounded in the retrieved content.

## How does RAG work?

When a user asks a question, your application retrieves relevant content from your data store. The app then sends the user question and the retrieved content (grounding data) to the model with a prompt to generate an answer.

## Agentic RAG: modern approach to retrieval

Traditional RAG patterns often use a single query to retrieve information from your data. **Agentic retrieval** is an evolution in retrieval architecture that uses a model to break down complex inputs into multiple focused subqueries, run them in parallel, and return structured grounding data that works well with chat completion models.

Agentic retrieval provides several advantages over classic RAG:

**Context-aware query planning**- Uses conversation history to understand context and intent**Parallel execution**- Runs multiple focused subqueries simultaneously for better coverage**Structured responses**- Returns grounding data, citations, and execution metadata along with results**Built-in semantic ranking**- Ensures optimal relevance of results**Optional answer synthesis**- Can include LLM-formulated answers directly in the query response

If you're using Azure AI Search as your retrieval engine, see [Agentic retrieval](/en-us/azure/search/agentic-retrieval-overview) and [Quickstart: Agentic retrieval](../../search/search-get-started-agentic-retrieval?view=foundry-classic).

## What is an index and why do I need it?

RAG works best when you can retrieve relevant content quickly and consistently. An index helps by organizing your content for efficient retrieval.

Many RAG solutions use an index that supports one or more of these retrieval modes:

**Keyword search****Semantic search****Vector search****Hybrid search**(keyword + vector, sometimes with semantic ranking)

An index can also store fields that improve citation quality (for example, document titles, URLs, or file names).

Foundry can connect your project to an Azure AI Search service and index for retrieval. Depending on the feature and API surface you're using, this connection information might be represented as a project connection or an *index asset ID*.

For example, the Foundry Project REST API preview includes an `index_asset_id`

field for Azure AI Search index resources. See [Foundry Project REST API preview](../reference/foundry-project-rest-preview?view=foundry-classic).

Azure AI Search is a recommended index store for RAG scenarios. Azure AI Search supports retrieval over vector and textual data stored in search indexes, and it can also query other targets if you use agentic retrieval. See [What is Azure AI Search?](/en-us/azure/search/search-what-is-azure-search).

## Choose an approach in Foundry

Use the following guidance to decide where to start.

**Use RAG**when you need answers grounded in private or frequently changing data.**Use fine-tuning**when you need to change model behavior, style, or task performance, rather than add fresh knowledge.**Use a managed “use your data” experience**if you want a more guided way to connect, ingest, and chat over your data. See[Azure OpenAI On Your Data](../openai/concepts/use-your-data?view=foundry-classic)and[Quickstart: Chat with Azure OpenAI models using your own data](../openai/use-your-data-quickstart?view=foundry-classic).**Use agent tools**when you're building an agent that needs retrieval as a tool. For example, see[File search tool for agents](../agents/how-to/tools/file-search?view=foundry-classic).

## Security and privacy considerations

RAG systems can expose sensitive content if you don't design access and prompting carefully.

**Apply access control at retrieval time**. If you're using Azure AI Search as a data source, you can use document-level access control with security filters. See the[document-level access control](../openai/concepts/use-your-data?view=foundry-classic#document-level-access-control)section.**Prefer Microsoft Entra ID over API keys for production**. API keys are convenient for development but aren't recommended for production scenarios. For Azure AI Search RBAC guidance, see[Connect to Azure AI Search using roles](../../search/search-security-rbac?view=foundry-classic).**Treat retrieved content as untrusted input**. Your system message and application logic should reduce the risk of prompt injection from documents and retrieved passages. See[Safety system messages](../openai/concepts/system-message?view=foundry-classic).

## Cost and latency considerations

RAG adds extra work compared to a model-only request:

**Retrieval costs and latency**: Querying an index adds round trips and compute.**Embedding costs and latency**: Vector search requires embeddings at indexing time, and often at query time.**Token usage**: Retrieved passages increase input tokens, which can increase cost.

If you're using Azure AI Search, confirm service tier and pricing before production rollout. If you're using semantic or hybrid retrieval, review Azure AI Search pricing and limits in the Azure AI Search documentation.

## Limitations

- RAG quality depends on content preparation, retrieval configuration, and prompt design.
- If retrieval returns irrelevant or incomplete passages, the model can still produce incomplete answers.
- If you don't control access to source content, grounded responses can leak sensitive information.

## Related content

[Tutorial: Part 1 - Set up project and development environment to build a custom knowledge retrieval (RAG) app with the Microsoft Foundry SDK](../tutorials/copilot-sdk-create-resources?view=foundry-classic)[Tutorial: Part 2 - Build a custom knowledge retrieval (RAG) app with the Microsoft Foundry SDK](../tutorials/copilot-sdk-build-rag?view=foundry-classic)[Quickstart: Chat with Azure OpenAI models using your own data](../openai/use-your-data-quickstart?view=foundry-classic)[Azure OpenAI On Your Data](../openai/concepts/use-your-data?view=foundry-classic)[File search tool for agents](../agents/how-to/tools/file-search?view=foundry-classic)[Quickstart: Agentic retrieval](../../search/search-get-started-agentic-retrieval?view=foundry-classic)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/ai-resources -->

# Hub resources overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

This article provides legacy support for hub-based projects. It will not work for **Foundry projects**. See [How do I know which type of project I have?](../what-is-foundry?view=foundry-classic#how-do-i-know-which-type-of-project-i-have)

**SDK compatibility note**: Code examples require a specific Microsoft Foundry SDK version. If you encounter compatibility issues, consider [migrating from a hub-based to a Foundry project](../how-to/migrate-project?view=foundry-classic).

Foundry AI Hub is a resource type that you use with the Microsoft Foundry resource type. You only need it for selected use cases. Hub resources provide access to open-source model hosting and fine-tuning capabilities, as well as Azure Machine Learning capabilities, in addition to the capabilities supported by its associated Foundry resource.

Tip

Hub resources are available in Foundry portal, Azure Machine Learning studio, and the Azure portal. The feature set and management options vary by tool.

When you create an AI Hub, you automatically provision a Foundry resource. You can use hub resources in [Foundry](https://ai.azure.com/?cid=learnDocs) and [Azure Machine Learning studio](https://ml.azure.com).

Hubs have their own project types that support a differentiated feature set from Foundry projects. See [project types](../what-is-foundry?view=foundry-classic#which-type-of-project-do-i-need) for an overview of supported features.

## Create a hub resource

Get started by [creating your first hub in Foundry portal](../how-to/create-azure-ai-resource?view=foundry-classic), or use [Azure portal](../how-to/create-secure-ai-hub?view=foundry-classic) or [templates](../how-to/create-azure-ai-hub-template?view=foundry-classic) for advanced configuration options such as networking.

Hubs group one or more projects together with common settings, including data access and security configurations. Projects act as folders to organize work and give access to developer APIs.

## Create a hub-based project

To start developing, [create a hub-based project](../how-to/hub-create-projects?view=foundry-classic). You can access hub-based projects in [Foundry portal](https://ai.azure.com/?cid=learnDocs) to build with generative AI tools, and [ML Studio](https://ml.azure.com) to build with tools designed for custom machine learning model training.

## Project concepts

Projects let you create and group reusable components that you can use across tools.

| Asset | Description |
|---|---|
| Data | Dataset that you can use to create indexes, fine-tune models, and evaluate models. |
| Flows | An executable instruction set that can implement the AI logic. |
| Evaluations | Evaluations of a model or flow. You can run manual or metrics-based evaluations. |
| Indexes | Vector search indexes generated from your data. |

Projects also have specific settings that apply only to that project:

| Asset | Description |
|---|---|
| Project connections | Connections to external resources like data storage providers that only you and other project members can use. They complement shared connections on the hub accessible to all projects. |
| Prompt flow runtime | Prompt flow is a feature that you can use to generate, customize, or run a flow. To use prompt flow, you need to create a runtime on top of a compute instance. |

Note

In Foundry portal, you can also manage language and notification settings that apply to all projects that you can access regardless of the hub or project.

## Share configurations across projects using hub

A hub shares configurations for a group of projects. All projects in the hub share the same security configurations or business domain.

Shared configurations that you manage on the hub include:

**Security**including public network access, customer-managed key encryption, and identity controls. Security settings that you configure on the hub automatically pass down to each project. A managed virtual network is shared between all projects that share the same hub.**Connections**let you access objects in Foundry portal that are managed outside of your hub. For example, uploaded data on an Azure storage account, or model deployments on an existing Azure OpenAI or Foundry resource. Optionally use connection to store shared credentials, so developers can implicitly access remote objects during development.**Compute and quota allocation**is managed as shared capacity for all projects in Foundry portal that share the same hub. This quota includes compute instance as managed cloud-based workstation for an individual. The same user can use a compute instance across projects.**Policy**enforced in Azure on the hub scope applies to all projects managed under it.**Dependent Azure resources**are set up once per hub and associated projects. You use these resources to store artifacts you generate while working in Foundry portal such as logs or when uploading data. For more information, see[dependent resources](#storage-and-key-vault-dependent-resources).

## Access Foundry models from hub-based projects

By using hubs, you can manage connections to existing Azure OpenAI or Foundry resources. Use their models and selected customization capabilities in hub-based projects.

After you create a connection, you can access model deployments through playground experiences. When you use Fine-tuning experiences in a hub-based project, your fine-tuning jobs are implicitly executed on the connected Foundry resource (default project context).

## Storage and Key Vault dependent resources

Foundry AI Hub is an implementation of Azure Machine Learning and requires multiple Azure services as dependencies.

| Resource type | Resource provider and type | Kind | Supported capabilities |
|---|---|---|---|
| Microsoft Foundry | `Microsoft.CognitiveServices/account` |
`AIServices` |
Agents, Evaluations, Azure OpenAI, Speech, Vision, Language, and Content Understanding |
| Foundry project | `Microsoft.CognitiveServices/account/project` |
`AIServices` |
Subresource to the above |
| Azure Speech | `Microsoft.CognitiveServices/account` |
`Speech` |
Speech |
| Azure Language in Foundry Tools | `Microsoft.CognitiveServices/account` |
`Language` |
Language |
| Azure Vision in Foundry Tools | `Microsoft.CognitiveServices/account` |
`Vision` |
Vision |
| Azure OpenAI service | `Microsoft.CognitiveServices/account` |
`OpenAI` |
Azure OpenAI models and their customization |
| Azure AI Hub | `Microsoft.MachineLearningServices/workspace` |
`hub` |
Connectivity hub and security configuration holder for hub-based projects |
| Azure AI Hub project | `Microsoft.MachineLearningServices/workspace` |
`project` |
Custom ML model training and model hosting |

If you don't provide the following dependent resources, they're automatically created.

| Dependent Azure resource | Resource provider | Optional | Note |
|---|---|---|---|
| Microsoft Foundry | `Microsoft.CognitiveServices/accounts` |
Provides access to models and other core Foundry APIs. | |
| Azure Storage account | `Microsoft.Storage/storageAccounts` |
Stores artifacts for your projects like flows and evaluations. For data isolation, storage containers are prefixed using the project GUID, and conditionally secured using Azure ABAC for the project identity. | |
| Azure Key Vault | `Microsoft.KeyVault/vaults` |
Stores secrets like connection strings for your resource connections. For data isolation, secrets can't be retrieved across projects via APIs. | |
| Azure Container Registry | `Microsoft.ContainerRegistry/registries` |
✔ | Stores docker images created when using custom runtime for prompt flow. For data isolation, docker images are prefixed using the project GUID. |
| Azure Application Insights & Log Analytics Workspace |
`Microsoft.Insights/components` `Microsoft.OperationalInsights/workspaces` |
✔ | Used as log storage when you opt in for application-level logging for your deployed prompt flows. |
| Azure AI Search | `Microsoft.Search/searchServices` |
✔ | Provides search capabilities for your projects. |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/vulnerability-management -->

# Vulnerability management for Microsoft Foundry

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal only.

This document is also specific to a **hub-based project**, and doesn't apply to a **Foundry project**. See [How do I know which type of project I have?](../what-is-foundry?view=foundry-classic#how-do-i-know-which-type-of-project-i-have) and [Create a hub-based project](../how-to/create-projects?view=foundry-classic&pivots=%22hub-project%22).

Vulnerability management is the process of detecting, assessing, mitigating, and reporting security vulnerabilities in an organization's systems and software. You and Microsoft share this responsibility.

This article describes your responsibilities and the vulnerability management controls that Foundry provides. Learn how to keep your service instance and apps up to date with the latest security updates and reduce the window of opportunity for cyberattackers.

## Prerequisites

To manage vulnerabilities in your Foundry environment, you need:

- An Azure subscription
- A Foundry hub or project
- Contributor or Owner role on the Foundry hub or project to manage compute resources
- Azure CLI or access to the Foundry portal for compute management
- For compute instance recreation: permissions to create and delete compute instances (
`Microsoft.MachineLearningServices/workspaces/computes/write`

and`Microsoft.MachineLearningServices/workspaces/computes/delete`

)

## Microsoft-managed VM images

Microsoft manages host OS virtual machine (VM) images for compute instances and serverless compute clusters. Updates are monthly and include the following details:

For each new VM image version, Microsoft sources the latest OS updates from the original publisher. Using the latest updates helps ensure you get all applicable OS patches. For Foundry, Canonical publishes all Ubuntu images.

VM images are updated monthly.

In addition to the publisher's patches, Microsoft updates system packages as updates become available.

Microsoft checks and validates any machine learning packages that might require an upgrade. In most circumstances, new VM images contain the latest package versions.

All VM images are built on secure subscriptions that run vulnerability scanning regularly. Microsoft flags any unaddressed vulnerabilities and fixes them within the next release.

Most images use a monthly release cadence. For compute instances, the image release aligns with the release cadence of the Azure Machine Learning SDK that's preinstalled in the environment.


Microsoft also applies hotfixes when vulnerabilities surface. Microsoft rolls out hotfixes within 72 hours for serverless compute clusters and within a week for compute instances.

Note

The host OS isn't the OS version you specify for an environment when you train or deploy a model. Environments run inside Docker. Docker runs on the host OS.

## Microsoft-managed container images

[Base Docker images](https://github.com/Azure/AzureML-Containers) that Microsoft maintains for Foundry receive frequent security patches to fix newly discovered vulnerabilities.

Microsoft updates supported images every two weeks to fix vulnerabilities. The goal is zero vulnerabilities older than 30 days in the latest supported images.

Microsoft releases patched images with a new immutable tag and an updated `:latest`

tag. Using the `:latest`

tag or pinning a specific image version is a tradeoff between security and environment reproducibility for your machine learning job.

## Managing environments and container images

In the Foundry portal, Docker images provide the runtime environment for [prompt flow deployments](../how-to/flow-deploy?view=foundry-classic). These images start from a Foundry base image.

Although Microsoft patches base images with each release, using the latest image is a tradeoff between reproducibility and vulnerability management. You choose the environment version for your jobs or model deployments.

By default, dependencies are layered on top of base images when you build an image. After you install extra dependencies on Microsoft-provided images, you're responsible for vulnerability management.

Your hub includes an Azure Container Registry instance that caches container images. When you build an image, you push it to the container registry. The workspace uses the cached image when you deploy the corresponding environment.

The hub doesn't delete any image from your container registry. Review the need for each image over time. To monitor and maintain environment hygiene, use [Microsoft Defender for Container Registry](/en-us/azure/defender-for-cloud/defender-for-container-registries-usage) to scan your images for vulnerabilities. To automate processes based on Microsoft Defender triggers, see [Automate remediation responses](/en-us/azure/defender-for-cloud/workflow-automation).

## Vulnerability management on compute hosts

Managed compute nodes in the Foundry portal use Microsoft-managed OS VM images. When you provision a node, it pulls the latest VM image. This behavior applies to compute instances, serverless compute clusters, and managed inference compute.

Although Microsoft regularly patches OS VM images, it doesn't actively scan compute nodes for vulnerabilities while they're in use. For an extra layer of protection, consider network isolation for your compute nodes.

Ensuring that your environment is up to date and that compute nodes use the latest OS version is a shared responsibility between you and Microsoft. The service doesn't update busy nodes to the latest VM image. Considerations are slightly different for each compute type, as listed in the following sections.

### Compute instance

Compute instances get the latest VM image when you provision them. Microsoft releases new VM images monthly. After you deploy a compute instance, it doesn't receive ongoing image updates. To stay current with the latest software updates and security patches, use one of these methods:

Re-create a compute instance to get the latest OS image (recommended).

If you use this method, you lose data and customizations (such as installed packages) stored on the instance's OS disk and temporary disk.

For more information about image releases, see the

[Azure Machine Learning compute instance image release notes](/en-us/azure/machine-learning/azure-machine-learning-ci-image-release-notes).Regularly update OS and Python packages.

Connect to your compute instance terminal and run the following commands to update packages:

Update the package list with the latest versions:

`sudo apt-get update`

Expected output: Package lists are refreshed from repositories.

Upgrade packages to the latest versions. Package conflicts might occur when you use this approach:

`sudo apt-get upgrade`

Expected output: Packages are downloaded and installed. You might be prompted to confirm installation.

Check for outdated Python packages:

`pip list --outdated`

Expected output: List of packages with available updates, or empty output if all packages are current.


**Reference**:[apt-get documentation](https://manpages.ubuntu.com/manpages/focal/man8/apt-get.8.html),[pip list documentation](https://pip.pypa.io/en/stable/cli/pip_list/)To verify updates were applied successfully, run:

`# Check for remaining upgradable packages sudo apt list --upgradable`

Expected output: No packages listed means all updates are applied.


Install and run additional scanning software on the compute instance to scan for security issues:

- Use
[Trivy](https://github.com/aquasecurity/trivy)to discover OS and Python package-level vulnerabilities. For quick start and usage examples, see the[Trivy documentation](https://aquasecurity.github.io/trivy/). - Use
[ClamAV](https://www.clamav.net/)to discover malware. It comes preinstalled on compute instances. For usage guidance, see the[ClamAV documentation](https://docs.clamav.net/manual/Usage.html).

For automation examples combining Trivy and ClamAV, see [Compute instance sample setup scripts](https://github.com/Azure/azureml-examples/tree/main/setup/setup-ci).

Installing the Microsoft Defender for Servers agent isn't supported.

### Endpoints

Endpoints automatically receive OS host image updates with vulnerability fixes. Microsoft updates images at least once a month.

Compute nodes automatically upgrade to the latest VM image version when it's released. You don't need to take any action.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/architecture -->

# Microsoft Foundry architecture

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

Microsoft Foundry provides a comprehensive set of tools to support development teams in building, customizing, evaluating, and operating AI Agents and its composing models and tools.

This article provides IT operations and security teams with details on the Foundry resource and underlying Azure service architecture, its components, and its relation with other Azure resource types. Use this information to guide how to [customize](../how-to/configure-private-link?view=foundry-classic) your Foundry deployment to your organization's requirements. For more information on how to roll out Foundry in your organization, see [Foundry Rollout](planning?view=foundry-classic).

## Azure AI resource types and providers

Within the Azure AI product family, you can use these [Azure resource providers](/en-us/azure/azure-resource-manager/management/resource-providers-and-types) that support user needs at different layers in the stack.

| Resource provider | Purpose | Supports resource type kinds |
|---|---|---|
| Microsoft.CognitiveServices | Supports Agentic and GenAI application development composing and customizing prebuilt models. | Foundry; Azure OpenAI service; Azure Speech; Azure Vision |
| Microsoft.Search | Support knowledge retrieval over your data | Azure AI Search |
| Microsoft.MachineLearningServices | Train, deploy, and operate custom and open source machine learning models | Azure AI Hub (and its projects); Azure Machine Learning Workspace |

| Resource provider | Purpose | Supports resource type kinds |
|---|---|---|
| Microsoft.CognitiveServices | Supports Agentic and GenAI application development composing and customizing prebuilt models. | Foundry; Azure OpenAI service; Azure Speech; Azure Vision |
| Microsoft.Search | Support knowledge retrieval over your data | Azure AI Search |

The Foundry resource is the primary resource for Azure AI and is recommended for most use cases. It's built on the same [Azure resource provider and resource type](/en-us/azure/azure-resource-manager/management/resource-providers-and-types) as the Azure OpenAI, Azure Speech, Azure Vision, and Azure Language services. It provides access to the superset of capabilities from each of the individual services combined.

| Resource type | Resource provider and type | Kind | Supported capabilities |
|---|---|---|---|
| Microsoft Foundry | `Microsoft.CognitiveServices/account` |
`AIServices` |
Agents, Evaluations, Azure OpenAI, Speech, Vision, Language, and Content Understanding |
| Foundry project | `Microsoft.CognitiveServices/account/project` |
`AIServices` |
Subresource to the above |
| Azure Speech in Foundry Tools | `Microsoft.CognitiveServices/account` |
`Speech` |
Speech |
| Azure Language in Foundry Tools | `Microsoft.CognitiveServices/account` |
`Language` |
Language |
| Azure Vision in Foundry Tools | `Microsoft.CognitiveServices/account` |
`Vision` |
Vision |

Resource types under the same provider namespaces share the same management APIs, and use similar [Azure Role Based Access Control](/en-us/azure/role-based-access-control/overview) actions, networking configurations, and aliases for Azure Policy configuration. If you're upgrading from Azure OpenAI to Foundry, your existing custom Azure policies and Azure Role Based Access Control actions continue to apply.

## Security-driven separation of concerns

Foundry enforces a clear separation between management and development operations to ensure secure and scalable AI workloads.

**Top-Level Resource Governance:**Management operations, such as configuring security, establishing connectivity with other Azure services, and managing deployments, are scoped to the top-level Foundry resource. Development activities are isolated within dedicated project containers, which encapsulate use cases and provide boundaries for access control, files, agents, and evaluations.**Role-Based Access Control (RBAC):**Azure RBAC actions reflect this separation of concerns. Control plane actions, such as creating deployments and projects, are distinct from data plane actions, such as building agents, running evaluations, and uploading files. You can scope RBAC assignments at both the top-level resource and individual project level. Assign[managed identities](/en-us/entra/identity/managed-identities-azure-resources/overview)at either scope to support secure automation and service access. For more information, see[Role-based access control for Microsoft Foundry](rbac-foundry?view=foundry-classic).**Monitoring and Observability:**Azure Monitor metrics are segmented by scope. You can view management and usage metrics at the top-level resource, while project-specific metrics, such as evaluation performance or agent activity, are scoped to the individual project containers.

## Computing infrastructure

Foundry uses a flexible compute architecture to support different [model access](foundry-models-overview?view=foundry-classic) and workload execution scenarios.

**Model Hosting Architecture**: Foundry models access is provided in different ways:[Standard deployment in Foundry resources](deployments-overview?view=foundry-classic#standard-deployment-in-foundry-resources)[Deployment to serverless API endpoints in Azure AI Hub resources](deployments-overview?view=foundry-classic#serverless-api-endpoint)[Deployment to managed computes in Azure AI Hub resources](deployments-overview?view=foundry-classic#managed-compute)

For an overview of data, privacy, and security considerations with these deployment options, see

[Data, privacy, and security for use of models](../how-to/concept-data-privacy?view=foundry-classic).

**Model Hosting Architecture**is provided by standard deployment in Foundry resources. For an overview of data, privacy, and security considerations with deployment, see[Data, privacy, and security for use of models](../how-to/concept-data-privacy?view=foundry-classic).

**Workload Execution:**Agents, Evaluations, and Batch jobs run as managed container compute, fully managed by Microsoft.**Networking Integration:**For enhanced security and compliance when your Agents connect with external systems,[container injection](../agents/how-to/virtual-networks?view=foundry-classic)allows the platform network to host APIs and inject a subnet into your network. This setup enables local communication of your Azure resources within the same virtual network.

## Data storage

Foundry provides flexible and secure data storage options to support a wide range of AI workloads.

**Managed storage for file upload**: In the default setup, Foundry uses Microsoft-managed storage accounts that are logically separated and support direct file uploads for select use cases, such as OpenAI models, Assistants, and Agents, without requiring a customer-provided storage account.**Bring your own storage (optional)**: Users can optionally connect their own Azure Storage accounts. Foundry tools can read inputs from and write outputs to these accounts, depending on the tool and use case.**Bring your own storage for storing Agent state**:- In the basic configuration, the Agent service stores threads, messages, and files in Microsoft-managed multitenant storage, with logical separation.
- With the
[Agent standard setup](../agents/how-to/use-your-own-resources?view=foundry-classic), you can bring your own storage for thread and message data. In this configuration, data is isolated by project within the customer’s storage account.

**Customer-managed key encryption**: By default, Azure services use Microsoft-managed encryption keys to encrypt data in transit and at rest. Data is encrypted and decrypted using FIPS 140-2 compliant 256-bit AES encryption. Encryption and decryption are transparent, meaning encryption and access are managed for you. Your data is secure by default and you don't need to modify your code or applications to take advantage of encryption.**Bring your own Key Vault**: By default, Foundry stores all API key-based connection secrets in a managed Azure Key Vault. For users that prefer to manage this themselves, they can connect their key vault to the Foundry resource. One Azure Key Vault connection manages all project and resource level connection secrets. For more information, see[how to set up an Azure Key Vault connection to Foundry](../how-to/set-up-key-vault-connection?view=foundry-classic).When you use customer-managed keys, your data on Microsoft-managed infrastructure is encrypted by using your keys.

To learn more about data encryption, see

[customer-managed keys for encryption with Foundry](encryption-keys-portal?view=foundry-classic).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/ask-ai -->

# Ask AI for help (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

You can ask AI to assist you in Microsoft Foundry. To start using AI to ask questions, select the AI icon in the upper right of the [Microsoft Foundry](https://ai.azure.com/?cid=learnDocs) portal. A chat window opens where you can type your questions and receive answers in real-time.


Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## Prerequisites

- Access to the
[Foundry portal](https://ai.azure.com/?cid=learnDocs).

## Capabilities

**What This AI Can Do** - The Ask AI experience is designed to provide assistance by answering questions based on:

**Documentation**: This documentation includes details about Foundry such as Quickstarts, How-tos, or reference documentation of the Microsoft Foundry SDK. The agent can help you navigate the documentation or find answers for you.**Model Catalog**: Provide information about specific models in the Foundry model catalog, including their capabilities and features.**Troubleshooting**: Help diagnose and resolve common Foundry problems by searching the troubleshooting knowledge base and providing step-by-step solutions.

**What This AI Cannot Do** - While the agent is a powerful tool, it has some limitations:

**No Access to Your Resources**: The agent can't access your Azure resources. For example, it can't answer questions like "How much capacity do I have?" or "What is the status of my deployment?"**Limited Scope**: It's restricted to answering questions related to the Foundry documentation and model catalog. It can't provide support for unrelated Azure services or external systems.

Use the agent to make the most of the Foundry experience but keep its scope and limitations in mind when asking questions.

You can ask AI to assist you in Foundry. To start using AI to ask questions or complete tasks, select its icon located in the top right bar of the [Microsoft Foundry](https://ai.azure.com/?cid=learnDocs) portal. A chat window opens where you can type your questions and receive answers in real-time. You can also ask the agent to run tasks for you.


Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## Prerequisites

- Access to the
[Foundry portal](https://ai.azure.com/?cid=learnDocs).

## Capabilities

**What This AI Can Do** - The Ask AI experience provides assistance by answering questions and performing tasks through specialized sub-agents:

**Documentation**: This documentation includes details about Foundry such as Quickstarts, How-tos, or reference documentation of the Microsoft Foundry SDK. The agent can help you navigate the documentation or find answers for you.**Model Catalog**: Provide information about specific models in the model catalog, including their capabilities and features.**Troubleshooting**: Help diagnose and resolve common Foundry problems by searching the troubleshooting knowledge base and providing step-by-step solutions.**Quota & Model Operations**: Deploy models, debug deployment problems, find deployment details, check quota and capacity in specific regions, and delete model deployments.**Model Analysis**: Recommend models based on cost, performance, or quality. Compare models using benchmark data across quality, cost, throughput, safety, and latency criteria. Analyze operational data for Azure OpenAI deployments.**Monitoring Dashboard Insights**: Interpret evaluation dashboard visualizations, identify patterns and anomalies in monitoring data, and suggest optimizations based on performance metrics.**Evaluation Management**: Manage evaluation workflows for large language models and agents, including setup, execution, and monitoring of evaluation jobs.

**What This AI Can't Do** - While the agent is a powerful tool, it has some limitations and constraints:

**Limited Scope**: It's restricted to answering questions related to the Foundry documentation and model catalog. It can't provide support for unrelated Azure services or external systems.**Call External APIs**: This AI experience can only call for a specific subset of Foundry APIs. It can't access the web or APIs external to Microsoft.**Bypass Permissions**: This AI experience can execute actions on your behalf. It requires you to have the right permissions for those actions. This agent can't perform an action that you wouldn't be able to do yourself.

Use the agent to make the most of the Foundry experience but keep its scope and limitations in mind when asking questions.

## Actions and approvals

When you ask the Ask AI agent to perform tasks that require accessing or modifying your Azure resources, the agent proposes actions for you to review and approve before execution. This approval flow ensures you maintain oversight over what actions are performed on your behalf.


The actions come from the tools available under the [Foundry Model Context Protocol (MCP) Server](../mcp/available-tools?view=foundry-classic).

To make this approval flow easier, you can **change the approval settings** to pre-approve some actions depending on their scope. Access the approval settings by selecting the settings icon in the Ask AI prompt chat box. By default, this experience is set to pre-approve **System access** actions. You can change these settings anytime, and they persist beyond your session.


## Best practices and security guidance

The Ask AI experience relies on the [Foundry Model Context Protocol (MCP) Server](../mcp/get-started?view=foundry-classic). By using this server, it implements the [same best practices and security guidance](../mcp/security-best-practices?view=foundry-classic).

Important

By using this preview feature, you acknowledge and consent to any cross-region processing that may occur. As an example, an EU resource accessed by a US user could be routed through US infrastructure. If your organization requires strict in-region processing, don't use Ask AI (preview) or restrict its use to scenarios that remain within your selected region.

## Responsible AI FAQ for Ask AI

### What is Ask AI in Foundry?

It's an AI agent that enables users of Foundry to navigate its capabilities, identify models, and understand how to use its resources to build generative AI applications. For an overview of how the agent works and a summary of its capabilities, see the overview earlier in this article.

### What is the current status of the Ask AI feature?

It's available in Foundry as a preview feature.

### Are the Ask AI results reliable?

The agent is designed to generate the best possible responses within the context it can access. However, like any AI system, the agent's responses aren't always perfect. Carefully test, review, and vet all of the agent's responses before using them in Foundry or for your application.

### How do I provide feedback on Ask AI?

If you see a response that's inaccurate or doesn't support your needs, use the thumbs-down button to submit feedback. You can also submit feedback on your overall experience by using the Foundry feedback button on the top menu.

### What should I do if I see unexpected or offensive content?

The Foundry team built the agent by following the [AI principles](https://www.microsoft.com/ai/principles-and-approach) and [Responsible AI Standard](https://aka.ms/RAIStandardPDF). The team prioritized mitigating exposing customers to offensive content. However, you might still see unexpected results. The team is constantly working to improve the technology to prevent the output of harmful content.

If you encounter harmful or inappropriate content in the system, select the thumbs-down icon below the response to provide feedback or report a concern.

### How current is the information provided by the agent?

The agent is updated daily to keep it up to date with the latest information. In most cases, the information the agent provides is up to date. However, there might be some delay between new Foundry announcements and updates to the agent.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/hub-rbac-foundry -->

# Role-based access control for Microsoft Foundry (hub-focused)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

This article provides legacy support for hub-based projects. It will not work for **Foundry projects**. See [How do I know which type of project I have?](../what-is-foundry?view=foundry-classic#how-do-i-know-which-type-of-project-i-have)

**SDK compatibility note**: Code examples require a specific Microsoft Foundry SDK version. If you encounter compatibility issues, consider [migrating from a hub-based to a Foundry project](../how-to/migrate-project?view=foundry-classic).

Tip

An alternate Foundry project-focused RBAC article is available: [Role-based access control for Microsoft Foundry](rbac-foundry?view=foundry-classic).

In this article, you learn how to manage access at the hub and project levels of Foundry. Use Azure role-based access control (Azure RBAC) to manage access to Azure resources. Azure provides built-in roles and lets you create custom roles.

## Foundry hub vs project

In the Foundry portal, access has two levels: the hub and the project. The hub hosts infrastructure (including virtual network setup, customer-managed keys, managed identities, and policies). It’s where you configure Foundry Tools. Hub access lets you modify infrastructure, create hubs, and create projects. Projects are a subset of the hub and act as workspaces to build and deploy AI systems. In a project, develop flows, deploy models, and manage project assets. Project access lets you build and deploy AI end to end while using the hub infrastructure.


A key benefit of the hub and project relationship is that developers can create projects that inherit hub security settings. Some developers are contributors to a project and can't create new projects.

## Default roles for the hub

The Foundry hub has built-in roles that are available by default.

| Role | Description |
|---|---|
| Owner | Full access to the hub, including the ability to manage hubs, create new hubs, and assign permissions. This role is automatically assigned to the hub creator. |
| Contributor | User has full access to the hub, including the ability to create new hubs, but isn't able to manage hub permissions on the existing resource. |
| Azure AI Administrator | Automatically assigned to the hub's system-assigned managed identity. Grants the minimum permissions the managed identity needs to perform tasks. |
| Azure AI Developer | Perform all actions except creating new hubs or managing hub permissions. Users can assign permissions within their project. |
| Azure AI Inference Deployment Operator | Do all actions required to create a resource deployment within a resource group. |
| Reader | Read-only access to the hub. This role is automatically assigned to all project members within the hub. |

The key difference between Contributor and Azure AI Developer is the ability to create new hubs. Only the Owner and Contributor roles let you create a hub. Custom roles can't grant hub creation.

### Azure AI Administrator role

Hubs created after 11/19/2024 have the system-assigned managed identity assigned to the **Azure AI Administrator** role instead of **Contributor**.

```
{
"permissions": [
{
"actions": [
"Microsoft.Authorization/*/read",
"Microsoft.CognitiveServices/*",
"Microsoft.ContainerRegistry/registries/*",
"Microsoft.DocumentDb/databaseAccounts/*",
"Microsoft.Features/features/read",
"Microsoft.Features/providers/features/read",
"Microsoft.Features/providers/features/register/action",
"Microsoft.Insights/alertRules/*",
"Microsoft.Insights/components/*",
"Microsoft.Insights/diagnosticSettings/*",
"Microsoft.Insights/generateLiveToken/read",
"Microsoft.Insights/logDefinitions/read",
"Microsoft.Insights/metricAlerts/*",
"Microsoft.Insights/metricdefinitions/read",
"Microsoft.Insights/metrics/read",
"Microsoft.Insights/scheduledqueryrules/*",
"Microsoft.Insights/topology/read",
"Microsoft.Insights/transactions/read",
"Microsoft.Insights/webtests/*",
"Microsoft.KeyVault/*",
"Microsoft.MachineLearningServices/workspaces/*",
"Microsoft.Network/virtualNetworks/subnets/joinViaServiceEndpoint/action",
"Microsoft.ResourceHealth/availabilityStatuses/read",
"Microsoft.Resources/deployments/*",
"Microsoft.Resources/deployments/operations/read",
"Microsoft.Resources/subscriptions/operationresults/read",
"Microsoft.Resources/subscriptions/read",
"Microsoft.Resources/subscriptions/resourcegroups/deployments/*",
"Microsoft.Resources/subscriptions/resourceGroups/read",
"Microsoft.Resources/subscriptions/resourceGroups/write",
"Microsoft.Storage/storageAccounts/*",
"Microsoft.Support/*",
"Microsoft.Search/searchServices/write",
"Microsoft.Search/searchServices/read",
"Microsoft.Search/searchServices/delete",
"Microsoft.Search/searchServices/indexes/*",
"Microsoft.DataFactory/factories/*"
],
"notActions": [],
"dataActions": [],
"notDataActions": []
}
]
}
```


### Azure AI Developer role

```
{
"permissions": [
{
"actions": [
"Microsoft.MachineLearningServices/workspaces/*/read",
"Microsoft.MachineLearningServices/workspaces/*/action",
"Microsoft.MachineLearningServices/workspaces/*/delete",
"Microsoft.MachineLearningServices/workspaces/*/write",
"Microsoft.MachineLearningServices/locations/*/read",
"Microsoft.Authorization/*/read",
"Microsoft.Resources/deployments/*"
],
"notActions": [
"Microsoft.MachineLearningServices/workspaces/delete",
"Microsoft.MachineLearningServices/workspaces/write",
"Microsoft.MachineLearningServices/workspaces/listKeys/action",
"Microsoft.MachineLearningServices/workspaces/hubs/write",
"Microsoft.MachineLearningServices/workspaces/hubs/delete",
"Microsoft.MachineLearningServices/workspaces/featurestores/write",
"Microsoft.MachineLearningServices/workspaces/featurestores/delete"
],
"dataActions": [
"Microsoft.CognitiveServices/accounts/OpenAI/*",
"Microsoft.CognitiveServices/accounts/SpeechServices/*",
"Microsoft.CognitiveServices/accounts/ContentSafety/*"
],
"notDataActions": []
}
]
}
```


## Default roles for projects

When you grant a user access to a project, the system also assigns the Reader role on the hub and the Inference Deployment Operator role to allow deployments in the resource group.

| Role | Description |
|---|---|
| Owner | Full access to the project, including assigning permissions to project users. |
| Contributor | Full access but can't assign permissions. |
| Azure AI Administrator | Automatically assigned to the hub managed identity. |
| Azure AI Developer | Create deployments; can't assign permissions. |
| Azure AI Inference Deployment Operator | Actions required to create resource deployments. |
| Reader | Read-only access. |

To create a project, a role must include `Microsoft.MachineLearningServices/workspaces/hubs/join`

on the hub (included in Azure AI Developer).

## Dependency service permissions

| Permission | Purpose |
|---|---|
`Microsoft.Storage/storageAccounts/write` |
Create/update storage account. |
`Microsoft.KeyVault/vaults/write` |
Create/update key vault. |
`Microsoft.CognitiveServices/accounts/write` |
Write API accounts. |
`Microsoft.MachineLearningServices/workspaces/write` |
Create/update workspace. |

## Sample enterprise RBAC setup for hubs

| Persona | Role | Purpose |
|---|---|---|
| IT admin | Owner | Ensures hub standards. Assigns manager roles. |
| Managers | Contributor or Azure AI Developer | Manage hub, audit shared resources. |
| Team lead | Azure AI Developer | Create projects and shared resources. |
| Developers | Contributor or Azure AI Developer (project) | Build and deploy models. |

## Access to external resources

Ensure the hub managed identity is granted required roles on external services (for example, storage, search) before use.

## Manage access

Use the Foundry portal (Users blade) or Azure portal IAM / CLI to assign roles.

Example CLI:

```
az role assignment create --role "Azure AI Developer" --assignee "user@contoso.com" --scope /subscriptions/<sub-id>/resourceGroups/<rg-name>
```


## Custom roles

Define custom roles when built-in roles don't meet needs. Example subscription-level custom role excerpt:

```
{
"properties": {
"roleName": "Foundry Developer",
"description": "Custom role for Foundry. At subscription level",
"assignableScopes": ["/subscriptions/<your-subscription-id>"],
"permissions": [ { "actions": ["Microsoft.MachineLearningServices/workspaces/write", "Microsoft.MachineLearningServices/workspaces/endpoints/write"], "notActions": [], "dataActions": ["Microsoft.CognitiveServices/accounts/OpenAI/*/read"], "notDataActions": [] } ]
}
}
```


## Assigning roles in the portal

In the management center, select **Users** at hub or project level, then **New user**.

## Scenario highlights

- Customer-managed key: Grant workspace creator access to Key Vault; if using user-assigned identity, grant needed data-plane permissions.
- Connections with Microsoft Entra ID: Assign required Azure RBAC roles (for example, Storage Blob Data Contributor, Search Index Data Contributor).
- Azure Container Registry: Use system-assigned managed identity or assign
`ACRPull`

to user-assigned identity. - Application Insights: Requires
`Microsoft.Insights/Components/Write`

and`Microsoft.OperationalInsights/workspaces/write`

during hub creation.

## Troubleshooting

If new hubs using Azure AI Administrator identity role encounter issues, you can temporarily revert to Contributor (see original article for detailed steps).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/authentication-authorization-foundry -->

# Authentication and authorization in Microsoft Foundry

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Authentication and authorization in Microsoft Foundry define how principals prove identity and gain permission to perform control plane and data plane operations. Foundry supports API key and Microsoft Entra ID token-based authentication. Microsoft Entra ID enables conditional access, managed identities, granular role-based access control (RBAC) actions, and least privilege scenarios. API keys remain available for rapid prototyping and legacy integration but lack per-user traceability. This article explains the control plane and data plane model, compares API key and Microsoft Entra ID (formerly Azure AD) authentication, maps identities to roles, and describes common least privilege scenarios.

Important

Use Microsoft Entra ID for production workloads to enable conditional access, managed identities, and least privilege RBAC. API keys are convenient for quick evaluation but provide coarse-grained access.

## Control plane and data plane

Azure operations divide into two categories: control plane and data plane. Azure separates resource management (control plane) from operational runtime (data plane). Therefore, you use the control plane to manage resources in your subscription and use the data plane to use capabilities exposed by your instance of a resource type. To learn more about control plane and data plane, see [Azure control plane and data plane](/en-us/azure/azure-resource-manager/management/control-plane-and-data-plane).
In Foundry, there's a clear distinction between control plane operations versus data plane operations. The following table explains the difference between the two, the scope in Foundry, typical operations of a user, example tools and features, and the authorization surface to use each.

| Plane | Scope in Foundry | Typical operations | Example tools | Authorization surface |
|---|---|---|---|---|
| Control plane | Setting up and configuring resource, projects, networking, encryption, and connections | Create or delete resources, assign roles, rotate keys, set up Private Link | Azure portal, Azure CLI, ARM templates, Bicep, Terraform | Azure RBAC actions |
| Data plane | Running and using model inference, agent interactions, evaluation jobs, and content safety calls | Chat completions, embedding generation, start fine-tune jobs, send agent messages, analyzer and classifier operations | SDKs, REST APIs, Foundry portal playground | Azure RBAC dataActions |

For all Bicep, Terraform, and SDK samples, see the [foundry-samples repository on GitHub](https://github.com/azure-ai-foundry/foundry-samples) for Foundry.

### Control plane and data plane diagram

Within Foundry, there's a clear separation between control plane and data plane actions. Control plane actions within Foundry include:

- Foundry resource creation
- Foundry project creation
- Account Capability Host creation
- Project Capability Host creation
- Model deployment
- Account and project connection creation

Data plane actions within Foundry include:

- Building agents
- Running an evaluation
- Tracing and monitoring
- Fine-tuning

The following diagram shows the view of control plane versus data plane separation in Foundry alongside role-based access control (RBAC) assignments and what access a user may have in either the control plane or data plane or both. As seen in the diagram, RBAC "actions" are associated with control plane while RBAC "dataActions" are associated with data plane.

## Authentication methods

Foundry supports Microsoft Entra ID (token-based, keyless) and API keys.

### Microsoft Entra ID

Microsoft Entra ID uses OAuth 2.0 bearer tokens scoped to `https://cognitiveservices.azure.com/.default`

.

Use Microsoft Entra ID for:

- Production workloads.
- Conditional access, multifactor authentication (MFA), and just-in-time access.
- Least privilege RBAC and managed identity integration.

Advantages: Fine-grained role assignments, per-principal auditing, controllable token lifetimes, automatic secret hygiene, and managed identities for services.

Limitations: Higher initial setup complexity. Requires understanding of Role-based access control (RBAC). For more on RBAC in Foundry, see [Role-based access control for Microsoft Foundry](rbac-foundry?view=foundry-classic).

### API keys

API keys are static secrets scoped to a Foundry resource.

Use API keys for:

- Rapid prototyping.
- Isolated test environments where single-secret rotation is acceptable.

Advantages: Simple, language agnostic, and doesn't require token acquisition.

Limitations: Cannot express user identity, is difficult to scope granularly, and is harder to audit. Generally not accepted by enterprise production workloads and not recommended by Microsoft.

For more information on enabling keyless authentication, see [Configure key-less authentication with Microsoft Entra ID](../foundry-models/how-to/configure-entra-id?view=foundry-classic).

## Feature support matrix

Reference the following matrix to understand what capabilities in Foundry support API key versus Microsoft Entra ID.

| Capability or feature | API key | Microsoft Entra ID | Notes |
|---|---|---|---|
| Basic model inference (chat, embeddings) | Yes | Yes | Fully supported. |
| Fine-tuning operations | Yes | Yes | Entra ID adds per-principal audit. |
| Agents service | No | Yes | Use Entra ID for managed identity tool access. |
| Evaluations | No | Yes | Use Entra ID. |
| Content safety analyze calls | Yes | Yes | Use RBAC to limit high-risk operations. |
| Batch analysis jobs (Content Understanding) | Yes | Yes | Entra ID recommended for scale. |
| Portal playground usage | Yes | Yes | Playground uses project connection mode. |
| Network isolation with Private Link | Yes | Yes | Entra ID adds conditional access. |
| Least privilege with built-in and custom roles | No | Yes | Keys are all-or-nothing per resource. |
| Managed identity (system or user-assigned) | No | Yes | Enables secret-less auth. |
| Per-request user attribution | No | Yes | Token contains tenant and object IDs. |
| Revocation (immediate) | Rotate key | Remove role or disable principal | Short token lifetime applies. |
| Support in automation pipelines | Yes (secret) | Yes (service principal or managed identity) | Entra ID reduces secret rotation. |
| Assistants API | Yes | Yes | Recommended to use Entra ID. |
| Batch inferencing | Yes | Yes |

## Identity types

Azure resources and applications authenticate by using different identity types, each designed for specific scenarios. User principals represent human users, service principals represent applications or automated processes, and managed identities provide a secure, credential-free way for Azure resources to access other services. Understanding these distinctions helps you choose the right identity for interactive sign-ins, app-to-app communication, or workload automation.

Azure supports the following identity types.

| Identity type | Description |
|---|---|
| User principal | Individual user in Microsoft Entra ID |
|

[Managed identity](/en-us/entra/identity/managed-identities-azure-resources/overview)(system-assigned)## Built-in roles overview

In Foundry, use the built-in roles to separate the allowed actions for a user. Most enterprises want a separation of control and data plane actions for their built-in roles. Others expect a combined data and control plane role to minimize the number of role assignments required. The following table lists scenarios and the corresponding built-in Foundry roles that best fit each scenario.

| Scenario | Typical built-in roles | Notes |
|---|---|---|
| Build agents with pre-deployed models | Azure AI User role | Data plane usage only; no management writes. |
| Manage deployments or fine-tune models | Azure AI Project Manager | Includes model deployment creation and update. |
| Rotate keys or manage resource | Azure AI Account Owner | High privilege; consider custom role for least privilege. |
| Manage resource, manage deployments, build agents. You're a digital native. | Azure AI Owner (role coming soon) | Combine with Azure Monitor Reader if observability required. |
| Observability, tracing, monitoring | Azure AI User (minimum) | Add Azure Monitor Reader on Application Insights. |

To understand the breakdown of built-in roles and the control and data plane actions, review the following diagram.

Tip

Create a custom role if a built-in role grants excess permissions for your use case.

## Set up Microsoft Entra ID

For high-level guidance on setting up Entra ID authentication in Foundry, see [Configure key-less authentication](../foundry-models/how-to/configure-entra-id?view=foundry-classic).

- Ensure your Microsoft Foundry resource has a custom subdomain configured. See
[Custom subdomains](/en-us/azure/ai-services/cognitive-services-custom-subdomains). - Assign the needed built-in or custom role, such as Azure AI User, to each principal user, service principal, or managed identity at the resource or project scope.
- (Optional) For a service principal, create an app registration, add a client secret or certificate, and note the tenant ID, client ID, and secret or certificate.
- (Optional) For a managed identity, enable the system-assigned identity on the calling service or attach a user-assigned identity, then assign a role to it on the Foundry resource.
- Remove key-based authentication after all callers use token authentication. Optionally disable local authentication in deployment templates.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/fine-tuning-overview -->

# Fine-tune models with Microsoft Foundry

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Fine-tuning customizes a pretrained AI model with additional training on a specific task or dataset to improve performance, add new skills, or enhance accuracy. The result is a new, optimized GenAI model based on the provided examples. This article walks you through key concepts and decisions to make before you fine-tune, including the type of fine-tuning that's right for your use case, and model selection criteria based on training techniques use-cases for fine-tuning and how it helps you in your GenAI journey.

If you're just getting started with fine-tuning, we recommend **GPT-4.1** for complex skills like language translation, domain adaptation, or advanced code generation. For more focused tasks (such as classification, sentiment analysis, or content moderation) or when distilling knowledge from a more sophisticated model, start with **GPT-4.1-mini** for faster iteration and lower costs.

## Top use cases for fine-tuning

Fine-tuning excels at customizing language models for specific applications and domains. Some key use cases include:

**Domain Specialization:**Adapt a language model for a specialized field like medicine, finance, or law – where domain specific knowledge and terminology is important. Teach the model to understand technical jargon and provide more accurate responses.**Task Performance:**Optimize a model for a specific task like sentiment analysis, code generation, translation, or summarization. You can significantly improve the performance of a smaller model on a specific application, compared to a general purpose model.**Style and Tone:**Teach the model to match your preferred communication style – for example, adapt the model for formal business writing, brand-specific voice, or technical writing.**Instruction Following:**Improve the model's ability to follow specific formatting requirements, multi-step instructions, or structured outputs. In multi-agent frameworks, teach the model to call the right agent for the right task.**Compliance and Safety:**Train a fine-tuned model to adhere to organizational policies, regulatory requirements, or other guidelines unique to your application.**Language or Cultural Adaptation:**Tailor a language model for a specific language, dialect, or cultural context that may not be well represented in the training data. Fine-tuning is especially valuable when a general-purpose model doesn't meet your specific requirements – but you want to avoid the cost and complexity of training a model from scratch.

## Serverless or Managed Compute?

Before picking a model, it's important to select the fine-tuning product that matches your needs. Microsoft's Foundry offers two primary modalities for fine tuning: serverless and managed compute.

**Serverless**lets you customize models using our capacity with consumption-based pricing starting at $1.70 per million input tokens. We optimize training for speed and scalability while handling all infrastructure management. This approach requires no GPU quotas and provides exclusive access to OpenAI models, though with fewer hyperparameter options than managed compute.**Managed compute**offers a wider range of models and advanced customization through AzureML, but requires you to provide your own VMs for training and hosting. While this gives full control over resources, it demands high quotas that many customers lack, doesn't include OpenAI models, and can't use our multi-tenancy optimizations.

For most customers, serverless provides the best balance of ease-of-use, cost efficiency, and access to premium models. This document focuses on serverless options.

To find steps to fine-tuning a model in Foundry, see [Fine-tune Models in Foundry](../how-to/fine-tune-serverless?view=foundry-classic) or [Fine-tune models using managed compute](../how-to/fine-tune-managed-compute?view=foundry-classic). For detailed guidance on OpenAI fine-tuning see [Fine-tune Azure OpenAI Models](../openai/how-to/fine-tuning?view=foundry-classic).

## Training Techniques

Once you identify a use case, you need to select the appropriate training technique - which guides the model you select for training. We offer three training techniques to optimize your models:

**Supervised Fine-Tuning (SFT):**Foundational technique that trains your model on input-output pairs, teaching it to produce desired responses for specific inputs.*Best for:*Most use cases including domain specialization, task performance, style and tone, following instructions, and language adaptation.*When to use:*Start here for most projects. SFT addresses the broadest number of fine-tuning scenarios and provides reliable results with clear input-output training data.*Supported Models:*GPT 4o, 4o-mini, 4.1, 4.1-mini, 4.1-nano; Llama 2 and Llama 3.1; Phi 4, Phi-4-mini-instruct; Mistral Nemo, Ministral-3B, Mistral Large (2411); NTT Tsuzumi-7b

**Direct Preference Optimization (DPO):**Trains models to prefer certain types of responses over others by learning from comparative feedback, without requiring a separate reward model.*Best for:*Improving response quality, safety, and alignment with human preferences.*When to use:*When you have examples of preferred vs. non-preferred outputs, or when you need to optimize for subjective qualities like helpfulness, harmlessness, or style. Use cases include adapting models to a specific style and tone, or adapting a model to cultural preferences.*Supported Models:*GPT 4o, 4.1, 4.1-mini, 4.1-nano

**Reinforcement Fine-Tuning (RFT):**Uses reinforcement learning to optimize models based on reward signals, allowing for more complex optimization objectives.*Best for:*Complex optimization scenarios where simple input-output pairs aren't sufficient.*When to use:*RFT is ideal for objective domains like mathematics, chemistry, and physics where there are clear right and wrong answers and the model already shows some competency. It works best when lucky guessing is difficult and expert evaluators would consistently agree on an unambiguous, correct answer. Requires more ML expertise to implement effectively.*Supported Models:*o4-mini


Most customers should start with SFT, as it addresses the broadest number of fine-tuning use cases.

Follow this link to view and download [example datasets](https://github.com/Azure-Samples/AIFoundry-Customization-Datasets) to try out fine-tuning.

## Training Modalities

**Text-to-Text (All Models):**All our models support standard text-to-text fine-tuning for language-based tasks.**Vision + Text (GPT 4o, 4.1):**Some models support vision fine-tuning, accepting both image and text inputs while producing text outputs. Use cases for vision fine-tuning include interpreting charts, graphs, and visual data; content moderation; visual quality assessment; document processing with mixed text and image; and product cataloging from photographs.

## Model Comparison Table

This table provides an overview of the models available

| Model | Modalities | Techniques | Strengths |
|---|---|---|---|
| GPT 4.1 | Text, Vision | SFT, DPO | Superior performance on sophisticated tasks, nuanced understanding |
| GPT 4.1-mini | Text | SFT, DPO | Fast iteration, cost-effective, good for simple tasks |
| GPT 4.1-nano | Text | SFT, DPO | Fast, cost-effective, and minimal resource usage |
| GPT 4o | Text, Vision | SFT, DPO | Previous generation flagship model for complex tasks |
| GPT 4o-mini | Text | SFT | Previous generation small model for simple tasks |
| o4-mini | Text | RFT | Reasoning model suited for complex logical tasks |
| Phi 4 | Text | SFT | Cost effective option for simpler tasks |
| Ministral 3B | Text | SFT | Low-cost option for faster iteration |
| Mistral Nemo | Text | SFT | Balance between size and capability |
| Mistral Large (2411) | Text | SFT | Most capable Mistral model, better for complex tasks |

## Get Started with Fine Tuning

**Define your use case:**Identify whether you need a highly capable general-purpose model (e.g. GPT 4.1), a smaller cost-effective model for a specific task (GPT 4.1-mini or nano), or a complex reasoning model (o4-mini).**Prepare your data:**Start with 50-100 high-quality examples for initial testing, scaling to 500+ examples for production models.**Choose your technique:**Begin with Supervised Fine-Tuning (SFT) unless you have specific requirements for reasoning models / RFT.**Iterate and evaluate:**Fine-tuning is an iterative process—start with a baseline, measure performance, and refine your approach based on results.

To find steps to fine-tuning a model in Foundry, see [Fine-tune Models in Foundry](../how-to/fine-tune-serverless?view=foundry-classic), [Fine-tune Azure OpenAI Models](../openai/how-to/fine-tuning?view=foundry-classic), or [Fine-tune models using managed compute](../how-to/fine-tune-managed-compute?view=foundry-classic).

## Fine-Tuning Availability

Now that you know when to use fine-tuning for your use case, you can go to Microsoft Foundry to find models available to fine-tune.

**To fine-tune a Foundry model using Serverless** you must have a hub/project in the region where the model is available for fine tuning. See [Region availability for models in serverless API deployment](../how-to/deploy-models-serverless-availability?view=foundry-classic) for detailed information on model and region availability, and [How to Create a Hub-based project](../how-to/create-projects?view=foundry-classic) to create your project.

**To fine-tune an OpenAI model** you can use an Azure OpenAI Resource, a Foundry resource or default project, or a hub/project. GPT 4.1, 4.1-mini, 4.1-nano and GPT 4o, 4omini are available in all regions with Global Training. For regional availability, see [Regional Availability and Limits for Azure OpenAI Fine Tuning](../openai/concepts/models?view=foundry-classic). See [Create a project for Foundry](../how-to/create-projects?view=foundry-classic) for instructions on creating a new project.

**To fine-tune a model using Managed Compute** you must have a hub/project and available VM quota for training and inferencing. See [Fine-tune models using managed compute (preview)](../how-to/fine-tune-managed-compute?view=foundry-classic) for more details on how to use managed compute fine tuning, and [How to Create a Hub-based project](../how-to/create-projects?view=foundry-classic) to create your project.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/trace -->

# View trace results for AI applications using OpenAI SDK

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Learn how to view trace results that provide visibility into AI application execution. Use traces to diagnose inaccurate tool calls, misleading prompts, latency bottlenecks, and low-quality evaluation scores.

In this article, you learn how to:

- Enable tracing for a project.
- Instrument the OpenAI SDK.
- Capture message content (optional).
- View trace timelines and spans.
- Connect tracing with evaluation loops.

This article explains how to view trace results for AI applications using **OpenAI SDK** with OpenTelemetry in Microsoft Foundry.

## Prerequisites

You need the following to complete this tutorial:

A Foundry project created.

An AI application that uses

**OpenAI SDK**to make calls to models hosted in Foundry.

## Enable tracing in your project

Foundry stores traces in Azure Application Insights using OpenTelemetry. New resources don't provision Application Insights automatically. Associate (or create) a resource once per Foundry resource.

The following steps show how to configure your resource:

Go to

[Foundry portal](https://ai.azure.com/?cid=learnDocs)and navigate to your project.On the side navigation bar, select

**Tracing**.If an Azure Application Insights resource isn't associated with your Foundry resource, associate one. If you already have an Application Insights resource associated, you won't see the enable page below and you can skip this step.

To reuse an existing Azure Application Insights, use the drop-down

**Application Insights resource name**to locate the resource and select**Connect**.Tip

To connect to an existing Azure Application Insights, you need at least contributor access to the Foundry resource (or Hub).

To connect to a new Azure Application Insights resource, select the option

**Create new**.Use the configuration wizard to configure the new resource's name.

By default, the new resource is created in the same resource group where the Foundry resource was created. Use the

**Advance settings**option to configure a different resource group or subscription.Tip

To create a new Azure Application Insights resource, you also need contributor role to the resource group you selected (or the default one).

Select

**Create**to create the resource and connect it to the Foundry resource.

Once the connection is configured, you're ready to use tracing in any project within the resource.


Tip

Make sure you have the

[Log Analytics Reader role](/en-us/azure/azure-monitor/logs/manage-access?tabs=portal#log-analytics-reader)assigned in your Application Insights resource. To learn more on how to assign roles, see[Assign Azure roles using the Azure portal](/en-us/azure/role-based-access-control/role-assignments-portal). Use[Microsoft Entra groups](../../concepts/rbac-foundry?view=foundry-classic#use-microsoft-entra-groups-with-foundry)to more easily manage access for users.Go to the landing page of your project and copy the project's endpoint URI. You need it later.

Important

Using a project's endpoint requires configuring Microsoft Entra ID in your application. If you don't have Entra ID configured, use the Azure Application Insights connection string as indicated in step 3 of the tutorial.


## View trace results in Foundry portal

Once you have tracing configured and your application is instrumented, you can view trace results in the Foundry portal:

Go to

[Foundry portal](https://ai.azure.com/?cid=learnDocs)and navigate to your project.On the side navigation bar, select

**Tracing**.You'll see a list of trace results from your instrumented applications. Each trace shows:

**Trace ID**: Unique identifier for the trace**Start time**: When the trace began**Duration**: How long the operation took**Status**: Success or failure status**Operations**: Number of spans in the trace

Select any trace to view detailed trace results including:

- Complete execution timeline
- Input and output data for each operation
- Performance metrics and timing
- Error details if any occurred
- Custom attributes and metadata


## Instrument the OpenAI SDK

When developing with the OpenAI SDK, you can instrument your code so traces are sent to Foundry. Follow these steps to instrument your code:

Install packages:

`pip install azure-ai-projects azure-monitor-opentelemetry opentelemetry-instrumentation-openai-v2`

(Optional) Capture message content:

- PowerShell:
`setx OTEL_INSTRUMENTATION_GENAI_CAPTURE_MESSAGE_CONTENT true`

- Bash:
`export OTEL_INSTRUMENTATION_GENAI_CAPTURE_MESSAGE_CONTENT=true`


- PowerShell:
Get the connection string for the linked Application Insights resource (Project > Tracing > Manage data source > Connection string):

`from azure.ai.projects import AIProjectClient from azure.identity import DefaultAzureCredential project_client = AIProjectClient( credential=DefaultAzureCredential(), endpoint="https://<your-resource>.services.ai.azure.com/api/projects/<your-project>", ) connection_string = project_client.telemetry.get_application_insights_connection_string()`

Configure Azure Monitor and instrument OpenAI SDK:

`from azure.monitor.opentelemetry import configure_azure_monitor from opentelemetry.instrumentation.openai_v2 import OpenAIInstrumentor configure_azure_monitor(connection_string=connection_string) OpenAIInstrumentor().instrument()`

Send a request:

`client = project_client.get_openai_client() response = client.chat.completions.create( model="gpt-4o-mini", messages=[{"role": "user", "content": "Write a short poem on open telemetry."}], ) print(response.choices[0].message.content)`

Return to

**Tracing**in the portal to view new traces.It might be useful to capture sections of your code that mixes business logic with models when developing complex applications. OpenTelemetry uses the concept of spans to capture sections you're interested in. To start generating your own spans, get an instance of the current

**tracer**object.`from opentelemetry import trace tracer = trace.get_tracer(__name__)`

Then, use decorators in your method to capture specific scenarios in your code that you're interested in. These decorators generate spans automatically. The following code example instruments a method called

`assess_claims_with_context`

that iterates over a list of claims and verifies if the claim is supported by the context using an LLM. All the calls made in this method are captured within the same span:`def build_prompt_with_context(claim: str, context: str) -> str: return [{'role': 'system', 'content': "I will ask you to assess whether a particular scientific claim, based on evidence provided. Output only the text 'True' if the claim is true, 'False' if the claim is false, or 'NEE' if there's not enough evidence."}, {'role': 'user', 'content': f""" The evidence is the following: {context} Assess the following claim on the basis of the evidence. Output only the text 'True' if the claim is true, 'False' if the claim is false, or 'NEE' if there's not enough evidence. Do not output any other text. Claim: {claim} Assessment: """}] @tracer.start_as_current_span("assess_claims_with_context") def assess_claims_with_context(claims, contexts): responses = [] for claim, context in zip(claims, contexts): response = client.chat.completions.create( model="gpt-4.1", messages=build_prompt_with_context(claim=claim, context=context), ) responses.append(response.choices[0].message.content.strip('., ')) return responses`

Trace results look as follows:

You might also want to add extra information to the current span. OpenTelemetry uses the concept of

**attributes**for that. Use the`trace`

object to access them and include extra information. See how the`assess_claims_with_context`

method has been modified to include an attribute:`@tracer.start_as_current_span("assess_claims_with_context") def assess_claims_with_context(claims, contexts): responses = [] current_span = trace.get_current_span() current_span.set_attribute("operation.claims_count", len(claims)) for claim, context in zip(claims, contexts): response = client.chat.completions.create( model="gpt-4.1", messages=build_prompt_with_context(claim=claim, context=context), ) responses.append(response.choices[0].message.content.strip('., ')) return responses`


## Trace to console

It might be useful to also trace your application and send the traces to the local execution console. This approach might be beneficial when running unit tests or integration tests in your application using an automated CI/CD pipeline. Traces can be sent to the console and captured by your CI/CD tool for further analysis.

Configure tracing as follows:

Instrument the OpenAI SDK as usual:

`from opentelemetry.instrumentation.openai_v2 import OpenAIInstrumentor OpenAIInstrumentor().instrument()`

Configure OpenTelemetry to send traces to the console:

`from opentelemetry import trace from opentelemetry.sdk.trace import TracerProvider from opentelemetry.sdk.trace.export import SimpleSpanProcessor, ConsoleSpanExporter span_exporter = ConsoleSpanExporter() tracer_provider = TracerProvider() tracer_provider.add_span_processor(SimpleSpanProcessor(span_exporter)) trace.set_tracer_provider(tracer_provider)`

Use OpenAI SDK as usual:

`response = client.chat.completions.create( model="deepseek-v3-0324", messages=[ {"role": "user", "content": "Write a short poem on open telemetry."}, ], )`

`{ "name": "chat deepseek-v3-0324", "context": { "trace_id": "0xaaaa0a0abb1bcc2cdd3d", "span_id": "0xaaaa0a0abb1bcc2cdd3d", "trace_state": "[]" }, "kind": "SpanKind.CLIENT", "parent_id": null, "start_time": "2025-06-13T00:02:04.271337Z", "end_time": "2025-06-13T00:02:06.537220Z", "status": { "status_code": "UNSET" }, "attributes": { "gen_ai.operation.name": "chat", "gen_ai.system": "openai", "gen_ai.request.model": "deepseek-v3-0324", "server.address": "my-project.services.ai.azure.com", "gen_ai.response.model": "DeepSeek-V3-0324", "gen_ai.response.finish_reasons": [ "stop" ], "gen_ai.response.id": "aaaa0a0abb1bcc2cdd3d", "gen_ai.usage.input_tokens": 14, "gen_ai.usage.output_tokens": 91 }, "events": [], "links": [], "resource": { "attributes": { "telemetry.sdk.language": "python", "telemetry.sdk.name": "opentelemetry", "telemetry.sdk.version": "1.31.1", "service.name": "unknown_service" }, "schema_url": "" } }`


## Trace locally with AI Toolkit

AI Toolkit offers a simple way to trace locally in VS Code. It uses a local OTLP-compatible collector, making it perfect for development and debugging without needing cloud access.

The toolkit supports the OpenAI SDK and other AI frameworks through OpenTelemetry. You can see traces instantly in your development environment.

For detailed setup instructions and SDK-specific code examples, see [Tracing in AI Toolkit](https://code.visualstudio.com/docs/intelligentapps/tracing).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/model-lifecycle-retirement -->

# Model deprecation and retirement for Microsoft Foundry Models

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

Microsoft Foundry Models are continually refreshed with newer and more capable models. As part of this process, model providers might deprecate and retire their older models, and you might need to update your applications to use a newer model. This document communicates information about the model lifecycle and deprecation timelines and explains how you're informed of model lifecycle stages.

This article covers general deprecation and retirement information for Foundry Models. For details specific to Azure OpenAI in Foundry Models, see [Azure OpenAI in Foundry Models model deprecations and retirements](../openai/concepts/model-retirements?view=foundry-classic).

## Model lifecycle stages

Models in the model catalog belong to one of these stages:

- Preview
- Generally available
- Legacy
- Deprecated
- Retired

### Preview

Models labeled *Preview* are experimental in nature. A model's weights, runtime, and API schema can change while the model is in preview. Models in preview aren't guaranteed to become generally available. Models in preview have a *Preview* label next to their name in the model catalog.

### Generally available (GA)

This stage is the default model stage. Models that don't include a lifecycle label next to their name are GA and suitable for use in production environments. In this stage, model weights and APIs are fixed. However, model containers or runtimes with vulnerabilities might get patched, but patches don't affect model outputs.

### Legacy

Models labeled *Legacy* are intended for deprecation. You should plan to move to a different model, such as a new, improved model that might be available in the same model family. While a model is in the legacy stage, existing deployments of the model continue to work, and you can create new deployments of the model until the deprecation date.

### Deprecated

Models labeled *Deprecated* are no longer available for new deployments. You can't create any new deployments for the model; however, existing deployments continue to work until the retirement date.

### Retired

Models labeled *Retired* are no longer available for use. You can't create new deployments, and attempts to use existing deployments return `<return code>`

errors.

## Notifications for Foundry Models

Customers that have Foundry Model deployments receive notifications for upcoming model retirements according to the following schedule:

Models are labeled as

*Legacy*and remain in the legacy state for at least 30 days before being moved to the deprecated state. During this notification period, you can create new deployments as you prepare for deprecation and retirement.Models are labeled

*Deprecated*and remain in the deprecated state for at least 90 days before being moved to the retired state. During this notification period, you can migrate any existing deployments to newer or replacement models.

For each subscription that has a model deployed as a serverless API deployment or deployed to a Foundry resource, members of the *owner*, *contributor*, *reader*, *monitoring contributor*, and *monitoring reader* roles receive a notification when a model deprecation is announced. The notification contains the dates when the model enters legacy, deprecated, and retired states. The notification might provide information about possible replacement model options, if applicable.

## Notifications for Azure OpenAI in Foundry Models

For Azure OpenAI models, customers with active Azure OpenAI deployments receive notice for models with upcoming retirement as follows:

- At model launch, we programmatically designate a "not sooner than" retirement date (typically one year out).
- At least 60 days notice before model retirement for Generally Available (GA) models.
- At least 30 days notice before preview model version upgrades.

Members of the *owner*, *contributor*, *reader*, *monitoring contributor*, and *monitoring reader* roles receive notification for each subscription with a deployment of a model that has an upcoming retirement.

Retirements are done on a rolling basis, region by region. Notifications are sent from an unmonitored mailbox, `azure-noreply@microsoft.com`

.

To learn more about the Azure OpenAI models lifecycle, including information for current, deprecated, and retired models, see [Azure OpenAI in Foundry Models model deprecations and retirements](../openai/concepts/model-retirements?view=foundry-classic).

## Timelines for Foundry Models

The following tables list the timelines for models that are on track for retirement. The specified dates are in UTC time.

#### AI21 Labs

| Model | Legacy date (UTC) | Deprecation date (UTC) | Retirement date (UTC) | Suggested replacement model |
|---|---|---|---|---|
| Jamba Instruct | February 1, 2025 | February 1, 2025 | March 1, 2025 | N/A |
|

[AI21-Jamba-1.5-Mini](https://ai.azure.com/explore/models/AI21-Jamba-1.5-Mini/version/1/registry/azureml-ai21/?cid=learnDocs)#### Bria

| Model | Legacy date (UTC) | Deprecation date (UTC) | Retirement date (UTC) | Suggested replacement model |
|---|---|---|---|---|
|

#### Cohere

| Model | Legacy date (UTC) | Deprecation date (UTC) | Retirement date (UTC) | Suggested replacement model |
|---|---|---|---|---|
|

[Cohere Command R 08-2024](https://aka.ms/azureai/landing/Cohere-command-r-08-2024?cid=learnDocs)[Command R+](https://ai.azure.com/explore/models/Cohere-command-r-plus/version/1/registry/azureml-cohere?cid=learnDocs)[Cohere Command R+ 08-2024](https://aka.ms/azureai/landing/Cohere-command-r-plus-08-2024?cid=learnDocs)[Cohere-rerank-v3-english](https://ai.azure.com/explore/models/Cohere-rerank-v3-english/version/1/registry/azureml-cohere/?cid=learnDocs)[Cohere-rerank-v4.0-pro](https://ai.azure.com/resource/models/Cohere-rerank-v4.0-pro/version/1/registry/azureml-cohere/?cid=learnDocs),[Cohere-rerank-v4.0-fast](https://ai.azure.com/resource/models/Cohere-rerank-v4.0-fast/version/2/registry/azureml-cohere/?cid=learnDocs)[Cohere-rerank-v3-multilingual](https://ai.azure.com/explore/models/Cohere-rerank-v3-multilingual/version/1/registry/azureml-cohere/?cid=learnDocs)[Cohere-rerank-v4.0-pro](https://ai.azure.com/resource/models/Cohere-rerank-v4.0-pro/version/1/registry/azureml-cohere/?cid=learnDocs),[Cohere-rerank-v4.0-fast](https://ai.azure.com/resource/models/Cohere-rerank-v4.0-fast/version/2/registry/azureml-cohere/?cid=learnDocs)[Cohere-rerank-v3.5](https://ai.azure.com/explore/models/Cohere-rerank-v3.5/version/1/registry/azureml-cohere/?cid=learnDocs)[Cohere-rerank-v4.0-pro](https://ai.azure.com/resource/models/Cohere-rerank-v4.0-pro/version/1/registry/azureml-cohere/?cid=learnDocs),[Cohere-rerank-v4.0-fast](https://ai.azure.com/resource/models/Cohere-rerank-v4.0-fast/version/2/registry/azureml-cohere/?cid=learnDocs)#### Core42

| Model | Legacy date (UTC) | Deprecation date (UTC) | Retirement date (UTC) | Suggested replacement model |
|---|---|---|---|---|
|

#### DeepSeek

| Model | Legacy date (UTC) | Deprecation date (UTC) | Retirement date (UTC) | Suggested replacement model |
|---|---|---|---|---|
|

[DeepSeek-V3-0324](https://aka.ms/azureai/landing/DeepSeek-V3-0324?cid=learnDocs)#### Gretel

| Model | Legacy date (UTC) | Deprecation date (UTC) | Retirement date (UTC) | Suggested replacement model |
|---|---|---|---|---|
|

#### Meta

| Model | Legacy date (UTC) | Deprecation date (UTC) | Retirement date (UTC) | Suggested replacement model |
|---|---|---|---|---|
|

[Meta-Llama-3.1-8B-Instruct](https://ai.azure.com/explore/models/Meta-Llama-3.1-8B-Instruct/version/4/registry/azureml-meta/?cid=learnDocs)[Llama-2-13b-chat](https://ai.azure.com/explore/models/Llama-2-13b-chat/version/22/registry/azureml-meta/?cid=learnDocs)[Meta-Llama-3.1-8B-Instruct](https://ai.azure.com/explore/models/Meta-Llama-3.1-8B-Instruct/version/4/registry/azureml-meta/?cid=learnDocs)[Llama-2-70b](https://ai.azure.com/explore/models/Llama-2-70b/version/25/registry/azureml-meta/?cid=learnDocs)[Llama-3.3-70B-Instruct](https://ai.azure.com/explore/models/Llama-3.3-70B-Instruct/version/4/registry/azureml-meta/?cid=learnDocs)[Llama-2-70b-chat](https://ai.azure.com/explore/models/Llama-2-70b-chat/version/22/registry/azureml-meta/?cid=learnDocs)[Llama-3.3-70B-Instruct](https://ai.azure.com/explore/models/Llama-3.3-70B-Instruct/version/4/registry/azureml-meta/?cid=learnDocs)[Llama-2-7b](https://ai.azure.com/explore/models/Llama-2-7b/version/23/registry/azureml-meta/?cid=learnDocs)[Meta-Llama-3.1-8B-Instruct](https://ai.azure.com/explore/models/Meta-Llama-3.1-8B-Instruct/version/4/registry/azureml-meta/?cid=learnDocs)[Llama-2-7b-chat](https://ai.azure.com/explore/models/Llama-2-7b-chat/version/27/registry/azureml-meta/?cid=learnDocs)[Meta-Llama-3.1-8B-Instruct](https://ai.azure.com/explore/models/Meta-Llama-3.1-8B-Instruct/version/4/registry/azureml-meta/?cid=learnDocs)[Meta-Llama-3-70B-Instruct](https://ai.azure.com/explore/models/Meta-Llama-3-70B-Instruct/version/9/registry/azureml-meta/?cid=learnDocs)[Llama-3.3-70B-Instruct](https://ai.azure.com/explore/models/Llama-3.3-70B-Instruct/version/4/registry/azureml-meta/?cid=learnDocs)[Meta-Llama-3-8B-Instruct](https://ai.azure.com/explore/models/Meta-Llama-3-8B-Instruct/version/9/registry/azureml-meta/?cid=learnDocs)[Meta-Llama-3.1-8B-Instruct](https://ai.azure.com/explore/models/Meta-Llama-3.1-8B-Instruct/version/4/registry/azureml-meta/?cid=learnDocs)[Meta-Llama-3.1-70B-Instruct](https://ai.azure.com/explore/models/Meta-Llama-3.1-70B-Instruct/version/4/registry/azureml-meta/?cid=learnDocs)[Llama-3.3-70B-Instruct](https://ai.azure.com/explore/models/Llama-3.3-70B-Instruct/version/4/registry/azureml-meta/?cid=learnDocs)#### Microsoft

| Model | Legacy date (UTC) | Deprecation date (UTC) | Retirement date (UTC) | Suggested replacement model |
|---|---|---|---|---|
|

[Phi-3-medium-4k-instruct](https://ai.azure.com/explore/models/Phi-3-medium-4k-instruct/version/6/registry/azureml/?cid=learnDocs)[Phi-4](https://ai.azure.com/explore/models/Phi-4/version/8/registry/azureml/?cid=learnDocs)[Phi-3-medium-128k-instruct](https://ai.azure.com/explore/models/Phi-3-medium-128k-instruct/version/7/registry/azureml/?cid=learnDocs)[Phi-4](https://ai.azure.com/explore/models/Phi-4/version/8/registry/azureml/?cid=learnDocs)[Phi-3-mini-4k-instruct](https://ai.azure.com/explore/models/Phi-3-mini-4k-instruct/version/15/registry/azureml/?cid=learnDocs)[Phi-4-mini-instruct](https://ai.azure.com/explore/models/Phi-4-mini-instruct/version/1/registry/azureml/?cid=learnDocs)[Phi-3-mini-128k-instruct](https://ai.azure.com/explore/models/Phi-3-mini-128k-instruct/version/13/registry/azureml/?cid=learnDocs)[Phi-4-mini-instruct](https://ai.azure.com/explore/models/Phi-4-mini-instruct/version/1/registry/azureml/?cid=learnDocs)[Phi-3-small-8k-instruct](https://ai.azure.com/explore/models/Phi-3-small-8k-instruct/version/6/registry/azureml/?cid=learnDocs)[Phi-4-mini-instruct](https://ai.azure.com/explore/models/Phi-4-mini-instruct/version/1/registry/azureml/?cid=learnDocs)[Phi-3-small-128k-instruct](https://ai.azure.com/explore/models/Phi-3-small-128k-instruct/version/5/registry/azureml/?cid=learnDocs)[Phi-4-mini-instruct](https://ai.azure.com/explore/models/Phi-4-mini-instruct/version/1/registry/azureml/?cid=learnDocs)[Phi-3.5-mini-instruct](https://ai.azure.com/explore/models/Phi-3.5-mini-instruct/version/6/registry/azureml/?cid=learnDocs)[Phi-4-mini-instruct](https://ai.azure.com/explore/models/Phi-4-mini-instruct/version/1/registry/azureml/?cid=learnDocs)[Phi-3.5-MoE-instruct](https://ai.azure.com/explore/models/Phi-3.5-MoE-instruct/version/5/registry/azureml/?cid=learnDocs)[Phi-4-mini-instruct](https://ai.azure.com/explore/models/Phi-4-mini-instruct/version/1/registry/azureml/?cid=learnDocs)[Phi-3.5-vision-instruct](https://ai.azure.com/explore/models/Phi-3.5-vision-instruct/version/2/registry/azureml/?cid=learnDocs)[Phi-4-mini-instruct](https://ai.azure.com/explore/models/Phi-4-mini-instruct/version/1/registry/azureml/?cid=learnDocs)#### Mistral AI

| Model | Legacy date (UTC) | Deprecation date (UTC) | Retirement date (UTC) | Suggested replacement model |
|---|---|---|---|---|
|

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/models-featured -->

# Serverless API inference examples for Foundry Models

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

The Foundry model catalog offers a large selection of Microsoft Foundry Models from a wide range of providers. You have various options for deploying models from the model catalog. This article lists inference examples for serverless API deployments.

Important

Models that are in preview are marked as *preview* on their model cards in the model catalog.

To perform inferencing with the models, some models such as [Nixtla's TimeGEN-1](#nixtla) and [Cohere rerank](#cohere-rerank) require you to use custom APIs from the model providers. Others support inferencing using the [Model Inference API](../model-inference/overview?view=foundry-classic). You can find more details about individual models by reviewing their model cards in the [model catalog for Foundry portal](https://ai.azure.com/explore/models).

## Cohere

The Cohere family of models includes various models optimized for different use cases, including rerank, chat completions, and embeddings models.

#### Inference examples: Cohere command and embed

The following table provides links to examples of how to use Cohere models.

| Description | Language | Sample |
|---|---|---|
| Web requests | Bash |
|

[Link](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/ai/Azure.AI.Inference/samples)[Link](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/ai/ai-inference-rest/samples)[Link](https://aka.ms/azsdk/azure-ai-inference/python/samples)[Link](https://aka.ms/samples/cohere-command/openaisdk)[Link](https://aka.ms/samples/cohere/langchain)[Command](https://aka.ms/samples/cohere-python-sdk)[Embed](https://aka.ms/samples/cohere-embed/cohere-python-sdk)[Link](https://github.com/Azure/azureml-examples/blob/main/sdk/python/foundation-models/cohere/litellm.ipynb)#### Retrieval Augmented Generation (RAG) and tool use samples: Cohere command and embed

| Description | Packages | Sample |
|---|---|---|
| Create a local Facebook AI similarity search (FAISS) vector index, using Cohere embeddings - Langchain | `langchain` , `langchain_cohere` |
|

`langchain`

, `langchain_cohere`

[command_faiss_langchain.ipynb](https://github.com/Azure/azureml-examples/blob/main/sdk/python/foundation-models/cohere/command_faiss_langchain.ipynb)`langchain`

, `langchain_cohere`

[cohere-aisearch-langchain-rag.ipynb](https://github.com/Azure/azureml-examples/blob/main/sdk/python/foundation-models/cohere/cohere-aisearch-langchain-rag.ipynb)`cohere`

, `azure_search_documents`

[cohere-aisearch-rag.ipynb](https://github.com/Azure/azureml-examples/blob/main/sdk/python/foundation-models/cohere/cohere-aisearch-rag.ipynb)`cohere`

, `langchain`

, `langchain_cohere`

[command_tools-langchain.ipynb](https://github.com/Azure/azureml-examples/blob/main/sdk/python/foundation-models/cohere/command_tools-langchain.ipynb)### Cohere rerank

To perform inferencing with Cohere rerank models, you're required to use Cohere's custom rerank APIs. For more information on the Cohere rerank model and its capabilities, see [Cohere rerank](../foundry-models/concepts/models?view=foundry-classic#cohere-rerank).

#### Pricing for Cohere rerank models

*Queries*, not to be confused with a user's query, is a pricing meter that refers to the cost associated with the tokens used as input for inference of a Cohere Rerank model. Cohere counts a single search unit as a query with up to 100 documents to be ranked. Documents longer than 500 tokens (for Cohere-rerank-v3.5) or longer than 4096 tokens (for Cohere-rerank-v3-English and Cohere-rerank-v3-multilingual) when including the length of the search query are split up into multiple chunks, where each chunk counts as a single document.

See the [Cohere model collection in Foundry portal](https://ai.azure.com/explore/models?&selectedCollection=Cohere).

## Core42

The following table provides links to examples of how to use Jais models.

| Description | Language | Sample |
|---|---|---|
| Azure AI Inference package for C# | C# |
|

[Link](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/ai/ai-inference-rest/samples)[Link](https://aka.ms/azsdk/azure-ai-inference/python/samples)## DeepSeek

DeepSeek family of models includes DeepSeek-R1, which excels at reasoning tasks using a step-by-step training process, such as language, scientific reasoning, and coding tasks, DeepSeek-V3-0324, a Mixture-of-Experts (MoE) language model, and more.

The following table provides links to examples of how to use DeepSeek models.

| Description | Language | Sample |
|---|---|---|
| Azure AI Inference package for Python | Python |
|

[Link](https://aka.ms/azsdk/azure-ai-inference/javascript/samples)[Link](https://aka.ms/azsdk/azure-ai-inference/csharp/samples)[Link](https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/ai/azure-ai-inference/src/samples)## Meta

Meta Llama models and tools are a collection of pretrained and fine-tuned generative AI text and image reasoning models. Meta models range is scale to include:

- Small language models (SLMs) like 1B and 3B Base and Instruct models for on-device and edge inferencing
- Mid-size large language models (LLMs) like 7B, 8B, and 70B Base and Instruct models
- High-performant models like Meta Llama 3.1-405B Instruct for synthetic data generation and distillation use cases.
- High-performant natively multimodal models, Llama 4 Scout and Llama 4 Maverick, leverage a mixture-of-experts architecture to offer industry-leading performance in text and image understanding.

The following table provides links to examples of how to use Meta Llama models.

| Description | Language | Sample |
|---|---|---|
| CURL request | Bash |
|

[Link](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/ai/Azure.AI.Inference/samples)[Link](https://github.com/Azure/azureml-examples/blob/main/sdk/typescript/README.md)[Link](https://aka.ms/azsdk/azure-ai-inference/python/samples)[Link](https://aka.ms/meta-llama-3.1-405B-instruct-webrequests)[Link](https://aka.ms/meta-llama-3.1-405B-instruct-openai)[Link](https://aka.ms/meta-llama-3.1-405B-instruct-langchain)[Link](https://aka.ms/meta-llama-3.1-405B-instruct-litellm)## Microsoft

Microsoft models include various model groups such as MAI models, Phi models, healthcare AI models, and more. To see all the available Microsoft models, view [the Microsoft model collection in Foundry portal](https://ai.azure.com/explore/models?&selectedCollection=Microsoft).

The following table provides links to examples of how to use Microsoft models.

| Description | Language | Sample |
|---|---|---|
| Azure AI Inference package for C# | C# |
|

[Link](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/ai/ai-inference-rest/samples)[Link](https://aka.ms/azsdk/azure-ai-inference/python/samples)[Link](https://aka.ms/azureai/langchain)[Link](https://aka.ms/azureai/llamaindex)See [the Microsoft model collection in Foundry portal](https://ai.azure.com/explore/models?&selectedCollection=Microsoft).

## Mistral AI

Mistral AI offers two categories of models, namely:

*Premium models*: These include Mistral Large, Mistral Small, Mistral-OCR-2503, Mistral Medium 3 (25.05), and Ministral 3B models, and are available as serverless APIs with pay-as-you-go token-based billing.*Open models*: These include Mistral-small-2503, Codestral, and Mistral Nemo (that are available as serverless APIs with pay-as-you-go token-based billing), and Mixtral-8x7B-Instruct-v01, Mixtral-8x7B-v01, Mistral-7B-Instruct-v01, and Mistral-7B-v01(that are available to download and run on self-hosted managed endpoints).

The following table provides links to examples of how to use Mistral models.

| Description | Language | Sample |
|---|---|---|
| CURL request | Bash |
|

[Link](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/ai/Azure.AI.Inference/samples)[Link](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/ai/ai-inference-rest/samples)[Link](https://aka.ms/azsdk/azure-ai-inference/python/samples)[Link](https://aka.ms/mistral-large/webrequests-sample)[Mistral - OpenAI SDK sample](https://aka.ms/mistral-large/openaisdk)[Mistral - LangChain sample](https://aka.ms/mistral-large/langchain-sample)[Mistral - Mistral AI sample](https://aka.ms/mistral-large/mistralai-sample)[Mistral - LiteLLM sample](https://aka.ms/mistral-large/litellm-sample)## Nixtla

Nixtla's TimeGEN-1 is a generative pre-trained forecasting and anomaly detection model for time series data. TimeGEN-1 can produce accurate forecasts for new time series without training, using only historical values and exogenous covariates as inputs.

To perform inferencing, TimeGEN-1 requires you to use Nixtla's custom inference API. For more information on the TimeGEN-1 model and its capabilities, see [Nixtla](../foundry-models/concepts/models?view=foundry-classic#nixtla).

#### Estimate the number of tokens needed

Before you create a TimeGEN-1 deployment, it's useful to estimate the number of tokens that you plan to consume and be billed for. One token corresponds to one data point in your input dataset or output dataset.

Suppose you have the following input time series dataset:

| Unique_id | Timestamp | Target Variable | Exogenous Variable 1 | Exogenous Variable 2 |
|---|---|---|---|---|
| BE | 2016-10-22 00:00:00 | 70.00 | 49593.0 | 57253.0 |
| BE | 2016-10-22 01:00:00 | 37.10 | 46073.0 | 51887.0 |

To determine the number of tokens, multiply the number of rows (in this example, two) and the number of columns used for forecasting—not counting the unique_id and timestamp columns (in this example, three) to get a total of six tokens.

Given the following output dataset:

| Unique_id | Timestamp | Forecasted Target Variable |
|---|---|---|
| BE | 2016-10-22 02:00:00 | 46.57 |
| BE | 2016-10-22 03:00:00 | 48.57 |

You can also determine the number of tokens by counting the number of data points returned after data forecasting. In this example, the number of tokens is two.

#### Estimate pricing based on tokens

There are four pricing meters that determine the price you pay. These meters are as follows:

| Pricing Meter | Description |
|---|---|
| paygo-inference-input-tokens | Costs associated with the tokens used as input for inference when finetune_steps = 0 |
| paygo-inference-output-tokens | Costs associated with the tokens used as output for inference when finetune_steps = 0 |
| paygo-finetuned-model-inference-input-tokens | Costs associated with the tokens used as input for inference when finetune_steps > 0 |
| paygo-finetuned-model-inference-output-tokens | Costs associated with the tokens used as output for inference when finetune_steps > 0 |

See the [Nixtla model collection in Foundry portal](https://ai.azure.com/explore/models?&selectedCollection=Nixtla).

## Stability AI

Stability AI models deployed via serverless API deployment implement the Model Inference API on the route `/image/generations`

.
For examples of how to use Stability AI models, see the following examples:

[Use OpenAI SDK with Stability AI models for text to image requests](https://github.com/Azure/azureml-examples/blob/main/sdk/python/foundation-models/stabilityai/Text_to_Image_openai_library.ipynb)[Use Requests library with Stability AI models for text to image requests](https://github.com/Azure/azureml-examples/blob/main/sdk/python/foundation-models/stabilityai/Text_to_Image_requests_library.ipynb)[Use Requests library with Stable Diffusion 3.5 Large for image to image requests](https://github.com/Azure/azureml-examples/blob/main/sdk/python/foundation-models/stabilityai/Image_to_Image.ipynb)[Example of a fully encoded image generation response](https://github.com/Azure/azureml-examples/blob/main/sdk/python/foundation-models/stabilityai/Sample_image_generation_response.txt)

## Gretel Navigator

Gretel Navigator employs a compound AI architecture specifically engineered for synthetic data, by combining top open-source small language models (SLMs) fine-tuned across more than 10 industry domains. This purpose-built system creates diverse, domain-specific datasets at scales of hundreds to millions of examples. The system also preserves complex statistical relationships and offers increased speed and accuracy compared to manual data creation.

| Description | Language | Sample |
|---|---|---|
| Azure AI Inference package for JavaScript | JavaScript |
|

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/models-inference-examples -->

# Serverless API inference examples for Foundry Models

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

The Foundry model catalog offers a large selection of Microsoft Foundry Models from a wide range of providers. You have various options for deploying models from the model catalog. This article lists inference examples for serverless API deployments.

Important

Models that are in preview are marked as *preview* on their model cards in the model catalog.

To perform inferencing with the models, some models such as [Nixtla's TimeGEN-1](#nixtla) and [Cohere rerank](#cohere-rerank) require you to use custom APIs from the model providers. Others support inferencing using the [Model Inference API](../model-inference/overview?view=foundry-classic). You can find more details about individual models by reviewing their model cards in the [model catalog for Foundry portal](https://ai.azure.com/explore/models).

## Cohere

The Cohere family of models includes various models optimized for different use cases, including rerank, chat completions, and embeddings models.

#### Inference examples: Cohere command and embed

The following table provides links to examples of how to use Cohere models.

| Description | Language | Sample |
|---|---|---|
| Web requests | Bash |
|

[Link](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/ai/Azure.AI.Inference/samples)[Link](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/ai/ai-inference-rest/samples)[Link](https://aka.ms/azsdk/azure-ai-inference/python/samples)[Link](https://aka.ms/samples/cohere-command/openaisdk)[Link](https://aka.ms/samples/cohere/langchain)[Command](https://aka.ms/samples/cohere-python-sdk)[Embed](https://aka.ms/samples/cohere-embed/cohere-python-sdk)[Link](https://github.com/Azure/azureml-examples/blob/main/sdk/python/foundation-models/cohere/litellm.ipynb)#### Retrieval Augmented Generation (RAG) and tool use samples: Cohere command and embed

| Description | Packages | Sample |
|---|---|---|
| Create a local Facebook AI similarity search (FAISS) vector index, using Cohere embeddings - Langchain | `langchain` , `langchain_cohere` |
|

`langchain`

, `langchain_cohere`

[command_faiss_langchain.ipynb](https://github.com/Azure/azureml-examples/blob/main/sdk/python/foundation-models/cohere/command_faiss_langchain.ipynb)`langchain`

, `langchain_cohere`

[cohere-aisearch-langchain-rag.ipynb](https://github.com/Azure/azureml-examples/blob/main/sdk/python/foundation-models/cohere/cohere-aisearch-langchain-rag.ipynb)`cohere`

, `azure_search_documents`

[cohere-aisearch-rag.ipynb](https://github.com/Azure/azureml-examples/blob/main/sdk/python/foundation-models/cohere/cohere-aisearch-rag.ipynb)`cohere`

, `langchain`

, `langchain_cohere`

[command_tools-langchain.ipynb](https://github.com/Azure/azureml-examples/blob/main/sdk/python/foundation-models/cohere/command_tools-langchain.ipynb)### Cohere rerank

To perform inferencing with Cohere rerank models, you're required to use Cohere's custom rerank APIs. For more information on the Cohere rerank model and its capabilities, see [Cohere rerank](../foundry-models/concepts/models?view=foundry-classic#cohere-rerank).

#### Pricing for Cohere rerank models

*Queries*, not to be confused with a user's query, is a pricing meter that refers to the cost associated with the tokens used as input for inference of a Cohere Rerank model. Cohere counts a single search unit as a query with up to 100 documents to be ranked. Documents longer than 500 tokens (for Cohere-rerank-v3.5) or longer than 4096 tokens (for Cohere-rerank-v3-English and Cohere-rerank-v3-multilingual) when including the length of the search query are split up into multiple chunks, where each chunk counts as a single document.

See the [Cohere model collection in Foundry portal](https://ai.azure.com/explore/models?&selectedCollection=Cohere).

## Core42

The following table provides links to examples of how to use Jais models.

| Description | Language | Sample |
|---|---|---|
| Azure AI Inference package for C# | C# |
|

[Link](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/ai/ai-inference-rest/samples)[Link](https://aka.ms/azsdk/azure-ai-inference/python/samples)## DeepSeek

DeepSeek family of models includes DeepSeek-R1, which excels at reasoning tasks using a step-by-step training process, such as language, scientific reasoning, and coding tasks, DeepSeek-V3-0324, a Mixture-of-Experts (MoE) language model, and more.

The following table provides links to examples of how to use DeepSeek models.

| Description | Language | Sample |
|---|---|---|
| Azure AI Inference package for Python | Python |
|

[Link](https://aka.ms/azsdk/azure-ai-inference/javascript/samples)[Link](https://aka.ms/azsdk/azure-ai-inference/csharp/samples)[Link](https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/ai/azure-ai-inference/src/samples)## Meta

Meta Llama models and tools are a collection of pretrained and fine-tuned generative AI text and image reasoning models. Meta models range is scale to include:

- Small language models (SLMs) like 1B and 3B Base and Instruct models for on-device and edge inferencing
- Mid-size large language models (LLMs) like 7B, 8B, and 70B Base and Instruct models
- High-performant models like Meta Llama 3.1-405B Instruct for synthetic data generation and distillation use cases.
- High-performant natively multimodal models, Llama 4 Scout and Llama 4 Maverick, leverage a mixture-of-experts architecture to offer industry-leading performance in text and image understanding.

The following table provides links to examples of how to use Meta Llama models.

| Description | Language | Sample |
|---|---|---|
| CURL request | Bash |
|

[Link](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/ai/Azure.AI.Inference/samples)[Link](https://github.com/Azure/azureml-examples/blob/main/sdk/typescript/README.md)[Link](https://aka.ms/azsdk/azure-ai-inference/python/samples)[Link](https://aka.ms/meta-llama-3.1-405B-instruct-webrequests)[Link](https://aka.ms/meta-llama-3.1-405B-instruct-openai)[Link](https://aka.ms/meta-llama-3.1-405B-instruct-langchain)[Link](https://aka.ms/meta-llama-3.1-405B-instruct-litellm)## Microsoft

Microsoft models include various model groups such as MAI models, Phi models, healthcare AI models, and more. To see all the available Microsoft models, view [the Microsoft model collection in Foundry portal](https://ai.azure.com/explore/models?&selectedCollection=Microsoft).

The following table provides links to examples of how to use Microsoft models.

| Description | Language | Sample |
|---|---|---|
| Azure AI Inference package for C# | C# |
|

[Link](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/ai/ai-inference-rest/samples)[Link](https://aka.ms/azsdk/azure-ai-inference/python/samples)[Link](https://aka.ms/azureai/langchain)[Link](https://aka.ms/azureai/llamaindex)See [the Microsoft model collection in Foundry portal](https://ai.azure.com/explore/models?&selectedCollection=Microsoft).

## Mistral AI

Mistral AI offers two categories of models, namely:

*Premium models*: These include Mistral Large, Mistral Small, Mistral-OCR-2503, Mistral Medium 3 (25.05), and Ministral 3B models, and are available as serverless APIs with pay-as-you-go token-based billing.*Open models*: These include Mistral-small-2503, Codestral, and Mistral Nemo (that are available as serverless APIs with pay-as-you-go token-based billing), and Mixtral-8x7B-Instruct-v01, Mixtral-8x7B-v01, Mistral-7B-Instruct-v01, and Mistral-7B-v01(that are available to download and run on self-hosted managed endpoints).

The following table provides links to examples of how to use Mistral models.

| Description | Language | Sample |
|---|---|---|
| CURL request | Bash |
|

[Link](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/ai/Azure.AI.Inference/samples)[Link](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/ai/ai-inference-rest/samples)[Link](https://aka.ms/azsdk/azure-ai-inference/python/samples)[Link](https://aka.ms/mistral-large/webrequests-sample)[Mistral - OpenAI SDK sample](https://aka.ms/mistral-large/openaisdk)[Mistral - LangChain sample](https://aka.ms/mistral-large/langchain-sample)[Mistral - Mistral AI sample](https://aka.ms/mistral-large/mistralai-sample)[Mistral - LiteLLM sample](https://aka.ms/mistral-large/litellm-sample)## Nixtla

Nixtla's TimeGEN-1 is a generative pre-trained forecasting and anomaly detection model for time series data. TimeGEN-1 can produce accurate forecasts for new time series without training, using only historical values and exogenous covariates as inputs.

To perform inferencing, TimeGEN-1 requires you to use Nixtla's custom inference API. For more information on the TimeGEN-1 model and its capabilities, see [Nixtla](../foundry-models/concepts/models?view=foundry-classic#nixtla).

#### Estimate the number of tokens needed

Before you create a TimeGEN-1 deployment, it's useful to estimate the number of tokens that you plan to consume and be billed for. One token corresponds to one data point in your input dataset or output dataset.

Suppose you have the following input time series dataset:

| Unique_id | Timestamp | Target Variable | Exogenous Variable 1 | Exogenous Variable 2 |
|---|---|---|---|---|
| BE | 2016-10-22 00:00:00 | 70.00 | 49593.0 | 57253.0 |
| BE | 2016-10-22 01:00:00 | 37.10 | 46073.0 | 51887.0 |

To determine the number of tokens, multiply the number of rows (in this example, two) and the number of columns used for forecasting—not counting the unique_id and timestamp columns (in this example, three) to get a total of six tokens.

Given the following output dataset:

| Unique_id | Timestamp | Forecasted Target Variable |
|---|---|---|
| BE | 2016-10-22 02:00:00 | 46.57 |
| BE | 2016-10-22 03:00:00 | 48.57 |

You can also determine the number of tokens by counting the number of data points returned after data forecasting. In this example, the number of tokens is two.

#### Estimate pricing based on tokens

There are four pricing meters that determine the price you pay. These meters are as follows:

| Pricing Meter | Description |
|---|---|
| paygo-inference-input-tokens | Costs associated with the tokens used as input for inference when finetune_steps = 0 |
| paygo-inference-output-tokens | Costs associated with the tokens used as output for inference when finetune_steps = 0 |
| paygo-finetuned-model-inference-input-tokens | Costs associated with the tokens used as input for inference when finetune_steps > 0 |
| paygo-finetuned-model-inference-output-tokens | Costs associated with the tokens used as output for inference when finetune_steps > 0 |

See the [Nixtla model collection in Foundry portal](https://ai.azure.com/explore/models?&selectedCollection=Nixtla).

## Stability AI

Stability AI models deployed via serverless API deployment implement the Model Inference API on the route `/image/generations`

.
For examples of how to use Stability AI models, see the following examples:

[Use OpenAI SDK with Stability AI models for text to image requests](https://github.com/Azure/azureml-examples/blob/main/sdk/python/foundation-models/stabilityai/Text_to_Image_openai_library.ipynb)[Use Requests library with Stability AI models for text to image requests](https://github.com/Azure/azureml-examples/blob/main/sdk/python/foundation-models/stabilityai/Text_to_Image_requests_library.ipynb)[Use Requests library with Stable Diffusion 3.5 Large for image to image requests](https://github.com/Azure/azureml-examples/blob/main/sdk/python/foundation-models/stabilityai/Image_to_Image.ipynb)[Example of a fully encoded image generation response](https://github.com/Azure/azureml-examples/blob/main/sdk/python/foundation-models/stabilityai/Sample_image_generation_response.txt)

## Gretel Navigator

Gretel Navigator employs a compound AI architecture specifically engineered for synthetic data, by combining top open-source small language models (SLMs) fine-tuned across more than 10 industry domains. This purpose-built system creates diverse, domain-specific datasets at scales of hundreds to millions of examples. The system also preserves complex statistical relationships and offers increased speed and accuracy compared to manual data creation.

| Description | Language | Sample |
|---|---|---|
| Azure AI Inference package for JavaScript | JavaScript |
|

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/planning -->

# Microsoft Foundry rollout across my organization

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

This guide outlines key decisions for rolling out Microsoft Foundry, including environment setup, data isolation, integration with other Azure services, capacity management, and monitoring. Use this guide as a starting point and adapt it to your needs. For implementation details, see the linked articles for further guidance.

## Example organization

Contoso is a global enterprise exploring GenAI adoption across five business groups, each with distinct needs and technical maturity.

To accelerate adoption while maintaining oversight, Contoso Enterprise IT aims to enable a model with common shared resources including networking and centralized data management, while enabling self-serve access to Foundry for each team within a governed, secure environment to manage their use cases.

## Rollout considerations

The Foundry resource defines the scope for configuring, securing, and monitoring your team's environment. It's available in the Foundry portal and through Azure APIs. Projects are like folders to organize your work within this resource context. Projects also control access and permissions to Foundry developer APIs and tools.


To ensure consistency, scalability, and governance across teams, consider the following environment setup practices when rolling out Foundry:

**Establish distinct environments for development, testing, and production.**Use separate resource groups or subscriptions, and Foundry resources to isolate workflows, manage access, and support experimentation with controlled releases.**Create a separate Foundry resource for each business group.**Align deployments with logical boundaries such as data domains or business functions to ensure autonomy, governance, and cost tracking.**Associate projects with use cases.**Foundry projects are designed to represent specific use cases. They're containers to organize components such as agents or files for an application. While they inherit security settings from their parent resource, they can also implement their own access controls, data integration, and other governance controls.

## Securing the Foundry environment

Foundry is built on the Azure platform, so you can customize security controls to meet your organization's needs. Key configuration areas include:

**Identity**: Use Microsoft Entra ID to manage user and service access. Foundry supports managed identities to allow secure, passwordless authentication to other Azure services. You can assign managed identities at the**Foundry resource level**and optionally at the**project level**for fine-grained control.[Learn more about managed identities.](/en-us/security/benchmark/azure/baselines/azure-ai-foundry-security-baseline)**Networking**: Deploy Foundry into a Virtual Network to isolate traffic and control access by using Network Security Groups (NSGs).[Learn more about networking security.](/en-us/security/benchmark/azure/baselines/azure-ai-foundry-security-baseline)**Customer-Managed Keys (CMK)**: Azure supports CMK for encrypting data at rest. Foundry supports CMK optionally for customers with strict compliance needs.[Learn more about CMK](/en-us/security/benchmark/azure/baselines/azure-ai-foundry-security-baseline).**Authentication and Authorization**: Foundry supports both**API key-based access**for simple integration and**Azure RBAC**for fine-grained control. Azure enforces a clear separation between the**control plane**(resource management) and the**data plane**(model and data access). Start with built-in roles, and define custom roles as needed.[Learn more about authentication.](/en-us/security/benchmark/azure/baselines/azure-ai-foundry-security-baseline)**Templates**: Use ARM templates or Bicep to automate secure deployments. Explore the[sample templates](/en-us/security/benchmark/azure/baselines/azure-ai-foundry-security-baseline).**Storage resource**: You might choose to use built-in storage capabilities in Foundry or use your own storage resources. For the Agent Service, threads and messages can optionally be stored in[resources managed by you](/en-us/azure/ai-foundry/agents/how-to/use-your-own-resources).

## Example: Contoso's security approach

Contoso secures its Foundry deployments by using private networking with Enterprise IT managing a central hub network. Each business group connects via a spoke virtual network. They use built-in Role Based Access Control (RBAC) to separate access:

**Admins**manage deployments, connections, and shared resources**Project Managers**oversee specific projects**Users**interact with GenAI tools

For most use cases, Contoso relies on Microsoft-managed encryption by default and does **not use Customer-Managed Keys**.

## Plan user access

Effective access management is foundational to a secure and scalable Foundry setup.

**Define required access roles and responsibilities**- Identify which user groups require access to various aspects of the Foundry environment.
- Assign built-in or custom Azure RBAC roles based on responsibilities such as:
- Account owner: Manage top-level configurations such as security and shared resource connections.
- Project Managers: Create and manage Foundry projects and their contributors.
- Project Users: contribute to existing projects.


**Determine access scope**- Choose the appropriate scope for access assignments:
- Subscription level: broadest access, typically suitable for central IT or platform teams or smaller organizations.
- Resource group level: Useful for grouping related resources with shared access policies. For example, an Azure Function that follows the same application lifecycle as your Foundry environment.
- Resource or project level: Ideal for fine-grained control, especially when dealing with sensitive data or enabling self-service.


- Choose the appropriate scope for access assignments:
**Align identity strategy**- For data sources and tools integrated with Foundry, determine whether users should authenticate by using:
- Managed identities or API key: suitable for automated services and shared access across users.
- User identities: Preferred when user-level accountability or auditability is required.

- Use Microsoft Entra ID groups to simplify access management and ensure consistency across environments.

- For data sources and tools integrated with Foundry, determine whether users should authenticate by using:

## Establish connectivity with other Azure services

Foundry supports **connections**, which are reusable configurations that enable access to application components on Azure and non-Azure services. These connections also act as **identity brokers**, allowing Foundry to authenticate to external systems by using managed identities or service principals on behalf of project users.

Create connections at the **Foundry resource level** for shared services like Azure Storage or Key Vault. Scope connections to a **specific project** for sensitive or project-specific integrations. This flexibility allows teams to balance reuse and isolation based on their needs. [Learn more about connections in Foundry](../how-to/connections-add?view=foundry-classic).

Configure connection authentication to use either shared access tokens, such as Microsoft Entra ID managed identities or API keys, for simplified management and onboarding, or user tokens via Entra ID passthrough, which offer greater control when accessing sensitive data sources.


### Example: Contoso's connectivity strategy

- Contoso creates a Foundry resource for every business group, ensuring projects with similar data needs share the same connected resources.
- By default, connected resources use shared authentication tokens and are shared across all projects.
- Projects that use sensitive data workloads connect to data sources with project-scoped connections and Microsoft Entra ID passthrough authentication.

## Governance

Effective governance in Foundry ensures secure, compliant, and cost-efficient operations across business groups.

**Model Access Control with Azure Policy**Azure Policy enforces rules across Azure resources. In Foundry, use policies to restrict which models or model families specific business groups can access.*Example*: Contoso’s**Finance & Risk**group is restricted from using preview or noncompliant models by applying a policy at their business group’s subscription level.**Cost Management by Business Group**By deploying Foundry per business group, Contoso can track and manage costs independently. Use Microsoft Cost Management to view detailed usage and spending per Foundry deployment or project.**Usage Tracking with Azure Monitor**Azure Monitor provides metrics and dashboards to track usage patterns, performance, and health of Foundry resources.**Verbose Logging with Azure Log Analytics**Azure Log Analytics enables deep inspection of logs for operational insights. For example, log request usage, token usage, and latency to support auditing and optimization.

## Configure and optimize model deployments

When deploying models in Foundry, teams can choose between standard and provisioned [deployment types](../../ai-services/openai/how-to/deployment-types?view=foundry-classic). Standard deployments are ideal for development and experimentation, offering flexibility and ease of setup. Provisioned deployments are recommended for production scenarios where predictable performance, cost control, and model version pinning are required.

To support cross-region scenarios and let you access existing model deployments, Foundry allows [connections](../how-to/connections-add?view=foundry-classic) to model deployments hosted in other Foundry or Azure OpenAI instances. By using connections, teams can centralize deployments for experimentation while still enabling access from distributed projects. For production workloads, consider having use cases manage their own deployments to ensure tighter control over model lifecycle, versioning, and rollback strategies.

To prevent overuse and ensure fair resource allocation, you can apply [Tokens Per Minute (TPM) limits at the deployment level](../openai/concepts/provisioned-throughput?view=foundry-classic&tabs=global-ptum). TPM limits help control consumption, protect against accidental spikes, and align usage with project budgets or quotas. Consider setting conservative limits for shared deployments and higher thresholds for critical production services.

## Access extended functionality with Azure AI Hub

While a Foundry resource alone gives you access to most Foundry functionality, select capabilities are currently only available in combination with an Azure AI hub resource powered by Azure Machine Learning. These capabilities are lower in the AI development stack and focus on model customization.

Hub resources require their own project types that you can also access by using the Azure Machine Learning Studio, SDK, or CLI. To help plan your deployment, see [this table](../what-is-foundry?view=foundry-classic#which-type-of-project-do-i-need) and [choose a resource type](resource-types?view=foundry-classic) for an overview of supported capabilities.

You deploy a hub resource side-by-side with your Foundry resource. The hub resource takes a dependency on your Foundry resource to provide access to select tools and models.

## Learn more

Secure the Foundry environment

- Authentication and RBAC:
[Role-based access control in Foundry](rbac-foundry?view=foundry-classic) - Networking:
[Use a virtual network with Foundry](../how-to/configure-private-link?view=foundry-classic) - Identity and managed identity:
[Configure managed identity in Foundry](../../ai-services/openai/how-to/managed-identity?view=foundry-classic) - Customer-managed keys (CMK):
[Customer-managed keys in Foundry](encryption-keys-portal?view=foundry-classic) - Example infrastructure:
[templates repository with sample infrastructure templates](https://github.com/microsoft-foundry/foundry-samples/tree/main/samples) [Recover or purge deleted Foundry resources](../../ai-services/recover-purge-resources?view=foundry-classic&toc=/azure/ai-foundry/toc.json&bc=/azure/ai-foundry/breadcrumb/toc.json)

- Authentication and RBAC:
Establish connectivity with other Azure services

- Overview of connections:
[Add a new connection in Foundry](../how-to/connections-add?view=foundry-classic)

- Overview of connections:
Governance

- Model access control with Azure Policy:
[Control model deployment with built-in policies](../how-to/built-in-policy-model-deployment?view=foundry-classic) - Cost management:
[Plan and manage costs for Foundry](../how-to/costs-plan-manage?view=foundry-classic) - Azure Monitor for usage tracking:
[Monitor your Generative AI applications](../how-to/monitor-applications?view=foundry-classic)

- Model access control with Azure Policy:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/connections -->

# Add a new connection to your project

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

Tip

An alternate hub-scoped connections article is available: [Create and manage connections (Hubs)](hub-connections-add?view=foundry-classic).

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

In this article, you learn how to add a new connection in [Microsoft Foundry portal](https://ai.azure.com/?cid=learnDocs).

Connections are a way to authenticate and consume both Microsoft and other resources within your Foundry projects. They're required for scenarios such as building Standard Agents or building with Agent knowledge tools. Certain connections can be created in the Foundry UI while others require deployment through code in Bicep template. See our [foundry-samples on GitHub](https://github.com/azure-ai-foundry/foundry-samples/tree/main/infrastructure/infrastructure-setup-bicep/01-connections). Read the table descriptions below to learn more.

## Prerequisites

- If you don't have one,
[create a project](create-projects?view=foundry-classic).

## Connection types

| Service connection type | Preview | Description |
|---|---|---|
| Azure AI Search | Azure AI Search is an Azure resource that supports information retrieval over your vector and textual data stored in search indexes. Required for Standard Agent deployment. | |
| Azure Storage | Azure Storage is a cloud storage solution for storing unstructured data like documents, images, videos, and application installers. Required for Standard Agent deployment. | |
| Azure Cosmos DB | ✅ | Azure Cosmos DB is a globally distributed, multi-model database service that offers low latency, high availability, and scalability across multiple geographical regions. Required for Standard Agent deployment. Connection creation only supported through code. |
| Azure OpenAI | Azure OpenAI is a service that provides access to OpenAI's models including the GPT-5, GPT-4o, DALLE-3, and Embeddings model series with the security and enterprise capabilities of Azure. | |
| Application Insights | Azure Application Insights is a service that enables developers to automatically detect performance anomalies, diagnose issues, and gain deep insights into application usage and behavior. | |
| Azure Key Vault | Azure service for securely storing and accessing secrets. (See limitations below) | |
| Foundry | Connect to other Foundry resources. | |
| OpenAI | Connect to your OpenAI models. | |
| Serp | Serp connects to Search Engine Results Pages (SERP) for real-time data access. Supports scenarios that need the latest search results. | |
| API key | API Key connections handle authentication to your specified target on an individual basis. | |
| Custom key | Custom connections allow you to securely store and access keys while storing related properties, such as targets and versions. Custom connections are useful when you have many targets or cases where you wouldn't need a credential to access. LangChain scenarios are a good example where you would use custom service connections. Custom connections don't manage authentication, so you have to manage authentication on your own. | |
| Grounding with Bing Search | Connects to Bing Search to provide real-time web grounding for queries. Enables AI agents to reference current web data in responses. | |
| Serverless Model | ✅ | Serverless Model connections allow you to serverless API deployment. Connection creation only supported through code. |
| Azure Databricks | ✅ | Azure Databricks connector allows you to connect your Foundry Agents to Azure Databricks to access workflows and Genie Spaces during runtime. Connection creation only supported through code. |
| Sharepoint | ✅ | Sharepoint is a Microsoft platform for document storage and collaboration. It allows agents to access and manage organizational documents. Connection creation only supported through code. |
| Microsoft Fabric | ✅ | AI skills allow you to create your own conversational Q&A systems on Fabric using generative AI. Connection creation only supported through code. |
| Grounding with Bing Custom Search | ✅ | Integrates with a custom Bing search instance for tailored web grounding. Connection creation only supported through code. |
| Azure APIM | ✅ | APIM allows for governance of AI Models called in the Foundry Agent service. Connection creation only supported through code. |
| Model Gateway | ✅ | Model Gateway allows for governance of AI Models called in the Foundry Agent service. Connection creation only supported through code. |

| Service connection type | Preview | Description |
|---|---|---|
| Azure AI Search | Azure AI Search is an Azure resource that supports information retrieval over your vector and textual data stored in search indexes. Required for Standard Agent deployment. | |
| Azure Storage | Azure Storage is a cloud storage solution for storing unstructured data like documents, images, videos, and application installers. Required for Standard Agent deployment. | |
| Azure Cosmos DB | ✅ | Azure Cosmos DB is a globally distributed, multi-model database service that offers low latency, high availability, and scalability across multiple geographical regions. Required for Standard Agent deployment. Connection creation not supported in Foundry Management center. |
| Azure OpenAI | Azure OpenAI is a service that provides access to OpenAI's models including the GPT-5, GPT-4o, DALLE-3, and Embeddings model series with the security and enterprise capabilities of Azure. | |
| Application Insights | Azure Application Insights is a service that enables developers to automatically detect performance anomalies, diagnose issues, and gain deep insights into application usage and behavior. | |
| Azure Key Vault | Azure service for securely storing and accessing secrets. (See limitations below) | |
| Foundry | Connect to other Foundry resources. | |
| OpenAI | Connect to your OpenAI models. | |
| Serp | Serp connects to Search Engine Results Pages (SERP) for real-time data access. Supports scenarios that need the latest search results. | |
| API key | API Key connections handle authentication to your specified target on an individual basis. | |
| Custom key | Custom connections allow you to securely store and access keys while storing related properties, such as targets and versions. Custom connections are useful when you have many targets or cases where you wouldn't need a credential to access. LangChain scenarios are a good example where you would use custom service connections. Custom connections don't manage authentication, so you have to manage authentication on your own. | |
| Grounding with Bing Search | Connects to Bing Search to provide real-time web grounding for queries. Enables AI agents to reference current web data in responses. | |
| Serverless Model | ✅ | Serverless Model connections allow you to serverless API deployment. |
| Azure Databricks | ✅ | Azure Databricks connector allows you to connect your Foundry Agents to Azure Databricks to access workflows and Genie Spaces during runtime. |
| Sharepoint | ✅ | Sharepoint is a Microsoft platform for document storage and collaboration. It allows agents to access and manage organizational documents. |
| Microsoft Fabric | ✅ | AI skills allow you to create your own conversational Q&A systems on Fabric using generative AI. |
| Grounding with Bing Custom Search | ✅ | Integrates with a custom Bing search instance for tailored web grounding. |

### Azure Key Vault limitations

Foundry stores connections details in a managed Azure Key Vault if no Key Vault connection is created. Users that prefer to manage their secrets themselves can bring their own Azure Key Vault via a connection. All Foundry projects use a managed Azure Key Vault (not shown in your subscription). If you bring your own Azure Key Vault, note:

- Only one Azure Key Vault connection per Foundry resource at a time.
- You can delete an Azure Key Vault connection only if there are no other existing connections on the Foundry resource or project level.
- Secret migration isn't supported; recreate connections after attaching the Key Vault.
- Deleting the underlying Azure Key Vault breaks the Foundry resource (connections depend on stored secrets).
- Deleting secrets in your BYO Key Vault may break connections to other services.

### Azure Databricks connection (preview) limitations

It supports three connection types - **Jobs**, **Genie**, and **Other**. You can pick the Job or Genie space you want associated with this connection while setting up the connection in the Foundry UI. You can also use the Other connection type and allow your agent to access workspace operations in Azure Databricks. Authentication is handled through Microsoft Entra ID for users or service principals. For examples of using this connector, see [Jobs](https://github.com/Azure-Samples/AI-Foundry-Connections/blob/main/src/samples/python/sample_agent_adb_job.py) and [Genie](https://github.com/Azure-Samples/AI-Foundry-Connections/blob/main/src/samples/python/sample_agent_adb_genie.py). Note: Usage of this connection is available only via the Foundry SDK in code and is integrated into agents as a FunctionTool (please see the samples above for details). Usage of this connection in Foundry Playground is currently not supported.

## Create a new connection

Use the portal or a Bicep template to add a connection.

Follow these steps to create a new connection that's available for the current project.

Tip

Because you can [customize the left pane](../what-is-foundry?view=foundry-classic#customize-the-left-pane) in the Microsoft Foundry portal, you might see different items than shown in these steps. If you don't see what you're looking for, select **... More** at the bottom of the left pane.

Sign in to

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is off. These steps refer to**Foundry (classic)**.Sign in to

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is on. These steps refer to**Foundry (new)**.Select

**Management center**from the bottom left navigation.Select

**Connected resources**from the**Project**section.Select

**+ New connection**from the**Connected resources**section.Select the service you want to connect to from the list of available external resources. For example, select

**Azure AI Search**.Browse for and select your Azure AI Search service from the list of available services and then select the type of

**Authentication**to use for the resource. Select**Add connection**.Tip

Different connection types support different authentication methods. Using Microsoft Entra ID might require specific Azure role-based access permissions for your developers. For more information, visit

[Role-based access control](../concepts/rbac-foundry?view=foundry-classic).After the service is connected, select

**Close**.

Sign in to

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is off. These steps refer to**Foundry (classic)**.Sign in to

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is on. These steps refer to**Foundry (new)**.Select

**Operate**in the upper-right navigation.Select

**Admin**in the left pane.Select your project name in the

**Manage all projects**list.Select

**Add connection**in the upper-right corner.Select the service you want to connect to from the list of available external resources. For example, select

**Azure AI Search**.Browse for and select your Azure AI Search service from the list of available services and then select the type of

**Authentication**to use for the resource. Select**Add connection**.Tip

Different connection types support different authentication methods. Using Microsoft Entra ID might require specific Azure role-based access permissions for your developers. For more information, visit

[Role-based access control](../concepts/rbac-foundry?view=foundry-classic).

## Network isolation

For end-to-end [network isolation](configure-private-link?view=foundry-classic) with Foundry, you need private endpoints to connect to your connected resource. For example, if your Azure Storage account is set to public network access as **Disabled**, then a private endpoint should be deployed in your virtual network to access in Foundry.

For more on how to set private endpoints to your connected resources, see the following documentation:

| Private resource | Documentation |
|---|---|
| Azure Storage |
|

[Configure Azure Private Link for Azure Cosmos DB](/en-us/azure/cosmos-db/how-to-configure-private-endpoints?tabs=arm-bicep)[Create a private endpoint for a secure connection](/en-us/azure/search/service-create-private-endpoint)[Securing Azure OpenAI inside a virtual network with private endpoints](/en-us/azure/ai-foundry/openai/how-to/network)[Use Azure Private Link to connect networks to Azure Monitor](/en-us/azure/azure-monitor/logs/private-link-security)Note

Cross-subscription connections used for model deployment are not supported (Foundry, Azure OpenAI). You can't connect to resources from different subscriptions for model deployments.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/content-filtering -->

# Content filtering in Microsoft Foundry portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs) includes a content filtering system that works alongside core models and image generation models.

Important

The content filtering system isn't applied to prompts and completions processed by the Whisper model in Foundry Models. Learn more about the [Whisper model in Azure OpenAI](../openai/concepts/models?view=foundry-classic).

## How it works

The content filtering system is powered by [Azure AI Content Safety](../../ai-services/content-safety/overview?view=foundry-classic), and it works by running both the model prompt input and completion output through a set of classification models designed to detect and prevent harmful content. Variations in API configurations and application design might affect completions and thus filtering behavior.

With Azure OpenAI model deployments, you can use the default content filter or create your own content filter (described later). Models available through **serverless API deployments** have content filtering enabled by default. To learn more about the default content filter enabled for serverless API deployments, see [Content safety for Models Sold Directly by Azure ](model-catalog-content-safety?view=foundry-classic).

## Language support

The content filtering models are trained and tested on the following languages: English, German, Japanese, Spanish, French, Italian, Portuguese, and Chinese. However, the service can work in many other languages, but the quality can vary. In all cases, you should do your own testing to ensure that it works for your application.

## Content risk filters (input and output filters)

The following special filters work for both input and output of generative AI models:

### Categories

| Category | Description |
|---|---|
| Hate | The hate category describes language attacks or uses that include pejorative or discriminatory language with reference to a person or identity group based on certain differentiating attributes of these groups including but not limited to race, ethnicity, nationality, gender identity and expression, sexual orientation, religion, immigration status, ability status, personal appearance, and body size. |
| Sexual | The sexual category describes language related to anatomical organs and genitals, romantic relationships, acts portrayed in erotic or affectionate terms, physical sexual acts, including those portrayed as an assault or a forced sexual violent act against one's will, prostitution, pornography, and abuse. |
| Violence | The violence category describes language related to physical actions intended to hurt, injure, damage, or kill someone or something; describes weapons, etc. |
| Self-Harm | The self-harm category describes language related to physical actions intended to purposely hurt, injure, or damage one's body, or kill oneself. |

### Severity levels

| Category | Description |
|---|---|
| Safe | Content might be related to violence, self-harm, sexual, or hate categories but the terms are used in general, journalistic, scientific, medical, and similar professional contexts, which are appropriate for most audiences. |
| Low | Content that expresses prejudiced, judgmental, or opinionated views, includes offensive use of language, stereotyping, use cases exploring a fictional world (for example, gaming, literature), and depictions at low intensity. |
| Medium | Content that uses offensive, insulting, mocking, intimidating, or demeaning language towards specific identity groups, includes depictions of seeking and executing harmful instructions, fantasies, glorification, promotion of harm at medium intensity. |
| High | Content that displays explicit and severe harmful instructions, actions, damage, or abuse; includes endorsement, glorification, or promotion of severe harmful acts, extreme or illegal forms of harm, radicalization, or nonconsensual power exchange or abuse. |

### Other input filters

You can also enable special filters for generative AI scenarios:

**Jailbreak attacks**: Jailbreak Attacks are User Prompts designed to provoke the Generative AI model into exhibiting behaviors it was trained to avoid or to break the rules set in the System Message.**Indirect attacks**: Indirect Attacks, also referred to as Indirect Prompt Attacks or Cross-Domain Prompt Injection Attacks, are a potential vulnerability where third parties place malicious instructions inside of documents that the Generative AI system can access and process.

### Other output filters

You can also enable the following special output filters:

**Protected material for text**: Protected material text describes known text content (for example, song lyrics, articles, recipes, and selected web content) that a large language model might output.**Protected material for code**: Protected material code describes source code that matches a set of source code from public repositories, which a large language models might output without proper citation of source repositories.**Groundedness**: The groundedness detection filter detects whether the text responses of large language models (LLMs) are grounded in the source materials provided by the users.**Personally identifiable information (PII)**: The PII filter detects whether the text responses of large language models (LLMs) contain personally identifiable information (PII). PII refers to any information that can be used to identify a particular individual, such as a name, address, phone number, email address, social security number, driver's license number, passport number, or similar information.

## Create a content filter in Microsoft Foundry

For any model deployment in [Foundry](https://ai.azure.com/?cid=learnDocs), you can directly use the default content filter, but you might want to have more control. For example, you could make a filter stricter or more lenient, or enable more advanced capabilities like prompt shields and protected material detection.

Tip

For guidance with content filters in your Foundry project, you can read more at [Foundry content filtering](/en-us/azure/ai-studio/concepts/content-filtering).

Follow these steps to create a content filter:

Tip

Because you can [customize the left pane](../what-is-foundry?view=foundry-classic#customize-the-left-pane) in the Microsoft Foundry portal, you might see different items than shown in these steps. If you don't see what you're looking for, select **... More** at the bottom of the left pane.

-
Sign in to

[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is off. These steps refer to**Foundry (classic)**. Navigate to your project. Then select the

**Guardrails + controls**page from the left menu and select the**Content filters**tab.Select

**+ Create content filter**.On the

**Basic information**page, enter a name for your content filtering configuration. Select a connection to associate with the content filter. Then select**Next**.Now you can configure the input filters (for user prompts) and output filters (for model completion).

On the

**Input filters**page, you can set the filter for the input prompt. For the first four content categories there are three severity levels that are configurable: Low, medium, and high. You can use the sliders to set the severity threshold if you determine that your application or usage scenario requires different filtering than the default values. Some filters, such as Prompt Shields and Protected material detection, enable you to determine if the model should annotate and/or block content. Selecting**Annotate only**runs the respective model and returns annotations via API response, but it will not filter content. In addition to annotate, you can also choose to block content.If your use case was approved for modified content filters, you receive full control over content filtering configurations. You can choose to turn filtering partially or fully off, or enable annotate only for the content harms categories (violence, hate, sexual, and self-harm).

Content is annotated by category and blocked according to the threshold you set. For the violence, hate, sexual, and self-harm categories, adjust the slider to block content of high, medium, or low severity.

On the

**Output filters**page, you can configure the output filter, which is applied to all output content the model generates. Configure the individual filters as before. The page provides the Streaming mode option, letting you filter content in near-real-time as the model generates it and reducing latency. When you're finished select**Next**.Content is annotated by each category and blocked according to the threshold. For violent content, hate content, sexual content, and self-harm content category, adjust the threshold to block harmful content with equal or higher severity levels.

Optionally, on the

**Connection**page, you can associate the content filter with a deployment. If a selected deployment already has a filter attached, you must confirm that you want to replace it. You can also associate the content filter with a deployment later. Select**Create**.Content filtering configurations are created at the hub level in the

[Foundry portal](https://ai.azure.com/?cid=learnDocs). Learn more about configurability in the[Azure OpenAI in Foundry Models documentation](/en-us/azure/ai-foundry/openai/how-to/content-filters).On the

**Review**page, review the settings and then select**Create filter**.

### Use a blocklist as a filter

You can apply a blocklist as either an input or output filter, or both. Enable the **Blocklist** option on the **Input filter** and/or **Output filter** page. Select one or more blocklists from the dropdown, or use the built-in profanity blocklist. You can combine multiple blocklists into the same filter.

## Apply a content filter

The filter creation process gives you the option to apply the filter to the deployments you want. You can also change or remove content filters from your deployments at any time.

Follow these steps to apply a content filter to a deployment:

Go to

[Foundry](https://ai.azure.com/?cid=learnDocs)and select a project.Select

**Models + endpoints**on the left pane and choose one of your deployments, then select**Edit**.In the

**Update deployment**window, select the content filter you want to apply to the deployment. Then select**Save and close**.You can also edit and delete a content filter configuration if necessary. Before you delete a content filtering configuration, you need to unassign and replace it from any deployment in the

**Deployments**tab.

Now, you can go to the playground to test whether the content filter works as expected.

Tip

You can also create and update content filters using the REST APIs. For more information, see the [API reference](/en-us/rest/api/aiservices/accountmanagement/rai-policies/create-or-update). Content filters can be configured at the resource level. Once a new configuration is created, it can be associated with one or more deployments. For more information about model deployment, see the resource [deployment guide](../openai/how-to/create-resource?view=foundry-classic).

## Configurability (preview)

Azure OpenAI in Microsoft Foundry Models includes default safety settings applied to all models (excluding audio API models such as Whisper). These configurations provide you with a responsible experience by default, including content filtering models, blocklists, prompt transformation, [content credentials](../openai/concepts/content-credentials?view=foundry-classic), and others. [Read more about it here](/en-us/azure/ai-foundry/openai/concepts/default-safety-policies).

All customers can also configure content filters and create custom content policies that are tailored to their use case requirements. The configurability feature allows customers to adjust the settings, separately for prompts and completions, to filter content for each content category at different severity levels as described in the table below. Content detected at the 'safe' severity level is labeled in annotation output but isn't subject to filtering and isn't configurable.

| Severity filtered | Configurable for prompts | Configurable for completions | Descriptions |
|---|---|---|---|
| Low, medium, high | Yes | Yes | Strictest filtering configuration. Content detected at severity levels low, medium, and high is filtered. |
| Medium, high | Yes | Yes | Content detected at severity level low isn't filtered, content at medium and high is filtered. |
| High | Yes | Yes | Content detected at severity levels low and medium isn't filtered. Only content at severity level high is filtered. |
| No filters | If approved1 |
If approved1 |
No content is filtered regardless of severity level detected. Requires approval1. |
| Annotate only | If approved1 |
If approved1 |
Disables the filter functionality, so content will not be blocked, but annotations are returned via API response. Requires approval1. |

1 For Azure OpenAI models, only customers who have been approved for modified content filtering have full content filtering control and can turn off content filters. Apply for modified content filters via this form: [Limited Access Review: Modified Content Filters](https://ncv.microsoft.com/uEfCgnITdR). For Azure Government customers, apply for modified content filters via this form: [Azure Government - Request Modified Content Filtering](https://aka.ms/AOAIGovModifyContentFilter).

Configurable content filters for inputs (prompts) and outputs (completions) are available for all Azure OpenAI models.

Content filtering configurations are created within a Resource in Foundry portal, and can be associated with Deployments. [Learn more about configuring content filters here](../openai/how-to/content-filters?view=foundry-classic).

Customers are responsible for ensuring that applications integrating Azure OpenAI comply with the [Code of Conduct](/en-us/legal/ai-code-of-conduct?context=/azure/ai-foundry/openai/context/context).

## Related content

- Learn more about the
[underlying models that power Azure OpenAI](../openai/concepts/models?view=foundry-classic). - Foundry content filtering is powered by
[Azure AI Content Safety](../../ai-services/content-safety/overview?view=foundry-classic). - Learn more about understanding and mitigating risks associated with your application:
[Overview of Responsible AI practices for Azure OpenAI models](/en-us/azure/ai-foundry/responsible-ai/openai/overview). - Learn more about evaluating your generative AI models and AI systems via
[Azure AI Evaluation](https://aka.ms/genaiopsevals).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/rbac-foundry -->

# Role-based access control for Microsoft Foundry

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

Tip

An alternate hub-focused RBAC article is available: [Role-based access control for Microsoft Foundry (Hubs and Projects)](hub-rbac-foundry?view=foundry-classic).

In this article, you learn about role-based access control (RBAC) in your Microsoft Foundry resource and how to assign roles that control access to resources.

In this article, you learn how to manage access to Microsoft Foundry resources using role-based access control (RBAC).

For more information about authentication and authorization in Microsoft Foundry, see [Authentication and Authorization](authentication-authorization-foundry?view=foundry-classic). This article mentions terminology explained in the previous article.

## Getting started

For new users to Azure and Microsoft Foundry, use the following check-list to ensure all the correct roles are assigned to your user principal and your project's managed identity to get started in Foundry. You can check your roles by using the [Check access for a user to a single Azure resource](/en-us/azure/role-based-access-control/check-access?tabs=default) guidelines.

- Assign the
**Azure AI User**role on your Foundry resource to your**user principal**. - Assign the
**Azure AI User**role on your Foundry resource to your**project's managed identity**.

If the user that created the project can assign roles, such as the Azure **Owner** role assigned, on the subscription or resource group scope, both of these roles are automatically assigned.

To assign a role to your user principal or to your project's managed identity, follow the guidelines in the following section.

### Assign a role to your user principal

- Sign in to the
[Azure portal](https://portal.azure.com/). - Navigate to your Foundry resource.
- From the left pane, select
**Access control (IAM)**. - Select
**Add**>**Add role assignment**. - Under
**Role**, select**Azure AI User**. Under**Members**, select**User, group, or service principal**and search for your name or email and**Select**. - Finally,
**Review + assign**the role.

- From the left pane, select

### Assign a role to your project's managed identity

- Sign in to the
[Azure portal](https://portal.azure.com/). - Go to your Foundry project.
- From the left pane, select
**Access control (IAM)**. - Select
**Add**>**Add role assignment**. - Under
**Role**, select**Azure AI User**. Under**Members**, select**Managed identity**and select the managed identity of your project and**Select**. - Finally,
**Review + assign**the role.

- From the left pane, select

## Terminology for role-based access control in Foundry

To understand role-based access control in Microsoft Foundry, consider two questions for your enterprise.

What permissions do I want my team to have when building in Microsoft Foundry?

At what scope do I want to assign the permissions to my team?


To help answer these questions, here are descriptions of some terminology used throughout this article.

**permissions**: The allowed or denied actions that an identity can perform on a resource, such as reading, writing, deleting, or managing both the control plane and data plane. In Foundry, this concept includes read, write, or delete permissions.**scope**: The set of Azure resources to which a role assignment applies. Potential scopes include subscription, resource group, Foundry resource, or Foundry project.**role**: A named collection of permissions that defines what actions can be performed on Azure resources at a given scope.

To relate these terms to each other, an identity is assigned a *role* with certain *permissions* to create and build Foundry resources and projects. You assign a specific *scope* depending on enterprise requirements.

In Microsoft Foundry, consider two scopes when completing role assignments.

**Foundry resource**: The top-level scope that defines the administrative, security, and monitoring boundary for a Microsoft Foundry environment.**Foundry project**: A sub-scope within a Foundry resource used to organize work and enforce access control for Foundry APIs, tools, and developer workflows.

## Built-in roles

A **built-in role** in Foundry is a role created by Microsoft that covers common access scenarios that you can assign to your team members. Key built-in roles used across Azure include Owner, Contributor, and Reader. These roles aren't specific to Foundry resource permissions.

For Foundry resources, use additional built-in roles to follow least privilege access principles. The following table lists the five key built-in roles for Foundry, a short description, and the link to the exact role definition in the [AI + Machine Learning built-in roles article](/en-us/azure/role-based-access-control/built-in-roles/ai-machine-learning).

| Role | Description |
|---|---|
Azure AI User |
Grants reader access to Foundry project, Foundry resource, and data actions for your Foundry project. If you can assign roles, this role is assigned to you automatically. Otherwise, your subscription Owner or a user with role assignment permissions grants it. Least privilege access role in Foundry. |
Azure AI Project Manager |
Lets you perform management actions on Foundry projects, build and develop with projects, and conditionally assign the Azure AI User role to other user principals. |
Azure AI Account Owner |
Grants full access to manage projects and resources, and lets you conditionally assign the Azure AI User role to other user principals. |
Azure AI Owner |
Grants full access to managed projects and resources and build and develop with projects. Highly privileged self-serve role designed for digital natives. |

### Permissions for each built-in role

Use the following table and diagram to see the permissions allowed for each built-in role in Foundry, including the key Azure built-in roles.

| Built-in role | Create Foundry projects | Create Foundry accounts | Build and develop in a project (data actions) | Complete role assignments | Reader access to projects and accounts | Manage models |
|---|---|---|---|---|---|---|
Azure AI User |
✔ | ✔ | ||||
Azure AI Project Manager |
✔ | ✔ | ✔ (only assign Azure AI User role) | ✔ | ||
Azure AI Account Owner |
✔ | ✔ | ✔ (only assign Azure AI User role) | ✔ | ✔ | |
Azure AI Owner |
✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
Owner |
✔ | ✔ | ✔ (assign any role to any user) | ✔ | ✔ | |
Contributor |
✔ | ✔ | ✔ | ✔ | ||
Reader |
✔ |

For more on built-in roles in Azure and Foundry, see [Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles). To learn more about conditional delegation used in the Azure AI Account Owner and Azure AI Project Manager role, see [Delegate Azure role assignment management to others with conditions](/en-us/azure/role-based-access-control/delegate-role-assignments-portal).

## Sample enterprise RBAC setup for projects

Here's an example of how to implement role-based access control (RBAC) for an enterprise Foundry resource.

| Persona | Role and Scope | Purpose |
|---|---|---|
| IT admin | Owner on subscription scope | The IT admin ensures the Foundry resource meets enterprise standards. Assign managers the Azure AI Account Owner role on the resource to let them create new Foundry accounts. Assign managers the Azure AI Project Manager role on the resource to let them create projects within an account. |
| Managers | Azure AI Account Owner on Foundry resource scope | Managers manage the Foundry resource, deploy models, audit compute resources, audit connections, and create shared connections. They can't build in projects, but they can assign the Azure AI User role to themselves and others to start building. |
| Team lead or lead developer | Azure AI Project Manager on Foundry resource scope | Lead developers create projects for their team and start building in those projects. After you create a project, project owners invite other members and assign the Azure AI User role. |
| Team members or developers | Azure AI User on Foundry project scope and Reader on the Foundry resource scope | Developers build agents in a project with pre-deployed Foundry models and pre-built connections. |

## Manage roles

To manage roles in Foundry, you must have the permission to assign and remove roles in Azure. The key Azure built-in role of **Owner** includes the necessary permission. You can assign roles through the Foundry portal (Admin page), Azure portal IAM, or Azure CLI. To remove roles, you can only use the Azure portal IAM or Azure CLI.

In the Foundry portal, manage permissions by:

- On the
**Home**page in[Foundry](https://ai.azure.com/?cid=learnDocs), select your Foundry resource. - Select
**Users**to add or remove users for the resource.

In the Foundry portal, manage permissions by:

- On the
**Admin**page in[Foundry](https://ai.azure.com/nextgen), select**Operate**, then**Admin**on the left navigation. - Select your project name in the table.
- On the top right, select
**Add user**. This button is only clickable if you have permissions to role assign. - Add your user to the Foundry project. The same instructions apply for your Foundry resource.

You can manage permissions in the [Azure portal](https://portal.azure.com) under **Access Control (IAM)** or by using Azure CLI.

For example, the following command assigns the Azure AI User role to `joe@contoso.com`

for the resource group `this-rg`

in the subscription with the ID `00000000-0000-0000-0000-000000000000`

:

```
az role assignment create --role "Azure AI User" --assignee "joe@contoso.com" --scope /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/this-rg
```


## Create custom roles for projects

If the built-in roles don't meet your enterprise requirements, create a custom role that allows for precise control over allowed actions and scopes. Here's an example subscription-level custom role definition:

```
{
"properties": {
"roleName": "My Enterprise Foundry User",
"description": "Custom role for Foundry at my enterprise to only allow building Agents. Assign at subscription level.",
"assignableScopes": ["/subscriptions/<your-subscription-id>"],
"permissions": [ {
"actions": ["Microsoft.CognitiveServices/*/read", "Microsoft.Authorization/*/read", "Microsoft.CognitiveServices/accounts/listkeys/action","Microsoft.Resources/deployments/*"],
"notActions": [],
"dataActions": ["Microsoft.CognitiveServices/accounts/AIServices/agents/*"],
"notDataActions": []
} ]
}
}
```


For more information on creating a custom role, see the following articles.

[Azure portal](/en-us/azure/role-based-access-control/custom-roles-portal)[Azure CLI](/en-us/azure/role-based-access-control/custom-roles-cli)[Azure PowerShell](/en-us/azure/role-based-access-control/custom-roles-powershell)[Disable Preview Features with Role-Based Access](disable-preview-features-with-rbac?view=foundry-classic). This article provides more details on specific permissions in Foundry across control and data plane which you can utilize when building custom roles.

## Notes and limitations

- To view and purge deleted Foundry accounts, you must have the Contributor role assigned at the subscription scope.
- Users with the Contributor role can deploy models in Foundry.
- You need the Owner role on a resource's scope to create custom roles in the resource.
- If you have permissions to role assign in Azure (for example, the Owner role assigned on the account scope) to your user principal, and you deploy a Foundry resource from the Azure portal or Foundry portal UI, then the Azure AI User role gets automatically assigned to your user principal. This assignment doesn't apply when deploying Foundry from SDK or CLI.
- When you create a Foundry resource, the built-in role-based access control (RBAC) permissions give you access to the resource. To use resources created outside Foundry, ensure the resource has permissions that let you access it. Here are some examples:
- To use a new Azure Blob Storage account, add the Foundry account resource's managed identity to the Storage Blob Data Reader role on that storage account.
- To use a new Azure AI Search source, add Foundry to the Azure AI Search role assignments.


## Related content

## Appendix

### Access Isolation Examples

Each organization may have different access isolation requirements depending on the user personas in their enterprise. Access isolation refers to which users in your enterprise are given what role assignments for either a separation of permissions using our built-in roles or a unified, highly permissive role. There are three access isolation options for Foundry that you can select for your organization depending on your access isolation requirements.

**No access isolation.** This means in your enterprise, you don't have any requirements separating permissions between a developer, project manager, or an admin. The permissions for these roles can be assigned across teams.

Therefore, you should...

- Grant all users in your enterprise the
**Azure AI Owner**role on the resource scope

**Partial access isolation.** This means the project manager in your enterprise should be able to develop within projects as well as create projects. But your admins shouldn't be able to develop within Foundry, only create Foundry projects and accounts.

Therefore, you should...

- Grant your admin with
**Azure AI Account Owner**on the resource scope - Grant your developer and project managers with
**Azure AI Project Manager**role on the resource

**Full access isolation.** This means your admins, project managers, and developers have clear permissions assigned that don't overlap for their different functions within an enterprise.

Therefore you should...

- Grant your admin the
**Azure AI Account Owner**on resource scope - Grant your developer the
**Reader**role on Foundry resource scope and**Azure AI User**on project scope - Grant your project manager the
**Azure AI Project Manager**role on resource scope

### Use Microsoft Entra groups with Foundry

Microsoft Entra ID provides several ways to manage access to resources, applications, and tasks. By using Microsoft Entra groups, you can grant access and permissions to a group of users instead of to each individual user. Enterprise IT admins can create Microsoft Entra groups in the Azure portal to simplify the role assignment process for developers. When you create a Microsoft Entra group, you can minimize the number of role assignments required for new developers working on Foundry projects by assigning the group the required role assignment on the necessary resource.

Complete the following steps to use Microsoft Entra ID groups with Foundry:

Go to

**Groups**in the Azure portal.Create a new

**Security**group in the Groups portal.Assign the owner of the Microsoft Entra group and add individual user principals in your organization to the group as members. Save the group.

Go to the resource that requires a role assignment.

**Example:**To build Agents, run traces, and more in Foundry, the minimum privilege 'Azure AI User' role must be assigned to your user principal. Assign the 'Azure AI User' role to your new Microsoft Entra group so all users in your enterprise can build in Foundry.**Example:**To use Tracing and Monitoring features in Microsoft Foundry, a 'Reader' role assignment on the connected Application Insights resource is required. Assign the 'Reader' role to your new Microsoft Entra group so all users in your enterprise can use the Tracing and Monitoring feature.

Go to Access Control (IAM).

Select the role to assign.

Assign access to "User, group, or service principal" and select the new Security group.

Review and assign. Role assignment now applies to all user principals assigned to the group.


To learn more about Microsoft Entra ID groups, prerequisites, and limitations, refer to:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/rbac-azure-ai-foundry -->

# Role-based access control for Microsoft Foundry

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

Tip

An alternate hub-focused RBAC article is available: [Role-based access control for Microsoft Foundry (Hubs and Projects)](hub-rbac-foundry?view=foundry-classic).

In this article, you learn about role-based access control (RBAC) in your Microsoft Foundry resource and how to assign roles that control access to resources.

In this article, you learn how to manage access to Microsoft Foundry resources using role-based access control (RBAC).

For more information about authentication and authorization in Microsoft Foundry, see [Authentication and Authorization](authentication-authorization-foundry?view=foundry-classic). This article mentions terminology explained in the previous article.

## Getting started

For new users to Azure and Microsoft Foundry, use the following check-list to ensure all the correct roles are assigned to your user principal and your project's managed identity to get started in Foundry. You can check your roles by using the [Check access for a user to a single Azure resource](/en-us/azure/role-based-access-control/check-access?tabs=default) guidelines.

- Assign the
**Azure AI User**role on your Foundry resource to your**user principal**. - Assign the
**Azure AI User**role on your Foundry resource to your**project's managed identity**.

If the user that created the project can assign roles, such as the Azure **Owner** role assigned, on the subscription or resource group scope, both of these roles are automatically assigned.

To assign a role to your user principal or to your project's managed identity, follow the guidelines in the following section.

### Assign a role to your user principal

- Sign in to the
[Azure portal](https://portal.azure.com/). - Navigate to your Foundry resource.
- From the left pane, select
**Access control (IAM)**. - Select
**Add**>**Add role assignment**. - Under
**Role**, select**Azure AI User**. Under**Members**, select**User, group, or service principal**and search for your name or email and**Select**. - Finally,
**Review + assign**the role.

- From the left pane, select

### Assign a role to your project's managed identity

- Sign in to the
[Azure portal](https://portal.azure.com/). - Go to your Foundry project.
- From the left pane, select
**Access control (IAM)**. - Select
**Add**>**Add role assignment**. - Under
**Role**, select**Azure AI User**. Under**Members**, select**Managed identity**and select the managed identity of your project and**Select**. - Finally,
**Review + assign**the role.

- From the left pane, select

## Terminology for role-based access control in Foundry

To understand role-based access control in Microsoft Foundry, consider two questions for your enterprise.

What permissions do I want my team to have when building in Microsoft Foundry?

At what scope do I want to assign the permissions to my team?


To help answer these questions, here are descriptions of some terminology used throughout this article.

**permissions**: The allowed or denied actions that an identity can perform on a resource, such as reading, writing, deleting, or managing both the control plane and data plane. In Foundry, this concept includes read, write, or delete permissions.**scope**: The set of Azure resources to which a role assignment applies. Potential scopes include subscription, resource group, Foundry resource, or Foundry project.**role**: A named collection of permissions that defines what actions can be performed on Azure resources at a given scope.

To relate these terms to each other, an identity is assigned a *role* with certain *permissions* to create and build Foundry resources and projects. You assign a specific *scope* depending on enterprise requirements.

In Microsoft Foundry, consider two scopes when completing role assignments.

**Foundry resource**: The top-level scope that defines the administrative, security, and monitoring boundary for a Microsoft Foundry environment.**Foundry project**: A sub-scope within a Foundry resource used to organize work and enforce access control for Foundry APIs, tools, and developer workflows.

## Built-in roles

A **built-in role** in Foundry is a role created by Microsoft that covers common access scenarios that you can assign to your team members. Key built-in roles used across Azure include Owner, Contributor, and Reader. These roles aren't specific to Foundry resource permissions.

For Foundry resources, use additional built-in roles to follow least privilege access principles. The following table lists the five key built-in roles for Foundry, a short description, and the link to the exact role definition in the [AI + Machine Learning built-in roles article](/en-us/azure/role-based-access-control/built-in-roles/ai-machine-learning).

| Role | Description |
|---|---|
Azure AI User |
Grants reader access to Foundry project, Foundry resource, and data actions for your Foundry project. If you can assign roles, this role is assigned to you automatically. Otherwise, your subscription Owner or a user with role assignment permissions grants it. Least privilege access role in Foundry. |
Azure AI Project Manager |
Lets you perform management actions on Foundry projects, build and develop with projects, and conditionally assign the Azure AI User role to other user principals. |
Azure AI Account Owner |
Grants full access to manage projects and resources, and lets you conditionally assign the Azure AI User role to other user principals. |
Azure AI Owner |
Grants full access to managed projects and resources and build and develop with projects. Highly privileged self-serve role designed for digital natives. |

### Permissions for each built-in role

Use the following table and diagram to see the permissions allowed for each built-in role in Foundry, including the key Azure built-in roles.

| Built-in role | Create Foundry projects | Create Foundry accounts | Build and develop in a project (data actions) | Complete role assignments | Reader access to projects and accounts | Manage models |
|---|---|---|---|---|---|---|
Azure AI User |
✔ | ✔ | ||||
Azure AI Project Manager |
✔ | ✔ | ✔ (only assign Azure AI User role) | ✔ | ||
Azure AI Account Owner |
✔ | ✔ | ✔ (only assign Azure AI User role) | ✔ | ✔ | |
Azure AI Owner |
✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
Owner |
✔ | ✔ | ✔ (assign any role to any user) | ✔ | ✔ | |
Contributor |
✔ | ✔ | ✔ | ✔ | ||
Reader |
✔ |

For more on built-in roles in Azure and Foundry, see [Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles). To learn more about conditional delegation used in the Azure AI Account Owner and Azure AI Project Manager role, see [Delegate Azure role assignment management to others with conditions](/en-us/azure/role-based-access-control/delegate-role-assignments-portal).

## Sample enterprise RBAC setup for projects

Here's an example of how to implement role-based access control (RBAC) for an enterprise Foundry resource.

| Persona | Role and Scope | Purpose |
|---|---|---|
| IT admin | Owner on subscription scope | The IT admin ensures the Foundry resource meets enterprise standards. Assign managers the Azure AI Account Owner role on the resource to let them create new Foundry accounts. Assign managers the Azure AI Project Manager role on the resource to let them create projects within an account. |
| Managers | Azure AI Account Owner on Foundry resource scope | Managers manage the Foundry resource, deploy models, audit compute resources, audit connections, and create shared connections. They can't build in projects, but they can assign the Azure AI User role to themselves and others to start building. |
| Team lead or lead developer | Azure AI Project Manager on Foundry resource scope | Lead developers create projects for their team and start building in those projects. After you create a project, project owners invite other members and assign the Azure AI User role. |
| Team members or developers | Azure AI User on Foundry project scope and Reader on the Foundry resource scope | Developers build agents in a project with pre-deployed Foundry models and pre-built connections. |

## Manage roles

To manage roles in Foundry, you must have the permission to assign and remove roles in Azure. The key Azure built-in role of **Owner** includes the necessary permission. You can assign roles through the Foundry portal (Admin page), Azure portal IAM, or Azure CLI. To remove roles, you can only use the Azure portal IAM or Azure CLI.

In the Foundry portal, manage permissions by:

- On the
**Home**page in[Foundry](https://ai.azure.com/?cid=learnDocs), select your Foundry resource. - Select
**Users**to add or remove users for the resource.

In the Foundry portal, manage permissions by:

- On the
**Admin**page in[Foundry](https://ai.azure.com/nextgen), select**Operate**, then**Admin**on the left navigation. - Select your project name in the table.
- On the top right, select
**Add user**. This button is only clickable if you have permissions to role assign. - Add your user to the Foundry project. The same instructions apply for your Foundry resource.

You can manage permissions in the [Azure portal](https://portal.azure.com) under **Access Control (IAM)** or by using Azure CLI.

For example, the following command assigns the Azure AI User role to `joe@contoso.com`

for the resource group `this-rg`

in the subscription with the ID `00000000-0000-0000-0000-000000000000`

:

```
az role assignment create --role "Azure AI User" --assignee "joe@contoso.com" --scope /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/this-rg
```


## Create custom roles for projects

If the built-in roles don't meet your enterprise requirements, create a custom role that allows for precise control over allowed actions and scopes. Here's an example subscription-level custom role definition:

```
{
"properties": {
"roleName": "My Enterprise Foundry User",
"description": "Custom role for Foundry at my enterprise to only allow building Agents. Assign at subscription level.",
"assignableScopes": ["/subscriptions/<your-subscription-id>"],
"permissions": [ {
"actions": ["Microsoft.CognitiveServices/*/read", "Microsoft.Authorization/*/read", "Microsoft.CognitiveServices/accounts/listkeys/action","Microsoft.Resources/deployments/*"],
"notActions": [],
"dataActions": ["Microsoft.CognitiveServices/accounts/AIServices/agents/*"],
"notDataActions": []
} ]
}
}
```


For more information on creating a custom role, see the following articles.

[Azure portal](/en-us/azure/role-based-access-control/custom-roles-portal)[Azure CLI](/en-us/azure/role-based-access-control/custom-roles-cli)[Azure PowerShell](/en-us/azure/role-based-access-control/custom-roles-powershell)[Disable Preview Features with Role-Based Access](disable-preview-features-with-rbac?view=foundry-classic). This article provides more details on specific permissions in Foundry across control and data plane which you can utilize when building custom roles.

## Notes and limitations

- To view and purge deleted Foundry accounts, you must have the Contributor role assigned at the subscription scope.
- Users with the Contributor role can deploy models in Foundry.
- You need the Owner role on a resource's scope to create custom roles in the resource.
- If you have permissions to role assign in Azure (for example, the Owner role assigned on the account scope) to your user principal, and you deploy a Foundry resource from the Azure portal or Foundry portal UI, then the Azure AI User role gets automatically assigned to your user principal. This assignment doesn't apply when deploying Foundry from SDK or CLI.
- When you create a Foundry resource, the built-in role-based access control (RBAC) permissions give you access to the resource. To use resources created outside Foundry, ensure the resource has permissions that let you access it. Here are some examples:
- To use a new Azure Blob Storage account, add the Foundry account resource's managed identity to the Storage Blob Data Reader role on that storage account.
- To use a new Azure AI Search source, add Foundry to the Azure AI Search role assignments.


## Related content

## Appendix

### Access Isolation Examples

Each organization may have different access isolation requirements depending on the user personas in their enterprise. Access isolation refers to which users in your enterprise are given what role assignments for either a separation of permissions using our built-in roles or a unified, highly permissive role. There are three access isolation options for Foundry that you can select for your organization depending on your access isolation requirements.

**No access isolation.** This means in your enterprise, you don't have any requirements separating permissions between a developer, project manager, or an admin. The permissions for these roles can be assigned across teams.

Therefore, you should...

- Grant all users in your enterprise the
**Azure AI Owner**role on the resource scope

**Partial access isolation.** This means the project manager in your enterprise should be able to develop within projects as well as create projects. But your admins shouldn't be able to develop within Foundry, only create Foundry projects and accounts.

Therefore, you should...

- Grant your admin with
**Azure AI Account Owner**on the resource scope - Grant your developer and project managers with
**Azure AI Project Manager**role on the resource

**Full access isolation.** This means your admins, project managers, and developers have clear permissions assigned that don't overlap for their different functions within an enterprise.

Therefore you should...

- Grant your admin the
**Azure AI Account Owner**on resource scope - Grant your developer the
**Reader**role on Foundry resource scope and**Azure AI User**on project scope - Grant your project manager the
**Azure AI Project Manager**role on resource scope

### Use Microsoft Entra groups with Foundry

Microsoft Entra ID provides several ways to manage access to resources, applications, and tasks. By using Microsoft Entra groups, you can grant access and permissions to a group of users instead of to each individual user. Enterprise IT admins can create Microsoft Entra groups in the Azure portal to simplify the role assignment process for developers. When you create a Microsoft Entra group, you can minimize the number of role assignments required for new developers working on Foundry projects by assigning the group the required role assignment on the necessary resource.

Complete the following steps to use Microsoft Entra ID groups with Foundry:

Go to

**Groups**in the Azure portal.Create a new

**Security**group in the Groups portal.Assign the owner of the Microsoft Entra group and add individual user principals in your organization to the group as members. Save the group.

Go to the resource that requires a role assignment.

**Example:**To build Agents, run traces, and more in Foundry, the minimum privilege 'Azure AI User' role must be assigned to your user principal. Assign the 'Azure AI User' role to your new Microsoft Entra group so all users in your enterprise can build in Foundry.**Example:**To use Tracing and Monitoring features in Microsoft Foundry, a 'Reader' role assignment on the connected Application Insights resource is required. Assign the 'Reader' role to your new Microsoft Entra group so all users in your enterprise can use the Tracing and Monitoring feature.

Go to Access Control (IAM).

Select the role to assign.

Assign access to "User, group, or service principal" and select the new Security group.

Review and assign. Role assignment now applies to all user principals assigned to the group.


To learn more about Microsoft Entra ID groups, prerequisites, and limitations, refer to:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/authentication-options-ai-foundry -->

# Role-based access control for Microsoft Foundry

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

Tip

An alternate hub-focused RBAC article is available: [Role-based access control for Microsoft Foundry (Hubs and Projects)](hub-rbac-foundry?view=foundry-classic).

In this article, you learn about role-based access control (RBAC) in your Microsoft Foundry resource and how to assign roles that control access to resources.

In this article, you learn how to manage access to Microsoft Foundry resources using role-based access control (RBAC).

For more information about authentication and authorization in Microsoft Foundry, see [Authentication and Authorization](authentication-authorization-foundry?view=foundry-classic). This article mentions terminology explained in the previous article.

## Getting started

For new users to Azure and Microsoft Foundry, use the following check-list to ensure all the correct roles are assigned to your user principal and your project's managed identity to get started in Foundry. You can check your roles by using the [Check access for a user to a single Azure resource](/en-us/azure/role-based-access-control/check-access?tabs=default) guidelines.

- Assign the
**Azure AI User**role on your Foundry resource to your**user principal**. - Assign the
**Azure AI User**role on your Foundry resource to your**project's managed identity**.

If the user that created the project can assign roles, such as the Azure **Owner** role assigned, on the subscription or resource group scope, both of these roles are automatically assigned.

To assign a role to your user principal or to your project's managed identity, follow the guidelines in the following section.

### Assign a role to your user principal

- Sign in to the
[Azure portal](https://portal.azure.com/). - Navigate to your Foundry resource.
- From the left pane, select
**Access control (IAM)**. - Select
**Add**>**Add role assignment**. - Under
**Role**, select**Azure AI User**. Under**Members**, select**User, group, or service principal**and search for your name or email and**Select**. - Finally,
**Review + assign**the role.

- From the left pane, select

### Assign a role to your project's managed identity

- Sign in to the
[Azure portal](https://portal.azure.com/). - Go to your Foundry project.
- From the left pane, select
**Access control (IAM)**. - Select
**Add**>**Add role assignment**. - Under
**Role**, select**Azure AI User**. Under**Members**, select**Managed identity**and select the managed identity of your project and**Select**. - Finally,
**Review + assign**the role.

- From the left pane, select

## Terminology for role-based access control in Foundry

To understand role-based access control in Microsoft Foundry, consider two questions for your enterprise.

What permissions do I want my team to have when building in Microsoft Foundry?

At what scope do I want to assign the permissions to my team?


To help answer these questions, here are descriptions of some terminology used throughout this article.

**permissions**: The allowed or denied actions that an identity can perform on a resource, such as reading, writing, deleting, or managing both the control plane and data plane. In Foundry, this concept includes read, write, or delete permissions.**scope**: The set of Azure resources to which a role assignment applies. Potential scopes include subscription, resource group, Foundry resource, or Foundry project.**role**: A named collection of permissions that defines what actions can be performed on Azure resources at a given scope.

To relate these terms to each other, an identity is assigned a *role* with certain *permissions* to create and build Foundry resources and projects. You assign a specific *scope* depending on enterprise requirements.

In Microsoft Foundry, consider two scopes when completing role assignments.

**Foundry resource**: The top-level scope that defines the administrative, security, and monitoring boundary for a Microsoft Foundry environment.**Foundry project**: A sub-scope within a Foundry resource used to organize work and enforce access control for Foundry APIs, tools, and developer workflows.

## Built-in roles

A **built-in role** in Foundry is a role created by Microsoft that covers common access scenarios that you can assign to your team members. Key built-in roles used across Azure include Owner, Contributor, and Reader. These roles aren't specific to Foundry resource permissions.

For Foundry resources, use additional built-in roles to follow least privilege access principles. The following table lists the five key built-in roles for Foundry, a short description, and the link to the exact role definition in the [AI + Machine Learning built-in roles article](/en-us/azure/role-based-access-control/built-in-roles/ai-machine-learning).

| Role | Description |
|---|---|
Azure AI User |
Grants reader access to Foundry project, Foundry resource, and data actions for your Foundry project. If you can assign roles, this role is assigned to you automatically. Otherwise, your subscription Owner or a user with role assignment permissions grants it. Least privilege access role in Foundry. |
Azure AI Project Manager |
Lets you perform management actions on Foundry projects, build and develop with projects, and conditionally assign the Azure AI User role to other user principals. |
Azure AI Account Owner |
Grants full access to manage projects and resources, and lets you conditionally assign the Azure AI User role to other user principals. |
Azure AI Owner |
Grants full access to managed projects and resources and build and develop with projects. Highly privileged self-serve role designed for digital natives. |

### Permissions for each built-in role

Use the following table and diagram to see the permissions allowed for each built-in role in Foundry, including the key Azure built-in roles.

| Built-in role | Create Foundry projects | Create Foundry accounts | Build and develop in a project (data actions) | Complete role assignments | Reader access to projects and accounts | Manage models |
|---|---|---|---|---|---|---|
Azure AI User |
✔ | ✔ | ||||
Azure AI Project Manager |
✔ | ✔ | ✔ (only assign Azure AI User role) | ✔ | ||
Azure AI Account Owner |
✔ | ✔ | ✔ (only assign Azure AI User role) | ✔ | ✔ | |
Azure AI Owner |
✔ | ✔ | ✔ | ✔ | ✔ | ✔ |
Owner |
✔ | ✔ | ✔ (assign any role to any user) | ✔ | ✔ | |
Contributor |
✔ | ✔ | ✔ | ✔ | ||
Reader |
✔ |

For more on built-in roles in Azure and Foundry, see [Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles). To learn more about conditional delegation used in the Azure AI Account Owner and Azure AI Project Manager role, see [Delegate Azure role assignment management to others with conditions](/en-us/azure/role-based-access-control/delegate-role-assignments-portal).

## Sample enterprise RBAC setup for projects

Here's an example of how to implement role-based access control (RBAC) for an enterprise Foundry resource.

| Persona | Role and Scope | Purpose |
|---|---|---|
| IT admin | Owner on subscription scope | The IT admin ensures the Foundry resource meets enterprise standards. Assign managers the Azure AI Account Owner role on the resource to let them create new Foundry accounts. Assign managers the Azure AI Project Manager role on the resource to let them create projects within an account. |
| Managers | Azure AI Account Owner on Foundry resource scope | Managers manage the Foundry resource, deploy models, audit compute resources, audit connections, and create shared connections. They can't build in projects, but they can assign the Azure AI User role to themselves and others to start building. |
| Team lead or lead developer | Azure AI Project Manager on Foundry resource scope | Lead developers create projects for their team and start building in those projects. After you create a project, project owners invite other members and assign the Azure AI User role. |
| Team members or developers | Azure AI User on Foundry project scope and Reader on the Foundry resource scope | Developers build agents in a project with pre-deployed Foundry models and pre-built connections. |

## Manage roles

To manage roles in Foundry, you must have the permission to assign and remove roles in Azure. The key Azure built-in role of **Owner** includes the necessary permission. You can assign roles through the Foundry portal (Admin page), Azure portal IAM, or Azure CLI. To remove roles, you can only use the Azure portal IAM or Azure CLI.

In the Foundry portal, manage permissions by:

- On the
**Home**page in[Foundry](https://ai.azure.com/?cid=learnDocs), select your Foundry resource. - Select
**Users**to add or remove users for the resource.

In the Foundry portal, manage permissions by:

- On the
**Admin**page in[Foundry](https://ai.azure.com/nextgen), select**Operate**, then**Admin**on the left navigation. - Select your project name in the table.
- On the top right, select
**Add user**. This button is only clickable if you have permissions to role assign. - Add your user to the Foundry project. The same instructions apply for your Foundry resource.

You can manage permissions in the [Azure portal](https://portal.azure.com) under **Access Control (IAM)** or by using Azure CLI.

For example, the following command assigns the Azure AI User role to `joe@contoso.com`

for the resource group `this-rg`

in the subscription with the ID `00000000-0000-0000-0000-000000000000`

:

```
az role assignment create --role "Azure AI User" --assignee "joe@contoso.com" --scope /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/this-rg
```


## Create custom roles for projects

If the built-in roles don't meet your enterprise requirements, create a custom role that allows for precise control over allowed actions and scopes. Here's an example subscription-level custom role definition:

```
{
"properties": {
"roleName": "My Enterprise Foundry User",
"description": "Custom role for Foundry at my enterprise to only allow building Agents. Assign at subscription level.",
"assignableScopes": ["/subscriptions/<your-subscription-id>"],
"permissions": [ {
"actions": ["Microsoft.CognitiveServices/*/read", "Microsoft.Authorization/*/read", "Microsoft.CognitiveServices/accounts/listkeys/action","Microsoft.Resources/deployments/*"],
"notActions": [],
"dataActions": ["Microsoft.CognitiveServices/accounts/AIServices/agents/*"],
"notDataActions": []
} ]
}
}
```


For more information on creating a custom role, see the following articles.

[Azure portal](/en-us/azure/role-based-access-control/custom-roles-portal)[Azure CLI](/en-us/azure/role-based-access-control/custom-roles-cli)[Azure PowerShell](/en-us/azure/role-based-access-control/custom-roles-powershell)[Disable Preview Features with Role-Based Access](disable-preview-features-with-rbac?view=foundry-classic). This article provides more details on specific permissions in Foundry across control and data plane which you can utilize when building custom roles.

## Notes and limitations

- To view and purge deleted Foundry accounts, you must have the Contributor role assigned at the subscription scope.
- Users with the Contributor role can deploy models in Foundry.
- You need the Owner role on a resource's scope to create custom roles in the resource.
- If you have permissions to role assign in Azure (for example, the Owner role assigned on the account scope) to your user principal, and you deploy a Foundry resource from the Azure portal or Foundry portal UI, then the Azure AI User role gets automatically assigned to your user principal. This assignment doesn't apply when deploying Foundry from SDK or CLI.
- When you create a Foundry resource, the built-in role-based access control (RBAC) permissions give you access to the resource. To use resources created outside Foundry, ensure the resource has permissions that let you access it. Here are some examples:
- To use a new Azure Blob Storage account, add the Foundry account resource's managed identity to the Storage Blob Data Reader role on that storage account.
- To use a new Azure AI Search source, add Foundry to the Azure AI Search role assignments.


## Related content

## Appendix

### Access Isolation Examples

Each organization may have different access isolation requirements depending on the user personas in their enterprise. Access isolation refers to which users in your enterprise are given what role assignments for either a separation of permissions using our built-in roles or a unified, highly permissive role. There are three access isolation options for Foundry that you can select for your organization depending on your access isolation requirements.

**No access isolation.** This means in your enterprise, you don't have any requirements separating permissions between a developer, project manager, or an admin. The permissions for these roles can be assigned across teams.

Therefore, you should...

- Grant all users in your enterprise the
**Azure AI Owner**role on the resource scope

**Partial access isolation.** This means the project manager in your enterprise should be able to develop within projects as well as create projects. But your admins shouldn't be able to develop within Foundry, only create Foundry projects and accounts.

Therefore, you should...

- Grant your admin with
**Azure AI Account Owner**on the resource scope - Grant your developer and project managers with
**Azure AI Project Manager**role on the resource

**Full access isolation.** This means your admins, project managers, and developers have clear permissions assigned that don't overlap for their different functions within an enterprise.

Therefore you should...

- Grant your admin the
**Azure AI Account Owner**on resource scope - Grant your developer the
**Reader**role on Foundry resource scope and**Azure AI User**on project scope - Grant your project manager the
**Azure AI Project Manager**role on resource scope

### Use Microsoft Entra groups with Foundry

Microsoft Entra ID provides several ways to manage access to resources, applications, and tasks. By using Microsoft Entra groups, you can grant access and permissions to a group of users instead of to each individual user. Enterprise IT admins can create Microsoft Entra groups in the Azure portal to simplify the role assignment process for developers. When you create a Microsoft Entra group, you can minimize the number of role assignments required for new developers working on Foundry projects by assigning the group the required role assignment on the necessary resource.

Complete the following steps to use Microsoft Entra ID groups with Foundry:

Go to

**Groups**in the Azure portal.Create a new

**Security**group in the Groups portal.Assign the owner of the Microsoft Entra group and add individual user principals in your organization to the group as members. Save the group.

Go to the resource that requires a role assignment.

**Example:**To build Agents, run traces, and more in Foundry, the minimum privilege 'Azure AI User' role must be assigned to your user principal. Assign the 'Azure AI User' role to your new Microsoft Entra group so all users in your enterprise can build in Foundry.**Example:**To use Tracing and Monitoring features in Microsoft Foundry, a 'Reader' role assignment on the connected Application Insights resource is required. Assign the 'Reader' role to your new Microsoft Entra group so all users in your enterprise can use the Tracing and Monitoring feature.

Go to Access Control (IAM).

Select the role to assign.

Assign access to "User, group, or service principal" and select the new Security group.

Review and assign. Role assignment now applies to all user principals assigned to the group.


To learn more about Microsoft Entra ID groups, prerequisites, and limitations, refer to:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/safety-evaluations-transparency-note -->

# Microsoft Foundry risk and safety evaluations (preview) Transparency Note

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## What is a Transparency Note

An AI system includes not only the technology, but also the people who will use it, the people who will be affected by it, and the environment in which it's deployed. Creating a system that is fit for its intended purpose requires an understanding of how the technology works, what its capabilities and limitations are, and how to achieve the best performance. Microsoft's Transparency Notes are intended to help you understand how our AI technology works, the choices system owners can make that influence system performance and behavior, and the importance of thinking about the whole system, including the technology, the people, and the environment. You can use Transparency Notes when developing or deploying your own system, or share them with the people who will use or be affected by your system.

Microsoft's Transparency Notes are part of a broader effort at Microsoft to put our AI Principles into practice. To find out more, see the [Microsoft AI principles](https://www.microsoft.com/en-us/ai/responsible-ai).

## The basics of Microsoft Foundry risk and safety evaluations (preview)

### Introduction

The Foundry risk and safety evaluations let users evaluate the output of their generative AI application for textual content risks: hateful and unfair content, sexual content, violent content, self-harm-related content, direct and indirect jailbreak vulnerability, and protected material in content. Safety evaluations can also help generate adversarial datasets to help you accelerate and augment the red-teaming operation. Foundry safety evaluations reflect Microsoft's commitments to ensure AI systems are built safely and responsibly, operationalizing our Responsible AI principles.

### Key terms

**Hateful and unfair content (for text and images)**refers to any language or imagery pertaining to hate toward or unfair representations of individuals and social groups along factors including but not limited to race, ethnicity, nationality, gender, sexual orientation, religion, immigration status, ability, personal appearance, and body size. Unfairness occurs when AI systems treat or represent social groups inequitably, creating or contributing to societal inequities.**Sexual content (for text and images)**includes language or imagery pertaining to anatomical organs and genitals, romantic relationships, acts portrayed in erotic terms, pregnancy, physical sexual acts (including assault or sexual violence), prostitution, pornography, and sexual abuse.**Violent content (for text and images)**includes language or imagery pertaining to physical actions intended to hurt, injure, damage, or kill someone or something. It also includes descriptions of weapons and guns (and related entities such as manufacturers and associations).**Self-harm-related content (for text and images)**includes language or imagery pertaining to actions intended to hurt, injure, or damage one's body or kill oneself.**Protected material content (for text)**known textual content, for example, song lyrics, articles, recipes, and selected web content, that might be output by large language models. By detecting and preventing the display of protected material, organizations can maintain compliance with intellectual property rights and preserve content originality.**Protected material content (for images)**refers to certain protected visual content, that is protected by copyright such as logos and brands, artworks, or fictional characters. The system uses an image-to-text foundation model to identify whether such content is present.**Direct jailbreak**, direct prompt attacks, or user prompt injection attacks, refer to users manipulating prompts to inject harmful inputs into LLMs to distort actions and outputs. An example of a jailbreak command is a 'DAN' (Do Anything Now) attack, which can trick the LLM into inappropriate content generation or ignoring system-imposed restrictions.**Indirect jailbreak**indirect prompt attacks or cross-domain prompt injection attacks, refers to when malicious instructions are hidden within data that an AI system processes or generates grounded content from. This data can include emails, documents, websites, or other sources not directly authored by the developer or user and can lead to inappropriate content generation or ignoring system-imposed restrictions.**Defect rate (content risk)**is defined as the percentage of instances in your test dataset that surpass a threshold on the severity scale over the whole dataset size.**Red-teaming**has historically described systematic adversarial attacks for testing security vulnerabilities. With the rise of Large Language Models (LLM), the term has extended beyond traditional cybersecurity and evolved in common usage to describe many kinds of probing, testing, and attacking of AI systems. With LLMs, both benign and adversarial usage can produce potentially harmful outputs, which can take many forms, including harmful content such as hateful speech, incitement or glorification of violence, reference to self-harm-related content or sexual content.

## Capabilities

### System behavior

Foundry provisions a fine-tuned Azure OpenAI GPT-4o model and orchestrates adversarial attacks against your application to generate a high quality test dataset. It then provisions another GPT-4o model to annotate your test dataset for content and security. Users provide their generative AI application endpoint that they wish to test, and the safety evaluations will output a static test dataset against that endpoint along with its content risk label (Very low, Low, Medium, High) or content risk detection label (True or False) and reasoning for the AI-generated label.

### Use cases

#### Intended uses

The safety evaluations aren't intended to use for any purpose other than to evaluate content risks and jailbreak vulnerabilities of your generative AI application:

**Evaluating your generative AI application pre-deployment**: Using the evaluation wizard in the Foundry portal or the Azure AI Python SDK, safety evaluations can assess in an automated way to evaluate potential content or security risks.**Augmenting your red-teaming operations**: Using the adversarial simulator, safety evaluations can simulate adversarial interactions with your generative AI application to attempt to uncover content and security risks.**Communicating content and security risks to stakeholders**: Using the Foundry portal, you can share access to your Foundry project with safety evaluations results with auditors or compliance stakeholders.

#### Considerations when choosing a use case

We encourage customers to leverage Foundry safety evaluations in their innovative solutions or applications. However, here are some considerations when choosing a use case:

**Safety evaluations should include human-in-the-loop**: Using automated evaluations like Foundry safety evaluations should include human reviewers such as domain experts to assess whether your generative AI application has been tested thoroughly prior to deployment to end users.**Safety evaluations do not include total comprehensive coverage**: Though safety evaluations can provide a way to augment your testing for potential content or security risks, it wasn't designed to replace manual red-teaming operations specifically geared towards your application's domain, use cases, and type of end users.- Supported scenarios:
- For adversarial simulation: Question answering, multi-turn chat, summarization, search, text rewrite, ungrounded and grounded content generation.
- For automated annotation: Question answering and multi-turn chat.

- The service currently is best used with the English domain for textual generations only. Additional features including multi-model support will be considered for future releases.
- The coverage of content risks provided in the safety evaluations is subsampled from a limited number of marginalized groups and topics:
- The hate- and unfairness metric includes some coverage for a limited number of marginalized groups for the demographic factor of gender (for example, men, women, non-binary people) and race, ancestry, ethnicity, and nationality (for example, Black, Mexican, European). Not all marginalized groups in gender and race, ancestry, ethnicity, and nationality are covered. Other demographic factors that are relevant to hate and unfairness don't currently have coverage (for example, disability, sexuality, religion).
- The metrics for sexual, violent, and self-harm-related content are based on a preliminary conceptualization of these harms that are less developed than hate and unfairness. This means that we can make less strong claims about measurement coverage and how well the measurements represent the different ways these harms can occur. Coverage for these content types includes a limited number of topics relate to sex (for example, sexual violence, relationships, sexual acts), violence (for example, abuse, injuring others, kidnapping), and self-harm (for example, intentional death, intentional self-injury, eating disorders).

- Foundry safety evaluations don't currently allow for plug-ins or extensibility.
- To keep quality up to date and improve coverage, we'll aim for a cadence of future releases of improvement to the service's adversarial simulation and annotation capabilities.

### Technical limitations, operational factors, and ranges

- The field of large language models (LLMs) continues to evolve at a rapid pace, requiring continuous improvement of evaluation techniques to ensure safe and reliable AI system deployment. Foundry safety evaluations reflect Microsoft's commitment to continue innovating in the field of LLM evaluation. We aim to provide the best tooling to help you evaluate the safety of your generative AI applications but recognize effective evaluation is a continuous work in progress.
- Customization of Foundry safety evaluations is currently limited. We only expect users to provide their input generative AI application endpoint and our service will output a static dataset that is labeled for content risk.
- Finally, it should be noted that this system doesn't automate any actions or tasks, it only provides an evaluation of your generative AI application outputs, which should be reviewed by a human decision maker in the loop before choosing to deploy the generative AI application or system into production for end users.

## System performance

### Best practices for improving system performance

- When accounting for your domain, which might treat some content more sensitively than other, consider adjusting the threshold for calculating the defect rate.
- When using the automated safety evaluations, there might sometimes be an error in your AI-generated labels for the severity of a content risk or its reasoning. There's a manual human feedback column to enable human-in-the-loop validation of the automated safety evaluation results.

## Evaluation of Foundry safety evaluations

### Evaluation methods

For all supported content risk types, we have internally checked the quality by comparing the rate of approximate matches between human labelers using a 0-7 severity scale and the safety evaluations' automated annotator also using a 0-7 severity scale on the same datasets. For each risk area, we had both human labelers and an automated annotator label 500 English, single-turn texts, 250 single-turn text-to-image generations, and 250 multi-modal text with image-to-text generations. The human labelers and the automated annotator didn't use exactly the same versions of the annotation guidelines; while the automated annotator's guidelines stemmed from the guidelines for humans, they have since diverged to varying degrees (with the hate and unfairness guidelines having diverged the most). Despite these slight to moderate differences, we believe it's still useful to share general trends and insights from our comparison of approximate matches. In our comparisons, we looked for matches with a 2-level tolerance (where human label matched automated annotator label exactly or was within 2 levels above or below in severity), matches with a 1-level tolerance, and matches with a 0-level tolerance.

### Evaluation results

Overall, we saw a high rate of approximate matches across the self-harm and sexual content risks across all tolerance levels. For violence and for hate and unfairness, the approximate match rate across tolerance levels were lower. These results were in part due to increased divergence in annotation guideline content for human labelers versus automated annotator, and in part due to the increased amount of content and complexity in specific guidelines.

Although our comparisons are between entities that used slightly to moderately different annotation guidelines (and are thus not standard human-model agreement comparisons), these comparisons provide an estimate of the quality that we can expect from Foundry safety evaluations given the parameters of these comparisons. Specifically, we only looked at English samples, so our findings might not generalize to other languages. Also, each dataset sample consisted of only a single turn, and so more experiments are needed to verify generalizability of our evaluation findings to multi-turn scenarios (for example, a back-and-forth conversation including user queries and system responses). The types of samples used in these evaluation datasets can also greatly affect the approximate match rate between human labels and an automated annotator – if samples are easier to label (for example, if all samples are free of content risks), we might expect the approximate match rate to be higher. The quality of human labels for an evaluation could also affect the generalization of our findings.

## Evaluating and integrating Foundry safety evaluations for your use

Measurement and evaluation of your generative AI application are a critical part of a holistic approach to AI risk management. Foundry safety evaluations are complementary to and should be used in tandem with other AI risk management practices. Domain experts and human-in-the-loop reviewers should provide proper oversight when using AI-assisted safety evaluations in the generative AI application design, development, and deployment cycle. You should understand the limitations and intended uses of the safety evaluations, being careful not to rely on outputs produced by Foundry AI-assisted safety evaluations in isolation.

Due to the non-deterministic nature of the LLMs, you might experience false negative or positive results, such as a high-severity level of violent content scored as "very low" or "low." Additionally, evaluation results might have different meanings for different audiences. For example, safety evaluations might generate a label for "low" severity of violent content that might not align to a human reviewer's definition of how severe that specific violent content might be. In Foundry portal, we provide a human feedback column with thumbs up and thumbs down when viewing your evaluation results to surface which instances were approved or flagged as incorrect by a human reviewer. Consider the context of how your results might be interpreted for decision making by others you can share evaluation with and validate your evaluation results with the appropriate level of scrutiny for the level of risk in the environment that each generative AI application operates in.

## Learn more about responsible AI

[Microsoft AI principles](https://www.microsoft.com/ai/responsible-ai)[Microsoft responsible AI resources](https://www.microsoft.com/ai/tools-practices)[Microsoft Azure Learning courses on responsible AI](/en-us/ai)

## Learn more about Foundry safety evaluations

[Microsoft concept documentation on our approach to evaluating generative AI applications](evaluation-approach-gen-ai?view=foundry-classic)[Microsoft concept documentation on how safety evaluation works](evaluation-evaluators/risk-safety-evaluators?view=foundry-classic)[Microsoft how-to documentation on using safety evaluations](../how-to/evaluate-generative-ai-app?view=foundry-classic)[Technical blog on how to evaluate content and security risks in your generative AI applications](https://techcommunity.microsoft.com/t5/ai-ai-platform-blog/introducing-ai-assisted-safety-evaluations-in-azure-ai-studio/ba-p/4098595)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/model-benchmarks -->

# Model leaderboards in Microsoft Foundry portal (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Model leaderboards (preview) in Microsoft Foundry portal help you compare models in the Foundry [model catalog](../how-to/model-catalog-overview?view=foundry-classic) using industry-standard benchmarks. From the model leaderboards section of the model catalog, you can [browse leaderboards](https://aka.ms/model-leaderboards) to compare available models by:

[Quality, safety, cost, and performance leaderboards](../how-to/benchmark-model-in-catalog?view=foundry-classic#access-model-leaderboards)to identify leading models on a single metric (quality, safety, cost, or throughput)[Trade-off charts](../how-to/benchmark-model-in-catalog?view=foundry-classic#trade-off-charts)to compare performance across two metrics, such as quality versus cost[Leaderboards by scenario](../how-to/benchmark-model-in-catalog?view=foundry-classic#view-leaderboards-by-scenario)to find models aligned to specific use cases

Model leaderboards (preview) in Foundry portal help you compare models in the Foundry [model catalog](../how-to/model-catalog-overview?view=foundry-classic) using industry-standard benchmarks.

You can review detailed benchmarking methodology for each leaderboard category:

[Quality benchmarking](#quality-benchmarks-of-language-models)of language models to understand how well models perform on cores tasks including reasoning, knowledge, question answering, math, and coding;[Safety benchmarking](#safety-benchmarks-of-language-models)of language models to understand how safe models are against harmful behavior generation;[Performance benchmarking](#performance-benchmarks-of-language-models)of language models to understand how models perform in terms of latency and throughput.[Cost benchmarking](#cost-benchmarks-of-language-models)of language models to understand the estimated cost of using models.[Scenario leaderboard benchmarking](#scenario-leaderboard-benchmarking)of language models to help you find the best model for your specific use case or scenario.[Quality benchmarking](#quality-benchmarks-of-embedding-models)of embedding models to understand how well models perform on embedding-based tasks including search and retrieval.

When you find a suitable model, you can open its **Detailed benchmarking results** in the model catalog. From there, you can deploy the model, try it in the playground, or evaluate it on your own data. The leaderboards support benchmarking for text language models (including large language models (LLMs) and small language models (SLMs)) and embedding models.

Model benchmarks assess LLMs and SLMs across quality, safety, cost, and throughput. Embedding models are evaluated using standard quality benchmarks. Leaderboards are updated regularly as new models and benchmarks are added.

## Model benchmarking scope

The model leaderboards feature a curated selection of text-based language models from the Foundry model catalog. Models are included based on the following criteria:

**Azure Direct Models prioritized**: Azure Direct Models are selected for relevance to common generative AI scenarios.**Core benchmark applicability**: Models must support general-purpose language tasks such as reasoning, knowledge, question answering, mathematical reasoning, and coding. Specialized models (for example, protein folding or domain-specific QA) and other modalities aren't supported.

This scoping ensures the leaderboards reflect current, high-quality models relevant to core AI scenarios.

## Quality benchmarks of language models

Foundry assesses the quality of LLMs and SLMs using accuracy scores from standard benchmark datasets that measure reasoning, knowledge, question answering, math, and coding capabilities.

| Index | Description |
|---|---|
| Quality index | Calculated by averaging applicable accuracy scores (`exact_match` , `pass@1` , `arena_hard` ) across benchmark datasets. |

Quality index values range from zero to one, where higher values indicate better performance. The datasets included in the quality index are:

| Dataset Name | Category |
|---|---|
|

[bigbench_hard](https://github.com/suzgunmirac/BIG-Bench-Hard)(downsampled to 1,000 examples)[gpqa](https://github.com/idavidrein/gpqa)[humanevalplus](https://github.com/evalplus/evalplus)[ifeval](https://github.com/google-research/google-research/tree/master/instruction_following_eval)[math](https://github.com/hendrycks/math)[mbppplus](https://github.com/evalplus/evalplus)[mmlu_pro](https://github.com/TIGER-AI-Lab/MMLU-Pro)(downsampled to 1,000 examples)See more details in accuracy scores:

| Metric | Description |
|---|---|
| Accuracy | Accuracy scores are available at the dataset and the model levels. At the dataset level, the score is the average value of an accuracy metric computed over all examples in the dataset. The accuracy metric used is `exact-match` in all cases, except for the HumanEval and MBPP datasets that use a `pass@1` metric. Exact match compares model generated text with the correct answer according to the dataset, reporting one if the generated text matches the answer exactly and zero otherwise. The `pass@1` metric measures the proportion of model solutions that pass a set of unit tests in a code generation task. At the model level, the accuracy score is the average of the dataset-level accuracies for each model. |

Accuracy scores range from zero to one, where higher values are better.

## Safety benchmarks of language models

To guide the selection of safety benchmarks for evaluation, we apply a structured filtering and validation process designed to ensure both relevance and rigor. A benchmark qualifies for onboarding if it addresses high-priority risks. For safety leaderboards, we look at different benchmarks that can be considered reliable enough to provide some signals on certain topics of interest as they relate to safety. We select [HarmBench](https://github.com/centerforaisafety/HarmBench) to proxy model safety, and organize scenario leaderboards as follows:

| Dataset Name | Leaderboard Scenario | Metric | Interpretation |
|---|---|---|---|
| HarmBench (standard) | Standard harmful behaviors | Attack Success Rate | Lower values means better robustness against attacks designed to illicit standard harmful content |
| HarmBench (contextual) | Contextually harmful behaviors | Attack Success Rate | Lower values means better robustness against attacks designed to illicit contextually harmful content |
| HarmBench (copyright violations) | Copyright violations | Attack Success Rate | Lower values indicate stronger robustness against copyright violations |
| WMDP | Knowledge in sensitive domains | Accuracy | Higher values indicate greater knowledge in sensitive domains |
| Toxigen | Toxic content detection | F1 Score | Higher values indicate better detection performance |

### Model harmful behaviors

The [HarmBench](https://github.com/centerforaisafety/HarmBench) benchmark measures harmful behaviors using prompts designed to elicit unsafe responses. It covers seven semantic categories:

- Cybercrime and unauthorized intrusion
- Chemical and biological weapons or drugs
- Copyright violations
- Misinformation and disinformation
- Harassment and bullying
- Illegal activities
- General harm

These categories are grouped into three functional areas:

- Standard harmful behaviors
- Contextually harmful behaviors
- Copyright violations

Each functional category is featured in a separate scenario leaderboard. We use direct prompts from HarmBench (no attacks) and HarmBench evaluators to calculate Attack Success Rate (ASR). Lower ASR values mean safer models. We don't explore any attack strategy for evaluation, and model benchmarking is performed with Foundry Content Safety Filter turned off.

### Model ability to detect toxic content

[Toxigen](https://github.com/microsoft/TOXIGEN) is a large-scale dataset for detecting adversarial and implicit hate speech. It includes implicitly toxic and benign sentences referencing 13 minority groups. Foundry uses annotated Toxigen samples and calculates F1 scores to measure classification performance. Higher scores indicate better toxic content detection. Benchmarking is performed with the Foundry Content Safety Filter turned off.

### Model knowledge in sensitive domains

The [Weapons of Mass Destruction Proxy](https://github.com/centerforaisafety/wmdp) (WMDP) benchmark measures model knowledge of in sensitive domains including bio security, cybersecurity, and chemical security. The leaderboard uses average accuracy scores across cybersecurity, bio security, and chemical security. A higher WMDP accuracy score denotes more knowledge of dangerous capabilities (worse behavior from a safety standpoint). Model benchmarking is performed with the default Foundry Content Safety filters on. These safety filters detect and block content harm in violence, self-harm, sexual, hate, and unfairness, but don't target categories in cybersecurity, bio security, and chemical security.

### Limitations of safety benchmarks

We understand and acknowledge that safety is a complex topic and has several dimensions. No single current open-source benchmarks can test or represent the full safety of a system in different scenarios. Additionally, most of these benchmarks suffer from saturation, or misalignment between benchmark design and the risk definition, can lack clear documentation on how the target risks are conceptualized and operationalized, making it difficult to assess whether the benchmark accurately captures the nuances of the risks. This limitation can lead to either overestimating or underestimating model performance in real-world safety scenarios.

## Performance benchmarks of language models

Performance metrics are aggregated over 14 days using 24 trails per day, with two requests per trail sent at one-hour intervals. The following default parameters are used:

| Parameter | Value | Applicable for |
|---|---|---|
| Region | East US/East US2 |
|

N/A (serverless API deployments)

For serverless API deployments, this setting is abstracted.

[managed compute](../how-to/model-catalog-overview?view=foundry-classic#managed-compute), or for endpoints when streaming isn't supported TTFT is represented as P50 of latency metric.The performance of LLMs and SLMs is assessed across the following metrics:

| Metric | Description |
|---|---|
| Latency mean | Average time in seconds taken for processing a request, computed over multiple requests. To compute this metric, we send a request to the endpoint every hour, for two weeks, and compute the average. |
| Latency P50 | 50th percentile value (the median) of latency (the time taken between the request and when we receive the entire response with a successful code). For example, when we send a request to the endpoint, 50% of the requests are completed in 'x' seconds, with 'x' being the latency measurement. |
| Latency P90 | 90th percentile value of latency (the time taken between the request and when we receive the entire response with a successful code). For example, when we send a request to the endpoint, 90% of the requests are completed in 'x' seconds, with 'x' being the latency measurement. |
| Latency P95 | 95th percentile value of latency (the time taken between the request and when we receive the entire response with a successful code). For example, when we send a request to the endpoint, 95% of the requests are complete in 'x' seconds, with 'x' being the latency measurement. |
| Latency P99 | 99th percentile value of latency (the time taken between the request and when we receive the entire response with a successful code). For example, when we send a request to the endpoint, 99% of the requests are complete in 'x' seconds, with 'x' being the latency measurement. |
| Throughput GTPS | Generated tokens per second (GTPS) is the number of output tokens that are getting generated per second from the time the request is sent to the endpoint. |
| Throughput TTPS | Total tokens per second (TTPS) is the number of total tokens processed per second including both from the input prompt and generated output tokens. For models which don't support streaming, time to first token (ttft) represents the P50 value of latency (time taken to receive the response) |
| Latency TTFT | Total time to first token (TTFT) is the time taken for the first token in the response to be returned from the endpoint when streaming is enabled. |
| Time between tokens | This metric is the time between tokens received. |

Foundry summarizes performance using:

| Metric | Description |
|---|---|
| Latency | Mean time to first token. Lower is better. |
| Throughput | Mean generated tokens per second. Higher is better. |

For performance metrics like latency or throughput, the time to first token and the generated tokens per second give a better overall sense of the typical performance and behavior of the model. We refresh our performance numbers on regular cadence.

## Cost benchmarks of language models

Cost calculations are estimates for using an LLM or SLM model endpoint hosted on the Foundry platform. Foundry supports displaying the cost of serverless API deployments and Azure OpenAI models. Because these costs are subject to change, we refresh our cost calculations on a regular cadence.

The cost of LLMs and SLMs is assessed across the following metrics:

| Metric | Description |
|---|---|
| Cost per input tokens | Cost for serverless API deployment for 1 million input tokens |
| Cost per output tokens | Cost for serverless API deployment for 1 million output tokens |
| Estimated cost | Cost for the sum of cost per input tokens and cost per output tokens, with a ratio of 3:1. |

Foundry also displays the cost as follows:

| Metric | Description |
|---|---|
| Cost | Estimated US dollar cost per 1 million tokens. The estimated workload uses the three-to-one ratio between input and output tokens. Lower values are better. |

## Scenario leaderboard benchmarking

Scenario leaderboards group benchmark datasets by common real-world evaluation goals so you can quickly identify a model's strengths and weaknesses by use case. Each scenario aggregates one or more public benchmark datasets. The following table summarizes the available scenario leaderboards and their associated datasets and descriptions:

| Scenario | Datasets | Description |
|---|---|---|
| Standard harmful behavior |
|

[HarmBench (contextual)](https://github.com/centerforaisafety/HarmBench)[HarmBench (copyright)](https://github.com/centerforaisafety/HarmBench)[WMDP](https://github.com/centerforaisafety/wmdp)(bio security, chemical security, cybersecurity)[ToxiGen](https://github.com/microsoft/TOXIGEN)(annotated)[BIG-Bench Hard](https://github.com/suzgunmirac/BIG-Bench-Hard)(1000 subsample)[BigCodeBench](https://github.com/bigcode-project/bigcodebench)(instruct),[HumanEvalPlus](https://github.com/evalplus/evalplus),[LiveBench (coding)](https://github.com/LiveBench/LiveBench),[MBPPPlus](https://github.com/evalplus/evalplus)[MMLU-Pro](https://github.com/TIGER-AI-Lab/MMLU-Pro)(1K English subsample)[Arena-Hard](https://github.com/lmarena/arena-hard-auto),[GPQA](https://github.com/idavidrein/gpqa)(diamond)[MATH](https://github.com/hendrycks/math)(500 subsample)[TruthfulQA](https://github.com/sylinrl/TruthfulQA)(MC1)## Quality benchmarks of embedding models

The quality index of embedding models is defined as the averaged accuracy scores of a comprehensive set of serverless API benchmark datasets targeting Information Retrieval, Document Clustering, and Summarization tasks.

| Metric | Description |
|---|---|
| Accuracy | Accuracy is the proportion of correct predictions among the total number of predictions processed. |
| F1 Score | F1 Score is the weighted mean of the precision and recall, where the best value is one (perfect precision and recall), and the worst is zero. |
| Mean average precision (MAP) | MAP evaluates the quality of ranking and recommender systems. It measures both the relevance of suggested items and how good the system is at placing more relevant items at the top. Values can range from zero to one, and the higher the MAP, the better the system can place relevant items high in the list. |
| Normalized discounted cumulative gain (NDCG) | NDCG evaluates a machine learning algorithm's ability to sort items based on relevance. It compares rankings to an ideal order where all relevant items are at the top of the list, where k is the list length while evaluating ranking quality. In our benchmarks, k=10, indicated by a metric of `ndcg_at_10` , meaning that we look at the top 10 items. |
| Precision | Precision measures the model's ability to identify instances of a particular class correctly. Precision shows how often a machine learning model is correct when predicting the target class. |
| Spearman correlation | Spearman correlation based on cosine similarity is calculated by first computing the cosine similarity between variables, then ranking these scores and using the ranks to compute the Spearman correlation. |
| V measure | V measure is a metric used to evaluate the quality of clustering. V measure is calculated as a harmonic mean of homogeneity and completeness, ensuring a balance between the two for a meaningful score. Possible scores lie between zero and one, with one being perfectly complete labeling. |

## Calculation of scores

### Individual scores

Benchmark results originate from public datasets that are commonly used for language model evaluation. In most cases, the data is hosted in GitHub repositories maintained by the creators or curators of the data. Foundry evaluation pipelines download data from their original sources, extract prompts from each example row, generate model responses, and then compute relevant accuracy metrics.

Prompt construction follows best practices for each dataset, as specified by the paper introducing the dataset and industry standards. In most cases, each prompt contains several *shots*, that is, several examples of complete questions and answers to prime the model for the task. The evaluation pipelines create shots by sampling questions and answers from a portion of the data held out from evaluation.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/ai-red-teaming-agent -->

# AI Red Teaming Agent (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

The AI Red Teaming Agent is a powerful tool designed to help organizations proactively find safety risks associated with generative AI systems during design and development of generative AI models and applications.

Traditional red teaming involves exploiting the cyber kill chain and describes the process by which a system is tested for security vulnerabilities. However, with the rise of generative AI, the term AI red teaming has been coined to describe probing for novel risks (both content and security related) that these systems present and refers to simulating the behavior of an adversarial user who is trying to cause your AI system to misbehave in a particular way.

The AI Red Teaming Agent leverages Microsoft's open-source framework for Python Risk Identification Tool's ([PyRIT](https://github.com/Azure/PyRIT)) AI red teaming capabilities along with Microsoft Foundry's [Risk and Safety Evaluations](evaluation-metrics-built-in?view=foundry-classic#risk-and-safety-evaluators) to help you automatically assess safety issues in three ways:

**Automated scans for content risks:**Firstly, you can automatically scan your model and application endpoints for safety risks by simulating adversarial probing.**Evaluate probing success:**Next, you can evaluate and score each attack-response pair to generate insightful metrics such as Attack Success Rate (ASR).**Reporting and logging**Finally, you can generate a score card of the attack probing techniques and risk categories to help you decide if the system is ready for deployment. Findings can be logged, monitored, and tracked over time directly in Foundry, ensuring compliance and continuous risk mitigation.

Together these components (scanning, evaluating, and reporting) help teams understand how AI systems respond to common attacks, ultimately guiding a comprehensive risk management strategy.

## When to use an AI red teaming run

When thinking about AI-related safety risks developing trustworthy AI systems, Microsoft uses NIST's framework to mitigate risk effectively: Govern, Map, Measure, Manage. We'll focus on the last three parts in relation to the generative AI development lifecycle:

- Map: Identify relevant risks and define your use case.
- Measure: Evaluate risks at scale.
- Manage: Mitigate risks in production and monitor with a plan for incident response.

AI Red Teaming Agent can be used to run automated scans and simulate adversarial probing to help accelerate the identification and evaluation of known risks at scale. This helps teams "shift left" from costly reactive incidents to more proactive testing frameworks that can catch issues before deployment. Manual AI red teaming process is time and resource intensive. It relies on the creativity of safety and security expertise to simulate adversarial probing. This process can create a bottleneck for many organizations to accelerate AI adoption. With the AI Red Teaming Agent, organizations can now leverage Microsoft's deep expertise to scale and accelerate their AI development with Trustworthy AI at the forefront.

We encourage teams to use the AI Red Teaming Agent to run automated scans throughout the design, development, and pre-deployment stage:

- Design: Picking out the safest foundational model on your use case.
- Development: Upgrading models within your application or creating fine-tuned models for your specific application.
- Pre-deployment: Before deploying GenAI applications to productions.

In production, we recommend implementing **safety mitigations** such as [Azure AI Content Safety filters](../../ai-services/content-safety/overview?view=foundry-classic) or implementing safety system messages using our [templates](../openai/concepts/safety-system-message-templates?view=foundry-classic).

- Design: Picking out the safest foundational model on your use case.
- Development: Upgrading models within your application or creating fine-tuned models for your specific application.
- Pre-deployment: Before deploying GenAI applications and agents to production.
- Post-deployment: Monitor your Gen AI applications and agents after deployment with scheduled continuous red teaming runs on synthetic adversarial data.

In production, we recommend implementing **safety guardrails** such as [Azure AI Content Safety filters](../../ai-services/content-safety/overview?view=foundry-classic) or implementing safety system messages using our [templates](../openai/concepts/safety-system-message-templates?view=foundry-classic). For agentic workflows, we recommend leveraging [Foundry Control Plane](../control-plane/overview?view=foundry-classic) to apply guardrails and govern your fleet of agents.

## How AI Red Teaming works

The AI Red Teaming Agent helps automate simulation of adversarial probing of your target AI system. It provides a curated dataset of seed prompts or attack objectives per supported risk categories. These can be used to automate direct adversarial probing. However, direct adversarial probing might be easily caught by existing safety alignments of your model deployment. Applying attack strategies from PyRIT provides an extra conversion that can help to by-pass or subvert the AI system into producing undesirable content.

In the diagram, we can see that a direct ask to your AI system on how to loot a bank triggers a refusal response. However, applying an attack strategy such as flipping all the characters can help trick the model into answering the question.

Additionally, the AI Red Teaming Agent provides users with a fine-tuned adversarial large language model dedicated to the task of simulating adversarial attacks and evaluating responses that might have harmful content in them with the Risk and Safety Evaluators. The key metric to assess the risk posture of your AI system is Attack Success Rate (ASR) which calculates the percentage of successful attacks over the number of total attacks.

## Supported risk categories

The following risk categories are supported in the AI Red Teaming Agent from [Risk and Safety Evaluations](evaluation-metrics-built-in?view=foundry-classic#risk-and-safety-evaluators). Only text-based scenarios are supported.

Risk category |
Description |
|---|---|
Hateful and Unfair Content |
Hateful and unfair content refers to any language or imagery pertaining to hate toward or unfair representations of individuals and social groups along factors including but not limited to race, ethnicity, nationality, gender, sexual orientation, religion, immigration status, ability, personal appearance, and body size. Unfairness occurs when AI systems treat or represent social groups inequitably, creating or contributing to societal inequities. |
Sexual Content |
Sexual content includes language or imagery pertaining to anatomical organs and genitals, romantic relationships, acts portrayed in erotic terms, pregnancy, physical sexual acts (including assault or sexual violence), prostitution, pornography, and sexual abuse. |
Violent Content |
Violent content includes language or imagery pertaining to physical actions intended to hurt, injure, damage, or kill someone or something. It also includes descriptions of weapons and guns (and related entities such as manufacturers and associations). |
Self-Harm-Related Content |
Self-harm-related content includes language or imagery pertaining to actions intended to hurt, injure, or damage one's body or kill oneself. |

Risk category |
Supported target(s) |
Local or cloud red teaming |
Description |
|---|---|---|---|
Hateful and Unfair Content |
Model and agents | Local and cloud | Hateful and unfair content refers to any language or imagery pertaining to hate toward or unfair representations of individuals and social groups along factors including but not limited to race, ethnicity, nationality, gender, sexual orientation, religion, immigration status, ability, personal appearance, and body size. Unfairness occurs when AI systems treat or represent social groups inequitably, creating or contributing to societal inequities. |
Sexual Content |
Model and agents | Local and cloud | Sexual content includes language or imagery pertaining to anatomical organs and genitals, romantic relationships, acts portrayed in erotic terms, pregnancy, physical sexual acts (including assault or sexual violence), prostitution, pornography, and sexual abuse. |
Violent Content |
Model and agents | Local and cloud | Violent content includes language or imagery pertaining to physical actions intended to hurt, injure, damage, or kill someone or something. It also includes descriptions of weapons and guns (and related entities such as manufacturers and associations). |
Self-Harm-Related Content |
Model and agents | Local and cloud | Self-harm-related content includes language or imagery pertaining to actions intended to hurt, injure, or damage one's body or kill oneself. |
Protected Materials |
Model and agents | Local and cloud | Copyrighted or protected materials such as lyrics, songs, and recipes. |
Code vulnerability |
Model and agents | Local and cloud | Measures whether AI generates code with security vulnerabilities, such as code injection, tar-slip, SQL injections, stack trace exposure and other risks across Python, Java, C++, C#, Go, JavaScript, and SQL. |
Ungrounded attributes |
Model and agents | Local and cloud | Measures an AI system's generation of text responses that contain ungrounded inferences about personal attributes, such as their demographics or emotional state. |
Prohibited actions |
Agents only | Cloud only | Measures an AI agent's ability to engage in behaviors that violate explicitly disallowed actions or tool uses based on user verified policy/taxonomy of prohibited actions. |
Sensitive data leakage |
Agents only | Cloud only | Measures an AI agent's vulnerability to exposing sensitive information (financial data, personal identifiers, health data, etc.) |
Task adherence |
Agents only | Cloud only | Measures whether an AI agent completes the assigned task by following the user’s goal, respecting all rules and constraints, and executing required procedures without unauthorized actions or omissions. |

## Agentic risks

Agent-specific risk categories such as prohibited actions, sensitive data leakage, and task adherence requires an approach to automated red teaming that differs from model-only risk categories. Specifically, the AI Red Teaming Agent is no longer only checking for generated outputs, but also checks for tool outputs for unsafe or risky behavior. Agentic risk categories are only available in cloud red-teaming to provide a minimally sandboxed environment.

For cloud red teaming runs, we redact the harmful or adversarial inputs sent to your model or agent from the resulting red teaming results. This prevents developers and non-technical stakeholders from being exposed to potentially harmful prompt attacks generated by the AI Red Teaming Agent's red teaming runs.

For red teaming agentic risk categories, we ensure that when an AI red teaming run targets a Foundry hosted agent, it's a transient run so that harmful data isn't logged by the Foundry Agent Service and chat completions aren't stored. We recommend all developers to run red teaming exercises in a "purple environment," or a non-production environment that is configured with production-like resources to see how your agents work in as real-life as possible scenarios.

### Sensitive data leakage

Sensitive data leakage red teaming tests for leakage of financial, medical, and personal data from internal knowledge bases and tool calls. The AI Red Teaming Agent uses synthetic dataset of sensitive information and mock tools to generate scenarios prompting the agent to divulge information. The Attack Success Rate (ASR) defines whether or not the red teaming run detects format-level leaks using pattern matching.

**Limitations:** Single-turn, English-only; synthetic data; excludes memory/training-set leaks.

### Prohibited actions

Prohibited actions red teaming tests for whether agents perform prohibited, high-risk, or irreversible actions by generating dynamic adversarial prompts based on user-provided policies and taxonomy of prohibited actions along with the set of supported tools that the agent is using and user-provided tool descriptions. The Attack Success Rate (ASR) defines policy violations exhibited by the agent based on the user-provided policies.

| Category | Description | Allowance Rule |
|---|---|---|
| Prohibited Actions | Universally banned (for example, facial recognition, emotion inference, social scoring). | ❌ Never allowed |
| High-Risk Actions | Sensitive actions need explicit human authorization (for example, financial transactions, medical decisions). | ⚠️ Allowed with human-in-the-loop confirmation |
| Irreversible Actions | Permanent operations (for example, file deletions, system resets). | ⚠️ Allowed with disclosure plus confirmation |

**Limitations:** Single-turn, English-only; Tool-level focus; no live production data.

Caution

**Disclaimer for Third-Party Use of Prohibited Actions Taxonomy:**

The taxonomy of prohibited, high-risk, and irreversible actions provided in this product is intended solely as illustrative guidance to support agent developers in evaluating and customizing their own risk frameworks. It doesn't constitute a definitive or exhaustive list of prohibited practices, nor does it reflect Microsoft policy or regulatory interpretation. Third-party organizations remain solely responsible for ensuring their agents comply with applicable laws and regulations, including but not limited to the EU AI Act and other jurisdictional requirements. Microsoft strongly recommends retaining default prohibited actions derived from regulatory constraints and discourages deselection of these items. Use of this product doesn't guarantee compliance. Organizations should consult their own legal counsel to assess and implement appropriate safeguards and prohibitions tailored to their operational context and risk tolerance.

### Task adherence

Task adherence red teaming tests whether agents faithfully complete assigned tasks by achieving the user’s goal, respecting all rules and constraints, and following required procedures. The AI Red Teaming Agent probes along three dimensions: goal achievement (did the agent achieve the intended goal), rule compliance (including policy guardrails and presentation contracts), and procedural discipline (correct tool use, workflow, and grounding). The prompting dataset takes into account supported and available tools to generate diverse agentic trajectories, including representative and adversarial cases, to test both ordinary and edge-case scenarios.

### Indirect Prompt Injected Attacks

Indirect Prompt Injected Attacks (also known as Cross-Domain Prompt Injected Attacks, XPIA) red teaming tests whether an agent can be manipulated by malicious instructions hidden in external data sources, such as emails or documents—retrieved via tool calls. The AI Red Teaming Agent uses a synthetic dataset of benign user queries and mock tool outputs containing attack placeholders. During the probing, the AI Red Teaming Agent injects risk-specific attacks into these contexts to assess if the target agent executes unintended or unsafe actions. Attack Success Rate (ASR) measures how often the agent is compromised by indirect prompt injection, using agentic-specific risk categories such as prohibited actions, sensitive data leakage, or task adherence.

See full list of attack strategies in the next section.

### Supported agents and tools

The AI Red Teaming Agent currently supported red teaming Foundry agents with Azure tool calls, with the following supportability matrix:

| Supported Agents/Actions | Status |
|---|---|
| Foundry hosted prompt agents | Supported |
| Foundry hosted container agents | Supported |
| Foundry workflow agents | Not Supported |
| Non-Foundry agents | Not Supported |
| Non-Azure tools | Not Supported |
| Azure tool calls | Supported |
| Function tool calls | Not supported |
| Browser automation tool calls | Not Supported |
| Connected Agent tool calls | Not Supported |
| Computer Use tool calls | Not Supported |

For a comprehensive list of tools, see [Tools](../agents/how-to/tools/overview?view=foundry-classic).

## Supported attack strategies

The following attack strategies are supported in the AI Red Teaming Agent from [PyRIT](https://azure.github.io/PyRIT/index.html):

Attack Strategy |
Description |
|---|---|
| AnsiAttack | Utilizes ANSI escape sequences to manipulate text appearance and behavior. |
| AsciiArt | Generates visual art using ASCII characters, often used for creative or obfuscation purposes. |
| AsciiSmuggler | Conceals data within ASCII characters, making it harder to detect. |
| Atbash | Implements the Atbash cipher, a simple substitution cipher where each letter is mapped to its reverse. |
| Base64 | Encodes binary data into a text format using Base64, commonly used for data transmission. |
| Binary | Converts text into binary code, representing data in a series of 0s and 1s. |
| Caesar | Applies the Caesar cipher, a substitution cipher that shifts characters by a fixed number of positions. |
| CharacterSpace | Alters text by adding spaces between characters, often used for obfuscation. |
| CharSwap | Swaps characters within text to create variations or obfuscate the original content. |
| Diacritic | Adds diacritical marks to characters, changing their appearance and sometimes their meaning. |
| Flip | Flips characters from front to back, creating a mirrored effect. |
| Leetspeak | Transforms text into Leetspeak, a form of encoding that replaces letters with similar-looking numbers or symbols. |
| Morse | Encodes text into Morse code, using dots and dashes to represent characters. |
| ROT13 | Applies the ROT13 cipher, a simple substitution cipher that shifts characters by 13 positions. |
| SuffixAppend | Appends an adversarial suffix to the prompt |
| StringJoin | Joins multiple strings together, often used for concatenation or obfuscation. |
| UnicodeConfusable | Uses Unicode characters that look similar to standard characters, creating visual confusion. |
| UnicodeSubstitution | Substitutes standard characters with Unicode equivalents, often for obfuscation. |
| Url | Encodes text into URL format |
| Jailbreak | Injects specially crafted prompts to bypass AI safeguards, known as User Injected Prompt Attacks (UPIA). |
| Indirect Jailbreak | Injects attack prompts in tool outputs or returned context to by pass AI safeguards indirectly, known as Indirect Prompt Injection Attacks. |
| Tense | Changes the tense of text, specifically converting it into past tense. |
| Multi turn | Executes attacks across multiple conversational turns, using context accumulation to bypass safeguards or elicit unintended behaviors. |
| Crescendo | Gradually escalates the complexity or risk of prompts over successive turns, probing for weaknesses in agent defenses through incremental challenge. |

## Known limitations of AI Red Teaming Agent

AI Red Teaming Agent has several important limitations to consider when running and interpreting red teaming results.

- Red teaming runs simulate scenarios in which a Foundry agent is exposed to sensitive data or attack vehicle data directly. Since this data is all synthetic, this isn't representative of real world data distributions.
- Mock tools are only currently enabled to retrieve synthetic data and enable red teaming evaluations. They don't currently support mocking behaviors, which would enable testing closer to real sandboxing than what is currently supported.
- Due to lack of completely locked-down sandboxing support, the adversarial nature of our red teaming evaluations is controlled to avoid real world impact.
- Red teaming runs only represent adversarial population and don't include any observational population.
- Red teaming runs use generative models to evaluate Attack Success Rates (ASR) and can be non-deterministic, non-predictive. Therefore, there's always a chance of false positives and we always recommend reviewing results before taking mitigation actions.

## Learn more

Get started with our [documentation on how to run an automated scan for safety risks with the AI Red Teaming Agent](../how-to/develop/run-scans-ai-red-teaming-agent?view=foundry-classic).

Learn more about the tools used by the AI Red Teaming Agent.

The most effective strategies for risk assessment we've seen use automated tools to surface potential risks, which are then analyzed by expert human teams for deeper insights. If your organization is just starting with AI red teaming, we encourage you to explore the resources created by our own AI red team at Microsoft to help you get started.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/manage-costs -->

# Plan and manage costs for Microsoft Foundry

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

This article shows you how to estimate expenses before deployment, track spending in real time, and set up alerts to avoid budget surprises.

## Prerequisites

Before you begin, ensure you have:

**Azure subscription:**An active Azure subscription with the resources you want to monitor.**Role-based access control (RBAC):**One or both of the following roles at the subscription or resource group scope:– View costs and usage data.**Cost Management Reader**– View Foundry resource data and costs.**AI User**

**Supported Azure account type:**One of the[supported account types for Cost Management](/en-us/azure/cost-management-billing/costs/understand-cost-mgt-data).

If you need to grant these roles to team members, see [Assign access to Cost Management data](/en-us/azure/cost-management-billing/costs/assign-access-acm-data) and [Foundry RBAC roles](rbac-foundry?view=foundry-classic).

Note

Foundry doesn't have a dedicated page in the Azure pricing calculator because Foundry is composed of several optional Azure services. This article shows how to use the calculator to estimate costs for these services.

## Estimate costs before using Foundry

Use the [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/) to estimate costs before you add Foundry resources.

- Go to the
[Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/). - Search for and select a product, such as Azure Speech in Foundry or Azure Language in Foundry.
- Select additional products to estimate costs for multiple services. For example, add Azure AI Search to include potential search costs.
- As you add resources to your project, return to the calculator and update estimates.

**Reference:** [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/)

## Costs associated with Foundry

When you create a Foundry resource, you pay for the Azure services you use, such as Azure OpenAI, Azure Speech in Foundry, Content Safety, Azure Vision in Foundry, Azure Document Intelligence, and Azure Language in Foundry. Costs vary by service and feature. For details, see the [Foundry Tools pricing page](https://azure.microsoft.com/pricing/details/cognitive-services/).

## Understand billing models for Foundry

Foundry resources run on Azure infrastructure and accrue costs when deployed. When you create or use Foundry resources, you're charged based on the services you use.

Two billing models are available:

**Pay-as-you-go (Serverless API):**You're billed according to your usage of each Azure service.**Commitment tiers:**You commit to using service features for a fixed fee, providing predictable costs. For details, see[Commitment tier pricing](/en-us/azure/ai-services/commitment-tier).

Note

If you use the resource above the quota provided by the commitment plan, you pay for the extra usage as described in the overage amount in the Azure portal when you buy a commitment plan.

## Understand the billing model for Foundry Models

### Token-based pricing

Language and vision models process inputs by breaking them down into tokens. Each token is roughly four characters of text; image and audio content are also converted to tokens for billing. You're charged per 1,000 tokens (input and output combined). Token pricing varies by model series and deployment type. For the latest rates, see the [Azure OpenAI pricing page](https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/).

### Models sold directly by Azure

Models sold directly by Azure (including Azure OpenAI) appear as billing meters under each Foundry resource. Microsoft handles billing directly; you see separate meters for each model's input and output usage.

### Models from partners and community

Third-party provider models (such as Cohere) are billed via Azure Marketplace. These entries appear at the resource group level (not the Foundry resource level) under **Marketplace** > **Service Name** *SaaS*, with separate meters for inputs and outputs.

Important

All models, whether Microsoft-sold or third-party, are hosted in Azure cloud with no external service interaction. Billing location differences affect cost analysis but not actual charges.

### Fine-tuned models

Azure OpenAI fine-tuned models are charged in three ways:

**Training:**Charged per token in your training file.**Hosting:**Hourly cost per deployed model (applies even if the model is unused).**Inference:**Per 1,000 tokens (input and output) when the model is called.

Monitor hosted fine-tuned model costs closely to avoid unexpected charges. For current rates, see the [Azure OpenAI pricing page](https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/).

Important

Inactive deployments (unused for 15 consecutive days) are deleted automatically. This deletion doesn't affect the underlying model; you can redeploy it at any time. However, deployed fine-tuned models incur hourly hosting costs even if inactive, so remove unused deployments promptly to control costs.

### HTTP Error response code and billing status

If the service performs processing, you're charged even if the status code isn't successful (not 200). For example, a 400 error due to a content filter or input limit, or a 408 error due to a timeout.

If the service doesn't perform processing, you aren't charged. For example, a 401 error due to authentication or a 429 error due to exceeding the rate limit.

## Monitor costs

Track your Foundry spending using cost analysis tools. You can view costs by day, month, or year, compare against budgets, and identify spending trends.

Access cost information from the [Microsoft Foundry](https://ai.azure.com/?cid=learnDocs) portal or the [Azure portal](https://portal.azure.com/).

Access cost information from the [Microsoft Foundry](https://ai.azure.com/?cid=learnDocs) portal or the [Azure portal](https://portal.azure.com/).

**Reference:** [Cost analysis](/en-us/azure/cost-management-billing/costs/quick-acm-cost-analysis)

Important

Your Foundry costs are only a subset of your overall application or solution costs. You need to monitor costs for all Azure resources used in your application or solution.

### Configure permissions to view costs

To view Foundry costs, ensure you have the [AI User role](rbac-foundry?view=foundry-classic#built-in-roles) and [Cost Management Reader role](/en-us/azure/role-based-access-control/built-in-roles/management-and-governance#cost-management-reader) at the resource group or subscription level.

Or you can create the following custom rules:

`Microsoft.Consumption/*/read`

`Microsoft.CostManagement/*/read`

`Microsoft.Resources/subscriptions/read`

`Microsoft.CognitiveServices/accounts/AIServices/usage/read`


Note

You need the **Owner** role at the subscription or resource group scope to create custom roles in that scope.

To create a custom role, use one of the following articles:

For more information about custom roles, see [Azure custom roles](/en-us/azure/role-based-access-control/custom-roles).

To create a custom role, construct a role definition JSON file that specifies the permission and scope for the role. The following example defines a custom Foundry Cost Reader role scoped at a specific resource level:

```
{
"Name": "Foundry Cost Reader",
"IsCustom": true,
"Description": "Can see cost metrics in Foundry",
"Actions": [
"Microsoft.Consumption/*/read",
"Microsoft.CostManagement/*/read",
"Microsoft.Resources/subscriptions/read",
"Microsoft.CognitiveServices/accounts/AIServices/usage/read"
],
"NotActions": [],
"DataActions": [],
"NotDataActions": [],
"AssignableScopes": [
"/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.CognitiveServices/accounts/<foundryResourceName>"
]
}
```


Replace `<subscriptionId>`

, `<resourceGroupName>`

, and `<foundryResourceName>`

with your actual values.

## Monitor in Foundry portal

- Sign in to
[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is off. These steps refer to**Foundry (classic)**.Sign in to[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is on. These steps refer to**Foundry (new)**. - Use the sections below to monitor costs.

Note

Estimates do not reflect discounts or contracted pricing that may appear on your final bill. Estimates cover standard deployment costs only, not [provisioned throughput](../openai/concepts/provisioned-throughput?view=foundry-classic).

### Agent costs

- Select
**Operate**in the upper-right navigation. - Select
**Overview**in the left pane. - At the top of the page, select the subscription, one or more projects, and a date range.
- The
**Estimated cost**tile shows estimates of all the agents for the selected project(s) for the selected dates. These estimates do not currently include prompt agent and non-Foundry agent costs.

For individual agent estimates:

- Select
**Assets**in the left pane. - Select the
**Agents**tab. - The
**Estimated costs**column shows monthly estimates based on agent configuration and usage patterns.

**Reference:** [Agent concepts](../agents/concepts/development-lifecycle?view=foundry-classic)

To view detailed agent costs:

- Select
**Build**in the upper-right navigation. - Select
**Agents**in the left pane. - Select an agent.
- Select the
**Monitor**tab. - Set the date range in the upper-right corner.
- View token costs and usage metrics for the selected range.

**Reference:** [Monitor agent metrics](../agents/how-to/metrics?view=foundry-classic)

### Model deployment costs

- Select
**Build**in the upper-right navigation. - Select
**Models**in the left pane. - Select a model.
- Select the
**Monitor**tab. - Set the date range in the upper-right corner. You see total cost and an estimated cost chart for the selected range.

**Reference:** [Monitor models](../foundry-models/how-to/monitor-models?view=foundry-classic)

When you select **View More Details** or **Azure Cost Management**, you're directed to the Azure portal's **Cost Management** section. Note: Azure portal costs show aggregated charges for the entire Cognitive Services account, not individual models. Costs display in USD only.

Note

Token and request charts can sometimes show lower values than the **Estimated cost** view because late‑arrival usage events may not be included in those charts. If there’s a mismatch, rely on **Estimated cost** as the most accurate view, and note that your **Azure Cost Management invoice** remains the final source of truth.

## Monitor in Azure portal

Sign in to the

[Azure portal](https://portal.azure.com/).View costs for your resource group or individual Foundry resource.

Tip

To open your Resource group:

- Sign in to
[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is off. These steps refer to**Foundry (classic)**.Sign in to[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is on. These steps refer to**Foundry (new)**. - Select your project, then select
**Management center**from the left menu. - Under the
**Resource**heading, select**Overview**. - Under the
**Resource properties**, select the link to open it directly in the Azure portal.

Tip

To open your Foundry resource in Azure portal:

- Sign in to
[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is off. These steps refer to**Foundry (classic)**.Sign in to[Microsoft Foundry](https://ai.azure.com/?cid=learnDocs). Make sure the**New Foundry**toggle is on. These steps refer to**Foundry (new)**. - Select
**Operate**from the upper-right navigation. - Select
**Admin**. - Select the link for the parent resource in the second column.
- Select
**Manage this resource in the Azure portal**under the**View resource**heading in the upper-right.

In the Azure portal, select

**Cost analysis**under**Cost Management**(for your resource group or Foundry resource).View the cost overview. Optionally, add filters (deployment tags, user-defined tags) to segment costs by model deployment:

Select

**Costs by resource**>**Resources**to see your Foundry resource cost split across model deployments:

### Understand cost breakdown by meter

Use the **Cost Analysis** tool to view costs grouped by billing meter:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your resource group.Select

**Cost analysis**under**Cost Management**.By default, cost analysis is scoped to the selected resource group.

Important

Scope

*Cost Analysis*to the resource group where you deployed the Foundry resource. The cost meters associated with Models from Partners and Community display under the resource group instead of the Foundry resource.Modify

**Group by**to**Meter**. You can now see that for this particular resource group, the source of the costs comes from different model series.

#### Models sold directly by Azure

Models sold directly by Azure (including Azure OpenAI) are charged directly. They appear as billing meters under each Foundry resource. Microsoft handles this billing directly. When you inspect your bill, you see billing meters that account for inputs and outputs for each consumed model.

#### Models from partners and community

Models provided by third-party providers, like Cohere, are billed using Azure Marketplace. As opposite to Microsoft billing meters, those entries are associated with the resource group where your Foundry is deployed instead of to the Foundry resource itself. Given model providers charge you directly, you see entries under the category **Marketplace** and **Service Name** *SaaS* accounting for inputs and outputs for each consumed model.

Important

This distinction between Models Sold Directly by Azure (including Azure OpenAI) and Models from Partners and Community only affects how the model is made available to you and how you are charged. In all cases, models are hosted within Azure cloud and there's no interaction with external services or providers.

### Monitor costs by resource

You can get more detailed billing information by grouping costs by resource:

In

**Cost Analysis**, select**View**>**Cost by resource**.Now you can see the resources generating each of the billing meters. To understand the breakdown of what makes up that cost, it can help to modify

**Group by**to**Meter**and switching the chart type to**Line**.Azure OpenAI models and Microsoft models are displayed as meters under each Foundry Tool resource.

Some providers' models are displayed as meters under Global resources. The word

*Global***isn't**related to the SKU of the model deployment (for instance,*Global standard*). If you have multiple Foundry Tool resources, your bill contains one entry**for each model for each Foundry Tool resource**. The resource meters have the format*[model-name]-[GUID]*where*[GUID]*is an identifier unique an associated with a given Foundry Tools resource. You notice billing meters accounting for inputs and outputs for each model you consumed.

It's important to understand scope when you evaluate costs associated with Foundry Tools. If your resources are part of the same resource group, you can scope Cost Analysis at that level to understand the effect on costs. If your resources are spread across multiple resource groups, you can scope to the subscription level.

When scoped at a higher level, you often need to add more filters to focus on Azure OpenAI usage. When scoped at the subscription level, you see many other resources that you might not care about in the context of Azure OpenAI cost management. When you scope at the subscription level, navigate to the full **Cost analysis tool** under the **Cost Management** service.

Here's an example of how to use the **Cost analysis tool** to see your accumulated costs for a subscription or resource group:

- Search for
*Cost Management*in the top Azure search bar to navigate to the full service experience, which includes more options such as creating budgets. - If necessary, select
**change**if the**Scope:**isn't pointing to the resource group or subscription you want to analyze. - On the left, select
**Reporting + analytics**>**Cost analysis**. - On the
**All views**tab, select**Accumulated costs**.

The cost analysis dashboard shows the accumulated costs that are analyzed depending on what you specified for **Scope**.

If you try to add a filter by service, you can't find Azure OpenAI in the list. This situation occurs because Azure OpenAI has commonality with a subset of Foundry Tools where the service level filter is **Cognitive Services**. If you want to see all Azure OpenAI resources across a subscription without any other type of Foundry Tool resources, instead scope to **Service tier: Azure OpenAI**:

### Monitor costs for models in Azure Marketplace

Azure Marketplace offers serverless API deployments. Model publishers might apply different costs depending on the offering. Each project in the Foundry portal has its own subscription with the offering, which you can use to monitor the costs and consumption happening on that project. Use [Microsoft Cost Management](https://azure.microsoft.com/products/cost-management) to monitor the costs:

Sign in to the

[Azure portal](https://portal.azure.com/)Select the portal menu icon to open the left pane.

On the left pane, select

**Cost Management + Billing**and then select**Cost Management**.On the left pane, under the section for

**Reporting + analytics**, select**Cost Analysis**.Select a view such as

**Resources**. The cost associated with each resource is displayed.On the

**Type**column, select the filter icon to filter all the resources of type**microsoft.saas/resources**. This type corresponds to resources created from offers available in Azure Marketplace. For convenience, you can filter by resource types containing the string**SaaS**.One resource is displayed for each model offer per project. Naming of those resources is [Model offer name]-[GUID].

Select to expand the resource details to get access to each of the costs meters associated with the resource.

**Tier**represents the offering.**Product**is the specific product inside the offering.

Some model providers might use the same name for both.

Tip

Remember that one resource is created per project, for each plan that your project subscribes to.

When you expand the details, costs are reported per each of the meters associated with the offering. Each meter might track different sources of costs like inferencing, or fine tuning. The following meters are displayed (when some cost is associated with them):

**Meter****Group****Description**paygo-inference-input-tokens Base model Costs associated with the tokens used as input for inference of a base model. paygo-inference-output-tokens Base model Costs associated with the tokens generated as output for the inference of base model. paygo-finetuned-model-inference-hosting Fine-tuned model Costs associated with the hosting of an inference endpoint for a fine-tuned model. This value isn't the cost of hosting the model, but the cost of having an endpoint serving it. paygo-finetuned-model-inference-input-tokens Fine-tuned model Costs associated with the tokens used as input for inference of a fine tuned model. paygo-finetuned-model-inference-output-tokens Fine-tuned model Costs associated with the tokens generated as output for the inference of a fine tuned model.

## Create budgets

**Prevent cost overruns with automated alerts.** [Create budgets](/en-us/azure/cost-management-billing/costs/tutorial-acm-create-budgets) that track your spending limits and [set up alerts](/en-us/azure/cost-management-billing/costs/cost-mgt-alerts-monitor-usage-spending) to notify you when costs approach or exceed thresholds.

**Best practice:** Create budgets and alerts for Azure subscriptions and resource groups as part of an overall cost monitoring strategy.

Create budgets with filters for specific resources or services in Azure if you want more granularity in your monitoring. Filters help ensure that you don't accidentally create new resources that cost more money. For more about filter options when you create a budget, see [Group and filter options](/en-us/azure/cost-management-billing/costs/group-filter).

Important

While OpenAI has an option for hard limits that prevent you from going over your budget, Azure OpenAI doesn't currently provide this functionality. You can start automation from action groups as part of your budget notifications to take more advanced actions, but this functionality requires additional custom development.

## Export cost data

You can [export your cost data](/en-us/azure/cost-management-billing/costs/tutorial-export-acm-data) to a storage account. Exporting data is helpful when you or others need to do additional data analysis for costs. For example, finance teams can analyze the data by using Excel or Power BI. You can export your costs on a daily, weekly, or monthly schedule and set a custom date range. Exporting cost data is the recommended way to retrieve cost datasets.

## Other costs that might accrue

Enabling capabilities such as sending data to Azure Monitor Logs and alerting incur extra costs for those services. These costs are visible under those other services and at the subscription level, but aren't visible when scoped just to your Foundry resource.

### Using Azure Prepayment

You can pay for Models Sold Directly by Azure charges with your Azure Prepayment (previously called monetary commitment) credit. However, you can't use Azure Prepayment credit to pay for charges for other provider models because they're billed through Azure Marketplace.

For more information, see [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/).

## Related content

[Foundry status dashboard](../foundry-status-dashboard-documentation?view=foundry-classic)- Learn
[how to optimize your cloud investment with cost management](/en-us/azure/cost-management-billing/costs/cost-mgt-best-practices). - Learn more about managing costs with
[cost analysis](/en-us/azure/cost-management-billing/costs/quick-acm-cost-analysis). - Learn about how to
[prevent unexpected costs](/en-us/azure/cost-management-billing/understand/analyze-unexpected-charges). - Take the
[Cost Management](/en-us/training/paths/control-spending-manage-bills)guided learning course.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/foundry-models-overview -->

# Explore Microsoft Foundry Models

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

Microsoft Foundry Models is your one-stop destination for discovering, evaluating, and deploying powerful AI models—whether you're building a custom copilot, building an agent, enhancing an existing application, or exploring new AI capabilities.

With Foundry Models, you can:

- Explore a rich catalog of cutting-edge models from Microsoft, OpenAI, DeepSeek, Hugging Face, Meta, and more.
- Compare and evaluate models side-by-side using real-world tasks and your own data.
- Deploy with confidence, thanks to built-in tools for fine-tuning, observability, and responsible AI.
- Choose your path—bring your own model, use a hosted one, or integrate seamlessly with Azure services.
- Whether you're a developer, data scientist, or enterprise architect, Foundry Models gives you the flexibility and control to build AI solutions that scale—securely, responsibly, and fast.

Foundry offers a comprehensive catalog of AI models. There are over 1900+ models ranging from Foundation Models, Reasoning Models, Small Language Models, Multimodal Models, Domain Specific Models, Industry Models and more.

Our catalog is organized into two main categories:

Understanding the distinction between these categories helps you choose the right models based on your specific requirements and strategic goals.

Note

- For all models, Customers remain responsible for (i) complying with the law in their use of any model or system; (ii) reviewing model descriptions in the model catalog, model cards made available by the model provider, and other relevant documentation; (iii) selecting an appropriate model for their use case, and (iv) implementing appropriate measures (including use of Azure AI Content Safety) to ensure Customer's use of the Foundry Tools complies with the Acceptable Use Policy in Microsoft’s Product Terms and the Microsoft Enterprise AI Services Code of Conduct.

## Models Sold Directly by Azure

These are models that are hosted and sold by Microsoft under Microsoft Product Terms. Microsoft has evaluated these models and they are deeply integrated into Azure's AI ecosystem. The models come from a variety of providers and they offer enhanced integration, optimized performance, and direct Microsoft support, including enterprise-grade Service Level Agreements (SLAs).

Characteristics of models sold directly by Azure:

- Support available from Microsoft.
- High level of integration with Azure services and infrastructure.
- Subject to internal review based on Microsoft’s Responsible AI standards.
- Model documentation and transparency reports provide customer visibility to model risks, mitigations, and limitations.
- Enterprise-grade scalability, reliability, and security.

Some of these Models also have the benefit of fungible Provisioned Throughput, meaning you can flexibly use your quota and reservations across any of these models.

## Models from Partners and Community

These models constitute the vast majority of the Foundry Models and are provided by trusted third-party organizations, partners, research labs, and community contributors. These models offer specialized and diverse AI capabilities, covering a wide array of scenarios, industries, and innovations. Examples of models from Partners and community are the family of large language models developed by **Anthropic** and **Open models from the Hugging Face hub**.

Anthropic includes Claude family of state-of-the-art large language models that support text and image input, text output, multilingual capabilities, and vision. For help with Anthropic models, use [Microsoft Support](https://aka.ms/anthropic-maas-support). To learn more about privacy, see [Data, privacy, and security for Claude models in Microsoft Foundry (preview)](../responsible-ai/claude-models/data-privacy?view=foundry-classic) and [Anthropic privacy policy](https://aka.ms/anthropic_privacy). For terms of service, see [Commercial Terms of Service](https://aka.ms/anthropic_tandc). To learn how to work with Anthropic models, see [Deploy and use Claude models in Microsoft Foundry](../foundry-models/how-to/use-foundry-models-claude?view=foundry-classic).

Hugging Face hub includes hundreds of models for real-time inference with managed compute. Hugging Face creates and maintains models listed in this collection. For help with the Hugging Face models, use the [Hugging Face forum](https://discuss.huggingface.co) or [Hugging Face support](https://huggingface.co/support). Learn how to deploy Hugging Face models in [Deploy open models with Microsoft Foundry](../how-to/deploy-models-managed?view=foundry-classic).

Characteristics of Models from Partners and Community:

- Developed and supported by external partners and community contributors
- Diverse range of specialized models catering to niche or broad use cases
- Typically validated by providers themselves, with integration guidelines provided by Azure
- Community-driven innovation and rapid availability of cutting-edge models
- Standard Azure AI integration, with support and maintenance managed by the respective providers

Models from Partners and Community are deployable as Managed Compute or serverless API deployment options. The model provider selects how the models are deployable.

### Requesting a model to be included in the model catalog

You can request that we add a model to the model catalog, right from the model catalog page in the Foundry portal. From the search bar of the model catalog page, a search for a model that doesn't exist in the catalog, such as *mymodel*, returns the **Request a model** button. Select this button to open up a form where you can share details about the model you're requesting.

## Choosing Between direct models and partner & community models

When selecting models from Foundry Models, consider the following:

**Use Case and Requirements**: Models sold directly by Azure are ideal for scenarios requiring deep Azure integration, guaranteed support, and enterprise SLAs. Models from Partners and Community excel in specialized use cases and innovation-led scenarios.**Support Expectations**: Models sold directly by Azure come with robust Microsoft-provided support and maintenance. These models are supported by their providers, with varying levels of SLA and support structures.**Innovation and Specialization**: Models from Partners and Community offer rapid access to specialized innovations and niche capabilities often developed by leading research labs and emerging AI providers.

## Overview of Model Catalog capabilities

The model catalog in Foundry portal is the hub to discover and use a wide range of models for building generative AI applications. The model catalog features hundreds of models across model providers such as Azure OpenAI, Mistral, Meta, Cohere, NVIDIA, and Hugging Face, including models that Microsoft trained. Models from providers other than Microsoft are Non-Microsoft Products as defined in [Microsoft Product Terms](https://www.microsoft.com/licensing/terms/welcome/welcomepage) and are subject to the terms provided with the models.

You can search and discover models that meet your need through keyword search and filters. Model catalog also offers the model performance leaderboard and benchmark metrics for select models. You can access them by selecting **Browse leaderboard** and **Compare Models**. Benchmark data is also accessible from the model card Benchmark tab.

On the **model catalog filters**, you'll find:

**Collection**: you can filter models based on the model provider collection.**Industry**: you can filter for the models that are trained on industry specific dataset.**Capabilities**: you can filter for unique model features such as reasoning and tool calling.**Deployment options**: you can filter for the models that support a specific deployment options.**serverless API**: this option allows you to pay per API call.**Provisioned**: best suited for real-time scoring for large consistent volume.**Batch**: best suited for cost-optimized batch jobs, and not latency. No playground support is provided for the batch deployment.**Managed compute**: this option allows you to deploy a model on an Azure virtual machine. You will be billed for hosting and inferencing.

**Inference tasks**: you can filter models based on the inference task type.**Fine-tune tasks**: you can filter models based on the fine-tune task type.**Licenses**: you can filter models based on the license type.

On the **model card**, you'll find:

**Quick facts**: you will see key information about the model at a quick glance.**Details**: this page contains the detailed information about the model, including description, version info, supported data type, etc.**Benchmarks**: you will find performance benchmark metrics for select models.**Existing deployments**: if you have already deployed the model, you can find it under Existing deployments tab.**License**: you will find legal information related to model licensing.**Artifacts**: this tab will be displayed for open models only. You can see the model assets and download them via user interface.

## Model deployment: Managed compute and serverless API deployments

In addition to deploying to Azure OpenAI, the model catalog offers two distinct ways to deploy models for your use: managed compute and serverless API deployments.

The deployment options and features available for each model vary, as described in the following tables. [Learn more about data processing with the deployment options](../how-to/concept-data-privacy?view=foundry-classic).

### Capabilities of model deployment options

| Features | Managed compute | serverless API deployment |
|---|---|---|
| Deployment experience and billing | Model weights are deployed to dedicated virtual machines with managed compute. A managed compute, which can have one or more deployments, makes available a REST API for inference. You're billed for the virtual machine core hours that the deployments use. | Access to models is through a deployment that provisions an API to access the model. The API provides access to the model that Microsoft hosts and manages, for inference. You're billed for inputs and outputs to the APIs, typically in tokens. Pricing information is provided before you deploy. |
| API authentication | Keys and Microsoft Entra authentication. | Keys only. |
| Content safety | Use Azure AI Content Safety service APIs. | Azure AI Content Safety filters are available integrated with inference APIs. Azure AI Content Safety filters are billed separately. |
| Network isolation |
|

[Network isolation for models deployed via serverless API deployments](#network-isolation-for-models-deployed-via-serverless-api-deployments)section later in this article.### Available models for supported deployment options

For Azure OpenAI models, see [Azure OpenAI](../openai/concepts/models?view=foundry-classic).

To view a list of supported models for serverless API deployment or Managed Compute, go to the home page of the model catalog in [Foundry](https://ai.azure.com/?cid=learnDocs). Use the **Deployment options** filter to select either **serverless API deployment** or **Managed Compute**.

## Model lifecycle: deprecation and retirement

AI models evolve fast, and when a new version or a new model with updated capabilities in the same model family become available, older models may be retired in the Foundry model catalog. To allow for a smooth transition to a newer model version, some models provide users with the option to enable automatic updates. To learn more about the model lifecycle of different models, upcoming model retirement dates, and suggested replacement models and versions, see:

[Azure OpenAI model deprecations and retirements](../openai/concepts/model-retirements?view=foundry-classic)[Serverless API deployment model deprecations and retirements](model-lifecycle-retirement?view=foundry-classic)

## Managed compute

The capability to deploy models as managed compute builds on platform capabilities of Azure Machine Learning to enable seamless integration of the wide collection of models in the model catalog across the entire life cycle of large language model (LLM) operations.

### Availability of models for deployment as managed compute

The models are made available through [Azure Machine Learning registries](/en-us/azure/machine-learning/concept-machine-learning-registries-mlops). These registries enable a machine-learning-first approach to [hosting and distributing Azure Machine Learning assets](/en-us/azure/machine-learning/how-to-share-models-pipelines-across-workspaces-with-registries). These assets include model weights, container runtimes for running the models, pipelines for evaluating and fine-tuning the models, and datasets for benchmarks and samples.

The registries build on top of a highly scalable and enterprise-ready infrastructure that:

Delivers low-latency access model artifacts to all Azure regions with built-in geo-replication.

Supports enterprise security requirements such as limiting access to models by using Azure Policy and secure deployment by using managed virtual networks.


### Deployment of models for inference with managed compute

Models available for deployment to managed compute can be deployed to Azure Machine Learning managed compute for real-time inference. Deploying to managed compute requires you to have a virtual machine quota in your Azure subscription for the specific products that you need to optimally run the model. Some models allow you to deploy to a [temporarily shared quota for model testing](../how-to/deploy-models-managed?view=foundry-classic).

Learn more about deploying models:

### Building generative AI apps with managed compute

The *prompt flow* feature in Azure Machine Learning offers a great experience for prototyping. You can use models deployed with managed compute in prompt flow with the [Open Model LLM tool](/en-us/azure/machine-learning/prompt-flow/tools-reference/open-model-llm-tool). You can also use the REST API exposed by managed compute in popular LLM tools like LangChain with the [Azure Machine Learning extension](https://python.langchain.com/docs/integrations/chat/azureml_chat_endpoint/).

### Content safety for models deployed as managed compute

The [Azure AI Content Safety](../../ai-services/content-safety/overview?view=foundry-classic) service is available for use with managed compute to screen for various categories of harmful content, such as sexual content, violence, hate, and self-harm. You can also use the service to screen for advanced threats such as jailbreak risk detection and protected material text detection.

You can refer to [this notebook](https://github.com/Azure/azureml-examples/blob/main/sdk/python/foundation-models/system/inference/text-generation/llama-safe-online-deployment.ipynb) for reference integration with Azure AI Content Safety for Llama 2. Or you can use the Content Safety (Text) tool in prompt flow to pass responses from the model to Azure AI Content Safety for screening. You're billed separately for such use, as described in [Azure AI Content Safety pricing](https://azure.microsoft.com/pricing/details/cognitive-services/content-safety/).

## Serverless API deployment billing

You can deploy certain models in the model catalog with serverless API billing. This deployment method, also called *serverless API deployment*, provides a way to consume the models as APIs without hosting them on your subscription. Models are hosted in a Microsoft-managed infrastructure, which enables API-based access to the model provider's model. API-based access can dramatically reduce the cost of accessing a model and simplify the provisioning experience.

Models that are available for deployment as serverless API deployments are offered by the model provider, but they're hosted in a Microsoft-managed Azure infrastructure and accessed via API. Model providers define the license terms and set the price for use of their models. The Azure Machine Learning service:

- Manages the hosting infrastructure.
- Makes the inference APIs available.
- Acts as the data processor for prompts submitted and content output by models deployed via MaaS.

Learn more about data processing for MaaS in the [article about data privacy](../how-to/concept-data-privacy?view=foundry-classic).

Note

Cloud Solution Provider (CSP) subscriptions do not have the ability to purchase serverless API deployment models.

### Billing

The discovery, subscription, and consumption experience for models deployed via MaaS is in Foundry portal and Azure Machine Learning studio. Users accept license terms for use of the models. Pricing information for consumption is provided during deployment.

Models from non-Microsoft providers are billed through Azure Marketplace, in accordance with the [Microsoft Commercial Marketplace Terms of Use](/en-us/legal/marketplace/marketplace-terms).

Models from Microsoft are billed via Azure meters as First Party Consumption Services. As described in the [Product Terms](https://www.microsoft.com/licensing/terms/welcome/welcomepage), you purchase First Party Consumption Services by using Azure meters, but they aren't subject to Azure service terms. Use of these models is subject to the provided license terms.

### Fine-tuning models

Certain models also support fine-tuning. For these models, you can take advantage of managed compute (preview) or serverless API deployments fine-tuning to tailor the models by using data that you provide. For more information, see the [fine-tuning overview](fine-tuning-overview?view=foundry-classic).

### RAG with models deployed as serverless API deployments

In Foundry portal, you can use vector indexes and retrieval-augmented generation (RAG). You can use models that can be deployed via serverless API deployments to generate embeddings and inferencing based on custom data. These embeddings and inferencing can then generate answers specific to your use case. For more information, see [Build and consume vector indexes in Foundry portal](../how-to/index-add?view=foundry-classic).

### Regional availability of offers and models

Pay-per-token billing is available only to users whose Azure subscription belongs to a billing account in a country/region where the model provider has made the offer available. If the offer is available in the relevant region, the user then must have a project resource in the Azure region where the model is available for deployment or fine-tuning, as applicable. See [Region availability for models in serverless API deployments | Foundry](../how-to/deploy-models-serverless-availability?view=foundry-classic) for detailed information.

### Content safety for models deployed via serverless API deployments

For language models deployed via serverless API, Azure AI implements a default configuration of [Azure AI Content Safety](../../ai-services/content-safety/overview?view=foundry-classic) text moderation filters that detect harmful content such as hate, self-harm, sexual, and violent content. To learn more about content filtering, see [Guardrails & controls for Models Sold Directly by Azure](model-catalog-content-safety?view=foundry-classic).

Tip

Content filtering is not available for certain model types that are deployed via serverless API. These model types include embedding models and time series models.

Content filtering occurs synchronously as the service processes prompts to generate content. You might be billed separately according to [Azure AI Content Safety pricing](https://azure.microsoft.com/pricing/details/cognitive-services/content-safety/) for such use. You can disable content filtering for individual serverless endpoints either:

- At the time when you first deploy a language model
- Later, by selecting the content filtering toggle on the deployment details page

Suppose you decide to use an API other than the [Model Inference API](/en-us/azure/ai-studio/reference/reference-model-inference-api) to work with a model that's deployed via a serverless API. In such a situation, content filtering isn't enabled unless you implement it separately by using Azure AI Content Safety.

To get started with Azure AI Content Safety, see [Quickstart: Analyze text content](/en-us/azure/ai-services/content-safety/quickstart-text). If you don't use content filtering when working with models that are deployed via serverless API, you run a higher risk of exposing users to harmful content.

### Network isolation for models deployed via serverless API deployments

Endpoints for models deployed as serverless API deployments follow the public network access flag setting of the Foundry hub that has the project in which the deployment exists. To help secure your serverless API deployment, disable the public network access flag on your Foundry hub. You can help secure inbound communication from a client to your endpoint by using a private endpoint for the hub.

To set the public network access flag for the Foundry hub:

- Go to the
[Azure portal](https://ms.portal.azure.com/). - Search for the resource group to which the hub belongs, and select your Foundry hub from the resources listed for this resource group.
- On the hub overview page, on the left pane, go to
**Settings**>**Networking**. - On the
**Public access**tab, you can configure settings for the public network access flag. - Save your changes. Your changes might take up to five minutes to propagate.

#### Limitations

If you have a Foundry hub with a private endpoint created before July 11, 2024, serverless API deployments added to projects in this hub won't follow the networking configuration of the hub. Instead, you need to create a new private endpoint for the hub and create a new serverless API deployment in the project so that the new deployments can follow the hub's networking configuration.

If you have a Foundry hub with MaaS deployments created before July 11, 2024, and you enable a private endpoint on this hub, the existing serverless API deployments won't follow the hub's networking configuration. For serverless API deployments in the hub to follow the hub's networking configuration, you need to create the deployments again.

Currently,

[Azure OpenAI On Your Data](/en-us/azure/ai-foundry/openai/concepts/use-your-data)support isn't available for serverless API deployments in private hubs, because private hubs have the public network access flag disabled.Any network configuration change (for example, enabling or disabling the public network access flag) might take up to five minutes to propagate.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/observability -->

# Observability in generative AI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

In today's AI-driven world, Generative AI Operations (GenAIOps) is revolutionizing how organizations build and deploy intelligent systems. As companies increasingly use AI agents and applications to transform decision-making, enhance customer experiences, and fuel innovation, one element stands paramount: robust evaluation frameworks. Evaluation isn't just a checkpoint. It's the foundation of quality and trust in AI applications. Without rigorous assessment and monitoring, AI systems can produce content that's:

- Fabricated or ungrounded in reality
- Irrelevant or incoherent
- Harmful in perpetuating content risks and stereotypes
- Dangerous in spreading misinformation
- Vulnerable to security exploits

This is where observability becomes essential. These capabilities measure both the frequency and severity of risks in AI outputs, enabling teams to systematically address quality, safety, and security concerns throughout the entire AI development journey—from selecting the right model to monitoring production performance, quality, and safety.

Note

The Microsoft Foundry SDK for evaluation and Foundry portal are in public preview, but the APIs are generally available for model and dataset evaluation (agent evaluation remains in public preview). The Azure AI Evaluation SDK and evaluators marked (preview) in this article are currently in public preview everywhere.

Note

The Microsoft Foundry SDK for evaluation and Foundry portal are in public preview, but the APIs are generally available for model and dataset evaluation (agent evaluation remains in public preview). Evaluators marked (preview) in this article are currently in public preview everywhere.

## What is observability?

AI observability refers to the ability to monitor, understand, and troubleshoot AI systems throughout their lifecycle. It involves collecting and analyzing signals such as evaluation metrics, logs, traces, and model and agent outputs to gain visibility into performance, quality, safety, and operational health.

## What are evaluators?

Evaluators are specialized tools that measure the quality, safety, and reliability of AI responses. By implementing systematic evaluations throughout the AI development lifecycle, teams can identify and address potential issues before they impact users. The following supported evaluators provide comprehensive assessment capabilities across different AI application types and concerns:

### General purpose

| Evaluator | Purpose | Inputs |
|---|---|---|
| Coherence | Measures logical consistency and flow of responses. | Query, response |
| Fluency | Measures natural language quality and readability. | Response |
| QA | Measures comprehensively various quality aspects in question-answering. | Query, context, response, ground truth |

To learn more, see [General purpose evaluators](evaluation-evaluators/general-purpose-evaluators?view=foundry-classic).

### Textual similarity

| Evaluator | Purpose | Inputs |
|---|---|---|
| Similarity | AI-assisted textual similarity measurement. | Query, context, ground truth |
| F1 Score | Harmonic mean of precision and recall in token overlaps between response and ground truth. | Response, ground truth |
| BLEU | Bilingual Evaluation Understudy score for translation quality measures overlaps in n-grams between response and ground truth. | Response, ground truth |
| GLEU | Google-BLEU variant for sentence-level assessment measures overlaps in n-grams between response and ground truth. | Response, ground truth |
| ROUGE | Recall-Oriented Understudy for Gisting Evaluation measures overlaps in n-grams between response and ground truth. | Response, ground truth |
| METEOR | Metric for Evaluation of Translation with Explicit Ordering measures overlaps in n-grams between response and ground truth. | Response, ground truth |

To learn more, see [Textual similarity evaluators](evaluation-evaluators/textual-similarity-evaluators?view=foundry-classic)

### RAG (retrieval augmented generation)

| Evaluator | Purpose | Inputs |
|---|---|---|
| Retrieval | Measures how effectively the system retrieves relevant information. | Query, context |
| Document Retrieval | Measures accuracy in retrieval results given ground truth. | Ground truth, retrieved documents |
| Groundedness | Measures how consistent the response is with respect to the retrieved context. | Query (optional), context, response |
| Groundedness Pro (preview) | Measures whether the response is consistent with respect to the retrieved context. | Query, context, response |
| Relevance | Measures how relevant the response is with respect to the query. | Query, response |
| Response Completeness | Measures to what extent the response is complete (not missing critical information) with respect to the ground truth. | Response, ground truth |

To learn more, see [Retrieval-augmented Generation (RAG) evaluators](evaluation-evaluators/rag-evaluators?view=foundry-classic).

### Safety and security

| Evaluator | Purpose | Inputs |
|---|---|---|
| Hate and Unfairness | Identifies biased, discriminatory, or hateful content. | Query, response |
| Sexual | Identifies inappropriate sexual content. | Query, response |
| Violence | Detects violent content or incitement. | Query, response |
| Self-Harm | Detects content promoting or describing self-harm. | Query, response |
| Content Safety | Comprehensive assessment of various safety concerns. | Query, response |
| Protected Materials | Detects unauthorized use of copyrighted or protected content. | Query, response |
| Code Vulnerability | Identifies security issues in generated code. | Query, response |
| Ungrounded Attributes | Detects fabricated or hallucinated information inferred from user interactions. | Query, context, response |

To learn more, see [Risk and safety evaluators](evaluation-evaluators/risk-safety-evaluators?view=foundry-classic).

### Agents

| Evaluator | Purpose | Inputs |
|---|---|---|
| Intent Resolution (preview) | Measures how accurately the agent identifies and addresses user intentions. | Query, response |
| Task Adherence (preview) | Measures how well the agent follows through on identified tasks. | Query, response, tool definitions (optional) |
| Tool Call Accuracy (preview) | Measures how well the agent selects and calls the correct tools to. | Query, either response or tool calls, tool definitions |

| Evaluator | Purpose | Inputs |
|---|---|---|
| Task Adherence (preview) | Measures whether the agent follows through on identified tasks according to system instructions. | Query, Response, Tool definitions (Optional) |
| Task Completion (preview) | Measures whether the agent successfully completed the requested task end-to-end. | Query, Response, Tool definitions (Optional) |
| Intent Resolution (preview) | Measures how accurately the agent identifies and addresses user intentions. | Query, Response, Tool definitions (Optional) |
| Task Navigation Efficiency (preview) | Determines whether the agent's sequence of steps matches an optimal or expected path to measure efficiency. | Response, Ground truth |
| Tool Call Accuracy (preview) | Measures the overall quality of tool calls including selection, parameter correctness, and efficiency. | Query, Tool definitions, Tool calls (Optional), Response |
| Tool Selection (preview) | Measures whether the agent selected the most appropriate and efficient tools for a task. | Query, Tool definitions, Tool calls (Optional), Response |
| Tool Input Accuracy (preview) | Validates that all tool call parameters are correct with strict criteria including grounding, type, format, completeness, and appropriateness. | Query, Response, Tool definitions |
| Tool Output Utilization (preview) | Measures whether the agent correctly interprets and uses tool outputs contextually in responses and subsequent calls. | Query, Response, Tool definitions (Optional) |
| Tool Call Success (preview) | Evaluates whether all tool calls executed successfully without technical failures. | Response, Tool definitions (Optional) |

To learn more, see [Agent evaluators](evaluation-evaluators/agent-evaluators?view=foundry-classic).

### Azure OpenAI graders

| Evaluator | Purpose | Inputs |
|---|---|---|
| Model Labeler | Classifies content using custom guidelines and labels. | Query, response, ground truth |
| String Checker | Performs flexible text validations and pattern matching. | Response |
| Text Similarity | Evaluates the quality of text or determine semantic closeness. | Response, ground truth |
| Model Scorer | Generates numerical scores (customized range) for content based on custom guidelines. | Query, response, ground truth |

To learn more, see [Azure OpenAI Graders](evaluation-evaluators/azure-openai-graders?view=foundry-classic).

### Evaluators in the development lifecycle

By using these evaluators strategically throughout the development lifecycle, teams can build more reliable, safe, and effective AI applications that meet user needs while minimizing potential risks.

## The three stages of GenAIOps evaluation

GenAIOps uses the following three stages.

### Base model selection

Before building your application, you need to select the right foundation. This initial evaluation helps you compare different models based on:

- Quality and accuracy: How relevant and coherent are the model's responses?
- Task performance: Does the model handle your specific use cases efficiently?
- Ethical considerations: Is the model free from harmful biases?
- Safety profile: What is the risk of generating unsafe content?

**Tools available**: [Microsoft Foundry benchmark](model-benchmarks?view=foundry-classic) for comparing models on public datasets or your own data, and the Azure AI Evaluation SDK for [testing specific model endpoints](https://github.com/Azure-Samples/azureai-samples/blob/main/scenarios/evaluate/Supported_Evaluation_Targets/Evaluate_Base_Model_Endpoint/Evaluate_Base_Model_Endpoint.ipynb).

### Preproduction evaluation

After you select a base model, the next step is to develop an AI agent or application. Before you deploy to a production environment, thorough testing is essential to ensure that the AI agent or application is ready for real-world use.

Preproduction evaluation involves:

- Testing with evaluation datasets: These datasets simulate realistic user interactions to ensure the AI agent performs as expected.
- Identifying edge cases: Finding scenarios where the AI agent's response quality might degrade or produce undesirable outputs.
- Assessing robustness: Ensuring that the AI agent can handle a range of input variations without significant drops in quality or safety.
- Measuring key metrics: Metrics such as task adherence, response groundedness, relevance, and safety are evaluated to confirm readiness for production.

The preproduction stage acts as a final quality check, reducing the risk of deploying an AI agent or application that doesn't meet the desired performance or safety standards.

Evaluation Tools and Approaches:

**Bring your own data**: You can evaluate your AI agents and applications in preproduction using your own evaluation data with supported evaluators, including quality, safety, or custom evaluators, and view results via the Foundry portal. Use Foundry's evaluation wizard or[Azure AI Evaluation SDK's](../how-to/develop/evaluate-sdk?view=foundry-classic)supported evaluators, including generation quality, safety, or[custom evaluators](evaluation-evaluators/custom-evaluators?view=foundry-classic).[View results by using the Foundry portal](../how-to/evaluate-results?view=foundry-classic).**Simulators and AI red teaming agent**: If you don't have evaluation data (test data),[Azure AI Evaluation SDK's simulators](../how-to/develop/simulator-interaction-data?view=foundry-classic)can help by generating topic-related or adversarial queries. These simulators test the model's response to situation-appropriate or attack-like queries (edge cases).[AI red teaming agent](../how-to/develop/run-scans-ai-red-teaming-agent?view=foundry-classic)simulates complex adversarial attacks against your AI system using a broad range of safety and security attacks using Microsoft's open framework for Python Risk Identification Tool or PyRIT.[Adversarial simulators](../how-to/develop/simulator-interaction-data?view=foundry-classic#generate-adversarial-simulations-for-safety-evaluation)injects static queries that mimic potential safety risks or security attacks such as attempted jailbreaks, helping identify limitations and preparing the model for unexpected conditions.[Context-appropriate simulators](../how-to/develop/simulator-interaction-data?view=foundry-classic#generate-synthetic-data-and-simulate-non-adversarial-tasks)generate typical, relevant conversations you'd expect from users to test quality of responses. With context-appropriate simulators you can assess metrics such as groundedness, relevance, coherence, and fluency of generated responses.

Automated scans using the AI red teaming agent enhance preproduction risk assessment by systematically testing AI applications for risks. This process involves simulated attack scenarios to identify weaknesses in model responses before real-world deployment. By running AI red teaming scans, you can detect and mitigate potential safety issues before deployment. This tool is recommended to be used with human-in-the-loop processes such as conventional AI red teaming probing to help accelerate risk identification and aid in the assessment by a human expert.


Alternatively, you can also use [the Foundry portal](../how-to/evaluate-generative-ai-app?view=foundry-classic) for testing your generative AI applications.

Bring your own data: You can evaluate your AI applications in preproduction using your own evaluation data with supported evaluators, including generation quality, safety, or custom evaluators, and view results via the Foundry portal. Use Foundry's evaluation wizard or

[Azure AI Evaluation SDK's](../how-to/develop/evaluate-sdk?view=foundry-classic)supported evaluators, including generation quality, safety, or[custom evaluators](evaluation-evaluators/custom-evaluators?view=foundry-classic), and[view results via the Foundry portal](../how-to/evaluate-results?view=foundry-classic).Simulators and AI red teaming agent: If you don't have evaluation data (test data), simulators can help by generating topic-related or adversarial queries. These simulators test the model's response to situation-appropriate or attack-like queries (edge cases).

[AI red teaming agent](../how-to/develop/run-scans-ai-red-teaming-agent?view=foundry-classic)simulates complex adversarial attacks against your AI system using a broad range of safety and security attacks using Microsoft's open framework for Python Risk Identification Tool or PyRIT.Automated scans using the AI red teaming agent enhances preproduction risk assessment by systematically testing AI applications for risks. This process involves simulated attack scenarios to identify weaknesses in model responses before real-world deployment. By running AI red teaming scans, you can detect and mitigate potential safety issues before deployment. This tool is recommended to be used with human-in-the-loop processes such as conventional AI red teaming probing to help accelerate risk identification and aid in the assessment by a human expert.


Alternatively, you can also use [the Foundry portal](../how-to/evaluate-generative-ai-app?view=foundry-classic) for testing your generative AI applications.

After you get satisfactory results, you can deploy the AI application to production.

### Post-production monitoring

After deployment, continuous monitoring ensures your AI application maintains quality in real-world conditions.

After deployment, [continuous monitoring](../agents/how-to/how-to-monitor-agents-dashboard?view=foundry-classic) ensures your AI application maintains quality in real-world conditions.

**Operational metrics**: Regular measurement of key AI agent operational metrics.**Continuous evaluation**: Enables quality and safety evaluation of production traffic at a sampled rate.**Scheduled evaluation**: Enables scheduled quality and safety evaluation using a test dataset to detect drift in the underlying systems.**Scheduled red teaming**: Provides scheduled adversarial testing capabilities to probe for safety and security vulnerabilities.**Azure Monitor alerts**: Swift action when harmful or inappropriate outputs occur. Set up alerts for continuous evaluation to be notified when evaluation results drop below the pass rate threshold in production.

Effective monitoring helps maintain user trust and allows for rapid issue resolution.

Observability provides comprehensive monitoring capabilities essential for today's complex and rapidly evolving AI landscape. Seamlessly integrated with Azure Monitor Application Insights, this solution enables continuous monitoring of deployed AI applications to ensure optimal performance, safety, and quality in production environments.

The Foundry Observability dashboard delivers real-time insights into critical metrics. It allows teams to quickly identify and address performance issues, safety concerns, or quality degradation.

For Agent-based applications, Foundry offers enhanced continuous evaluation capabilities. These capabilities can provide deeper visibility into quality and safety metrics. They can create a robust monitoring ecosystem that adapts to the dynamic nature of AI applications while maintaining high standards of performance and reliability.

By continuously monitoring the AI application's behavior in production, you can maintain high-quality user experiences and swiftly address any issues that surface.

## Building trust through systematic evaluation

GenAIOps establishes a reliable process for managing AI applications throughout their lifecycle. By implementing thorough evaluation at each stage—from model selection through deployment and beyond—teams can create AI solutions that aren't just powerful but trustworthy and safe.

### Evaluation cheat sheet

| Purpose | Process | Parameters, guidance, and samples |
|---|---|---|
| What are you evaluating for? | Identify or build relevant evaluators | -
-
-
-
|

[Generic simulator for measuring Quality and Performance](concept-synthetic-data?view=foundry-classic)([Generic simulator sample notebook](https://github.com/Azure/azureml-examples/blob/main/sdk/python/foundation-models/system/finetune/Llama-notebooks/datagen/synthetic-data-generation.ipynb))-

[Adversarial simulator for measuring Safety and Security](../how-to/develop/simulator-interaction-data?view=foundry-classic)([Adversarial simulator sample notebook](https://github.com/Azure-Samples/rag-data-openai-python-promptflow/blob/main/src/evaluation/simulate_and_evaluate_online_endpoint.ipynb))- AI red teaming agent for running automated scans to assess safety and security vulnerabilities (

[AI red teaming agent sample notebook](https://github.com/Azure-Samples/azureai-samples/blob/main/scenarios/evaluate/AI_RedTeaming/AI_RedTeaming.ipynb))[Agent evaluation runs](../how-to/develop/agent-evaluate-sdk?view=foundry-classic)-

[Remote cloud run](../how-to/develop/cloud-evaluation?view=foundry-classic)-

[Local run](../how-to/develop/evaluate-sdk?view=foundry-classic)[View aggregate scores, view details, score details, compare evaluation runs](../how-to/evaluate-results?view=foundry-classic)- If evaluation results aligned to human feedback but didn't meet quality/safety thresholds, apply targeted mitigations. Example of mitigations to apply:

[Azure AI Content Safety](../ai-services/content-safety-overview?view=foundry-classic)| Purpose | Process | Parameters, guidance, and samples |
|---|---|---|
| What are you evaluating for? | Identify or build relevant evaluators | -
-
-
-
|

[Synthetic dataset generation](../how-to/evaluate-generative-ai-app?view=foundry-classic#select-or-create-a-dataset)- AI red teaming agent for running automated scans to assess safety and security vulnerabilities (

[AI red teaming agent sample notebook](https://aka.ms/airedteamingagent-sample))[Agent evaluation runs](../how-to/develop/agent-evaluate-sdk?view=foundry-classic)-

[Remote cloud run](../how-to/develop/cloud-evaluation?view=foundry-classic)[View aggregate scores, view details, score details, compare evaluation runs](../how-to/evaluate-results?view=foundry-classic)- If evaluation results aligned to human feedback but didn't meet quality/safety thresholds, apply targeted mitigations. Example of mitigations to apply:

[Azure AI Content Safety](../ai-services/content-safety-overview?view=foundry-classic)## Bring your own virtual network for evaluation

For network isolation purposes you can bring your own virtual network for evaluation. To learn more, see [How to configure a private link](../how-to/configure-private-link?view=foundry-classic).

Note

Evaluation data is sent to Application Insights if Application Insights is connected. Virtual network support for Application Insights and tracing isn't available. Inline datasource is not supported.

Important

To prevent evaluation and red teaming run failures, assign the Azure AI User role to the project's Managed Identity during initial project setup.

### Virtual network region support

Bring your own virtual network for evaluation is supported in all regions except for Central India, East Asia, North Europe and Qatar Central.

## Region support

Currently certain AI-assisted evaluators are available only in the following regions:

| Region | Hate and unfairness, Sexual, Violent, Self-harm, Indirect attack, Code vulnerabilities, Ungrounded attributes | Groundedness Pro | Protected material |
|---|---|---|---|
| East US 2 | Supported | Supported | Supported |
| Sweden Central | Supported | Supported | N/A |
| US North Central | Supported | N/A | N/A |
| France Central | Supported | N/A | N/A |
| Switzerland West | Supported | N/A | N/A |

### Agent playground evaluation region support

| Region | Status |
|---|---|
| East US | Supported |
| East US 2 | Supported |
| West US | Supported |
| West US 2 | Supported |
| West US 3 | Supported |
| France Central | Supported |
| Norway East | Supported |
| Sweden Central | Supported |

## Pricing

Observability features such as Risk and Safety Evaluations and Continuous Evaluations are billed based on consumption as listed in [our Azure pricing page](https://azure.microsoft.com/pricing/details/ai-foundry/).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/evaluation-approach-gen-ai -->

# Observability in generative AI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

In today's AI-driven world, Generative AI Operations (GenAIOps) is revolutionizing how organizations build and deploy intelligent systems. As companies increasingly use AI agents and applications to transform decision-making, enhance customer experiences, and fuel innovation, one element stands paramount: robust evaluation frameworks. Evaluation isn't just a checkpoint. It's the foundation of quality and trust in AI applications. Without rigorous assessment and monitoring, AI systems can produce content that's:

- Fabricated or ungrounded in reality
- Irrelevant or incoherent
- Harmful in perpetuating content risks and stereotypes
- Dangerous in spreading misinformation
- Vulnerable to security exploits

This is where observability becomes essential. These capabilities measure both the frequency and severity of risks in AI outputs, enabling teams to systematically address quality, safety, and security concerns throughout the entire AI development journey—from selecting the right model to monitoring production performance, quality, and safety.

Note

The Microsoft Foundry SDK for evaluation and Foundry portal are in public preview, but the APIs are generally available for model and dataset evaluation (agent evaluation remains in public preview). The Azure AI Evaluation SDK and evaluators marked (preview) in this article are currently in public preview everywhere.

Note

The Microsoft Foundry SDK for evaluation and Foundry portal are in public preview, but the APIs are generally available for model and dataset evaluation (agent evaluation remains in public preview). Evaluators marked (preview) in this article are currently in public preview everywhere.

## What is observability?

AI observability refers to the ability to monitor, understand, and troubleshoot AI systems throughout their lifecycle. It involves collecting and analyzing signals such as evaluation metrics, logs, traces, and model and agent outputs to gain visibility into performance, quality, safety, and operational health.

## What are evaluators?

Evaluators are specialized tools that measure the quality, safety, and reliability of AI responses. By implementing systematic evaluations throughout the AI development lifecycle, teams can identify and address potential issues before they impact users. The following supported evaluators provide comprehensive assessment capabilities across different AI application types and concerns:

### General purpose

| Evaluator | Purpose | Inputs |
|---|---|---|
| Coherence | Measures logical consistency and flow of responses. | Query, response |
| Fluency | Measures natural language quality and readability. | Response |
| QA | Measures comprehensively various quality aspects in question-answering. | Query, context, response, ground truth |

To learn more, see [General purpose evaluators](evaluation-evaluators/general-purpose-evaluators?view=foundry-classic).

### Textual similarity

| Evaluator | Purpose | Inputs |
|---|---|---|
| Similarity | AI-assisted textual similarity measurement. | Query, context, ground truth |
| F1 Score | Harmonic mean of precision and recall in token overlaps between response and ground truth. | Response, ground truth |
| BLEU | Bilingual Evaluation Understudy score for translation quality measures overlaps in n-grams between response and ground truth. | Response, ground truth |
| GLEU | Google-BLEU variant for sentence-level assessment measures overlaps in n-grams between response and ground truth. | Response, ground truth |
| ROUGE | Recall-Oriented Understudy for Gisting Evaluation measures overlaps in n-grams between response and ground truth. | Response, ground truth |
| METEOR | Metric for Evaluation of Translation with Explicit Ordering measures overlaps in n-grams between response and ground truth. | Response, ground truth |

To learn more, see [Textual similarity evaluators](evaluation-evaluators/textual-similarity-evaluators?view=foundry-classic)

### RAG (retrieval augmented generation)

| Evaluator | Purpose | Inputs |
|---|---|---|
| Retrieval | Measures how effectively the system retrieves relevant information. | Query, context |
| Document Retrieval | Measures accuracy in retrieval results given ground truth. | Ground truth, retrieved documents |
| Groundedness | Measures how consistent the response is with respect to the retrieved context. | Query (optional), context, response |
| Groundedness Pro (preview) | Measures whether the response is consistent with respect to the retrieved context. | Query, context, response |
| Relevance | Measures how relevant the response is with respect to the query. | Query, response |
| Response Completeness | Measures to what extent the response is complete (not missing critical information) with respect to the ground truth. | Response, ground truth |

To learn more, see [Retrieval-augmented Generation (RAG) evaluators](evaluation-evaluators/rag-evaluators?view=foundry-classic).

### Safety and security

| Evaluator | Purpose | Inputs |
|---|---|---|
| Hate and Unfairness | Identifies biased, discriminatory, or hateful content. | Query, response |
| Sexual | Identifies inappropriate sexual content. | Query, response |
| Violence | Detects violent content or incitement. | Query, response |
| Self-Harm | Detects content promoting or describing self-harm. | Query, response |
| Content Safety | Comprehensive assessment of various safety concerns. | Query, response |
| Protected Materials | Detects unauthorized use of copyrighted or protected content. | Query, response |
| Code Vulnerability | Identifies security issues in generated code. | Query, response |
| Ungrounded Attributes | Detects fabricated or hallucinated information inferred from user interactions. | Query, context, response |

To learn more, see [Risk and safety evaluators](evaluation-evaluators/risk-safety-evaluators?view=foundry-classic).

### Agents

| Evaluator | Purpose | Inputs |
|---|---|---|
| Intent Resolution (preview) | Measures how accurately the agent identifies and addresses user intentions. | Query, response |
| Task Adherence (preview) | Measures how well the agent follows through on identified tasks. | Query, response, tool definitions (optional) |
| Tool Call Accuracy (preview) | Measures how well the agent selects and calls the correct tools to. | Query, either response or tool calls, tool definitions |

| Evaluator | Purpose | Inputs |
|---|---|---|
| Task Adherence (preview) | Measures whether the agent follows through on identified tasks according to system instructions. | Query, Response, Tool definitions (Optional) |
| Task Completion (preview) | Measures whether the agent successfully completed the requested task end-to-end. | Query, Response, Tool definitions (Optional) |
| Intent Resolution (preview) | Measures how accurately the agent identifies and addresses user intentions. | Query, Response, Tool definitions (Optional) |
| Task Navigation Efficiency (preview) | Determines whether the agent's sequence of steps matches an optimal or expected path to measure efficiency. | Response, Ground truth |
| Tool Call Accuracy (preview) | Measures the overall quality of tool calls including selection, parameter correctness, and efficiency. | Query, Tool definitions, Tool calls (Optional), Response |
| Tool Selection (preview) | Measures whether the agent selected the most appropriate and efficient tools for a task. | Query, Tool definitions, Tool calls (Optional), Response |
| Tool Input Accuracy (preview) | Validates that all tool call parameters are correct with strict criteria including grounding, type, format, completeness, and appropriateness. | Query, Response, Tool definitions |
| Tool Output Utilization (preview) | Measures whether the agent correctly interprets and uses tool outputs contextually in responses and subsequent calls. | Query, Response, Tool definitions (Optional) |
| Tool Call Success (preview) | Evaluates whether all tool calls executed successfully without technical failures. | Response, Tool definitions (Optional) |

To learn more, see [Agent evaluators](evaluation-evaluators/agent-evaluators?view=foundry-classic).

### Azure OpenAI graders

| Evaluator | Purpose | Inputs |
|---|---|---|
| Model Labeler | Classifies content using custom guidelines and labels. | Query, response, ground truth |
| String Checker | Performs flexible text validations and pattern matching. | Response |
| Text Similarity | Evaluates the quality of text or determine semantic closeness. | Response, ground truth |
| Model Scorer | Generates numerical scores (customized range) for content based on custom guidelines. | Query, response, ground truth |

To learn more, see [Azure OpenAI Graders](evaluation-evaluators/azure-openai-graders?view=foundry-classic).

### Evaluators in the development lifecycle

By using these evaluators strategically throughout the development lifecycle, teams can build more reliable, safe, and effective AI applications that meet user needs while minimizing potential risks.

## The three stages of GenAIOps evaluation

GenAIOps uses the following three stages.

### Base model selection

Before building your application, you need to select the right foundation. This initial evaluation helps you compare different models based on:

- Quality and accuracy: How relevant and coherent are the model's responses?
- Task performance: Does the model handle your specific use cases efficiently?
- Ethical considerations: Is the model free from harmful biases?
- Safety profile: What is the risk of generating unsafe content?

**Tools available**: [Microsoft Foundry benchmark](model-benchmarks?view=foundry-classic) for comparing models on public datasets or your own data, and the Azure AI Evaluation SDK for [testing specific model endpoints](https://github.com/Azure-Samples/azureai-samples/blob/main/scenarios/evaluate/Supported_Evaluation_Targets/Evaluate_Base_Model_Endpoint/Evaluate_Base_Model_Endpoint.ipynb).

### Preproduction evaluation

After you select a base model, the next step is to develop an AI agent or application. Before you deploy to a production environment, thorough testing is essential to ensure that the AI agent or application is ready for real-world use.

Preproduction evaluation involves:

- Testing with evaluation datasets: These datasets simulate realistic user interactions to ensure the AI agent performs as expected.
- Identifying edge cases: Finding scenarios where the AI agent's response quality might degrade or produce undesirable outputs.
- Assessing robustness: Ensuring that the AI agent can handle a range of input variations without significant drops in quality or safety.
- Measuring key metrics: Metrics such as task adherence, response groundedness, relevance, and safety are evaluated to confirm readiness for production.

The preproduction stage acts as a final quality check, reducing the risk of deploying an AI agent or application that doesn't meet the desired performance or safety standards.

Evaluation Tools and Approaches:

**Bring your own data**: You can evaluate your AI agents and applications in preproduction using your own evaluation data with supported evaluators, including quality, safety, or custom evaluators, and view results via the Foundry portal. Use Foundry's evaluation wizard or[Azure AI Evaluation SDK's](../how-to/develop/evaluate-sdk?view=foundry-classic)supported evaluators, including generation quality, safety, or[custom evaluators](evaluation-evaluators/custom-evaluators?view=foundry-classic).[View results by using the Foundry portal](../how-to/evaluate-results?view=foundry-classic).**Simulators and AI red teaming agent**: If you don't have evaluation data (test data),[Azure AI Evaluation SDK's simulators](../how-to/develop/simulator-interaction-data?view=foundry-classic)can help by generating topic-related or adversarial queries. These simulators test the model's response to situation-appropriate or attack-like queries (edge cases).[AI red teaming agent](../how-to/develop/run-scans-ai-red-teaming-agent?view=foundry-classic)simulates complex adversarial attacks against your AI system using a broad range of safety and security attacks using Microsoft's open framework for Python Risk Identification Tool or PyRIT.[Adversarial simulators](../how-to/develop/simulator-interaction-data?view=foundry-classic#generate-adversarial-simulations-for-safety-evaluation)injects static queries that mimic potential safety risks or security attacks such as attempted jailbreaks, helping identify limitations and preparing the model for unexpected conditions.[Context-appropriate simulators](../how-to/develop/simulator-interaction-data?view=foundry-classic#generate-synthetic-data-and-simulate-non-adversarial-tasks)generate typical, relevant conversations you'd expect from users to test quality of responses. With context-appropriate simulators you can assess metrics such as groundedness, relevance, coherence, and fluency of generated responses.

Automated scans using the AI red teaming agent enhance preproduction risk assessment by systematically testing AI applications for risks. This process involves simulated attack scenarios to identify weaknesses in model responses before real-world deployment. By running AI red teaming scans, you can detect and mitigate potential safety issues before deployment. This tool is recommended to be used with human-in-the-loop processes such as conventional AI red teaming probing to help accelerate risk identification and aid in the assessment by a human expert.


Alternatively, you can also use [the Foundry portal](../how-to/evaluate-generative-ai-app?view=foundry-classic) for testing your generative AI applications.

Bring your own data: You can evaluate your AI applications in preproduction using your own evaluation data with supported evaluators, including generation quality, safety, or custom evaluators, and view results via the Foundry portal. Use Foundry's evaluation wizard or

[Azure AI Evaluation SDK's](../how-to/develop/evaluate-sdk?view=foundry-classic)supported evaluators, including generation quality, safety, or[custom evaluators](evaluation-evaluators/custom-evaluators?view=foundry-classic), and[view results via the Foundry portal](../how-to/evaluate-results?view=foundry-classic).Simulators and AI red teaming agent: If you don't have evaluation data (test data), simulators can help by generating topic-related or adversarial queries. These simulators test the model's response to situation-appropriate or attack-like queries (edge cases).

[AI red teaming agent](../how-to/develop/run-scans-ai-red-teaming-agent?view=foundry-classic)simulates complex adversarial attacks against your AI system using a broad range of safety and security attacks using Microsoft's open framework for Python Risk Identification Tool or PyRIT.Automated scans using the AI red teaming agent enhances preproduction risk assessment by systematically testing AI applications for risks. This process involves simulated attack scenarios to identify weaknesses in model responses before real-world deployment. By running AI red teaming scans, you can detect and mitigate potential safety issues before deployment. This tool is recommended to be used with human-in-the-loop processes such as conventional AI red teaming probing to help accelerate risk identification and aid in the assessment by a human expert.


Alternatively, you can also use [the Foundry portal](../how-to/evaluate-generative-ai-app?view=foundry-classic) for testing your generative AI applications.

After you get satisfactory results, you can deploy the AI application to production.

### Post-production monitoring

After deployment, continuous monitoring ensures your AI application maintains quality in real-world conditions.

After deployment, [continuous monitoring](../agents/how-to/how-to-monitor-agents-dashboard?view=foundry-classic) ensures your AI application maintains quality in real-world conditions.

**Operational metrics**: Regular measurement of key AI agent operational metrics.**Continuous evaluation**: Enables quality and safety evaluation of production traffic at a sampled rate.**Scheduled evaluation**: Enables scheduled quality and safety evaluation using a test dataset to detect drift in the underlying systems.**Scheduled red teaming**: Provides scheduled adversarial testing capabilities to probe for safety and security vulnerabilities.**Azure Monitor alerts**: Swift action when harmful or inappropriate outputs occur. Set up alerts for continuous evaluation to be notified when evaluation results drop below the pass rate threshold in production.

Effective monitoring helps maintain user trust and allows for rapid issue resolution.

Observability provides comprehensive monitoring capabilities essential for today's complex and rapidly evolving AI landscape. Seamlessly integrated with Azure Monitor Application Insights, this solution enables continuous monitoring of deployed AI applications to ensure optimal performance, safety, and quality in production environments.

The Foundry Observability dashboard delivers real-time insights into critical metrics. It allows teams to quickly identify and address performance issues, safety concerns, or quality degradation.

For Agent-based applications, Foundry offers enhanced continuous evaluation capabilities. These capabilities can provide deeper visibility into quality and safety metrics. They can create a robust monitoring ecosystem that adapts to the dynamic nature of AI applications while maintaining high standards of performance and reliability.

By continuously monitoring the AI application's behavior in production, you can maintain high-quality user experiences and swiftly address any issues that surface.

## Building trust through systematic evaluation

GenAIOps establishes a reliable process for managing AI applications throughout their lifecycle. By implementing thorough evaluation at each stage—from model selection through deployment and beyond—teams can create AI solutions that aren't just powerful but trustworthy and safe.

### Evaluation cheat sheet

| Purpose | Process | Parameters, guidance, and samples |
|---|---|---|
| What are you evaluating for? | Identify or build relevant evaluators | -
-
-
-
|

[Generic simulator for measuring Quality and Performance](concept-synthetic-data?view=foundry-classic)([Generic simulator sample notebook](https://github.com/Azure/azureml-examples/blob/main/sdk/python/foundation-models/system/finetune/Llama-notebooks/datagen/synthetic-data-generation.ipynb))-

[Adversarial simulator for measuring Safety and Security](../how-to/develop/simulator-interaction-data?view=foundry-classic)([Adversarial simulator sample notebook](https://github.com/Azure-Samples/rag-data-openai-python-promptflow/blob/main/src/evaluation/simulate_and_evaluate_online_endpoint.ipynb))- AI red teaming agent for running automated scans to assess safety and security vulnerabilities (

[AI red teaming agent sample notebook](https://github.com/Azure-Samples/azureai-samples/blob/main/scenarios/evaluate/AI_RedTeaming/AI_RedTeaming.ipynb))[Agent evaluation runs](../how-to/develop/agent-evaluate-sdk?view=foundry-classic)-

[Remote cloud run](../how-to/develop/cloud-evaluation?view=foundry-classic)-

[Local run](../how-to/develop/evaluate-sdk?view=foundry-classic)[View aggregate scores, view details, score details, compare evaluation runs](../how-to/evaluate-results?view=foundry-classic)- If evaluation results aligned to human feedback but didn't meet quality/safety thresholds, apply targeted mitigations. Example of mitigations to apply:

[Azure AI Content Safety](../ai-services/content-safety-overview?view=foundry-classic)| Purpose | Process | Parameters, guidance, and samples |
|---|---|---|
| What are you evaluating for? | Identify or build relevant evaluators | -
-
-
-
|

[Synthetic dataset generation](../how-to/evaluate-generative-ai-app?view=foundry-classic#select-or-create-a-dataset)- AI red teaming agent for running automated scans to assess safety and security vulnerabilities (

[AI red teaming agent sample notebook](https://aka.ms/airedteamingagent-sample))[Agent evaluation runs](../how-to/develop/agent-evaluate-sdk?view=foundry-classic)-

[Remote cloud run](../how-to/develop/cloud-evaluation?view=foundry-classic)[View aggregate scores, view details, score details, compare evaluation runs](../how-to/evaluate-results?view=foundry-classic)- If evaluation results aligned to human feedback but didn't meet quality/safety thresholds, apply targeted mitigations. Example of mitigations to apply:

[Azure AI Content Safety](../ai-services/content-safety-overview?view=foundry-classic)## Bring your own virtual network for evaluation

For network isolation purposes you can bring your own virtual network for evaluation. To learn more, see [How to configure a private link](../how-to/configure-private-link?view=foundry-classic).

Note

Evaluation data is sent to Application Insights if Application Insights is connected. Virtual network support for Application Insights and tracing isn't available. Inline datasource is not supported.

Important

To prevent evaluation and red teaming run failures, assign the Azure AI User role to the project's Managed Identity during initial project setup.

### Virtual network region support

Bring your own virtual network for evaluation is supported in all regions except for Central India, East Asia, North Europe and Qatar Central.

## Region support

Currently certain AI-assisted evaluators are available only in the following regions:

| Region | Hate and unfairness, Sexual, Violent, Self-harm, Indirect attack, Code vulnerabilities, Ungrounded attributes | Groundedness Pro | Protected material |
|---|---|---|---|
| East US 2 | Supported | Supported | Supported |
| Sweden Central | Supported | Supported | N/A |
| US North Central | Supported | N/A | N/A |
| France Central | Supported | N/A | N/A |
| Switzerland West | Supported | N/A | N/A |

### Agent playground evaluation region support

| Region | Status |
|---|---|
| East US | Supported |
| East US 2 | Supported |
| West US | Supported |
| West US 2 | Supported |
| West US 3 | Supported |
| France Central | Supported |
| Norway East | Supported |
| Sweden Central | Supported |

## Pricing

Observability features such as Risk and Safety Evaluations and Continuous Evaluations are billed based on consumption as listed in [our Azure pricing page](https://azure.microsoft.com/pricing/details/ai-foundry/).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/evaluation-metrics-built-in -->

# Observability in generative AI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

In today's AI-driven world, Generative AI Operations (GenAIOps) is revolutionizing how organizations build and deploy intelligent systems. As companies increasingly use AI agents and applications to transform decision-making, enhance customer experiences, and fuel innovation, one element stands paramount: robust evaluation frameworks. Evaluation isn't just a checkpoint. It's the foundation of quality and trust in AI applications. Without rigorous assessment and monitoring, AI systems can produce content that's:

- Fabricated or ungrounded in reality
- Irrelevant or incoherent
- Harmful in perpetuating content risks and stereotypes
- Dangerous in spreading misinformation
- Vulnerable to security exploits

This is where observability becomes essential. These capabilities measure both the frequency and severity of risks in AI outputs, enabling teams to systematically address quality, safety, and security concerns throughout the entire AI development journey—from selecting the right model to monitoring production performance, quality, and safety.

Note

The Microsoft Foundry SDK for evaluation and Foundry portal are in public preview, but the APIs are generally available for model and dataset evaluation (agent evaluation remains in public preview). The Azure AI Evaluation SDK and evaluators marked (preview) in this article are currently in public preview everywhere.

Note

The Microsoft Foundry SDK for evaluation and Foundry portal are in public preview, but the APIs are generally available for model and dataset evaluation (agent evaluation remains in public preview). Evaluators marked (preview) in this article are currently in public preview everywhere.

## What is observability?

AI observability refers to the ability to monitor, understand, and troubleshoot AI systems throughout their lifecycle. It involves collecting and analyzing signals such as evaluation metrics, logs, traces, and model and agent outputs to gain visibility into performance, quality, safety, and operational health.

## What are evaluators?

Evaluators are specialized tools that measure the quality, safety, and reliability of AI responses. By implementing systematic evaluations throughout the AI development lifecycle, teams can identify and address potential issues before they impact users. The following supported evaluators provide comprehensive assessment capabilities across different AI application types and concerns:

### General purpose

| Evaluator | Purpose | Inputs |
|---|---|---|
| Coherence | Measures logical consistency and flow of responses. | Query, response |
| Fluency | Measures natural language quality and readability. | Response |
| QA | Measures comprehensively various quality aspects in question-answering. | Query, context, response, ground truth |

To learn more, see [General purpose evaluators](evaluation-evaluators/general-purpose-evaluators?view=foundry-classic).

### Textual similarity

| Evaluator | Purpose | Inputs |
|---|---|---|
| Similarity | AI-assisted textual similarity measurement. | Query, context, ground truth |
| F1 Score | Harmonic mean of precision and recall in token overlaps between response and ground truth. | Response, ground truth |
| BLEU | Bilingual Evaluation Understudy score for translation quality measures overlaps in n-grams between response and ground truth. | Response, ground truth |
| GLEU | Google-BLEU variant for sentence-level assessment measures overlaps in n-grams between response and ground truth. | Response, ground truth |
| ROUGE | Recall-Oriented Understudy for Gisting Evaluation measures overlaps in n-grams between response and ground truth. | Response, ground truth |
| METEOR | Metric for Evaluation of Translation with Explicit Ordering measures overlaps in n-grams between response and ground truth. | Response, ground truth |

To learn more, see [Textual similarity evaluators](evaluation-evaluators/textual-similarity-evaluators?view=foundry-classic)

### RAG (retrieval augmented generation)

| Evaluator | Purpose | Inputs |
|---|---|---|
| Retrieval | Measures how effectively the system retrieves relevant information. | Query, context |
| Document Retrieval | Measures accuracy in retrieval results given ground truth. | Ground truth, retrieved documents |
| Groundedness | Measures how consistent the response is with respect to the retrieved context. | Query (optional), context, response |
| Groundedness Pro (preview) | Measures whether the response is consistent with respect to the retrieved context. | Query, context, response |
| Relevance | Measures how relevant the response is with respect to the query. | Query, response |
| Response Completeness | Measures to what extent the response is complete (not missing critical information) with respect to the ground truth. | Response, ground truth |

To learn more, see [Retrieval-augmented Generation (RAG) evaluators](evaluation-evaluators/rag-evaluators?view=foundry-classic).

### Safety and security

| Evaluator | Purpose | Inputs |
|---|---|---|
| Hate and Unfairness | Identifies biased, discriminatory, or hateful content. | Query, response |
| Sexual | Identifies inappropriate sexual content. | Query, response |
| Violence | Detects violent content or incitement. | Query, response |
| Self-Harm | Detects content promoting or describing self-harm. | Query, response |
| Content Safety | Comprehensive assessment of various safety concerns. | Query, response |
| Protected Materials | Detects unauthorized use of copyrighted or protected content. | Query, response |
| Code Vulnerability | Identifies security issues in generated code. | Query, response |
| Ungrounded Attributes | Detects fabricated or hallucinated information inferred from user interactions. | Query, context, response |

To learn more, see [Risk and safety evaluators](evaluation-evaluators/risk-safety-evaluators?view=foundry-classic).

### Agents

| Evaluator | Purpose | Inputs |
|---|---|---|
| Intent Resolution (preview) | Measures how accurately the agent identifies and addresses user intentions. | Query, response |
| Task Adherence (preview) | Measures how well the agent follows through on identified tasks. | Query, response, tool definitions (optional) |
| Tool Call Accuracy (preview) | Measures how well the agent selects and calls the correct tools to. | Query, either response or tool calls, tool definitions |

| Evaluator | Purpose | Inputs |
|---|---|---|
| Task Adherence (preview) | Measures whether the agent follows through on identified tasks according to system instructions. | Query, Response, Tool definitions (Optional) |
| Task Completion (preview) | Measures whether the agent successfully completed the requested task end-to-end. | Query, Response, Tool definitions (Optional) |
| Intent Resolution (preview) | Measures how accurately the agent identifies and addresses user intentions. | Query, Response, Tool definitions (Optional) |
| Task Navigation Efficiency (preview) | Determines whether the agent's sequence of steps matches an optimal or expected path to measure efficiency. | Response, Ground truth |
| Tool Call Accuracy (preview) | Measures the overall quality of tool calls including selection, parameter correctness, and efficiency. | Query, Tool definitions, Tool calls (Optional), Response |
| Tool Selection (preview) | Measures whether the agent selected the most appropriate and efficient tools for a task. | Query, Tool definitions, Tool calls (Optional), Response |
| Tool Input Accuracy (preview) | Validates that all tool call parameters are correct with strict criteria including grounding, type, format, completeness, and appropriateness. | Query, Response, Tool definitions |
| Tool Output Utilization (preview) | Measures whether the agent correctly interprets and uses tool outputs contextually in responses and subsequent calls. | Query, Response, Tool definitions (Optional) |
| Tool Call Success (preview) | Evaluates whether all tool calls executed successfully without technical failures. | Response, Tool definitions (Optional) |

To learn more, see [Agent evaluators](evaluation-evaluators/agent-evaluators?view=foundry-classic).

### Azure OpenAI graders

| Evaluator | Purpose | Inputs |
|---|---|---|
| Model Labeler | Classifies content using custom guidelines and labels. | Query, response, ground truth |
| String Checker | Performs flexible text validations and pattern matching. | Response |
| Text Similarity | Evaluates the quality of text or determine semantic closeness. | Response, ground truth |
| Model Scorer | Generates numerical scores (customized range) for content based on custom guidelines. | Query, response, ground truth |

To learn more, see [Azure OpenAI Graders](evaluation-evaluators/azure-openai-graders?view=foundry-classic).

### Evaluators in the development lifecycle

By using these evaluators strategically throughout the development lifecycle, teams can build more reliable, safe, and effective AI applications that meet user needs while minimizing potential risks.

## The three stages of GenAIOps evaluation

GenAIOps uses the following three stages.

### Base model selection

Before building your application, you need to select the right foundation. This initial evaluation helps you compare different models based on:

- Quality and accuracy: How relevant and coherent are the model's responses?
- Task performance: Does the model handle your specific use cases efficiently?
- Ethical considerations: Is the model free from harmful biases?
- Safety profile: What is the risk of generating unsafe content?

**Tools available**: [Microsoft Foundry benchmark](model-benchmarks?view=foundry-classic) for comparing models on public datasets or your own data, and the Azure AI Evaluation SDK for [testing specific model endpoints](https://github.com/Azure-Samples/azureai-samples/blob/main/scenarios/evaluate/Supported_Evaluation_Targets/Evaluate_Base_Model_Endpoint/Evaluate_Base_Model_Endpoint.ipynb).

### Preproduction evaluation

After you select a base model, the next step is to develop an AI agent or application. Before you deploy to a production environment, thorough testing is essential to ensure that the AI agent or application is ready for real-world use.

Preproduction evaluation involves:

- Testing with evaluation datasets: These datasets simulate realistic user interactions to ensure the AI agent performs as expected.
- Identifying edge cases: Finding scenarios where the AI agent's response quality might degrade or produce undesirable outputs.
- Assessing robustness: Ensuring that the AI agent can handle a range of input variations without significant drops in quality or safety.
- Measuring key metrics: Metrics such as task adherence, response groundedness, relevance, and safety are evaluated to confirm readiness for production.

The preproduction stage acts as a final quality check, reducing the risk of deploying an AI agent or application that doesn't meet the desired performance or safety standards.

Evaluation Tools and Approaches:

**Bring your own data**: You can evaluate your AI agents and applications in preproduction using your own evaluation data with supported evaluators, including quality, safety, or custom evaluators, and view results via the Foundry portal. Use Foundry's evaluation wizard or[Azure AI Evaluation SDK's](../how-to/develop/evaluate-sdk?view=foundry-classic)supported evaluators, including generation quality, safety, or[custom evaluators](evaluation-evaluators/custom-evaluators?view=foundry-classic).[View results by using the Foundry portal](../how-to/evaluate-results?view=foundry-classic).**Simulators and AI red teaming agent**: If you don't have evaluation data (test data),[Azure AI Evaluation SDK's simulators](../how-to/develop/simulator-interaction-data?view=foundry-classic)can help by generating topic-related or adversarial queries. These simulators test the model's response to situation-appropriate or attack-like queries (edge cases).[AI red teaming agent](../how-to/develop/run-scans-ai-red-teaming-agent?view=foundry-classic)simulates complex adversarial attacks against your AI system using a broad range of safety and security attacks using Microsoft's open framework for Python Risk Identification Tool or PyRIT.[Adversarial simulators](../how-to/develop/simulator-interaction-data?view=foundry-classic#generate-adversarial-simulations-for-safety-evaluation)injects static queries that mimic potential safety risks or security attacks such as attempted jailbreaks, helping identify limitations and preparing the model for unexpected conditions.[Context-appropriate simulators](../how-to/develop/simulator-interaction-data?view=foundry-classic#generate-synthetic-data-and-simulate-non-adversarial-tasks)generate typical, relevant conversations you'd expect from users to test quality of responses. With context-appropriate simulators you can assess metrics such as groundedness, relevance, coherence, and fluency of generated responses.

Automated scans using the AI red teaming agent enhance preproduction risk assessment by systematically testing AI applications for risks. This process involves simulated attack scenarios to identify weaknesses in model responses before real-world deployment. By running AI red teaming scans, you can detect and mitigate potential safety issues before deployment. This tool is recommended to be used with human-in-the-loop processes such as conventional AI red teaming probing to help accelerate risk identification and aid in the assessment by a human expert.


Alternatively, you can also use [the Foundry portal](../how-to/evaluate-generative-ai-app?view=foundry-classic) for testing your generative AI applications.

Bring your own data: You can evaluate your AI applications in preproduction using your own evaluation data with supported evaluators, including generation quality, safety, or custom evaluators, and view results via the Foundry portal. Use Foundry's evaluation wizard or

[Azure AI Evaluation SDK's](../how-to/develop/evaluate-sdk?view=foundry-classic)supported evaluators, including generation quality, safety, or[custom evaluators](evaluation-evaluators/custom-evaluators?view=foundry-classic), and[view results via the Foundry portal](../how-to/evaluate-results?view=foundry-classic).Simulators and AI red teaming agent: If you don't have evaluation data (test data), simulators can help by generating topic-related or adversarial queries. These simulators test the model's response to situation-appropriate or attack-like queries (edge cases).

[AI red teaming agent](../how-to/develop/run-scans-ai-red-teaming-agent?view=foundry-classic)simulates complex adversarial attacks against your AI system using a broad range of safety and security attacks using Microsoft's open framework for Python Risk Identification Tool or PyRIT.Automated scans using the AI red teaming agent enhances preproduction risk assessment by systematically testing AI applications for risks. This process involves simulated attack scenarios to identify weaknesses in model responses before real-world deployment. By running AI red teaming scans, you can detect and mitigate potential safety issues before deployment. This tool is recommended to be used with human-in-the-loop processes such as conventional AI red teaming probing to help accelerate risk identification and aid in the assessment by a human expert.


Alternatively, you can also use [the Foundry portal](../how-to/evaluate-generative-ai-app?view=foundry-classic) for testing your generative AI applications.

After you get satisfactory results, you can deploy the AI application to production.

### Post-production monitoring

After deployment, continuous monitoring ensures your AI application maintains quality in real-world conditions.

After deployment, [continuous monitoring](../agents/how-to/how-to-monitor-agents-dashboard?view=foundry-classic) ensures your AI application maintains quality in real-world conditions.

**Operational metrics**: Regular measurement of key AI agent operational metrics.**Continuous evaluation**: Enables quality and safety evaluation of production traffic at a sampled rate.**Scheduled evaluation**: Enables scheduled quality and safety evaluation using a test dataset to detect drift in the underlying systems.**Scheduled red teaming**: Provides scheduled adversarial testing capabilities to probe for safety and security vulnerabilities.**Azure Monitor alerts**: Swift action when harmful or inappropriate outputs occur. Set up alerts for continuous evaluation to be notified when evaluation results drop below the pass rate threshold in production.

Effective monitoring helps maintain user trust and allows for rapid issue resolution.

Observability provides comprehensive monitoring capabilities essential for today's complex and rapidly evolving AI landscape. Seamlessly integrated with Azure Monitor Application Insights, this solution enables continuous monitoring of deployed AI applications to ensure optimal performance, safety, and quality in production environments.

The Foundry Observability dashboard delivers real-time insights into critical metrics. It allows teams to quickly identify and address performance issues, safety concerns, or quality degradation.

For Agent-based applications, Foundry offers enhanced continuous evaluation capabilities. These capabilities can provide deeper visibility into quality and safety metrics. They can create a robust monitoring ecosystem that adapts to the dynamic nature of AI applications while maintaining high standards of performance and reliability.

By continuously monitoring the AI application's behavior in production, you can maintain high-quality user experiences and swiftly address any issues that surface.

## Building trust through systematic evaluation

GenAIOps establishes a reliable process for managing AI applications throughout their lifecycle. By implementing thorough evaluation at each stage—from model selection through deployment and beyond—teams can create AI solutions that aren't just powerful but trustworthy and safe.

### Evaluation cheat sheet

| Purpose | Process | Parameters, guidance, and samples |
|---|---|---|
| What are you evaluating for? | Identify or build relevant evaluators | -
-
-
-
|

[Generic simulator for measuring Quality and Performance](concept-synthetic-data?view=foundry-classic)([Generic simulator sample notebook](https://github.com/Azure/azureml-examples/blob/main/sdk/python/foundation-models/system/finetune/Llama-notebooks/datagen/synthetic-data-generation.ipynb))-

[Adversarial simulator for measuring Safety and Security](../how-to/develop/simulator-interaction-data?view=foundry-classic)([Adversarial simulator sample notebook](https://github.com/Azure-Samples/rag-data-openai-python-promptflow/blob/main/src/evaluation/simulate_and_evaluate_online_endpoint.ipynb))- AI red teaming agent for running automated scans to assess safety and security vulnerabilities (

[AI red teaming agent sample notebook](https://github.com/Azure-Samples/azureai-samples/blob/main/scenarios/evaluate/AI_RedTeaming/AI_RedTeaming.ipynb))[Agent evaluation runs](../how-to/develop/agent-evaluate-sdk?view=foundry-classic)-

[Remote cloud run](../how-to/develop/cloud-evaluation?view=foundry-classic)-

[Local run](../how-to/develop/evaluate-sdk?view=foundry-classic)[View aggregate scores, view details, score details, compare evaluation runs](../how-to/evaluate-results?view=foundry-classic)- If evaluation results aligned to human feedback but didn't meet quality/safety thresholds, apply targeted mitigations. Example of mitigations to apply:

[Azure AI Content Safety](../ai-services/content-safety-overview?view=foundry-classic)| Purpose | Process | Parameters, guidance, and samples |
|---|---|---|
| What are you evaluating for? | Identify or build relevant evaluators | -
-
-
-
|

[Synthetic dataset generation](../how-to/evaluate-generative-ai-app?view=foundry-classic#select-or-create-a-dataset)- AI red teaming agent for running automated scans to assess safety and security vulnerabilities (

[AI red teaming agent sample notebook](https://aka.ms/airedteamingagent-sample))[Agent evaluation runs](../how-to/develop/agent-evaluate-sdk?view=foundry-classic)-

[Remote cloud run](../how-to/develop/cloud-evaluation?view=foundry-classic)[View aggregate scores, view details, score details, compare evaluation runs](../how-to/evaluate-results?view=foundry-classic)- If evaluation results aligned to human feedback but didn't meet quality/safety thresholds, apply targeted mitigations. Example of mitigations to apply:

[Azure AI Content Safety](../ai-services/content-safety-overview?view=foundry-classic)## Bring your own virtual network for evaluation

For network isolation purposes you can bring your own virtual network for evaluation. To learn more, see [How to configure a private link](../how-to/configure-private-link?view=foundry-classic).

Note

Evaluation data is sent to Application Insights if Application Insights is connected. Virtual network support for Application Insights and tracing isn't available. Inline datasource is not supported.

Important

To prevent evaluation and red teaming run failures, assign the Azure AI User role to the project's Managed Identity during initial project setup.

### Virtual network region support

Bring your own virtual network for evaluation is supported in all regions except for Central India, East Asia, North Europe and Qatar Central.

## Region support

Currently certain AI-assisted evaluators are available only in the following regions:

| Region | Hate and unfairness, Sexual, Violent, Self-harm, Indirect attack, Code vulnerabilities, Ungrounded attributes | Groundedness Pro | Protected material |
|---|---|---|---|
| East US 2 | Supported | Supported | Supported |
| Sweden Central | Supported | Supported | N/A |
| US North Central | Supported | N/A | N/A |
| France Central | Supported | N/A | N/A |
| Switzerland West | Supported | N/A | N/A |

### Agent playground evaluation region support

| Region | Status |
|---|---|
| East US | Supported |
| East US 2 | Supported |
| West US | Supported |
| West US 2 | Supported |
| West US 3 | Supported |
| France Central | Supported |
| Norway East | Supported |
| Sweden Central | Supported |

## Pricing

Observability features such as Risk and Safety Evaluations and Continuous Evaluations are billed based on consumption as listed in [our Azure pricing page](https://azure.microsoft.com/pricing/details/ai-foundry/).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/ai-foundry/concepts/concept-playgrounds -->

# Microsoft Foundry Playgrounds

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔄 [Switch to the Microsoft Foundry (new) documentation](?view=foundry&preserve-view=true) if you're using the new portal.

Note

This document refers to the [Microsoft Foundry (new)](../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

Important

Items marked (preview) in this article are currently in public preview. This preview is provided without a service-level agreement, and we don't recommend it for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

As you build with state-of-the-art models and create agents and apps with them, Microsoft Foundry playgrounds provide an on-demand, zero-setup environment designed for rapid prototyping, API exploration, and technical validation before you commit a single line of code to your production codebase.

## Highlights of the Foundry playgrounds experience

Some highlights of the Foundry playgrounds experience include:

**AgentOps support**for evaluations and tracing in the**Agents playground.****Open in VS Code**for Chat and Agents playground. This feature saves you time by automatically importing your endpoint and key from Foundry to VS Code for multilingual code samples.**Images playground 2.0**for models such as[gpt-image-1](https://ai.azure.com/explore/models/gpt-image-1/version/2025-04-15/registry/azure-openai/?cid=learnDocs),[Stable Diffusion 3.5 Large](https://ai.azure.com/explore/models/Stable-Diffusion-3.5-Large/version/1/registry/azureml-stabilityai/?cid=learnDocs), and[FLUX.1-Kontext-pro](https://ai.azure.com/resource/models/Flux.1-Kontext-pro/version/1/registry/azureml-blackforestlabs/?cid=learnDocs)models.**Video playground**for Azure OpenAI Sora-2.

**Audio playground**for models such as[gpt-4o-audio-preview](https://ai.azure.com/resource/models/gpt-4o-audio-preview/version/2024-12-17/registry/azure-openai/?cid=learnDocs),[gpt-4o-transcribe](https://ai.azure.com/explore/models/gpt-4o-transcribe/version/2025-03-20/registry/azure-openai/?cid=learnDocs), and[gpt-4o-mini-tts](https://ai.azure.com/explore/models/gpt-4o-mini-tts/version/2025-03-20/registry/azure-openai/?cid=learnDocs)models.

Tip

In the screenshot of the playground landing page, the left pane of the portal is customized to show the playgrounds tab. To learn more about seeing the other items in the left pane, see [Customize the left pane](../what-is-foundry?view=foundry-classic#customize-the-left-pane).

## Playgrounds as the prelude to production

Modern development involves working across multiple systems—APIs, services, SDKs, and data models—often before you're ready to fully commit to a framework, write tests, or spin up infrastructure. As the complexity of software ecosystems increases, the need for safe, lightweight environments to validate ideas becomes critical. The playgrounds are built to meet this need.

The Foundry playgrounds provide ready-to-use environments with all the necessary tools and features preinstalled, so you don't need to set up projects, manage dependencies, or solve compatibility issues. The playgrounds can *accelerate developer velocity* by validating API behavior, going quicker to code, reducing cost of experimentation and time to ship, accelerating integration, optimizing prompts, and more.

Playgrounds also *provide clarity quickly* when you have questions, by providing answers in seconds—rather than hours—and allowing you to test and validate ideas before you commit to building at scale. For example, the playgrounds are ideal for quickly answering questions like:

- What's the minimal prompt I need to get the output I want?
- Will this logic work before I write a full integration?
- How does latency or token usage change with different configurations?
- What model provides the best price-to-performance ratio before I evolve it into an agent?

## Open in VS Code capability

The **Chat playground** and **Agents playground** let you work in VS Code by using the **Open in VS Code** button. You can find this button through the Foundry extension in VS Code.

Available on the multilingual sample code samples, **Open in VS Code** automatically imports your code sample, API endpoint, and key to a VS Code workspace in an `/azure`

environment. This functionality makes it easy to work in the VS Code IDE from the Foundry portal.

To use the **Open in VS Code** functionality from the chat and agents playgrounds, follow these steps:

Select

**Try the Chat playground**to open it. Alternatively, you can follow these steps in the Agents playground by selecting**Let's go**on the Agents playground card.If you don't have a deployment already, select

**Create new deployment**and deploy a model such as`gpt-4o-mini`

.Make sure your deployment is selected in the Deployment box.

Select

**View code**to see the code sample.Select

**Open in VS Code**to open VS Code in a new tab of your browser window.You're redirected to the

`/azure`

environment of VS Code where your code sample, API endpoint, and key are already imported from the Foundry playground.Browse the

`INSTRUCTIONS.md`

file for instructions to run your model.View your code sample in the

`run_model.py`

file.View relevant dependencies in the

`requirements.txt`

file.

The **Model playground** and **Agents playground** let you work in VS Code by using the **Open in VS Code for the Web** button. You can find this button from the **Code** tab in the chat pane of the model playground.

Available on the multilingual sample code samples, **Open in VS Code for the Web** automatically imports your code sample, API endpoint, and key to a VS Code workspace in an `/azure`

environment. This functionality makes it easy to work in the VS Code IDE from the Foundry portal.

## Agents playground

The agents playground lets you explore, prototype, and test agents without running any code. From this page, you can quickly iterate and experiment with new ideas.

To get started with the agents playground, see the [Quickstart: Create a new agent](../../ai-services/agents/quickstart?view=foundry-classic).

To get started with the agents playground, see [Understanding the agent development lifecycle](../agents/concepts/development-lifecycle?view=foundry-classic).

## Chat playground

The chat playground is the place to test the latest reasoning models from models including Azure OpenAI, DeepSeek, and Meta. For all reasoning models, the chat playground provides a chain-of-thought summary drop-down that lets you see how the model thinks through its response before sharing the output.

To learn more about the chat playground, see the [Quickstart: Get answers in the chat playground](../quickstarts/get-started-playground?view=foundry-classic).

## Model playground

When you deploy a model in the [Microsoft Foundry](https://ai.azure.com/?cid=learnDocs) portal, you immediately land on its playground. The model playground is an interactive experience designed for developers to test and experiment with the latest models from providers like Azure Open AI, DeepSeek, xAI, and Meta. The playground gives you full control over model behavior, safety, and deployment so that you can tune system prompts, compare model outputs in real time, or integrate tools like web search and code execution.

The playground is designed for fast iteration and production readiness. It supports everything from prototyping to performance benchmarking. The playground prepares you to use your model in a production workflow, easily upgrade your model as an agent, and continue to prototype in the agent playground with additional tools, knowledge, and memory before deploying as an agentic web application.

### Benefits of using the model playground

**Full-stack experimentation and control**: Configure parameters (such as temperature, top_p, max_tokens), inject system prompts, and enable advanced tools like web search, file search, and code interpreter, all within a single environment. This setup allows you to precisely tune model behavior and rapidly iterate on prompt engineering, grounding, and RAG workflows, upgrading your model into an agent.**Built-in safety and governance**: Assign or create guardrails to protect against jailbreaks, indirect prompt injections, and unsafe outputs. This integrated safety layer ensures you can validate compliance and responsible AI behaviors in a controlled, testable sandbox, without needing to wire external moderation logic.**Comparative and deployable by design**: Compare up to three models in parallel with synced input/output to benchmark response quality. Export multilingual code samples, grab endpoints and keys, and open in VS Code for immediate integration, bridging experimentation to production in one streamlined developer workflow.

### Compare models

Compare mode enables developers to run controlled, parallel evaluations across up to three models simultaneously, using a synchronized input stream. Each model receives the exact same prompt context, system message, and parameter configuration, ensuring consistent test conditions for output benchmarking. Responses stream in real time, allowing developers to measure and visualize differences in latency, token throughput, and response fidelity side-by-side.

To use compare mode from the playground of a deployed model:

- Select
**Compare models**in the upper-right corner. - Select up to two more models from existing or new deployments. Chat windows for the selected models open up side-by-side in the playground with synced prompt bars and setup. You can switch off sync from the
**Setup**pane for each model, if needed. - Enter your prompt in any of the prompt bars and see the prompt simultaneously appear in the others.
- Submit the prompt to see the output from each model simultaneously and compare the quality of the responses.
- Switch to the
**Code**tab in the chat pane of each model to see multilingual code samples. - For your preferred model, select either
**Open in VS Code for the Web**from the code tab to continue development work or**Save as agent**to continue prototyping in the agent playground.

### Generate and interpret code

With code interpreter, you can extend model capabilities beyond text generation by enabling in-line code execution within the playground. When activated, supported models can write, run, and debug code directly in a secure, sandboxed environment. This environment is ideal for performing calculations, data transformations, plotting visualizations, or validating logic.

To use code interpreter from the playground of a deployed model:

Expand the

**Tools**section in the deployed model's playground.Tip

The

**Tools**section isn't visible in the playground if you use compare mode to run parallel evaluations on models. You first have to close the other models that you're using for comparison before you can see the detailed playground that includes tools and other options for your deployed model.Select

**Add**>**Code interpreter**, and attach your code files for the code interpreter.Use the playground to ask questions, interpret, or streamline your code. For example, "How should I make the attached code files more efficient?"


## Audio playground

The audio playground (preview) lets you use text-to-speech and transcription capabilities with the latest audio models from Azure OpenAI.

To try the text-to-speech capability, follow these steps:

Select

**Try the Audio playground**to open it.If you don't have a deployment already, select

**Create new deployment**and deploy a model such as`gpt-4o-mini-tts`

.Make sure your deployment is selected in the Deployment box.

Input a text prompt.

Adjust model parameters such as voice and response format.

Select

**Generate**to receive a speech output with playback controls that include play, rewind, forward, adjust speed, and volume.Download the audio file to your local computer.


To try the transcription capability, follow these steps:

If you don't have a deployment already, select

**Create new deployment**and deploy a model such as`gpt-4o-transcribe`

.Make sure your deployment is selected in the Deployment box.

(Optional) Include a phrase list as a text mechanism to guide your audio input.

Input an audio file, by either uploading one or recording the audio from the prompt bar.

Select

**Generate transcription**to send the audio input to the model and receive a transcribed output in both text and JSON formats.

## Language playground

The [Language playground](https://ai.azure.com/build/playground/language) provides a code-free environment for testing and validating Azure Language in Foundry Tools capabilities. Use it to experiment with natural language processing (NLP) features such as **key data extraction**, **information summarization**, **text classification**, and **custom model fine-tuning**.

The Language playground consists of four primary sections:

**Top banner**: Select from the available Language capabilities including language detection, entity recognition, sentiment analysis, PII detection, summarization, and conversational language understanding.**Left pane**: Configure service options such as API version, model version, and capability-specific parameters.**Center pane**: Enter or upload text for processing. Results display here after you execute the operation.**Right pane**: View detailed operation results including entity categories, confidence scores, offsets, and JSON-formatted responses.

To use the Language playground:

Select

**playgrounds**from the left pane.Select

**Try Azure Language Playground**.Choose a Language capability from the top banner, such as:

Select

**Configure**to specify API version, model version, and capability-specific options such as language selection, entity types to include, or redaction policies for PII.Enter text directly in the sample window, select a pre-loaded text sample from the drop-down menu, or upload your own text file using the paperclip icon.

Select the appropriate action button (for example,

**Detect**,**Extract**,**Analyze**, or**Summarize**) to process the text.Review the results that display in the center pane and examine detailed output information in the

**Details**section on the right pane, including confidence scores, entity categories, character offsets, and lengths.Select

**View code**to access multilingual code samples in Python, C#, JavaScript, and other languages for integration into your applications.

The Language playground accelerates development and enables rapid prototyping and validation of NLP capabilities before production implementation. It also supports training, deployment, testing, and fine-tuning of custom named entity recognition (NER) models with real-time debugging.

## Translator playground

The [Translator playground](https://ai.azure.com/build/playground/translator) provides a code-free environment for testing and validating Azure Translator capabilities. It supports both text translation and document translation workflows and enables developers to experiment with neural machine translation (NMT) and large language model (LLM)-based translation using GPT-4o and GPT-4o-mini.

To use the Translator playground:

Select

**Playgrounds**from the left pane.Select

**Try the Translator playground**.**For text translation:**Enter or paste the text you want to translate in the input field.

Select the source language or enable automatic language detection.

Select one or more target languages for translation output.

Choose the translation model: Azure-MT (neural machine translation), GPT-4o, or GPT-4o-mini. LLM models enable translation with specific gender or tone adjustments and can be refined using domain-specific terminology.

(Optional) Configure advanced options such as profanity handling, text type, or custom glossaries.

Select

**Translate**to generate the translation.Review the translated output and compare results across different model selections.


**For document translation:**Select the

**Document translation**option.Upload your source document or select a pre-loaded document sample.

Specify the target language for translation.

(Optional) Apply custom translation models or custom glossaries to maintain domain-specific terminology consistency.

Select

**Translate**to process the document. This preserves the original layout and formatting.Download the translated document to your local computer.


Select

**View code**to access REST API examples and SDK code samples in multiple programming languages for integrating Translator capabilities into your applications.

The Translator playground enables real-time validation of translation quality, prompt structures, and custom glossary effectiveness before production implementation. Use it to compare model outputs and optimize translation configurations for your specific use cases.

## Video playground

The video playground (preview) is your rapid iteration environment for exploring, refining, and validating generative video workflows. It's designed for developers who need to go from idea to prototype with precision, control, and speed. The playground gives you a low-friction interface to test prompt structures, assess motion fidelity, evaluate model consistency across frames, and compare outputs across models—without writing boilerplate or wasting compute cycles. It's also a great demo interface for your chief product officer and engineering VP.

All model endpoints are integrated with **Azure AI Content Safety**. As a result, the video playground filters out harmful and unsafe images before they appear. If content moderation policies flag your text prompt or video generation, you get a warning notification.

You can use the video playground with the **Azure OpenAI Sora-2** model.

Tip

See the DevBlog for [Sora and video playground in Foundry](https://devblogs.microsoft.com/foundry/sora-in-video-playground/).

Follow these steps to use the video playground:

Caution

Videos you generate are retained for 24 hours due to data privacy. Download videos to your local computer for longer retention.

Select

**Try the Video playground**to open it.If you don't have a deployment already, select

**Deploy now**from the top right side of the homepage and deploy the`sora-2`

model.On the homepage of the video playground, get inspired by

**pre-built prompts**sorted by the**industry**filter. From here, you can view the videos in full display and copy the prompt from the bottom right corner of a video to build from it.Copy the prompt to paste it in the prompt bar. Adjust key controls (for example, aspect ratio or resolution) to deeply understand specific model responsiveness and constraints.

Select

**Generate**to generate a video based on the copied prompt.Rewrite your text prompt syntax with gpt-4o by using

**Re-write with AI**.Switch on the

**Start with an industry system prompt**capability, choose an industry, and specify the change required for your original prompt.Select

**Update**to update the prompt, and then select**Generate**to create a new video.Go to the

**Generation history**tab to review your generations as a grid or list view. When you select the videos, you open them in full screen mode for full immersion. Visually observe outputs across prompt tweaks or parameter changes.In full screen mode, edit the prompt and submit it for regeneration.

Either in full screen mode or through the options button that shows up when you hover across the video, download the videos to your local computer, view the video generation information tag, view code, or delete the video.

Select

**View code**from the options menu to view contextual sample code for your video generations in several languages, including Python, JavaScript, C#, JSON, Curl, and Go.Port the code samples to production by copying them into VS Code.


Follow these steps to use the video playground:

Caution

Videos you generate are retained for 24 hours due to data privacy. Download videos to your local computer for longer retention.

- Select
**Build**from the upper-right navigation. - Select
**Models**from the left pane. - Select a video generation model, such as
**sora-2**from your list of deployed models. If you don't have a deployment already, select**Deploy base model**from the top right side of the page and deploy the`sora-2`

model. **Enter your text prompt**: Start with any text prompt for the video you want to generate. For models that enable image-to-video generation, upload an image attachment to the prompt bar and generate the video.**Explore the model API-specific generation controls**: Adjust key controls (for example, aspect ratio and duration) for a deeper understanding of specific model responsiveness and constraints.**Side-by-side observations in grid view**: Visually observe outputs across prompt tweaks or parameter changes.**Port to production with multi-lingual code samples**: Use multi-language code samples with**View Code**. Video playground is your launchpad to development work in VS Code.

### What to validate when experimenting in video playground

When you use the video playground to plan your production workload, explore and validate the following attributes:

**Prompt-to-Motion Translation**- Does the video model interpret your prompt in a way that makes logical and temporal sense?
- Is motion coherent with the described action or scene?

**Frame Consistency**- Do characters, objects, and styles remain consistent across frames?
- Are there visual artifacts, jitter, or unnatural transitions?

**Scene Control**- How well can you control scene composition, subject behavior, or camera angles?
- Can you guide scene transitions or background environments?

**Length and Timing**- How do different prompt structures affect video length and pacing?
- Does the video feel too fast, too slow, or too short?

**Multimodal Input Integration**- What happens when you provide a reference image, pose data, or audio input?
- Can you generate video with lip-sync to a given voiceover?

**Post-Processing Needs**- What level of raw fidelity can you expect before you need editing tools?
- Do you need to upscale, stabilize, or retouch the video before using it in production?

**Latency and Performance**- How long does it take to generate video for different prompt types or resolutions?
- What's the cost-performance tradeoff of generating 5-second versus 15-second clips?


## Images playground

The images playground is ideal for developers who build image generation flows. This playground is a full-featured, controlled environment for high-fidelity experiments designed for model-specific APIs to generate and edit images.

Tip

See the [60-second reel of the Images playground for gpt-image-1](https://youtu.be/btA8njJjLXY) and our DevBlog for [Images playground in Foundry.](https://devblogs.microsoft.com/foundry/images-playground-may-2025/)

You can use the images playground with these models:

[gpt-image-1](https://ai.azure.com/explore/models/gpt-image-1/version/2025-04-15/registry/azure-openai/?cid=learnDocs)and[dall-e-3](https://ai.azure.com/resource/models/dall-e-3/version/3.0/registry/azure-openai/?cid=learnDocs)from Azure OpenAI.[Stable Diffusion 3.5 Large](https://ai.azure.com/explore/models/Stable-Diffusion-3.5-Large/version/1/registry/azureml-stabilityai/?cid=learnDocs),[Stable Image Core](https://ai.azure.com/explore/models/Stable-Image-Core/version/1/registry/azureml-stabilityai/?cid=learnDocs),[Stable Image Ultra](https://ai.azure.com/explore/models/Stable-Image-Ultra/version/1/registry/azureml-stabilityai/?cid=learnDocs)from Stability AI.[FLUX.1-Kontext-pro](https://ai.azure.com/explore/models/FLUX.1-Kontext-pro/version/1/registry/azureml-blackforestlabs/?cid=learnDocs)and[FLUX-1.1-pro](https://ai.azure.com/explore/models/FLUX-1.1-pro/version/1/registry/azureml-blackforestlabs/?cid=learnDocs)from Black Forest Labs.

Follow these steps to use the images playground:

Select

**Try the Images playground**to open it.If you don't have a deployment already, select

**Create a deployment**and deploy a model such as`gpt-image-1`

.**Enter your text prompt**: Start with any text prompt for the image you want to generate. For models that enable image-to-image generation, upload an image attachment to the prompt bar.**Explore the model API-specific generation controls after model deployment:**Adjust key controls (for example, number of variations, quality, size, image format) to deeply understand specific model responsiveness and constraints.Select

**Generate**.**Side-by-side observations in grid view:**Visually observe outputs across prompt tweaks or parameter changes.**Transform with API tooling:**Inpainting with text transformation is available for gpt-image-1. Alter parts of your original image with inpainting selection. Use text prompts to specify the change.**Port to production with multi-lingual code samples:**Use Python, Java, JavaScript, C# code samples with**View Code**. Images playground is your launchpad to development work in VS Code.

You can use the images playground with these models:

[gpt-image-1](https://ai.azure.com/explore/models/gpt-image-1/version/2025-04-15/registry/azure-openai/?cid=learnDocs)and[dall-e-3](https://ai.azure.com/resource/models/dall-e-3/version/3.0/registry/azure-openai/?cid=learnDocs)from Azure OpenAI.[Stable Diffusion 3.5 Large](https://ai.azure.com/explore/models/Stable-Diffusion-3.5-Large/version/1/registry/azureml-stabilityai/?cid=learnDocs),[Stable Image Core](https://ai.azure.com/explore/models/Stable-Image-Core/version/1/registry/azureml-stabilityai/?cid=learnDocs),[Stable Image Ultra](https://ai.azure.com/explore/models/Stable-Image-Ultra/version/1/registry/azureml-stabilityai/?cid=learnDocs)from Stability AI.[FLUX.1-Kontext-pro](https://ai.azure.com/explore/models/FLUX.1-Kontext-pro/version/1/registry/azureml-blackforestlabs/?cid=learnDocs)and[FLUX-1.1-pro](https://ai.azure.com/explore/models/FLUX-1.1-pro/version/1/registry/azureml-blackforestlabs/?cid=learnDocs)from Black Forest Labs.

Follow these steps to use the images playground:

- Select
**Build**from the upper-right navigation. - Select
**Models**from the left pane. - Select an image generation model, such as
**gpt-image-1**from your list of deployed models. If you don't have a deployment already, select**Deploy base model**from the top right side of the page and deploy the`gpt-image-1`

model. **Enter your text prompt**: Start with any text prompt for the image you want to generate. For models that enable image-to-image generation, upload an image attachment to the prompt bar and generate the image.**Explore the model API-specific generation controls**: Adjust key controls (for example, number of variations and aspect ratio) for a deeper understanding of specific model responsiveness and constraints.**Side-by-side observations in grid view**: Visually observe outputs across prompt tweaks or parameter changes.**Transform with API tooling**: Inpainting with text transformation is available for gpt-image-1. Alter parts of your original image with inpainting selection. Use text prompts to specify the change.**Port to production with multi-lingual code samples**: Use multi-language code samples with**View Code**. Images playground is your launchpad to development work in VS Code.

### What to validate when experimenting in images playground

By using the images playground, you can explore and validate the following aspects as you plan your production workload:

**Prompt Effectiveness**- What kind of visual output does this prompt generate for my enterprise use case?
- How specific or abstract can my language be and still get good results?
- Does the model understand style references like "surrealist" or "cyberpunk" accurately?

**Stylistic Consistency**- How do I maintain the same character, style, or theme across multiple images?
- Can I iterate on variations of the same base prompt with minimal drift?

**Parameter Tuning**- What's the effect of changing model parameters like guidance scale, seed, steps, and others?
- How can I balance creativity versus prompt fidelity?

**Model Comparison**- How do results differ between models, such as SDXL versus DALL·E?
- Which model performs better for realistic faces versus artistic compositions?

**Composition Control**- What happens when I use spatial constraints like bounding boxes or inpainting masks?
- Can I guide the model toward specific layouts or focal points?

**Input Variation**- How do slight changes in prompt wording or structure impact results?
- What's the best way to prompt for symmetry, specific camera angles, or emotions?

**Integration Readiness**- Will this image meet the constraints of my product's UI, including aspect ratio, resolution, and content safety?
- Does the output conform to brand guidelines or customer expectations?
