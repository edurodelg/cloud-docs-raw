---
source_url: https://learn.microsoft.com/en-us/azure/search/agentic-knowledge-source-how-to-search-index
fetched_at: 2026-01-25T03:13:11.679755
---

# Create a search index knowledge source

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

A *search index knowledge source* specifies a connection to an Azure AI Search index that provides searchable content in an agentic retrieval pipeline. [Knowledge sources](agentic-knowledge-source-overview) are created independently, referenced in a [knowledge base](agentic-retrieval-how-to-create-knowledge-base), and used as grounding data when an agent or chatbot calls a [retrieve action](agentic-retrieval-how-to-retrieve) at query time.

## Prerequisites

Azure AI Search in any

[region that provides agentic retrieval](search-region-support). You must have[semantic ranker enabled](semantic-how-to-enable-disable).A search index containing plain text or vector content with a semantic configuration.

[Review the index criteria for agentic retrieval](agentic-retrieval-how-to-create-index#criteria-for-agentic-retrieval). The index must be on the same search service as the knowledge base.The latest preview version of the

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


The following JSON is an example response for a search index knowledge source. Notice that the knowledge source specifies a single index name and which fields in the index to include in the query.

```
{
"SearchIndexParameters": {
"SearchIndexName": "earth-at-night",
"SourceDataFields": [
{
"Name": "id"
},
{
"Name": "page_chunk"
},
{
"Name": "page_number"
}
],
"SearchFields": [],
"SemanticConfigurationName": "semantic-config"
},
"Name": "earth-knowledge-source",
"Description": null,
"EncryptionKey": null,
"ETag": "<redacted>"
}
```


## Create a knowledge source

Run the following code to create a search index knowledge source.

```
using Azure.Search.Documents.Indexes.Models;
// Create the knowledge source
var indexKnowledgeSource = new SearchIndexKnowledgeSource(
name: knowledgeSourceName,
searchIndexParameters: new SearchIndexKnowledgeSourceParameters(searchIndexName: indexName)
{
SourceDataFields = { new SearchIndexFieldReference(name: "id"), new SearchIndexFieldReference(name: "page_chunk"), new SearchIndexFieldReference(name: "page_number") }
}
);
await indexClient.CreateOrUpdateKnowledgeSourceAsync(indexKnowledgeSource);
Console.WriteLine($"Knowledge source '{knowledgeSourceName}' created or updated successfully.");
```


### Source-specific properties

You can pass the following properties to create a search index knowledge source.

| Name | Description | Type | Editable | Required |
|---|---|---|---|---|
`Name` |
The name of the knowledge source, which must be unique within the knowledge sources collection and follow the
|

`Description`

`EncryptionKey`

[customer-managed key](search-security-manage-encryption-keys)to encrypt sensitive information in both the knowledge source and the generated objects.`SearchIndexParameters`

`search_index_name`

, `SemanticConfigurationName`

, `SourceDataFields`

, and `SearchFields`

.`SearchIndexName`

`SemanticConfigurationName`

`SourceDataFields`

`include_reference_source_data`

in the knowledge base definition. These fields are used for citations and should be `retrievable`

. Examples include the document name, file name, page numbers, or chapter numbers.`SearchFields`

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

A *search index knowledge source* specifies a connection to an Azure AI Search index that provides searchable content in an agentic retrieval pipeline. [Knowledge sources](agentic-knowledge-source-overview) are created independently, referenced in a [knowledge base](agentic-retrieval-how-to-create-knowledge-base), and used as grounding data when an agent or chatbot calls a [retrieve action](agentic-retrieval-how-to-retrieve) at query time.

## Prerequisites

Azure AI Search in any

[region that provides agentic retrieval](search-region-support). You must have[semantic ranker enabled](semantic-how-to-enable-disable).A search index containing plain text or vector content with a semantic configuration.

[Review the index criteria for agentic retrieval](agentic-retrieval-how-to-create-index#criteria-for-agentic-retrieval). The index must be on the same search service as the knowledge base.The latest preview version of the

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


The following JSON is an example response for a search index knowledge source. Notice that the knowledge source specifies a single index name and which fields in the index to include in the query.

```
{
"name": "my-search-index-ks",
"kind": "searchIndex",
"description": "A sample search index knowledge source.",
"encryptionKey": null,
"searchIndexParameters": {
"searchIndexName": "my-search-index",
"semanticConfigurationName": null,
"sourceDataFields": [],
"searchFields": []
}
}
```


## Create a knowledge source

Run the following code to create a search index knowledge source.

```
# Create a search index knowledge source
from azure.core.credentials import AzureKeyCredential
from azure.search.documents.indexes import SearchIndexClient
from azure.search.documents.indexes.models import SearchIndexKnowledgeSource, SearchIndexKnowledgeSourceParameters, SearchIndexFieldReference
index_client = SearchIndexClient(endpoint = "search_url", credential = AzureKeyCredential("api_key"))
knowledge_source = SearchIndexKnowledgeSource(
name = "my-search-index-ks",
description= "This knowledge source pulls from an existing index designed for agentic retrieval.",
encryption_key = None,
search_index_parameters = SearchIndexKnowledgeSourceParameters(
search_index_name = "search_index_name",
semantic_configuration_name = "semantic_configuration_name",
source_data_fields = [
SearchIndexFieldReference(name="description"),
SearchIndexFieldReference(name="category"),
],
search_fields = [
SearchIndexFieldReference(name="id")
],
)
)
index_client.create_or_update_knowledge_source(knowledge_source)
print(f"Knowledge source '{knowledge_source.name}' created or updated successfully.")
```


### Source-specific properties

You can pass the following properties to create a search index knowledge source.

| Name | Description | Type | Editable | Required |
|---|---|---|---|---|
`name` |
The name of the knowledge source, which must be unique within the knowledge sources collection and follow the
|

`description`

`encryption_key`

[customer-managed key](search-security-manage-encryption-keys)to encrypt sensitive information in both the knowledge source and the generated objects.`search_index_parameters`

`search_index_name`

, `semantic_configuration_name`

, `source_data_fields`

, and `search_fields`

.`search_index_name`

`semantic_configuration_name`

`source_data_fields`

`include_reference_source_data`

in the knowledge base definition. These fields are used for citations and should be `retrievable`

. Examples include the document name, file name, page numbers, or chapter numbers.`search_fields`

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

A *search index knowledge source* specifies a connection to an Azure AI Search index that provides searchable content in an agentic retrieval pipeline. [Knowledge sources](agentic-knowledge-source-overview) are created independently, referenced in a [knowledge base](agentic-retrieval-how-to-create-knowledge-base), and used as grounding data when an agent or chatbot calls a [retrieve action](agentic-retrieval-how-to-retrieve) at query time.

## Prerequisites

Azure AI Search in any

[region that provides agentic retrieval](search-region-support). You must have[semantic ranker enabled](semantic-how-to-enable-disable).A search index containing plain text or vector content with a semantic configuration. Review the

[index criteria for agentic retrieval](agentic-retrieval-how-to-create-index#criteria-for-agentic-retrieval). The index must be on the same search service as the knowledge base.The

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


The following JSON is an example response for a search index knowledge source. Notice that the knowledge source specifies a single index name and which fields in the index to include in the query.

```
{
"name": "my-search-index-ks",
"kind": "searchIndex",
"description": "A sample search index knowledge source.",
"encryptionKey": null,
"searchIndexParameters": {
"searchIndexName": "my-search-index",
"semanticConfigurationName": null,
"sourceDataFields": [],
"searchFields": []
}
}
```


## Create a knowledge source

Use [Knowledge Sources - Create or Update (REST API)](/en-us/rest/api/searchservice/knowledge-sources/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true) to create a search index knowledge source.

```
POST {{search-url}}/knowledgesources/my-search-index-ks?api-version=2025-11-01-preview
api-key: {{api-key}}
Content-Type: application/json
{
"name": "my-search-index-ks",
"kind": "searchIndex",
"description": "This knowledge source pulls from an existing index designed for agentic retrieval.",
"encryptionKey": null,
"searchIndexParameters": {
"searchIndexName": "<YOUR INDEX NAME>",
"semanticConfigurationName": "my-semantic-config",
"sourceDataFields": [
{ "name": "description" },
{ "name": "category" }
],
"searchFields": [
{ "name": "*" }
]
}
}
```


### Source-specific properties

You can pass the following properties to create a search index knowledge source.

| Name | Description | Type | Editable | Required |
|---|---|---|---|---|
`name` |
The name of the knowledge source, which must be unique within the knowledge sources collection and follow the
|

`kind`

`searchIndex`

in this case.`description`

`encryptionKey`

[customer-managed key](search-security-manage-encryption-keys)to encrypt sensitive information in both the knowledge source and the generated objects.`searchIndexParameters`

`searchIndexName`

, `semanticConfigurationName`

, `sourceDataFields`

, and `searchFields`

.`searchIndexName`

`semanticConfigurationName`

`sourceDataFields`

`includeReferenceSourceData`

in the knowledge base definition. These fields are used for citations and should be `retrievable`

. Examples include the document name, file name, page numbers, or chapter numbers.`searchFields`

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