---
source_url: https://learn.microsoft.com/en-us/azure/search/agentic-knowledge-source-how-to-sharepoint-indexed
fetched_at: 2026-01-25T02:06:24.090216
---

# Create an indexed SharePoint knowledge source

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Use an *indexed SharePoint knowledge source* to index and query SharePoint content in an agentic retrieval pipeline. [Knowledge sources](agentic-knowledge-source-overview) are created independently, referenced in a [knowledge base](agentic-retrieval-how-to-create-knowledge-base), and used as grounding data when an agent or chatbot calls a [retrieve action](agentic-retrieval-how-to-retrieve) at query time.

When you create an indexed SharePoint knowledge source, you specify a SharePoint connection string, models, and properties to automatically generate the following Azure AI Search objects:

- A data source that points to SharePoint sites.
- A skillset that chunks and optionally vectorizes multimodal content.
- An index that stores enriched content and meets the criteria for agentic retrieval.
- An indexer that uses the previous objects to drive the indexing and enrichment pipeline.

## Prerequisites

Azure AI Search in any

[region that provides agentic retrieval](search-region-support). You must have[semantic ranker enabled](semantic-how-to-enable-disable).Completion of the

[SharePoint indexer prerequisites](search-how-to-index-sharepoint-online#prerequisites).Completion of three SharePoint indexer configuration steps:

The latest preview version of the

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


The following JSON is an example response for an indexed SharePoint knowledge source.

```
{
"name": "my-indexed-sharepoint-ks",
"kind": "indexedSharePoint",
"description": "A sample indexed SharePoint knowledge source",
"encryptionKey": null,
"indexedSharePointParameters": {
"connectionString": "<redacted>",
"containerName": "defaultSiteLibrary",
"query": null,
"ingestionParameters": {
"disableImageVerbalization": false,
"ingestionPermissionOptions": [],
"contentExtractionMode": "minimal",
"identity": null,
"embeddingModel": {
"kind": "azureOpenAI",
"azureOpenAIParameters": {
"resourceUri": "<redacted>",
"deploymentId": "text-embedding-3-large",
"apiKey": "<redacted>",
"modelName": "text-embedding-3-large",
"authIdentity": null
}
},
"chatCompletionModel": null,
"ingestionSchedule": null,
"assetStore": null,
"aiServices": null
},
"createdResources": {
"datasource": "my-indexed-sharepoint-ks-datasource",
"indexer": "my-indexed-sharepoint-ks-indexer",
"skillset": "my-indexed-sharepoint-ks-skillset",
"index": "my-indexed-sharepoint-ks-index"
}
},
"indexedOneLakeParameters": null
}
```


Note

Sensitive information is redacted. The generated resources appear at the end of the response.

## Create a knowledge source

Run the following code to create an indexed SharePoint knowledge source.

```
// Create an IndexedSharePoint knowledge source
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
var sharePointParams = new IndexedSharePointKnowledgeSourceParameters(
connectionString: sharePointConnectionString,
containerName: "defaultSiteLibrary")
{
IngestionParameters = ingestionParams
};
var knowledgeSource = new IndexedSharePointKnowledgeSource(
name: "my-indexed-sharepoint-ks",
indexedSharePointParameters: sharePointParams)
{
Description = "A sample indexed SharePoint knowledge source."
};
await indexClient.CreateOrUpdateKnowledgeSourceAsync(knowledgeSource);
Console.WriteLine($"Knowledge source '{knowledgeSource.Name}' created or updated successfully.");
```


### Source-specific properties

You can pass the following properties to create an indexed SharePoint knowledge source.

| Name | Description | Type | Editable | Required |
|---|---|---|---|---|
`Name` |
The name of the knowledge source, which must be unique within the knowledge sources collection and follow the
|

`Description`

`EncryptionKey`

[customer-managed key](search-security-manage-encryption-keys)to encrypt sensitive information in both the knowledge source and the generated objects.`IndexedSharePointKnowledgeSourceParameters`

`connectionString`

, `containerName`

, and `query`

.`connectionString`

[Connection string syntax](search-how-to-index-sharepoint-online#connection-string-format).`containerName`

`defaultSiteLibrary`

to index content from the site's default document library or `allSiteLibraries`

to index content from every document library in the site. Ignore `useQuery`

for now.`query`

[query](search-how-to-index-sharepoint-online#query)to filter SharePoint content.`ingestion_parameters`

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

When you create an indexed SharePoint knowledge source, your search service also creates an indexer, index, skillset, and data source. We don't recommend that you edit these objects, as introducing an error or incompatibility can break the pipeline.

After you create a knowledge source, the response lists the created objects. These objects are created according to a fixed template, and their names are based on the name of the knowledge source. You can't change the object names.

We recommend using the Azure portal to validate output creation. The workflow is:

- Check the indexer for success or failure messages. Connection or quota errors appear here.
- Check the index for searchable content. Use Search Explorer to run queries.
- Check the skillset to learn how your content is chunked and optionally vectorized.
- Check the data source for connection details. Our example uses API keys for simplicity, but you can use Microsoft Entra ID for authentication and role-based access control for authorization.

## Assign to a knowledge base

If you're satisfied with the knowledge source, continue to the next step: specify the knowledge source in a [knowledge base](search-agentic-retrieval-how-to-create).

For any knowledge base that specifies an indexed SharePoint knowledge source, be sure to set `includeReferenceSourceData`

to `true`

. This step is necessary for pulling the source document URL into the citation.

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

Use an *indexed SharePoint knowledge source* to index and query SharePoint content in an agentic retrieval pipeline. [Knowledge sources](agentic-knowledge-source-overview) are created independently, referenced in a [knowledge base](agentic-retrieval-how-to-create-knowledge-base), and used as grounding data when an agent or chatbot calls a [retrieve action](agentic-retrieval-how-to-retrieve) at query time.

When you create an indexed SharePoint knowledge source, you specify a SharePoint connection string, models, and properties to automatically generate the following Azure AI Search objects:

- A data source that points to SharePoint sites.
- A skillset that chunks and optionally vectorizes multimodal content.
- An index that stores enriched content and meets the criteria for agentic retrieval.
- An indexer that uses the previous objects to drive the indexing and enrichment pipeline.

## Prerequisites

Azure AI Search in any

[region that provides agentic retrieval](search-region-support). You must have[semantic ranker enabled](semantic-how-to-enable-disable).Completion of the

[SharePoint indexer prerequisites](search-how-to-index-sharepoint-online#prerequisites).Completion of three SharePoint indexer configuration steps:

The latest preview version of the

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


The following JSON is an example response for an indexed SharePoint knowledge source.

```
{
"name": "my-indexed-sharepoint-ks",
"kind": "indexedSharePoint",
"description": "A sample indexed SharePoint knowledge source",
"encryptionKey": null,
"indexedSharePointParameters": {
"connectionString": "<redacted>",
"containerName": "defaultSiteLibrary",
"query": null,
"ingestionParameters": {
"disableImageVerbalization": false,
"ingestionPermissionOptions": [],
"contentExtractionMode": "minimal",
"identity": null,
"embeddingModel": {
"kind": "azureOpenAI",
"azureOpenAIParameters": {
"resourceUri": "<redacted>",
"deploymentId": "text-embedding-3-large",
"apiKey": "<redacted>",
"modelName": "text-embedding-3-large",
"authIdentity": null
}
},
"chatCompletionModel": null,
"ingestionSchedule": null,
"assetStore": null,
"aiServices": null
},
"createdResources": {
"datasource": "my-indexed-sharepoint-ks-datasource",
"indexer": "my-indexed-sharepoint-ks-indexer",
"skillset": "my-indexed-sharepoint-ks-skillset",
"index": "my-indexed-sharepoint-ks-index"
}
},
"indexedOneLakeParameters": null
}
```


Note

Sensitive information is redacted. The generated resources appear at the end of the response.

## Create a knowledge source

Run the following code to create an indexed SharePoint knowledge source.

```
# Create an indexed SharePoint knowledge source
from azure.core.credentials import AzureKeyCredential
from azure.search.documents.indexes import SearchIndexClient
from azure.search.documents.indexes.models import IndexedSharePointKnowledgeSource, IndexedSharePointKnowledgeSourceParameters, KnowledgeBaseAzureOpenAIModel, AzureOpenAIVectorizerParameters, KnowledgeSourceAzureOpenAIVectorizer, KnowledgeSourceContentExtractionMode, KnowledgeSourceIngestionParameters
index_client = SearchIndexClient(endpoint = "search_url", credential = AzureKeyCredential("api_key"))
knowledge_source = IndexedSharePointKnowledgeSource(
name = "my-indexed-sharepoint-ks",
description = "A sample indexed SharePoint knowledge source.",
encryption_key = None,
indexed_share_point_parameters = IndexedSharePointKnowledgeSourceParameters(
connection_string = "connection_string",
container_name = "defaultSiteLibrary",
query = None,
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

You can pass the following properties to create an indexed SharePoint knowledge source.

| Name | Description | Type | Editable | Required |
|---|---|---|---|---|
`name` |
The name of the knowledge source, which must be unique within the knowledge sources collection and follow the
|

`description`

`encryption_key`

[customer-managed key](search-security-manage-encryption-keys)to encrypt sensitive information in both the knowledge source and the generated objects.`indexed_share_point_parameters`

`connection_string`

, `container_name`

, and `query`

.`connection_string`

[Connection string syntax](search-how-to-index-sharepoint-online#connection-string-format).`container_name`

`defaultSiteLibrary`

to index content from the site's default document library or `allSiteLibraries`

to index content from every document library in the site. Ignore `useQuery`

for now.`query`

[query](search-how-to-index-sharepoint-online#query)to filter SharePoint content.`ingestion_parameters`

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

When you create an indexed SharePoint knowledge source, your search service also creates an indexer, index, skillset, and data source. We don't recommend that you edit these objects, as introducing an error or incompatibility can break the pipeline.

After you create a knowledge source, the response lists the created objects. These objects are created according to a fixed template, and their names are based on the name of the knowledge source. You can't change the object names.

We recommend using the Azure portal to validate output creation. The workflow is:

- Check the indexer for success or failure messages. Connection or quota errors appear here.
- Check the index for searchable content. Use Search Explorer to run queries.
- Check the skillset to learn how your content is chunked and optionally vectorized.
- Check the data source for connection details. Our example uses API keys for simplicity, but you can use Microsoft Entra ID for authentication and role-based access control for authorization.

## Assign to a knowledge base

If you're satisfied with the knowledge source, continue to the next step: specify the knowledge source in a [knowledge base](search-agentic-retrieval-how-to-create).

For any knowledge base that specifies an indexed SharePoint knowledge source, be sure to set `includeReferenceSourceData`

to `true`

. This step is necessary for pulling the source document URL into the citation.

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

Use an *indexed SharePoint knowledge source* to index and query SharePoint content in an agentic retrieval pipeline. [Knowledge sources](agentic-knowledge-source-overview) are created independently, referenced in a [knowledge base](agentic-retrieval-how-to-create-knowledge-base), and used as grounding data when an agent or chatbot calls a [retrieve action](agentic-retrieval-how-to-retrieve) at query time.

When you create an indexed SharePoint knowledge source, you specify a SharePoint connection string, models, and properties to automatically generate the following Azure AI Search objects:

- A data source that points to SharePoint sites.
- A skillset that chunks and optionally vectorizes multimodal content.
- An index that stores enriched content and meets the criteria for agentic retrieval.
- An indexer that uses the previous objects to drive the indexing and enrichment pipeline.

## Prerequisites

Azure AI Search in any

[region that provides agentic retrieval](search-region-support). You must have[semantic ranker enabled](semantic-how-to-enable-disable).Completion of the

[SharePoint indexer prerequisites](search-how-to-index-sharepoint-online#prerequisites).Completion of three SharePoint indexer configuration steps:

The

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


The following JSON is an example response for an indexed SharePoint knowledge source.

```
{
"name": "my-indexed-sharepoint-ks",
"kind": "indexedSharePoint",
"description": "A sample indexed SharePoint knowledge source",
"encryptionKey": null,
"indexedSharePointParameters": {
"connectionString": "<redacted>",
"containerName": "defaultSiteLibrary",
"query": null,
"ingestionParameters": {
"disableImageVerbalization": false,
"ingestionPermissionOptions": [],
"contentExtractionMode": "minimal",
"identity": null,
"embeddingModel": {
"kind": "azureOpenAI",
"azureOpenAIParameters": {
"resourceUri": "<redacted>",
"deploymentId": "text-embedding-3-large",
"apiKey": "<redacted>",
"modelName": "text-embedding-3-large",
"authIdentity": null
}
},
"chatCompletionModel": null,
"ingestionSchedule": null,
"assetStore": null,
"aiServices": null
},
"createdResources": {
"datasource": "my-indexed-sharepoint-ks-datasource",
"indexer": "my-indexed-sharepoint-ks-indexer",
"skillset": "my-indexed-sharepoint-ks-skillset",
"index": "my-indexed-sharepoint-ks-index"
}
},
"indexedOneLakeParameters": null
}
```


Note

Sensitive information is redacted. The generated resources appear at the end of the response.

## Create a knowledge source

Use [Knowledge Sources - Create or Update (REST API)](/en-us/rest/api/searchservice/knowledge-sources/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true) to create an indexed SharePoint knowledge source.

```
POST {{search-url}}/knowledgesources/my-indexed-sharepoint-ks?api-version=2025-11-01-preview
api-key: {{api-key}}
Content-Type: application/json
{
"name": "my-indexed-sharepoint-ks",
"kind": "indexedSharePoint",
"description": "A sample indexed SharePoint knowledge source.",
"encryptionKey": null,
"indexedSharePointParameters": {
"connectionString": "{{sharepoint-connection-string}}",
"containerName": "defaultSiteLibrary",
"query": null,
"ingestionParameters": {
"identity": null,
"embeddingModel": {
"kind": "azureOpenAI",
"azureOpenAIParameters": {
"deploymentId": "text-embedding-3-large",
"modelName": "text-embedding-3-large",
"resourceUri": "{{aoai-endpoint}}",
"apiKey": "{{aoai-key}}"
}
},
"chatCompletionModel": null,
"disableImageVerbalization": false,
"ingestionSchedule": null,
"ingestionPermissionOptions": [],
"contentExtractionMode": "minimal"
}
}
}
```


### Source-specific properties

You can pass the following properties to create an indexed SharePoint knowledge source.

| Name | Description | Type | Editable | Required |
|---|---|---|---|---|
`name` |
The name of the knowledge source, which must be unique within the knowledge sources collection and follow the
|

`kind`

`indexedSharePoint`

in this case.`description`

`encryptionKey`

[customer-managed key](search-security-manage-encryption-keys)to encrypt sensitive information in both the knowledge source and the generated objects.`indexedSharePointParameters`

`connectionString`

, `containerName`

, and `query`

.`connectionString`

[Connection string syntax](search-how-to-index-sharepoint-online#connection-string-format).`container_name`

`defaultSiteLibrary`

to index content from the site's default document library or `allSiteLibraries`

to index content from every document library in the site. Ignore `useQuery`

for now.`query`

[query](search-how-to-index-sharepoint-online#query)to filter SharePoint content.`ingestionParameters`

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

When you create an indexed SharePoint knowledge source, your search service also creates an indexer, index, skillset, and data source. We don't recommend that you edit these objects, as introducing an error or incompatibility can break the pipeline.

After you create a knowledge source, the response lists the created objects. These objects are created according to a fixed template, and their names are based on the name of the knowledge source. You can't change the object names.

We recommend using the Azure portal to validate output creation. The workflow is:

- Check the indexer for success or failure messages. Connection or quota errors appear here.
- Check the index for searchable content. Use Search Explorer to run queries.
- Check the skillset to learn how your content is chunked and optionally vectorized.
- Check the data source for connection details. Our example uses API keys for simplicity, but you can use Microsoft Entra ID for authentication and role-based access control for authorization.

## Assign to a knowledge base

If you're satisfied with the knowledge source, continue to the next step: specify the knowledge source in a [knowledge base](search-agentic-retrieval-how-to-create).

For any knowledge base that specifies an indexed SharePoint knowledge source, be sure to set `includeReferenceSourceData`

to `true`

. This step is necessary for pulling the source document URL into the citation.

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