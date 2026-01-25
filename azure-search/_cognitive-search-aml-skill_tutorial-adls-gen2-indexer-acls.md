---
merged_at: 2026-01-25T02:11:58.427109
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: cognitive-search-aml-skill.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-aml-skill -->

# AML skill

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Support for indexer connections to the model catalog is in public preview under [supplemental terms of use](https://azure.microsoft.com/support/legal/preview-supplemental-terms/). Preview REST APIs support this capability.

Use the **AML** skill to extend AI enrichment with a deployed base embedding model from the [Microsoft Foundry model catalog](vector-search-integrated-vectorization-ai-studio) or a custom [Azure Machine Learning](../machine-learning/overview-what-is-azure-machine-learning) (AML) model. Your data is processed in the [Geo](https://azure.microsoft.com/explore/global-infrastructure/data-residency/) where your model is deployed.

You specify the AML skill in a skillset, which then integrates your deployed model into an AI enrichment pipeline. The AML skill is useful for performing processing or inference not supported by built-in skills. Examples include generating embeddings with your own model and applying custom machine learning logic to enriched content.

For AML online endpoints, use a stable API version or an equivalent Azure SDK to call the AML skill. For connections to the model catalog, use a preview API version.

## AML skill usage

Like other skills, the AML skill has inputs and outputs. The inputs are sent as a JSON object to a serverless deployment from the Foundry model catalog or an AML online endpoint. The output should include a success status code, JSON payload, and the parameters specified by your AML skill definition. Any other response is considered an error, and no enrichments are performed.

The indexer retries two times for the following HTTP status codes:

`503 Service Unavailable`

`429 Too Many Requests`


## AML skill for models in Foundry

Azure AI Search provides the [Microsoft Foundry model catalog vectorizer](vector-search-vectorizer-azure-machine-learning-ai-studio-catalog), which is also available in the [ Import data (new) wizard](search-import-data-portal#skills), for query-time connections to the model catalog. If you want to use this vectorizer for queries, the AML skill is the

*indexing counterpart*for generating embeddings using a model from the model catalog.

During indexing, the AML skill can connect to the model catalog to generate vectors for the index. At query time, queries can use a vectorizer to connect to the same model to vectorize text strings. You should use the AML skill and the Microsoft Foundry model catalog vectorizer together so that the same embedding model is used for indexing and queries. For more information, see [Use embedding models from the Foundry model catalog](vector-search-integrated-vectorization-ai-studio).

We recommend using the [ Import data (new) wizard](search-get-started-portal-import-vectors) to generate a skillset that includes an AML skill for deployed embedding models in Foundry. The wizard generates the AML skill definition for inputs, outputs, and mappings, providing an easy way to test a model before writing any code.

## Prerequisites

A

[Microsoft Foundry hub-based project](/en-us/azure/ai-foundry/how-to/hub-create-projects)or an[AML workspace](../machine-learning/concept-workspace)for a custom model that you create.For hub-based projects only, a serverless deployment of a

[supported model](#skill-parameters)from the Microsoft Foundry model catalog. You can use an[ARM/Bicep template](https://github.com/Azure-Samples/azure-ai-search-multimodal-sample/blob/42b4d07f2dd9f7720fdc0b0788bf107bdac5eecb/infra/ai/modules/project.bicep#L37C1-L38C1)to provision the serverless deployment.

## @odata.type

Microsoft.Skills.Custom.AmlSkill

## Skill parameters

Parameters are case sensitive. The parameters you use depend on what [authentication your model provider requires](#WhatSkillParametersToUse), if any.

| Parameter name | Description |
|---|---|
`uri` |
(Required for
|

`key`

[key authentication](#WhatSkillParametersToUse)) The API key of the model provider.`resourceId`

[token authentication](#WhatSkillParametersToUse)) The Azure Resource Manager resource ID of the model provider. For an AML online endpoint, use the`subscriptions/{guid}/resourceGroups/{resource-group-name}/Microsoft.MachineLearningServices/workspaces/{workspace-name}/onlineendpoints/{endpoint_name}`

format.`region`

[token authentication](#WhatSkillParametersToUse)) The region in which the model provider is deployed. Required if the region is different from the region of the search service.`timeout`

[ISO 8601 duration](https://www.w3.org/TR/xmlschema11-2/#dayTimeDuration)value. For example,`PT60S`

for 60 seconds. If not set, a default value of 30 seconds is chosen. You can set the timeout to a minimum of 1 second and a maximum of 230 seconds.`degreeOfParallelism`

`degreeOfParallelism`

to a minimum of 1 and a maximum of 10.## Authentication

The AML skill provides two authentication options:

**Key-based authentication**. You provide a static key to authenticate scoring requests from the AML skill. Set the`uri`

and`key`

parameters for this connection.**Token-based authentication**. The Foundry hub-based project or AML online endpoint is deployed using token-based authentication. The Azure AI Search service must have a[managed identity](/en-us/azure/active-directory/managed-identities-azure-resources/overview)and a role assignment on the model provider. The AML skill then uses the search service identity to authenticate against the model provider, with no static keys required. The search service identity must have the**Owner**or**Contributor**role. Set the`resourceId`

parameter, and if the search service is in a different region from the model provider, set the`region`

parameter.

## Skill inputs

Skill inputs are a node of the [enriched document](cognitive-search-working-with-skillsets#enrichment-tree) created during *document cracking*. For example, it might be the root document, a normalized image, or the content of a blob. There are no predefined inputs for this skill. For inputs, you should specify one or more nodes that are populated at the time of the AML skill's execution.

## Skill outputs

Skill outputs are new nodes of an enriched document created by the skill. There are no predefined outputs for this skill. For outputs, you should provide nodes that can be populated from the JSON response of your AML skill.

## Sample definition

```
{
"@odata.type": "#Microsoft.Skills.Custom.AmlSkill",
"description": "A custom model that detects the language in a document.",
"uri": "https://language-model.models.contoso.com/score",
"context": "/document",
"inputs": [
{
"name": "text",
"source": "/document/content"
}
],
"outputs": [
{
"name": "detected_language_code"
}
]
}
```


## Sample input JSON structure

This JSON structure represents the payload sent to your Foundry hub-based project or AML online endpoint. The top-level fields of the structure correspond to the "names" specified in the `inputs`

section of the skill definition. The values of those fields are from the "sources" of those fields, which could be from a field in the document or another skill.

```
{
"text": "Este es un contrato en Inglés"
}
```


## Sample output JSON structure

The output corresponds to the response from your Foundry hub-based project or AML online endpoint. The model provider should only return a JSON payload (verified by looking at the `Content-Type`

response header) and should be an object whose fields are enrichments matching the "names" in the `output`

and whose value is considered the enrichment.

```
{
"detected_language_code": "es"
}
```


## Inline shaping sample definition

```
{
"@odata.type": "#Microsoft.Skills.Custom.AmlSkill",
"description": "A sample model that detects the language of sentence",
"uri": "https://language-model.models.contoso.com/score",
"context": "/document",
"inputs": [
{
"name": "shapedText",
"sourceContext": "/document",
"inputs": [
{
"name": "content",
"source": "/document/content"
}
]
}
],
"outputs": [
{
"name": "detected_language_code"
}
]
}
```


## Inline shaping input JSON structure

```
{
"shapedText": { "content": "Este es un contrato en Inglés" }
}
```


## Inline shaping sample output JSON structure

```
{
"detected_language_code": "es"
}
```


## Error cases

In addition to your Foundry hub-based project or AML online endpoint being unavailable or sending nonsuccessful status codes, the following cases are considered errors:

The model provider returns a success status code, but the response indicates that it isn't

`application/json`

. The response is thus invalid, and no enrichments are performed.The model provider returns invalid JSON.


If the model provider is unavailable or returns an HTTP error, a friendly error with any available details about the HTTP error is added to the indexer execution history.


---

<!-- DOCUMENTO FUSIONADO: tutorial-adls-gen2-indexer-acls.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/tutorial-adls-gen2-indexer-acls -->

# Tutorial: Index permission metadata from ADLS Gen2 and query with permission-filtered results

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This tutorial demonstrates how to index Azure Data Lake Storage (ADLS) Gen2 [Access Control Lists (ACLs)](/en-us/azure/storage/blobs/data-lake-storage-access-control-model#access-control-lists-acls) and [role-based access control (RBAC)](/en-us/azure/storage/blobs/data-lake-storage-access-control-model#role-based-access-control-azure-rbac) scope into a search index using an indexer.

It also shows you how to structure a query that respects user access permissions. A successful query outcome confirms the permission transfer that occurred during index.

For more information about indexing ACLs, see [Use an ADLS Gen2 indexer to ingest permission metadata](search-indexer-access-control-lists-and-role-based-access).

In this tutorial, you learn how to:

- Configure RBAC scope and ACLs on an
`adlsgen2`

data source - Create an Azure AI Search index containing permission information fields
- Create and run an indexer to ingest permission information into an index from a data source
- Search the index you just created

Use a REST client to complete this tutorial and the [latest preview REST API](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2025-11-01-preview&preserve-view=true). Currently, there's no support for ACL indexing in the Azure portal.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).Microsoft Entra ID authentication and authorization. Services and apps must be in the same tenant. Role assignments are used for each authenticated connection. Users and groups must be in the same tenant. You should have user and groups to work with. Creating tenants and security principals is out-of-scope for this tutorial.

[ADLS Gen2](/en-us/azure/storage/blobs/create-data-lake-storage-account)with a hierarchical namespace.Files in a hierarchical folder structure. This tutorial assumes the ADLS Gen2 demo of folder structure for file

. This tutorial guides you through ACL assignment on folders and files so that you can complete the exercise successfully.`/Oregon/Portland/Data.txt`

[Azure AI Search](search-create-service-portal), any region. Basic tier or higher is required for managed identity support.[Visual Studio Code](https://code.visualstudio.com/download)with a[REST client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)or a[Python client](https://code.visualstudio.com/docs/languages/python)and[Jupyter package](https://pypi.org/project/jupyter/).

## Prepare sample data

Upload the [state parks sample data](https://github.com/Azure-Samples/azure-search-sample-data) to a container in ADLS Gen2. The container name should be "parks" and it should have two folders: "Oregon" and "Washington".

## Check search service configuration

You search service must be configured for Microsoft Entra ID authentication and authorization. Review this checklist to make sure you're prepared.

## Get a personal identity token for local testing

This tutorial assumes a REST client on a local system, connecting to Azure over a public internet connection.

[Follow these steps](search-get-started-rbac) to acquire a personal identity token and set up Visual Studio Code for local connections to your Azure resources.

## Set permissions in ADLS Gen2

As a best practice, use [ Group sets](search-indexer-access-control-lists-and-role-based-access#recommendations-and-best-practices) rather than directly assigning

`User`

sets.Grant the search service identity read access to the container. The indexer connects to Azure Storage under the search service identity. The search service must have

**Storage Blob Data Reader**permissions to retrieve data.Grant per-group or user permissions in the file hierarchy. In the file hierarchy, identify all

`Group`

and`User`

sets that are assigned to containers, directories, and files.You can use the Azure portal to manage ACLs. In Storage Browser, select the Oregon directory and then select

**Manage ACL**from the context menu.Add new security principals for users and groups.

Remove existing principals for owning groups, owning users, and other. These principals aren't supported for ACL indexing during the public preview.


## Create a search index for permission metadata

[Create an index](search-how-to-create-search-index#create-an-index) that contains fields for content and [permission metadata](search-indexer-access-control-lists-and-role-based-access#create-permission-fields-in-the-index).

Be sure to use the [latest preview REST API](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2025-11-01-preview&preserve-view=true) or a preview Azure SDK package that provides equivalent functionality. The permission filter properties are only available in the preview APIs.

For demo purposes, the permission field has `retrievable`

enabled so that you can check the values from the index. In a production environment, you should disable `retrievable`

to avoid leaking sensitive information.

```
{
"name" : "my-adlsgen2-acl-index",
"fields": [
{
"name": "name", "type": "Edm.String",
"searchable": true, "filterable": false, "retrievable": true
},
{
"name": "description", "type": "Edm.String",
"searchable": true, "filterable": false, "retrievable": true
},
{
"name": "location", "type": "Edm.String",
"searchable": true, "filterable": false, "retrievable": true
},
{
"name": "state", "type": "Edm.String",
"searchable": true, "filterable": false, "retrievable": true
},
{
"name": "AzureSearch_DocumentKey", "type": "Edm.String",
"searchable": true, "filterable": false, "retrievable": true
"stored": true,
"key": true
},
{
"name": "UserIds", "type": "Collection(Edm.String)",
"permissionFilter": "userIds",
"searchable": true, "filterable": false, "retrievable": true
},
{
"name": "GroupIds", "type": "Collection(Edm.String)",
"permissionFilter": "groupIds",
"searchable": true, "filterable": false, "retrievable": true
},
{
"name": "RbacScope", "type": "Edm.String",
"permissionFilter": "rbacScope",
"searchable": true, "filterable": false, "retrievable": true
}
],
"permissionFilterOption": "enabled"
}
```


## Create a data source

Modify [data source configuration](search-indexer-access-control-lists-and-role-based-access#create-the-data-source) to specify indexer permission ingestion and the types of permission metadata that you want to index.

A data source needs `indexerPermissionOptions`

.

In this tutorial, use a system-assigned managed identity for the authenticated connection.

```
{
"name" : "my-adlsgen2-acl-datasource",
"type": "adlsgen2",
"indexerPermissionOptions": ["userIds", "groupIds", "rbacScope"],
"credentials": {
"connectionString": "ResourceId=/subscriptions/<your subscription ID>/resourceGroups/<your resource group name>/providers/Microsoft.Storage/storageAccounts/<your storage account name>/;"
},
"container": {
"name": "parks",
"query": null
}
}
```


## Create and run the indexer

Indexer configuration for permission ingestion is primarily about defining `fieldMappings`

from [permission metadata](search-indexer-access-control-lists-and-role-based-access#).

```
{
"name" : "my-adlsgen2-acl-indexer",
"dataSourceName" : "my-adlsgen2-acl-datasource",
"targetIndexName" : "my-adlsgen2-acl-index",
"parameters": {
"batchSize": null,
"maxFailedItems": 0,
"maxFailedItemsPerBatch": 0,
"configuration": {
"dataToExtract": "contentAndMetadata",
"parsingMode": "delimitedText",
"firstLineContainsHeaders": true,
"delimitedTextDelimiter": ",",
"delimitedTextHeaders": ""
},
"fieldMappings": [
{ "sourceFieldName": "metadata_user_ids", "targetFieldName": "UserIds" },
{ "sourceFieldName": "metadata_group_ids", "targetFieldName": "GroupIds" },
{ "sourceFieldName": "metadata_rbac_scope", "targetFieldName": "RbacScope" }
]
}
}
```


After indexer creation and immediate run, the file content along with permission metadata information are indexed into the index.

## Run a query to check results

Now that documents are loaded, you can issue queries against them by using [Documents - Search Post (REST)](/en-us/rest/api/searchservice/documents/search-post).

The URI is extended to include a query input, which is specified by using the `/docs/search`

operator. The query token is passed in the request header. For more information, see [Query-time ACL and RBAC enforcement](search-query-access-control-rbac-enforcement).

```
POST {{endpoint}}/indexes/stateparks/docs/search?api-version=2025-11-01-preview
Authorization: Bearer {{search-token}}
x-ms-query-source-authorization: {{search-token}}
Content-Type: application/json
{
"search": "*",
"select": "name,description,location,GroupIds",
"orderby": "name asc"
}
```
