---
merged_at: 2026-01-25T03:18:13.760624
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: vector-search-vectorizer-azure-machine-learning-ai-studio-catalog.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/vector-search-vectorizer-azure-machine-learning-ai-studio-catalog -->

# Microsoft Foundry model catalog vectorizer

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

This vectorizer is in public preview under [Supplemental Terms of Use](https://azure.microsoft.com/support/legal/preview-supplemental-terms/). To use this feature, we recommend the latest preview version of [Indexes - Create Or Update (REST API)](/en-us/rest/api/searchservice/indexes/create-or-update).

The **Microsoft Foundry model catalog** vectorizer connects to an embedding model deployed from the [Foundry model catalog](/en-us/azure/ai-foundry/how-to/model-catalog-overview) or an [Azure Machine Learning](../machine-learning/overview-what-is-azure-machine-learning) (AML) endpoint. Your data is processed in the [Geo](https://azure.microsoft.com/explore/global-infrastructure/data-residency/) where your model is deployed.

If you're using integrated vectorization to create the vector arrays, the skillset should include an [AML skill](cognitive-search-aml-skill) that points to the same model specified in the vectorizer.

## Prerequisites

A

[Microsoft Foundry hub-based project](/en-us/azure/ai-foundry/how-to/hub-create-projects)or an[AML workspace](../machine-learning/concept-workspace)for a custom model that you create.For hub-based projects only, a serverless deployment of a

[supported model](#vectorizer-parameters)from the Microsoft Foundry model catalog. You can use an[ARM/Bicep template](https://github.com/Azure-Samples/azure-ai-search-multimodal-sample/blob/42b4d07f2dd9f7720fdc0b0788bf107bdac5eecb/infra/ai/modules/project.bicep#L37C1-L38C1)to provision the serverless deployment.

## Vectorizer parameters

Parameters are case sensitive. The parameters you use depend on what [authentication your model provider requires](#WhatParametersToUse), if any.

| Parameter name | Description |
|---|---|
`uri` |
(Required for
|

`key`

[key authentication](#WhatParametersToUse)) The API key of the model provider.`resourceId`

[token authentication](#WhatParametersToUse)) The Azure Resource Manager resource ID of the model provider. For an AML online endpoint, use the`subscriptions/{guid}/resourceGroups/{resource-group-name}/Microsoft.MachineLearningServices/workspaces/{workspace-name}/onlineendpoints/{endpoint_name}`

format.`modelName`

`uri`

. Supported models (serverless deployments only) are:- Cohere-embed-v3-english
- Cohere-embed-v3-multilingual
- Cohere-embed-v4

`region`

[token authentication](#WhatParametersToUse)) The region in which the model provider is deployed. Required if the region is different from the region of the search service.`timeout`

[ISO 8601 duration](https://www.w3.org/TR/xmlschema11-2/#dayTimeDuration)value). For example,`PT60S`

for 60 seconds. If not set, a default value of 30 seconds is chosen. The timeout can be set to a maximum of 230 seconds and a minimum of 1 second.## What authentication parameters to use

The Microsoft Foundry model catalog vectorizer provides two authentication options:

**Key-based authentication**. You provide a static key to authenticate scoring requests from the vectorizer. Set the`uri`

and`key`

parameters for this connection.**Token-based authentication**. The Foundry hub-based project or AML online endpoint is deployed using token-based authentication. The Azure AI Search service must have a[managed identity](/en-us/azure/active-directory/managed-identities-azure-resources/overview)and a role assignment on the model provider. The vectorizer then uses the search service identity to authenticate against the model provider, with no static keys required. The search service identity must have the**Owner**or**Contributor**role. Set the`resourceId`

parameter, and if the search service is in a different region from the model provider, set the`region`

parameter.

## Supported vector query types

Which vector query types are supported by the Microsoft Foundry model catalog vectorizer depends on the `modelName`

that is configured.

| Embedding model | Supports `text` query |
Supports `imageUrl` query |
Supports `imageBinary` query |
|---|---|---|---|
| Cohere-embed-v3-english | X | X | |
| Cohere-embed-v3-multilingual | X | X | |
| Cohere-embed-v4 | X | X |

## Expected field dimensions

The expected field dimensions for a vector field configured with a Microsoft Foundry model catalog vectorizer depend on the `modelName`

that is configured.

`modelName` |
Expected dimensions |
|---|---|
| Cohere-embed-v3-english | 1024 |
| Cohere-embed-v3-multilingual | 1024 |
| Cohere-embed-v4 | 256–1536 |

## Sample definition

Suggested model names in the Foundry model catalog consist of the base model plus a random three-letter suffix. The name of your model will be different from the one shown in this example.

```
"vectorizers": [
{
"name": "my-model-catalog-vectorizer",
"kind": "aml",
"amlParameters": {
"uri": "https://Cohere-embed-v3-multilingual-hin.eastus.models.ai.azure.com",
"key": "aaaaaaaa-0b0b-1c1c-2d2d-333333333333",
"timeout": "PT60S",
"modelName": "Cohere-embed-v3-multilingual-hin",
"resourceId": null,
"region": null,
},
}
]
```


---

<!-- DOCUMENTO FUSIONADO: search-how-to-alias.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-how-to-alias -->

# Create an index alias in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Index aliases are currently in public preview and available under [supplemental terms of use](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

In Azure AI Search, an index alias is a secondary name for a search index. You can create an alias that maps to a search index and substitute the alias name in places where you would otherwise reference an index name. This gives you flexibility if you ever need to change which index your application is pointing to. Instead of updating the references to the index name in your production code, you can just update the mapping for your alias.

You can create and manage aliases in Azure AI Search service via HTTP requests (POST, GET, PUT, DELETE) against a given alias resource. Aliases are service level resources and maintained independently from search indexes. Once a search index is created, you can create an alias that maps to that search index.

Before using an alias, your application sends requests directly to `hotel-samples-index`

.

```
POST /indexes/hotel-samples-index/docs/search?api-version=2025-11-01-preview
{
"search": "pool spa +airport",
"select": "HotelId, HotelName, Category, Description",
"count": true
}
```


After using an alias, your application sends requests to `my-alias`

, which maps to `hotel-samples-index`

.

```
POST /indexes/my-alias/docs/search?api-version=2025-11-01-preview
{
"search": "pool spa +airport",
"select": "HotelId, HotelName, Category, Description",
"count": true
}
```


## Supported scenarios

You can only use an alias with document operations or to get and update an index definition.

Aliases can't be used to [delete an index](/en-us/rest/api/searchservice/indexes/delete), or [test text tokenization](/en-us/rest/api/searchservice/indexes/analyze), or be referenced as the `targetIndexName`

on an [indexer](/en-us/rest/api/searchservice/indexers/create-or-update) or [knowledge source](agentic-knowledge-source-how-to-search-index).

## Create an index alias

Creating an alias establishes a mapping between an alias name and an index name. If the request is successful, the alias can be used for indexing, querying, and other operations.

Updating an alias allows you to map that alias to a different search index. When you update an existing alias, the entire definition is replaced with the contents of the request body. In general, the best pattern to use for updates is to retrieve the alias definition with a GET, modify it, and then update it with PUT.

You can create an alias using the preview REST API, the preview SDKs, or through the [Azure portal](https://portal.azure.com). An alias consists of the `name`

of the alias and the name of the search index that the alias is mapped to. Only one index name can be specified in the `indexes`

array.

The maximum number of aliases that you can create varies by pricing tier. For more information, see [Service limits](search-limits-quotas-capacity).

You can use the [Create or Update Alias (REST preview)](/en-us/rest/api/searchservice/aliases/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true) to create an index alias.

```
POST /aliases?api-version=2025-11-01-preview
{
"name": "my-alias",
"indexes": ["hotel-samples-index"]
}
```


## Send requests to an index alias

Aliases can be used for all document operations including querying, indexing, suggestions, and autocomplete.

This query sends the request to `my-alias`

, which is mapped to an actual index on your search service.

```
POST /indexes/my-alias/docs/search?api-version=2025-11-01-preview
{
"search": "pool spa +airport",
"searchMode": any,
"queryType": "simple",
"select": "HotelId, HotelName, Category, Description",
"count": true
}
```


## Get an alias definition

This request returns a list of existing alias objects by name.

```
GET https://[service name].search.windows.net/aliases?api-version=[api-version]&$select=name
api-key: [admin key]
```


This request returns an alias definition

```
GET https://[service name].search.windows.net/aliases/my-alias?api-version=[api-version]
api-key: [admin key]
```


## Update an alias

The most common update to an alias is changing the index name when the underlying index is replaced with a newer version.

PUT is required for alias updates as described in [Create or Update Alias (REST preview)](/en-us/rest/api/searchservice/aliases/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true).

```
PUT /aliases/my-alias?api-version=2025-11-01-preview
{
"name": "my-alias",
"indexes": ["hotel-samples-index2"]
}
```


An update to an alias may take up to 10 seconds to propagate through the system so you should wait at least 10 seconds before deleting the index that the alias was previously mapped to.

If you attempt to delete an index that is currently mapped to an alias, the operation will fail with 400 (Bad Request) and an error message stating that the alias(es) that's mapped to that index must be deleted or mapped to a different index before the index can be deleted.
