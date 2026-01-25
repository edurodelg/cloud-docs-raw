---
merged_at: 2026-01-25T02:11:58.413672
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-get-started-terraform.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-get-started-terraform -->

# Quickstart: Deploy Azure AI Search service using Terraform

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows how to use Terraform to create an [Azure AI Search service](search-what-is-azure-search) using [Terraform](/en-us/azure/developer/terraform/quickstart-configure).

[Terraform](https://www.terraform.io) enables the definition, preview, and deployment of cloud infrastructure. Using Terraform, you create configuration files using [HCL syntax](https://developer.hashicorp.com/terraform/language/syntax/configuration). The HCL syntax allows you to specify the cloud provider - such as Azure - and the elements that make up your cloud infrastructure. After you create your configuration files, you create an *execution plan* that allows you to preview your infrastructure changes before they're deployed. Once you verify the changes, you apply the execution plan to deploy the infrastructure.

In this article, you learn how to:

- Create a random pet name for the Azure resource group name using
[random_pet](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/pet) - Create an Azure resource group using
[azurerm_resource_group](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/resource_group) - Create a random string using
[random_string](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/string) - Create an Azure AI Search service using
[azurerm_search_service](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/search_service)

## Prerequisites

## Implement the Terraform code

Create a directory in which to test and run the sample Terraform code and make it the current directory.

Create a file named

`main.tf`

and insert the following code:`resource "random_pet" "rg_name" { prefix = var.resource_group_name_prefix } resource "azurerm_resource_group" "rg" { name = random_pet.rg_name.id location = var.resource_group_location } resource "random_string" "azurerm_search_service_name" { length = 25 upper = false numeric = false special = false } resource "azurerm_search_service" "search" { name = random_string.azurerm_search_service_name.result resource_group_name = azurerm_resource_group.rg.name location = azurerm_resource_group.rg.location sku = var.sku replica_count = var.replica_count partition_count = var.partition_count }`

Create a file named

`outputs.tf`

and insert the following code:`output "resource_group_name" { value = azurerm_resource_group.rg.name } output "azurerm_search_service_name" { value = azurerm_search_service.search.name }`

Create a file named

`providers.tf`

and insert the following code:`terraform { required_version = ">=1.0" required_providers { azurerm = { source = "hashicorp/azurerm" version = "~>3.0" } random = { source = "hashicorp/random" version = "~>3.0" } } } provider "azurerm" { features {} }`

Create a file named

`variables.tf`

and insert the following code:`variable "resource_group_location" { type = string description = "Location for all resources." default = "eastus" } variable "resource_group_name_prefix" { type = string description = "Prefix of the resource group name that's combined with a random ID so name is unique in your Azure subscription." default = "rg" } variable "sku" { description = "The pricing tier of the search service you want to create (for example, basic or standard)." default = "standard" type = string validation { condition = contains(["free", "basic", "standard", "standard2", "standard3", "storage_optimized_l1", "storage_optimized_l2"], var.sku) error_message = "The sku must be one of the following values: free, basic, standard, standard2, standard3, storage_optimized_l1, storage_optimized_l2." } } variable "replica_count" { type = number description = "Replicas distribute search workloads across the service. You need at least two replicas to support high availability of query workloads (not applicable to the free tier)." default = 1 validation { condition = var.replica_count >= 1 && var.replica_count <= 12 error_message = "The replica_count must be between 1 and 12." } } variable "partition_count" { type = number description = "Partitions allow for scaling of document count as well as faster indexing by sharding your index over multiple search units." default = 1 validation { condition = contains([1, 2, 3, 4, 6, 12], var.partition_count) error_message = "The partition_count must be one of the following values: 1, 2, 3, 4, 6, 12." } }`


## Initialize Terraform

Run [terraform init](https://www.terraform.io/docs/commands/init.html) to initialize the Terraform deployment. This command downloads the Azure provider required to manage your Azure resources.

```
terraform init -upgrade
```


**Key points:**

- The
`-upgrade`

parameter upgrades the necessary provider plugins to the newest version that complies with the configuration's version constraints.

## Create a Terraform execution plan

Run [terraform plan](https://www.terraform.io/docs/commands/plan.html) to create an execution plan.

```
terraform plan -out main.tfplan
```


**Key points:**

- The
`terraform plan`

command creates an execution plan, but doesn't execute it. Instead, it determines what actions are necessary to create the configuration specified in your configuration files. This pattern allows you to verify whether the execution plan matches your expectations before making any changes to actual resources. - The optional
`-out`

parameter allows you to specify an output file for the plan. Using the`-out`

parameter ensures that the plan you reviewed is exactly what is applied.

## Apply a Terraform execution plan

Run [terraform apply](https://www.terraform.io/docs/commands/apply.html) to apply the execution plan to your cloud infrastructure.

```
terraform apply main.tfplan
```


**Key points:**

- The example
`terraform apply`

command assumes you previously ran`terraform plan -out main.tfplan`

. - If you specified a different filename for the
`-out`

parameter, use that same filename in the call to`terraform apply`

. - If you didn't use the
`-out`

parameter, call`terraform apply`

without any parameters.

## Verify the results

Get the Azure resource name in which the Azure AI Search service was created.

`resource_group_name=$(terraform output -raw resource_group_name)`

Get the Azure AI Search service name.

`azurerm_search_service_name=$(terraform output -raw azurerm_search_service_name)`

Run

[az search service show](/en-us/cli/azure/search/service#az-search-service-show)to show the Azure AI Search service you created in this article.`az search service show --name $azurerm_search_service_name \ --resource-group $resource_group_name`


## Clean up resources

When you no longer need the resources created via Terraform, do the following steps:

Run

[terraform plan](https://www.terraform.io/docs/commands/plan.html)and specify the`destroy`

flag.`terraform plan -destroy -out main.destroy.tfplan`

**Key points:**- The
`terraform plan`

command creates an execution plan, but doesn't execute it. Instead, it determines what actions are necessary to create the configuration specified in your configuration files. This pattern allows you to verify whether the execution plan matches your expectations before making any changes to actual resources. - The optional
`-out`

parameter allows you to specify an output file for the plan. Using the`-out`

parameter ensures that the plan you reviewed is exactly what is applied.

- The
Run

[terraform apply](https://www.terraform.io/docs/commands/apply.html)to apply the execution plan.`terraform apply main.destroy.tfplan`


## Troubleshoot Terraform on Azure

[Troubleshoot common problems when using Terraform on Azure](/en-us/azure/developer/terraform/troubleshoot)


---

<!-- DOCUMENTO FUSIONADO: cognitive-search-skill-azure-openai-embedding.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-azure-openai-embedding -->

# Azure OpenAI Embedding skill

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The **Azure OpenAI Embedding** skill connects to an embedding model deployed to your [Azure OpenAI in Foundry Models](/en-us/azure/ai-services/openai/overview) resource or [Microsoft Foundry](/en-us/azure/ai-foundry/what-is-foundry) project to generate embeddings during indexing. Your data is processed in the [Geo](https://azure.microsoft.com/explore/global-infrastructure/data-residency/) where your model is deployed.

The [ Import data (new) wizard](search-get-started-portal-import-vectors) in the Azure portal uses the Azure OpenAI Embedding skill to vectorize content. You can run the wizard and review the generated skillset to see how the wizard builds the skill for embedding models.

Note

This skill is bound to Azure OpenAI and is charged at the [Azure OpenAI Standard price](https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/#pricing).

## Prerequisites

An

[Azure OpenAI in Foundry Models resource](/en-us/azure/ai-foundry/openai/how-to/create-resource)or[Foundry project](/en-us/azure/ai-foundry/how-to/create-projects).Your Azure OpenAI resource must have a

[custom subdomain](/en-us/azure/ai-services/cognitive-services-custom-subdomains), such as`https://<resource-name>.openai.azure.com`

. You can find this endpoint on the**Keys and Endpoint**page in the Azure portal and use it for the`resourceUri`

property in this skill.The

[parent resource](/en-us/azure/ai-services/multi-service-resource)of your Foundry project provides access to multiple endpoints, including`https://<resource-name>.openai.azure.com`

,`https://<resource-name>.services.ai.azure.com`

, and`https://<resource-name>.cognitiveservices.azure.com`

. You can find these endpoints on the**Keys and Endpoint**page in the Azure portal and use any of them for the`resourceUri`

property in this skill.

An Azure OpenAI embedding model deployed to your resource or project. For supported models, see the

[Skill parameters](#skill-parameters)section.

## @odata.type

Microsoft.Skills.Text.AzureOpenAIEmbeddingSkill

## Data limits

The maximum size of a text input should be 8,000 tokens. If input exceeds the maximum allowed, the model throws an invalid request error. For more information, see the [tokens](/en-us/azure/ai-services/openai/overview#tokens) key concept in the Azure OpenAI documentation. Consider using the [Text Split skill](cognitive-search-skill-textsplit) if you need data chunking.

## Skill parameters

Parameters are case sensitive.

| Inputs | Description |
|---|---|
`resourceUri` |
(Required) The URI of the model provider. Supported domains are:
This field is required if your resource is deployed behind a private endpoint or uses virtual network (VNet) integration. |
`apiKey` |
The secret key used to access the model. If you provide a key, leave `authIdentity` empty. If you set both `apiKey` and `authIdentity` , the `apiKey` is used on the connection. |
`deploymentId` |
(Required) The ID of the deployed Azure OpenAI embedding model. This is the deployment name you specified when you deployed the model. |
`authIdentity` |
A user-managed identity used by the search service for the connection. You can use either a
`apiKey` and `authIdentity` blank. The system-managed identity is used automatically. A managed identity must have
|

`modelName`

`deploymentId`

. Supported values are:`text-embedding-ada-002`

`text-embedding-3-large`

`text-embedding-3-small`


`dimensions`

[supports a range of dimensions](#supported-dimensions-by-modelname). The default is the maximum dimensions for each model. For skillsets created with REST API versions prior to the 2023-10-01-preview, the dimensions are fixed at 1536. If you set the`dimensions`

property in this skill, set the `dimensions`

property on the [vector field definition](vector-search-how-to-create-index#add-a-vector-field-to-the-fields-collection)to the same value.## Supported dimensions by `modelName`


The supported dimensions for an Azure OpenAI Embedding skill depend on the `modelName`

that is configured.

`modelName` |
Minimum dimensions | Maximum dimensions |
|---|---|---|
| text-embedding-ada-002 | 1536 | 1536 |
| text-embedding-3-large | 1 | 3072 |
| text-embedding-3-small | 1 | 1536 |

## Skill inputs

| Input | Description |
|---|---|
`text` |
The input text to be vectorized. If you're using data chunking, the source might be `/document/pages/*` . |

## Skill outputs

| Output | Description |
|---|---|
`embedding` |
Vectorized embedding for the input text. |

## Sample definition

Consider a record that has the following fields:

```
{
"content": "Microsoft released Windows 10."
}
```


Then your skill definition might look like this:

```
{
"@odata.type": "#Microsoft.Skills.Text.AzureOpenAIEmbeddingSkill",
"description": "Connects a deployed embedding model.",
"resourceUri": "https://my-demo-openai-eastus.openai.azure.com/",
"deploymentId": "my-text-embedding-ada-002-model",
"modelName": "text-embedding-ada-002",
"dimensions": 1536,
"inputs": [
{
"name": "text",
"source": "/document/content"
}
],
"outputs": [
{
"name": "embedding"
}
]
}
```


## Sample output

For the given input text, a vectorized embedding output is produced.

```
{
"embedding": [
0.018990106880664825,
-0.0073809814639389515,
....
0.021276434883475304,
]
}
```


The output resides in memory. To send this output to a field in the search index, you must define an [outputFieldMapping](cognitive-search-output-field-mapping) that maps the vectorized embedding output (which is an array) to a [vector field](vector-search-how-to-create-index). Assuming the skill output resides in the document's **embedding** node, and **content_vector** is the field in the search index, the outputFieldMapping in indexer should look like:

```
"outputFieldMappings": [
{
"sourceFieldName": "/document/embedding/*",
"targetFieldName": "content_vector"
}
]
```


## Best practices

The following are some best practices you need to consider when utilizing this skill:

If you are hitting your Azure OpenAI TPM (Tokens per minute) limit, consider the

[quota limits advisory](/en-us/azure/ai-services/openai/quotas-limits)so you can address accordingly. Refer to the[Azure OpenAI monitoring](/en-us/azure/ai-services/openai/how-to/monitoring)documentation for more information about your Azure OpenAI instance performance.The Azure OpenAI embeddings model deployment you use for this skill should be ideally separate from the deployment used for other use cases, including the

[query vectorizer](vector-search-how-to-configure-vectorizer). This helps each deployment to be tailored to its specific use case, leading to optimized performance and identifying traffic from the indexer and the index embedding calls easily.Your Azure OpenAI instance should be in the same region or at least geographically close to the region where your AI Search service is hosted. This reduces latency and improves the speed of data transfer between the services.

If you have a larger than default Azure OpenAI TPM (Tokens per minute) limit as published in

[quotas and limits](/en-us/azure/ai-services/openai/quotas-limits)documentation, open a[support case](/en-us/azure/azure-portal/supportability/how-to-create-azure-support-request)with the Azure AI Search team, so this can be adjusted accordingly. This helps your indexing process not being unnecessarily slowed down by the documented default TPM limit, if you have higher limits.For examples and working code samples using this skill, see the following links:


## Errors and warnings

| Condition | Result |
|---|---|
| Null or invalid URI | Error |
| Null or invalid deploymentID | Error |
| Text is empty | Warning |
| Text is larger than 8,000 tokens | Error |
