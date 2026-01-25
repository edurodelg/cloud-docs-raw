---
merged_at: 2026-01-25T03:18:13.759197
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-get-started-bicep.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-get-started-bicep -->

# Quickstart: Deploy Azure AI Search using Bicep

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you use a Bicep file to deploy an Azure AI Search service in the Azure portal.

[Bicep](/en-us/azure/azure-resource-manager/bicep/overview) is a domain-specific language (DSL) that uses declarative syntax to deploy Azure resources. It provides concise syntax, reliable type safety, and support for code reuse. Bicep offers the best authoring experience for your infrastructure-as-code solutions in Azure.

Only those properties included in the template are used in the deployment. If more customization is required, such as [setting up network security](search-security-overview#network-security), you can update the service as a post-deployment task. To customize an existing service with the fewest steps, use [Azure CLI](search-manage-azure-cli) or [Azure PowerShell](search-manage-powershell). If you're evaluating preview features, use the [Management REST API](search-manage-rest).

Tip

For an alternative Bicep template that deploys Azure AI Search with a pre-configured indexer to Cosmos DB for NoSQL, see [Bicep deployment of Azure AI Search](https://github.com/Azure-Samples/azure-search-deployment-template). There's no bicep template support for Azure AI Search data plane operations like creating an index, but you can add a module that calls REST APIs. The sample includes a module that creates an index, data source connector, and an indexer that refreshes from Cosmos DB at 5-minute intervals.

## Prerequisites

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Review the Bicep file

The Bicep file used in this quickstart is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/azure-search-create/).

```
@description('Service name must only contain lowercase letters, digits or dashes, cannot use dash as the first two or last one characters, cannot contain consecutive dashes, and is limited between 2 and 60 characters in length.')
@minLength(2)
@maxLength(60)
param name string
@allowed([
'free'
'basic'
'standard'
'standard2'
'standard3'
'storage_optimized_l1'
'storage_optimized_l2'
])
@description('The pricing tier of the search service you want to create (for example, basic or standard).')
param sku string = 'standard'
@description('Replicas distribute search workloads across the service. You need at least two replicas to support high availability of query workloads (not applicable to the free tier).')
@minValue(1)
@maxValue(12)
param replicaCount int = 1
@description('Partitions allow for scaling of document count as well as faster indexing by sharding your index over multiple search units.')
@allowed([
1
2
3
4
6
12
])
param partitionCount int = 1
@description('Applicable only for SKUs set to standard3. You can set this property to enable a single, high density partition that allows up to 1000 indexes, which is much higher than the maximum indexes allowed for any other SKU.')
@allowed([
'default'
'highDensity'
])
param hostingMode string = 'default'
@description('Location for all resources.')
param location string = resourceGroup().location
resource search 'Microsoft.Search/searchServices@2020-08-01' = {
name: name
location: location
sku: {
name: sku
}
properties: {
replicaCount: replicaCount
partitionCount: partitionCount
hostingMode: hostingMode
}
}
```


The Azure resource defined in this Bicep file:

[Microsoft.Search/searchServices](/en-us/azure/templates/Microsoft.Search/searchServices): create an Azure AI Search service

## Deploy the Bicep file

Save the Bicep file as

**main.bicep**to your local computer.Deploy the Bicep file using either Azure CLI or Azure PowerShell.

`az group create --name exampleRG --location eastus az deployment group create --resource-group exampleRG --template-file main.bicep --parameters serviceName=<service-name>`

Note

Replace

**<service-name>**with the name of the Search service. The service name must only contain lowercase letters, digits, or dashes. You can't use a dash as the first two characters or the last character. The name has a minimum length of 2 characters and a maximum length of 60 characters.When the deployment finishes, you should see a message indicating the deployment succeeded.


## Review deployed resources

Use the Azure portal, Azure CLI, or Azure PowerShell to list the deployed resources in the resource group.

```
az resource list --resource-group exampleRG
```


## Clean up resources

Azure AI Search is a billable resource. If it's no longer needed, delete it from your subscription to avoid charges. You can use the Azure portal, Azure CLI, or Azure PowerShell to delete the resource group and its resources.

```
az group delete --name exampleRG
```


## Related content

In this quickstart, you created an Azure AI Search service using a Bicep file and then validated the deployment. To learn more about Azure AI Search and Azure Resource Manager, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: samples-python.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/samples-python -->

# Python samples for Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Learn about Python code samples that demonstrate the functionality and workflow of an Azure AI Search solution. These samples use the [Azure AI Search client library](/en-us/python/api/overview/azure/search-documents-readme) for the [Azure SDK for Python](/en-us/azure/developer/python/), which you can explore through the following links.

| Target | Link |
|---|---|
| Package download |
|

[azure-search-documents](/en-us/python/api/azure-search-documents)[github.com/Azure/azure-sdk-for-python/tree/main/sdk/search/azure-search-documents/tests](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/search/azure-search-documents/tests)[github.com/Azure/azure-sdk-for-python/tree/main/sdk/search/azure-search-documents](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/search/azure-search-documents)[github.com/Azure/azure-sdk-for-python/blob/main/sdk/search/azure-search-documents/CHANGELOG.md](https://github.com/Azure/azure-sdk-for-python/blob/main/sdk/search/azure-search-documents/CHANGELOG.md)## SDK samples

Code samples from the Azure SDK development team demonstrate API usage. You can find these samples in [Azure/azure-sdk-for-python/tree/main/sdk/search/azure-search-documents/samples](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/search/azure-search-documents/samples) on GitHub.

## Doc samples

Code samples from the Azure AI Search team demonstrate features and workflows. The following samples are referenced in tutorials, quickstarts, and how-to articles. You can find these samples in [Azure-Samples/azure-search-python-samples](https://github.com/Azure-Samples/azure-search-python-samples) on GitHub.

| Sample | Article | Description |
|---|---|---|
|

[Quickstart: Agentic retrieval](search-get-started-agentic-retrieval)[Quickstart-Keyword-Search](https://github.com/Azure-Samples/azure-search-python-samples/tree/main/Quickstart-Keyword-Search)[Quickstart: Full-text search](search-get-started-text)[Quickstart-Semantic-Ranking](https://github.com/Azure-Samples/azure-search-python-samples/tree/main/Quickstart-Semantic-Ranking)[Quickstart: Semantic ranking](search-get-started-semantic)[Quickstart-Vector-Search](https://github.com/Azure-Samples/azure-search-python-samples/tree/main/Quickstart-Vector-Search)[Quickstart: Vector search](search-get-started-vector)[agentic-retrieval-pipeline-example](https://github.com/Azure-Samples/azure-search-python-samples/tree/main/agentic-retrieval-pipeline-example)[Tutorial: Build an end-to-end agentic retrieval solution](agentic-retrieval-how-to-create-pipeline)[Quickstart-Agentic-Retrieval](https://github.com/Azure-Samples/azure-search-python-samples/tree/main/Quickstart-Agentic-Retrieval), this sample incorporates Foundry Agent Service for request orchestration.## Accelerators

An accelerator is an end-to-end solution that includes code and documentation you can adapt for your own implementation of a specific scenario.

| Sample | Description |
|---|---|
|

## Demos

A demo repo provides proof-of-concept source code for examples or scenarios shown in demonstrations. Unlike accelerators, demo solutions aren't designed for adaptation.

| Sample | Description |
|---|---|
|

[azure-search-openai-demo](https://github.com/Azure-Samples/azure-search-openai-demo/blob/main)[blog post](https://techcommunity.microsoft.com/blog/azure-ai-services-blog/revolutionize-your-enterprise-data-with-chatgpt-next-gen-apps-w-azure-openai-and/3762087).[aisearch-openai-rag-audio](https://github.com/Azure-Samples/aisearch-openai-rag-audio)[video](https://www.youtube.com/watch?v=vXJka8xZ9Ko).## Other samples

The following samples are also published by the Azure AI Search team but aren't referenced in documentation. Associated README files provide usage instructions.

| Sample | Description |
|---|---|
|

[Quickstart-Document-Permissions-Pull-API](https://github.com/Azure-Samples/azure-search-python-samples/tree/main/Quickstart-Document-Permissions-Pull-API)[Quickstart-Document-Permissions-Push-API](https://github.com/Azure-Samples/azure-search-python-samples/tree/main/Quickstart-Document-Permissions-Push-API)[azure-function-search](https://github.com/Azure-Samples/azure-search-python-samples/tree/main/azure-function-search)`api`

code used in [Add search to web sites with .NET](tutorial-csharp-overview).[bulk-insert](https://github.com/Azure-Samples/azure-search-python-samples/tree/main/bulk-insert)[Use the push APIs](search-how-to-load-search-index)to upload and index documents.[index-backup-and-restore.ipynb](https://github.com/Azure/azure-search-vector-samples/tree/main/demo-python/code/utilities/index-backup-restore)[resumable-index-backup-restore](https://github.com/Azure/azure-search-vector-samples/blob/main/demo-python/code/utilities/resumable-index-backup-restore/backup-and-restore.ipynb)Tip

Use the [samples browser](/en-us/samples/browse/?languages=python&products=azure-cognitive-search) to search for Microsoft code samples on GitHub. You can filter your search by product, service, and language.
