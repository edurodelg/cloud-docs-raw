---
source_url: https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-how-to-create-knowledge-base
fetched_at: 2026-01-25T03:10:23.173685
---

# Create a knowledge base in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

In Azure AI Search, a *knowledge base* is a top-level object that orchestrates [agentic retrieval](agentic-retrieval-overview). It defines which knowledge sources to query and the default behavior for retrieval operations. At query time, the [retrieve method](agentic-retrieval-how-to-retrieve) targets the knowledge base to run the configured retrieval pipeline.

You can create a knowledge base in a [Foundry IQ workload](/en-us/azure/ai-foundry/agents/how-to/tools/knowledge-retrieval) in the Microsoft Foundry (new) portal. You also need a knowledge base in any agentic solutions that you create using the Azure AI Search APIs.

A knowledge base specifies:

- One or more knowledge sources that point to searchable content.
- An optional LLM that provides reasoning capabilities for query planning and answer formulation.
- A retrieval reasoning effort that determines whether an LLM is invoked and manages cost, latency, and quality.
- Custom properties that control routing, source selection, output format, and object encryption.

After you create a knowledge base, you can update its properties at any time. If the knowledge base is in use, updates take effect on the next retrieval.

Important

2025-11-01-preview renames the 2025-08-01-preview "knowledge agent" to "knowledge base." This is a breaking change. We recommend [migrating existing code](agentic-retrieval-how-to-migrate) to the new APIs as soon as possible.

## Prerequisites

Azure AI Search in any

[region that provides agentic retrieval](search-region-support). You must have[semantic ranker enabled](semantic-how-to-enable-disable). If you're using a[managed identity](search-how-to-managed-identities)for role-based access to deployed models, your search service must be on the Basic pricing tier or higher.Azure OpenAI with a

[supported LLM](#supported-models)deployment.One or more

[knowledge sources](agentic-knowledge-source-overview#supported-knowledge-sources)on your search service.Permission to create and use objects on Azure AI Search. We recommend

[role-based access](search-security-rbac).**Search Service Contributor**can create and manage a knowledge base.**Search Index Data Reader**can run queries. Alternatively, you can use[API keys](search-security-api-keys)if a role assignment isn't feasible. For more information, see[Connect to a search service](search-get-started-rbac).The latest preview version of the

for the .NET SDK.`Azure.Search.Documents`

client library

### Supported models

Use one of the following LLMs from Azure OpenAI in Foundry Models or an equivalent open-source model. For deployment instructions, see [Deploy Microsoft Foundry Models in the Foundry portal](/en-us/azure/ai-foundry/how-to/deploy-models-openai).

`gpt-4o`

`gpt-4o-mini`

`gpt-4.1`

`gpt-4.1-nano`

`gpt-4.1-mini`

`gpt-5`

`gpt-5-nano`

`gpt-5-mini`


## Configure access

Azure AI Search needs access to the LLM from Azure OpenAI. We recommend Microsoft Entra ID for authentication and role-based access for authorization. To assign roles, you must be an **Owner or User Access Administrator**. If you can't use roles, use key-based authentication instead.

On your model provider, such as Foundry Models, assign

**Cognitive Services User**to the managed identity of your search service. If you're testing locally, assign the same role to your user account.For local testing, follow the steps in

[Quickstart: Connect without keys](search-get-started-rbac)to sign in to a specific subscription and tenant. Use`DefaultAzureCredential`

instead of`AzureKeyCredential`

in each request, which should look similar to the following example:`using Azure.Search.Documents.Indexes; using Azure.Identity; var indexClient = new SearchIndexClient(new Uri(searchEndpoint), new DefaultAzureCredential());`


Important

Code snippets in this article use API keys. If you use role-based authentication, update each request accordingly. In a request that specifies both approaches, the API key takes precedence.

## Check for existing knowledge bases

Knowing about existing knowledge bases is helpful for either reusing them or naming new objects. Any 2025-08-01-preview knowledge agents are returned in the knowledge bases collection.

Run the following code to list existing knowledge bases by name.

```
// List knowledge bases by name
using Azure.Search.Documents.Indexes;
var indexClient = new SearchIndexClient(new Uri(searchEndpoint), credential);
var knowledgeBases = indexClient.GetKnowledgeBasesAsync();
Console.WriteLine("Knowledge Bases:");
await foreach (var kb in knowledgeBases)
{
Console.WriteLine($" - {kb.Name}");
}
```


You can also return a single knowledge base by name to review its JSON definition.

```
using Azure.Search.Documents.Indexes;
using System.Text.Json;
var indexClient = new SearchIndexClient(new Uri(searchEndpoint), credential);
// Specify the knowledge base name to retrieve
string kbNameToGet = "earth-knowledge-base";
// Get a specific knowledge base definition
var knowledgeBaseResponse = await indexClient.GetKnowledgeBaseAsync(kbNameToGet);
var kb = knowledgeBaseResponse.Value;
// Serialize to JSON for display
string json = JsonSerializer.Serialize(kb, new JsonSerializerOptions { WriteIndented = true });
Console.WriteLine(json);
```


The following JSON is an example of a knowledge base.

```
{
"Name": "earth-knowledge-base",
"KnowledgeSources": [
{
"Name": "earth-knowledge-source"
}
],
"Models": [
{}
],
"RetrievalReasoningEffort": {},
"OutputMode": {},
"ETag": "\u00220x8DE278629D782B3\u0022",
"EncryptionKey": null,
"Description": null,
"RetrievalInstructions": null,
"AnswerInstructions": null
}
```


## Create a knowledge base

A knowledge base drives the agentic retrieval pipeline. In application code, other agents or chatbots call it.

A knowledge base connects knowledge sources (searchable content) to an LLM deployment from Azure OpenAI. Properties on the LLM establish the connection, while properties on the knowledge source establish defaults that inform query execution and the response.

Run the following code to create a knowledge base.

```
using Azure.Search.Documents.Indexes.Models;
using Azure.Search.Documents.KnowledgeBases.Models;
var indexClient = new SearchIndexClient(new Uri(searchEndpoint), credential);
// Create a knowledge base
var knowledgeBase = new KnowledgeBase(
name: knowledgeBaseName,
knowledgeSources: new KnowledgeSourceReference[] { new KnowledgeSourceReference(knowledgeSourceName) }
)
{
RetrievalReasoningEffort = new KnowledgeRetrievalLowReasoningEffort(),
OutputMode = KnowledgeRetrievalOutputMode.AnswerSynthesis,
Models = { model }
};
await indexClient.CreateOrUpdateKnowledgeBaseAsync(knowledgeBase);
Console.WriteLine($"Knowledge base '{knowledgeBaseName}' created or updated successfully.");
```


```
# Create a knowledge base
using Azure.Search.Documents.Indexes;
using Azure.Search.Documents.Indexes.Models;
using Azure.Search.Documents.KnowledgeBases.Models;
using Azure;
var indexClient = new SearchIndexClient(new Uri(searchEndpoint), new AzureKeyCredential(apiKey));
var aoaiParams = new AzureOpenAIVectorizerParameters
{
ResourceUri = new Uri(aoaiEndpoint),
DeploymentName = aoaiGptDeployment,
ModelName = aoaiGptModel
};
var knowledgeBase = new KnowledgeBase(
name: "my-kb",
knowledgeSources: new KnowledgeSourceReference[]
{
new KnowledgeSourceReference("hotels-sample-knowledge-source"),
new KnowledgeSourceReference("earth-knowledge-source")
}
)
{
Description = "This knowledge base handles questions directed at two unrelated sample indexes.",
RetrievalInstructions = "Use the hotels knowledge source for queries about where to stay, otherwise use the earth at night knowledge source.",
AnswerInstructions = "Provide a two sentence concise and informative answer based on the retrieved documents.",
OutputMode = KnowledgeRetrievalOutputMode.AnswerSynthesis,
Models = { new KnowledgeBaseAzureOpenAIModel(azureOpenAIParameters: aoaiParams) },
RetrievalReasoningEffort = new KnowledgeRetrievalLowReasoningEffort()
};
await indexClient.CreateOrUpdateKnowledgeBaseAsync(knowledgeBase);
Console.WriteLine($"Knowledge base '{knowledgeBase.Name}' created or updated successfully.");
```


### Knowledge base properties

Pass the following properties to create a knowledge base.

| Name | Description | Type | Required |
|---|---|---|---|
`name` |
The name of the knowledge base. It must be unique within the knowledge bases collection and follow the
|

`knowledgeSources`

[supported knowledge sources](agentic-knowledge-source-overview#supported-knowledge-sources).`Description`

`RetrievalInstructions`

`AnswerInstructions`

[Use answer synthesis for citation-backed responses](agentic-retrieval-how-to-answer-synthesis).`OutputMode`

`AnswerSynthesis`

for an LLM-formulated answer or `ExtractedData`

for full search results that you can pass to an LLM as a downstream step.`Models`

[supported LLM](#supported-models)used for answer formulation or query planning. In this preview,`Models`

can contain just one model, and the model provider must be Azure OpenAI. Obtain model information from the Foundry portal or a command-line request. Provide the parameters by using the [KnowledgeBaseAzureOpenAIModel class](/en-us/dotnet/api/azure.search.documents.indexes.models.knowledgebaseazureopenaimodel?view=azure-dotnet-preview&preserve-view=true). You can use role-based access control instead of API keys for the Azure AI Search connection to the model. For more information, see[How to deploy Azure OpenAI models with Foundry](/en-us/azure/ai-foundry/how-to/deploy-models-openai).`RetrievalReasoningEffort`

`minimal`

, `low`

(default), and `medium`

. For more information, see [Set the retrieval reasoning effort](agentic-retrieval-how-to-set-retrieval-reasoning-effort).## Query a knowledge base

Set up the instructions and messages to send to the LLM.

```
string instructions = @"
Use the earth at night index to answer the question. If you can't find relevant content, say you don't know.
";
var messages = new List<Dictionary<string, string>>
{
new Dictionary<string, string>
{
{ "role", "system" },
{ "content", instructions }
}
};
```


Call the `retrieve`

action on the knowledge base to verify the LLM connection and return results. For more information about the `retrieve`

request and response schema, see [Retrieve data using a knowledge base in Azure AI Search](agentic-retrieval-how-to-retrieve).

Replace "Where does the ocean look green?" with a query string that's valid for your knowledge sources.

```
using Azure.Search.Documents.KnowledgeBases;
using Azure.Search.Documents.KnowledgeBases.Models;
var baseClient = new KnowledgeBaseRetrievalClient(
endpoint: new Uri(searchEndpoint),
knowledgeBaseName: knowledgeBaseName,
tokenCredential: new DefaultAzureCredential()
);
messages.Add(new Dictionary<string, string>
{
{ "role", "user" },
{ "content", @"Where does the ocean look green?" }
});
var retrievalRequest = new KnowledgeBaseRetrievalRequest();
foreach (Dictionary<string, string> message in messages) {
if (message["role"] != "system") {
retrievalRequest.Messages.Add(new KnowledgeBaseMessage(content: new[] { new KnowledgeBaseMessageTextContent(message["content"]) }) { Role = message["role"] });
}
}
retrievalRequest.RetrievalReasoningEffort = new KnowledgeRetrievalLowReasoningEffort();
var retrievalResult = await baseClient.RetrieveAsync(retrievalRequest);
messages.Add(new Dictionary<string, string>
{
{ "role", "assistant" },
{ "content", (retrievalResult.Value.Response[0].Content[0] as KnowledgeBaseMessageTextContent).Text }
});
(retrievalResult.Value.Response[0].Content[0] as KnowledgeBaseMessageTextContent).Text
// Print the response, activity, and references
Console.WriteLine("Response:");
Console.WriteLine((retrievalResult.Value.Response[0].Content[0] as KnowledgeBaseMessageTextContent)!.Text);
```


**Key points:**

[KnowledgeBaseRetrievalRequest](/en-us/dotnet/api/azure.search.documents.knowledgebases.models.knowledgebaseretrievalrequest?view=azure-dotnet-preview&preserve-view=true)is the input contract for the retrieval request.[RetrievalReasoningEffort](/en-us/dotnet/api/azure.search.documents.knowledgebases.models.knowledgebaseretrievalrequest.retrievalreasoningeffort?view=azure-dotnet-preview#azure-search-documents-knowledgebases-models-knowledgebaseretrievalrequest-retrievalreasoningeffort&preserve-view=true)is required. Setting it to`minimal`

excludes LLMs from the query pipeline and only intents are used for the query input. The default is`low`

and it supports LLM-based query planning and answer synthesis with messages and context.are used to overwrite default parameters at query time.`knowledgeSourceParams`


The response to the sample query might look like the following example:

```
"response": [
{
"content": [
{
"type": "text",
"text": "The ocean appears green off the coast of Antarctica due to phytoplankton flourishing in the water, particularly in Granite Harbor near Antarctica’s Ross Sea, where they can grow in large quantities during spring, summer, and even autumn under the right conditions [ref_id:0]. Additionally, off the coast of Namibia, the ocean can also look green due to blooms of phytoplankton and yellow-green patches of sulfur precipitating from bacteria in oxygen-depleted waters [ref_id:1]. In the Strait of Georgia, Canada, the waters turned bright green due to a massive bloom of coccolithophores, a type of phytoplankton [ref_id:5]. Furthermore, a milky green and blue bloom was observed off the coast of Patagonia, Argentina, where nutrient-rich waters from different currents converge [ref_id:6]. Lastly, a large bloom of cyanobacteria was captured in the Baltic Sea, which can also give the water a green appearance [ref_id:9]."
}
]
}
]
```


## Delete a knowledge base

If you no longer need the knowledge base or need to rebuild it on your search service, use this request to delete the object.

```
using Azure.Search.Documents.Indexes;
var indexClient = new SearchIndexClient(new Uri(searchEndpoint), credential);
await indexClient.DeleteKnowledgeBaseAsync(knowledgeBaseName);
System.Console.WriteLine($"Knowledge base '{knowledgeBaseName}' deleted successfully.");
```


Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

In Azure AI Search, a *knowledge base* is a top-level object that orchestrates [agentic retrieval](agentic-retrieval-overview). It defines which knowledge sources to query and the default behavior for retrieval operations. At query time, the [retrieve method](agentic-retrieval-how-to-retrieve) targets the knowledge base to run the configured retrieval pipeline.

You can create a knowledge base in a [Foundry IQ workload](/en-us/azure/ai-foundry/agents/how-to/tools/knowledge-retrieval) in the Microsoft Foundry (new) portal. You also need a knowledge base in any agentic solutions that you create using the Azure AI Search APIs.

A knowledge base specifies:

- One or more knowledge sources that point to searchable content.
- An optional LLM that provides reasoning capabilities for query planning and answer formulation.
- A retrieval reasoning effort that determines whether an LLM is invoked and manages cost, latency, and quality.
- Custom properties that control routing, source selection, output format, and object encryption.

After you create a knowledge base, you can update its properties at any time. If the knowledge base is in use, updates take effect on the next retrieval.

Important

2025-11-01-preview renames the 2025-08-01-preview "knowledge agent" to "knowledge base." This is a breaking change. We recommend [migrating existing code](agentic-retrieval-how-to-migrate) to the new APIs as soon as possible.

## Prerequisites

Azure AI Search in any

[region that provides agentic retrieval](search-region-support). You must have[semantic ranker enabled](semantic-how-to-enable-disable). If you're using a[managed identity](search-how-to-managed-identities)for role-based access to deployed models, your search service must be on the Basic pricing tier or higher.Azure OpenAI with a

[supported LLM](#supported-models)deployment.One or more

[knowledge sources](agentic-knowledge-source-overview#supported-knowledge-sources)on your search service.Permission to create and use objects on Azure AI Search. We recommend

[role-based access](search-security-rbac).**Search Service Contributor**can create and manage a knowledge base.**Search Index Data Reader**can run queries. Alternatively, you can use[API keys](search-security-api-keys)if a role assignment isn't feasible. For more information, see[Connect to a search service](search-get-started-rbac).The latest preview version of the

for Python.`azure-search-documents`

client library

### Supported models

Use one of the following LLMs from Azure OpenAI in Foundry Models or an equivalent open-source model. For deployment instructions, see [Deploy Microsoft Foundry Models in the Foundry portal](/en-us/azure/ai-foundry/how-to/deploy-models-openai).

`gpt-4o`

`gpt-4o-mini`

`gpt-4.1`

`gpt-4.1-nano`

`gpt-4.1-mini`

`gpt-5`

`gpt-5-nano`

`gpt-5-mini`


## Configure access

Azure AI Search needs access to the LLM from Azure OpenAI. We recommend Microsoft Entra ID for authentication and role-based access for authorization. You must be an **Owner or User Access Administrator** to assign roles. If roles aren't feasible, use key-based authentication instead.

On your model provider, such as Foundry Models, assign

**Cognitive Services User**to the managed identity of your search service. If you're testing locally, assign the same role to your user account.For local testing, follow the steps in

[Quickstart: Connect without keys](search-get-started-rbac)to sign in to a specific subscription and tenant. Use`DefaultAzureCredential`

instead of`AzureKeyCredential`

in each request, which should look similar to the following example:`# Authenticate using roles from azure.identity import DefaultAzureCredential index_client = SearchIndexClient(endpoint = "search_url", credential = DefaultAzureCredential())`


Important

Code snippets in this article use API keys. If you use role-based authentication, update each request accordingly. In a request that specifies both approaches, the API key takes precedence.

## Check for existing knowledge bases

Knowing about existing knowledge bases is helpful for either reuse or naming new objects. Any 2025-08-01-preview knowledge agents are returned in the knowledge bases collection.

Run the following code to list existing knowledge bases by name.

```
# List knowledge bases by name
import requests
import json
endpoint = "{search_url}/knowledgebases"
params = {"api-version": "2025-11-01-preview", "$select": "name"}
headers = {"api-key": "{api_key}"}
response = requests.get(endpoint, params = params, headers = headers)
print(json.dumps(response.json(), indent = 2))
```


You can also return a single knowledge base by name to review its JSON definition.

```
# Get a knowledge base definition
import requests
import json
endpoint = "{search_url}/knowledgebases/{knowledge_base_name}"
params = {"api-version": "2025-11-01-preview"}
headers = {"api-key": "{api_key}"}
response = requests.get(endpoint, params = params, headers = headers)
print(json.dumps(response.json(), indent = 2))
```


The following JSON is an example response for a knowledge base.

```
{
"name": "my-kb",
"description": "A sample knowledge base.",
"retrievalInstructions": null,
"answerInstructions": null,
"outputMode": null,
"knowledgeSources": [
{
"name": "my-blob-ks"
}
],
"models": [],
"encryptionKey": null,
"retrievalReasoningEffort": {
"kind": "low"
}
}
```


## Create a knowledge base

A knowledge base drives the agentic retrieval pipeline. In application code, other agents or chatbots call it.

A knowledge base connects knowledge sources (searchable content) to an LLM deployment from Azure OpenAI. Properties on the LLM establish the connection, while properties on the knowledge source establish defaults that inform query execution and the response.

Run the following code to create a knowledge base.

```
# Create a knowledge base
from azure.core.credentials import AzureKeyCredential
from azure.search.documents.indexes import SearchIndexClient
from azure.search.documents.indexes.models import KnowledgeBase, KnowledgeBaseAzureOpenAIModel, KnowledgeSourceReference, AzureOpenAIVectorizerParameters, KnowledgeRetrievalOutputMode, KnowledgeRetrievalLowReasoningEffort
index_client = SearchIndexClient(endpoint = "search_url", credential = AzureKeyCredential("api_key"))
aoai_params = AzureOpenAIVectorizerParameters(
resource_url = "aoai_endpoint",
api_key="aoai_api_key",
deployment_name = "aoai_gpt_deployment",
model_name = "aoai_gpt_model",
)
knowledge_base = KnowledgeBase(
name = "my-kb",
description = "This knowledge base handles questions directed at two unrelated sample indexes.",
retrieval_instructions = "Use the hotels knowledge source for queries about where to stay, otherwise use the earth at night knowledge source.",
answer_instructions = "Provide a two sentence concise and informative answer based on the retrieved documents.",
output_mode = KnowledgeRetrievalOutputMode.ANSWER_SYNTHESIS,
knowledge_sources = [
KnowledgeSourceReference(name = "hotels-ks"),
KnowledgeSourceReference(name = "earth-at-night-ks"),
],
models = [KnowledgeBaseAzureOpenAIModel(azure_open_ai_parameters = aoai_params)],
encryption_key = None,
retrieval_reasoning_effort = KnowledgeRetrievalLowReasoningEffort,
)
index_client.create_or_update_knowledge_base(knowledge_base)
print(f"Knowledge base '{knowledge_base.name}' created or updated successfully.")
```


### Knowledge base properties

Pass the following properties to create a knowledge base.

| Name | Description | Type | Required |
|---|---|---|---|
`name` |
The name of the knowledge base. It must be unique within the knowledge bases collection and follow the
|

`description`

`retrieval_instructions`

`answer_instructions`

[Use answer synthesis for citation-backed responses](agentic-retrieval-how-to-answer-synthesis).`output_mode`

`answer_synthesis`

for an LLM-formulated answer or `extracted_data`

for full search results that you can pass to an LLM as a downstream step.`knowledge_sources`

[supported knowledge sources](agentic-knowledge-source-overview#supported-knowledge-sources).`models`

[supported LLM](#supported-models)used for answer formulation or query planning. In this preview,`models`

can contain just one model, and the model provider must be Azure OpenAI. Obtain model information from the Foundry portal or a command-line request. You can use role-based access control instead of API keys for the Azure AI Search connection to the model. For more information, see [How to deploy Azure OpenAI models with Foundry](/en-us/azure/ai-foundry/how-to/deploy-models-openai).`encryption_key`

[customer-managed key](search-security-manage-encryption-keys)to encrypt sensitive information in both the knowledge base and the generated objects.`retrieval_reasoning_effort`

`minimal`

, `low`

(default), and `medium`

. For more information, see [Set the retrieval reasoning effort](agentic-retrieval-how-to-set-retrieval-reasoning-effort).## Query a knowledge base

Call the `retrieve`

action on the knowledge base to verify the LLM connection and return results. For more information about the `retrieve`

request and response schema, see [Retrieve data using a knowledge base in Azure AI Search](agentic-retrieval-how-to-retrieve).

Replace "Where does the ocean look green?" with a query string that's valid for your knowledge sources.

```
# Send grounding request
from azure.core.credentials import AzureKeyCredential
from azure.search.documents.knowledgebases import KnowledgeBaseRetrievalClient
from azure.search.documents.knowledgebases.models import KnowledgeBaseMessage, KnowledgeBaseMessageTextContent, KnowledgeBaseRetrievalRequest, SearchIndexKnowledgeSourceParams
kb_client = KnowledgeBaseRetrievalClient(endpoint = "search_url", knowledge_base_name = "knowledge_base_name", credential = AzureKeyCredential("api_key"))
request = KnowledgeBaseRetrievalRequest(
messages=[
KnowledgeBaseMessage(
role = "assistant",
content = [KnowledgeBaseMessageTextContent(text = "Use the earth at night index to answer the question. If you can't find relevant content, say you don't know.")]
),
KnowledgeBaseMessage(
role = "user",
content = [KnowledgeBaseMessageTextContent(text = "Where does the ocean look green?")]
),
],
knowledge_source_params=[
SearchIndexKnowledgeSourceParams(
knowledge_source_name = "earth-at-night-ks",
include_references = True,
include_reference_source_data = True,
always_query_source = False,
)
],
include_activity = True,
)
result = kb_client.retrieve(request)
print(result.response[0].content[0].text)
```


**Key points:**

is required, but you can run this example by using just the`messages`

`user`

role that provides the query.specifies one or more query targets. For each knowledge source, you can specify how much information to include in the output.`knowledge_source_params`


The response to the sample query might look like the following example:

```
"response": [
{
"content": [
{
"type": "text",
"text": "The ocean appears green off the coast of Antarctica due to phytoplankton flourishing in the water, particularly in Granite Harbor near Antarctica’s Ross Sea, where they can grow in large quantities during spring, summer, and even autumn under the right conditions [ref_id:0]. Additionally, off the coast of Namibia, the ocean can also look green due to blooms of phytoplankton and yellow-green patches of sulfur precipitating from bacteria in oxygen-depleted waters [ref_id:1]. In the Strait of Georgia, Canada, the waters turned bright green due to a massive bloom of coccolithophores, a type of phytoplankton [ref_id:5]. Furthermore, a milky green and blue bloom was observed off the coast of Patagonia, Argentina, where nutrient-rich waters from different currents converge [ref_id:6]. Lastly, a large bloom of cyanobacteria was captured in the Baltic Sea, which can also give the water a green appearance [ref_id:9]."
}
]
}
]
```


## Delete a knowledge base

If you no longer need the knowledge base or need to rebuild it on your search service, use this request to delete the object.

```
# Delete a knowledge base
from azure.core.credentials import AzureKeyCredential
from azure.search.documents.indexes import SearchIndexClient
index_client = SearchIndexClient(endpoint = "search_url", credential = AzureKeyCredential("api_key"))
index_client.delete_knowledge_base("knowledge_base_name")
print(f"Knowledge base deleted successfully.")
```


Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

In Azure AI Search, a *knowledge base* is a top-level object that orchestrates [agentic retrieval](agentic-retrieval-overview). It defines which knowledge sources to query and the default behavior for retrieval operations. At query time, the [retrieve method](agentic-retrieval-how-to-retrieve) targets the knowledge base to run the configured retrieval pipeline.

You can create a knowledge base in a [Foundry IQ workload](/en-us/azure/ai-foundry/agents/how-to/tools/knowledge-retrieval) in the Microsoft Foundry (new) portal. You also need a knowledge base in any agentic solutions that you create using the Azure AI Search APIs.

A knowledge base specifies:

- One or more knowledge sources that point to searchable content.
- An optional LLM that provides reasoning capabilities for query planning and answer formulation.
- A retrieval reasoning effort that determines whether an LLM is invoked and manages cost, latency, and quality.
- Custom properties that control routing, source selection, output format, and object encryption.

After you create a knowledge base, you can update its properties at any time. If the knowledge base is in use, updates take effect on the next retrieval.

Important

2025-11-01-preview renames the 2025-08-01-preview "knowledge agent" to "knowledge base." This is a breaking change. We recommend [migrating existing code](agentic-retrieval-how-to-migrate) to the new APIs as soon as possible.

## Prerequisites

Azure AI Search in any

[region that provides agentic retrieval](search-region-support). You must have[semantic ranker enabled](semantic-how-to-enable-disable). If you're using a[managed identity](search-how-to-managed-identities)for role-based access to deployed models, your search service must be on the Basic pricing tier or higher.Azure OpenAI with a

[supported LLM](#supported-models)deployment.One or more

[knowledge sources](agentic-knowledge-source-overview#supported-knowledge-sources)on your search service.Permission to create and use objects on Azure AI Search. We recommend

[role-based access](search-security-rbac).**Search Service Contributor**can create and manage a knowledge base.**Search Index Data Reader**can run queries. Alternatively, you can use[API keys](search-security-api-keys)if a role assignment isn't feasible. For more information, see[Connect to a search service](search-get-started-rbac).The

[2025-11-01-preview](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2025-11-01-preview&preserve-view=true)version of the Search Service REST APIs.

### Supported models

Use one of the following LLMs from Azure OpenAI in Foundry Models or an equivalent open-source model. For deployment instructions, see [Deploy Microsoft Foundry Models in the Foundry portal](/en-us/azure/ai-foundry/how-to/deploy-models-openai).

`gpt-4o`

`gpt-4o-mini`

`gpt-4.1`

`gpt-4.1-nano`

`gpt-4.1-mini`

`gpt-5`

`gpt-5-nano`

`gpt-5-mini`


## Configure access

Azure AI Search needs access to the LLM from Azure OpenAI. We recommend Microsoft Entra ID for authentication and role-based access for authorization. To assign roles, you must be an **Owner or User Access Administrator**. If you can't use roles, use key-based authentication instead.

On your model provider, such as Foundry Models, assign

**Cognitive Services User**to the managed identity of your search service. If you're testing locally, assign the same role to your user account.For local testing, follow the steps in

[Quickstart: Connect without keys](search-get-started-rbac)to get a personal access token for a specific subscription and tenant. Specify your access token in each request, which should look similar to the following example:`# List indexes using roles GET https://{{search-url}}/indexes?api-version=2025-11-01-preview Content-Type: application/json Authorization: Bearer {{access-token}}`


Important

Code snippets in this article use API keys. If you use role-based authentication, update each request accordingly. In a request that specifies both approaches, the API key takes precedence.

## Check for existing knowledge bases

A knowledge base is a top-level, reusable object. Knowing about existing knowledge bases is helpful for either reuse or naming new objects. Any 2025-08-01-preview knowledge agents are returned in the knowledge bases collection.

Use [Knowledge Bases - List (REST API)](/en-us/rest/api/searchservice/knowledge-bases/list?view=rest-searchservice-2025-11-01-preview&preserve-view=true) to list knowledge bases by name and type.

```
# List knowledge bases
GET {{search-url}}/knowledgebases?api-version=2025-11-01-preview&$select=name
Content-Type: application/json
api-key: {{search-api-key}}
```


You can also return a single knowledge base by name to review its JSON definition.

```
# Get knowledge base
GET {{search-url}}/knowledgebases/{{knowledge-base-name}}?api-version=2025-11-01-preview
Content-Type: application/json
api-key: {{search-api-key}}
```


The following JSON is an example response for a knowledge base.

```
{
"name": "my-kb",
"description": "A sample knowledge base.",
"retrievalInstructions": null,
"answerInstructions": null,
"outputMode": null,
"knowledgeSources": [
{
"name": "my-blob-ks"
}
],
"models": [],
"encryptionKey": null,
"retrievalReasoningEffort": {
"kind": "low"
}
}
```


## Create a knowledge base

A knowledge base drives the agentic retrieval pipeline. In application code, other agents or chatbots call it.

A knowledge base connects knowledge sources (searchable content) to an LLM deployment from Azure OpenAI. Properties on the LLM establish the connection, while properties on the knowledge source set defaults that guide query execution and the response.

Use [Knowledge Bases - Create or Update (REST API)](/en-us/rest/api/searchservice/knowledge-bases/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true) to formulate the request.

```
# Create a knowledge base
PUT {{search-url}}/knowledgebases/{{knowledge-base-name}}?api-version=2025-11-01-preview
Content-Type: application/json
api-key: {{search-api-key}}
{
"name" : "my-kb",
"description": "This knowledge base handles questions directed at two unrelated sample indexes.",
"retrievalInstructions": "Use the hotels knowledge source for queries about where to stay, otherwise use the earth at night knowledge source.",
"answerInstructions": null,
"outputMode": "answerSynthesis",
"knowledgeSources": [
{
"name": "hotels-ks"
},
{
"name": "earth-at-night-ks"
}
],
"models" : [
{
"kind": "azureOpenAI",
"azureOpenAIParameters": {
"resourceUri": "{{model-provider-url}}",
"apiKey": "{{model-api-key}}",
"deploymentId": "gpt-4.1-mini",
"modelName": "gpt-4.1-mini"
}
}
],
"encryptionKey": null,
"retrievalReasoningEffort": {
"kind": "low"
}
}
```


### Knowledge base properties

Pass the following properties to create a knowledge base.

| Name | Description | Type | Required |
|---|---|---|---|
`name` |
The name of the knowledge base. It must be unique within the knowledge bases collection and follow the
|

`description`

`retrievalInstructions`

`answerInstructions`

[Use answer synthesis for citation-backed responses](agentic-retrieval-how-to-answer-synthesis).`outputMode`

`answerSynthesis`

for an LLM-formulated answer or `extractedData`

for full search results that you can pass to an LLM as a downstream step.`knowledgeSources`

[supported knowledge sources](agentic-knowledge-source-overview#supported-knowledge-sources).`models`

[supported LLM](#supported-models)used for answer formulation or query planning. In this preview,`models`

can contain just one model, and the model provider must be Azure OpenAI. Obtain model information from the Foundry portal or a command-line request. You can use role-based access control instead of API keys for the Azure AI Search connection to the model. For more information, see [How to deploy Azure OpenAI models with Foundry](/en-us/azure/ai-foundry/how-to/deploy-models-openai).`encryptionKey`

[customer-managed key](search-security-manage-encryption-keys)to encrypt sensitive information in both the knowledge base and the generated objects.`retrievalReasoningEffort.kind`

`minimal`

, `low`

(default), and `medium`

. For more information, see [Set the retrieval reasoning effort](agentic-retrieval-how-to-set-retrieval-reasoning-effort).## Query a knowledge base

Call the `retrieve`

action on the knowledge base to verify the LLM connection and return results. For more information about the `retrieve`

request and response schema, see [Retrieve data using a knowledge base in Azure AI Search](agentic-retrieval-how-to-retrieve).

Use [Knowledge Retrieval - Retrieve (REST API)](/en-us/rest/api/searchservice/knowledge-retrieval/retrieve?view=rest-searchservice-2025-11-01-preview&preserve-view=true) to formulate the request. Replace "Where does the ocean look green?" with a query string that's valid for your knowledge sources.

```
# Send grounding request
POST {{search-url}}/knowledgebases/{{knowledge-base-name}}/retrieve?api-version=2025-11-01-preview
Content-Type: application/json
api-key: {{search-api-key}}
{
"messages" : [
{ "role" : "assistant",
"content" : [
{ "type" : "text", "text" : "Use the earth at night index to answer the question. If you can't find relevant content, say you don't know." }
]
},
{
"role" : "user",
"content" : [
{
"text" : "Where does the ocean look green?",
"type" : "text"
}
]
}
],
"includeActivity": true,
"knowledgeSourceParams": [
{
"knowledgeSourceName": "earth-at-night-ks",
"kind": "searchIndex",
"includeReferences": true,
"includeReferenceSourceData": true,
"alwaysQuerySource": false
}
]
}
```


**Key points:**

is required, but you can run this example by using just the`messages`

`user`

role that provides the query.specifies one or more query targets. For each knowledge source, you can specify how much information to include in the output.`knowledgeSourceParams`


The response to the sample query might look like the following example:

```
"response": [
{
"content": [
{
"type": "text",
"text": "The ocean appears green off the coast of Antarctica due to phytoplankton flourishing in the water, particularly in Granite Harbor near Antarctica’s Ross Sea, where they can grow in large quantities during spring, summer, and even autumn under the right conditions [ref_id:0]. Additionally, off the coast of Namibia, the ocean can also look green due to blooms of phytoplankton and yellow-green patches of sulfur precipitating from bacteria in oxygen-depleted waters [ref_id:1]. In the Strait of Georgia, Canada, the waters turned bright green due to a massive bloom of coccolithophores, a type of phytoplankton [ref_id:5]. Furthermore, a milky green and blue bloom was observed off the coast of Patagonia, Argentina, where nutrient-rich waters from different currents converge [ref_id:6]. Lastly, a large bloom of cyanobacteria was captured in the Baltic Sea, which can also give the water a green appearance [ref_id:9]."
}
]
}
]
```


## Delete a knowledge base

If you no longer need the knowledge base or need to rebuild it on your search service, use this request to delete the object.

```
# Delete a knowledge base
DELETE {{search-url}}/knowledgebases/{{knowledge-base-name}}?api-version=2025-11-01-preview
api-key: {{search-api-key}}
```