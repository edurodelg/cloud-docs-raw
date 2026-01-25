---
source_url: https://learn.microsoft.com/en-us/azure/search/agentic-knowledge-source-how-to-web
fetched_at: 2026-01-25T02:06:27.116789
---

# Create a Web Knowledge Source resource

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Web Knowledge Source, which uses Grounding with Bing Search and/or Grounding with Bing Custom Search, is a

[First Party Consumption Service](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/EAEAS)governed by the[Grounding with Bing terms of use](https://www.microsoft.com/en-us/bing/apis/grounding-legal-enterprise)and the[Microsoft Privacy Statement](https://www.microsoft.com/en-us/privacy/privacystatement).The

[Microsoft Data Protection Addendum](https://www.microsoft.com/licensing/docs/view/Microsoft-Products-and-Services-Data-Protection-Addendum-DPA)doesn't apply to data sent to Web Knowledge Source. When Customer uses Web Knowledge Source, Customer Data flows outside the Azure compliance and Geo boundary. This also means use of Web Knowledge Source waives all elevated Government Community Cloud security and compliance commitments to include data sovereignty and screened/citizenship-based support, as applicable.Use of Web Knowledge Source incurs costs; learn more about

[pricing](https://www.microsoft.com/en-us/bing/apis/grounding-pricing).Learn more about how Azure admins can

[manage access to use of Web Knowledge Source](agentic-knowledge-source-how-to-web-manage).

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

*Web Knowledge Source* enables retrieval of real-time web data from Microsoft Bing in an agentic retrieval pipeline. [Knowledge sources](agentic-knowledge-source-overview) are created independently, referenced in a [knowledge base](agentic-retrieval-how-to-create-knowledge-base), and used as grounding data when an agent or chatbot calls a [retrieve action](agentic-retrieval-how-to-retrieve) at query time.

Bing Custom Search is always the search provider for Web Knowledge Source. Although you can't specify alternative search providers or engines, you can include or exclude specific *domains*, such as [https://learn.microsoft.com](/en-us/). When no domains are specified, Web Knowledge Source has unrestricted access to the entire public internet.

Web Knowledge Source works best alongside other knowledge sources. Use Web Knowledge Source when your proprietary content doesn't provide complete, up-to-date answers or when you want to supplement results with information from a commercial search engine.

When you use Web Knowledge Source, keep the following in mind:

The response is always a single, formulated answer to the query instead of raw search results from the web.

Because Web Knowledge Source doesn't support extractive data, your knowledge base must use

[answer synthesis](agentic-retrieval-how-to-answer-synthesis)and[low or medium reasoning effort](agentic-retrieval-how-to-create-knowledge-base#create-a-knowledge-base). You also can't define answer instructions.

## Prerequisites

An Azure subscription with

[access to Web Knowledge Source](agentic-knowledge-source-how-to-web-manage). By default, access is enabled. Contact your admin if access is disabled.An Azure AI Search service in any

[region that provides agentic retrieval](search-region-support). You must have[semantic ranker enabled](semantic-how-to-enable-disable). The service must also be in an[Azure public region](search-region-support#azure-public-regions), as Web Knowledge Source isn't supported in private or sovereign clouds.The latest preview version of the

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


The following JSON is an example response for a Web Knowledge Source resource.

```
{
"WebParameters": {
"Domains": null
},
"Name": "my-web-ks",
"Description": "A sample Web Knowledge Source.",
"EncryptionKey": null,
}
```


## Create a knowledge source

Run the following code to create a Web Knowledge Source resource.

```
// Create Web Knowledge Source
// Create a Web knowledge source
using Azure.Search.Documents.Indexes;
using Azure.Search.Documents.Indexes.Models;
using Azure;
var indexClient = new SearchIndexClient(new Uri(searchEndpoint), new AzureKeyCredential(apiKey));
var knowledgeSource = new WebKnowledgeSource(name: "my-web-ks")
{
Description = "A sample Web Knowledge Source.",
WebParameters = new WebKnowledgeSourceParameters
{
Domains = new WebKnowledgeSourceDomains
{
AllowedDomains =
{
new WebKnowledgeSourceDomain(address: "learn.microsoft.com") { IncludeSubpages = true }
},
BlockedDomains =
{
new WebKnowledgeSourceDomain(address: "bing.com") { IncludeSubpages = false }
}
}
}
};
await indexClient.CreateOrUpdateKnowledgeSourceAsync(knowledgeSource);
Console.WriteLine($"Knowledge source '{knowledgeSource.Name}' created or updated successfully.");
```


### Source-specific properties

You can pass the following properties to create a Web Knowledge Source resource.

| Name | Description | Type | Editable | Required |
|---|---|---|---|---|
`Name` |
The name of the knowledge source, which must be unique within the knowledge sources collection and follow the
|

`Description`

`EncryptionKey`

[customer-managed key](search-security-manage-encryption-keys)to encrypt sensitive information in the knowledge source.`WebParameters`

`Domains`

.`Domains`

[Grounding with Bing Search](/en-us/azure/ai-foundry/agents/how-to/tools/bing-grounding)to search the entire public internet. When you specify domains, the knowledge source uses[Grounding with Bing Custom Search](/en-us/azure/ai-foundry/agents/how-to/tools/bing-custom-search)to restrict results to the specified domains. In both cases, Bing Custom Search is the search provider.`AllowedDomains`

`address`

in the `website.com`

format. You can also specify whether to include the domain's subpages by setting `IncludeSubpages`

to `true`

or `false`

.`BlockedDomains`

`address`

in the `website.com`

format. You can also specify whether to include the domain's subpages by setting `IncludeSubpages`

to `true`

or `false`

.## Assign to a knowledge base

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


Important

Web Knowledge Source, which uses Grounding with Bing Search and/or Grounding with Bing Custom Search, is a

[First Party Consumption Service](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/EAEAS)governed by the[Grounding with Bing terms of use](https://www.microsoft.com/en-us/bing/apis/grounding-legal-enterprise)and the[Microsoft Privacy Statement](https://www.microsoft.com/en-us/privacy/privacystatement).The

[Microsoft Data Protection Addendum](https://www.microsoft.com/licensing/docs/view/Microsoft-Products-and-Services-Data-Protection-Addendum-DPA)doesn't apply to data sent to Web Knowledge Source. When Customer uses Web Knowledge Source, Customer Data flows outside the Azure compliance and Geo boundary. This also means use of Web Knowledge Source waives all elevated Government Community Cloud security and compliance commitments to include data sovereignty and screened/citizenship-based support, as applicable.Use of Web Knowledge Source incurs costs; learn more about

[pricing](https://www.microsoft.com/en-us/bing/apis/grounding-pricing).Learn more about how Azure admins can

[manage access to use of Web Knowledge Source](agentic-knowledge-source-how-to-web-manage).

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

*Web Knowledge Source* enables retrieval of real-time web data from Microsoft Bing in an agentic retrieval pipeline. [Knowledge sources](agentic-knowledge-source-overview) are created independently, referenced in a [knowledge base](agentic-retrieval-how-to-create-knowledge-base), and used as grounding data when an agent or chatbot calls a [retrieve action](agentic-retrieval-how-to-retrieve) at query time.

Bing Custom Search is always the search provider for Web Knowledge Source. Although you can't specify alternative search providers or engines, you can include or exclude specific *domains*, such as [https://learn.microsoft.com](/en-us/). When no domains are specified, Web Knowledge Source has unrestricted access to the entire public internet.

Web Knowledge Source works best alongside other knowledge sources. Use Web Knowledge Source when your proprietary content doesn't provide complete, up-to-date answers or when you want to supplement results with information from a commercial search engine.

When you use Web Knowledge Source, keep the following in mind:

The response is always a single, formulated answer to the query instead of raw search results from the web.

Because Web Knowledge Source doesn't support extractive data, your knowledge base must use

[answer synthesis](agentic-retrieval-how-to-answer-synthesis)and[low or medium reasoning effort](agentic-retrieval-how-to-create-knowledge-base#create-a-knowledge-base). You also can't define answer instructions.

## Prerequisites

An Azure subscription with

[access to Web Knowledge Source](agentic-knowledge-source-how-to-web-manage). By default, access is enabled. Contact your admin if access is disabled.An Azure AI Search service in any

[region that provides agentic retrieval](search-region-support). You must have[semantic ranker enabled](semantic-how-to-enable-disable). The service must also be in an[Azure public region](search-region-support#azure-public-regions), as Web Knowledge Source isn't supported in private or sovereign clouds.The latest preview version of the

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


The following JSON is an example response for a Web Knowledge Source resource.

```
{
"name": "my-web-ks",
"kind": "web",
"description": "A sample Web Knowledge Source.",
"encryptionKey": null,
"webParameters": {
"domains": null
}
}
```


## Create a knowledge source

Run the following code to create a Web Knowledge Source resource.

```
# Create Web Knowledge Source
from azure.core.credentials import AzureKeyCredential
from azure.search.documents.indexes import SearchIndexClient
from azure.search.documents.indexes.models import WebKnowledgeSource, WebKnowledgeSourceParameters, WebKnowledgeSourceDomains
index_client = SearchIndexClient(endpoint = "search_url", credential = AzureKeyCredential("api_key"))
knowledge_source = WebKnowledgeSource(
name = "my-web-ks",
description = "A sample Web Knowledge Source.",
encryption_key = None,
web_parameters = WebKnowledgeSourceParameters(
domains = WebKnowledgeSourceDomains(
allowed_domains = [ { "address": "learn.microsoft.com", "include_subpages": True } ],
blocked_domains = [ { "address": "bing.com", "include_subpages": False } ]
)
)
)
index_client.create_or_update_knowledge_source(knowledge_source)
print(f"Knowledge source '{knowledge_source.name}' created or updated successfully.")
```


### Source-specific properties

You can pass the following properties to create a Web Knowledge Source resource.

| Name | Description | Type | Editable | Required |
|---|---|---|---|---|
`name` |
The name of the knowledge source, which must be unique within the knowledge sources collection and follow the
|

`description`

`encryption_key`

[customer-managed key](search-security-manage-encryption-keys)to encrypt sensitive information in the knowledge source.`web_parameters`

`domains`

.`domains`

[Grounding with Bing Search](/en-us/azure/ai-foundry/agents/how-to/tools/bing-grounding)to search the entire public internet. When you specify domains, the knowledge source uses[Grounding with Bing Custom Search](/en-us/azure/ai-foundry/agents/how-to/tools/bing-custom-search)to restrict results to the specified domains. In both cases, Bing Custom Search is the search provider.`allowed_domains`

`address`

in the `website.com`

format. You can also specify whether to include the domain's subpages by setting `include_subpages`

to `true`

or `false`

.`blocked_domains`

`address`

in the `website.com`

format. You can also specify whether to include the domain's subpages by setting `include_subpages`

to `true`

or `false`

.## Assign to a knowledge base

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


Important

Web Knowledge Source, which uses Grounding with Bing Search and/or Grounding with Bing Custom Search, is a

[First Party Consumption Service](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/EAEAS)governed by the[Grounding with Bing terms of use](https://www.microsoft.com/en-us/bing/apis/grounding-legal-enterprise)and the[Microsoft Privacy Statement](https://www.microsoft.com/en-us/privacy/privacystatement).The

[Microsoft Data Protection Addendum](https://www.microsoft.com/licensing/docs/view/Microsoft-Products-and-Services-Data-Protection-Addendum-DPA)doesn't apply to data sent to Web Knowledge Source. When Customer uses Web Knowledge Source, Customer Data flows outside the Azure compliance and Geo boundary. This also means use of Web Knowledge Source waives all elevated Government Community Cloud security and compliance commitments to include data sovereignty and screened/citizenship-based support, as applicable.Use of Web Knowledge Source incurs costs; learn more about

[pricing](https://www.microsoft.com/en-us/bing/apis/grounding-pricing).Learn more about how Azure admins can

[manage access to use of Web Knowledge Source](agentic-knowledge-source-how-to-web-manage).

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

*Web Knowledge Source* enables retrieval of real-time web data from Microsoft Bing in an agentic retrieval pipeline. [Knowledge sources](agentic-knowledge-source-overview) are created independently, referenced in a [knowledge base](agentic-retrieval-how-to-create-knowledge-base), and used as grounding data when an agent or chatbot calls a [retrieve action](agentic-retrieval-how-to-retrieve) at query time.

Bing Custom Search is always the search provider for Web Knowledge Source. Although you can't specify alternative search providers or engines, you can include or exclude specific *domains*, such as [https://learn.microsoft.com](/en-us/). When no domains are specified, Web Knowledge Source has unrestricted access to the entire public internet.

Web Knowledge Source works best alongside other knowledge sources. Use Web Knowledge Source when your proprietary content doesn't provide complete, up-to-date answers or when you want to supplement results with information from a commercial search engine.

When you use Web Knowledge Source, keep the following in mind:

The response is always a single, formulated answer to the query instead of raw search results from the web.

Because Web Knowledge Source doesn't support extractive data, your knowledge base must use

[answer synthesis](agentic-retrieval-how-to-answer-synthesis)and[low or medium reasoning effort](agentic-retrieval-how-to-create-knowledge-base#create-a-knowledge-base). You also can't define answer instructions.

## Prerequisites

An Azure subscription with

[access to Web Knowledge Source](agentic-knowledge-source-how-to-web-manage). By default, access is enabled. Contact your admin if access is disabled.An Azure AI Search service in any

[region that provides agentic retrieval](search-region-support). You must have[semantic ranker enabled](semantic-how-to-enable-disable). The service must also be in an[Azure public region](search-region-support#azure-public-regions), as Web Knowledge Source isn't supported in private or sovereign clouds.The

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


The following JSON is an example response for a Web Knowledge Source resource.

```
{
"name": "my-web-ks",
"kind": "web",
"description": "A sample Web Knowledge Source.",
"encryptionKey": null,
"webParameters": {
"domains": null
}
}
```


## Create a knowledge source

Use [Knowledge Sources - Create or Update (REST API)](/en-us/rest/api/searchservice/knowledge-sources/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true) to create a Web Knowledge Source resource.

```
PUT {{search-url}}/knowledgesources/my-web-ks?api-version=2025-11-01-preview
Content-Type: application/json
api-key: {{api-key}}
{
"name": "my-web-ks",
"kind": "web",
"description": "This knowledge source pulls content from the web.",
"encryptionKey": null,
"webParameters": {
"domains": {
"allowedDomains": [ { "address": "learn.microsoft.com", "includeSubpages": true } ],
"blockedDomains": [ { "address": "bing.com", "includeSubpages": false } ]
}
}
}
```


### Source-specific properties

You can pass the following properties to create a Web Knowledge Source resource.

| Name | Description | Type | Editable | Required |
|---|---|---|---|---|
`name` |
The name of the knowledge source, which must be unique within the knowledge sources collection and follow the
|

`kind`

`web`

in this case.`description`

`encryptionKey`

[customer-managed key](search-security-manage-encryption-keys)to encrypt sensitive information in the knowledge source.`webParameters`

`domains`

.`domains`

[Grounding with Bing Search](/en-us/azure/ai-foundry/agents/how-to/tools/bing-grounding)to search the entire public internet. When you specify domains, the knowledge source uses[Grounding with Bing Custom Search](/en-us/azure/ai-foundry/agents/how-to/tools/bing-custom-search)to restrict results to the specified domains. In both cases, Bing Custom Search is the search provider.`allowedDomains`

`address`

in the `website.com`

format. You can also specify whether to include the domain's subpages by setting `includeSubpages`

to `true`

or `false`

.`blockedDomains`

`address`

in the `website.com`

format. You can also specify whether to include the domain's subpages by setting `includeSubpages`

to `true`

or `false`

.## Assign to a knowledge base

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