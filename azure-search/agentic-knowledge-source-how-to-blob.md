---
source_url: https://learn.microsoft.com/en-us/azure/search/agentic-knowledge-source-how-to-blob
fetched_at: 2026-01-25T03:13:05.282450
---

# Create a blob knowledge source from Azure Blob Storage and ADLS Gen2

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Use a *blob knowledge source* to index and query Azure blob content in an agentic retrieval pipeline. [Knowledge sources](agentic-knowledge-source-overview) are created independently, referenced in a [knowledge base](agentic-retrieval-how-to-create-knowledge-base), and used as grounding data when an agent or chatbot calls a [retrieve action](agentic-retrieval-how-to-retrieve) at query time.

Unlike a [search index knowledge source](agentic-knowledge-source-how-to-search-index), which specifies an existing and qualified index, a blob knowledge source specifies an external data source, models, and properties to automatically generate the following Azure AI Search objects:

- A data source that represents a blob container.
- A skillset that chunks and optionally vectorizes multimodal content from the container.
- An index that stores enriched content and meets the criteria for agentic retrieval.
- An indexer that uses the previous objects to drive the indexing and enrichment pipeline.

Note

If user access is specified at the document (blob) level in Azure Storage, a knowledge source can carry permission metadata forward to indexed content in Azure AI Search. For more information, see [ADLS Gen2 permission metadata](/en-us/azure/search/search-indexer-access-control-lists-and-role-based-access) or [Blob RBAC scopes](/en-us/azure/search/search-blob-indexer-role-based-access).

## Prerequisites

Azure AI Search in any

[region that provides agentic retrieval](search-region-support). You must have[semantic ranker enabled](semantic-how-to-enable-disable).An

[Azure Blob Storage](/en-us/azure/storage/common/storage-account-create)or[Azure Data Lake Storage (ADLS) Gen2](/en-us/azure/storage/blobs/create-data-lake-storage-account)account.A blob container with

[supported content types](search-how-to-index-azure-blob-storage#supported-document-formats)for text content. For optional image verbalization, the supported content type depends on whether your chat completion model can analyze and describe the image file.The latest preview version of the

for the .NET SDK.`Azure.Search.Documents`

client libraryPermission to create and use objects on Azure AI Search. We recommend

[role-based access](search-security-rbac), but you can use[API keys](search-security-api-keys)if a role assignment isn't feasible. For more information, see[Connect to a search service](search-get-started-rbac).

## Check for existing knowledge sources

A knowledge source is a top-level, reusable object. Knowing about existing knowledge sources is helpful for either reuse or naming new objects.

Run the following code to list knowledge sources by name and type.

```
// List knowledge sources by name and type
using Azure.Search.Documents.Indexes;
var indexClient = new SearchIndexClient(new Uri(searchEndpoint), credential);
var knowledgeSources = indexClient.GetKnowledgeSourcesAsync();
Console.WriteLine("Knowledge Sources:");
await foreach (var ks in knowledgeSources)
{
Console.WriteLine($" Name: {ks.Name}, Type: {ks.GetType().Name}");
}
```


You can also return a single knowledge source by name to review its JSON definition.

```
using Azure.Search.Documents.Indexes;
using System.Text.Json;
var indexClient = new SearchIndexClient(new Uri(searchEndpoint), credential);
// Specify the knowledge source name to retrieve
string ksNameToGet = "earth-knowledge-source";
// Get its definition
var knowledgeSourceResponse = await indexClient.GetKnowledgeSourceAsync(ksNameToGet);
var ks = knowledgeSourceResponse.Value;
// Serialize to JSON for display
var jsonOptions = new JsonSerializerOptions
{
WriteIndented = true,
DefaultIgnoreCondition = System.Text.Json.Serialization.JsonIgnoreCondition.Never
};
Console.WriteLine(JsonSerializer.Serialize(ks, ks.GetType(), jsonOptions));
```


The following JSON is an example response for a blob knowledge source.

```
{
"name": "my-blob-ks",
"kind": "azureBlob",
"description": "A sample blob knowledge source.",
"encryptionKey": null,
"azureBlobParameters": {
"connectionString": "<REDACTED>",
"containerName": "blobcontainer",
"folderPath": null,
"isADLSGen2": false,
"ingestionParameters": {
"disableImageVerbalization": false,
"ingestionPermissionOptions": [],
"contentExtractionMode": "standard",
"identity": null,
"embeddingModel": {
"kind": "azureOpenAI",
"azureOpenAIParameters": {
"resourceUri": "<REDACTED>",
"deploymentId": "text-embedding-3-large",
"apiKey": "<REDACTED>",
"modelName": "text-embedding-3-large",
"authIdentity": null
}
},
"chatCompletionModel": {
"kind": "azureOpenAI",
"azureOpenAIParameters": {
"resourceUri": "<REDACTED>",
"deploymentId": "gpt-5-mini",
"apiKey": "<REDACTED>",
"modelName": "gpt-5-mini",
"authIdentity": null
}
},
"ingestionSchedule": null,
"assetStore": null,
"aiServices": {
"uri": "<REDACTED>",
"apiKey": "<REDACTED>"
}
},
"createdResources": {
"datasource": "my-blob-ks-datasource",
"indexer": "my-blob-ks-indexer",
"skillset": "my-blob-ks-skillset",
"index": "my-blob-ks-index"
}
}
}
```


Note

Sensitive information is redacted. The generated resources appear at the end of the response.

## Create a knowledge source

Run the following code to [create a blob knowledge source](/en-us/dotnet/api/azure.search.documents.indexes.models.azureblobknowledgesource?view=azure-dotnet-preview&preserve-view=true).

```
// Create a blob knowledge source
using Azure.Search.Documents.Indexes;
using Azure.Search.Documents.Indexes.Models;
using Azure.Search.Documents.KnowledgeBases.Models;
using Azure;
var indexClient = new SearchIndexClient(new Uri(searchEndpoint), new AzureKeyCredential(apiKey));
var chatCompletionParams = new AzureOpenAIVectorizerParameters
{
ResourceUri = new Uri(aoaiEndpoint),
DeploymentName = aoaiGptDeployment,
ModelName = aoaiGptModel
};
var embeddingParams = new AzureOpenAIVectorizerParameters
{
ResourceUri = new Uri(aoaiEndpoint),
DeploymentName = aoaiEmbeddingDeployment,
ModelName = aoaiEmbeddingModel
};
var ingestionParams = new KnowledgeSourceIngestionParameters
{
DisableImageVerbalization = false,
ChatCompletionModel = new KnowledgeBaseAzureOpenAIModel(azureOpenAIParameters: chatCompletionParams),
EmbeddingModel = new KnowledgeSourceAzureOpenAIVectorizer
{
AzureOpenAIParameters = embeddingParams
}
};
var blobParams = new AzureBlobKnowledgeSourceParameters(
connectionString: connectionString,
containerName: containerName
)
{
IsAdlsGen2 = false,
IngestionParameters = ingestionParams
};
var knowledgeSource = new AzureBlobKnowledgeSource(
name: "my-blob-ks",
azureBlobParameters: blobParams
)
{
Description = "This knowledge source pulls from a blob storage container."
};
await indexClient.CreateOrUpdateKnowledgeSourceAsync(knowledgeSource);
Console.WriteLine($"Knowledge source '{knowledgeSource.Name}' created or updated successfully.");
```


### Source-specific properties

You can pass the following properties to create a blob knowledge source.

| Name | Description | Type | Editable | Required |
|---|---|---|---|---|
`name` |
The name of the knowledge source, which must be unique within the knowledge sources collection and follow the
|

`Description`

`encryptionKey`

[customer-managed key](search-security-manage-encryption-keys)to encrypt sensitive information in both the knowledge source and the generated objects.`chatCompletionParams`

`embeddingParams`

`azureBlobParameters`

`connectionString`

, `containerName`

, `folderPath`

, and `isAdlsGen2`

.`connectionString`

[connection string](search-how-to-index-azure-blob-storage#supported-credentials-and-connection-strings)or, if you're using a managed identity, the resource ID.`containerName`

`folderPath`

`isAdlsGen2`

`False`

. Set to `True`

if you're using an ADLS Gen2 storage account.`ingestionParameters`

properties

For indexed knowledge sources only, you can pass the following `ingestionParameters`

properties to control how content is ingested and processed.

| Name | Description | Type | Editable | Required |
|---|---|---|---|---|
`Identity` |
A
|

`DisableImageVerbalization`

`False`

, which *enables*image verbalization. Set to`True`

to *disable*image verbalization.`ChatCompletionModel`

`gpt-4o`

, `gpt-4o-mini`

, `gpt-4.1`

, `gpt-4.1-mini`

, `gpt-4.1-nano`

, `gpt-5`

, `gpt-5-mini`

, and `gpt-5-nano`

. The [GenAI Prompt skill](cognitive-search-skill-genai-prompt)will be included in the generated skillset. Setting this parameter also requires that`disable_image_verbalization`

is set to `False`

.`api_key`

and `deployment_name`

are editable`EmbeddingModel`

`text-embedding-ada-002`

, `text-embedding-3-small`

, and `text-embedding-3-large`

. The [Azure OpenAI Embedding skill](cognitive-search-skill-azure-openai-embedding)will be included in the generated skillset, and the[Azure OpenAI vectorizer](vector-search-vectorizer-azure-open-ai)will be included in the generated index.`api_key`

and `deployment_name`

are editable`ContentExtractionMode`

`minimal`

, which uses standard content extraction for text and images. Set to `standard`

for advanced document cracking and chunking using the [Azure Content Understanding skill](cognitive-search-skill-content-understanding), which will be included in the generated skillset. For`standard`

only, the `AiServices`

and `AssetStore`

parameters are specifiable.`AiServices`

`ContentExtractionMode`

is set to `standard`

.`api_key`

is editable`IngestionSchedule`

[add a schedule](search-howto-schedule-indexers)later to automate data refresh.`IngestionPermissionOptions`

[ADLS Gen2](agentic-knowledge-source-how-to-blob)or[indexed SharePoint](agentic-knowledge-source-how-to-sharepoint-indexed). If you specify`user_ids`

, `group_ids`

, or `rbac_scope`

, the generated [ADLS Gen2 indexer](search-indexer-access-control-lists-and-role-based-access)or[SharePoint indexer](search-indexer-sharepoint-access-control-lists)will include the ingested permissions.## Check ingestion status

Run the following code to monitor ingestion progress and health, including [indexer status](/en-us/dotnet/api/azure.search.documents.indexes.models.knowledgesourcestatus?view=azure-dotnet-preview&preserve-view=true) for knowledge sources that generate an indexer pipeline and populate a search index.

```
// Get knowledge source ingestion status
using Azure.Search.Documents.Indexes;
using System.Text.Json;
var indexClient = new SearchIndexClient(new Uri(searchEndpoint), new AzureKeyCredential(apiKey));
// Get the knowledge source status
var statusResponse = await indexClient.GetKnowledgeSourceStatusAsync(knowledgeSourceName);
var status = statusResponse.Value;
// Serialize to JSON for display
var json = JsonSerializer.Serialize(status, new JsonSerializerOptions { WriteIndented = true });
Console.WriteLine(json);
```


A response for a request that includes ingestion parameters and is actively ingesting content might look like the following example.

```
{
"synchronizationStatus": "active", // creating, active, deleting
"synchronizationInterval" : "1d", // null if no schedule
"currentSynchronizationState" : { // spans multiple indexer "runs"
"startTime": "2025-10-27T19:30:00Z",
"itemUpdatesProcessed": 1100,
"itemsUpdatesFailed": 100,
"itemsSkipped": 1100,
},
"lastSynchronizationState" : { // null on first sync
"startTime": "2025-10-27T19:30:00Z",
"endTime": "2025-10-27T19:40:01Z", // this value appears on the activity record on each /retrieve
"itemUpdatesProcessed": 1100,
"itemsUpdatesFailed": 100,
"itemsSkipped": 1100,
},
"statistics": { // null on first sync
"totalSynchronization": 25,
"averageSynchronizationDuration": "00:15:20",
"averageItemsProcessedPerSynchronization" : 500
}
}
```


## Review the created objects

When you create a blob knowledge source, your search service also creates an indexer, index, skillset, and data source. We don't recommend that you edit these objects, as introducing an error or incompatibility can break the pipeline.

After you create a knowledge source, the response lists the created objects. These objects are created according to a fixed template, and their names are based on the name of the knowledge source. You can't change the object names.

We recommend using the Azure portal to validate output creation. The workflow is:

- Check the indexer for success or failure messages. Connection or quota errors appear here.
- Check the index for searchable content. Use Search Explorer to run queries.
- Check the skillset to learn how your content is chunked and optionally vectorized.
- Check the data source for connection details. Our example uses API keys for simplicity, but you can use Microsoft Entra ID for authentication and role-based access control for authorization.

## Assign to a knowledge base

If you're satisfied with the knowledge source, continue to the next step: specify the knowledge source in a [knowledge base](agentic-retrieval-how-to-create-knowledge-base).

After the knowledge base is configured, use the [retrieve action](agentic-retrieval-how-to-retrieve) to query the knowledge source.

## Delete a knowledge source

Before you can delete a knowledge source, you must delete any knowledge base that references it or update the knowledge base definition to remove the reference. For knowledge sources that generate an index and indexer pipeline, all *generated objects* are also deleted. However, if you used an existing index to create a knowledge source, your index isn't deleted.

If you try to delete a knowledge source that's in use, the action fails and returns a list of affected knowledge bases.

To delete a knowledge source:

Get a list of all knowledge bases on your search service.

`using Azure.Search.Documents.Indexes; var indexClient = new SearchIndexClient(new Uri(searchEndpoint), credential); var knowledgeBases = indexClient.GetKnowledgeBasesAsync(); Console.WriteLine("Knowledge Bases:"); await foreach (var kb in knowledgeBases) { Console.WriteLine($" - {kb.Name}"); }`

An example response might look like the following:

`Knowledge Bases: - earth-knowledge-base - hotels-sample-knowledge-base - my-demo-knowledge-base`

Get an individual knowledge base definition to check for knowledge source references.

`using Azure.Search.Documents.Indexes; using System.Text.Json; var indexClient = new SearchIndexClient(new Uri(searchEndpoint), credential); // Specify the knowledge base name to retrieve string kbNameToGet = "earth-knowledge-base"; // Get a specific knowledge base definition var knowledgeBaseResponse = await indexClient.GetKnowledgeBaseAsync(kbNameToGet); var kb = knowledgeBaseResponse.Value; // Serialize to JSON for display string json = JsonSerializer.Serialize(kb, new JsonSerializerOptions { WriteIndented = true }); Console.WriteLine(json);`

An example response might look like the following:

`{ "Name": "earth-knowledge-base", "KnowledgeSources": [ { "Name": "earth-knowledge-source" } ], "Models": [ {} ], "RetrievalReasoningEffort": {}, "OutputMode": {}, "ETag": "\u00220x8DE278629D782B3\u0022", "EncryptionKey": null, "Description": null, "RetrievalInstructions": null, "AnswerInstructions": null }`

Either delete the knowledge base or

[update the knowledge base](/en-us/dotnet/api/azure.search.documents.indexes.searchindexclient.createorupdateknowledgebaseasync?view=azure-dotnet-preview&preserve-view=true)to remove the knowledge source if you have multiple sources. This example shows deletion.`using Azure.Search.Documents.Indexes; var indexClient = new SearchIndexClient(new Uri(searchEndpoint), credential); await indexClient.DeleteKnowledgeBaseAsync(knowledgeBaseName); System.Console.WriteLine($"Knowledge base '{knowledgeBaseName}' deleted successfully.");`

Delete the knowledge source.

`await indexClient.DeleteKnowledgeSourceAsync(knowledgeSourceName); System.Console.WriteLine($"Knowledge source '{knowledgeSourceName}' deleted successfully.");`


Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Use a *blob knowledge source* to index and query Azure blob content in an agentic retrieval pipeline. [Knowledge sources](agentic-knowledge-source-overview) are created independently, referenced in a [knowledge base](agentic-retrieval-how-to-create-knowledge-base), and used as grounding data when an agent or chatbot calls a [retrieve action](agentic-retrieval-how-to-retrieve) at query time.

Unlike a [search index knowledge source](agentic-knowledge-source-how-to-search-index), which specifies an existing and qualified index, a blob knowledge source specifies an external data source, models, and properties to automatically generate the following Azure AI Search objects:

- A data source that represents a blob container.
- A skillset that chunks and optionally vectorizes multimodal content from the container.
- An index that stores enriched content and meets the criteria for agentic retrieval.
- An indexer that uses the previous objects to drive the indexing and enrichment pipeline.

Note

If user access is specified at the document (blob) level in Azure Storage, a knowledge source can carry permission metadata forward to indexed content in Azure AI Search. For more information, see [ADLS Gen2 permission metadata](/en-us/azure/search/search-indexer-access-control-lists-and-role-based-access) or [Blob RBAC scopes](/en-us/azure/search/search-blob-indexer-role-based-access).

## Prerequisites

Azure AI Search in any

[region that provides agentic retrieval](search-region-support). You must have[semantic ranker enabled](semantic-how-to-enable-disable).An

[Azure Blob Storage](/en-us/azure/storage/common/storage-account-create)or[Azure Data Lake Storage (ADLS) Gen2](/en-us/azure/storage/blobs/create-data-lake-storage-account)account.A blob container with

[supported content types](search-how-to-index-azure-blob-storage#supported-document-formats)for text content. For optional image verbalization, the supported content type depends on whether your chat completion model can analyze and describe the image file.The latest preview version of the

for Python.`azure-search-documents`

client libraryPermission to create and use objects on Azure AI Search. We recommend

[role-based access](search-security-rbac), but you can use[API keys](search-security-api-keys)if a role assignment isn't feasible. For more information, see[Connect to a search service](search-get-started-rbac).

## Check for existing knowledge sources

A knowledge source is a top-level, reusable object. Knowing about existing knowledge sources is helpful for either reuse or naming new objects.

Run the following code to list knowledge sources by name and type.

```
# List knowledge sources by name and type
import requests
import json
endpoint = "{search_url}/knowledgesources"
params = {"api-version": "2025-11-01-preview", "$select": "name, kind"}
headers = {"api-key": "{api_key}"}
response = requests.get(endpoint, params = params, headers = headers)
print(json.dumps(response.json(), indent = 2))
```


You can also return a single knowledge source by name to review its JSON definition.

```
# Get a knowledge source definition
import requests
import json
endpoint = "{search_url}/knowledgesources/{knowledge_source_name}"
params = {"api-version": "2025-11-01-preview"}
headers = {"api-key": "{api_key}"}
response = requests.get(endpoint, params = params, headers = headers)
print(json.dumps(response.json(), indent = 2))
```


The following JSON is an example response for a blob knowledge source.

```
{
"name": "my-blob-ks",
"kind": "azureBlob",
"description": "A sample blob knowledge source.",
"encryptionKey": null,
"azureBlobParameters": {
"connectionString": "<REDACTED>",
"containerName": "blobcontainer",
"folderPath": null,
"isADLSGen2": false,
"ingestionParameters": {
"disableImageVerbalization": false,
"ingestionPermissionOptions": [],
"contentExtractionMode": "standard",
"identity": null,
"embeddingModel": {
"kind": "azureOpenAI",
"azureOpenAIParameters": {
"resourceUri": "<REDACTED>",
"deploymentId": "text-embedding-3-large",
"apiKey": "<REDACTED>",
"modelName": "text-embedding-3-large",
"authIdentity": null
}
},
"chatCompletionModel": {
"kind": "azureOpenAI",
"azureOpenAIParameters": {
"resourceUri": "<REDACTED>",
"deploymentId": "gpt-5-mini",
"apiKey": "<REDACTED>",
"modelName": "gpt-5-mini",
"authIdentity": null
}
},
"ingestionSchedule": null,
"assetStore": null,
"aiServices": {
"uri": "<REDACTED>",
"apiKey": "<REDACTED>"
}
},
"createdResources": {
"datasource": "my-blob-ks-datasource",
"indexer": "my-blob-ks-indexer",
"skillset": "my-blob-ks-skillset",
"index": "my-blob-ks-index"
}
}
}
```


Note

Sensitive information is redacted. The generated resources appear at the end of the response.

## Create a knowledge source

Run the following code to create a blob knowledge source.

```
# Create a blob knowledge source
from azure.core.credentials import AzureKeyCredential
from azure.search.documents.indexes import SearchIndexClient
from azure.search.documents.indexes.models import AzureBlobKnowledgeSource, AzureBlobKnowledgeSourceParameters, KnowledgeBaseAzureOpenAIModel, AzureOpenAIVectorizerParameters, KnowledgeSourceAzureOpenAIVectorizer, KnowledgeSourceContentExtractionMode, KnowledgeSourceIngestionParameters
index_client = SearchIndexClient(endpoint = "search_url", credential = AzureKeyCredential("api_key"))
knowledge_source = AzureBlobKnowledgeSource(
name = "my-blob-ks",
description = "This knowledge source pulls from a blob storage container.",
encryption_key = None,
azure_blob_parameters = AzureBlobKnowledgeSourceParameters(
connection_string = "blob_connection_string",
container_name = "blob_container_name",
folder_path = None,
is_adls_gen2 = False,
ingestion_parameters = KnowledgeSourceIngestionParameters(
identity = None,
disable_image_verbalization = False,
chat_completion_model = KnowledgeBaseAzureOpenAIModel(
azure_open_ai_parameters = AzureOpenAIVectorizerParameters(
# TRIMMED FOR BREVITY
)
),
embedding_model = KnowledgeSourceAzureOpenAIVectorizer(
azure_open_ai_parameters=AzureOpenAIVectorizerParameters(
# TRIMMED FOR BREVITY
)
),
content_extraction_mode = KnowledgeSourceContentExtractionMode.MINIMAL,
ingestion_schedule = None,
ingestion_permission_options = None
)
)
)
index_client.create_or_update_knowledge_source(knowledge_source)
print(f"Knowledge source '{knowledge_source.name}' created or updated successfully.")
```


### Source-specific properties

You can pass the following properties to create a blob knowledge source.

| Name | Description | Type | Editable | Required |
|---|---|---|---|---|
`name` |
The name of the knowledge source, which must be unique within the knowledge sources collection and follow the
|

`description`

`encryption_key`

[customer-managed key](search-security-manage-encryption-keys)to encrypt sensitive information in both the knowledge source and the generated objects.`azure_blob_parameters`

`connection_string`

, `container_name`

, `folder_path`

, and `is_adls_gen2`

.`connection_string`

[connection string](search-how-to-index-azure-blob-storage#supported-credentials-and-connection-strings)or, if you're using a managed identity, the resource ID.`container_name`

`folder_path`

`is_adls_gen2`

`False`

. Set to `True`

if you're using an ADLS Gen2 storage account.`ingestionParameters`

properties

For indexed knowledge sources only, you can pass the following `ingestionParameters`

properties to control how content is ingested and processed.

| Name | Description | Type | Editable | Required |
|---|---|---|---|---|
`identity` |
A
|

`disable_image_verbalization`

`False`

, which *enables*image verbalization. Set to`True`

to *disable*image verbalization.`chat_completion_model`

`gpt-4o`

, `gpt-4o-mini`

, `gpt-4.1`

, `gpt-4.1-mini`

, `gpt-4.1-nano`

, `gpt-5`

, `gpt-5-mini`

, and `gpt-5-nano`

. The [GenAI Prompt skill](cognitive-search-skill-genai-prompt)will be included in the generated skillset. Setting this parameter also requires that`disable_image_verbalization`

is set to `False`

.`api_key`

and `deployment_name`

are editable`embedding_model`

`text-embedding-ada-002`

, `text-embedding-3-small`

, and `text-embedding-3-large`

. The [Azure OpenAI Embedding skill](cognitive-search-skill-azure-openai-embedding)will be included in the generated skillset, and the[Azure OpenAI vectorizer](vector-search-vectorizer-azure-open-ai)will be included in the generated index.`api_key`

and `deployment_name`

are editable`content_extraction_mode`

`minimal`

, which uses standard content extraction for text and images. Set to `standard`

for advanced document cracking and chunking using the [Azure Content Understanding skill](cognitive-search-skill-content-understanding), which will be included in the generated skillset. For`standard`

only, the `ai_services`

and `asset_store`

parameters are specifiable.`ai_services`

`content_extraction_mode`

is set to `standard`

.`api_key`

is editable`asset_store`

`content_extraction_mode`

is set to `standard`

.`ingestion_schedule`

[add a schedule](search-howto-schedule-indexers)later to automate data refresh.`ingestion_permission_options`

[ADLS Gen2](agentic-knowledge-source-how-to-blob)or[indexed SharePoint](agentic-knowledge-source-how-to-sharepoint-indexed). If you specify`user_ids`

, `group_ids`

, or `rbac_scope`

, the generated [ADLS Gen2 indexer](search-indexer-access-control-lists-and-role-based-access)or[SharePoint indexer](search-indexer-sharepoint-access-control-lists)will include the ingested permissions.## Check ingestion status

Run the following code to monitor ingestion progress and health, including indexer status for knowledge sources that generate an indexer pipeline and populate a search index.

```
# Check knowledge source ingestion status
import requests
import json
endpoint = "{search_url}/knowledgesources/{knowledge_source_name}/status"
params = {"api-version": "2025-11-01-preview"}
headers = {"api-key": "{api_key}"}
response = requests.get(endpoint, params = params, headers = headers)
print(json.dumps(response.json(), indent = 2))
```


A response for a request that includes ingestion parameters and is actively ingesting content might look like the following example.

```
{
"synchronizationStatus": "active", // creating, active, deleting
"synchronizationInterval" : "1d", // null if no schedule
"currentSynchronizationState" : { // spans multiple indexer "runs"
"startTime": "2025-10-27T19:30:00Z",
"itemUpdatesProcessed": 1100,
"itemsUpdatesFailed": 100,
"itemsSkipped": 1100,
},
"lastSynchronizationState" : { // null on first sync
"startTime": "2025-10-27T19:30:00Z",
"endTime": "2025-10-27T19:40:01Z", // this value appears on the activity record on each /retrieve
"itemUpdatesProcessed": 1100,
"itemsUpdatesFailed": 100,
"itemsSkipped": 1100,
},
"statistics": { // null on first sync
"totalSynchronization": 25,
"averageSynchronizationDuration": "00:15:20",
"averageItemsProcessedPerSynchronization" : 500
}
}
```


## Review the created objects

When you create a blob knowledge source, your search service also creates an indexer, index, skillset, and data source. We don't recommend that you edit these objects, as introducing an error or incompatibility can break the pipeline.

After you create a knowledge source, the response lists the created objects. These objects are created according to a fixed template, and their names are based on the name of the knowledge source. You can't change the object names.

We recommend using the Azure portal to validate output creation. The workflow is:

- Check the indexer for success or failure messages. Connection or quota errors appear here.
- Check the index for searchable content. Use Search Explorer to run queries.
- Check the skillset to learn how your content is chunked and optionally vectorized.
- Check the data source for connection details. Our example uses API keys for simplicity, but you can use Microsoft Entra ID for authentication and role-based access control for authorization.

## Assign to a knowledge base

If you're satisfied with the knowledge source, continue to the next step: specify the knowledge source in a [knowledge base](agentic-retrieval-how-to-create-knowledge-base).

After the knowledge base is configured, use the [retrieve action](agentic-retrieval-how-to-retrieve) to query the knowledge source.

## Delete a knowledge source

Before you can delete a knowledge source, you must delete any knowledge base that references it or update the knowledge base definition to remove the reference. For knowledge sources that generate an index and indexer pipeline, all *generated objects* are also deleted. However, if you used an existing index to create a knowledge source, your index isn't deleted.

If you try to delete a knowledge source that's in use, the action fails and returns a list of affected knowledge bases.

To delete a knowledge source:

Get a list of all knowledge bases on your search service.

`# Get knowledge bases import requests import json endpoint = "{search_url}/knowledgebases" params = {"api-version": "2025-11-01-preview", "$select": "name"} headers = {"api-key": "{api_key}"} response = requests.get(endpoint, params = params, headers = headers) print(json.dumps(response.json(), indent = 2))`

An example response might look like the following:

`{ "@odata.context": "https://my-search-service.search.windows.net/$metadata#knowledgebases(name)", "value": [ { "name": "my-kb" }, { "name": "my-kb-2" } ] }`

Get an individual knowledge base definition to check for knowledge source references.

`# Get a knowledge base definition import requests import json endpoint = "{search_url}/knowledgebases/{knowledge_base_name}" params = {"api-version": "2025-11-01-preview"} headers = {"api-key": "{api_key}"} response = requests.get(endpoint, params = params, headers = headers) print(json.dumps(response.json(), indent = 2))`

An example response might look like the following:

`{ "name": "my-kb", "description": null, "retrievalInstructions": null, "answerInstructions": null, "outputMode": null, "knowledgeSources": [ { "name": "my-blob-ks", } ], "models": [], "encryptionKey": null, "retrievalReasoningEffort": { "kind": "low" } }`

Either delete the knowledge base or

[update the knowledge base](/en-us/rest/api/searchservice/knowledge-bases/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true)to remove the knowledge source if you have multiple sources. This example shows deletion.`# Delete a knowledge base from azure.core.credentials import AzureKeyCredential from azure.search.documents.indexes import SearchIndexClient index_client = SearchIndexClient(endpoint = "search_url", credential = AzureKeyCredential("api_key")) index_client.delete_knowledge_base("knowledge_base_name") print(f"Knowledge base deleted successfully.")`

Delete the knowledge source.

`# Delete a knowledge source from azure.core.credentials import AzureKeyCredential from azure.search.documents.indexes import SearchIndexClient index_client = SearchIndexClient(endpoint = "search_url", credential = AzureKeyCredential("api_key")) index_client.delete_knowledge_source("knowledge_source_name") print(f"Knowledge source deleted successfully.")`


Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Use a *blob knowledge source* to index and query Azure blob content in an agentic retrieval pipeline. [Knowledge sources](agentic-knowledge-source-overview) are created independently, referenced in a [knowledge base](agentic-retrieval-how-to-create-knowledge-base), and used as grounding data when an agent or chatbot calls a [retrieve action](agentic-retrieval-how-to-retrieve) at query time.

Unlike a [search index knowledge source](agentic-knowledge-source-how-to-search-index), which specifies an existing and qualified index, a blob knowledge source specifies an external data source, models, and properties to automatically generate the following Azure AI Search objects:

- A data source that represents a blob container.
- A skillset that chunks and optionally vectorizes multimodal content from the container.
- An index that stores enriched content and meets the criteria for agentic retrieval.
- An indexer that uses the previous objects to drive the indexing and enrichment pipeline.

Note

If user access is specified at the document (blob) level in Azure Storage, a knowledge source can carry permission metadata forward to indexed content in Azure AI Search. For more information, see [ADLS Gen2 permission metadata](/en-us/azure/search/search-indexer-access-control-lists-and-role-based-access) or [Blob RBAC scopes](/en-us/azure/search/search-blob-indexer-role-based-access).

## Prerequisites

Azure AI Search in any

[region that provides agentic retrieval](search-region-support). You must have[semantic ranker enabled](semantic-how-to-enable-disable).An

[Azure Blob Storage](/en-us/azure/storage/common/storage-account-create)or[Azure Data Lake Storage (ADLS) Gen2](/en-us/azure/storage/blobs/create-data-lake-storage-account)account.A blob container with

[supported content types](search-how-to-index-azure-blob-storage#supported-document-formats)for text content. For optional image verbalization, the supported content type depends on whether your chat completion model can analyze and describe the image file.The

[2025-11-01-preview](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2025-11-01-preview&preserve-view=true)version of the Search Service REST APIs.Permission to create and use objects on Azure AI Search. We recommend

[role-based access](search-security-rbac), but you can use[API keys](search-security-api-keys)if a role assignment isn't feasible. For more information, see[Connect to a search service](search-get-started-rbac).

## Check for existing knowledge sources

A knowledge source is a top-level, reusable object. Knowing about existing knowledge sources is helpful for either reuse or naming new objects.

Use [Knowledge Sources - Get (REST API)](/en-us/rest/api/searchservice/knowledge-sources/get?view=rest-searchservice-2025-11-01-preview&preserve-view=true) to list knowledge sources by name and type.

```
### List knowledge sources by name and type
GET {{search-url}}/knowledgesources?api-version=2025-11-01-preview&$select=name,kind
api-key: {{api-key}}
```


You can also return a single knowledge source by name to review its JSON definition.

```
### Get a knowledge source definition
GET {{search-url}}/knowledgesources/{{knowledge-source-name}}?api-version=2025-11-01-preview
api-key: {{api-key}}
```


The following JSON is an example response for a blob knowledge source.

```
{
"name": "my-blob-ks",
"kind": "azureBlob",
"description": "A sample blob knowledge source.",
"encryptionKey": null,
"azureBlobParameters": {
"connectionString": "<REDACTED>",
"containerName": "blobcontainer",
"folderPath": null,
"isADLSGen2": false,
"ingestionParameters": {
"disableImageVerbalization": false,
"ingestionPermissionOptions": [],
"contentExtractionMode": "standard",
"identity": null,
"embeddingModel": {
"kind": "azureOpenAI",
"azureOpenAIParameters": {
"resourceUri": "<REDACTED>",
"deploymentId": "text-embedding-3-large",
"apiKey": "<REDACTED>",
"modelName": "text-embedding-3-large",
"authIdentity": null
}
},
"chatCompletionModel": {
"kind": "azureOpenAI",
"azureOpenAIParameters": {
"resourceUri": "<REDACTED>",
"deploymentId": "gpt-5-mini",
"apiKey": "<REDACTED>",
"modelName": "gpt-5-mini",
"authIdentity": null
}
},
"ingestionSchedule": null,
"assetStore": null,
"aiServices": {
"uri": "<REDACTED>",
"apiKey": "<REDACTED>"
}
},
"createdResources": {
"datasource": "my-blob-ks-datasource",
"indexer": "my-blob-ks-indexer",
"skillset": "my-blob-ks-skillset",
"index": "my-blob-ks-index"
}
}
}
```


Note

Sensitive information is redacted. The generated resources appear at the end of the response.

## Create a knowledge source

Use [Knowledge Sources - Create or Update (REST API)](/en-us/rest/api/searchservice/knowledge-sources/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true) to create a blob knowledge source.

```
PUT {{search-url}}/knowledgesources/my-blob-ks?api-version=2025-11-01-preview
api-key: {{api-key}}
Content-Type: application/json
{
"name": "my-blob-ks",
"kind": "azureBlob",
"description": "This knowledge source pulls from a blob storage container.",
"encryptionKey": null,
"azureBlobParameters": {
"connectionString": "<YOUR AZURE STORAGE CONNECTION STRING>",
"containerName": "<YOUR BLOB CONTAINER NAME>",
"folderPath": null,
"isADLSGen2": false,
"ingestionParameters": {
"identity": null,
"disableImageVerbalization": null,
"chatCompletionModel": { TRIMMED FOR BREVITY },
"embeddingModel": { TRIMMED FOR BREVITY },
"contentExtractionMode": "minimal",
"ingestionSchedule": null,
"ingestionPermissionOptions": []
}
}
}
```


### Source-specific properties

You can pass the following properties to create a blob knowledge source.

| Name | Description | Type | Editable | Required |
|---|---|---|---|---|
`name` |
The name of the knowledge source, which must be unique within the knowledge sources collection and follow the
|

`kind`

`azureBlob`

in this case.`description`

`encryptionKey`

[customer-managed key](search-security-manage-encryption-keys)to encrypt sensitive information in both the knowledge source and the generated objects.`azureBlobParameters`

`connectionString`

, `containerName`

, `folderPath`

, and `isADLSGen2`

.`connectionString`

[connection string](search-how-to-index-azure-blob-storage#supported-credentials-and-connection-strings)or, if you're using a managed identity, the resource ID.`containerName`

`folderPath`

`isADLSGen2`

`false`

. Set to `true`

if you're using an ADLS Gen2 storage account.`ingestionParameters`

properties

For indexed knowledge sources only, you can pass the following `ingestionParameters`

properties to control how content is ingested and processed.

| Name | Description | Type | Editable | Required |
|---|---|---|---|---|
`identity` |
A
|

`disableImageVerbalization`

`false`

, which *enables*image verbalization. Set to`true`

to *disable*image verbalization.`chatCompletionModel`

`gpt-4o`

, `gpt-4o-mini`

, `gpt-4.1`

, `gpt-4.1-mini`

, `gpt-4.1-nano`

, `gpt-5`

, `gpt-5-mini`

, and `gpt-5-nano`

. The [GenAI Prompt skill](cognitive-search-skill-genai-prompt)will be included in the generated skillset. Setting this parameter also requires that`disableImageVerbalization`

is set to `false`

.`apiKey`

and `deploymentId`

are editable`embeddingModel`

`text-embedding-ada-002`

, `text-embedding-3-small`

, and `text-embedding-3-large`

. The [Azure OpenAI Embedding skill](cognitive-search-skill-azure-openai-embedding)will be included in the generated skillset, and the[Azure OpenAI vectorizer](vector-search-vectorizer-azure-open-ai)will be included in the generated index.`apiKey`

and `deploymentId`

are editable`contentExtractionMode`

`minimal`

, which uses standard content extraction for text and images. Set to `standard`

for advanced document cracking and chunking using the [Azure Content Understanding skill](cognitive-search-skill-content-understanding), which will be included in the generated skillset. For`standard`

only, the `aiServices`

and `assetStore`

parameters are specifiable.`aiServices`

`contentExtractionMode`

is set to `standard`

.`apiKey`

is editable`assetStore`

`contentExtractionMode`

is set to `standard`

.`ingestionSchedule`

[add a schedule](search-howto-schedule-indexers)later to automate data refresh.`ingestionPermissionOptions`

[ADLS Gen2](agentic-knowledge-source-how-to-blob)or[indexed SharePoint](agentic-knowledge-source-how-to-sharepoint-indexed). If you specify`userIds`

, `groupIds`

, or `rbacScope`

, the generated [ADLS Gen2 indexer](search-indexer-access-control-lists-and-role-based-access)or[SharePoint indexer](search-indexer-sharepoint-access-control-lists)will include the ingested permissions.## Check ingestion status

Use [Knowledge Sources - Status (REST API)](/en-us/rest/api/searchservice/knowledge-sources/get-status) to monitor ingestion progress and health, including indexer status for knowledge sources that generate an indexer pipeline and populate a search index.

```
### Check knowledge source ingestion status
GET {{search-url}}/knowledgesources/{{knowledge-source-name}}/status?api-version=2025-11-01-preview
api-key: {{api-key}}
Content-Type: application/json
```


A response for a request that includes ingestion parameters and is actively ingesting content might look like the following example.

```
{
"synchronizationStatus": "active", // creating, active, deleting
"synchronizationInterval" : "1d", // null if no schedule
"currentSynchronizationState" : { // spans multiple indexer "runs"
"startTime": "2025-10-27T19:30:00Z",
"itemUpdatesProcessed": 1100,
"itemsUpdatesFailed": 100,
"itemsSkipped": 1100,
},
"lastSynchronizationState" : { // null on first sync
"startTime": "2025-10-27T19:30:00Z",
"endTime": "2025-10-27T19:40:01Z", // this value appears on the activity record on each /retrieve
"itemUpdatesProcessed": 1100,
"itemsUpdatesFailed": 100,
"itemsSkipped": 1100,
},
"statistics": { // null on first sync
"totalSynchronization": 25,
"averageSynchronizationDuration": "00:15:20",
"averageItemsProcessedPerSynchronization" : 500
}
}
```


## Review the created objects

When you create a blob knowledge source, your search service also creates an indexer, index, skillset, and data source. We don't recommend that you edit these objects, as introducing an error or incompatibility can break the pipeline.

After you create a knowledge source, the response lists the created objects. These objects are created according to a fixed template, and their names are based on the name of the knowledge source. You can't change the object names.

We recommend using the Azure portal to validate output creation. The workflow is:

- Check the indexer for success or failure messages. Connection or quota errors appear here.
- Check the index for searchable content. Use Search Explorer to run queries.
- Check the skillset to learn how your content is chunked and optionally vectorized.
- Check the data source for connection details. Our example uses API keys for simplicity, but you can use Microsoft Entra ID for authentication and role-based access control for authorization.

## Assign to a knowledge base

If you're satisfied with the knowledge source, continue to the next step: specify the knowledge source in a [knowledge base](agentic-retrieval-how-to-create-knowledge-base).

After the knowledge base is configured, use the [retrieve action](agentic-retrieval-how-to-retrieve) to query the knowledge source.

## Delete a knowledge source

Before you can delete a knowledge source, you must delete any knowledge base that references it or update the knowledge base definition to remove the reference. For knowledge sources that generate an index and indexer pipeline, all *generated objects* are also deleted. However, if you used an existing index to create a knowledge source, your index isn't deleted.

If you try to delete a knowledge source that's in use, the action fails and returns a list of affected knowledge bases.

To delete a knowledge source:

Get a list of all knowledge bases on your search service.

`### Get knowledge bases GET {{search-endpoint}}/knowledgebases?api-version=2025-11-01-preview&$select=name api-key: {{api-key}}`

An example response might look like the following:

`{ "@odata.context": "https://my-search-service.search.windows.net/$metadata#knowledgebases(name)", "value": [ { "name": "my-kb" }, { "name": "my-kb-2" } ] }`

Get an individual knowledge base definition to check for knowledge source references.

`### Get a knowledge base definition GET {{search-endpoint}}/knowledgebases/{{knowledge-base-name}}?api-version=2025-11-01-preview api-key: {{api-key}}`

An example response might look like the following:

`{ "name": "my-kb", "description": null, "retrievalInstructions": null, "answerInstructions": null, "outputMode": null, "knowledgeSources": [ { "name": "my-blob-ks", } ], "models": [], "encryptionKey": null, "retrievalReasoningEffort": { "kind": "low" } }`

Either delete the knowledge base or

[update the knowledge base](/en-us/rest/api/searchservice/knowledge-bases/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true)by removing the knowledge source if you have multiple sources. This example shows deletion.`### Delete a knowledge base DELETE {{search-endpoint}}/knowledgebases/{{knowledge-base-name}}?api-version=2025-11-01-preview api-key: {{api-key}}`

Delete the knowledge source.

`### Delete a knowledge source DELETE {{search-endpoint}}/knowledgesources/{{knowledge-source-name}}?api-version=2025-11-01-preview api-key: {{api-key}}`