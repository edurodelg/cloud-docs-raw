---
source_url: https://learn.microsoft.com/en-us/azure/search/agentic-knowledge-source-how-to-sharepoint-remote
fetched_at: 2026-01-25T02:06:22.303223
---

# Create a remote SharePoint knowledge source

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

A *remote SharePoint knowledge source* uses the [Copilot Retrieval API](/en-us/microsoft-365-copilot/extensibility/api/ai-services/retrieval/overview) to query textual content directly from SharePoint in Microsoft 365, returning results to the agentic retrieval engine for merging, ranking, and response formulation. There's no search index used by this knowledge source, and only textual content is queried.

At query time, the remote SharePoint knowledge source calls the Copilot Retrieval API on behalf of the user identity, so no connection strings are needed in the knowledge source definition. All content to which a user has access is in-scope for knowledge retrieval. To limit sites or constrain search, set a [filter expression](/en-us/sharepoint/dev/general-development/keyword-query-language-kql-syntax-reference). Your Azure tenant and the Microsoft 365 tenant must use the same Microsoft Entra ID tenant, and the caller's identity must be recognized by both tenants.

You can use filters to scope search by URLs, date ranges, file types, and other metadata.

SharePoint permissions and Purview labels are honored in requests for content.

Usage is billed through Microsoft 365 and a Copilot license.


Like any other knowledge source, you specify a remote SharePoint knowledge source in a [knowledge base](agentic-retrieval-how-to-create-knowledge-base) and use the results as grounding data when an agent or chatbot calls a [retrieve action](agentic-retrieval-how-to-retrieve) at query time.

## Prerequisites

Azure AI Search in any

[region that provides agentic retrieval](search-region-support). You must have[semantic ranker enabled](semantic-how-to-enable-disable).SharePoint in a Microsoft 365 tenant that's under the same Microsoft Entra ID tenant as Azure.

A personal access token for local development or a user's identity from a client application.

The latest preview version of the

for the .NET SDK.`Azure.Search.Documents`

client libraryPermission to create and use objects on Azure AI Search. We recommend

[role-based access](search-security-rbac), but you can use[API keys](search-security-api-keys)if a role assignment isn't feasible.

For local development, the agentic retrieval engine uses your access token to call SharePoint on your behalf. For more information about using a personal access token on requests, see [Connect to Azure AI Search](search-get-started-rbac).

## Limitations

The following limitations in the [Copilot Retrieval API](/en-us/microsoft-365-copilot/extensibility/api/ai-services/retrieval/overview) apply to remote SharePoint knowledge sources.

There's no support for Copilot connectors or OneDrive content. Content is retrieved from SharePoint sites only.

Limit of 200 requests per user per hour.

Query character limit of 1,500 characters.

Hybrid queries are only supported for the following file extensions: .doc, .docx, .pptx, .pdf, .aspx, and .one.

Multimodal retrieval (nontextual content, including tables, images, and charts) isn't supported.

Maximum of 25 results from a query.

Results are returned by Copilot Retrieval API as unordered.

Invalid Keyword Query Language (KQL) filter expressions are ignored and the query continues to execute without the filter.


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


The following JSON is an example response for a remote SharePoint knowledge source.

```
{
"name": "my-sharepoint-ks",
"kind": "remoteSharePoint",
"description": "A sample remote SharePoint knowledge source",
"encryptionKey": null,
"remoteSharePointParameters": {
"filterExpression": "filetype:docx",
"containerTypeId": null,
"resourceMetadata": [
"Author",
"Title"
]
}
}
```


## Create a knowledge source

Run the following code to create a remote SharePoint knowledge source.

[API keys](search-security-api-keys) are used for your client connection to Azure AI Search and Azure OpenAI. Your access token is used by Azure AI Search to connect to SharePoint in Microsoft 365 on your behalf. You can only retrieve content that you're permitted to access. For more information about getting a personal access token and other values, see [Connect to Azure AI Search](search-get-started-rbac).

Note

You can also use your personal access token to access Azure AI Search and Azure OpenAI if you [set up role assignments on each resource](search-security-rbac). Using API keys allows you to omit this step in this example.

```
// Create a remote SharePoint knowledge source
using Azure.Search.Documents.Indexes;
using Azure.Search.Documents.Indexes.Models;
using Azure.Search.Documents.KnowledgeBases.Models;
using Azure;
var indexClient = new SearchIndexClient(new Uri(searchEndpoint), credential);
var knowledgeSource = new RemoteSharePointKnowledgeSource(name: "my-remote-sharepoint-ks")
{
Description = "This knowledge source queries .docx files in a trusted Microsoft 365 tenant.",
RemoteSharePointParameters = new RemoteSharePointKnowledgeSourceParameters()
{
FilterExpression = "filetype:docx",
ResourceMetadata = { "Author", "Title" }
}
};
await indexClient.CreateOrUpdateKnowledgeSourceAsync(knowledgeSource);
Console.WriteLine($"Knowledge source '{knowledgeSource.Name}' created or updated successfully.");
```


### Source-specific properties

You can pass the following properties to create a remote SharePoint knowledge source.

| Name | Description | Type | Editable | Required |
|---|---|---|---|---|
`name` |
The name of the knowledge source, which must be unique within the knowledge sources collection and follow the
|

`description`

`encryptionKey`

[customer-managed key](search-security-manage-encryption-keys)to encrypt sensitive information in the knowledge source.`remoteSharePointParameters`

`filterExpression`

, `resourceMetadata`

, and `containerTypeId`

.`filterExpression`

[KQL](/en-us/sharepoint/dev/general-development/keyword-query-language-kql-syntax-reference), which is used to specify sites and paths to content.`resourceMetadata`

`containerTypeId`

### Filter expression examples

Not all SharePoint properties are supported in the `filterExpression`

. For a list of supported properties, see the [API reference](/en-us/microsoft-365-copilot/extensibility/api/ai-services/retrieval/copilotroot-retrieval). Here's some more information about queryable properties that you can use in filter: [queryable properties](/en-us/graph/connecting-external-content-manage-schema#queryable).

Learn more about [KQL filters](/en-us/microsoft-365-copilot/extensibility/api/ai-services/retrieval/copilotroot-retrieval?pivots=graph-v1#example-7-use-filter-expressions) in the syntax reference.

| Example | Filter expression |
|---|---|
| Filter to a single site by ID | `"filterExpression": "SiteID:\"00aa00aa-bb11-cc22-dd33-44ee44ee44ee\""` |
| Filter to multiple sites by ID | `"filterExpression": "SiteID:\"00aa00aa-bb11-cc22-dd33-44ee44ee44ee\" OR SiteID:\"11bb11bb-cc22-dd33-ee44-55ff55ff55ff\""` |
| Filter to files under a specific path | `"filterExpression": "Path:\"https://my-demo.sharepoint.com/sites/mysite/Shared Documents/en/mydocs\""` |
| Filter to a specific date range | `"filterExpression": "LastModifiedTime >= 2024-07-22 AND LastModifiedTime <= 2025-01-08"` |
| Filter to files of a specific file type | `"filterExpression": "FileExtension:\"docx\" OR FileExtension:\"pdf\" OR FileExtension:\"pptx\""` |
| Filter to files of a specific information protection label | `"filterExpression": "InformationProtectionLabelId:\"f0ddcc93-d3c0-4993-b5cc-76b0a283e252\""` |

## Assign to a knowledge base

If you're satisfied with the knowledge source, continue to the next step: specify the knowledge source in a [knowledge base](search-agentic-retrieval-how-to-create).

After the knowledge base is configured, use the [retrieve action](agentic-retrieval-how-to-retrieve) to query the knowledge source.

## Query a knowledge base

The [retrieve action](agentic-retrieval-how-to-retrieve) on the knowledge base provides the user identity that authorizes access to content in Microsoft 365.

Azure AI Search uses the access token to call the Copilot Retrieval API on behalf of the user identity. The access token is provided in the retrieve endpoint as a `xMsQuerySourceAuthorization`

HTTP header.

```
using Azure;
using Azure.Search.Documents.KnowledgeBases;
using Azure.Search.Documents.KnowledgeBases.Models;
// Get access token
var credential = new DefaultAzureCredential();
var tokenRequestContext = new Azure.Core.TokenRequestContext(new[] { "https://search.azure.com/.default" });
var accessToken = await credential.GetTokenAsync(tokenRequestContext);
string token = accessToken.Token;
// Create knowledge base retrieval client
var baseClient = new KnowledgeBaseRetrievalClient(
endpoint: new Uri(searchEndpoint),
knowledgeBaseName: knowledgeBaseName,
credential: new AzureKeyCredential()
);
var spMessages = new List<Dictionary<string, string>>
{
new Dictionary<string, string>
{
{ "role", "user" },
{ "content", @"contoso product planning" }
}
};
// Create retrieval request
var retrievalRequest = new KnowledgeBaseRetrievalRequest();
foreach (Dictionary<string, string> message in spMessages) {
if (message["role"] != "system") {
retrievalRequest.Messages.Add(new KnowledgeBaseMessage(content: new[] { new KnowledgeBaseMessageTextContent(message["content"]) }) { Role = message["role"] });
}
}
retrievalRequest.RetrievalReasoningEffort = new KnowledgeRetrievalLowReasoningEffort();
var retrievalResult = await baseClient.RetrieveAsync(retrievalRequest, xMsQuerySourceAuthorization: token);
Console.WriteLine((retrievalResult.Value.Response[0].Content[0] as KnowledgeBaseMessageTextContent).Text);
```


The response might look like the following:

`Contoso's product planning for the NextGen Camera includes a 2019 launch with a core package design and minor modifications for three product versions, featuring Wi-Fi enabled technology and a new mobile app for photo organization and sharing, aiming for 100,000 users within six months [ref_id:0][ref_id:1]. Research and forecasting are central to their planning, with phase two research focusing on feedback from a diverse user group to shape deliverables and milestones [ref_id:0][ref_id:1].`


The retrieve request also takes a [KQL filter](/en-us/microsoft-365-copilot/extensibility/api/ai-services/retrieval/copilotroot-retrieval?pivots=graph-v1#example-7-use-filter-expressions) (`filterExpressionAddOn`

) if you want to apply constraints at query time. If you specify `filterExpressionAddOn`

on both the knowledge source and knowledge base retrieve action, the filters are AND'd together.

Queries asking questions about the content itself are more effective than questions about where a file is located or when it was last updated. For example, if you ask, "Where is the keynote doc for Ignite 2024", you might get "No relevant content was found for your query" because the content itself doesn't disclose its location. A filter on metadata is a better solution for file location or date-specific queries.

A better question to ask is, "What is the keynote doc for Ignite 2024". The response includes the synthesized answer, query activity and token counts, plus the URL and other metadata.

```
{
"resourceMetadata": {
"Author": "Nuwan Amarathunga;Nurul Izzati",
"Title": "Ignite 2024 Keynote Address"
}
},
"rerankerScore": 2.489522,
"webUrl": "https://contoso-my.sharepoint.com/keynotes/nuamarth_contoso_com/Documents/Keynote-Ignite-2024.docx",
"searchSensitivityLabelInfo": {
"displayName": "Confidential\\Contoso Extended",
"sensitivityLabelId": "aaaaaaaa-0b0b-1c1c-2d2d-333333333333",
"tooltip": "Data is classified and protected. Contoso Full Time Employees (FTE) and non-employees can edit, reply, forward and print. Recipient can unprotect content with the right justification.",
"priority": 5,
"color": "#FF8C00",
"isEncrypted": true
}
```


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

A *remote SharePoint knowledge source* uses the [Copilot Retrieval API](/en-us/microsoft-365-copilot/extensibility/api/ai-services/retrieval/overview) to query textual content directly from SharePoint in Microsoft 365, returning results to the agentic retrieval engine for merging, ranking, and response formulation. There's no search index used by this knowledge source, and only textual content is queried.

At query time, the remote SharePoint knowledge source calls the Copilot Retrieval API on behalf of the user identity, so no connection strings are needed in the knowledge source definition. All content to which a user has access is in-scope for knowledge retrieval. To limit sites or constrain search, set a [filter expression](/en-us/sharepoint/dev/general-development/keyword-query-language-kql-syntax-reference). Your Azure tenant and the Microsoft 365 tenant must use the same Microsoft Entra ID tenant, and the caller's identity must be recognized by both tenants.

You can use filters to scope search by URLs, date ranges, file types, and other metadata.

SharePoint permissions and Purview labels are honored in requests for content.

Usage is billed through Microsoft 365 and a Copilot license.


Like any other knowledge source, you specify a remote SharePoint knowledge source in a [knowledge base](agentic-retrieval-how-to-create-knowledge-base) and use the results as grounding data when an agent or chatbot calls a [retrieve action](agentic-retrieval-how-to-retrieve) at query time.

## Prerequisites

Azure AI Search in any

[region that provides agentic retrieval](search-region-support). You must have[semantic ranker enabled](semantic-how-to-enable-disable).SharePoint in a Microsoft 365 tenant that's under the same Microsoft Entra ID tenant as Azure.

A personal access token for local development or a user's identity from a client application.

The latest preview version of the

for Python.`azure-search-documents`

client libraryPermission to create and use objects on Azure AI Search. We recommend

[role-based access](search-security-rbac), but you can use[API keys](search-security-api-keys)if a role assignment isn't feasible.

For local development, the agentic retrieval engine uses your access token to call SharePoint on your behalf. For more information about using a personal access token on requests, see [Connect to Azure AI Search](search-get-started-rbac).

## Limitations

The following limitations in the [Copilot Retrieval API](/en-us/microsoft-365-copilot/extensibility/api/ai-services/retrieval/overview) apply to remote SharePoint knowledge sources.

There's no support for Copilot connectors or OneDrive content. Content is retrieved from SharePoint sites only.

Limit of 200 requests per user per hour.

Query character limit of 1,500 characters.

Hybrid queries are only supported for the following file extensions: .doc, .docx, .pptx, .pdf, .aspx, and .one.

Multimodal retrieval (nontextual content, including tables, images, and charts) isn't supported.

Maximum of 25 results from a query.

Results are returned by Copilot Retrieval API as unordered.

Invalid Keyword Query Language (KQL) filter expressions are ignored and the query continues to execute without the filter.


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


The following JSON is an example response for a remote SharePoint knowledge source.

```
{
"name": "my-sharepoint-ks",
"kind": "remoteSharePoint",
"description": "A sample remote SharePoint knowledge source",
"encryptionKey": null,
"remoteSharePointParameters": {
"filterExpression": "filetype:docx",
"containerTypeId": null,
"resourceMetadata": [
"Author",
"Title"
]
}
}
```


## Create a knowledge source

Run the following code to create a remote SharePoint knowledge source.

[API keys](search-security-api-keys) are used for your client connection to Azure AI Search and Azure OpenAI. Your access token is used by Azure AI Search to connect to SharePoint in Microsoft 365 on your behalf. You can only retrieve content that you're permitted to access. For more information about getting a personal access token and other values, see [Connect to Azure AI Search](search-get-started-rbac).

Note

You can also use your personal access token to access Azure AI Search and Azure OpenAI if you [set up role assignments on each resource](search-security-rbac). Using API keys allows you to omit this step in this example.

```
# Create a remote SharePoint knowledge source
from azure.core.credentials import AzureKeyCredential
from azure.search.documents.indexes import SearchIndexClient
from azure.search.documents.indexes.models import RemoteSharePointKnowledgeSource, RemoteSharePointKnowledgeSourceParameters
index_client = SearchIndexClient(endpoint = "search_url", credential = AzureKeyCredential("api_key"))
knowledge_source = RemoteSharePointKnowledgeSource(
name = "my-remote-sharepoint-ks",
description= "This knowledge source queries .docx files in a trusted Microsoft 365 tenant.",
encryption_key = None,
remote_share_point_parameters = RemoteSharePointKnowledgeSourceParameters(
filter_expression = "filetype:docx",
resource_metadata = ["Author", "Title"],
container_type_id = None
)
)
index_client.create_or_update_knowledge_source(knowledge_source)
print(f"Knowledge source '{knowledge_source.name}' created or updated successfully.")
```


### Source-specific properties

You can pass the following properties to create a remote SharePoint knowledge source.

| Name | Description | Type | Editable | Required |
|---|---|---|---|---|
`name` |
The name of the knowledge source, which must be unique within the knowledge sources collection and follow the
|

`description`

`encryption_key`

[customer-managed key](search-security-manage-encryption-keys)to encrypt sensitive information in the knowledge source.`remote_share_point_parameters`

`filter_expression`

, `resource_metadata`

, and `container_type_id`

.`filter_expression`

[KQL](/en-us/sharepoint/dev/general-development/keyword-query-language-kql-syntax-reference), which is used to specify sites and paths to content.`resource_metadata`

`container_type_id`

### Filter expression examples

Not all SharePoint properties are supported in the `filterExpression`

. For a list of supported properties, see the [API reference](/en-us/microsoft-365-copilot/extensibility/api/ai-services/retrieval/copilotroot-retrieval). Here's some more information about queryable properties that you can use in filter: [queryable properties](/en-us/graph/connecting-external-content-manage-schema#queryable).

Learn more about [KQL filters](/en-us/microsoft-365-copilot/extensibility/api/ai-services/retrieval/copilotroot-retrieval?pivots=graph-v1#example-7-use-filter-expressions) in the syntax reference.

| Example | Filter expression |
|---|---|
| Filter to a single site by ID | `"filterExpression": "SiteID:\"00aa00aa-bb11-cc22-dd33-44ee44ee44ee\""` |
| Filter to multiple sites by ID | `"filterExpression": "SiteID:\"00aa00aa-bb11-cc22-dd33-44ee44ee44ee\" OR SiteID:\"11bb11bb-cc22-dd33-ee44-55ff55ff55ff\""` |
| Filter to files under a specific path | `"filterExpression": "Path:\"https://my-demo.sharepoint.com/sites/mysite/Shared Documents/en/mydocs\""` |
| Filter to a specific date range | `"filterExpression": "LastModifiedTime >= 2024-07-22 AND LastModifiedTime <= 2025-01-08"` |
| Filter to files of a specific file type | `"filterExpression": "FileExtension:\"docx\" OR FileExtension:\"pdf\" OR FileExtension:\"pptx\""` |
| Filter to files of a specific information protection label | `"filterExpression": "InformationProtectionLabelId:\"f0ddcc93-d3c0-4993-b5cc-76b0a283e252\""` |

## Assign to a knowledge base

If you're satisfied with the knowledge source, continue to the next step: specify the knowledge source in a [knowledge base](search-agentic-retrieval-how-to-create).

After the knowledge base is configured, use the [retrieve action](agentic-retrieval-how-to-retrieve) to query the knowledge source.

## Query a knowledge base

The [retrieve action](agentic-retrieval-how-to-retrieve) on the knowledge base provides the user identity that authorizes access to content in Microsoft 365.

Azure AI Search uses the access token to call the Copilot Retrieval API on behalf of the user identity. The access token is provided in the retrieve endpoint as a `x-ms-query-source-authorization`

HTTP header.

```
from azure.identity import DefaultAzureCredential, get_bearer_token_provider
from azure.core.credentials import AzureKeyCredential
from azure.search.documents.knowledgebases import KnowledgeBaseRetrievalClient
from azure.search.documents.knowledgebases.models import KnowledgeBaseMessage, KnowledgeBaseMessageTextContent, KnowledgeBaseRetrievalRequest, RemoteSharePointKnowledgeSourceParams
# Get access token
identity_token_provider = get_bearer_token_provider(DefaultAzureCredential(), "https://search.azure.com/.default")
token = identity_token_provider()
# Create knowledge base retrieval client
kb_client = KnowledgeBaseRetrievalClient(endpoint = "search_url", knowledge_base_name = "knowledge_base_name", credential = AzureKeyCredential("api_key"))
# Create retrieval request
request = KnowledgeBaseRetrievalRequest(
include_activity = True,
messages = [
KnowledgeBaseMessage(role = "user", content = [KnowledgeBaseMessageTextContent(text = "What was covered in the keynote doc for Ignite 2024?")])
],
knowledge_source_params = [
RemoteSharePointKnowledgeSourceParams(
knowledge_source_name = "my-remote-sharepoint-ks",
filter_expression_add_on = "ModifiedBy:\"Adele Vance\"",
include_references = True,
include_reference_source_data = True
)
]
)
# Pass access token to retrieve from knowledge base
result = kb_client.retrieve(retrieval_request = request, x_ms_query_source_authorization = token)
print(result.response[0].content[0].text)
```


The retrieve request also takes a [KQL filter](/en-us/microsoft-365-copilot/extensibility/api/ai-services/retrieval/copilotroot-retrieval?pivots=graph-v1#example-7-use-filter-expressions) (`filter_expression_add_on`

) if you want to apply constraints at query time. If you specify `filter_expression_add_on`

on both the knowledge source and knowledge base retrieve action, the filters are AND'd together.

Queries asking questions about the content itself are more effective than questions about where a file is located or when it was last updated. For example, if you ask, "Where is the keynote doc for Ignite 2024", you might get "No relevant content was found for your query" because the content itself doesn't disclose its location. A filter on metadata is a better solution for file location or date-specific queries.

A better question to ask is, "What is the keynote doc for Ignite 2024". The response includes the synthesized answer, query activity and token counts, plus the URL and other metadata.

```
{
"resourceMetadata": {
"Author": "Nuwan Amarathunga;Nurul Izzati",
"Title": "Ignite 2024 Keynote Address"
}
},
"rerankerScore": 2.489522,
"webUrl": "https://contoso-my.sharepoint.com/keynotes/nuamarth_contoso_com/Documents/Keynote-Ignite-2024.docx",
"searchSensitivityLabelInfo": {
"displayName": "Confidential\\Contoso Extended",
"sensitivityLabelId": "aaaaaaaa-0b0b-1c1c-2d2d-333333333333",
"tooltip": "Data is classified and protected. Contoso Full Time Employees (FTE) and non-employees can edit, reply, forward and print. Recipient can unprotect content with the right justification.",
"priority": 5,
"color": "#FF8C00",
"isEncrypted": true
}
```


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

A *remote SharePoint knowledge source* uses the [Copilot Retrieval API](/en-us/microsoft-365-copilot/extensibility/api/ai-services/retrieval/overview) to query textual content directly from SharePoint in Microsoft 365, returning results to the agentic retrieval engine for merging, ranking, and response formulation. There's no search index used by this knowledge source, and only textual content is queried.

At query time, the remote SharePoint knowledge source calls the Copilot Retrieval API on behalf of the user identity, so no connection strings are needed in the knowledge source definition. All content to which a user has access is in-scope for knowledge retrieval. To limit sites or constrain search, set a [filter expression](/en-us/sharepoint/dev/general-development/keyword-query-language-kql-syntax-reference). Your Azure tenant and the Microsoft 365 tenant must use the same Microsoft Entra ID tenant, and the caller's identity must be recognized by both tenants.

You can use filters to scope search by URLs, date ranges, file types, and other metadata.

SharePoint permissions and Purview labels are honored in requests for content.

Usage is billed through Microsoft 365 and a Copilot license.


Like any other knowledge source, you specify a remote SharePoint knowledge source in a [knowledge base](agentic-retrieval-how-to-create-knowledge-base) and use the results as grounding data when an agent or chatbot calls a [retrieve action](agentic-retrieval-how-to-retrieve) at query time.

## Prerequisites

Azure AI Search in any

[region that provides agentic retrieval](search-region-support). You must have[semantic ranker enabled](semantic-how-to-enable-disable).SharePoint in a Microsoft 365 tenant that's under the same Microsoft Entra ID tenant as Azure.

A personal access token for local development or a user's identity from a client application.

The

[2025-11-01-preview](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2025-11-01-preview&preserve-view=true)version of the Search Service REST APIs.Permission to create and use objects on Azure AI Search. We recommend

[role-based access](search-security-rbac), but you can use[API keys](search-security-api-keys)if a role assignment isn't feasible.

For local development, the agentic retrieval engine uses your access token to call SharePoint on your behalf. For more information about using a personal access token on requests, see [Connect to Azure AI Search](search-get-started-rbac).

## Limitations

The following limitations in the [Copilot Retrieval API](/en-us/microsoft-365-copilot/extensibility/api/ai-services/retrieval/overview) apply to remote SharePoint knowledge sources.

There's no support for Copilot connectors or OneDrive content. Content is retrieved from SharePoint sites only.

Limit of 200 requests per user per hour.

Query character limit of 1,500 characters.

Hybrid queries are only supported for the following file extensions: .doc, .docx, .pptx, .pdf, .aspx, and .one.

Multimodal retrieval (nontextual content, including tables, images, and charts) isn't supported.

Maximum of 25 results from a query.

Results are returned by Copilot Retrieval API as unordered.

Invalid Keyword Query Language (KQL) filter expressions are ignored and the query continues to execute without the filter.


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


The following JSON is an example response for a remote SharePoint knowledge source.

```
{
"name": "my-sharepoint-ks",
"kind": "remoteSharePoint",
"description": "A sample remote SharePoint knowledge source",
"encryptionKey": null,
"remoteSharePointParameters": {
"filterExpression": "filetype:docx",
"containerTypeId": null,
"resourceMetadata": [
"Author",
"Title"
]
}
}
```


## Create a knowledge source

Use [Knowledge Sources - Create or Update (REST API)](/en-us/rest/api/searchservice/knowledge-sources/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true) to create a remote SharePoint knowledge source.

[API keys](search-security-api-keys) are used for your client connection to Azure AI Search and Azure OpenAI. Your access token is used by Azure AI Search to connect to SharePoint in Microsoft 365 on your behalf. You can only retrieve content that you're permitted to access. For more information about getting a personal access token and other values, see [Connect to Azure AI Search](search-get-started-rbac).

Note

You can also use your personal access token to access Azure AI Search and Azure OpenAI if you [set up role assignments on each resource](search-security-rbac). Using API keys allows you to omit this step in this example.

```
POST {{search-url}}/knowledgesources/my-remote-sharepoint-ks?api-version=2025-11-01-preview
api-key: {{api-key}}
Content-Type: application/json
{
"name": "my-remote-sharepoint-ks",
"kind": "remoteSharePoint",
"description": "This knowledge source queries .docx files in a trusted Microsoft 365 tenant.",
"encryptionKey": null,
"remoteSharePointParameters": {
"filterExpression": "filetype:docx",
"resourceMetadata": [ "Author", "Title" ],
"containerTypeId": null
}
}
```


### Source-specific properties

You can pass the following properties to create a remote SharePoint knowledge source.

| Name | Description | Type | Editable | Required |
|---|---|---|---|---|
`name` |
The name of the knowledge source, which must be unique within the knowledge sources collection and follow the
|

`kind`

`remoteSharePoint`

in this case.`description`

`encryptionKey`

[customer-managed key](search-security-manage-encryption-keys)to encrypt sensitive information in the knowledge source.`remoteSharePointParameters`

`filterExpression`

, `resourceMetadata`

, and `containerTypeId`

.`filterExpression`

[KQL](/en-us/sharepoint/dev/general-development/keyword-query-language-kql-syntax-reference), which is used to specify sites and paths to content.`resourceMetadata`

`containerTypeId`

### Filter expression examples

Not all SharePoint properties are supported in the `filterExpression`

. For a list of supported properties, see the [API reference](/en-us/microsoft-365-copilot/extensibility/api/ai-services/retrieval/copilotroot-retrieval). Here's some more information about queryable properties that you can use in filter: [queryable properties](/en-us/graph/connecting-external-content-manage-schema#queryable).

Learn more about [KQL filters](/en-us/microsoft-365-copilot/extensibility/api/ai-services/retrieval/copilotroot-retrieval?pivots=graph-v1#example-7-use-filter-expressions) in the syntax reference.

| Example | Filter expression |
|---|---|
| Filter to a single site by ID | `"filterExpression": "SiteID:\"00aa00aa-bb11-cc22-dd33-44ee44ee44ee\""` |
| Filter to multiple sites by ID | `"filterExpression": "SiteID:\"00aa00aa-bb11-cc22-dd33-44ee44ee44ee\" OR SiteID:\"11bb11bb-cc22-dd33-ee44-55ff55ff55ff\""` |
| Filter to files under a specific path | `"filterExpression": "Path:\"https://my-demo.sharepoint.com/sites/mysite/Shared Documents/en/mydocs\""` |
| Filter to a specific date range | `"filterExpression": "LastModifiedTime >= 2024-07-22 AND LastModifiedTime <= 2025-01-08"` |
| Filter to files of a specific file type | `"filterExpression": "FileExtension:\"docx\" OR FileExtension:\"pdf\" OR FileExtension:\"pptx\""` |
| Filter to files of a specific information protection label | `"filterExpression": "InformationProtectionLabelId:\"f0ddcc93-d3c0-4993-b5cc-76b0a283e252\""` |

## Assign to a knowledge base

If you're satisfied with the knowledge source, continue to the next step: specify the knowledge source in a [knowledge base](search-agentic-retrieval-how-to-create).

After the knowledge base is configured, use the [retrieve action](agentic-retrieval-how-to-retrieve) to query the knowledge source.

## Query a knowledge base

The [retrieve action](agentic-retrieval-how-to-retrieve) on the knowledge base provides the user identity that authorizes access to content in Microsoft 365.

Azure AI Search uses the access token to call the Copilot Retrieval API on behalf of the user identity. The access token is provided in the retrieve endpoint as a `x-ms-query-source-authorization`

HTTP header.

Make sure that you [generate an access token](search-get-started-rbac?pivots=rest#get-token) for the tenant that has your search service.

```
POST {{search-url}}/knowledgebases/remote-sp-kb/retrieve?api-version={{api-version}}
api-key: {{api-key}}
Content-Type: application/json
x-ms-query-source-authorization: {{access-token}}
{
"messages": [
{
"role": "user",
"content": [
{ "type": "text", "text": "What was covered in the keynote doc for Ignite 2024?" }
]
}
],
"includeActivity": true,
"knowledgeSourceParams": [
{
"filterExpressionAddOn": "ModifiedBy:\"Adele Vance\"",
"knowledgeSourceName": "my-remote-sharepoint-ks",
"kind": "remoteSharePoint",
"includeReferences": true,
"includeReferenceSourceData": true
}
]
}
```


The retrieve request also takes a [KQL filter](/en-us/microsoft-365-copilot/extensibility/api/ai-services/retrieval/copilotroot-retrieval?pivots=graph-v1#example-7-use-filter-expressions) (`filterExpressionAddOn`

) if you want to apply constraints at query time. If you specify `filterExpressionAddOn`

on both the knowledge source and knowledge base retrieve action, the filters are AND'd together.

Queries asking questions about the content itself are more effective than questions about where a file is located or when it was last updated. For example, if you ask, "Where is the keynote doc for Ignite 2024", you might get "No relevant content was found for your query" because the content itself doesn't disclose its location. A filter on metadata is a better solution for file location or date-specific queries.

A better question to ask is, "What is the keynote doc for Ignite 2024". The response includes the synthesized answer, query activity and token counts, plus the URL and other metadata.

```
{
"resourceMetadata": {
"Author": "Nuwan Amarathunga;Nurul Izzati",
"Title": "Ignite 2024 Keynote Address"
}
},
"rerankerScore": 2.489522,
"webUrl": "https://contoso-my.sharepoint.com/keynotes/nuamarth_contoso_com/Documents/Keynote-Ignite-2024.docx",
"searchSensitivityLabelInfo": {
"displayName": "Confidential\\Contoso Extended",
"sensitivityLabelId": "aaaaaaaa-0b0b-1c1c-2d2d-333333333333",
"tooltip": "Data is classified and protected. Contoso Full Time Employees (FTE) and non-employees can edit, reply, forward and print. Recipient can unprotect content with the right justification.",
"priority": 5,
"color": "#FF8C00",
"isEncrypted": true
}
```


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