---
merged_at: 2026-01-31T00:09:26.089066
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai-embeddingsstore-output -->

# Azure OpenAI embeddings store output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Azure OpenAI extension for Azure Functions is currently in preview.

The Azure OpenAI embeddings store output binding allows you to write files to a semantic document store that can be referenced later in a semantic search.

For information on setup and configuration details of the Azure OpenAI extension, see [Azure OpenAI extensions for Azure Functions](functions-bindings-openai). To learn more about semantic ranking in Azure AI Search, see [Semantic ranking in Azure AI Search](/en-us/azure/search/semantic-search-overview).

Note

References and examples are only provided for the [Node.js v4 model](functions-reference-node?pivots=nodejs-model-v4).

Note

References and examples are only provided for the [Python v2 model](functions-reference-python?pivots=python-mode-decorators#programming-model).

Note

While both C# process models are supported, only [isolated worker model](dotnet-isolated-process-guide) examples are provided.

## Example

This example writes an HTTP input stream to a semantic document store at the provided URL.

```
public class EmbeddingsRequest
{
[JsonPropertyName("url")]
public string? Url { get; set; }
}
[Function("IngestFile")]
public static async Task<EmbeddingsStoreOutputResponse> IngestFile(
[HttpTrigger(AuthorizationLevel.Function, "post")] HttpRequestData req)
{
using StreamReader reader = new(req.Body);
string request = await reader.ReadToEndAsync();
EmbeddingsStoreOutputResponse badRequestResponse = new()
{
HttpResponse = new BadRequestResult(),
SearchableDocument = new SearchableDocument(string.Empty)
};
if (string.IsNullOrWhiteSpace(request))
{
return badRequestResponse;
}
EmbeddingsRequest? requestBody = JsonSerializer.Deserialize<EmbeddingsRequest>(request);
if (string.IsNullOrWhiteSpace(requestBody?.Url))
{
throw new ArgumentException("Invalid request body. Make sure that you pass in {\"url\": value } as the request body.");
}
if (!Uri.TryCreate(requestBody.Url, UriKind.Absolute, out Uri? uri))
{
return badRequestResponse;
}
string filename = Path.GetFileName(uri.AbsolutePath);
return new EmbeddingsStoreOutputResponse
{
HttpResponse = new OkObjectResult(new { status = HttpStatusCode.OK }),
SearchableDocument = new SearchableDocument(filename)
};
}
```


This example writes an HTTP input stream to a semantic document store at the provided URL.

```
@FunctionName("IngestFile")
public HttpResponseMessage ingestFile(
@HttpTrigger(
name = "req",
methods = {HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<EmbeddingsRequest> request,
@EmbeddingsStoreOutput(name="EmbeddingsStoreOutput", input = "{url}", inputType = InputType.Url,
storeConnectionName = "AISearchEndpoint", collection = "openai-index",
embeddingsModel = "%EMBEDDING_MODEL_DEPLOYMENT_NAME%") OutputBinding<EmbeddingsStoreOutputResponse> output,
final ExecutionContext context) throws URISyntaxException {
if (request.getBody() == null || request.getBody().getUrl() == null)
{
throw new IllegalArgumentException("Invalid request body. Make sure that you pass in {\"url\": value } as the request body.");
}
URI uri = new URI(request.getBody().getUrl());
String filename = Paths.get(uri.getPath()).getFileName().toString();
EmbeddingsStoreOutputResponse embeddingsStoreOutputResponse = new EmbeddingsStoreOutputResponse(new SearchableDocument(filename));
output.setValue(embeddingsStoreOutputResponse);
JSONObject response = new JSONObject();
response.put("status", "success");
response.put("title", filename);
return request.createResponseBuilder(HttpStatus.CREATED)
.header("Content-Type", "application/json")
.body(response)
.build();
}
public class EmbeddingsStoreOutputResponse {
private SearchableDocument searchableDocument;
public EmbeddingsStoreOutputResponse(SearchableDocument searchableDocument) {
this.searchableDocument = searchableDocument;
}
public SearchableDocument getSearchableDocument() {
return searchableDocument;
}
}
```


This example writes an HTTP input stream to a semantic document store at the provided URL.

```
const embeddingsStoreOutput = output.generic({
type: "embeddingsStore",
input: "{url}",
inputType: "url",
connectionName: "AISearchEndpoint",
collection: "openai-index",
embeddingsModel: "%EMBEDDING_MODEL_DEPLOYMENT_NAME%"
});
app.http('IngestFile', {
methods: ['POST'],
authLevel: 'function',
extraOutputs: [embeddingsStoreOutput],
handler: async (request, context) => {
let requestBody = await request.json();
if (!requestBody || !requestBody.url) {
throw new Error("Invalid request body. Make sure that you pass in {\"url\": value } as the request body.");
}
let uri = requestBody.url;
let url = new URL(uri);
let fileName = path.basename(url.pathname);
context.extraOutputs.set(embeddingsStoreOutput, { title: fileName });
let response = {
status: "success",
title: fileName
};
return { status: 202, jsonBody: response }
}
});
```


```
interface EmbeddingsRequest {
url?: string;
}
const embeddingsStoreOutput = output.generic({
type: "embeddingsStore",
input: "{url}",
inputType: "url",
connectionName: "AISearchEndpoint",
collection: "openai-index",
embeddingsModel: "%EMBEDDING_MODEL_DEPLOYMENT_NAME%"
});
app.http('IngestFile', {
methods: ['POST'],
authLevel: 'function',
extraOutputs: [embeddingsStoreOutput],
handler: async (request, context) => {
let requestBody: EmbeddingsRequest | null = await request.json();
if (!requestBody || !requestBody.url) {
throw new Error("Invalid request body. Make sure that you pass in {\"url\": value } as the request body.");
}
let uri = requestBody.url;
let url = new URL(uri);
let fileName = path.basename(url.pathname);
context.extraOutputs.set(embeddingsStoreOutput, { title: fileName });
let response = {
status: "success",
title: fileName
};
return { status: 202, jsonBody: response }
}
});
```


This example writes an HTTP input stream to a semantic document store at the provided URL.

Here's the *function.json* file for ingesting files:

```
{
"bindings": [
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "Request",
"methods": [
"post"
]
},
{
"type": "http",
"direction": "out",
"name": "Response"
},
{
"name": "EmbeddingsStoreOutput",
"type": "embeddingsStore",
"direction": "out",
"input": "{url}",
"inputType": "Url",
"storeConnectionName": "AISearchEndpoint",
"collection": "openai-index",
"embeddingsModel": "%EMBEDDING_MODEL_DEPLOYMENT_NAME%"
}
]
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

```
using namespace System.Net
param($Request, $TriggerMetadata)
$ErrorActionPreference = 'Stop'
$inputJson = $Request.Body
if (-not $inputJson -or -not $inputJson.Url) {
throw 'Invalid request body. Make sure that you pass in {\"url\": value } as the request body.'
}
$uri = [URI]$inputJson.Url
$filename = [System.IO.Path]::GetFileName($uri.AbsolutePath)
Push-OutputBinding -Name EmbeddingsStoreOutput -Value @{
"title" = $filename
}
$response = @{
"status" = "success"
"title" = $filename
}
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $response
Headers = @{
"Content-Type" = "application/json"
}
})
```


This example writes an HTTP input stream to a semantic document store at the provided URL.

```
@app.function_name("IngestFile")
@app.route(methods=["POST"])
@app.embeddings_store_output(
arg_name="requests",
input="{url}",
input_type="url",
store_connection_name="AISearchEndpoint",
collection="openai-index",
embeddings_model="%EMBEDDING_MODEL_DEPLOYMENT_NAME%",
)
def ingest_file(
req: func.HttpRequest, requests: func.Out[str]
) -> func.HttpResponse:
user_message = req.get_json()
if not user_message:
return func.HttpResponse(
json.dumps({"message": "No message provided"}),
status_code=400,
mimetype="application/json",
)
file_name_with_extension = os.path.basename(user_message["url"])
title = os.path.splitext(file_name_with_extension)[0]
create_request = {"title": title}
requests.set(json.dumps(create_request))
response_json = {"status": "success", "title": title}
return func.HttpResponse(
json.dumps(response_json), status_code=200, mimetype="application/json"
)
```


## Attributes

Apply the `EmbeddingsStoreOutput`

attribute to define an embeddings store output binding, which supports these parameters:

| Parameter | Description |
|---|---|
Input |
The input string for which to generate embeddings. |
AIConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
EmbeddingsModel |
Optional. The ID of the model to use, which defaults to `text-embedding-ada-002` . You shouldn't change the model for an existing database. For more information, see
|
MaxChunkLength |
Optional. The maximum number of characters used for chunking the input. For more information, see
|
MaxOverlap |
Optional. Gets or sets the maximum number of characters to overlap between chunks. |
InputType |
Optional. Gets the type of the input. |
StoreConnectionName |
The name of an app setting or environment variable that contains the connection string value. This property supports binding expressions. |
Collection |
The name of the collection or table or index to search. This property supports binding expressions. |

## Annotations

The `EmbeddingsStoreOutput`

annotation enables you to define an embeddings store output binding, which supports these parameters:

| Element | Description |
|---|---|
name |
Gets or sets the name of the output binding. |
input |
The input string for which to generate embeddings. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
embeddingsModel |
Optional. The ID of the model to use, which defaults to `text-embedding-ada-002` . You shouldn't change the model for an existing database. For more information, see
|
maxChunkLength |
Optional. The maximum number of characters used for chunking the input. For more information, see
|
maxOverlap |
Optional. Gets or sets the maximum number of characters to overlap between chunks. |
inputType |
Optional. Gets the type of the input. |
storeConnectionName |
The name of an app setting or environment variable that contains the connection string value. This property supports binding expressions. |
collection |
The name of the collection or table or index to search. This property supports binding expressions. |

## Decorators

During the preview, define the output binding as a `generic_output_binding`

binding of type `semanticSearch`

, which supports these parameters:

| Parameter | Description |
|---|---|
arg_name |
The name of the variable that represents the binding parameter. |
input |
The input string for which to generate embeddings. |
ai_connection_name |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
embeddings_model |
Optional. The ID of the model to use, which defaults to `text-embedding-ada-002` . You shouldn't change the model for an existing database. For more information, see
|
maxChunkLength |
Optional. The maximum number of characters used for chunking the input. For more information, see
|
max_overlap |
Optional. Gets or sets the maximum number of characters to overlap between chunks. |
input_type |
Gets the type of the input. |
store_connection_name |
The name of an app setting or environment variable that contains the connection string value. This property supports binding expressions. |
collection |
The name of the collection or table or index to search. This property supports binding expressions. |

## Configuration

The binding supports these configuration properties that you set in the function.json file.

| Property | Description |
|---|---|
type |
Must be `embeddingsStore` . |
direction |
Must be `out` . |
name |
The name of the output binding. |
input |
The input string for which to generate embeddings. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
embeddingsModel |
Optional. The ID of the model to use, which defaults to `text-embedding-ada-002` . You shouldn't change the model for an existing database. For more information, see
|
maxChunkLength |
Optional. The maximum number of characters used for chunking the input. For more information, see
|
maxOverlap |
Optional. Gets or sets the maximum number of characters to overlap between chunks. |
inputType |
Optional. Gets the type of the input. |
storeConnectionName |
The name of an app setting or environment variable that contains the connection string value. This property supports binding expressions. |
collection |
The name of the collection or table or index to search. This property supports binding expressions. |

## Configuration

The binding supports these properties, which are defined in your code:

| Property | Description |
|---|---|
input |
The input string for which to generate embeddings. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
embeddingsModel |
Optional. The ID of the model to use, which defaults to `text-embedding-ada-002` . You shouldn't change the model for an existing database. For more information, see
|
maxChunkLength |
Optional. The maximum number of characters used for chunking the input. For more information, see
|
maxOverlap |
Optional. Gets or sets the maximum number of characters to overlap between chunks. |
inputType |
Optional. Gets the type of the input. |
storeConnectionName |
The name of an app setting or environment variable that contains the connection string value. This property supports binding expressions. |
collection |
The name of the collection or table or index to search. This property supports binding expressions. |

## Usage

See the [Example section](#example) for complete examples.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai-semanticsearch-input -->

# Azure OpenAI Semantic Search Input Binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Azure OpenAI extension for Azure Functions is currently in preview.

The Azure OpenAI semantic search input binding allows you to use semantic search on your embeddings.

For information on setup and configuration details of the Azure OpenAI extension, see [Azure OpenAI extensions for Azure Functions](functions-bindings-openai). To learn more about semantic ranking in Azure AI Search, see [Semantic ranking in Azure AI Search](/en-us/azure/search/semantic-search-overview).

Note

References and examples are only provided for the [Node.js v4 model](functions-reference-node?pivots=nodejs-model-v4).

Note

References and examples are only provided for the [Python v2 model](functions-reference-python?pivots=python-mode-decorators#programming-model).

Note

While both C# process models are supported, only [isolated worker model](dotnet-isolated-process-guide) examples are provided.

## Example

This example shows how to perform a semantic search on a file.

```
[Function("PromptFile")]
public static IActionResult PromptFile(
[HttpTrigger(AuthorizationLevel.Function, "post")] SemanticSearchRequest unused,
[SemanticSearchInput("AISearchEndpoint", "openai-index", Query = "{prompt}", ChatModel = "%CHAT_MODEL_DEPLOYMENT_NAME%", EmbeddingsModel = "%EMBEDDING_MODEL_DEPLOYMENT_NAME%")] SemanticSearchContext result)
{
return new ContentResult { Content = result.Response, ContentType = "text/plain" };
}
```


This example shows how to perform a semantic search on a file.

```
@FunctionName("PromptFile")
public HttpResponseMessage promptFile(
@HttpTrigger(
name = "req",
methods = {HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<SemanticSearchRequest> request,
@SemanticSearch(name = "search", searchConnectionName = "AISearchEndpoint", collection = "openai-index", query = "{prompt}", chatModel = "%CHAT_MODEL_DEPLOYMENT_NAME%", embeddingsModel = "%EMBEDDING_MODEL_DEPLOYMENT_NAME%", isReasoningModel = false ) String semanticSearchContext,
final ExecutionContext context) {
String response = new JSONObject(semanticSearchContext).getString("Response");
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(response)
.build();
}
public class SemanticSearchRequest {
public String prompt;
public String getPrompt() {
return prompt;
}
public void setPrompt(String prompt) {
this.prompt = prompt;
}
}
```


This example shows how to perform a semantic search on a file.

```
const semanticSearchInput = input.generic({
type: "semanticSearch",
connectionName: "AISearchEndpoint",
collection: "openai-index",
query: "{prompt}",
chatModel: "%CHAT_MODEL_DEPLOYMENT_NAME%",
embeddingsModel: "%EMBEDDING_MODEL_DEPLOYMENT_NAME%"
});
app.http('PromptFile', {
methods: ['POST'],
authLevel: 'function',
extraInputs: [semanticSearchInput],
handler: async (_request, context) => {
var responseBody = context.extraInputs.get(semanticSearchInput)
return { status: 200, body: responseBody.Response.trim() }
}
});
```


```
const semanticSearchInput = input.generic({
type: "semanticSearch",
connectionName: "AISearchEndpoint",
collection: "openai-index",
query: "{prompt}",
chatModel: "%CHAT_MODEL_DEPLOYMENT_NAME%",
embeddingsModel: "%EMBEDDING_MODEL_DEPLOYMENT_NAME%"
});
app.http('PromptFile', {
methods: ['POST'],
authLevel: 'function',
extraInputs: [semanticSearchInput],
handler: async (_request, context) => {
var responseBody: any = context.extraInputs.get(semanticSearchInput)
return { status: 200, body: responseBody.Response.trim() }
}
});
```


This example shows how to perform a semantic search on a file.

Here's the *function.json* file for prompting a file:

```
{
"bindings": [
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "Request",
"methods": [
"post"
]
},
{
"type": "http",
"direction": "out",
"name": "Response"
},
{
"name": "SemanticSearchInput",
"type": "semanticSearch",
"direction": "in",
"searchConnectionName": "AISearchEndpoint",
"collection": "openai-index",
"query": "{prompt}",
"chatModel": "%CHAT_MODEL_DEPLOYMENT_NAME%",
"embeddingsModel": "%EMBEDDING_MODEL_DEPLOYMENT_NAME%"
}
]
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

```
using namespace System.Net
param($Request, $TriggerMetadata, $SemanticSearchInput)
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $SemanticSearchInput.Response
})
```


This example shows how to perform a semantic search on a file.

```
@app.function_name("PromptFile")
@app.route(methods=["POST"])
@app.semantic_search_input(
arg_name="result",
search_connection_name="AISearchEndpoint",
collection="openai-index",
query="{prompt}",
embeddings_model="%EMBEDDING_MODEL_DEPLOYMENT_NAME%",
chat_model="%CHAT_MODEL_DEPLOYMENT_NAME%",
)
def prompt_file(req: func.HttpRequest, result: str) -> func.HttpResponse:
result_json = json.loads(result)
response_json = {
"content": result_json.get("Response"),
"content_type": "text/plain",
}
return func.HttpResponse(
json.dumps(response_json), status_code=200, mimetype="application/json"
)
```


## Attributes

Apply the `SemanticSearchInput`

attribute to define a semantic search input binding, which supports these parameters:

| Parameter | Description |
|---|---|
SearchConnectionName |
The name of an app setting or environment variable that contains the connection string value. This property supports binding expressions. |
Collection |
The name of the collection or table or index to search. This property supports binding expressions. |
Query |
The semantic query text to use for searching. This property supports binding expressions. |
EmbeddingsModel |
Optional. The ID of the model to use for embeddings. The default value is `text-embedding-3-small` . This property supports binding expressions. |
ChatModel |
Optional. Gets or sets the name of the Large Language Model to invoke for chat responses. The default value is `gpt-3.5-turbo` . This property supports binding expressions. |
AIConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
SystemPrompt |
Optional. Gets or sets the system prompt to use for prompting the large language model. The system prompt is appended with knowledge that is fetched as a result of the `Query` . The combined prompt is sent to the OpenAI Chat API. This property supports binding expressions. |
MaxKnowledgeCount |
Optional. Gets or sets the number of knowledge items to inject into the `SystemPrompt` . |
IsReasoningModel |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Annotations

The `SemanticSearchInput`

annotation enables you to define a semantic search input binding, which supports these parameters:

| Element | Description |
|---|---|
name |
Gets or sets the name of the input binding. |
searchConnectionName |
The name of an app setting or environment variable that contains the connection string value. This property supports binding expressions. |
collection |
The name of the collection or table or index to search. This property supports binding expressions. |
query |
The semantic query text to use for searching. This property supports binding expressions. |
embeddingsModel |
Optional. The ID of the model to use for embeddings. The default value is `text-embedding-3-small` . This property supports binding expressions. |
chatModel |
Optional. Gets or sets the name of the Large Language Model to invoke for chat responses. The default value is `gpt-3.5-turbo` . This property supports binding expressions. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
systemPrompt |
Optional. Gets or sets the system prompt to use for prompting the large language model. The system prompt is appended with knowledge that is fetched as a result of the `Query` . The combined prompt is sent to the OpenAI Chat API. This property supports binding expressions. |
maxKnowledgeCount |
Optional. Gets or sets the number of knowledge items to inject into the `SystemPrompt` . |
isReasoningModel |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Decorators

During the preview, define the input binding as a `generic_input_binding`

binding of type `semanticSearch`

, which supports these parameters:

| Parameter | Description |
|---|---|
arg_name |
The name of the variable that represents the binding parameter. |
search_connection_name |
The name of an app setting or environment variable that contains the connection string value. This property supports binding expressions. |
collection |
The name of the collection or table or index to search. This property supports binding expressions. |
query |
The semantic query text to use for searching. This property supports binding expressions. |
embeddings_model |
Optional. The ID of the model to use for embeddings. The default value is `text-embedding-3-small` . This property supports binding expressions. |
chat_model |
Optional. Gets or sets the name of the Large Language Model to invoke for chat responses. The default value is `gpt-3.5-turbo` . This property supports binding expressions. |
ai_connection_name |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
system_prompt |
Optional. Gets or sets the system prompt to use for prompting the large language model. The system prompt is appended with knowledge that is fetched as a result of the `Query` . The combined prompt is sent to the OpenAI Chat API. This property supports binding expressions. |
max_knowledge_count |
Optional. Gets or sets the number of knowledge items to inject into the `SystemPrompt` . |
is_reasoning _model |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Configuration

The binding supports these configuration properties that you set in the function.json file.

| Property | Description |
|---|---|
type |
Must be `semanticSearch` . |
direction |
Must be `in` . |
name |
The name of the input binding. |
searchConnectionName |
Gets or sets the name of an app setting or environment variable that contains a connection string value. This property supports binding expressions. |
collection |
The name of the collection or table or index to search. This property supports binding expressions. |
query |
The semantic query text to use for searching. This property supports binding expressions. |
embeddingsModel |
Optional. The ID of the model to use for embeddings. The default value is `text-embedding-3-small` . This property supports binding expressions. |
chatModel |
Optional. Gets or sets the name of the Large Language Model to invoke for chat responses. The default value is `gpt-3.5-turbo` . This property supports binding expressions. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
systemPrompt |
Optional. Gets or sets the system prompt to use for prompting the large language model. The system prompt is appended with knowledge that is fetched as a result of the `Query` . The combined prompt is sent to the OpenAI Chat API. This property supports binding expressions. |
maxKnowledgeCount |
Optional. Gets or sets the number of knowledge items to inject into the `SystemPrompt` . |
isReasoningModel |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Configuration

The binding supports these properties, which are defined in your code:

| Property | Description |
|---|---|
searchConnectionName |
The name of an app setting or environment variable that contains the connection string value. This property supports binding expressions. |
collection |
The name of the collection or table or index to search. This property supports binding expressions. |
query |
The semantic query text to use for searching. This property supports binding expressions. |
embeddingsModel |
Optional. The ID of the model to use for embeddings. The default value is `text-embedding-3-small` . This property supports binding expressions. |
chatModel |
Optional. Gets or sets the name of the Large Language Model to invoke for chat responses. The default value is `gpt-3.5-turbo` . This property supports binding expressions. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
systemPrompt |
Optional. Gets or sets the system prompt to use for prompting the large language model. The system prompt is appended with knowledge that is fetched as a result of the `Query` . The combined prompt is sent to the OpenAI Chat API. This property supports binding expressions. |
maxKnowledgeCount |
Optional. Gets or sets the number of knowledge items to inject into the `SystemPrompt` . |
isReasoningModel |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Usage

See the [Example section](#example) for complete examples.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-storage-queue-triggered-function -->

# Create a function triggered by Azure Queue storage

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Learn how to create a function that is triggered when messages are submitted to an Azure Storage queue.

Note

In-portal editing is only supported for JavaScript, PowerShell, and C# Script functions.
Python in-portal editing is supported only when running in the Consumption plan.
To create a C# Script app that supports in-portal editing, you must choose a runtime **Version** that supports the **in-process model**.

When possible, you should [develop your functions locally](functions-develop-local).

To learn more about the limitations on editing function code in the Azure portal, see [Development limitations in the Azure portal](functions-how-to-use-azure-function-app-settings#development-limitations-in-the-azure-portal).

## Prerequisites

- An Azure subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

## Create an Azure Function app

From the Azure portal menu or the

**Home**page, select**Create a resource**.In the

**New**page, select**Function App**.Under

**Select a hosting option**, select**Consumption**>**Select**to create your app in the default**Consumption**plan. In this[serverless](https://azure.microsoft.com/overview/serverless-computing/)hosting option, you pay only for the time your functions run.[Premium plan](functions-premium-plan)also offers dynamic scaling. When you run in an App Service plan, you must manage the[scaling of your function app](functions-scale).On the

**Basics**page, use the function app settings as specified in the following table:Setting Suggested value Description **Subscription**Your subscription The subscription under which you create your new function app. [Resource Group](../azure-resource-manager/management/overview)*myResourceGroup*Name for the new resource group in which you create your function app. You should create a new resource group because there are [known limitations when creating new function apps in an existing resource group](functions-scale#limitations-for-creating-new-function-apps-in-an-existing-resource-group).**Function App name**Globally unique name Name that identifies your new function app. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

. To guarantee a unique app name, you can optionally enable**Secure unique default hostname**, which is currently in preview.**Runtime stack**Preferred language Choose a runtime that supports your favorite function programming language. In-portal editing is only available for JavaScript, PowerShell, Python, TypeScript, and C# script.

To create a C# Script app that supports in-portal editing, you must choose a runtime**Version**that supports the**in-process model**.

C# class library and Java functions must be[developed locally](functions-develop-local#local-development-environments).**Version**Version number Choose the version of your installed runtime. **Region**Preferred region Select a [region](https://azure.microsoft.com/regions/)that's near you or near other services that your functions can access.**Operating system**Windows An operating system is preselected for you based on your runtime stack selection, but you can change the setting if necessary. In-portal editing is only supported on Windows. Accept the default options in the remaining tabs, including the default behavior of creating a new storage account on the

**Storage**tab and a new Application Insight instance on the**Monitoring**tab. You can also choose to use an existing storage account or Application Insights instance.Select

**Review + create**to review the app configuration you chose, and then select**Create**to provision and deploy the function app.Select the

**Notifications**icon in the upper-right corner of the portal and watch for the**Deployment succeeded**message.Select

**Go to resource**to view your new function app. You can also select**Pin to dashboard**. Pinning makes it easier to return to this function app resource from your dashboard.

Next, you create a function in the new function app.

## Create a Queue triggered function

In your function app, select

**Overview**, and then select**+ Create**under**Functions**.Under

**Select a template**, scroll down and choose the**Azure Queue Storage trigger**template.In

**Template details**, configure the new trigger with the settings as specified in this table, then select**Create**:Setting Suggested value Description **Job type**Append to app You only see this setting for a Python v2 app. **Name**Unique in your function app Name of this queue triggered function. **Queue name**myqueue-items Name of the queue to connect to in your Storage account. **Storage account connection**AzureWebJobsStorage You can use the storage account connection already being used by your function app, or create a new one. Azure creates the Queue Storage triggered function based on the provided values. Next, you connect to your Azure storage account and create the

**myqueue-items**storage queue.

## Create the queue

Return to the

**Overview**page for your function app, select your**Resource group**, then find and select the storage account in your resource group.In the storage account page, select

**Data storage**>**Queues**>**+ Queue**.In the

**Name**field, type`myqueue-items`

, and then select**Create**.Select the new

**myqueue-items**queue, which you use to test the function by adding a message to the queue.

## Test the function

In a new browser window, return to your function app page and select

**Log stream**, which displays real-time logging for your app.In the

**myqueue-items**queue, select**Add message**, type "Hello World!" in**Message text**, and select**OK**.Go back to your function app logs and verify that the function ran to process the message from the queue.

Back in your storage queue, select

**Refresh**and verify that the message has been processed and is no longer in the queue.

## Clean up resources

Other quickstarts in this collection build upon this quickstart. If you plan to work with subsequent quickstarts, tutorials, or with any of the services you've created in this quickstart, don't clean up the resources.

*Resources* in Azure refer to function apps, functions, storage accounts, and so forth. They're grouped into *resource groups*, and you can delete everything in a group by deleting the group.

You've created resources to complete these quickstarts. You might be billed for these resources, depending on your [account status](https://azure.microsoft.com/account/) and [service pricing](https://azure.microsoft.com/pricing/). If you don't need the resources anymore, here's how to delete them:

In the Azure portal, go to the

**Resource group**page.To get to that page from the function app page, select the

**Overview**tab, and then select the link under**Resource group**.To get to that page from the dashboard, select

**Resource groups**, and then select the resource group that you used for this article.In the

**Resource group**page, review the list of included resources, and verify that they're the ones you want to delete.Select

**Delete resource group**and follow the instructions.Deletion might take a couple of minutes. When it's done, a notification appears for a few seconds. You can also select the bell icon at the top of the page to view the notification.


## Next steps

You have created a function that runs when a message is added to a storage queue. For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue).

Now that you have a created your first function, let's add an output binding to the function that writes a message back to another queue.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-register -->

# Register Azure Functions binding extensions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Functions runtime natively runs HTTP and timer triggers. The behaviors of the other supported [triggers and bindings](functions-triggers-bindings) are implemented in separate extension packages.

Projects that use a .NET class library use binding extensions that are installed in the project as NuGet packages.

Extension bundles allow non-.NET apps to use binding extensions without having to interact with .NET infrastructure.

## Extension bundles

Extension bundles add a predefined set of compatible binding extensions to your function app. Extension bundles are versioned. Each version contains a specific set of binding extensions that are verified to work together. Select a bundle version based on the extensions that you need in your app.

When you create an Azure Functions project from a non-.NET template, extension bundles are already enabled in the app's `host.json`

file.

When possible, use the latest version range to obtain optimal app performance and access to the latest features. To learn more about extension bundles, see [Azure Functions extension bundles](extension-bundles).

In the unlikely event that you can't use an extension bundle, you must instead explicitly install extensions.

## Explicitly install extensions

For projects that use a compiled C# class library, you install the NuGet packages for the extensions that you need as you normally would in your apps. For more information, see the [Visual Studio Code developer guide](functions-develop-vs-code?tabs=csharp#install-binding-extensions) or the [Visual Studio developer guide](functions-develop-vs#add-bindings).

Make sure to obtain the correct package, because the namespace differs depending on the execution model:

| Execution model | Namespace |
|---|---|
|

`Microsoft.Azure.Functions.Worker.Extensions.*`

[In-process](functions-dotnet-class-library)`Microsoft.Azure.WebJobs.Extensions.*`

Azure Functions provides extension bundles for non-.NET projects. These bundles contain a full set of binding extensions that are verified to be compatible. If you're having compatibility problems between two or more binding extensions, review compatible combinations of extension versions. For supported combinations of binding extensions, see the [release page for extension bundles](https://github.com/Azure/azure-functions-extension-bundles/releases).

There are cases when you can't use extension bundles, such as when you need to use a specific prerelease version of a specific extension. In these rare cases, you must manually install any required binding extensions in a C# project file that references the specific extensions that your app requires.

To manually install binding extensions:

Remove the extension bundle reference from your

`host.json`

file.Use the

command in Azure Functions Core Tools to generate the required`func extensions install`

`extensions.csproj`

file in the root of your local project.For portal-only development, you need to manually create an

`extensions.csproj`

file in the root of your function app in Azure. To learn more, see[Manually install extensions](functions-how-to-use-azure-function-app-settings#manually-install-extensions).Edit the

`extensions.csproj`

file by explicitly adding a`PackageReference`

element for every specific binding extension and version that your app requires.Validate your app functionality locally and then redeploy your project, including

`extensions.csproj`

, to your function app in Azure.

As soon as possible, you should [switch your app back to using the latest supported extension bundle](extension-bundles#define-an-extension-bundle-reference).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/register-mcp-server-api-center -->

# Register MCP servers hosted in Azure Functions in Azure API Center

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

After hosting your MCP server remotely on Azure Functions, register it on Azure API Center. Azure API Center maintains an inventory (or registry) of remote MCP servers so that they're easily discoverable across your organization. All registered MCP servers appear in the API Center portal for teams in your organization.

Tip

The API Center name becomes your private tool catalog name in the registry filter. Choose an informative name that helps users identify your organization's tool catalog.

## Create resources

Sign in to the Azure portal, then

[create an Azure API Center resource](../api-center/set-up-api-center), if you don't already have one.[Create an environment](../api-center/tutorials/configure-environments-deployments#add-an-environment)in your API Center resource. For**Server**>**Type**, select**Azure Functions**.

## Register MCP server

Register your remote MCP server by adding it as an API:

In the left navigation pane of the API Center resource, select

**APIs**.Select

**+ Register an API**. The following table provides example values for the required settings. You can also fill in the optional settings like MCP server description, repository, external documentation, and other information displayed in the API Center portal.Setting Value **API Title**Enter a descriptive name for the MCP server, like `Weather MCP Server`

.**Identification**This value is autogenerated based on the API Title, but you can modify it. **API type****MCP****Runtime URL**Enter MCP server endpoint, such as `https://contoso.azurewebsites.net/mcp`

**Environment**Select the environment you created earlier. **Version title**Enter a version title of your choice, such as `v1`

.**Version identification**After you enter the preceding title, Azure API Center generates this identifier, which you can override. **Version lifecycle**Select the most appropriate value from the dropdown, such as **Testing**or**Production**.Select

**Create**.You should now see the MCP server registered as an API on the list.


## Update server definition

Create an API definition for a remote MCP server in OpenAPI 3.0 format. You need this definition so the API Center portal shows the URL endpoint of the MCP server. Save the definition where you can access it. You need to upload it in the next step.

Example OpenAPI 3.0 API definition for the MCP server:

`{ "openapi": "3.0.0", "info": { "title": "Weather MCP server", "description": "MCP server with tools returning weather forecast and alerts.", "version": "1.0" }, "servers": [ { "url": "https://my-mcp-server.azurewebsites.net/mcp" } ] }`

Update the server definition:

a. On the left menu, find

**Assets -> APIs**.b. Select the MCP server name to open the registration.

c. On the left menu, find

**Details -> Versions**.d. Under "Version", find and expand "v1". Then select

**Streamable Definition for...**to open the definition.d. Select

**Replace**.e. In the side pane that opens, change the "Specification version" to 3.0, then upload the definition from the last step.

f. Select

**Replace**.

## Set up API Center portal

[Set up the portal](../api-center/set-up-api-center-portal)if you don't already have one.Once the portal is set up, you can access it at

`https://<service-name>.portal.<location>.azure-apicenter.ms`

. Replace`<service-name>`

and`<location>`

with the name of your API center and the location where you deployed it. You need to sign in to see registered MCP servers.When you select a server name, a pane opens that shows information based on data you provide during server registration and the uploaded API definition. Users with access to the portal can connect to servers of their choice by copying the endpoint URL or the install in Visual Studio Code integration.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-consumption-costs -->

# Estimating consumption-based costs

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to estimate plan costs for both the [Flex Consumption plan](flex-consumption-plan) and the legacy [Consumption plan](consumption-plan).

Choose the hosting option that best supports the feature, performance, and cost requirements for your function executions. For more information, see [Azure Functions scale and hosting](functions-scale).

This article focuses on the two consumption plans because billing in these plans depends on active periods of executions inside each instance.

Provides fast horizontal scaling, with flexible compute options, virtual network integration, and full support for connections using Microsoft Entra ID authentication. In this plan, instances dynamically scale out based on configured per-instance concurrency, incoming events, and per-function workloads for optimal efficiency. Flex Consumption is the recommended plan for serverless hosting. For more information, see [Azure Functions Flex Consumption plan hosting](flex-consumption-plan).

Durable Functions can also run in both of these plans. For more information about the cost considerations when using Durable Functions, see [Durable Functions billing](durable/durable-functions-billing).

## Consumption-based costs

The way that consumption-based costs are calculated, including free grants, depends on the specific plan. For the most current cost and grant information, see the [Azure Functions pricing page](https://azure.microsoft.com/pricing/details/functions/).

There are two modes by which your costs are determined when running your apps in the Flex Consumption plan. Each mode is determined on a per-instance basis.

| Billing mode | Description |
|---|---|
On Demand |
When running in on demand mode, you are billed only for the amount of time your function code is executing on your available instances. In on demand mode, no minimum instance count is required. You're billed for:• The total amount of memory provisioned while each on demand instance is actively executing functions (in GB-seconds), minus a free grant of GB-s per month.• The total number of executions, minus a free grant (number) of executions per month. |
Always ready |
You can configure one or more instances, assigned to specific trigger types (HTTP/Durable/Blob) and individual functions, that are always available to handle requests. When you have any always ready instances enabled, you're billed for: • The total amount of memory provisioned across all of your always ready instances, known as the baseline (in GB-seconds).• The total amount of memory provisioned during the time each always ready instance is actively executing functions (in GB-seconds).• The total number of executions. In always ready billing, there are no free grants. |

For the most up-to-date information on execution pricing, always ready baseline costs, and free grants for on demand executions, see the [Azure Functions pricing page](https://azure.microsoft.com/pricing/details/functions/#pricing).

This diagram shows how on-demand costs are determined in this plan:


In addition to execution time, when you use one or more always ready instances, you pay a lower, baseline rate for the number of always ready instances you maintain. Execution time for always ready instances might be cheaper than execution time on instances with on demand execution.

Important

This article uses on-demand pricing to help you understand example calculations. Always check the current costs on the [Azure Functions pricing page](https://azure.microsoft.com/pricing/details/functions/) when estimating costs you might incur while running your functions in the Flex Consumption plan.

Consider a function app that has only HTTP triggers with these basic facts:

- HTTP triggers handle 40 constant requests per second.
- HTTP triggers handle 10 concurrent requests.
- The instance memory size is 2,048 MB.
- You configure
*no always ready instances*, which means the app can scale to zero.

In a situation like this, pricing depends more on the kind of work done during code execution. Let's look at two workload scenarios:

**CPU-bound workload:**In a CPU-bound workload, there's no advantage to processing multiple requests in parallel in the same instance. This limitation means that you're better off distributing each request to its own instance so requests complete as quickly as possible without contention. In this scenario, set a low[HTTP trigger concurrency](functions-concurrency#http-trigger-concurrency)of`1`

. With 10 concurrent requests, the app scales to a steady state of roughly 10 instances, and each instance is continuously active processing one request at a time.Because the size of each instance is ~2 GB, the consumption for a single continuously active instance is

`2 GB * 3600 s = 7200 GB-s`

. Assuming an on-demand execution rate of $0.000026 GB-s (without any free grants applied), the cost becomes`$0.1872 USD`

per hour per instance. Because the CPU-bound app scales to 10 instances, the total hourly rate for execution time is`$1.872 USD`

.Similarly, the on-demand per-execution charge (without any free grants) of 40 requests per second is equal to

`40 * 3600 = 144,000`

or`0.144 million`

executions per hour. Assuming an on-demand rate of`$0.40`

per million executions, the total (grant-free) hourly cost of executions is`0.144 * $0.40`

, which is`$0.0576`

per hour.In this scenario, the total hourly cost of running on-demand on 10 instances is

`$1.872 + $0.0576s = $1.9296 USD`

.**IO bound workload:**In an IO-bound workload, most of the application time is spent waiting on incoming request, which might be limited by network throughput or other upstream factors. Because of the limited inputs, the code can process multiple operations concurrently without negative impacts. In this scenario, assume you can process all 10 concurrent requests on the same instance.Because consumption charges are based only on the memory of each active instance, the consumption charge calculation is simply

`2 GB * 3600 s = 7200 GB-s`

, which at the assumed on-demand execution rate (without any free grants applied) is`$0.1872 USD`

per hour for the single instance.As in the CPU-bound scenario, the on-demand per-execution charge (without any free grants) of 40 requests per second is equal to

`40 * 3600 = 144,000`

or 0.144 million executions per hour. In this case, the total (grant-free) hourly cost of executions`0.144 * $0.40`

, which is`$0.0576`

per hour.In this scenario, the total hourly cost of running on-demand a single instance is

`$0.1872 + $0.0576 = $0.245 USD`

.

## Behaviors affecting execution time

The following behaviors of your functions can affect the execution time:

**Triggers and bindings**: The time taken to read input from and write output to your[function bindings](functions-triggers-bindings)counts as execution time. For example, when your function uses an output binding to write a message to an Azure storage queue, your execution time includes the time taken to write the message to the queue, which is included in the calculation of the function cost.**Asynchronous execution**: The time that your function waits for the results of an async request (`await`

in C#) counts as execution time. The GB-second calculation is based on the start and end time of the function and the memory usage over that period. What happens over that time in terms of CPU activity isn't factored into the calculation. You might be able to reduce costs during asynchronous operations by using[Durable Functions](durable/durable-functions-overview). You're not billed for time spent at awaits in orchestrator functions.

## Viewing and estimating costs from metrics

In [your invoice](../cost-management-billing/understand/download-azure-invoice), you can view the cost-related data along with the actual billed costs. However, this invoice data is a monthly aggregate for a past invoice period.

This section shows you how to use metrics, both app-level and function executions, to estimate costs for running your function apps.

### Function app-level metrics

The app-level metrics available to your app depend on the type of consumption plan you use.

These Azure Monitor metrics are related to Flex Consumption plan billing:

| Metric | Description | Meter calculation |
|---|---|---|
On Demand Function Execution Count |
Total number of function executions in on demand instances. | `OnDemandFunctionExecutionCount` relates to the On Demand Total Executions meter. |
Always Ready Function Execution Count |
Total number of function executions in always ready instances. | `AlwaysReadyFunctionExecutionCount` relates to the Always Ready Total Executions meter. |
On Demand Function Execution Units |
Total MB-milliseconds from on demand instances while actively executing functions. | `OnDemandFunctionExecutionUnits / 1,024,000` is the On Demand Execution Time meter, in GB-seconds. |
Always Ready Function Execution Units |
Total MB-milliseconds from always ready instances while actively executing functions. | `AlwaysReadyFunctionExecutionUnits / 1,024,000` is the Always Ready Execution Time meter, in GB-seconds. |
Always Ready Units |
The total MB-milliseconds of always ready instances assigned to the app, whether or not functions are actively executing. | `AlwaysReadyUnits / 1,024,000` is the Always Ready Baseline meter, in GB-seconds. |

For more information, see [Azure Functions monitoring data reference](monitor-functions-reference).

To better understand the costs of your functions, use Azure Monitor to view cost-related metrics that your function apps generate. You can view Monitor metrics by using one of these tools:

Use [Azure Monitor metrics explorer](/en-us/azure/azure-monitor/essentials/metrics-getting-started) to view cost-related data for your Flex Consumption plan function apps in a graphical format.

In the

[Azure portal](https://portal.azure.com), go to your function app.In the left panel, scroll down to

**Monitoring**and select**Metrics**.From

**Metric**, select**On Demand Function Execution Count**and**Sum**for**Aggregation**. This selection adds the sum of the execution counts during the chosen period to the chart.Select

**Add metric**and add**On Demand Function Execution Units**,**Always Ready Function Execution Count**,**Always Ready Function Execution Units**, and**Always Ready Units**to the chart.

The resulting chart contains the totals for all the Flex Consumption execution metrics in the chosen time range, which in this example is a custom time range.

Because the number of On Demand Function Execution Units is greater than On Demand Function Execution Count, and there were no [always ready instances](flex-consumption-plan#always-ready-instances) on the app, the chart just shows On Demand Function Execution Units.

This chart shows a total of 3.54 billion `On Demand Function Execution Units`

consumed in a 16-minute period, measured in MB-milliseconds. To convert to GB-seconds, divide by 1,024,000. In this example, the function app consumed `3,540,000,000 / 1,024,000 = 3,457.03`

GB-seconds. You can take this value and multiply it by the current price of On Demand Execution Time on the [Functions pricing page](https://azure.microsoft.com/pricing/details/functions/), which gives you the cost of these 16 minutes, assuming you already used any free grants of execution time. You can use this same calculation with the The Always Ready Function Execution Units metric and the Always Ready Execution Time billing meter cost, as well as with the Always Ready Units metric and the Always Ready Baseline billing meter cost, to find out the GB-seconds costs for always ready instances.

To calculate the On Demand Total Executions cost, take the On Demand Function Execution Count sum for the same time period, convert to millions, and then multiply by the On Demand Total Executions price on the [Functions pricing page](https://azure.microsoft.com/pricing/details/functions/). For example, 2,100 executions in the example above converts to `0.0021`

million executions. You can use this same calculation with the Always Ready Function Execution Count metric and the Always Ready Total Executions billing meter to find out the cost for executions handled by always ready instance.

### Function-level metrics

Memory usage is important when estimating costs of your function executions. However, the way memory usage impacts your costs depends on the specific plan type:

In the Flex Consumption plan, you pay for the time the instance runs based on your chosen [instance size](flex-consumption-plan#instance-sizes), which has a set memory limit. For more information, see [Billing](flex-consumption-plan#billing).

If you haven't already done so, [enable Application Insights in your function app](configure-monitoring#enable-application-insights-integration). With this integration enabled, you can [query this telemetry data in the portal](analyze-telemetry-data#query-telemetry-data).

You can use either [Azure Monitor metrics explorer](/en-us/azure/azure-monitor/essentials/metrics-getting-started) in the [Azure portal](https://portal.azure.com) or REST APIs to get Monitor Metrics data.

#### Determine memory usage

Under **Monitoring**, select **Logs (Analytics)**, then copy the following telemetry query and paste it into the query window and select **Run**. This query returns the total memory usage at each sampled time.

```
performanceCounters
| where name == "Private Bytes"
| project timestamp, name, value
```


The results look like the following example:

| timestamp [UTC] | name | value |
|---|---|---|
| 9/12/2019, 1:05:14.947 AM | Private Bytes | 209,932,288 |
| 9/12/2019, 1:06:14.994 AM | Private Bytes | 212,189,184 |
| 9/12/2019, 1:06:30.010 AM | Private Bytes | 231,714,816 |
| 9/12/2019, 1:07:15.040 AM | Private Bytes | 210,591,744 |
| 9/12/2019, 1:12:16.285 AM | Private Bytes | 216,285,184 |
| 9/12/2019, 1:12:31.376 AM | Private Bytes | 235,806,720 |

#### Determine duration

Azure Monitor tracks metrics at the resource level, which for Functions is the function app. Application Insights integration emits metrics on a per-function basis. Here's an example analytics query to get the average duration of a function:

```
customMetrics
| where name contains "Duration"
| extend averageDuration = valueSum / valueCount
| summarize averageDurationMilliseconds=avg(averageDuration) by name
```


| name | averageDurationMilliseconds |
|---|---|
| QueueTrigger AvgDurationMs | 16.087 |
| QueueTrigger MaxDurationMs | 90.249 |
| QueueTrigger MinDurationMs | 8.522 |

## Other related costs

When estimating the overall cost of running your functions in any plan, remember that the Functions runtime uses several other Azure services, which are each billed separately. When you estimate pricing for function apps, any triggers and bindings you have that integrate with other Azure services require you to create and pay for those other services.

For functions running in a Consumption plan, the total cost is the execution cost of your functions, plus the cost of bandwidth and other services.

When estimating the overall costs of your function app and related services, use the [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?service=functions).

| Related cost | Description |
|---|---|
Storage account |
Each function app requires that you have an associated General Purpose
|

**Application Insights**[Application Insights](/en-us/azure/azure-monitor/app/app-insights-overview)to provide a high-performance monitoring experience for your function apps. While not required, you should[enable Application Insights integration](configure-monitoring#enable-application-insights-integration). A free grant of telemetry data is included every month. To learn more, see[the Azure Monitor pricing page](https://azure.microsoft.com/pricing/details/monitor/).**Network bandwidth**

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/configure-monitoring -->

# How to configure monitoring for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions integrates with Application Insights to better enable you to monitor your function apps. Application Insights, a feature of Azure Monitor, is an extensible Application Performance Management (APM) service that collects data generated by your function app, including information your app writes to logs. Application Insights integration is typically enabled when your function app is created. If your app doesn't have the instrumentation key set, you must first [enable Application Insights integration](#enable-application-insights-integration).

You can use Application Insights without any custom configuration. However, the default configuration can result in high volumes of data. If you're using a Visual Studio Azure subscription, you might hit your data cap for Application Insights. For information about Application Insights costs, see [Application Insights billing](/en-us/azure/azure-monitor/logs/cost-logs#application-insights-billing). For more information, see [Solutions with high-volume of telemetry](#solutions-with-high-volume-of-telemetry).

In this article, you learn how to configure and customize the data that your functions send to Application Insights. You can set common logging configurations in the * host.json* file. By default, these settings also govern custom logs emitted by your code. However, in some cases this behavior can be disabled in favor of options that give you more control over logging. For more information, see

[Custom application logs](#custom-application-logs).

Note

You can use specially configured application settings to represent specific settings in a *host.json* file for a particular environment. Doing so lets you effectively change *host.json* settings without needing to republish the *host.json* file in your project. For more information, see [Override host.json values](functions-host-json#override-hostjson-values).

## Custom application logs

By default, custom application logs you write are sent to the Functions host, which then sends them to Application Insights under the [Worker category](#configure-categories). Some language stacks allow you to instead send the logs directly to Application Insights, which gives you full control over how logs you write are emitted. In this case, the logging pipeline changes from `worker -> Functions host -> Application Insights`

to `worker -> Application Insights`

.

The following table summarizes the configuration options available for each stack:

| Language stack | Where to configure custom logs |
|---|---|
| .NET (in-process model) | `host.json` |
| .NET (isolated model) | Default (send custom logs to the Functions host): `host.json` To send logs directly to Application Insights, see:
|
| Node.js | `host.json` |
| Python | `host.json` |
| Java | Default (send custom logs to the Functions host): `host.json` To send logs directly to Application Insights, see:
|
| PowerShell | `host.json` |

When you configure custom application logs to be sent directly, the host no longer emits them, and `host.json`

no longer controls their behavior. Similarly, the options exposed by each stack apply only to custom logs, and they don't change the behavior of the other runtime logs described in this article. In this case, to control the behavior of all logs, you might need to make changes in both configurations.

## Configure categories

The Azure Functions logger includes a *category* for every log. The category indicates which part of the runtime code or your function code wrote the log. Categories differ between version 1.x and later versions.

Category names are assigned differently in Functions compared to other .NET frameworks. For example, when you use `ILogger<T>`

in ASP.NET, the category is the name of the generic type. C# functions also use `ILogger<T>`

, but instead of setting the generic type name as a category, the runtime assigns categories based on the source. For example:

- Entries related to running a function are assigned a category of
`Function.<FUNCTION_NAME>`

. - Entries created by user code inside the function, such as when calling
`logger.LogInformation()`

, are assigned a category of`Function.<FUNCTION_NAME>.User`

.

The following table describes the main categories of logs that the runtime creates:

| Category | Table | Description |
|---|---|---|
`Function` |
traces |
Includes function started and completed logs for all function runs. For successful runs, these logs are at the `Information` level. Exceptions are logged at the `Error` level. The runtime also creates `Warning` level logs, such as when queue messages are sent to the
|
`Function.<YOUR_FUNCTION_NAME>` |
dependencies |
Dependency data is automatically collected for some services. For successful runs, these logs are at the `Information` level. For more information, see
`Error` level. The runtime also creates `Warning` level logs, such as when queue messages are sent to the
|
`Function.<YOUR_FUNCTION_NAME>` |
customMetricscustomEvents |
C# and JavaScript SDKs lets you collect custom metrics and log custom events. For more information, see
|

`Function.<YOUR_FUNCTION_NAME>`

**traces**`Information`

level. Exceptions are logged at the `Error`

level. The runtime also creates `Warning`

level logs, such as when queue messages are sent to the [poison queue](functions-bindings-storage-queue-trigger#poison-messages).`Function.<YOUR_FUNCTION_NAME>.User`

**traces**[Writing to logs](functions-monitoring#writing-to-logs).`Host.Aggregator`

**customMetrics**[configurable](#configure-the-aggregator)period of time. The default period is 30 seconds or 1,000 results, whichever comes first. Examples are the number of runs, success rate, and duration. All of these logs are written at the`Information`

level. If you filter at `Warning`

or higher, you don't see any of this data.`Host.Results`

**requests**`Information`

level. If you filter at `Warning`

or higher, you don't see any of this data.`Microsoft`

**traces**`Worker`

**traces**`Microsoft.*`

category, such as `Microsoft.Azure.WebJobs.Script.Workers.Rpc.RpcFunctionInvocationDispatcher`

. These logs are written at the `Information`

level.Note

For .NET class library functions, these categories assume you're using `ILogger`

and not `ILogger<T>`

. For more information, see the [Functions ILogger documentation](functions-dotnet-class-library#ilogger).

The **Table** column indicates to which table in Application Insights the log is written.

## Configure log levels

A *log level* is assigned to every log. The value is an integer that indicates relative importance:

| LogLevel | Code | Description |
|---|---|---|
| Trace | 0 | Logs that contain the most detailed messages. These messages might contain sensitive application data. These messages are disabled by default and should never be enabled in a production environment. |
| Debug | 1 | Logs that are used for interactive investigation during development. These logs should primarily contain information useful for debugging and have no long-term value. |
| Information | 2 | Logs that track the general flow of the application. These logs should have long-term value. |
| Warning | 3 | Logs that highlight an abnormal or unexpected event in the application flow, but don't otherwise cause the application execution to stop. |
| Error | 4 | Logs that highlight when the current flow of execution is stopped because of a failure. These errors should indicate a failure in the current activity, not an application-wide failure. |
| Critical | 5 | Logs that describe an unrecoverable application or system crash, or a catastrophic failure that requires immediate attention. |
| None | 6 | Disables logging for the specified category. |

The [ host.json file](functions-host-json) configuration determines how much logging a functions app sends to Application Insights.

For each category, you indicate the minimum log level to send. The *host.json* settings vary depending on the [Functions runtime version](functions-versions).

The following examples define logging based on the following rules:

- The default logging level is set to
`Warning`

to prevent[excessive logging](#solutions-with-high-volume-of-telemetry)for unanticipated categories. `Host.Aggregator`

and`Host.Results`

are set to lower levels. Setting logging levels too high (especially higher than`Information`

) can result in loss of metrics and performance data.- Logging for function runs is set to
`Information`

. If necessary, you can[override](functions-host-json#override-hostjson-values)this setting in local development to`Debug`

or`Trace`

.

```
{
"logging": {
"fileLoggingMode": "debugOnly",
"logLevel": {
"default": "Warning",
"Host.Aggregator": "Trace",
"Host.Results": "Information",
"Function": "Information"
}
}
}
```


If * host.json* includes multiple logs that start with the same string, the more defined logs ones are matched first. Consider the following example that logs everything in the runtime, except

`Host.Aggregator`

, at the `Error`

level:```
{
"logging": {
"fileLoggingMode": "debugOnly",
"logLevel": {
"default": "Information",
"Host": "Error",
"Function": "Error",
"Host.Aggregator": "Information"
}
}
}
```


You can use a log level setting of `None`

to prevent any logs from being written for a category.

Caution

Azure Functions integrates with Application Insights by storing telemetry events in Application Insights tables. If you set a category log level to any value different from `Information`

, it prevents the telemetry from flowing to those tables, and you won't be able to see related data in the **Application Insights** and **Function Monitor** tabs.

For example, for the previous samples:

- If you set the
`Host.Results`

category to the`Error`

log level, Azure gathers only host execution telemetry events in the`requests`

table for failed function executions, preventing the display of host execution details of successful executions in both the**Application Insights**and**Function Monitor**tabs. - If you set the
`Function`

category to the`Error`

log level, it stops gathering function telemetry data related to`dependencies`

,`customMetrics`

, and`customEvents`

for all the functions, preventing you from viewing any of this data in Application Insights. Azure gathers only`traces`

logged at the`Error`

level.

In both cases, Azure continues to collect errors and exceptions data in the **Application Insights** and **Function Monitor** tabs. For more information, see [Solutions with high-volume of telemetry](#solutions-with-high-volume-of-telemetry).

## Configure the aggregator

As noted in the previous section, the runtime aggregates data about function executions over a period of time. The default period is 30 seconds or 1,000 runs, whichever comes first. You can configure this setting in the * host.json* file. For example:

```
{
"aggregator": {
"batchSize": 1000,
"flushTimeout": "00:00:30"
}
}
```


## Configure sampling

Application Insights has a [sampling](/en-us/azure/azure-monitor/app/sampling) feature that can protect you from producing too much telemetry data on completed executions at times of peak load. When the rate of incoming executions exceeds a specified threshold, Application Insights starts to randomly ignore some of the incoming executions. The default setting for maximum number of executions per second is 20 (five in version 1.x). You can configure sampling in [ host.json](functions-host-json#applicationinsights). Here's an example:

```
{
"logging": {
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"maxTelemetryItemsPerSecond" : 20,
"excludedTypes": "Request;Exception"
}
}
}
}
```


You can exclude certain types of telemetry from sampling. In this example, data of type `Request`

and `Exception`

is excluded from sampling. It ensures that *all* function executions (requests) and exceptions are logged while other types of telemetry remain subject to sampling.

If your project uses a dependency on the Application Insights SDK to do manual telemetry tracking, you might experience unusual behavior if your sampling configuration differs from the sampling configuration in your function app. In such cases, use the same sampling configuration as the function app. For more information, see [Sampling in Application Insights](/en-us/azure/azure-monitor/app/sampling).

## Enable SQL query collection

Application Insights automatically collects data on dependencies for HTTP requests, database calls, and for several bindings. For more information, see [Dependencies](functions-monitoring#dependencies). For SQL calls, the name of the server and database is always collected and stored, but SQL query text isn't collected by default. You can use `dependencyTrackingOptions.enableSqlCommandTextInstrumentation`

to enable SQL query text logging by using the following settings (at a minimum) in your [host.json file](functions-host-json#applicationinsightsdependencytrackingoptions):

```
"logging": {
"applicationInsights": {
"enableDependencyTracking": true,
"dependencyTrackingOptions": {
"enableSqlCommandTextInstrumentation": true
}
}
}
```


For more information, see [Advanced SQL tracking to get full SQL query](/en-us/azure/azure-monitor/app/asp-net-dependencies#advanced-sql-tracking-to-get-full-sql-query).

## Configure scale controller logs

*This feature is in preview.*

You can have the [Azure Functions scale controller](event-driven-scaling#runtime-scaling) emit logs to either Application Insights or to Blob storage to better understand the decisions the scale controller is making for your function app.

To enable this feature, add an application setting named `SCALE_CONTROLLER_LOGGING_ENABLED`

to your function app settings. The following value of the setting must be in the format `<DESTINATION>:<VERBOSITY>`

. For more information, see the following table:

| Property | Description |
|---|---|
`<DESTINATION>` |
The destination to which logs are sent. Valid values are `AppInsights` and `Blob` .When you use `AppInsights` , ensure that the
When you set the destination to `Blob` , logs are created in a blob container named `azure-functions-scale-controller` in the default storage account set in the `AzureWebJobsStorage` application setting. |
`<VERBOSITY>` |
Specifies the level of logging. Supported values are `None` , `Warning` , and `Verbose` .When set to `Verbose` , the scale controller logs a reason for every change in the worker count, and information about the triggers that factor into those decisions. Verbose logs include trigger warnings and the hashes used by the triggers before and after the scale controller runs. |

Tip

Keep in mind that while you leave scale controller logging enabled, it impacts the [potential costs of monitoring your function app](functions-monitoring#application-insights-pricing-and-limits). Consider enabling logging until you collect enough data to understand how the scale controller is behaving, and then disabling it.

For example, the following Azure CLI command turns on verbose logging from the scale controller to Application Insights:

```
az functionapp config appsettings set --name <FUNCTION_APP_NAME> \
--resource-group <RESOURCE_GROUP_NAME> \
--settings SCALE_CONTROLLER_LOGGING_ENABLED=AppInsights:Verbose
```


In this example, replace `<FUNCTION_APP_NAME>`

and `<RESOURCE_GROUP_NAME>`

with the name of your function app and the resource group name, respectively.

The following Azure CLI command disables logging by setting the verbosity to `None`

:

```
az functionapp config appsettings set --name <FUNCTION_APP_NAME> \
--resource-group <RESOURCE_GROUP_NAME> \
--settings SCALE_CONTROLLER_LOGGING_ENABLED=AppInsights:None
```


You can also disable logging by removing the `SCALE_CONTROLLER_LOGGING_ENABLED`

setting using the following Azure CLI command:

```
az functionapp config appsettings delete --name <FUNCTION_APP_NAME> \
--resource-group <RESOURCE_GROUP_NAME> \
--setting-names SCALE_CONTROLLER_LOGGING_ENABLED
```


With scale controller logging enabled, you're now able to [query your scale controller logs](analyze-telemetry-data#query-scale-controller-logs).

## Enable Application Insights integration

For a function app to send data to Application Insights, it needs to connect to the Application Insights resource using **only one** of these application settings:

| Setting name | Description |
|---|---|
`APPLICATIONINSIGHTS_CONNECTION_STRING` |
This setting is recommended and is required when your Application Insights instance runs in a sovereign cloud. The connection string supports other
|

`APPINSIGHTS_INSTRUMENTATIONKEY`

When you create your function app in the [Azure portal](functions-get-started) from the command line by using [Azure Functions Core Tools](how-to-create-function-azure-cli?pivots=programming-language-csharp) or [Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-csharp), Application Insights integration is enabled by default. The Application Insights resource has the same name as your function app, and is created either in the same region or in the nearest region.

### Require Microsoft Entra authentication

You can use the [ APPLICATIONINSIGHTS_AUTHENTICATION_STRING](functions-app-settings#applicationinsights_authentication_string) setting to enable connections to Application Insights using Microsoft Entra authentication. This creates a consistent authentication experience across all Application Insights pipelines, including Profiler and Snapshot Debugger, as well as from the Functions host and language-specific agents.

Note

There's currently no Microsoft Entra ID authentication support for local development.

When Ingesting data in a sovereign cloud, Microsoft Entra ID authentication isn't available when using the Application Insights SDK. OpenTelemetry-based data collection supports Microsoft Entra ID authentication across all cloud environments, including sovereign clouds.

The value contains either `Authorization=AAD`

for a system-assigned managed identity or `ClientId=<YOUR_CLIENT_ID>;Authorization=AAD`

for a user-assigned managed identity. The managed identity must already be available to the function app, with an assigned role equivalent to [Monitoring Metrics Publisher](/en-us/azure/role-based-access-control/built-in-roles/monitor#monitoring-metrics-publisher). For more information, see [Microsoft Entra authentication for Application Insights](/en-us/azure/azure-monitor/app/azure-ad-authentication).

The [ APPLICATIONINSIGHTS_CONNECTION_STRING](functions-app-settings#applicationinsights_connection_string) setting is still required.

Note

When using `APPLICATIONINSIGHTS_AUTHENTICATION_STRING`

to connect to Application Insights using Microsoft Entra authentication, you should also [Disable local authentication for Application Insights](/en-us/azure/azure-monitor/app/azure-ad-authentication#disable-local-authentication). This configuration requires Microsoft Entra authentication in order for telemetry to be ingested into your workspace.

### New function app in the portal

To review the Application Insights resource being created, select it to expand the **Application Insights** window. You can change the **New resource name** or select a different **Location** in an [Azure geography](https://azure.microsoft.com/global-infrastructure/geographies/) where you want to store your data.


When you select **Create**, an Application Insights resource is created with your function app, which has the `APPLICATIONINSIGHTS_CONNECTION_STRING`

set in application settings. Everything is ready to go.

### Add to an existing function app

If an Application Insights resource wasn't created with your function app, use the following steps to create the resource. You can then add the connection string from that resource as an [application setting](functions-how-to-use-azure-function-app-settings#settings) in your function app.

In the

[Azure portal](https://portal.azure.com), search for and select**function app**, and then select your function app.Select the

**Application Insights is not configured**banner at the top of the window. If you don't see this banner, then your app might already have Application Insights enabled.Expand

**Change your resource**and create an Application Insights resource by using the settings specified in the following table:Setting Suggested value Description **New resource name**Unique app name It's easiest to use the same name as your function app, which must be unique in your subscription. **Location**West Europe If possible, use the same [region](https://azure.microsoft.com/regions/)as your function app, or the one that's close to that region.Select

**Apply**.The Application Insights resource is created in the same resource group and subscription as your function app. After the resource is created, close the

**Application Insights**window.In your function app, expand

**Settings**, and then select**Environment variables**. In the**App settings**tab, if you see an app setting named`APPLICATIONINSIGHTS_CONNECTION_STRING`

, Application Insights integration is enabled for your function app running in Azure. If this setting doesn't exist, add it by using your Application Insights connection string as the value.

Note

Older function apps might use `APPINSIGHTS_INSTRUMENTATIONKEY`

instead of `APPLICATIONINSIGHTS_CONNECTION_STRING`

. When possible, update your app to use the connection string instead of the instrumentation key.

## Disable built-in logging

Early versions of Functions used built-in monitoring, which is no longer recommended. When you enable Application Insights, disable the built-in logging that uses Azure Storage. The built-in logging is useful for testing with light workloads, but isn't intended for high-load production use. For production monitoring, we recommend Application Insights. If you use built-in logging in production, the logging record might be incomplete because of throttling on Azure Storage.

To disable built-in logging, delete the `AzureWebJobsDashboard`

app setting. For more information about how to delete app settings in the Azure portal, see the **Application settings** section of [How to manage a function app](functions-how-to-use-azure-function-app-settings#settings). Before you delete the app setting, ensure that no existing functions in the same function app use the setting for Azure Storage triggers or bindings.

## Solutions with high volume of telemetry

Function apps are an essential part of solutions that can cause high volumes of telemetry, such as IoT solutions, rapid event driven solutions, high load financial systems, and integration systems. In this case, you should consider extra configuration to reduce costs while maintaining observability.

The generated telemetry can be consumed in real-time dashboards, alerting, detailed diagnostics, and so on. Depending on how the generated telemetry is consumed, you need to define a strategy to reduce the volume of data generated. This strategy allows you to properly monitor, operate, and diagnose your function apps in production. Consider the following options:

**Use the correct table plan**:[Table plans](/en-us/azure/azure-monitor/logs/data-platform-logs#table-plans)help you manage data costs by controlling how often you use the data in a table and the kind of analysis you need to perform. To reduce costs, you can choose the`Basic`

plan, which does lack some features available in the`Analytics`

plan.**Use sampling**: As mentioned[previously](#configure-sampling), sampling helps to dramatically reduce the volume of telemetry events ingested while maintaining a statistically correct analysis. It could happen that even using sampling you still get a high volume of telemetry. Inspect the options that[adaptive sampling](/en-us/azure/azure-monitor/app/sampling#configuring-adaptive-sampling-for-aspnet-applications)provides to you. For example, set the`maxTelemetryItemsPerSecond`

to a value that balances the volume generated with your monitoring needs. Keep in mind that the telemetry sampling is applied per host executing your function app.**Default log level**: Use`Warning`

or`Error`

as the default value for all telemetry categories. Later, you can decide which[categories](#configure-categories)you want to set at the`Information`

level, so that you can monitor and diagnose your functions properly.**Tune your functions telemetry**: With the default log level set to`Error`

or`Warning`

, no detailed information from each function is gathered (dependencies, custom metrics, custom events, and traces). For those functions that are key for production monitoring, define an explicit entry for the`Function.<YOUR_FUNCTION_NAME>`

category and set it to`Information`

, so that you can gather detailed information. To avoid gathering[user-generated logs](functions-monitoring#writing-to-logs)at the`Information`

level, set the`Function.<YOUR_FUNCTION_NAME>.User`

category to the`Error`

or`Warning`

log level.**Host.Aggregator category**: As described in[configure categories](#configure-categories), this category provides aggregated information of function invocations. The information from this category is gathered in the Application Insights`customMetrics`

table, and is shown in the function**Overview**tab in the Azure portal. Depending on how you configure the aggregator, consider that there can be a delay, determined by the`flushTimeout`

setting, in the telemetry gathered. If you set this category to a value different from`Information`

, you stop gathering the data in the`customMetrics`

table and don't display metrics in the function**Overview**tab.The following screenshot shows

`Host.Aggregator`

telemetry data displayed in the function**Overview**tab:The following screenshot shows

`Host.Aggregator`

telemetry data in Application Insights`customMetrics`

table:**Host.Results category**: As described in[configure categories](#configure-categories), this category provides the runtime-generated logs indicating the success or failure of a function invocation. The information from this category is gathered in the Application Insights`requests`

table, and is shown in the function**Monitor**tab and in different Application Insights dashboards (Performance, Failures, and so on). If you set this category to a value different than`Information`

, you gather only telemetry generated at the log level defined (or higher). For example, setting it to`error`

results in tracking requests data only for failed executions.The following screenshot shows the

`Host.Results`

telemetry data displayed in the function**Monitor**tab:The following screenshot shows

`Host.Results`

telemetry data displayed in Application Insights Performance dashboard:**Host.Aggregator vs Host.Results**: Both categories provide good insights about function executions. If needed, you can remove the detailed information from one of these categories, so that you can use the other for monitoring and alerting. Here's a sample:

```
{
"version": "2.0",
"logging": {
"logLevel": {
"default": "Warning",
"Function": "Error",
"Host.Aggregator": "Error",
"Host.Results": "Information",
"Function.Function1": "Information",
"Function.Function1.User": "Error"
},
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"maxTelemetryItemsPerSecond": 1,
"excludedTypes": "Exception"
}
}
}
}
```


With this configuration:

The default value for all functions and telemetry categories is set to

`Warning`

(including Microsoft and Worker categories). So, by default, all errors and warnings generated by runtime and custom logging are gathered.The

`Function`

category log level is set to`Error`

, so for all functions, by default, only exceptions and error logs are gathered. Dependencies, user-generated metrics, and user-generated events are skipped.For the

`Host.Aggregator`

category, as it's set to the`Error`

log level, aggregated information from function invocations isn't gathered in the`customMetrics`

Application Insights table, and information about executions counts (total, successful, and failed) aren't shown in the function overview dashboard.For the

`Host.Results`

category, all the host execution information is gathered in the`requests`

Application Insights table. All the invocations results are shown in the function Monitor dashboard and in Application Insights dashboards.For the function called

`Function1`

, we set the log level to`Information`

. So, for this concrete function, all the telemetry is gathered (dependency, custom metrics, and custom events). For the same function, we set the`Function1.User`

category (user-generated traces) to`Error`

, so only custom error logging is gathered.Note

Configuration per function isn't supported in v1.x of the Functions runtime.

Sampling is configured to send one telemetry item per second per type, excluding the exceptions. This sampling happens for each server host running our function app. So, if we have four instances, this configuration emits four telemetry items per second per type and all the exceptions that might occur.

Note

Metric counts such as request rate and exception rate are adjusted to compensate for the sampling rate, so that they show approximately correct values in Metric Explorer.


Tip

Experiment with different configurations to ensure that you cover your requirements for logging, monitoring, and alerting. Also, ensure that you have detailed diagnostics in case of unexpected errors or malfunctioning.

## Overriding monitoring configuration at runtime

Finally, there could be situations where you need to quickly change the logging behavior of a certain category in production, and you don't want to make a whole deployment just for a change in the *host.json* file. For such cases, you can override the [host.json values](functions-host-json#override-hostjson-values).

To configure these values at App settings level (and avoid redeployment on just *host.json* changes), you should override specific `host.json`

values by creating an equivalent value as an application setting. When the runtime finds an application setting in the format `AzureFunctionsJobHost__path__to__setting`

, it overrides the equivalent `host.json`

setting located at `path.to.setting`

in the JSON. When expressed as an application setting, a double underscore (`__`

) replaces the dot (`.`

) used to indicate JSON hierarchy. For example, you can use the following app settings to configure individual function log levels in `host.json`

.

| Host.json path | App setting |
|---|---|
| logging.logLevel.default | AzureFunctionsJobHost__logging__logLevel__default |
| logging.logLevel.Host.Aggregator | AzureFunctionsJobHost__logging__logLevel__Host.Aggregator |
| logging.logLevel.Function | AzureFunctionsJobHost__logging__logLevel__Function |
| logging.logLevel.Function.Function1 | AzureFunctionsJobHost__logging__logLevel__Function.Function1 |
| logging.logLevel.Function.Function1.User | AzureFunctionsJobHost__logging__logLevel__Function.Function1.User |

You can override the settings directly at the Azure portal Function App Configuration pane or by using an Azure CLI or PowerShell script.

```
az functionapp config appsettings set --name MyFunctionApp --resource-group MyResourceGroup --settings "AzureFunctionsJobHost__logging__logLevel__Host.Aggregator=Information"
```


Note

Overriding the `host.json`

through changing app settings will restart your function app.
App settings that contain a period aren't supported when running on Linux in an Elastic Premium plan or a Dedicated (App Service) plan. In these hosting environments, you should continue to use the *host.json* file.

## Monitor function apps using Health check

You can use the Health Check feature to monitor function apps on the Premium (Elastic Premium) and Dedicated (App Service) plans. Health check isn't an option for the Flex Consumption and Consumption plans. To learn how to configure it, see [Monitor App Service instances using Health check](../app-service/monitor-instances-health-check). Your function app should have an HTTP trigger function that responds with an HTTP status code of 200 on the same endpoint as configured on the `Path`

parameter of the health check. You can also have that function perform extra checks to ensure that dependent services are reachable and working.

## Related content

For more information about monitoring, see:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/event-grid-how-tos -->

# How to work with Event Grid triggers and bindings in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions provides built-in integration with Azure Event Grid by using [triggers and bindings](functions-triggers-bindings). This article shows you how to configure and locally evaluate your Event Grid trigger and bindings. For more information about Event Grid trigger and output binding definitions and examples, see one of the following reference articles:

[Azure Event Grid bindings Overview](functions-bindings-event-grid)[Azure Event Grid trigger for Azure Functions](functions-bindings-event-grid-trigger)[Azure Event Grid output binding for Azure Functions](functions-bindings-event-grid-output)

## Create an event subscription

To start receiving Event Grid HTTP requests, you need a subscription to events raised by Event Grid. Event subscriptions specify the endpoint URL that invokes the function. When you create an event subscription from your function's **Integration** tab in the [Azure portal](https://portal.azure.com), the URL is supplied for you. When you programmatically create an event subscription or when you create the event subscription from Event Grid, you'll need to provide the endpoint. The endpoint URL contains a system key, which you must obtain from Functions administrator REST APIs.

## Get the webhook endpoint URL

The URL endpoint for your Event Grid triggered function depends on the version of the Functions runtime. The following example shows the version-specific URL pattern:

```
https://{functionappname}.azurewebsites.net/runtime/webhooks/eventgrid?functionName={functionname}&code={systemkey}
```


Note

There is a version of the Blob storage trigger that also uses event subscriptions. The endpoint URL for this kind of Blob storage trigger has a path of `/runtime/webhooks/blobs`

, whereas the path for an Event Grid trigger would be `/runtime/webhooks/EventGrid`

. For a comparison of options for processing blobs, see [Trigger on a blob container](storage-considerations#trigger-on-a-blob-container).

## Obtain the system key

The URL endpoint you construct includes a system key value. The system key is an authorization key, specific to the Event Grid webhook, that must be included in a request to the endpoint URL for an Event Grid trigger. The following section explains how to get the system key.

You can also get the master key for your function app from **Functions** > **App keys** in the portal.

Caution

The master key provides administrator access to your function app. Don't share this key with third parties or distribute it in native client applications.

For more information, see [Work with access keys in Azure Functions](function-keys-how-to).

You can get the system key from your function app by using the following administrator APIs (HTTP GET):

```
http://{functionappname}.azurewebsites.net/admin/host/systemkeys/eventgrid_extension?code={masterkey}
```


This REST API is an administrator API, so it requires your function app [master key](function-keys-how-to). Don't confuse the system key (for invoking an Event Grid trigger function) with the master key (for performing administrative tasks on the function app). When you subscribe to an Event Grid topic, be sure to use the system key.

Here's an example of the response that provides the system key:

```
{
"name": "eventgridextensionconfig_extension",
"value": "{the system key for the function}",
"links": [
{
"rel": "self",
"href": "{the URL for the function, without the system key}"
}
]
}
```


## Create the subscription

You can create an event subscription either from the [Azure portal](https://portal.azure.com) or by using the Azure CLI.

For functions that you develop in the Azure portal with the Event Grid trigger, select **Integration** then choose the **Event Grid Trigger** and select **Create Event Grid subscription**.


When you select this link, the portal opens the **Create Event Subscription** page with the current trigger endpoint already defined.


For more information about how to create subscriptions by using the Azure portal, see [Create custom event - Azure portal](../event-grid/custom-event-quickstart-portal) in the Event Grid documentation.

For more information about how to create a subscription, see [the blob storage quickstart](../storage/blobs/storage-blob-event-quickstart#subscribe-to-your-storage-account) or the other Event Grid quickstarts.

## Local testing with viewer web app

To test an Event Grid trigger locally, you have to get Event Grid HTTP requests delivered from their origin in the cloud to your local machine. One way to do that is by capturing requests online and manually resending them on your local machine:

[Create a viewer web app](#create-a-viewer-web-app)that captures event messages.[Create an Event Grid subscription](#create-an-event-grid-subscription)that sends events to the viewer app.[Generate a request](#generate-a-request)and copy the request body from the viewer app.[Manually post the request](#manually-post-the-request)to the localhost URL of your Event Grid trigger function.

To send an HTTP post request, you need an HTTP test tool. Make sure to choose a tool that keeps your data secure. For more information, see [HTTP test tools](functions-develop-local#http-test-tools).

When you're done testing, you can use the same subscription for production by updating the endpoint. Use the [ az eventgrid event-subscription update](/en-us/cli/azure/eventgrid/event-subscription#az-eventgrid-event-subscription-update) Azure CLI command.

## Create a viewer web app

To simplify capturing event messages, you can deploy a [pre-built web app](https://github.com/Azure-Samples/azure-event-grid-viewer) that displays the event messages. The deployed solution includes an App Service plan, an App Service web app, and source code from GitHub.

Select **Deploy to Azure** to deploy the solution to your subscription. In the Azure portal, provide values for the parameters.

The deployment may take a few minutes to complete. After the deployment has succeeded, view your web app to make sure it's running. In a web browser, navigate to:
`https://<your-site-name>.azurewebsites.net`


You see the site but no events have been posted to it yet.

## Create an Event Grid subscription

Create an Event Grid subscription of the type you want to test, and give it the URL from your web app as the endpoint for event notification. The endpoint for your web app must include the suffix `/api/updates/`

. So, the full URL is `https://<your-site-name>.azurewebsites.net/api/updates`


For information about how to create subscriptions by using the Azure portal, see [Create custom event - Azure portal](../event-grid/custom-event-quickstart-portal) in the Event Grid documentation.

## Generate a request

Trigger an event that will generate HTTP traffic to your web app endpoint. For example, if you created a blob storage subscription, upload or delete a blob. When a request shows up in your web app, copy the request body.

The subscription validation request will be received first; ignore any validation requests, and copy the event request.

## Manually post the request

Run your Event Grid function locally. The `Content-Type`

and `aeg-event-type`

headers are required to be manually set, while and all other values can be left as default.

Use your HTTP test tool to create an HTTP POST request:

Set a

`Content-Type: application/json`

header.Set an

`aeg-event-type: Notification`

header.Paste the RequestBin data into the request body.

Send an HTTP POST request to the endpoint that manually starts the Event Grid trigger.


The `functionName`

parameter must be the name specified in the `FunctionName`

attribute.

The Event Grid trigger function executes and shows logs similar to the following example:

## Next steps

To learn more about Event Grid with Functions, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-continuous-deployment -->

# Continuous deployment for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions enables you to continuously deploy the changes made in a source control repository to a connected function app. This [source control integration](functions-deployment-technologies#source-control) enables a workflow in which a code update triggers build, packaging, and deployment from your project to Azure.

You should always configure continuous deployment for a staging slot and not for the production slot. When you use the production slot, code updates are pushed directly to production without being verified in Azure. Instead, enable continuous deployment to a staging slot, verify updates in the staging slot, and after everything runs correctly you can [swap the staging slot code into production](functions-deployment-slots#swap-slots). If you connect to a production slot, make sure that only production-quality code makes it into the integrated code branch.

Steps in this article show you how to configure continuous code deployments to your function app in Azure by using the Deployment Center in the Azure portal. You can also [configure continuous integration using the Azure CLI](/en-us/cli/azure/functionapp/deployment). These steps can target either a staging or a production slot.

Azure Functions supports these sources for continuous deployment to your app:

Maintain your project code in [Azure Repos](https://azure.microsoft.com/services/devops/repos/), one of the services in Azure DevOps. Supports both Git and Team Foundation Version Control. Used with the [Azure Pipelines build provider](functions-continuous-deployment?tabs=azure-repos*zure-pipelines#build-providers). For more information, see [What is Azure Repos?](/en-us/azure/devops/repos/get-started/what-is-repos).

You can also connect your function app to an external Git repository, but this option requires a manual synchronization. For more information about deployment options, see [Deployment technologies in Azure Functions](functions-deployment-technologies).

Note

Continuous deployment options covered in this article are specific to code-only deployments. For containerized function app deployments, see the **Enable continuous deployment of containers to Azure** section in [Work with containers and Azure Functions](functions-how-to-custom-container).

## Requirements

The unit of deployment for functions in Azure is the function app. For continuous deployment to succeed, the directory structure of your project must be compatible with the basic folder structure that Azure Functions expects. When you create your code project using Azure Functions Core Tools, Visual Studio Code, or Visual Studio, the Azure Functions templates are used to create code projects with the correct directory structure. All functions in a function app are deployed at the same time and in the same package.

After you enable continuous deployment, access to function code in the Azure portal is configured as *read-only* because the *source of truth* is known to reside elsewhere.

Note

The Deployment Center doesn't support enabling continuous deployment for a function app with [inbound network restrictions](functions-networking-options?#inbound-networking-features). You need to instead configure the build provider workflow directly in GitHub or Azure Pipelines. These workflows also require you to use a virtual machine in the same virtual network as the function app as either a [self-hosted agent (Azure Pipelines)](/en-us/azure/devops/pipelines/agents/agents#self-hosted-agents) or a [self-hosted runner (GitHub)](https://docs.github.com/actions/hosting-your-own-runners/managing-self-hosted-runners/about-self-hosted-runners).

## Select a build provider

Building your code project is part of the deployment process. The specific build process depends on your specific language stack, operating system, and hosting plan. Builds can be done locally or remotely, again depending on your specific hosting. For more information, see [Remote build](functions-deployment-technologies#remote-build).

Important

For increased security, consider using a build provider that supports managed identities, including Azure Pipelines and GitHub Actions. The App Service (Kudu) service requires you to [enable basic authentication](#enable-basic-authentication-for-deployments) and work with text-based credentials.

Azure Functions supports these build providers:

Azure Pipelines is one of the services in Azure DevOps and the default build provider for Azure Repos projects. You can also use Azure Pipelines to build projects from GitHub. In Azure Pipelines, there's an [ AzureFunctionApp](/en-us/azure/devops/pipelines/tasks/reference/azure-function-app-v2) task designed specifically for deploying to Azure Functions. This task provides you with control over how the project gets built, packaged, and deployed. Azure Pipelines supports managed identities.

Keep the strengths and limitations of these providers in mind when you enable source control integration. You might need to change your repository source type to take advantage of a specific provider.

## Configure continuous deployment

The [Azure portal](https://portal.azure.com) provides a **Deployment center** for your function apps, which makes it easier to configure continuous deployment. The specific way you configure continuous deployment depends both on the type of source control repository in which your code resides and the [build provider](#build-providers) you choose.

In the [Azure portal](https://portal.azure.com), browse to your function app page and select **Deployment Center** under **Deployment** on the left pane.


Select the **Source** repository type where your project code is being maintained from one of these supported options:

Deployments from Azure Repos that use Azure Pipelines are defined in the [Azure DevOps portal](https://go.microsoft.com/fwlink/?linkid=2245703) and not from your function app. For a step-by-step guide for creating an Azure Pipelines-based deployment from Azure Repos, see [Continuous delivery with Azure Pipelines](functions-how-to-azure-devops).

After deployment finishes, all code from the specified source is deployed to your app. At that point, changes in the deployment source trigger a deployment of those changes to your function app in Azure.

## Enable continuous deployment during app creation

Currently, you can configure continuous deployment from GitHub using GitHub Actions when you create your function app in the Azure portal. You can make this setting on the **Deployment** tab in the **Create Function App** page.

If you want to use a different deployment source or build provider for continuous integration. First, create your function app, and then return to the portal and [set up continuous integration in the Deployment Center](#credentials).

## Enable basic authentication for deployments

In some cases, your function app is created with basic authentication access to the `scm`

endpoint disabled. This blocks publishing by all methods that can't use managed identities to access the `scm`

endpoint. The publishing impacts of having the `scm`

endpoint disabled are detailed in [Deploy without basic authentication](../app-service/configure-basic-auth-disable#deploy-without-basic-authentication).

Important

When you use basic authentication, credentials are sent in clear text. To protect these credentials, you must only access the `scm`

endpoint over an encrypted connection (HTTPS) when using basic authentication. For more information, see [Secure deployment](security-concepts#secure-deployment).

To enable basic authentication to the `scm`

endpoint:

In the

[Azure portal](https://portal.azure.com), go to your function app.On the app's left menu, select

**Settings**>**Configuration**>**General settings**.Set

**SCM Basic Auth Publishing Credentials**to**On**, and then select**Save**.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-web-pubsub-trigger -->

# Azure Web PubSub trigger binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use Azure Web PubSub trigger to handle client events from Azure Web PubSub service.

The trigger endpoint pattern would be as follows, which should be set in Web PubSub service side (Portal: settings -> event handler -> URL Template). In the endpoint pattern, the query part `code=<API_KEY>`

is **REQUIRED** when you're using Azure Function App for [security](function-keys-how-to#understand-keys) reasons. The key can be found in **Azure portal**. Find your function app resource and navigate to **Functions** -> **App keys** -> **System keys** -> **webpubsub_extension** after you deploy the function app to Azure. Though, this key isn't needed when you're working with local functions.

```
<Function_App_Url>/runtime/webhooks/webpubsub?code=<API_KEY>
```


## Example

The following sample shows how to handle user events from clients.

```
[Function("Broadcast")]
public static void Run(
[WebPubSubTrigger("<hub>", WebPubSubEventType.User, "message")] UserEventRequest request, ILogger log)
{
log.LogInformation($"Request from: {request.ConnectionContext.UserId}");
log.LogInformation($"Request message data: {request.Data}");
log.LogInformation($"Request message dataType: {request.DataType}");
}
```


`WebPubSubTrigger`

binding also supports return value in synchronize scenarios, for example, system `Connect`

and user event, when server can check and deny the client request, or send messages to the caller directly. `Connect`

event respects `ConnectEventResponse`

and `EventErrorResponse`

, and user event respects `UserEventResponse`

and `EventErrorResponse`

, rest types not matching current scenario is ignored.

```
[Function("Broadcast")]
public static UserEventResponse Run(
[WebPubSubTrigger("<hub>", WebPubSubEventType.User, "message")] UserEventRequest request)
{
return new UserEventResponse("[SYSTEM ACK] Received.");
}
```


```
const { app, trigger } = require('@azure/functions');
const wpsTrigger = trigger.generic({
type: 'webPubSubTrigger',
name: 'request',
hub: '<hub>',
eventName: 'message',
eventType: 'user'
});
app.generic('message', {
trigger: wpsTrigger,
handler: async (request, context) => {
context.log('Request from: ', request.connectionContext.userId);
context.log('Request message data: ', request.data);
context.log('Request message dataType: ', request.dataType);
}
});
```


`WebPubSubTrigger`

binding also supports return value in synchronize scenarios, for example, system `Connect`

and user event, when server can check and deny the client request, or send message to the request client directly. In JavaScript weakly typed language, it's deserialized regarding the object keys. And `EventErrorResponse`

has the highest priority compare to rest objects, that if `code`

is in the return, then it's parsed to `EventErrorResponse`

.

Note

Complete samples for this language are pending.

Note

The Web PubSub extensions for Java isn't supported yet.

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Required - must be set to `webPubSubTrigger` . |
direction |
n/a | Required - must be set to `in` . |
name |
n/a | Required - the variable name used in function code for the parameter that receives the event data. |
hub |
Hub | Required - the value must be set to the name of the Web PubSub hub for the function to be triggered. We support set the value in attribute as higher priority, or it can be set in app settings as a global value. |
eventType |
WebPubSubEventType | Required - the value must be set as the event type of messages for the function to be triggered. The value should be either `user` or `system` . |
eventName |
EventName | Required - the value must be set as the event of messages for the function to be triggered. For `system` event type, the event name should be in `connect` , `connected` , `disconnected` . For user-defined subprotocols, the event name is `message` . For system supported subprotocol `json.webpubsub.azure.v1.` , the event name is user-defined event name. |
clientProtocols |
ClientProtocols | Optional - specifies which client protocol can trigger the Web PubSub trigger functions. The following case-insensitive values are valid: `all` : Accepts all client protocols. Default value. `webPubSub` : Accepts only Web PubSub protocols. `mqtt` : Accepts only MQTT protocols. |
connection |
Connection | Optional - the name of an app settings or setting collection that specifies the upstream Azure Web PubSub service. The value is used for signature validation. And the value is auto resolved with app settings `WebPubSubConnectionString` by default. And `null` means the validation isn't needed and always succeed. |

Important

For optimal security, your function app should use managed identities when connecting to the Web PubSub service instead of using a connection string, which contains a shared secret key. For more information, see [Authorize a managed identity request by using Microsoft Entra ID](../azure-web-pubsub/howto-authorize-from-managed-identity).

## Usages

In C#, `WebPubSubEventRequest`

is type recognized binding parameter, rest parameters are bound by parameter name. Check following table for available parameters and types.

In weakly typed language like JavaScript, `name`

in `function.json`

is used to bind the trigger object regarding following mapping table. And respect `dataType`

in `function.json`

to convert message accordingly when `name`

is set to `data`

as the binding object for trigger input. All the parameters can be read from `context.bindingData.<BindingName>`

and is `JObject`

converted.

| Binding Name | Binding Type | Description | Properties |
|---|---|---|---|
| request | `WebPubSubEventRequest` |
Describes the upstream request | Property differs by different event types, including derived classes `ConnectEventRequest` , `MqttConnectEventRequest` , `ConnectedEventRequest` , `MqttConnectedEventRequest` , `UserEventRequest` , `DisconnectedEventRequest` , and `MqttDisconnectedEventRequest` . |
| connectionContext | `WebPubSubConnectionContext` |
Common request information | EventType, EventName, Hub, ConnectionId, UserId, Headers, Origin, Signature, States |
| data | `BinaryData` ,`string` ,`Stream` ,`byte[]` |
Request message data from client in user `message` event |
- |
| dataType | `WebPubSubDataType` |
Request message dataType, which supports `binary` , `text` , `json` |
- |
| claims | `IDictionary<string, string[]>` |
User Claims in system `connect` request |
- |
| query | `IDictionary<string, string[]>` |
User query in system `connect` request |
- |
| subprotocols | `IList<string>` |
Available subprotocols in system `connect` request |
- |
| clientCertificates | `IList<ClientCertificate>` |
A list of certificate thumbprint from clients in system `connect` request |
- |
| reason | `string` |
Reason in system `disconnected` request |
- |

Important

In C#, multiple types supported parameter **MUST** be put in the first, i.e. `request`

or `data`

that other than the default `BinaryData`

type to make the function binding correctly.

### Return response

`WebPubSubTrigger`

respects customer returned response for synchronous events of `connect`

and user event. Only matched response is sent back to service, otherwise, it's ignored. Besides, `WebPubSubTrigger`

return object supports users to `SetState()`

and `ClearStates()`

to manage the metadata for the connection. And the extension merges the results from return value with the original ones from request `WebPubSubConnectionContext.States`

. Value in existing key is overwrite and value in new key is added.

| Return Type | Description | Properties |
|---|---|---|
`ConnectEventResponse` |

`connect`

event`UserEventResponse`

`EventErrorResponse`

`*WebPubSubEventResponse`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr-output-invoke -->

# Dapr Invoke output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Dapr invoke output binding allows you to invoke another Dapr application during a function execution.

For information on setup and configuration details of the Dapr extension, see the [Dapr extension overview](functions-bindings-dapr).

## Example

A C# function can be created using one of the following C# modes:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).The following example demonstrates using a Dapr invoke output binding to perform a Dapr service invocation operation hosted in another Dapr-ized application. In this example, the function acts like a proxy.

```
[FunctionName("InvokeOutputBinding")]
public static async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Function, "get", Route = "invoke/{appId}/{methodName}")] HttpRequest req,
[DaprInvoke(AppId = "{appId}", MethodName = "{methodName}", HttpVerb = "post")] IAsyncCollector<InvokeMethodParameters> output,
ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
var outputContent = new InvokeMethodParameters
{
Body = requestBody
};
await output.AddAsync(outputContent);
return new OkResult();
}
```


The following example creates a `"InvokeOutputBinding"`

function using the `DaprInvokeOutput`

binding with an `HttpTrigger`

:

```
@FunctionName("InvokeOutputBinding")
public String run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "invoke/{appId}/{methodName}")
HttpRequestMessage<Optional<String>> request,
@DaprInvokeOutput(
appId = "{appId}",
methodName = "{methodName}",
httpVerb = "post")
OutputBinding<String> payload,
final ExecutionContext context)
```


In the following example, the Dapr invoke output binding is paired with an HTTP trigger, which is registered by the `app`

object:

```
const { app, trigger } = require('@azure/functions');
app.generic('InvokeOutputBinding', {
trigger: trigger.generic({
type: 'httpTrigger',
authLevel: 'anonymous',
methods: ['POST'],
route: "invoke/{appId}/{methodName}",
name: "req"
}),
return: daprInvokeOutput,
handler: async (request, context) => {
context.log("Node HTTP trigger function processed a request.");
const payload = await request.text();
context.log(JSON.stringify(payload));
return { body: payload };
}
});
```


The following examples show Dapr triggers in a *function.json* file and PowerShell code that uses those bindings.

Here's the *function.json* file for `daprInvoke`

:

```
{
"bindings":
{
"type": "daprInvoke",
"direction": "out",
"appId": "{appId}",
"methodName": "{methodName}",
"httpVerb": "post",
"name": "payload"
}
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

In code:

```
using namespace System.Net
# Input bindings are passed in via param block.
param($req, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "Powershell InvokeOutputBinding processed a request."
$req_body = $req.Body
$invoke_output_binding_req_body = @{
"body" = $req_body
}
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name payload -Value $invoke_output_binding_req_body
Push-OutputBinding -Name res -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $req_body
})
```


The following example shows a Dapr Invoke output binding, which uses the [v2 Python programming model](functions-reference-python). To use `daprInvoke`

in your Python function app code:

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="InvokeOutputBinding")
@app.route(route="invoke/{appId}/{methodName}", auth_level=dapp.auth_level.ANONYMOUS)
@app.dapr_invoke_output(arg_name = "payload", app_id = "{appId}", method_name = "{methodName}", http_verb = "post")
def main(req: func.HttpRequest, payload: func.Out[str] ) -> str:
# request body must be passed this way "{\"body\":{\"value\":{\"key\":\"some value\"}}}" to use the InvokeOutputBinding, all the data must be enclosed in body property.
logging.info('Python function processed a InvokeOutputBinding request from the Dapr Runtime.')
body = req.get_body()
logging.info(body)
if body is not None:
payload.set(body)
else:
logging.info('req body is none')
return 'ok'
```


## Attributes

In the [in-process model](functions-dotnet-class-library), use the `DaprInvoke`

attribute to define a Dapr invoke output binding, which supports these parameters:

| Parameter | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
AppId |
The Dapr app ID to invoke. | ✔️ | ✔️ |
MethodName |
The method name of the app to invoke. | ✔️ | ✔️ |
HttpVerb |
Optional. HTTP verb to use of the app to invoke. Default is `POST` . |
✔️ | ✔️ |
Body |
Required. The body of the request. |
❌ | ✔️ |

## Annotations

The `DaprInvokeOutput`

annotation allows you to have your function invoke and listen to an output binding.

| Element | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
appId |
The app ID of the application involved in the invoke binding. | ✔️ | ✔️ |
methodName |
The name of the method variable. | ✔️ | ✔️ |
httpVerb |
Post or get. | ✔️ | ✔️ |
body |
Required. The body of the request. |
❌ | ✔️ |

## Configuration

The following table explains the binding configuration properties that you set in the code.

| Property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
appId |
The app ID of the application involved in the invoke binding. | ✔️ | ✔️ |
methods |
Post or get. | ✔️ | ✔️ |
body |
Required. The body of the request. |
❌ | ✔️ |

The following table explains the binding configuration properties that you set in the function.json file.

| function.json property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
appId |
The app ID of the application involved in the invoke binding. | ✔️ | ✔️ |
methodName |
The name of the method variable. | ✔️ | ✔️ |
httpVerb |
Post or get. | ✔️ | ✔️ |
body |
Required. The body of the request. |
❌ | ✔️ |

The following table explains the binding configuration properties for `@dapp.dapr_invoke_output`

that you set in your Python code.

| Property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
app_id |
The app ID of the application involved in the invoke binding. | ✔️ | ✔️ |
method_name |
The name of the method variable. | ✔️ | ✔️ |
http_verb |
Set to `post` or `get` . |
✔️ | ✔️ |
body |
Required. The body of the request. |
❌ | ✔️ |

If properties are defined in both Attributes and `RequestBody`

, priority is given to data provided in `RequestBody`

.

See the [Example section](#example) for complete examples.

## Usage

To use the Dapr service invocation output binding, learn more about [how to use Dapr service invocation in the official Dapr documentation](https://docs.dapr.io/developing-applications/building-blocks/service-invocation/).

To use the `daprInvoke`

in Python v2, set up your project with the correct dependencies.

In your

`requirements.text`

file, add the following line:`azure-functions==1.18.0b3`

In the terminal, install the Python library.

`pip install -r .\requirements.txt`

Modify your

`local.setting.json`

file with the following configuration:`"PYTHON_ISOLATE_WORKER_DEPENDENCIES":1`

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/configure-monitoring -->

# How to configure monitoring for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions integrates with Application Insights to better enable you to monitor your function apps. Application Insights, a feature of Azure Monitor, is an extensible Application Performance Management (APM) service that collects data generated by your function app, including information your app writes to logs. Application Insights integration is typically enabled when your function app is created. If your app doesn't have the instrumentation key set, you must first [enable Application Insights integration](#enable-application-insights-integration).

You can use Application Insights without any custom configuration. However, the default configuration can result in high volumes of data. If you're using a Visual Studio Azure subscription, you might hit your data cap for Application Insights. For information about Application Insights costs, see [Application Insights billing](/en-us/azure/azure-monitor/logs/cost-logs#application-insights-billing). For more information, see [Solutions with high-volume of telemetry](#solutions-with-high-volume-of-telemetry).

In this article, you learn how to configure and customize the data that your functions send to Application Insights. You can set common logging configurations in the * host.json* file. By default, these settings also govern custom logs emitted by your code. However, in some cases this behavior can be disabled in favor of options that give you more control over logging. For more information, see

[Custom application logs](#custom-application-logs).

Note

You can use specially configured application settings to represent specific settings in a *host.json* file for a particular environment. Doing so lets you effectively change *host.json* settings without needing to republish the *host.json* file in your project. For more information, see [Override host.json values](functions-host-json#override-hostjson-values).

## Custom application logs

By default, custom application logs you write are sent to the Functions host, which then sends them to Application Insights under the [Worker category](#configure-categories). Some language stacks allow you to instead send the logs directly to Application Insights, which gives you full control over how logs you write are emitted. In this case, the logging pipeline changes from `worker -> Functions host -> Application Insights`

to `worker -> Application Insights`

.

The following table summarizes the configuration options available for each stack:

| Language stack | Where to configure custom logs |
|---|---|
| .NET (in-process model) | `host.json` |
| .NET (isolated model) | Default (send custom logs to the Functions host): `host.json` To send logs directly to Application Insights, see:
|
| Node.js | `host.json` |
| Python | `host.json` |
| Java | Default (send custom logs to the Functions host): `host.json` To send logs directly to Application Insights, see:
|
| PowerShell | `host.json` |

When you configure custom application logs to be sent directly, the host no longer emits them, and `host.json`

no longer controls their behavior. Similarly, the options exposed by each stack apply only to custom logs, and they don't change the behavior of the other runtime logs described in this article. In this case, to control the behavior of all logs, you might need to make changes in both configurations.

## Configure categories

The Azure Functions logger includes a *category* for every log. The category indicates which part of the runtime code or your function code wrote the log. Categories differ between version 1.x and later versions.

Category names are assigned differently in Functions compared to other .NET frameworks. For example, when you use `ILogger<T>`

in ASP.NET, the category is the name of the generic type. C# functions also use `ILogger<T>`

, but instead of setting the generic type name as a category, the runtime assigns categories based on the source. For example:

- Entries related to running a function are assigned a category of
`Function.<FUNCTION_NAME>`

. - Entries created by user code inside the function, such as when calling
`logger.LogInformation()`

, are assigned a category of`Function.<FUNCTION_NAME>.User`

.

The following table describes the main categories of logs that the runtime creates:

| Category | Table | Description |
|---|---|---|
`Function` |
traces |
Includes function started and completed logs for all function runs. For successful runs, these logs are at the `Information` level. Exceptions are logged at the `Error` level. The runtime also creates `Warning` level logs, such as when queue messages are sent to the
|
`Function.<YOUR_FUNCTION_NAME>` |
dependencies |
Dependency data is automatically collected for some services. For successful runs, these logs are at the `Information` level. For more information, see
`Error` level. The runtime also creates `Warning` level logs, such as when queue messages are sent to the
|
`Function.<YOUR_FUNCTION_NAME>` |
customMetricscustomEvents |
C# and JavaScript SDKs lets you collect custom metrics and log custom events. For more information, see
|

`Function.<YOUR_FUNCTION_NAME>`

**traces**`Information`

level. Exceptions are logged at the `Error`

level. The runtime also creates `Warning`

level logs, such as when queue messages are sent to the [poison queue](functions-bindings-storage-queue-trigger#poison-messages).`Function.<YOUR_FUNCTION_NAME>.User`

**traces**[Writing to logs](functions-monitoring#writing-to-logs).`Host.Aggregator`

**customMetrics**[configurable](#configure-the-aggregator)period of time. The default period is 30 seconds or 1,000 results, whichever comes first. Examples are the number of runs, success rate, and duration. All of these logs are written at the`Information`

level. If you filter at `Warning`

or higher, you don't see any of this data.`Host.Results`

**requests**`Information`

level. If you filter at `Warning`

or higher, you don't see any of this data.`Microsoft`

**traces**`Worker`

**traces**`Microsoft.*`

category, such as `Microsoft.Azure.WebJobs.Script.Workers.Rpc.RpcFunctionInvocationDispatcher`

. These logs are written at the `Information`

level.Note

For .NET class library functions, these categories assume you're using `ILogger`

and not `ILogger<T>`

. For more information, see the [Functions ILogger documentation](functions-dotnet-class-library#ilogger).

The **Table** column indicates to which table in Application Insights the log is written.

## Configure log levels

A *log level* is assigned to every log. The value is an integer that indicates relative importance:

| LogLevel | Code | Description |
|---|---|---|
| Trace | 0 | Logs that contain the most detailed messages. These messages might contain sensitive application data. These messages are disabled by default and should never be enabled in a production environment. |
| Debug | 1 | Logs that are used for interactive investigation during development. These logs should primarily contain information useful for debugging and have no long-term value. |
| Information | 2 | Logs that track the general flow of the application. These logs should have long-term value. |
| Warning | 3 | Logs that highlight an abnormal or unexpected event in the application flow, but don't otherwise cause the application execution to stop. |
| Error | 4 | Logs that highlight when the current flow of execution is stopped because of a failure. These errors should indicate a failure in the current activity, not an application-wide failure. |
| Critical | 5 | Logs that describe an unrecoverable application or system crash, or a catastrophic failure that requires immediate attention. |
| None | 6 | Disables logging for the specified category. |

The [ host.json file](functions-host-json) configuration determines how much logging a functions app sends to Application Insights.

For each category, you indicate the minimum log level to send. The *host.json* settings vary depending on the [Functions runtime version](functions-versions).

The following examples define logging based on the following rules:

- The default logging level is set to
`Warning`

to prevent[excessive logging](#solutions-with-high-volume-of-telemetry)for unanticipated categories. `Host.Aggregator`

and`Host.Results`

are set to lower levels. Setting logging levels too high (especially higher than`Information`

) can result in loss of metrics and performance data.- Logging for function runs is set to
`Information`

. If necessary, you can[override](functions-host-json#override-hostjson-values)this setting in local development to`Debug`

or`Trace`

.

```
{
"logging": {
"fileLoggingMode": "debugOnly",
"logLevel": {
"default": "Warning",
"Host.Aggregator": "Trace",
"Host.Results": "Information",
"Function": "Information"
}
}
}
```


If * host.json* includes multiple logs that start with the same string, the more defined logs ones are matched first. Consider the following example that logs everything in the runtime, except

`Host.Aggregator`

, at the `Error`

level:```
{
"logging": {
"fileLoggingMode": "debugOnly",
"logLevel": {
"default": "Information",
"Host": "Error",
"Function": "Error",
"Host.Aggregator": "Information"
}
}
}
```


You can use a log level setting of `None`

to prevent any logs from being written for a category.

Caution

Azure Functions integrates with Application Insights by storing telemetry events in Application Insights tables. If you set a category log level to any value different from `Information`

, it prevents the telemetry from flowing to those tables, and you won't be able to see related data in the **Application Insights** and **Function Monitor** tabs.

For example, for the previous samples:

- If you set the
`Host.Results`

category to the`Error`

log level, Azure gathers only host execution telemetry events in the`requests`

table for failed function executions, preventing the display of host execution details of successful executions in both the**Application Insights**and**Function Monitor**tabs. - If you set the
`Function`

category to the`Error`

log level, it stops gathering function telemetry data related to`dependencies`

,`customMetrics`

, and`customEvents`

for all the functions, preventing you from viewing any of this data in Application Insights. Azure gathers only`traces`

logged at the`Error`

level.

In both cases, Azure continues to collect errors and exceptions data in the **Application Insights** and **Function Monitor** tabs. For more information, see [Solutions with high-volume of telemetry](#solutions-with-high-volume-of-telemetry).

## Configure the aggregator

As noted in the previous section, the runtime aggregates data about function executions over a period of time. The default period is 30 seconds or 1,000 runs, whichever comes first. You can configure this setting in the * host.json* file. For example:

```
{
"aggregator": {
"batchSize": 1000,
"flushTimeout": "00:00:30"
}
}
```


## Configure sampling

Application Insights has a [sampling](/en-us/azure/azure-monitor/app/sampling) feature that can protect you from producing too much telemetry data on completed executions at times of peak load. When the rate of incoming executions exceeds a specified threshold, Application Insights starts to randomly ignore some of the incoming executions. The default setting for maximum number of executions per second is 20 (five in version 1.x). You can configure sampling in [ host.json](functions-host-json#applicationinsights). Here's an example:

```
{
"logging": {
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"maxTelemetryItemsPerSecond" : 20,
"excludedTypes": "Request;Exception"
}
}
}
}
```


You can exclude certain types of telemetry from sampling. In this example, data of type `Request`

and `Exception`

is excluded from sampling. It ensures that *all* function executions (requests) and exceptions are logged while other types of telemetry remain subject to sampling.

If your project uses a dependency on the Application Insights SDK to do manual telemetry tracking, you might experience unusual behavior if your sampling configuration differs from the sampling configuration in your function app. In such cases, use the same sampling configuration as the function app. For more information, see [Sampling in Application Insights](/en-us/azure/azure-monitor/app/sampling).

## Enable SQL query collection

Application Insights automatically collects data on dependencies for HTTP requests, database calls, and for several bindings. For more information, see [Dependencies](functions-monitoring#dependencies). For SQL calls, the name of the server and database is always collected and stored, but SQL query text isn't collected by default. You can use `dependencyTrackingOptions.enableSqlCommandTextInstrumentation`

to enable SQL query text logging by using the following settings (at a minimum) in your [host.json file](functions-host-json#applicationinsightsdependencytrackingoptions):

```
"logging": {
"applicationInsights": {
"enableDependencyTracking": true,
"dependencyTrackingOptions": {
"enableSqlCommandTextInstrumentation": true
}
}
}
```


For more information, see [Advanced SQL tracking to get full SQL query](/en-us/azure/azure-monitor/app/asp-net-dependencies#advanced-sql-tracking-to-get-full-sql-query).

## Configure scale controller logs

*This feature is in preview.*

You can have the [Azure Functions scale controller](event-driven-scaling#runtime-scaling) emit logs to either Application Insights or to Blob storage to better understand the decisions the scale controller is making for your function app.

To enable this feature, add an application setting named `SCALE_CONTROLLER_LOGGING_ENABLED`

to your function app settings. The following value of the setting must be in the format `<DESTINATION>:<VERBOSITY>`

. For more information, see the following table:

| Property | Description |
|---|---|
`<DESTINATION>` |
The destination to which logs are sent. Valid values are `AppInsights` and `Blob` .When you use `AppInsights` , ensure that the
When you set the destination to `Blob` , logs are created in a blob container named `azure-functions-scale-controller` in the default storage account set in the `AzureWebJobsStorage` application setting. |
`<VERBOSITY>` |
Specifies the level of logging. Supported values are `None` , `Warning` , and `Verbose` .When set to `Verbose` , the scale controller logs a reason for every change in the worker count, and information about the triggers that factor into those decisions. Verbose logs include trigger warnings and the hashes used by the triggers before and after the scale controller runs. |

Tip

Keep in mind that while you leave scale controller logging enabled, it impacts the [potential costs of monitoring your function app](functions-monitoring#application-insights-pricing-and-limits). Consider enabling logging until you collect enough data to understand how the scale controller is behaving, and then disabling it.

For example, the following Azure CLI command turns on verbose logging from the scale controller to Application Insights:

```
az functionapp config appsettings set --name <FUNCTION_APP_NAME> \
--resource-group <RESOURCE_GROUP_NAME> \
--settings SCALE_CONTROLLER_LOGGING_ENABLED=AppInsights:Verbose
```


In this example, replace `<FUNCTION_APP_NAME>`

and `<RESOURCE_GROUP_NAME>`

with the name of your function app and the resource group name, respectively.

The following Azure CLI command disables logging by setting the verbosity to `None`

:

```
az functionapp config appsettings set --name <FUNCTION_APP_NAME> \
--resource-group <RESOURCE_GROUP_NAME> \
--settings SCALE_CONTROLLER_LOGGING_ENABLED=AppInsights:None
```


You can also disable logging by removing the `SCALE_CONTROLLER_LOGGING_ENABLED`

setting using the following Azure CLI command:

```
az functionapp config appsettings delete --name <FUNCTION_APP_NAME> \
--resource-group <RESOURCE_GROUP_NAME> \
--setting-names SCALE_CONTROLLER_LOGGING_ENABLED
```


With scale controller logging enabled, you're now able to [query your scale controller logs](analyze-telemetry-data#query-scale-controller-logs).

## Enable Application Insights integration

For a function app to send data to Application Insights, it needs to connect to the Application Insights resource using **only one** of these application settings:

| Setting name | Description |
|---|---|
`APPLICATIONINSIGHTS_CONNECTION_STRING` |
This setting is recommended and is required when your Application Insights instance runs in a sovereign cloud. The connection string supports other
|

`APPINSIGHTS_INSTRUMENTATIONKEY`

When you create your function app in the [Azure portal](functions-get-started) from the command line by using [Azure Functions Core Tools](how-to-create-function-azure-cli?pivots=programming-language-csharp) or [Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-csharp), Application Insights integration is enabled by default. The Application Insights resource has the same name as your function app, and is created either in the same region or in the nearest region.

### Require Microsoft Entra authentication

You can use the [ APPLICATIONINSIGHTS_AUTHENTICATION_STRING](functions-app-settings#applicationinsights_authentication_string) setting to enable connections to Application Insights using Microsoft Entra authentication. This creates a consistent authentication experience across all Application Insights pipelines, including Profiler and Snapshot Debugger, as well as from the Functions host and language-specific agents.

Note

There's currently no Microsoft Entra ID authentication support for local development.

When Ingesting data in a sovereign cloud, Microsoft Entra ID authentication isn't available when using the Application Insights SDK. OpenTelemetry-based data collection supports Microsoft Entra ID authentication across all cloud environments, including sovereign clouds.

The value contains either `Authorization=AAD`

for a system-assigned managed identity or `ClientId=<YOUR_CLIENT_ID>;Authorization=AAD`

for a user-assigned managed identity. The managed identity must already be available to the function app, with an assigned role equivalent to [Monitoring Metrics Publisher](/en-us/azure/role-based-access-control/built-in-roles/monitor#monitoring-metrics-publisher). For more information, see [Microsoft Entra authentication for Application Insights](/en-us/azure/azure-monitor/app/azure-ad-authentication).

The [ APPLICATIONINSIGHTS_CONNECTION_STRING](functions-app-settings#applicationinsights_connection_string) setting is still required.

Note

When using `APPLICATIONINSIGHTS_AUTHENTICATION_STRING`

to connect to Application Insights using Microsoft Entra authentication, you should also [Disable local authentication for Application Insights](/en-us/azure/azure-monitor/app/azure-ad-authentication#disable-local-authentication). This configuration requires Microsoft Entra authentication in order for telemetry to be ingested into your workspace.

### New function app in the portal

To review the Application Insights resource being created, select it to expand the **Application Insights** window. You can change the **New resource name** or select a different **Location** in an [Azure geography](https://azure.microsoft.com/global-infrastructure/geographies/) where you want to store your data.


When you select **Create**, an Application Insights resource is created with your function app, which has the `APPLICATIONINSIGHTS_CONNECTION_STRING`

set in application settings. Everything is ready to go.

### Add to an existing function app

If an Application Insights resource wasn't created with your function app, use the following steps to create the resource. You can then add the connection string from that resource as an [application setting](functions-how-to-use-azure-function-app-settings#settings) in your function app.

In the

[Azure portal](https://portal.azure.com), search for and select**function app**, and then select your function app.Select the

**Application Insights is not configured**banner at the top of the window. If you don't see this banner, then your app might already have Application Insights enabled.Expand

**Change your resource**and create an Application Insights resource by using the settings specified in the following table:Setting Suggested value Description **New resource name**Unique app name It's easiest to use the same name as your function app, which must be unique in your subscription. **Location**West Europe If possible, use the same [region](https://azure.microsoft.com/regions/)as your function app, or the one that's close to that region.Select

**Apply**.The Application Insights resource is created in the same resource group and subscription as your function app. After the resource is created, close the

**Application Insights**window.In your function app, expand

**Settings**, and then select**Environment variables**. In the**App settings**tab, if you see an app setting named`APPLICATIONINSIGHTS_CONNECTION_STRING`

, Application Insights integration is enabled for your function app running in Azure. If this setting doesn't exist, add it by using your Application Insights connection string as the value.

Note

Older function apps might use `APPINSIGHTS_INSTRUMENTATIONKEY`

instead of `APPLICATIONINSIGHTS_CONNECTION_STRING`

. When possible, update your app to use the connection string instead of the instrumentation key.

## Disable built-in logging

Early versions of Functions used built-in monitoring, which is no longer recommended. When you enable Application Insights, disable the built-in logging that uses Azure Storage. The built-in logging is useful for testing with light workloads, but isn't intended for high-load production use. For production monitoring, we recommend Application Insights. If you use built-in logging in production, the logging record might be incomplete because of throttling on Azure Storage.

To disable built-in logging, delete the `AzureWebJobsDashboard`

app setting. For more information about how to delete app settings in the Azure portal, see the **Application settings** section of [How to manage a function app](functions-how-to-use-azure-function-app-settings#settings). Before you delete the app setting, ensure that no existing functions in the same function app use the setting for Azure Storage triggers or bindings.

## Solutions with high volume of telemetry

Function apps are an essential part of solutions that can cause high volumes of telemetry, such as IoT solutions, rapid event driven solutions, high load financial systems, and integration systems. In this case, you should consider extra configuration to reduce costs while maintaining observability.

The generated telemetry can be consumed in real-time dashboards, alerting, detailed diagnostics, and so on. Depending on how the generated telemetry is consumed, you need to define a strategy to reduce the volume of data generated. This strategy allows you to properly monitor, operate, and diagnose your function apps in production. Consider the following options:

**Use the correct table plan**:[Table plans](/en-us/azure/azure-monitor/logs/data-platform-logs#table-plans)help you manage data costs by controlling how often you use the data in a table and the kind of analysis you need to perform. To reduce costs, you can choose the`Basic`

plan, which does lack some features available in the`Analytics`

plan.**Use sampling**: As mentioned[previously](#configure-sampling), sampling helps to dramatically reduce the volume of telemetry events ingested while maintaining a statistically correct analysis. It could happen that even using sampling you still get a high volume of telemetry. Inspect the options that[adaptive sampling](/en-us/azure/azure-monitor/app/sampling#configuring-adaptive-sampling-for-aspnet-applications)provides to you. For example, set the`maxTelemetryItemsPerSecond`

to a value that balances the volume generated with your monitoring needs. Keep in mind that the telemetry sampling is applied per host executing your function app.**Default log level**: Use`Warning`

or`Error`

as the default value for all telemetry categories. Later, you can decide which[categories](#configure-categories)you want to set at the`Information`

level, so that you can monitor and diagnose your functions properly.**Tune your functions telemetry**: With the default log level set to`Error`

or`Warning`

, no detailed information from each function is gathered (dependencies, custom metrics, custom events, and traces). For those functions that are key for production monitoring, define an explicit entry for the`Function.<YOUR_FUNCTION_NAME>`

category and set it to`Information`

, so that you can gather detailed information. To avoid gathering[user-generated logs](functions-monitoring#writing-to-logs)at the`Information`

level, set the`Function.<YOUR_FUNCTION_NAME>.User`

category to the`Error`

or`Warning`

log level.**Host.Aggregator category**: As described in[configure categories](#configure-categories), this category provides aggregated information of function invocations. The information from this category is gathered in the Application Insights`customMetrics`

table, and is shown in the function**Overview**tab in the Azure portal. Depending on how you configure the aggregator, consider that there can be a delay, determined by the`flushTimeout`

setting, in the telemetry gathered. If you set this category to a value different from`Information`

, you stop gathering the data in the`customMetrics`

table and don't display metrics in the function**Overview**tab.The following screenshot shows

`Host.Aggregator`

telemetry data displayed in the function**Overview**tab:The following screenshot shows

`Host.Aggregator`

telemetry data in Application Insights`customMetrics`

table:**Host.Results category**: As described in[configure categories](#configure-categories), this category provides the runtime-generated logs indicating the success or failure of a function invocation. The information from this category is gathered in the Application Insights`requests`

table, and is shown in the function**Monitor**tab and in different Application Insights dashboards (Performance, Failures, and so on). If you set this category to a value different than`Information`

, you gather only telemetry generated at the log level defined (or higher). For example, setting it to`error`

results in tracking requests data only for failed executions.The following screenshot shows the

`Host.Results`

telemetry data displayed in the function**Monitor**tab:The following screenshot shows

`Host.Results`

telemetry data displayed in Application Insights Performance dashboard:**Host.Aggregator vs Host.Results**: Both categories provide good insights about function executions. If needed, you can remove the detailed information from one of these categories, so that you can use the other for monitoring and alerting. Here's a sample:

```
{
"version": "2.0",
"logging": {
"logLevel": {
"default": "Warning",
"Function": "Error",
"Host.Aggregator": "Error",
"Host.Results": "Information",
"Function.Function1": "Information",
"Function.Function1.User": "Error"
},
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"maxTelemetryItemsPerSecond": 1,
"excludedTypes": "Exception"
}
}
}
}
```


With this configuration:

The default value for all functions and telemetry categories is set to

`Warning`

(including Microsoft and Worker categories). So, by default, all errors and warnings generated by runtime and custom logging are gathered.The

`Function`

category log level is set to`Error`

, so for all functions, by default, only exceptions and error logs are gathered. Dependencies, user-generated metrics, and user-generated events are skipped.For the

`Host.Aggregator`

category, as it's set to the`Error`

log level, aggregated information from function invocations isn't gathered in the`customMetrics`

Application Insights table, and information about executions counts (total, successful, and failed) aren't shown in the function overview dashboard.For the

`Host.Results`

category, all the host execution information is gathered in the`requests`

Application Insights table. All the invocations results are shown in the function Monitor dashboard and in Application Insights dashboards.For the function called

`Function1`

, we set the log level to`Information`

. So, for this concrete function, all the telemetry is gathered (dependency, custom metrics, and custom events). For the same function, we set the`Function1.User`

category (user-generated traces) to`Error`

, so only custom error logging is gathered.Note

Configuration per function isn't supported in v1.x of the Functions runtime.

Sampling is configured to send one telemetry item per second per type, excluding the exceptions. This sampling happens for each server host running our function app. So, if we have four instances, this configuration emits four telemetry items per second per type and all the exceptions that might occur.

Note

Metric counts such as request rate and exception rate are adjusted to compensate for the sampling rate, so that they show approximately correct values in Metric Explorer.


Tip

Experiment with different configurations to ensure that you cover your requirements for logging, monitoring, and alerting. Also, ensure that you have detailed diagnostics in case of unexpected errors or malfunctioning.

## Overriding monitoring configuration at runtime

Finally, there could be situations where you need to quickly change the logging behavior of a certain category in production, and you don't want to make a whole deployment just for a change in the *host.json* file. For such cases, you can override the [host.json values](functions-host-json#override-hostjson-values).

To configure these values at App settings level (and avoid redeployment on just *host.json* changes), you should override specific `host.json`

values by creating an equivalent value as an application setting. When the runtime finds an application setting in the format `AzureFunctionsJobHost__path__to__setting`

, it overrides the equivalent `host.json`

setting located at `path.to.setting`

in the JSON. When expressed as an application setting, a double underscore (`__`

) replaces the dot (`.`

) used to indicate JSON hierarchy. For example, you can use the following app settings to configure individual function log levels in `host.json`

.

| Host.json path | App setting |
|---|---|
| logging.logLevel.default | AzureFunctionsJobHost__logging__logLevel__default |
| logging.logLevel.Host.Aggregator | AzureFunctionsJobHost__logging__logLevel__Host.Aggregator |
| logging.logLevel.Function | AzureFunctionsJobHost__logging__logLevel__Function |
| logging.logLevel.Function.Function1 | AzureFunctionsJobHost__logging__logLevel__Function.Function1 |
| logging.logLevel.Function.Function1.User | AzureFunctionsJobHost__logging__logLevel__Function.Function1.User |

You can override the settings directly at the Azure portal Function App Configuration pane or by using an Azure CLI or PowerShell script.

```
az functionapp config appsettings set --name MyFunctionApp --resource-group MyResourceGroup --settings "AzureFunctionsJobHost__logging__logLevel__Host.Aggregator=Information"
```


Note

Overriding the `host.json`

through changing app settings will restart your function app.
App settings that contain a period aren't supported when running on Linux in an Elastic Premium plan or a Dedicated (App Service) plan. In these hosting environments, you should continue to use the *host.json* file.

## Monitor function apps using Health check

You can use the Health Check feature to monitor function apps on the Premium (Elastic Premium) and Dedicated (App Service) plans. Health check isn't an option for the Flex Consumption and Consumption plans. To learn how to configure it, see [Monitor App Service instances using Health check](../app-service/monitor-instances-health-check). Your function app should have an HTTP trigger function that responds with an HTTP status code of 200 on the same endpoint as configured on the `Path`

parameter of the health check. You can also have that function perform extra checks to ensure that dependent services are reachable and working.

## Related content

For more information about monitoring, see:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-continuous-deployment -->

# Continuous deployment for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions enables you to continuously deploy the changes made in a source control repository to a connected function app. This [source control integration](functions-deployment-technologies#source-control) enables a workflow in which a code update triggers build, packaging, and deployment from your project to Azure.

You should always configure continuous deployment for a staging slot and not for the production slot. When you use the production slot, code updates are pushed directly to production without being verified in Azure. Instead, enable continuous deployment to a staging slot, verify updates in the staging slot, and after everything runs correctly you can [swap the staging slot code into production](functions-deployment-slots#swap-slots). If you connect to a production slot, make sure that only production-quality code makes it into the integrated code branch.

Steps in this article show you how to configure continuous code deployments to your function app in Azure by using the Deployment Center in the Azure portal. You can also [configure continuous integration using the Azure CLI](/en-us/cli/azure/functionapp/deployment). These steps can target either a staging or a production slot.

Azure Functions supports these sources for continuous deployment to your app:

Maintain your project code in [Azure Repos](https://azure.microsoft.com/services/devops/repos/), one of the services in Azure DevOps. Supports both Git and Team Foundation Version Control. Used with the [Azure Pipelines build provider](functions-continuous-deployment?tabs=azure-repos*zure-pipelines#build-providers). For more information, see [What is Azure Repos?](/en-us/azure/devops/repos/get-started/what-is-repos).

You can also connect your function app to an external Git repository, but this option requires a manual synchronization. For more information about deployment options, see [Deployment technologies in Azure Functions](functions-deployment-technologies).

Note

Continuous deployment options covered in this article are specific to code-only deployments. For containerized function app deployments, see the **Enable continuous deployment of containers to Azure** section in [Work with containers and Azure Functions](functions-how-to-custom-container).

## Requirements

The unit of deployment for functions in Azure is the function app. For continuous deployment to succeed, the directory structure of your project must be compatible with the basic folder structure that Azure Functions expects. When you create your code project using Azure Functions Core Tools, Visual Studio Code, or Visual Studio, the Azure Functions templates are used to create code projects with the correct directory structure. All functions in a function app are deployed at the same time and in the same package.

After you enable continuous deployment, access to function code in the Azure portal is configured as *read-only* because the *source of truth* is known to reside elsewhere.

Note

The Deployment Center doesn't support enabling continuous deployment for a function app with [inbound network restrictions](functions-networking-options?#inbound-networking-features). You need to instead configure the build provider workflow directly in GitHub or Azure Pipelines. These workflows also require you to use a virtual machine in the same virtual network as the function app as either a [self-hosted agent (Azure Pipelines)](/en-us/azure/devops/pipelines/agents/agents#self-hosted-agents) or a [self-hosted runner (GitHub)](https://docs.github.com/actions/hosting-your-own-runners/managing-self-hosted-runners/about-self-hosted-runners).

## Select a build provider

Building your code project is part of the deployment process. The specific build process depends on your specific language stack, operating system, and hosting plan. Builds can be done locally or remotely, again depending on your specific hosting. For more information, see [Remote build](functions-deployment-technologies#remote-build).

Important

For increased security, consider using a build provider that supports managed identities, including Azure Pipelines and GitHub Actions. The App Service (Kudu) service requires you to [enable basic authentication](#enable-basic-authentication-for-deployments) and work with text-based credentials.

Azure Functions supports these build providers:

Azure Pipelines is one of the services in Azure DevOps and the default build provider for Azure Repos projects. You can also use Azure Pipelines to build projects from GitHub. In Azure Pipelines, there's an [ AzureFunctionApp](/en-us/azure/devops/pipelines/tasks/reference/azure-function-app-v2) task designed specifically for deploying to Azure Functions. This task provides you with control over how the project gets built, packaged, and deployed. Azure Pipelines supports managed identities.

Keep the strengths and limitations of these providers in mind when you enable source control integration. You might need to change your repository source type to take advantage of a specific provider.

## Configure continuous deployment

The [Azure portal](https://portal.azure.com) provides a **Deployment center** for your function apps, which makes it easier to configure continuous deployment. The specific way you configure continuous deployment depends both on the type of source control repository in which your code resides and the [build provider](#build-providers) you choose.

In the [Azure portal](https://portal.azure.com), browse to your function app page and select **Deployment Center** under **Deployment** on the left pane.


Select the **Source** repository type where your project code is being maintained from one of these supported options:

Deployments from Azure Repos that use Azure Pipelines are defined in the [Azure DevOps portal](https://go.microsoft.com/fwlink/?linkid=2245703) and not from your function app. For a step-by-step guide for creating an Azure Pipelines-based deployment from Azure Repos, see [Continuous delivery with Azure Pipelines](functions-how-to-azure-devops).

After deployment finishes, all code from the specified source is deployed to your app. At that point, changes in the deployment source trigger a deployment of those changes to your function app in Azure.

## Enable continuous deployment during app creation

Currently, you can configure continuous deployment from GitHub using GitHub Actions when you create your function app in the Azure portal. You can make this setting on the **Deployment** tab in the **Create Function App** page.

If you want to use a different deployment source or build provider for continuous integration. First, create your function app, and then return to the portal and [set up continuous integration in the Deployment Center](#credentials).

## Enable basic authentication for deployments

In some cases, your function app is created with basic authentication access to the `scm`

endpoint disabled. This blocks publishing by all methods that can't use managed identities to access the `scm`

endpoint. The publishing impacts of having the `scm`

endpoint disabled are detailed in [Deploy without basic authentication](../app-service/configure-basic-auth-disable#deploy-without-basic-authentication).

Important

When you use basic authentication, credentials are sent in clear text. To protect these credentials, you must only access the `scm`

endpoint over an encrypted connection (HTTPS) when using basic authentication. For more information, see [Secure deployment](security-concepts#secure-deployment).

To enable basic authentication to the `scm`

endpoint:

In the

[Azure portal](https://portal.azure.com), go to your function app.On the app's left menu, select

**Settings**>**Configuration**>**General settings**.Set

**SCM Basic Auth Publishing Credentials**to**On**, and then select**Save**.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-web-pubsub-trigger -->

# Azure Web PubSub trigger binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use Azure Web PubSub trigger to handle client events from Azure Web PubSub service.

The trigger endpoint pattern would be as follows, which should be set in Web PubSub service side (Portal: settings -> event handler -> URL Template). In the endpoint pattern, the query part `code=<API_KEY>`

is **REQUIRED** when you're using Azure Function App for [security](function-keys-how-to#understand-keys) reasons. The key can be found in **Azure portal**. Find your function app resource and navigate to **Functions** -> **App keys** -> **System keys** -> **webpubsub_extension** after you deploy the function app to Azure. Though, this key isn't needed when you're working with local functions.

```
<Function_App_Url>/runtime/webhooks/webpubsub?code=<API_KEY>
```


## Example

The following sample shows how to handle user events from clients.

```
[Function("Broadcast")]
public static void Run(
[WebPubSubTrigger("<hub>", WebPubSubEventType.User, "message")] UserEventRequest request, ILogger log)
{
log.LogInformation($"Request from: {request.ConnectionContext.UserId}");
log.LogInformation($"Request message data: {request.Data}");
log.LogInformation($"Request message dataType: {request.DataType}");
}
```


`WebPubSubTrigger`

binding also supports return value in synchronize scenarios, for example, system `Connect`

and user event, when server can check and deny the client request, or send messages to the caller directly. `Connect`

event respects `ConnectEventResponse`

and `EventErrorResponse`

, and user event respects `UserEventResponse`

and `EventErrorResponse`

, rest types not matching current scenario is ignored.

```
[Function("Broadcast")]
public static UserEventResponse Run(
[WebPubSubTrigger("<hub>", WebPubSubEventType.User, "message")] UserEventRequest request)
{
return new UserEventResponse("[SYSTEM ACK] Received.");
}
```


```
const { app, trigger } = require('@azure/functions');
const wpsTrigger = trigger.generic({
type: 'webPubSubTrigger',
name: 'request',
hub: '<hub>',
eventName: 'message',
eventType: 'user'
});
app.generic('message', {
trigger: wpsTrigger,
handler: async (request, context) => {
context.log('Request from: ', request.connectionContext.userId);
context.log('Request message data: ', request.data);
context.log('Request message dataType: ', request.dataType);
}
});
```


`WebPubSubTrigger`

binding also supports return value in synchronize scenarios, for example, system `Connect`

and user event, when server can check and deny the client request, or send message to the request client directly. In JavaScript weakly typed language, it's deserialized regarding the object keys. And `EventErrorResponse`

has the highest priority compare to rest objects, that if `code`

is in the return, then it's parsed to `EventErrorResponse`

.

Note

Complete samples for this language are pending.

Note

The Web PubSub extensions for Java isn't supported yet.

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Required - must be set to `webPubSubTrigger` . |
direction |
n/a | Required - must be set to `in` . |
name |
n/a | Required - the variable name used in function code for the parameter that receives the event data. |
hub |
Hub | Required - the value must be set to the name of the Web PubSub hub for the function to be triggered. We support set the value in attribute as higher priority, or it can be set in app settings as a global value. |
eventType |
WebPubSubEventType | Required - the value must be set as the event type of messages for the function to be triggered. The value should be either `user` or `system` . |
eventName |
EventName | Required - the value must be set as the event of messages for the function to be triggered. For `system` event type, the event name should be in `connect` , `connected` , `disconnected` . For user-defined subprotocols, the event name is `message` . For system supported subprotocol `json.webpubsub.azure.v1.` , the event name is user-defined event name. |
clientProtocols |
ClientProtocols | Optional - specifies which client protocol can trigger the Web PubSub trigger functions. The following case-insensitive values are valid: `all` : Accepts all client protocols. Default value. `webPubSub` : Accepts only Web PubSub protocols. `mqtt` : Accepts only MQTT protocols. |
connection |
Connection | Optional - the name of an app settings or setting collection that specifies the upstream Azure Web PubSub service. The value is used for signature validation. And the value is auto resolved with app settings `WebPubSubConnectionString` by default. And `null` means the validation isn't needed and always succeed. |

Important

For optimal security, your function app should use managed identities when connecting to the Web PubSub service instead of using a connection string, which contains a shared secret key. For more information, see [Authorize a managed identity request by using Microsoft Entra ID](../azure-web-pubsub/howto-authorize-from-managed-identity).

## Usages

In C#, `WebPubSubEventRequest`

is type recognized binding parameter, rest parameters are bound by parameter name. Check following table for available parameters and types.

In weakly typed language like JavaScript, `name`

in `function.json`

is used to bind the trigger object regarding following mapping table. And respect `dataType`

in `function.json`

to convert message accordingly when `name`

is set to `data`

as the binding object for trigger input. All the parameters can be read from `context.bindingData.<BindingName>`

and is `JObject`

converted.

| Binding Name | Binding Type | Description | Properties |
|---|---|---|---|
| request | `WebPubSubEventRequest` |
Describes the upstream request | Property differs by different event types, including derived classes `ConnectEventRequest` , `MqttConnectEventRequest` , `ConnectedEventRequest` , `MqttConnectedEventRequest` , `UserEventRequest` , `DisconnectedEventRequest` , and `MqttDisconnectedEventRequest` . |
| connectionContext | `WebPubSubConnectionContext` |
Common request information | EventType, EventName, Hub, ConnectionId, UserId, Headers, Origin, Signature, States |
| data | `BinaryData` ,`string` ,`Stream` ,`byte[]` |
Request message data from client in user `message` event |
- |
| dataType | `WebPubSubDataType` |
Request message dataType, which supports `binary` , `text` , `json` |
- |
| claims | `IDictionary<string, string[]>` |
User Claims in system `connect` request |
- |
| query | `IDictionary<string, string[]>` |
User query in system `connect` request |
- |
| subprotocols | `IList<string>` |
Available subprotocols in system `connect` request |
- |
| clientCertificates | `IList<ClientCertificate>` |
A list of certificate thumbprint from clients in system `connect` request |
- |
| reason | `string` |
Reason in system `disconnected` request |
- |

Important

In C#, multiple types supported parameter **MUST** be put in the first, i.e. `request`

or `data`

that other than the default `BinaryData`

type to make the function binding correctly.

### Return response

`WebPubSubTrigger`

respects customer returned response for synchronous events of `connect`

and user event. Only matched response is sent back to service, otherwise, it's ignored. Besides, `WebPubSubTrigger`

return object supports users to `SetState()`

and `ClearStates()`

to manage the metadata for the connection. And the extension merges the results from return value with the original ones from request `WebPubSubConnectionContext.States`

. Value in existing key is overwrite and value in new key is added.

| Return Type | Description | Properties |
|---|---|---|
`ConnectEventResponse` |

`connect`

event`UserEventResponse`

`EventErrorResponse`

`*WebPubSubEventResponse`

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr-output-invoke -->

# Dapr Invoke output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Dapr invoke output binding allows you to invoke another Dapr application during a function execution.

For information on setup and configuration details of the Dapr extension, see the [Dapr extension overview](functions-bindings-dapr).

## Example

A C# function can be created using one of the following C# modes:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).The following example demonstrates using a Dapr invoke output binding to perform a Dapr service invocation operation hosted in another Dapr-ized application. In this example, the function acts like a proxy.

```
[FunctionName("InvokeOutputBinding")]
public static async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Function, "get", Route = "invoke/{appId}/{methodName}")] HttpRequest req,
[DaprInvoke(AppId = "{appId}", MethodName = "{methodName}", HttpVerb = "post")] IAsyncCollector<InvokeMethodParameters> output,
ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
var outputContent = new InvokeMethodParameters
{
Body = requestBody
};
await output.AddAsync(outputContent);
return new OkResult();
}
```


The following example creates a `"InvokeOutputBinding"`

function using the `DaprInvokeOutput`

binding with an `HttpTrigger`

:

```
@FunctionName("InvokeOutputBinding")
public String run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "invoke/{appId}/{methodName}")
HttpRequestMessage<Optional<String>> request,
@DaprInvokeOutput(
appId = "{appId}",
methodName = "{methodName}",
httpVerb = "post")
OutputBinding<String> payload,
final ExecutionContext context)
```


In the following example, the Dapr invoke output binding is paired with an HTTP trigger, which is registered by the `app`

object:

```
const { app, trigger } = require('@azure/functions');
app.generic('InvokeOutputBinding', {
trigger: trigger.generic({
type: 'httpTrigger',
authLevel: 'anonymous',
methods: ['POST'],
route: "invoke/{appId}/{methodName}",
name: "req"
}),
return: daprInvokeOutput,
handler: async (request, context) => {
context.log("Node HTTP trigger function processed a request.");
const payload = await request.text();
context.log(JSON.stringify(payload));
return { body: payload };
}
});
```


The following examples show Dapr triggers in a *function.json* file and PowerShell code that uses those bindings.

Here's the *function.json* file for `daprInvoke`

:

```
{
"bindings":
{
"type": "daprInvoke",
"direction": "out",
"appId": "{appId}",
"methodName": "{methodName}",
"httpVerb": "post",
"name": "payload"
}
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

In code:

```
using namespace System.Net
# Input bindings are passed in via param block.
param($req, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "Powershell InvokeOutputBinding processed a request."
$req_body = $req.Body
$invoke_output_binding_req_body = @{
"body" = $req_body
}
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name payload -Value $invoke_output_binding_req_body
Push-OutputBinding -Name res -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $req_body
})
```


The following example shows a Dapr Invoke output binding, which uses the [v2 Python programming model](functions-reference-python). To use `daprInvoke`

in your Python function app code:

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="InvokeOutputBinding")
@app.route(route="invoke/{appId}/{methodName}", auth_level=dapp.auth_level.ANONYMOUS)
@app.dapr_invoke_output(arg_name = "payload", app_id = "{appId}", method_name = "{methodName}", http_verb = "post")
def main(req: func.HttpRequest, payload: func.Out[str] ) -> str:
# request body must be passed this way "{\"body\":{\"value\":{\"key\":\"some value\"}}}" to use the InvokeOutputBinding, all the data must be enclosed in body property.
logging.info('Python function processed a InvokeOutputBinding request from the Dapr Runtime.')
body = req.get_body()
logging.info(body)
if body is not None:
payload.set(body)
else:
logging.info('req body is none')
return 'ok'
```


## Attributes

In the [in-process model](functions-dotnet-class-library), use the `DaprInvoke`

attribute to define a Dapr invoke output binding, which supports these parameters:

| Parameter | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
AppId |
The Dapr app ID to invoke. | ✔️ | ✔️ |
MethodName |
The method name of the app to invoke. | ✔️ | ✔️ |
HttpVerb |
Optional. HTTP verb to use of the app to invoke. Default is `POST` . |
✔️ | ✔️ |
Body |
Required. The body of the request. |
❌ | ✔️ |

## Annotations

The `DaprInvokeOutput`

annotation allows you to have your function invoke and listen to an output binding.

| Element | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
appId |
The app ID of the application involved in the invoke binding. | ✔️ | ✔️ |
methodName |
The name of the method variable. | ✔️ | ✔️ |
httpVerb |
Post or get. | ✔️ | ✔️ |
body |
Required. The body of the request. |
❌ | ✔️ |

## Configuration

The following table explains the binding configuration properties that you set in the code.

| Property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
appId |
The app ID of the application involved in the invoke binding. | ✔️ | ✔️ |
methods |
Post or get. | ✔️ | ✔️ |
body |
Required. The body of the request. |
❌ | ✔️ |

The following table explains the binding configuration properties that you set in the function.json file.

| function.json property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
appId |
The app ID of the application involved in the invoke binding. | ✔️ | ✔️ |
methodName |
The name of the method variable. | ✔️ | ✔️ |
httpVerb |
Post or get. | ✔️ | ✔️ |
body |
Required. The body of the request. |
❌ | ✔️ |

The following table explains the binding configuration properties for `@dapp.dapr_invoke_output`

that you set in your Python code.

| Property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
app_id |
The app ID of the application involved in the invoke binding. | ✔️ | ✔️ |
method_name |
The name of the method variable. | ✔️ | ✔️ |
http_verb |
Set to `post` or `get` . |
✔️ | ✔️ |
body |
Required. The body of the request. |
❌ | ✔️ |

If properties are defined in both Attributes and `RequestBody`

, priority is given to data provided in `RequestBody`

.

See the [Example section](#example) for complete examples.

## Usage

To use the Dapr service invocation output binding, learn more about [how to use Dapr service invocation in the official Dapr documentation](https://docs.dapr.io/developing-applications/building-blocks/service-invocation/).

To use the `daprInvoke`

in Python v2, set up your project with the correct dependencies.

In your

`requirements.text`

file, add the following line:`azure-functions==1.18.0b3`

In the terminal, install the Python library.

`pip install -r .\requirements.txt`

Modify your

`local.setting.json`

file with the following configuration:`"PYTHON_ISOLATE_WORKER_DEPENDENCIES":1`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/ip-addresses -->

# IP addresses in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains the following concepts related to IP addresses of function apps:

- Locating the IP addresses currently in use by a function app.
- Conditions that cause function app IP addresses to change.
- Restricting the IP addresses that can access a function app.
- Defining dedicated IP addresses for a function app.

IP addresses are associated with function apps, not with individual functions. Incoming HTTP requests can't use the inbound IP address to call individual functions; they must use the default domain name (functionappname.azurewebsites.net) or a custom domain name.

## Function app inbound IP address

Each function app starts out by using a single inbound IP address. When a function app runs in a Consumption or Premium plan, more inbound IP addresses might be added as event-driven scale-out occurs. To find the inbound IP address or addresses being used by your app, use the `nslookup`

utility from your local computer, as in the following example:

```
nslookup <APP_NAME>.azurewebsites.net
```


In this example, replace `<APP_NAME>`

with your function app name. If your app uses a [custom domain name](../app-service/app-service-web-tutorial-custom-domain), use `nslookup`

for that custom domain name instead.

## Function app outbound IP addresses

Each function app has a set of available outbound IP addresses. Any outbound connection from a function, such as to a back-end database, uses one of the available outbound IP addresses as the origin IP address. You can't know beforehand which IP address a given connection uses. For this reason, your back-end service must open its firewall to all of the function app's outbound IP addresses.

Tip

For some platform-level features such as [Key Vault references](../app-service/app-service-key-vault-references), the origin IP might not be one of the outbound IPs, and you shouldn't configure the target resource to rely on these specific addresses. We recommend that the app instead uses a virtual network integration, because the platform routes traffic to the target resource through that network.

To find the outbound IP addresses available to a function app:

- Sign in to the
[Azure Resource Explorer](https://resources.azure.com). - Select
**subscriptions**> {your subscription} >**providers**>**Microsoft.Web**>**sites**. - In the JSON panel, find the site with an
`id`

property that ends in the name of your function app. - See
`outboundIpAddresses`

and`possibleOutboundIpAddresses`

.

The set of `outboundIpAddresses`

is currently available to the function app. The set of `possibleOutboundIpAddresses`

includes IP addresses that are available only if the function app [scales to other pricing tiers](#outbound-ip-address-changes).

Note

When a function app that runs on the [Consumption plan](consumption-plan) or the [Premium plan](functions-premium-plan) is scaled, a new range of outbound IP addresses might be assigned. When running on either of these plans, you can't rely on the reported outbound IP addresses to create a definitive allowlist. To be able to include all potential outbound addresses used during dynamic scaling, you need to add the entire data center to your allowlist.

## Data center outbound IP addresses

If you need to add the outbound IP addresses used by your function apps to an allowlist, another option is to add the function apps' data center (Azure region) to an allowlist. You can [download a JSON file that lists IP addresses for all Azure data centers](https://www.microsoft.com/en-us/download/details.aspx?id=56519). Then find the JSON fragment that applies to the region that your function app runs in.

For example, the following JSON fragment is what the allowlist for Western Europe might look like:

```
{
"name": "AzureCloud.westeurope",
"id": "AzureCloud.westeurope",
"properties": {
"changeNumber": 9,
"region": "westeurope",
"platform": "Azure",
"systemService": "",
"addressPrefixes": [
"13.69.0.0/17",
"13.73.128.0/18",
... Some IP addresses not shown here
"213.199.180.192/27",
"213.199.183.0/24"
]
}
}
```


For information about when this file is updated and when the IP addresses change, expand the **Details** section of the [Download Center page](https://www.microsoft.com/en-us/download/details.aspx?id=56519).

## Inbound IP address changes

The inbound IP address **might** change when you:

- Delete a function app and recreate it in a different resource group.
- Delete the last function app in a resource group and region combination, and re-create it.
- Delete a TLS binding, such as during
[certificate renewal](../app-service/configure-ssl-certificate#renew-an-expiring-certificate).

When your function app runs in a [Consumption plan](consumption-plan) or in a [Premium plan](functions-premium-plan), the inbound IP address might also change even when you haven't taken any actions such as the ones here.

## Outbound IP address changes

The relative stability of the outbound IP address depends on the hosting plan.

### Consumption and Premium plans

Because of autoscaling behaviors, the outbound IP can change at any time when running on a [Consumption plan](consumption-plan) or in a [Premium plan](functions-premium-plan).

If you need to control the outbound IP address of your function app, such as when you need to add it to an allowlist, consider implementing a [virtual network NAT gateway](#virtual-network-nat-gateway-for-outbound-static-ip) while running in a Premium hosting plan. You can also do this by running in a Dedicated (App Service) plan.

### Dedicated plans

When a function app runs on Dedicated (App Service) plans, the set of available outbound IP addresses for a function app might change when you:

- Take any action that can change the inbound IP address.
- Change your Dedicated (App Service) plan pricing tier. The list of all possible outbound IP addresses your app can use, for all pricing tiers, is in the
`possibleOutboundIPAddresses`

property. See[Find outbound IPs](#find-outbound-ip-addresses).

#### Forcing an outbound IP address change

Use the following procedure to deliberately force an outbound IP address change in a Dedicated (App Service) plan:

Scale your App Service plan up or down between Standard and Premium v2 pricing tiers.

Wait 10 minutes.

Scale back to where you started.


## IP address restrictions

You can configure a list of IP addresses that you want to allow or deny access to a function app. For more information, see [Azure App Service access restrictions](../app-service/app-service-ip-restrictions).

## Dedicated IP addresses

There are several strategies to explore when your function app requires static, dedicated IP addresses.

### Virtual network NAT gateway for outbound static IP

You can control the IP address of outbound traffic from your functions by using a virtual network NAT gateway to direct traffic through a static public IP address. You can use this topology when running in a [Premium plan](functions-premium-plan) or in a [Dedicated hosting plan](dedicated-plan). To learn more, see [Tutorial: Control Azure Functions outbound IP with an Azure virtual network NAT gateway](functions-how-to-use-nat-gateway).

### App Service Environments

For full control over the IP addresses, both inbound and outbound, we recommend [App Service Environments](../app-service/environment/intro) (the [Isolated tier](https://azure.microsoft.com/pricing/details/app-service/) of App Service plans). For more information, see [App Service Environment overview](../app-service/environment/overview).

To find out if your function app runs in an App Service Environment:

- Sign in to the
[Azure portal](https://portal.azure.com). - Navigate to the function app.
- Select the
**Overview**tab. - The App Service plan tier appears under
**App Service plan/pricing tier**. The App Service Environment pricing tier is**Isolated**.

The App Service Environment `sku`

is `Isolated`

.

## Next steps

A common cause of IP changes is function app scale changes. [Learn more about function app scaling](functions-scale).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-triggers-bindings -->

# Azure Functions triggers and bindings

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn the high-level concepts surrounding triggers and bindings for functions.

Triggers cause a function to run. A trigger defines how a function is invoked, and a function must have exactly one trigger. Triggers can also pass data into your function, as you would with method calls.

Binding to a function is a way of declaratively connecting your functions to other resources. Bindings either pass data into your function (an *input binding*) or enable you to write data out from your function (an *output binding*) by using *binding parameters*. Your function trigger is essentially a special type of input binding.

You can mix and match bindings to suit your function's specific scenario. Bindings are optional, and a function might have one or multiple input and/or output bindings.

Triggers and bindings let you avoid hardcoding access to other services. Your function receives data (for example, the content of a queue message) in function parameters. You send data (for example, to create a queue message) by using the return value of the function.

Consider the following examples of how you could implement functions:

| Example scenario | Trigger | Input binding | Output binding |
|---|---|---|---|
| A new queue message arrives, which runs a function to write to another queue. | Queue* |
None |
Queue* |
| A scheduled job reads Azure Blob Storage contents and creates a new Azure Cosmos DB document. | Timer | Blob Storage | Azure Cosmos DB |
| Azure Event Grid is used to read an image from Blob Storage and a document from Azure Cosmos DB to send an email. | Event Grid | Blob Storage and Azure Cosmos DB | SendGrid |

* Represents different queues.

These examples aren't meant to be exhaustive, but they illustrate how you can use triggers and bindings together. For a more comprehensive set of scenarios, see [Azure Functions scenarios](functions-scenarios).

Tip

Azure Functions doesn't require you to use input and output bindings to connect to Azure services. You can always create an Azure SDK client in your code and use it instead for your data transfers. For more information, see [Connect to services](functions-reference#connect-to-services).

## Trigger and binding definitions

The following example shows an HTTP-triggered function with an output binding that writes a message to an Azure Storage queue.

For C# class library functions, you configure triggers and bindings by decorating methods and parameters with C# attributes. The specific attribute that you apply might depend on the C# runtime model:

The HTTP trigger (`HttpTrigger`

) is defined on the `Run`

method for a function named `HttpExample`

that returns a `MultiResponse`

object:

```
[Function("HttpExample")]
public static MultiResponse Run([HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequestData req,
FunctionContext executionContext)
{
```


This example shows the `MultiResponse`

object definition. The object definition returns `HttpResponse`

to the HTTP request and writes a message to a storage queue by using a `QueueOutput`

binding:

```
public class MultiResponse
{
[QueueOutput("outqueue",Connection = "AzureWebJobsStorage")]
public string[] Messages { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
```


For more information, see the [C# guide for isolated worker models](dotnet-isolated-process-guide#methods-recognized-as-functions).

Legacy C# script functions use a `function.json`

definition file. For more information, see the [Azure Functions C# script (.csx) developer reference](functions-reference-csharp).

For Java functions, you configure triggers and bindings by annotating specific methods and parameters. This HTTP trigger (`@HttpTrigger`

) is defined on the `run`

method for a function named `HttpExample`

. The function writes to a storage queue named `outqueue`

that the `@QueueOutput`

annotation defines on the `msg`

parameter:

```
@FunctionName("HttpExample")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@QueueOutput(name = "msg", queueName = "outqueue",
connection = "AzureWebJobsStorage") OutputBinding<String> msg,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
```


For more information, see the [Java developer guide](functions-reference-java#triggers-and-annotations).

The way that you define triggers and bindings for Node.js functions depends on the specific version of Node.js for Azure Functions:

In Node.js for Azure Functions version 4, you configure triggers and bindings by using objects exported from the `@azure/functions`

module. For more information, see the [Node.js developer guide](functions-reference-node?pivots=nodejs-model-v4#inputs-and-outputs).

The `http`

method on the exported `app`

object defines an HTTP trigger. The `storageQueue`

method on `output`

defines an output binding on this trigger.

```
const { app, output } = require('@azure/functions');
const queueOutput = output.storageQueue({
queueName: 'outqueue',
connection: 'MyStorageConnectionAppSetting',
});
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraOutputs: [queueOutput],
handler: async (request, context) => {
const body = await request.text();
context.extraOutputs.set(queueOutput, body);
return { body: 'Created queue item.' };
},
});
```


The `http`

method on the exported `app`

object defines an HTTP trigger. The `storageQueue`

method on `output`

defines an output binding on this trigger.

```
import { app, HttpRequest, HttpResponseInit, InvocationContext, output } from '@azure/functions';
const queueOutput = output.storageQueue({
queueName: 'outqueue',
connection: 'MyStorageConnectionAppSetting',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
const body = await request.text();
context.extraOutputs.set(queueOutput, body);
return { body: 'Created queue item.' };
}
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraOutputs: [queueOutput],
handler: httpTrigger1,
});
```


This example `function.json`

file defines the function:

```
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "Request",
"methods": [
"get",
"post"
]
},
{
"type": "http",
"direction": "out",
"name": "Response"
},
{
"type": "queue",
"direction": "out",
"name": "msg",
"queueName": "outqueue",
"connection": "AzureWebJobsStorage"
}
]
}
```


For more information, see the [PowerShell developer guide](functions-reference-powershell#bindings).

The way that the function is defined depends on the version of Python for Azure Functions:

In Python for Azure Functions version 2, you define the function directly in code by using decorators:

```
app = func.FunctionApp(http_auth_level=func.AuthLevel.ANONYMOUS)
@app.route(route="HttpExample")
@app.queue_output(arg_name="msg", queue_name="outqueue", connection="AzureWebJobsStorage")
def HttpExample(req: func.HttpRequest, msg: func.Out [func.QueueMessage]) -> func.HttpResponse:
logging.info('Python HTTP trigger function processed a request.')
```


## Binding considerations

Not all services support both input and output bindings. See your specific binding extension for

[specific code examples for bindings](#code-examples-for-bindings).Triggers and bindings are defined differently depending on the development language. Make sure to select your language at the

[top](#top)of this article.Trigger and binding names are limited to alphanumeric characters and

`_`

, the underscore.

## Task to add bindings to a function

You can connect your function to other services by using input or output bindings. Add a binding by adding its specific definitions to your function. To learn how, see [Add bindings to an existing function in Azure Functions](add-bindings-existing-function).

Azure Functions supports multiple bindings, which must be configured correctly. For example, a function can read data from a queue (input binding) and write data to a database (output binding) simultaneously.

## Supported bindings

This table shows the bindings that are supported in the major versions of the Azure Functions runtime:

| Type | 4.x1 |
1.x2 |
Trigger | Input | Output |
|---|---|---|---|---|---|
|

[Azure Cosmos DB](functions-bindings-cosmosdb-v2)[Azure Data Explorer](functions-bindings-azure-data-explorer)[Azure SQL](functions-bindings-azure-sql)[Dapr](functions-bindings-dapr)4[Event Grid](functions-bindings-event-grid)[Event Hubs](functions-bindings-event-hubs)[HTTP and webhooks](functions-bindings-http-webhook)[IoT Hub](functions-bindings-event-iot)[Kafka](functions-bindings-kafka)3[Mobile Apps](functions-bindings-mobile-apps)[Model Context Protocol](functions-bindings-mcp)[Notification Hubs](functions-bindings-notification-hubs)[Queue Storage](functions-bindings-storage-queue)[Redis](functions-bindings-cache)[RabbitMQ](functions-bindings-rabbitmq)3[SendGrid](functions-bindings-sendgrid)[Service Bus](functions-bindings-service-bus)[Azure SignalR Service](functions-bindings-signalr-service)[Table Storage](functions-bindings-storage-table)[Timer](functions-bindings-timer)[Twilio](functions-bindings-twilio)- Register all bindings except HTTP and timer. See
[Register Azure Functions binding extensions](functions-bindings-register). This step isn't required when using version 1.x of the Functions runtime. [Support ends for version 1.x of the Azure Functions runtime on September 14, 2026](https://aka.ms/azure-functions-retirements/hostv1).[Migrate your apps to version 4.x](migrate-version-1-version-4)for full support.- Triggers aren't supported in the Consumption plan. This binding type requires
[runtime-driven triggers](functions-networking-options#elastic-premium-plan-with-virtual-network-triggers). - This binding type is supported in Kubernetes, Azure IoT Edge, and other self-hosted modes only.

For information about which bindings are in preview or are approved for production use, see [Supported languages](supported-languages).

Specific versions of binding extensions are supported only while the underlying service SDK is supported. Changes to support in the underlying service SDK version affect the support for the consuming extension.

## SDK types

Azure Functions binding extensions use Azure service SDKs to connect to Azure services. The specific SDK types used by bindings can affect how you work with the data in your functions. Some bindings support SDK-specific types that provide richer functionality and better integration with the service, while others use more generic types like strings or byte arrays. When available, using SDK-specific types can provide benefits such as better type safety, easier data manipulation, and access to service-specific features.

This table indicates binding extensions that currently support SDK types:

| Extension | Types | Support level |
|---|---|---|
|

`BlobClient`

`BlobContainerClient`

`BlockBlobClient`

`PageBlobClient`

`AppendBlobClient`

Input: GA

[Azure Cosmos DB](functions-bindings-cosmosdb-v2?tabs=isolated-process,extensionv4&pivots=programming-language-csharp#binding-types)`CosmosClient`

`Database`

`Container`

[Azure Event Grid](functions-bindings-event-grid?tabs=isolated-process,extensionv3&pivots=programming-language-csharp#binding-types)`CloudEvent`

`EventGridEvent`

[Azure Event Hubs](functions-bindings-event-hubs?tabs=isolated-process,extensionv5&pivots=programming-language-csharp#binding-types)`EventData`

`EventHubProducerClient`

[Azure Queue Storage](functions-bindings-storage-queue?tabs=isolated-process,extensionv5&pivots=programming-language-csharp#binding-types)`QueueClient`

`QueueMessage`

[Azure Service Bus](functions-bindings-service-bus?tabs=isolated-process,extensionv5&pivots=programming-language-csharp#binding-types)`ServiceBusClient`

`ServiceBusReceiver`

`ServiceBusSender`

`ServiceBusMessage`

[Azure Table Storage](functions-bindings-storage-table?tabs=isolated-process,table-api&pivots=programming-language-csharp#binding-types)`TableClient`

`TableEntity`

Considerations for SDK types:

- When using
[binding expressions](functions-bindings-expressions-patterns)that rely on trigger data, SDK types for the trigger itself cannot be used. - For output scenarios where you might use an SDK type, create and work with SDK clients directly instead of using an output binding.
- The Azure Cosmos DB trigger uses the
[Azure Cosmos DB change feed](/en-us/azure/cosmos-db/change-feed)and exposes change feed items as JSON-serializable types. As a result, SDK types aren't supported for this trigger.

For more information, see [SDK types](dotnet-isolated-process-guide#sdk-types) in the C# developer guide.

| Extension | Types | Support level | Samples |
|---|---|---|---|
|

`BlobClient`

`ContainerClient`

`StorageStreamDownloader`

Input: GA

[Quickstart](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-python)`BlobClient`

`ContainerClient`

`StorageStreamDownloader`

[Azure Cosmos DB](functions-bindings-cosmosdb-v2)`CosmosClient`

`DatabaseProxy`

`ContainerProxy`

[Quickstart](https://github.com/Azure-Samples/azure-functions-cosmosdb-sdk-bindings-python)`ContainerProxy`

`CosmosClient`

`DatabaseProxy`

[Azure Event Hubs](functions-bindings-event-hubs)`EventData`

[Quickstart](https://github.com/Azure-Samples/azure-functions-eventhub-sdk-bindings-python)`EventData`

[Azure Service Bus](functions-bindings-service-bus)`ServiceBusReceivedMessage`

[Quickstart](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-servicebus/samples/README.md)`ServiceBusReceivedMessage`

Considerations for SDK types:

- For output scenarios where you might use an SDK type, create and work with SDK clients directly instead of using an output binding.
- The Azure Cosmos DB trigger uses the
[Azure Cosmos DB change feed](/en-us/azure/cosmos-db/change-feed)and exposes change feed items as JSON-serializable types. As a result, SDK types aren't supported for this trigger.

SDK types are supported only when using the Python v2 programming model. For more information, see [SDK type bindings](functions-reference-python#sdk-type-bindings) in the Python developer guide.

| Extension | Types | Support level |
|---|---|---|
|

`BlobClient`

`ContainerClient`

`ReadableStream`

[Azure Service Bus](functions-bindings-service-bus)`ServiceBusClient`

`ServiceBusReceiver`

`ServiceBusSender`

`ServiceBusMessage`

SDK types are supported only when using the Node v4 programming model. For more information, see [SDK types](functions-reference-node#sdk-types) in the Node.js developer guide.

| Extension | Types | Support level |
|---|---|---|
|

`BlobClient`

`BlobContainerClient`

For more information, see [SDK types](functions-reference-java#sdk-types) in the Java developer guide.

Important

SDK types aren't currently supported for PowerShell apps.

## Code examples for bindings

Use the following table to find more examples of specific binding types that show you how to work with bindings in your functions. First, choose the language tab that corresponds to your project.

Binding code for C# depends on the [specific process model](dotnet-isolated-process-guide#benefits-of-the-isolated-worker-model).

| Service | Examples | Samples |
|---|---|---|
| Blob Storage |
|

[Link](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/storage/Microsoft.Azure.WebJobs.Extensions.Storage.Blobs)[Trigger](functions-bindings-cosmosdb-v2-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Input](functions-bindings-cosmosdb-v2-input?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-cosmosdb-v2-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/dev/sample/ExtensionsSample/Samples)[Input](functions-bindings-azure-data-explorer-input?pivots=programming-language-csharp#examples)[Output](functions-bindings-azure-data-explorer-output?pivots=programming-language-csharp#examples)[Link](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-csharp)[Trigger](functions-bindings-azure-sql-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Input](functions-bindings-azure-sql-input?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-azure-sql-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](/en-us/samples/azure-samples/azure-sql-binding-func-dotnet-todo/todo-backend-dotnet-azure-sql-bindings-azure-functions/)[Trigger](functions-bindings-event-grid-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-event-grid-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/dev/sample/ExtensionsSample/Samples)[Trigger](functions-bindings-event-hubs-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-event-hubs-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Trigger](functions-bindings-event-iot-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-event-iot-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Trigger](functions-bindings-http-webhook-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd)[Trigger](functions-bindings-storage-queue-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-storage-queue-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/storage/Microsoft.Azure.WebJobs.Extensions.Storage.Queues/samples/functionapp)[Trigger](functions-bindings-rabbitmq-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-rabbitmq-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-sendgrid?tabs=isolated-process&pivots=programming-language-csharp#example)[Trigger](functions-bindings-service-bus-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-service-bus-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/servicebus/Microsoft.Azure.WebJobs.Extensions.ServiceBus)[Trigger](functions-bindings-signalr-service-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Input](functions-bindings-signalr-service-input?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-signalr-service-output?tabs=isolated-process&pivots=programming-language-csharp)[Input](functions-bindings-storage-table-input?tabs=isolated-process&pivots=programming-language-csharp)[Output](functions-bindings-storage-table-output?tabs=isolated-process&pivots=programming-language-csharp)[Trigger](functions-bindings-timer?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/dev/sample/ExtensionsSample/Samples)[Output](functions-bindings-twilio?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/dev/sample/ExtensionsSample/Samples)| Service | Examples | Samples |
|---|---|---|
| Blob Storage |
|

[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Trigger](functions-bindings-cosmosdb-v2-trigger?pivots=programming-language-java#example)[Input](functions-bindings-cosmosdb-v2-input?pivots=programming-language-java#example)[Output](functions-bindings-cosmosdb-v2-output?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/java-functions-eventhub-cosmosdb)[Input](functions-bindings-azure-data-explorer-input?pivots=programming-language-java#examples)[Output](functions-bindings-azure-data-explorer-output?pivots=programming-language-java#examples)[Link](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-java)[Trigger](functions-bindings-azure-sql-trigger?pivots=programming-language-java#example)[Input](functions-bindings-azure-sql-input?pivots=programming-language-java#example)[Output](functions-bindings-azure-sql-output?pivots=programming-language-java#example)[Trigger](functions-bindings-event-grid-trigger?pivots=programming-language-java#example)[Output](functions-bindings-event-grid-output?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Trigger](functions-bindings-event-hubs-trigger?pivots=programming-language-java#example)[Output](functions-bindings-event-hubs-output?pivots=programming-language-java#example)[Trigger](functions-bindings-event-iot-trigger?pivots=programming-language-java#example)[Output](functions-bindings-event-iot-output?pivots=programming-language-java#example)[Trigger](functions-bindings-http-webhook-trigger?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Trigger](functions-bindings-storage-queue-trigger?pivots=programming-language-java#example)[Output](functions-bindings-storage-queue-output?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Trigger](functions-bindings-rabbitmq-trigger?pivots=programming-language-java#example)[Output](functions-bindings-rabbitmq-output?pivots=programming-language-java#example)[Output](functions-bindings-sendgrid?pivots=programming-language-java#example)[Trigger](functions-bindings-service-bus-trigger?pivots=programming-language-java#example)[Output](functions-bindings-service-bus-output?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Trigger](functions-bindings-signalr-service-trigger?pivots=programming-language-java#example)[Input](functions-bindings-signalr-service-input?pivots=programming-language-java#example)[Output](functions-bindings-signalr-service-output?pivots=programming-language-java)[Input](functions-bindings-storage-table-input?pivots=programming-language-java)[Output](functions-bindings-storage-table-output?pivots=programming-language-java)[Trigger](functions-bindings-timer?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Output](functions-bindings-twilio?pivots=programming-language-java#example)| Service | Examples | Samples |
|---|---|---|
| Blob Storage |
|

[Link](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-nodejs)[Trigger](functions-bindings-cosmosdb-v2-trigger?pivots=programming-language-javascript#example)[Input](functions-bindings-cosmosdb-v2-input?pivots=programming-language-javascript#example)[Output](functions-bindings-cosmosdb-v2-output?pivots=programming-language-javascript#example)[Link](https://github.com/Azure-Samples/functions-docs-javascript/tree/master/functions-add-output-binding-cosmosdb-cli-v4-programming-model)[Input](functions-bindings-azure-data-explorer-input?pivots=programming-language-javascript#examples)[Output](functions-bindings-azure-data-explorer-output?pivots=programming-language-javascript#examples)[Trigger](functions-bindings-azure-sql-trigger?pivots=programming-language-javascript#example)[Input](functions-bindings-azure-sql-input?pivots=programming-language-javascript#example)[Output](functions-bindings-azure-sql-output?pivots=programming-language-javascript#example)[Link](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-node)[Trigger](functions-bindings-event-grid-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-event-grid-output?pivots=programming-language-javascript#example)[Trigger](functions-bindings-event-hubs-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-event-hubs-output?pivots=programming-language-javascript#example)[Trigger](functions-bindings-event-iot-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-event-iot-output?pivots=programming-language-javascript#example)[Trigger](functions-bindings-http-webhook-trigger?pivots=programming-language-javascript#example)[Link](https://github.com/Azure-Samples/functions-docs-javascript/tree/master/functions-typescript)[Trigger](functions-bindings-storage-queue-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-storage-queue-output?pivots=programming-language-javascript#example)[Link](https://github.com/Azure-Samples/functions-docs-javascript/tree/master/functions-add-output-binding-storage-queue-cli-v4-programming-model)[Trigger](functions-bindings-rabbitmq-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-rabbitmq-output?pivots=programming-language-javascript#example)[Output](functions-bindings-sendgrid?pivots=programming-language-javascript#example)[Trigger](functions-bindings-service-bus-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-service-bus-output?pivots=programming-language-javascript#example)[Link](https://github.com/Azure-Samples/azure-functions-servicebus-sdk-bindings-nodejs/tree/main/serviceBusSampleWithComplete)[Trigger](functions-bindings-signalr-service-trigger?pivots=programming-language-javascript#example)[Input](functions-bindings-signalr-service-input?pivots=programming-language-javascript#example)[Output](functions-bindings-signalr-service-output?pivots=programming-language-javascript)[Input](functions-bindings-storage-table-input?pivots=programming-language-javascript)[Output](functions-bindings-storage-table-output?pivots=programming-language-javascript)[Trigger](functions-bindings-timer?pivots=programming-language-javascript#example)[Output](functions-bindings-twilio?pivots=programming-language-javascript#example)| Service | Examples | Samples |
|---|---|---|
| Blob Storage |
|

[Trigger](functions-bindings-cosmosdb-v2-trigger?pivots=programming-language-powershell#example)[Input](functions-bindings-cosmosdb-v2-input?pivots=programming-language-powershell#example)[Output](functions-bindings-cosmosdb-v2-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-azure-sql-trigger?pivots=programming-language-powershell#example)[Input](functions-bindings-azure-sql-input?pivots=programming-language-powershell#example)[Output](functions-bindings-azure-sql-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-event-grid-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-event-grid-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-event-hubs-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-event-hubs-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-event-iot-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-event-iot-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-http-webhook-trigger?pivots=programming-language-powershell#example)[Link](https://github.com/Azure-Samples/functions-quickstart-powershell-azd)[Trigger](functions-bindings-storage-queue-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-storage-queue-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-rabbitmq-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-rabbitmq-output?pivots=programming-language-powershell#example)[Output](functions-bindings-sendgrid?pivots=programming-language-powershell#example)[Trigger](functions-bindings-service-bus-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-service-bus-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-signalr-service-trigger?pivots=programming-language-powershell#example)[Input](functions-bindings-signalr-service-input?pivots=programming-language-powershell#example)[Output](functions-bindings-signalr-service-output?pivots=programming-language-powershell)[Input](functions-bindings-storage-table-input?pivots=programming-language-powershell)[Output](functions-bindings-storage-table-output?pivots=programming-language-powershell)[Trigger](functions-bindings-timer?pivots=programming-language-powershell#example)[Output](functions-bindings-twilio?pivots=programming-language-powershell#example)Binding code for Python depends on the Python model version.

| Service | Examples | Samples |
|---|---|---|
| Blob Storage |
|

[Link](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-python)[Trigger](functions-bindings-cosmosdb-v2-trigger?tabs=python-v2&pivots=programming-language-python#example)[Input](functions-bindings-cosmosdb-v2-input?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-cosmosdb-v2-output?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure-Samples/functions-quickstart-python-azd-cosmosdb)[Input](functions-bindings-azure-data-explorer-input?pivots=programming-language-python#examples)[Output](functions-bindings-azure-data-explorer-output?pivots=programming-language-python#examples)[Trigger](functions-bindings-azure-sql-trigger?tabs=python-v2&pivots=programming-language-python#example)[Input](functions-bindings-azure-sql-input?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-azure-sql-output?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-python)[Trigger](functions-bindings-event-grid-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-event-grid-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-event-hubs-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-event-hubs-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-event-iot-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-event-iot-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-http-webhook-trigger?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure-Samples/functions-quickstart-python-http-azd)[Trigger](functions-bindings-storage-queue-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-storage-queue-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-rabbitmq-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-rabbitmq-output?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-sendgrid?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-service-bus-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-service-bus-output?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure-Samples/functions-quickstart-python-azd-service-bus)[Trigger](functions-bindings-signalr-service-trigger?tabs=python-v2&pivots=programming-language-python#example)[Input](functions-bindings-signalr-service-input?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-signalr-service-output?tabs=python-v2&pivots=programming-language-python)[Input](functions-bindings-storage-table-input?tabs=python-v2&pivots=programming-language-python)[Output](functions-bindings-storage-table-output?tabs=python-v2&pivots=programming-language-python)[Trigger](functions-bindings-timer?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-twilio?tabs=python-v2&pivots=programming-language-python#example)## Custom bindings

You can create custom input and output bindings. Bindings must be authored in .NET, but they can be consumed from any supported language. For more information about creating custom bindings, see [Creating custom input and output bindings](https://github.com/Azure/azure-webjobs-sdk/wiki/Creating-custom-input-and-output-bindings).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-service-bus-trigger -->

# Azure Service Bus trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the Service Bus trigger to respond to messages from a Service Bus queue or topic. Starting with extension version 3.1.0, you can trigger on a session-enabled queue or topic.

For information on setup and configuration details, see the [overview](functions-bindings-service-bus).

Service Bus scaling decisions for the Consumption and Premium plans are made based on target-based scaling. For more information, see [Target-based scaling](functions-target-based-scaling).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

## Example

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

This code defines and initializes the `ILogger`

:

```
private readonly ILogger<ServiceBusReceivedMessageFunctions> _logger;
public ServiceBusReceivedMessageFunctions(ILogger<ServiceBusReceivedMessageFunctions> logger)
{
_logger = logger;
}
```


This example shows a [C# function](dotnet-isolated-process-guide) that receives a single Service Bus queue message and writes it to the logs:

```
[Function(nameof(ServiceBusReceivedMessageFunction))]
[ServiceBusOutput("outputQueue", Connection = "ServiceBusConnection")]
public string ServiceBusReceivedMessageFunction(
[ServiceBusTrigger("queue", Connection = "ServiceBusConnection")] ServiceBusReceivedMessage message)
{
_logger.LogInformation("Message ID: {id}", message.MessageId);
_logger.LogInformation("Message Body: {body}", message.Body);
_logger.LogInformation("Message Content-Type: {contentType}", message.ContentType);
var outputMessage = $"Output message created at {DateTime.Now}";
return outputMessage;
}
```


This example shows a [C# function](dotnet-isolated-process-guide) that receives multiple Service Bus queue messages in a single batch and writes each to the logs:

```
[Function(nameof(ServiceBusReceivedMessageBatchFunction))]
public void ServiceBusReceivedMessageBatchFunction(
[ServiceBusTrigger("queue", Connection = "ServiceBusConnection", IsBatched = true)] ServiceBusReceivedMessage[] messages)
{
foreach (ServiceBusReceivedMessage message in messages)
{
_logger.LogInformation("Message ID: {id}", message.MessageId);
_logger.LogInformation("Message Body: {body}", message.Body);
_logger.LogInformation("Message Content-Type: {contentType}", message.ContentType);
}
}
```


This example shows a [C# function](dotnet-isolated-process-guide) that receives multiple Service Bus queue messages, writes it to the logs, and then settles the message as completed:

```
[Function(nameof(ServiceBusMessageActionsFunction))]
public async Task ServiceBusMessageActionsFunction(
[ServiceBusTrigger("queue", Connection = "ServiceBusConnection", AutoCompleteMessages = false)]
ServiceBusReceivedMessage message,
ServiceBusMessageActions messageActions)
{
_logger.LogInformation("Message ID: {id}", message.MessageId);
_logger.LogInformation("Message Body: {body}", message.Body);
_logger.LogInformation("Message Content-Type: {contentType}", message.ContentType);
// Complete the message
await messageActions.CompleteMessageAsync(message);
}
```


The following Java function uses the `@ServiceBusQueueTrigger`

annotation from the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime) to describe the configuration for a Service Bus queue trigger. The function grabs the message placed on the queue and adds it to the logs.

```
@FunctionName("sbprocessor")
public void serviceBusProcess(
@ServiceBusQueueTrigger(name = "msg",
queueName = "myqueuename",
connection = "myconnvarname") String message,
final ExecutionContext context
) {
context.getLogger().info(message);
}
```


Java functions can also be triggered when a message is added to a Service Bus topic. The following example uses the `@ServiceBusTopicTrigger`

annotation to describe the trigger configuration.

```
@FunctionName("sbtopicprocessor")
public void run(
@ServiceBusTopicTrigger(
name = "message",
topicName = "mytopicname",
subscriptionName = "mysubscription",
connection = "ServiceBusConnection"
) String message,
final ExecutionContext context
) {
context.getLogger().info(message);
}
```


This example uses the SDK type [ ServiceBusReceivedMessage](/en-us/javascript/api/@azure/service-bus/servicebusreceivedmessage) obtained from

`ServiceBusMessageContext`

provided by the Service Bus trigger:```
import '@azure/functions-extensions-servicebus'; // Ensure the Service Bus extension is imported
import { app, InvocationContext } from '@azure/functions';
import { ServiceBusMessageContext } from '@azure/functions-extensions-servicebus';
//This a SDKbinding = true
export async function serviceBusQueueTrigger(
serviceBusMessageContext: ServiceBusMessageContext,
context: InvocationContext
): Promise<void> {
const message = serviceBusMessageContext.messages[0];
context.log(message);
// Get current retry count from custom properties, default to 0
const currentRetryCount = message.applicationProperties?.retryCnt ? parseInt(message.applicationProperties.retryCnt as string) : 0;
context.log(`Current retry count: ${currentRetryCount}`);
if (currentRetryCount >= 3) {
// After 3 retries, complete the message to remove it from the queue
context.log(`Maximum retry count (3) reached. Completing message to prevent infinite loop.`);
await serviceBusMessageContext.actions.complete(message);
context.log('Message completed after maximum retries');
} else {
// Abandon with updated retry count
const newRetryCount = currentRetryCount + 1;
const propertiesToModify = {
retryCnt: newRetryCount.toString(),
lastRetryTime: new Date().toISOString(),
errorMessage: "Processing failed"
};
context.log(`Abandoning message with retry count: ${newRetryCount}`);
await serviceBusMessageContext.actions.abandon(message, propertiesToModify);
}
context.log('triggerMetadata: ', context.triggerMetadata);
context.log('Message body:', message.body);
}
app.serviceBusQueue('serviceBusQueueTrigger1', {
connection: 'ServiceBusConnection',
queueName: 'testqueue',
sdkBinding: true,
autoCompleteMessages: false,
cardinality: 'many',
handler: serviceBusQueueTrigger,
});
```


For another example using SDK types see the [exponential backoff strategy sample](https://github.com/Azure/azure-functions-nodejs-extensions/blob/main/azure-functions-nodejs-extensions-servicebus/samples/serviceBusTriggerExponentialBackOff/src/functions/serviceBusTopicTrigger.ts).

For more information, see [SDK types](functions-reference-node#sdk-types) in the Node.js reference article.

The following example shows a Service Bus trigger [TypeScript function](functions-reference-node?tabs=typescript). The function reads [message metadata](#message-metadata) and logs a Service Bus queue message.

```
import { app, InvocationContext } from '@azure/functions';
export async function serviceBusQueueTrigger1(message: unknown, context: InvocationContext): Promise<void> {
context.log('Service bus queue function processed message:', message);
context.log('EnqueuedTimeUtc =', context.triggerMetadata.enqueuedTimeUtc);
context.log('DeliveryCount =', context.triggerMetadata.deliveryCount);
context.log('MessageId =', context.triggerMetadata.messageId);
}
app.serviceBusQueue('serviceBusQueueTrigger1', {
connection: 'MyServiceBusConnection',
queueName: 'testqueue',
handler: serviceBusQueueTrigger1,
});
```


The following example shows a Service Bus trigger [JavaScript function](functions-reference-node). The function reads [message metadata](#message-metadata) and logs a Service Bus queue message.

```
const { app } = require('@azure/functions');
app.serviceBusQueue('serviceBusQueueTrigger1', {
connection: 'MyServiceBusConnection',
queueName: 'testqueue',
handler: (message, context) => {
context.log('Service bus queue function processed message:', message);
context.log('EnqueuedTimeUtc =', context.triggerMetadata.enqueuedTimeUtc);
context.log('DeliveryCount =', context.triggerMetadata.deliveryCount);
context.log('MessageId =', context.triggerMetadata.messageId);
},
});
```


The following example shows a Service Bus trigger binding in a *function.json* file and a [PowerShell function](functions-reference-powershell) that uses the binding.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"name": "mySbMsg",
"type": "serviceBusTrigger",
"direction": "in",
"topicName": "mytopic",
"subscriptionName": "mysubscription",
"connection": "AzureServiceBusConnectionString"
}
]
}
```


Here's the function that runs when a Service Bus message is sent.

```
param([string] $mySbMsg, $TriggerMetadata)
Write-Host "PowerShell ServiceBus queue trigger function processed message: $mySbMsg"
```


This example uses SDK types to directly access the underlying [ ServiceBusReceivedMessage](/en-us/python/api/azure-servicebus/azure.servicebus.servicebusreceivedmessage) object provided by the Service Bus trigger:

```
import logging
import azure.functions as func
import azurefunctions.extensions.bindings.servicebus as servicebus
app = func.FunctionApp(http_auth_level=func.AuthLevel.FUNCTION)
@app.service_bus_queue_trigger(arg_name="receivedmessage",
queue_name="QUEUE_NAME",
connection="SERVICEBUS_CONNECTION")
def servicebus_queue_trigger(receivedmessage: servicebus.ServiceBusReceivedMessage):
logging.info("Python ServiceBus queue trigger processed message.")
logging.info("Receiving: %s\n"
"Body: %s\n"
"Enqueued time: %s\n"
"Lock Token: %s\n"
"Message ID: %s\n"
"Sequence number: %s\n",
receivedmessage,
receivedmessage.body,
receivedmessage.enqueued_time_utc,
receivedmessage.lock_token,
receivedmessage.message_id,
receivedmessage.sequence_number)
```


The function reads various properties of the `ServiceBusReceivedMessage`

type and logs them.

For more examples using Service Bus SDK types, see the [ ServiceBusReceivedMessage](https://github.com/Azure/azure-functions-python-extensions/tree/dev/azurefunctions-extensions-bindings-servicebus/samples/servicebus_samples_single) samples. For a step-by-step tutorial on how to include SDK-type bindings in your function app, follow the

[Python SDK Bindings for Service Bus Sample](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-servicebus/samples/README.md).

Note

Known limitations include:

- The
`message`

property is not supported. - Batch message support requires version 4.1039 or later of the Functions runtime.

To learn more, including what other SDK type bindings are supported, see [SDK type bindings](functions-reference-python#sdk-type-bindings).

This example demonstrates how to read a Service Bus queue message via a trigger. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="ServiceBusQueueTrigger1")
@app.service_bus_queue_trigger(arg_name="msg",
queue_name="<QUEUE_NAME>",
connection="<CONNECTION_SETTING>")
def test_function(msg: func.ServiceBusMessage):
logging.info('Python ServiceBus queue trigger processed message: %s',
msg.get_body().decode('utf-8'))
```


The following example demonstrates how to read a Service Bus queue topic via a trigger.

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="ServiceBusTopicTrigger1")
@app.service_bus_topic_trigger(arg_name="message",
topic_name="TOPIC_NAME",
connection="CONNECTION_SETTING",
subscription_name="SUBSCRIPTION_NAME")
def test_function(message: func.ServiceBusMessage):
message_body = message.get_body().decode("utf-8")
logging.info("Python ServiceBus topic trigger processed message.")
logging.info("Message Body: " + message_body)
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the [ServiceBusTriggerAttribute](https://github.com/Azure/azure-functions-servicebus-extension/blob/master/src/Microsoft.Azure.WebJobs.Extensions.ServiceBus/ServiceBusTriggerAttribute.cs) attribute to define the function trigger. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#service-bus-trigger).

The following table explains the properties you can set using this trigger attribute:

| Property | Description |
|---|---|
QueueName |
Name of the queue to monitor. Set only if monitoring a queue, not for a topic. |
TopicName |
Name of the topic to monitor. Set only if monitoring a topic, not for a queue. |
SubscriptionName |
Name of the subscription to monitor. Set only if monitoring a topic, not for a queue. |
Connection |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

**IsBatched****IsSessionsEnabled**`true`

if connecting to a [session-aware](../service-bus-messaging/message-sessions)queue or subscription.`false`

otherwise, which is the default value.**AutoCompleteMessages**`true`

if the trigger should automatically complete the message after a successful invocation. `false`

if it should not, such as when you are [handling message settlement in code](#usage). If not explicitly set, the behavior is based on the[.](functions-bindings-service-bus#hostjson-settings)`autoCompleteMessages`

configuration in `host.json`

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, the following properties on the `service_bus_queue_trigger`

:

| Property | Description |
|---|---|
`arg_name` |
The name of the variable that represents the queue or topic message in function code. |
`queue_name` |
Name of the queue to monitor. Set only if monitoring a queue, not for a topic. |
`connection` |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

The `ServiceBusQueueTrigger`

annotation allows you to create a function that runs when a Service Bus queue message is created. Configuration options available include the following properties:

| Property | Description |
|---|---|
name |
The name of the variable that represents the queue or topic message in function code. |
queueName |
Name of the queue to monitor. Set only if monitoring a queue, not for a topic. |
topicName |
Name of the topic to monitor. Set only if monitoring a topic, not for a queue. |
subscriptionName |
Name of the subscription to monitor. Set only if monitoring a topic, not for a queue. |
connection |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

The `ServiceBusTopicTrigger`

annotation allows you to designate a topic and subscription to target what data triggers the function.

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

See the trigger [example](#example) for more detail.

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `app.serviceBusQueue()`

or `app.serviceBusTopic()`

methods.

| Property | Description |
|---|---|
queueName |
Name of the queue to monitor. Set only if monitoring a queue, not for a topic. |
topicName |
Name of the topic to monitor. Set only if monitoring a topic, not for a queue. |
subscriptionName |
Name of the subscription to monitor. Set only if monitoring a topic, not for a queue. |
connection |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

**accessRights**`manage`

and `listen`

. The default is `manage`

, which indicates that the `connection`

has the **Manage**permission. If you use a connection string that does not have the**Manage**permission, set`accessRights`

to "listen". Otherwise, the Functions runtime might fail trying to do operations that require manage rights. In Azure Functions version 2.x and higher, this property is not available because the latest version of the Service Bus SDK doesn't support manage operations.**isSessionsEnabled**`true`

if connecting to a [session-aware](../service-bus-messaging/message-sessions)queue or subscription.`false`

otherwise, which is the default value.**autoComplete**`true`

for non-C# functions, which means that the trigger should either automatically call complete after processing, or the function code manually calls complete.When set to

`true`

, the trigger completes the message automatically if the function execution completes successfully, and abandons the message otherwise.Exceptions in the function results in the runtime call

`abandonAsync`

in the background. If no exception occurs, then `completeAsync`

is called in the background. This property is available only in Azure Functions 2.x and higher.When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `serviceBusTrigger` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to "in". This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that represents the queue or topic message in function code. |
queueName |
Name of the queue to monitor. Set only if monitoring a queue, not for a topic. |
topicName |
Name of the topic to monitor. Set only if monitoring a topic, not for a queue. |
subscriptionName |
Name of the subscription to monitor. Set only if monitoring a topic, not for a queue. |
connection |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

**accessRights**`manage`

and `listen`

. The default is `manage`

, which indicates that the `connection`

has the **Manage**permission. If you use a connection string that does not have the**Manage**permission, set`accessRights`

to "listen". Otherwise, the Functions runtime might fail trying to do operations that require manage rights. In Azure Functions version 2.x and higher, this property is not available because the latest version of the Service Bus SDK doesn't support manage operations.**isSessionsEnabled**`true`

if connecting to a [session-aware](../service-bus-messaging/message-sessions)queue or subscription.`false`

otherwise, which is the default value.**autoComplete**`true`

for non-C# functions, which means that the trigger should either automatically call complete after processing, or the function code manually calls complete.When set to

`true`

, the trigger completes the message automatically if the function execution completes successfully, and abandons the message otherwise.Exceptions in the function results in the runtime call

`abandonAsync`

in the background. If no exception occurs, then `completeAsync`

is called in the background. This property is available only in Azure Functions 2.x and higher.When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

See the [Example section](#example) for complete examples.

## Usage

The following parameter types are supported by all C# modalities and extension versions:

| Type | Description |
|---|---|
|
Use when the message is simple text. |
byte[] |
Use for binary data messages. |
Object |
When a message contains JSON, Functions tries to deserialize the JSON data into known plain-old CLR object type. |

Messaging-specific parameter types contain additional message metadata. The specific types supported by the Service Bus trigger depend on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to process a single message, the Service Bus trigger can bind to the following types:

| Type | Description |
|---|---|
`string` |
The message as a string. Use when the message is simple text. |
`byte[]` |
The bytes of the message. |
| JSON serializable types | When an event contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

When binding to

`ServiceBusReceivedMessage`

, you can optionally also include a parameter of type [ServiceBusMessageActions](https://github.com/Azure/azure-functions-dotnet-worker/blob/main/extensions/Worker.Extensions.ServiceBus/src/ServiceBusMessageActions.cs)1,2to perform[message settlement](../service-bus-messaging/message-transfers-locks-settlement#peeklock)actions.When you want the function to process a batch of messages, the Service Bus trigger can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single message types |
An array of events from the batch. Each entry represents one event. When binding to `ServiceBusReceivedMessage[]` , you can optionally also include a parameter of type
1,2 to perform
|

1 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.ServiceBus 5.14.1 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.ServiceBus/5.14.1) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

2 When using `ServiceBusMessageActions`

, set the [ AutoCompleteMessages property of the trigger attribute](functions-bindings-service-bus-trigger#attributes) to

`false`

. This prevents the runtime from attempting to complete messages after a successful function invocation.When the `Connection`

property isn't defined, Functions looks for an app setting named `AzureWebJobsServiceBus`

, which is the default name for the Service Bus connection string. You can also set the `Connection`

property to specify the name of an application setting that contains the Service Bus connection string to use.

The incoming Service Bus message is available via a `ServiceBusQueueMessage`

or `ServiceBusTopicMessage`

parameter.

The Service Bus instance is available via the parameter configured in the *function.json* file's name property.

The queue message is available to the function via a parameter typed as `func.ServiceBusMessage`

. The Service Bus message is passed into the function as either a string or JSON object.

Functions also support Python SDK type bindings for Azure Service Bus, which lets you work with data using these underlying SDK types:

Important

Support for Service Bus SDK types support in Python is in Preview and is only supported for the Python v2 programming model. For more information, see [SDK types in Python](functions-reference-python#sdk-type-bindings).

For a complete example, see [the examples section](#example).

## Connections

The `connection`

property is a reference to environment configuration which specifies how the app should connect to Service Bus. It may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections).

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

To obtain a connection string, follow the steps shown at [Get the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues#get-the-connection-string). The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.

This connection string should be stored in an application setting with a name matching the value specified by the `connection`

property of the binding configuration.

If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name. For example, if you set `connection`

to "MyServiceBus", the Functions runtime looks for an app setting that is named "AzureWebJobsMyServiceBus". If you leave `connection`

empty, the Functions runtime uses the default Service Bus connection string in the app setting that is named "AzureWebJobsServiceBus".

### Identity-based connections

If you are using [version 5.x or higher of the extension](functions-bindings-service-bus?extensionv5), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). To do this, you would define settings under a common prefix which maps to the `connection`

property in the trigger and binding configuration.

In this mode, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Fully Qualified Namespace | `<CONNECTION_NAME_PREFIX>__fullyQualifiedNamespace` |
The fully qualified Service Bus namespace. | <service_bus_namespace>.servicebus.windows.net |

Additional properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

Note

When using [Azure App Configuration](../azure-app-configuration/quickstart-azure-functions-csharp) or [Key Vault](/en-us/azure/key-vault/general/overview) to provide settings for Managed Identity connections, setting names should use a valid key separator such as `:`

or `/`

in place of the `__`

to ensure names are resolved correctly.

For example, `<CONNECTION_NAME_PREFIX>:fullyQualifiedNamespace`

.

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

You'll need to create a role assignment that provides access to your topics and queues at runtime. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) aren't sufficient. The following table shows built-in roles that are recommended when using the Service Bus extension in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles |
|---|---|
Trigger1 |
|

[Azure Service Bus Data Sender](../role-based-access-control/built-in-roles#azure-service-bus-data-sender)1 For triggering from Service Bus topics, the role assignment needs to have effective scope over the Service Bus subscription resource. If only the topic is included, an error will occur. Some clients, such as the Azure portal, don't expose the Service Bus subscription resource as a scope for role assignment. In such cases, the Azure CLI may be used instead. To learn more, see [Azure built-in roles for Azure Service Bus](../service-bus-messaging/service-bus-managed-service-identity#resource-scope).

## Poison messages

Poison message handling can't be controlled or configured in Azure Functions. Service Bus handles poison messages itself.

## PeekLock behavior

The Functions runtime receives a message in [PeekLock mode](../service-bus-messaging/service-bus-performance-improvements#receive-mode).

By default, the runtime calls `Complete`

on the message if the function finishes successfully, or calls `Abandon`

if the function fails. You can disable automatic completion through with the [ autoCompleteMessages property in host.json](functions-bindings-service-bus#hostjson-settings).


By default, the runtime calls `Complete`

on the message if the function finishes successfully, or calls `Abandon`

if the function fails. You can disable automatic completion through with the [ autoCompleteMessages property in host.json](functions-bindings-service-bus#hostjson-settings) or through a


[property on the trigger attribute](#attributes). You should disable automatic completion if your function code handles message settlement.

If the function runs longer than the `PeekLock`

timeout, the lock is automatically renewed as long as the function is running. The `maxAutoRenewDuration`

is configurable in *host.json*, which maps to [ServiceBusProcessor.MaxAutoLockRenewalDuration](/en-us/dotnet/api/azure.messaging.servicebus.servicebusprocessor.maxautolockrenewalduration). The default value of this setting is 5 minutes.

## Message metadata

Messaging-specific types let you easily retrieve [metadata as properties of the object](functions-bindings-expressions-patterns#trigger-metadata). These properties depend on the Functions runtime version, the extension package version, and the C# modality used.

These properties are members of the [ServiceBusReceivedMessage](/en-us/dotnet/api/azure.messaging.servicebus.servicebusreceivedmessage) class.

| Property | Type | Description |
|---|---|---|
`ApplicationProperties` |
`ApplicationProperties` |
Properties set by the sender. |
`ContentType` |
`string` |
A content type identifier utilized by the sender and receiver for application-specific logic. |
`CorrelationId` |
`string` |
The correlation ID. |
`DeliveryCount` |
`Int32` |
The number of deliveries. |
`EnqueuedTime` |
`DateTime` |
The enqueued time in UTC. |
`ScheduledEnqueueTimeUtc` |
`DateTime` |
The scheduled enqueued time in UTC. |
`ExpiresAt` |
`DateTime` |
The expiration time in UTC. |
`MessageId` |
`string` |
A user-defined value that Service Bus can use to identify duplicate messages, if enabled. |
`ReplyTo` |
`string` |
The reply to queue address. |
`Subject` |
`string` |
The application-specific label which can be used in place of the `Label` metadata property. |
`To` |
`string` |
The send to address. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/configure-monitoring -->

# How to configure monitoring for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions integrates with Application Insights to better enable you to monitor your function apps. Application Insights, a feature of Azure Monitor, is an extensible Application Performance Management (APM) service that collects data generated by your function app, including information your app writes to logs. Application Insights integration is typically enabled when your function app is created. If your app doesn't have the instrumentation key set, you must first [enable Application Insights integration](#enable-application-insights-integration).

You can use Application Insights without any custom configuration. However, the default configuration can result in high volumes of data. If you're using a Visual Studio Azure subscription, you might hit your data cap for Application Insights. For information about Application Insights costs, see [Application Insights billing](/en-us/azure/azure-monitor/logs/cost-logs#application-insights-billing). For more information, see [Solutions with high-volume of telemetry](#solutions-with-high-volume-of-telemetry).

In this article, you learn how to configure and customize the data that your functions send to Application Insights. You can set common logging configurations in the * host.json* file. By default, these settings also govern custom logs emitted by your code. However, in some cases this behavior can be disabled in favor of options that give you more control over logging. For more information, see

[Custom application logs](#custom-application-logs).

Note

You can use specially configured application settings to represent specific settings in a *host.json* file for a particular environment. Doing so lets you effectively change *host.json* settings without needing to republish the *host.json* file in your project. For more information, see [Override host.json values](functions-host-json#override-hostjson-values).

## Custom application logs

By default, custom application logs you write are sent to the Functions host, which then sends them to Application Insights under the [Worker category](#configure-categories). Some language stacks allow you to instead send the logs directly to Application Insights, which gives you full control over how logs you write are emitted. In this case, the logging pipeline changes from `worker -> Functions host -> Application Insights`

to `worker -> Application Insights`

.

The following table summarizes the configuration options available for each stack:

| Language stack | Where to configure custom logs |
|---|---|
| .NET (in-process model) | `host.json` |
| .NET (isolated model) | Default (send custom logs to the Functions host): `host.json` To send logs directly to Application Insights, see:
|
| Node.js | `host.json` |
| Python | `host.json` |
| Java | Default (send custom logs to the Functions host): `host.json` To send logs directly to Application Insights, see:
|
| PowerShell | `host.json` |

When you configure custom application logs to be sent directly, the host no longer emits them, and `host.json`

no longer controls their behavior. Similarly, the options exposed by each stack apply only to custom logs, and they don't change the behavior of the other runtime logs described in this article. In this case, to control the behavior of all logs, you might need to make changes in both configurations.

## Configure categories

The Azure Functions logger includes a *category* for every log. The category indicates which part of the runtime code or your function code wrote the log. Categories differ between version 1.x and later versions.

Category names are assigned differently in Functions compared to other .NET frameworks. For example, when you use `ILogger<T>`

in ASP.NET, the category is the name of the generic type. C# functions also use `ILogger<T>`

, but instead of setting the generic type name as a category, the runtime assigns categories based on the source. For example:

- Entries related to running a function are assigned a category of
`Function.<FUNCTION_NAME>`

. - Entries created by user code inside the function, such as when calling
`logger.LogInformation()`

, are assigned a category of`Function.<FUNCTION_NAME>.User`

.

The following table describes the main categories of logs that the runtime creates:

| Category | Table | Description |
|---|---|---|
`Function` |
traces |
Includes function started and completed logs for all function runs. For successful runs, these logs are at the `Information` level. Exceptions are logged at the `Error` level. The runtime also creates `Warning` level logs, such as when queue messages are sent to the
|
`Function.<YOUR_FUNCTION_NAME>` |
dependencies |
Dependency data is automatically collected for some services. For successful runs, these logs are at the `Information` level. For more information, see
`Error` level. The runtime also creates `Warning` level logs, such as when queue messages are sent to the
|
`Function.<YOUR_FUNCTION_NAME>` |
customMetricscustomEvents |
C# and JavaScript SDKs lets you collect custom metrics and log custom events. For more information, see
|

`Function.<YOUR_FUNCTION_NAME>`

**traces**`Information`

level. Exceptions are logged at the `Error`

level. The runtime also creates `Warning`

level logs, such as when queue messages are sent to the [poison queue](functions-bindings-storage-queue-trigger#poison-messages).`Function.<YOUR_FUNCTION_NAME>.User`

**traces**[Writing to logs](functions-monitoring#writing-to-logs).`Host.Aggregator`

**customMetrics**[configurable](#configure-the-aggregator)period of time. The default period is 30 seconds or 1,000 results, whichever comes first. Examples are the number of runs, success rate, and duration. All of these logs are written at the`Information`

level. If you filter at `Warning`

or higher, you don't see any of this data.`Host.Results`

**requests**`Information`

level. If you filter at `Warning`

or higher, you don't see any of this data.`Microsoft`

**traces**`Worker`

**traces**`Microsoft.*`

category, such as `Microsoft.Azure.WebJobs.Script.Workers.Rpc.RpcFunctionInvocationDispatcher`

. These logs are written at the `Information`

level.Note

For .NET class library functions, these categories assume you're using `ILogger`

and not `ILogger<T>`

. For more information, see the [Functions ILogger documentation](functions-dotnet-class-library#ilogger).

The **Table** column indicates to which table in Application Insights the log is written.

## Configure log levels

A *log level* is assigned to every log. The value is an integer that indicates relative importance:

| LogLevel | Code | Description |
|---|---|---|
| Trace | 0 | Logs that contain the most detailed messages. These messages might contain sensitive application data. These messages are disabled by default and should never be enabled in a production environment. |
| Debug | 1 | Logs that are used for interactive investigation during development. These logs should primarily contain information useful for debugging and have no long-term value. |
| Information | 2 | Logs that track the general flow of the application. These logs should have long-term value. |
| Warning | 3 | Logs that highlight an abnormal or unexpected event in the application flow, but don't otherwise cause the application execution to stop. |
| Error | 4 | Logs that highlight when the current flow of execution is stopped because of a failure. These errors should indicate a failure in the current activity, not an application-wide failure. |
| Critical | 5 | Logs that describe an unrecoverable application or system crash, or a catastrophic failure that requires immediate attention. |
| None | 6 | Disables logging for the specified category. |

The [ host.json file](functions-host-json) configuration determines how much logging a functions app sends to Application Insights.

For each category, you indicate the minimum log level to send. The *host.json* settings vary depending on the [Functions runtime version](functions-versions).

The following examples define logging based on the following rules:

- The default logging level is set to
`Warning`

to prevent[excessive logging](#solutions-with-high-volume-of-telemetry)for unanticipated categories. `Host.Aggregator`

and`Host.Results`

are set to lower levels. Setting logging levels too high (especially higher than`Information`

) can result in loss of metrics and performance data.- Logging for function runs is set to
`Information`

. If necessary, you can[override](functions-host-json#override-hostjson-values)this setting in local development to`Debug`

or`Trace`

.

```
{
"logging": {
"fileLoggingMode": "debugOnly",
"logLevel": {
"default": "Warning",
"Host.Aggregator": "Trace",
"Host.Results": "Information",
"Function": "Information"
}
}
}
```


If * host.json* includes multiple logs that start with the same string, the more defined logs ones are matched first. Consider the following example that logs everything in the runtime, except

`Host.Aggregator`

, at the `Error`

level:```
{
"logging": {
"fileLoggingMode": "debugOnly",
"logLevel": {
"default": "Information",
"Host": "Error",
"Function": "Error",
"Host.Aggregator": "Information"
}
}
}
```


You can use a log level setting of `None`

to prevent any logs from being written for a category.

Caution

Azure Functions integrates with Application Insights by storing telemetry events in Application Insights tables. If you set a category log level to any value different from `Information`

, it prevents the telemetry from flowing to those tables, and you won't be able to see related data in the **Application Insights** and **Function Monitor** tabs.

For example, for the previous samples:

- If you set the
`Host.Results`

category to the`Error`

log level, Azure gathers only host execution telemetry events in the`requests`

table for failed function executions, preventing the display of host execution details of successful executions in both the**Application Insights**and**Function Monitor**tabs. - If you set the
`Function`

category to the`Error`

log level, it stops gathering function telemetry data related to`dependencies`

,`customMetrics`

, and`customEvents`

for all the functions, preventing you from viewing any of this data in Application Insights. Azure gathers only`traces`

logged at the`Error`

level.

In both cases, Azure continues to collect errors and exceptions data in the **Application Insights** and **Function Monitor** tabs. For more information, see [Solutions with high-volume of telemetry](#solutions-with-high-volume-of-telemetry).

## Configure the aggregator

As noted in the previous section, the runtime aggregates data about function executions over a period of time. The default period is 30 seconds or 1,000 runs, whichever comes first. You can configure this setting in the * host.json* file. For example:

```
{
"aggregator": {
"batchSize": 1000,
"flushTimeout": "00:00:30"
}
}
```


## Configure sampling

Application Insights has a [sampling](/en-us/azure/azure-monitor/app/sampling) feature that can protect you from producing too much telemetry data on completed executions at times of peak load. When the rate of incoming executions exceeds a specified threshold, Application Insights starts to randomly ignore some of the incoming executions. The default setting for maximum number of executions per second is 20 (five in version 1.x). You can configure sampling in [ host.json](functions-host-json#applicationinsights). Here's an example:

```
{
"logging": {
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"maxTelemetryItemsPerSecond" : 20,
"excludedTypes": "Request;Exception"
}
}
}
}
```


You can exclude certain types of telemetry from sampling. In this example, data of type `Request`

and `Exception`

is excluded from sampling. It ensures that *all* function executions (requests) and exceptions are logged while other types of telemetry remain subject to sampling.

If your project uses a dependency on the Application Insights SDK to do manual telemetry tracking, you might experience unusual behavior if your sampling configuration differs from the sampling configuration in your function app. In such cases, use the same sampling configuration as the function app. For more information, see [Sampling in Application Insights](/en-us/azure/azure-monitor/app/sampling).

## Enable SQL query collection

Application Insights automatically collects data on dependencies for HTTP requests, database calls, and for several bindings. For more information, see [Dependencies](functions-monitoring#dependencies). For SQL calls, the name of the server and database is always collected and stored, but SQL query text isn't collected by default. You can use `dependencyTrackingOptions.enableSqlCommandTextInstrumentation`

to enable SQL query text logging by using the following settings (at a minimum) in your [host.json file](functions-host-json#applicationinsightsdependencytrackingoptions):

```
"logging": {
"applicationInsights": {
"enableDependencyTracking": true,
"dependencyTrackingOptions": {
"enableSqlCommandTextInstrumentation": true
}
}
}
```


For more information, see [Advanced SQL tracking to get full SQL query](/en-us/azure/azure-monitor/app/asp-net-dependencies#advanced-sql-tracking-to-get-full-sql-query).

## Configure scale controller logs

*This feature is in preview.*

You can have the [Azure Functions scale controller](event-driven-scaling#runtime-scaling) emit logs to either Application Insights or to Blob storage to better understand the decisions the scale controller is making for your function app.

To enable this feature, add an application setting named `SCALE_CONTROLLER_LOGGING_ENABLED`

to your function app settings. The following value of the setting must be in the format `<DESTINATION>:<VERBOSITY>`

. For more information, see the following table:

| Property | Description |
|---|---|
`<DESTINATION>` |
The destination to which logs are sent. Valid values are `AppInsights` and `Blob` .When you use `AppInsights` , ensure that the
When you set the destination to `Blob` , logs are created in a blob container named `azure-functions-scale-controller` in the default storage account set in the `AzureWebJobsStorage` application setting. |
`<VERBOSITY>` |
Specifies the level of logging. Supported values are `None` , `Warning` , and `Verbose` .When set to `Verbose` , the scale controller logs a reason for every change in the worker count, and information about the triggers that factor into those decisions. Verbose logs include trigger warnings and the hashes used by the triggers before and after the scale controller runs. |

Tip

Keep in mind that while you leave scale controller logging enabled, it impacts the [potential costs of monitoring your function app](functions-monitoring#application-insights-pricing-and-limits). Consider enabling logging until you collect enough data to understand how the scale controller is behaving, and then disabling it.

For example, the following Azure CLI command turns on verbose logging from the scale controller to Application Insights:

```
az functionapp config appsettings set --name <FUNCTION_APP_NAME> \
--resource-group <RESOURCE_GROUP_NAME> \
--settings SCALE_CONTROLLER_LOGGING_ENABLED=AppInsights:Verbose
```


In this example, replace `<FUNCTION_APP_NAME>`

and `<RESOURCE_GROUP_NAME>`

with the name of your function app and the resource group name, respectively.

The following Azure CLI command disables logging by setting the verbosity to `None`

:

```
az functionapp config appsettings set --name <FUNCTION_APP_NAME> \
--resource-group <RESOURCE_GROUP_NAME> \
--settings SCALE_CONTROLLER_LOGGING_ENABLED=AppInsights:None
```


You can also disable logging by removing the `SCALE_CONTROLLER_LOGGING_ENABLED`

setting using the following Azure CLI command:

```
az functionapp config appsettings delete --name <FUNCTION_APP_NAME> \
--resource-group <RESOURCE_GROUP_NAME> \
--setting-names SCALE_CONTROLLER_LOGGING_ENABLED
```


With scale controller logging enabled, you're now able to [query your scale controller logs](analyze-telemetry-data#query-scale-controller-logs).

## Enable Application Insights integration

For a function app to send data to Application Insights, it needs to connect to the Application Insights resource using **only one** of these application settings:

| Setting name | Description |
|---|---|
`APPLICATIONINSIGHTS_CONNECTION_STRING` |
This setting is recommended and is required when your Application Insights instance runs in a sovereign cloud. The connection string supports other
|

`APPINSIGHTS_INSTRUMENTATIONKEY`

When you create your function app in the [Azure portal](functions-get-started) from the command line by using [Azure Functions Core Tools](how-to-create-function-azure-cli?pivots=programming-language-csharp) or [Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-csharp), Application Insights integration is enabled by default. The Application Insights resource has the same name as your function app, and is created either in the same region or in the nearest region.

### Require Microsoft Entra authentication

You can use the [ APPLICATIONINSIGHTS_AUTHENTICATION_STRING](functions-app-settings#applicationinsights_authentication_string) setting to enable connections to Application Insights using Microsoft Entra authentication. This creates a consistent authentication experience across all Application Insights pipelines, including Profiler and Snapshot Debugger, as well as from the Functions host and language-specific agents.

Note

There's currently no Microsoft Entra ID authentication support for local development.

When Ingesting data in a sovereign cloud, Microsoft Entra ID authentication isn't available when using the Application Insights SDK. OpenTelemetry-based data collection supports Microsoft Entra ID authentication across all cloud environments, including sovereign clouds.

The value contains either `Authorization=AAD`

for a system-assigned managed identity or `ClientId=<YOUR_CLIENT_ID>;Authorization=AAD`

for a user-assigned managed identity. The managed identity must already be available to the function app, with an assigned role equivalent to [Monitoring Metrics Publisher](/en-us/azure/role-based-access-control/built-in-roles/monitor#monitoring-metrics-publisher). For more information, see [Microsoft Entra authentication for Application Insights](/en-us/azure/azure-monitor/app/azure-ad-authentication).

The [ APPLICATIONINSIGHTS_CONNECTION_STRING](functions-app-settings#applicationinsights_connection_string) setting is still required.

Note

When using `APPLICATIONINSIGHTS_AUTHENTICATION_STRING`

to connect to Application Insights using Microsoft Entra authentication, you should also [Disable local authentication for Application Insights](/en-us/azure/azure-monitor/app/azure-ad-authentication#disable-local-authentication). This configuration requires Microsoft Entra authentication in order for telemetry to be ingested into your workspace.

### New function app in the portal

To review the Application Insights resource being created, select it to expand the **Application Insights** window. You can change the **New resource name** or select a different **Location** in an [Azure geography](https://azure.microsoft.com/global-infrastructure/geographies/) where you want to store your data.


When you select **Create**, an Application Insights resource is created with your function app, which has the `APPLICATIONINSIGHTS_CONNECTION_STRING`

set in application settings. Everything is ready to go.

### Add to an existing function app

If an Application Insights resource wasn't created with your function app, use the following steps to create the resource. You can then add the connection string from that resource as an [application setting](functions-how-to-use-azure-function-app-settings#settings) in your function app.

In the

[Azure portal](https://portal.azure.com), search for and select**function app**, and then select your function app.Select the

**Application Insights is not configured**banner at the top of the window. If you don't see this banner, then your app might already have Application Insights enabled.Expand

**Change your resource**and create an Application Insights resource by using the settings specified in the following table:Setting Suggested value Description **New resource name**Unique app name It's easiest to use the same name as your function app, which must be unique in your subscription. **Location**West Europe If possible, use the same [region](https://azure.microsoft.com/regions/)as your function app, or the one that's close to that region.Select

**Apply**.The Application Insights resource is created in the same resource group and subscription as your function app. After the resource is created, close the

**Application Insights**window.In your function app, expand

**Settings**, and then select**Environment variables**. In the**App settings**tab, if you see an app setting named`APPLICATIONINSIGHTS_CONNECTION_STRING`

, Application Insights integration is enabled for your function app running in Azure. If this setting doesn't exist, add it by using your Application Insights connection string as the value.

Note

Older function apps might use `APPINSIGHTS_INSTRUMENTATIONKEY`

instead of `APPLICATIONINSIGHTS_CONNECTION_STRING`

. When possible, update your app to use the connection string instead of the instrumentation key.

## Disable built-in logging

Early versions of Functions used built-in monitoring, which is no longer recommended. When you enable Application Insights, disable the built-in logging that uses Azure Storage. The built-in logging is useful for testing with light workloads, but isn't intended for high-load production use. For production monitoring, we recommend Application Insights. If you use built-in logging in production, the logging record might be incomplete because of throttling on Azure Storage.

To disable built-in logging, delete the `AzureWebJobsDashboard`

app setting. For more information about how to delete app settings in the Azure portal, see the **Application settings** section of [How to manage a function app](functions-how-to-use-azure-function-app-settings#settings). Before you delete the app setting, ensure that no existing functions in the same function app use the setting for Azure Storage triggers or bindings.

## Solutions with high volume of telemetry

Function apps are an essential part of solutions that can cause high volumes of telemetry, such as IoT solutions, rapid event driven solutions, high load financial systems, and integration systems. In this case, you should consider extra configuration to reduce costs while maintaining observability.

The generated telemetry can be consumed in real-time dashboards, alerting, detailed diagnostics, and so on. Depending on how the generated telemetry is consumed, you need to define a strategy to reduce the volume of data generated. This strategy allows you to properly monitor, operate, and diagnose your function apps in production. Consider the following options:

**Use the correct table plan**:[Table plans](/en-us/azure/azure-monitor/logs/data-platform-logs#table-plans)help you manage data costs by controlling how often you use the data in a table and the kind of analysis you need to perform. To reduce costs, you can choose the`Basic`

plan, which does lack some features available in the`Analytics`

plan.**Use sampling**: As mentioned[previously](#configure-sampling), sampling helps to dramatically reduce the volume of telemetry events ingested while maintaining a statistically correct analysis. It could happen that even using sampling you still get a high volume of telemetry. Inspect the options that[adaptive sampling](/en-us/azure/azure-monitor/app/sampling#configuring-adaptive-sampling-for-aspnet-applications)provides to you. For example, set the`maxTelemetryItemsPerSecond`

to a value that balances the volume generated with your monitoring needs. Keep in mind that the telemetry sampling is applied per host executing your function app.**Default log level**: Use`Warning`

or`Error`

as the default value for all telemetry categories. Later, you can decide which[categories](#configure-categories)you want to set at the`Information`

level, so that you can monitor and diagnose your functions properly.**Tune your functions telemetry**: With the default log level set to`Error`

or`Warning`

, no detailed information from each function is gathered (dependencies, custom metrics, custom events, and traces). For those functions that are key for production monitoring, define an explicit entry for the`Function.<YOUR_FUNCTION_NAME>`

category and set it to`Information`

, so that you can gather detailed information. To avoid gathering[user-generated logs](functions-monitoring#writing-to-logs)at the`Information`

level, set the`Function.<YOUR_FUNCTION_NAME>.User`

category to the`Error`

or`Warning`

log level.**Host.Aggregator category**: As described in[configure categories](#configure-categories), this category provides aggregated information of function invocations. The information from this category is gathered in the Application Insights`customMetrics`

table, and is shown in the function**Overview**tab in the Azure portal. Depending on how you configure the aggregator, consider that there can be a delay, determined by the`flushTimeout`

setting, in the telemetry gathered. If you set this category to a value different from`Information`

, you stop gathering the data in the`customMetrics`

table and don't display metrics in the function**Overview**tab.The following screenshot shows

`Host.Aggregator`

telemetry data displayed in the function**Overview**tab:The following screenshot shows

`Host.Aggregator`

telemetry data in Application Insights`customMetrics`

table:**Host.Results category**: As described in[configure categories](#configure-categories), this category provides the runtime-generated logs indicating the success or failure of a function invocation. The information from this category is gathered in the Application Insights`requests`

table, and is shown in the function**Monitor**tab and in different Application Insights dashboards (Performance, Failures, and so on). If you set this category to a value different than`Information`

, you gather only telemetry generated at the log level defined (or higher). For example, setting it to`error`

results in tracking requests data only for failed executions.The following screenshot shows the

`Host.Results`

telemetry data displayed in the function**Monitor**tab:The following screenshot shows

`Host.Results`

telemetry data displayed in Application Insights Performance dashboard:**Host.Aggregator vs Host.Results**: Both categories provide good insights about function executions. If needed, you can remove the detailed information from one of these categories, so that you can use the other for monitoring and alerting. Here's a sample:

```
{
"version": "2.0",
"logging": {
"logLevel": {
"default": "Warning",
"Function": "Error",
"Host.Aggregator": "Error",
"Host.Results": "Information",
"Function.Function1": "Information",
"Function.Function1.User": "Error"
},
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"maxTelemetryItemsPerSecond": 1,
"excludedTypes": "Exception"
}
}
}
}
```


With this configuration:

The default value for all functions and telemetry categories is set to

`Warning`

(including Microsoft and Worker categories). So, by default, all errors and warnings generated by runtime and custom logging are gathered.The

`Function`

category log level is set to`Error`

, so for all functions, by default, only exceptions and error logs are gathered. Dependencies, user-generated metrics, and user-generated events are skipped.For the

`Host.Aggregator`

category, as it's set to the`Error`

log level, aggregated information from function invocations isn't gathered in the`customMetrics`

Application Insights table, and information about executions counts (total, successful, and failed) aren't shown in the function overview dashboard.For the

`Host.Results`

category, all the host execution information is gathered in the`requests`

Application Insights table. All the invocations results are shown in the function Monitor dashboard and in Application Insights dashboards.For the function called

`Function1`

, we set the log level to`Information`

. So, for this concrete function, all the telemetry is gathered (dependency, custom metrics, and custom events). For the same function, we set the`Function1.User`

category (user-generated traces) to`Error`

, so only custom error logging is gathered.Note

Configuration per function isn't supported in v1.x of the Functions runtime.

Sampling is configured to send one telemetry item per second per type, excluding the exceptions. This sampling happens for each server host running our function app. So, if we have four instances, this configuration emits four telemetry items per second per type and all the exceptions that might occur.

Note

Metric counts such as request rate and exception rate are adjusted to compensate for the sampling rate, so that they show approximately correct values in Metric Explorer.


Tip

Experiment with different configurations to ensure that you cover your requirements for logging, monitoring, and alerting. Also, ensure that you have detailed diagnostics in case of unexpected errors or malfunctioning.

## Overriding monitoring configuration at runtime

Finally, there could be situations where you need to quickly change the logging behavior of a certain category in production, and you don't want to make a whole deployment just for a change in the *host.json* file. For such cases, you can override the [host.json values](functions-host-json#override-hostjson-values).

To configure these values at App settings level (and avoid redeployment on just *host.json* changes), you should override specific `host.json`

values by creating an equivalent value as an application setting. When the runtime finds an application setting in the format `AzureFunctionsJobHost__path__to__setting`

, it overrides the equivalent `host.json`

setting located at `path.to.setting`

in the JSON. When expressed as an application setting, a double underscore (`__`

) replaces the dot (`.`

) used to indicate JSON hierarchy. For example, you can use the following app settings to configure individual function log levels in `host.json`

.

| Host.json path | App setting |
|---|---|
| logging.logLevel.default | AzureFunctionsJobHost__logging__logLevel__default |
| logging.logLevel.Host.Aggregator | AzureFunctionsJobHost__logging__logLevel__Host.Aggregator |
| logging.logLevel.Function | AzureFunctionsJobHost__logging__logLevel__Function |
| logging.logLevel.Function.Function1 | AzureFunctionsJobHost__logging__logLevel__Function.Function1 |
| logging.logLevel.Function.Function1.User | AzureFunctionsJobHost__logging__logLevel__Function.Function1.User |

You can override the settings directly at the Azure portal Function App Configuration pane or by using an Azure CLI or PowerShell script.

```
az functionapp config appsettings set --name MyFunctionApp --resource-group MyResourceGroup --settings "AzureFunctionsJobHost__logging__logLevel__Host.Aggregator=Information"
```


Note

Overriding the `host.json`

through changing app settings will restart your function app.
App settings that contain a period aren't supported when running on Linux in an Elastic Premium plan or a Dedicated (App Service) plan. In these hosting environments, you should continue to use the *host.json* file.

## Monitor function apps using Health check

You can use the Health Check feature to monitor function apps on the Premium (Elastic Premium) and Dedicated (App Service) plans. Health check isn't an option for the Flex Consumption and Consumption plans. To learn how to configure it, see [Monitor App Service instances using Health check](../app-service/monitor-instances-health-check). Your function app should have an HTTP trigger function that responds with an HTTP status code of 200 on the same endpoint as configured on the `Path`

parameter of the health check. You can also have that function perform extra checks to ensure that dependent services are reachable and working.

## Related content

For more information about monitoring, see:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-continuous-deployment -->

# Continuous deployment for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions enables you to continuously deploy the changes made in a source control repository to a connected function app. This [source control integration](functions-deployment-technologies#source-control) enables a workflow in which a code update triggers build, packaging, and deployment from your project to Azure.

You should always configure continuous deployment for a staging slot and not for the production slot. When you use the production slot, code updates are pushed directly to production without being verified in Azure. Instead, enable continuous deployment to a staging slot, verify updates in the staging slot, and after everything runs correctly you can [swap the staging slot code into production](functions-deployment-slots#swap-slots). If you connect to a production slot, make sure that only production-quality code makes it into the integrated code branch.

Steps in this article show you how to configure continuous code deployments to your function app in Azure by using the Deployment Center in the Azure portal. You can also [configure continuous integration using the Azure CLI](/en-us/cli/azure/functionapp/deployment). These steps can target either a staging or a production slot.

Azure Functions supports these sources for continuous deployment to your app:

Maintain your project code in [Azure Repos](https://azure.microsoft.com/services/devops/repos/), one of the services in Azure DevOps. Supports both Git and Team Foundation Version Control. Used with the [Azure Pipelines build provider](functions-continuous-deployment?tabs=azure-repos*zure-pipelines#build-providers). For more information, see [What is Azure Repos?](/en-us/azure/devops/repos/get-started/what-is-repos).

You can also connect your function app to an external Git repository, but this option requires a manual synchronization. For more information about deployment options, see [Deployment technologies in Azure Functions](functions-deployment-technologies).

Note

Continuous deployment options covered in this article are specific to code-only deployments. For containerized function app deployments, see the **Enable continuous deployment of containers to Azure** section in [Work with containers and Azure Functions](functions-how-to-custom-container).

## Requirements

The unit of deployment for functions in Azure is the function app. For continuous deployment to succeed, the directory structure of your project must be compatible with the basic folder structure that Azure Functions expects. When you create your code project using Azure Functions Core Tools, Visual Studio Code, or Visual Studio, the Azure Functions templates are used to create code projects with the correct directory structure. All functions in a function app are deployed at the same time and in the same package.

After you enable continuous deployment, access to function code in the Azure portal is configured as *read-only* because the *source of truth* is known to reside elsewhere.

Note

The Deployment Center doesn't support enabling continuous deployment for a function app with [inbound network restrictions](functions-networking-options?#inbound-networking-features). You need to instead configure the build provider workflow directly in GitHub or Azure Pipelines. These workflows also require you to use a virtual machine in the same virtual network as the function app as either a [self-hosted agent (Azure Pipelines)](/en-us/azure/devops/pipelines/agents/agents#self-hosted-agents) or a [self-hosted runner (GitHub)](https://docs.github.com/actions/hosting-your-own-runners/managing-self-hosted-runners/about-self-hosted-runners).

## Select a build provider

Building your code project is part of the deployment process. The specific build process depends on your specific language stack, operating system, and hosting plan. Builds can be done locally or remotely, again depending on your specific hosting. For more information, see [Remote build](functions-deployment-technologies#remote-build).

Important

For increased security, consider using a build provider that supports managed identities, including Azure Pipelines and GitHub Actions. The App Service (Kudu) service requires you to [enable basic authentication](#enable-basic-authentication-for-deployments) and work with text-based credentials.

Azure Functions supports these build providers:

Azure Pipelines is one of the services in Azure DevOps and the default build provider for Azure Repos projects. You can also use Azure Pipelines to build projects from GitHub. In Azure Pipelines, there's an [ AzureFunctionApp](/en-us/azure/devops/pipelines/tasks/reference/azure-function-app-v2) task designed specifically for deploying to Azure Functions. This task provides you with control over how the project gets built, packaged, and deployed. Azure Pipelines supports managed identities.

Keep the strengths and limitations of these providers in mind when you enable source control integration. You might need to change your repository source type to take advantage of a specific provider.

## Configure continuous deployment

The [Azure portal](https://portal.azure.com) provides a **Deployment center** for your function apps, which makes it easier to configure continuous deployment. The specific way you configure continuous deployment depends both on the type of source control repository in which your code resides and the [build provider](#build-providers) you choose.

In the [Azure portal](https://portal.azure.com), browse to your function app page and select **Deployment Center** under **Deployment** on the left pane.


Select the **Source** repository type where your project code is being maintained from one of these supported options:

Deployments from Azure Repos that use Azure Pipelines are defined in the [Azure DevOps portal](https://go.microsoft.com/fwlink/?linkid=2245703) and not from your function app. For a step-by-step guide for creating an Azure Pipelines-based deployment from Azure Repos, see [Continuous delivery with Azure Pipelines](functions-how-to-azure-devops).

After deployment finishes, all code from the specified source is deployed to your app. At that point, changes in the deployment source trigger a deployment of those changes to your function app in Azure.

## Enable continuous deployment during app creation

Currently, you can configure continuous deployment from GitHub using GitHub Actions when you create your function app in the Azure portal. You can make this setting on the **Deployment** tab in the **Create Function App** page.

If you want to use a different deployment source or build provider for continuous integration. First, create your function app, and then return to the portal and [set up continuous integration in the Deployment Center](#credentials).

## Enable basic authentication for deployments

In some cases, your function app is created with basic authentication access to the `scm`

endpoint disabled. This blocks publishing by all methods that can't use managed identities to access the `scm`

endpoint. The publishing impacts of having the `scm`

endpoint disabled are detailed in [Deploy without basic authentication](../app-service/configure-basic-auth-disable#deploy-without-basic-authentication).

Important

When you use basic authentication, credentials are sent in clear text. To protect these credentials, you must only access the `scm`

endpoint over an encrypted connection (HTTPS) when using basic authentication. For more information, see [Secure deployment](security-concepts#secure-deployment).

To enable basic authentication to the `scm`

endpoint:

In the

[Azure portal](https://portal.azure.com), go to your function app.On the app's left menu, select

**Settings**>**Configuration**>**General settings**.Set

**SCM Basic Auth Publishing Credentials**to**On**, and then select**Save**.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-web-pubsub-trigger -->

# Azure Web PubSub trigger binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use Azure Web PubSub trigger to handle client events from Azure Web PubSub service.

The trigger endpoint pattern would be as follows, which should be set in Web PubSub service side (Portal: settings -> event handler -> URL Template). In the endpoint pattern, the query part `code=<API_KEY>`

is **REQUIRED** when you're using Azure Function App for [security](function-keys-how-to#understand-keys) reasons. The key can be found in **Azure portal**. Find your function app resource and navigate to **Functions** -> **App keys** -> **System keys** -> **webpubsub_extension** after you deploy the function app to Azure. Though, this key isn't needed when you're working with local functions.

```
<Function_App_Url>/runtime/webhooks/webpubsub?code=<API_KEY>
```


## Example

The following sample shows how to handle user events from clients.

```
[Function("Broadcast")]
public static void Run(
[WebPubSubTrigger("<hub>", WebPubSubEventType.User, "message")] UserEventRequest request, ILogger log)
{
log.LogInformation($"Request from: {request.ConnectionContext.UserId}");
log.LogInformation($"Request message data: {request.Data}");
log.LogInformation($"Request message dataType: {request.DataType}");
}
```


`WebPubSubTrigger`

binding also supports return value in synchronize scenarios, for example, system `Connect`

and user event, when server can check and deny the client request, or send messages to the caller directly. `Connect`

event respects `ConnectEventResponse`

and `EventErrorResponse`

, and user event respects `UserEventResponse`

and `EventErrorResponse`

, rest types not matching current scenario is ignored.

```
[Function("Broadcast")]
public static UserEventResponse Run(
[WebPubSubTrigger("<hub>", WebPubSubEventType.User, "message")] UserEventRequest request)
{
return new UserEventResponse("[SYSTEM ACK] Received.");
}
```


```
const { app, trigger } = require('@azure/functions');
const wpsTrigger = trigger.generic({
type: 'webPubSubTrigger',
name: 'request',
hub: '<hub>',
eventName: 'message',
eventType: 'user'
});
app.generic('message', {
trigger: wpsTrigger,
handler: async (request, context) => {
context.log('Request from: ', request.connectionContext.userId);
context.log('Request message data: ', request.data);
context.log('Request message dataType: ', request.dataType);
}
});
```


`WebPubSubTrigger`

binding also supports return value in synchronize scenarios, for example, system `Connect`

and user event, when server can check and deny the client request, or send message to the request client directly. In JavaScript weakly typed language, it's deserialized regarding the object keys. And `EventErrorResponse`

has the highest priority compare to rest objects, that if `code`

is in the return, then it's parsed to `EventErrorResponse`

.

Note

Complete samples for this language are pending.

Note

The Web PubSub extensions for Java isn't supported yet.

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Required - must be set to `webPubSubTrigger` . |
direction |
n/a | Required - must be set to `in` . |
name |
n/a | Required - the variable name used in function code for the parameter that receives the event data. |
hub |
Hub | Required - the value must be set to the name of the Web PubSub hub for the function to be triggered. We support set the value in attribute as higher priority, or it can be set in app settings as a global value. |
eventType |
WebPubSubEventType | Required - the value must be set as the event type of messages for the function to be triggered. The value should be either `user` or `system` . |
eventName |
EventName | Required - the value must be set as the event of messages for the function to be triggered. For `system` event type, the event name should be in `connect` , `connected` , `disconnected` . For user-defined subprotocols, the event name is `message` . For system supported subprotocol `json.webpubsub.azure.v1.` , the event name is user-defined event name. |
clientProtocols |
ClientProtocols | Optional - specifies which client protocol can trigger the Web PubSub trigger functions. The following case-insensitive values are valid: `all` : Accepts all client protocols. Default value. `webPubSub` : Accepts only Web PubSub protocols. `mqtt` : Accepts only MQTT protocols. |
connection |
Connection | Optional - the name of an app settings or setting collection that specifies the upstream Azure Web PubSub service. The value is used for signature validation. And the value is auto resolved with app settings `WebPubSubConnectionString` by default. And `null` means the validation isn't needed and always succeed. |

Important

For optimal security, your function app should use managed identities when connecting to the Web PubSub service instead of using a connection string, which contains a shared secret key. For more information, see [Authorize a managed identity request by using Microsoft Entra ID](../azure-web-pubsub/howto-authorize-from-managed-identity).

## Usages

In C#, `WebPubSubEventRequest`

is type recognized binding parameter, rest parameters are bound by parameter name. Check following table for available parameters and types.

In weakly typed language like JavaScript, `name`

in `function.json`

is used to bind the trigger object regarding following mapping table. And respect `dataType`

in `function.json`

to convert message accordingly when `name`

is set to `data`

as the binding object for trigger input. All the parameters can be read from `context.bindingData.<BindingName>`

and is `JObject`

converted.

| Binding Name | Binding Type | Description | Properties |
|---|---|---|---|
| request | `WebPubSubEventRequest` |
Describes the upstream request | Property differs by different event types, including derived classes `ConnectEventRequest` , `MqttConnectEventRequest` , `ConnectedEventRequest` , `MqttConnectedEventRequest` , `UserEventRequest` , `DisconnectedEventRequest` , and `MqttDisconnectedEventRequest` . |
| connectionContext | `WebPubSubConnectionContext` |
Common request information | EventType, EventName, Hub, ConnectionId, UserId, Headers, Origin, Signature, States |
| data | `BinaryData` ,`string` ,`Stream` ,`byte[]` |
Request message data from client in user `message` event |
- |
| dataType | `WebPubSubDataType` |
Request message dataType, which supports `binary` , `text` , `json` |
- |
| claims | `IDictionary<string, string[]>` |
User Claims in system `connect` request |
- |
| query | `IDictionary<string, string[]>` |
User query in system `connect` request |
- |
| subprotocols | `IList<string>` |
Available subprotocols in system `connect` request |
- |
| clientCertificates | `IList<ClientCertificate>` |
A list of certificate thumbprint from clients in system `connect` request |
- |
| reason | `string` |
Reason in system `disconnected` request |
- |

Important

In C#, multiple types supported parameter **MUST** be put in the first, i.e. `request`

or `data`

that other than the default `BinaryData`

type to make the function binding correctly.

### Return response

`WebPubSubTrigger`

respects customer returned response for synchronous events of `connect`

and user event. Only matched response is sent back to service, otherwise, it's ignored. Besides, `WebPubSubTrigger`

return object supports users to `SetState()`

and `ClearStates()`

to manage the metadata for the connection. And the extension merges the results from return value with the original ones from request `WebPubSubConnectionContext.States`

. Value in existing key is overwrite and value in new key is added.

| Return Type | Description | Properties |
|---|---|---|
`ConnectEventResponse` |

`connect`

event`UserEventResponse`

`EventErrorResponse`

`*WebPubSubEventResponse`

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr-output-invoke -->

# Dapr Invoke output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Dapr invoke output binding allows you to invoke another Dapr application during a function execution.

For information on setup and configuration details of the Dapr extension, see the [Dapr extension overview](functions-bindings-dapr).

## Example

A C# function can be created using one of the following C# modes:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).The following example demonstrates using a Dapr invoke output binding to perform a Dapr service invocation operation hosted in another Dapr-ized application. In this example, the function acts like a proxy.

```
[FunctionName("InvokeOutputBinding")]
public static async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Function, "get", Route = "invoke/{appId}/{methodName}")] HttpRequest req,
[DaprInvoke(AppId = "{appId}", MethodName = "{methodName}", HttpVerb = "post")] IAsyncCollector<InvokeMethodParameters> output,
ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
var outputContent = new InvokeMethodParameters
{
Body = requestBody
};
await output.AddAsync(outputContent);
return new OkResult();
}
```


The following example creates a `"InvokeOutputBinding"`

function using the `DaprInvokeOutput`

binding with an `HttpTrigger`

:

```
@FunctionName("InvokeOutputBinding")
public String run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "invoke/{appId}/{methodName}")
HttpRequestMessage<Optional<String>> request,
@DaprInvokeOutput(
appId = "{appId}",
methodName = "{methodName}",
httpVerb = "post")
OutputBinding<String> payload,
final ExecutionContext context)
```


In the following example, the Dapr invoke output binding is paired with an HTTP trigger, which is registered by the `app`

object:

```
const { app, trigger } = require('@azure/functions');
app.generic('InvokeOutputBinding', {
trigger: trigger.generic({
type: 'httpTrigger',
authLevel: 'anonymous',
methods: ['POST'],
route: "invoke/{appId}/{methodName}",
name: "req"
}),
return: daprInvokeOutput,
handler: async (request, context) => {
context.log("Node HTTP trigger function processed a request.");
const payload = await request.text();
context.log(JSON.stringify(payload));
return { body: payload };
}
});
```


The following examples show Dapr triggers in a *function.json* file and PowerShell code that uses those bindings.

Here's the *function.json* file for `daprInvoke`

:

```
{
"bindings":
{
"type": "daprInvoke",
"direction": "out",
"appId": "{appId}",
"methodName": "{methodName}",
"httpVerb": "post",
"name": "payload"
}
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

In code:

```
using namespace System.Net
# Input bindings are passed in via param block.
param($req, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "Powershell InvokeOutputBinding processed a request."
$req_body = $req.Body
$invoke_output_binding_req_body = @{
"body" = $req_body
}
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name payload -Value $invoke_output_binding_req_body
Push-OutputBinding -Name res -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $req_body
})
```


The following example shows a Dapr Invoke output binding, which uses the [v2 Python programming model](functions-reference-python). To use `daprInvoke`

in your Python function app code:

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="InvokeOutputBinding")
@app.route(route="invoke/{appId}/{methodName}", auth_level=dapp.auth_level.ANONYMOUS)
@app.dapr_invoke_output(arg_name = "payload", app_id = "{appId}", method_name = "{methodName}", http_verb = "post")
def main(req: func.HttpRequest, payload: func.Out[str] ) -> str:
# request body must be passed this way "{\"body\":{\"value\":{\"key\":\"some value\"}}}" to use the InvokeOutputBinding, all the data must be enclosed in body property.
logging.info('Python function processed a InvokeOutputBinding request from the Dapr Runtime.')
body = req.get_body()
logging.info(body)
if body is not None:
payload.set(body)
else:
logging.info('req body is none')
return 'ok'
```


## Attributes

In the [in-process model](functions-dotnet-class-library), use the `DaprInvoke`

attribute to define a Dapr invoke output binding, which supports these parameters:

| Parameter | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
AppId |
The Dapr app ID to invoke. | ✔️ | ✔️ |
MethodName |
The method name of the app to invoke. | ✔️ | ✔️ |
HttpVerb |
Optional. HTTP verb to use of the app to invoke. Default is `POST` . |
✔️ | ✔️ |
Body |
Required. The body of the request. |
❌ | ✔️ |

## Annotations

The `DaprInvokeOutput`

annotation allows you to have your function invoke and listen to an output binding.

| Element | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
appId |
The app ID of the application involved in the invoke binding. | ✔️ | ✔️ |
methodName |
The name of the method variable. | ✔️ | ✔️ |
httpVerb |
Post or get. | ✔️ | ✔️ |
body |
Required. The body of the request. |
❌ | ✔️ |

## Configuration

The following table explains the binding configuration properties that you set in the code.

| Property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
appId |
The app ID of the application involved in the invoke binding. | ✔️ | ✔️ |
methods |
Post or get. | ✔️ | ✔️ |
body |
Required. The body of the request. |
❌ | ✔️ |

The following table explains the binding configuration properties that you set in the function.json file.

| function.json property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
appId |
The app ID of the application involved in the invoke binding. | ✔️ | ✔️ |
methodName |
The name of the method variable. | ✔️ | ✔️ |
httpVerb |
Post or get. | ✔️ | ✔️ |
body |
Required. The body of the request. |
❌ | ✔️ |

The following table explains the binding configuration properties for `@dapp.dapr_invoke_output`

that you set in your Python code.

| Property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
app_id |
The app ID of the application involved in the invoke binding. | ✔️ | ✔️ |
method_name |
The name of the method variable. | ✔️ | ✔️ |
http_verb |
Set to `post` or `get` . |
✔️ | ✔️ |
body |
Required. The body of the request. |
❌ | ✔️ |

If properties are defined in both Attributes and `RequestBody`

, priority is given to data provided in `RequestBody`

.

See the [Example section](#example) for complete examples.

## Usage

To use the Dapr service invocation output binding, learn more about [how to use Dapr service invocation in the official Dapr documentation](https://docs.dapr.io/developing-applications/building-blocks/service-invocation/).

To use the `daprInvoke`

in Python v2, set up your project with the correct dependencies.

In your

`requirements.text`

file, add the following line:`azure-functions==1.18.0b3`

In the terminal, install the Python library.

`pip install -r .\requirements.txt`

Modify your

`local.setting.json`

file with the following configuration:`"PYTHON_ISOLATE_WORKER_DEPENDENCIES":1`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/ip-addresses -->

# IP addresses in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains the following concepts related to IP addresses of function apps:

- Locating the IP addresses currently in use by a function app.
- Conditions that cause function app IP addresses to change.
- Restricting the IP addresses that can access a function app.
- Defining dedicated IP addresses for a function app.

IP addresses are associated with function apps, not with individual functions. Incoming HTTP requests can't use the inbound IP address to call individual functions; they must use the default domain name (functionappname.azurewebsites.net) or a custom domain name.

## Function app inbound IP address

Each function app starts out by using a single inbound IP address. When a function app runs in a Consumption or Premium plan, more inbound IP addresses might be added as event-driven scale-out occurs. To find the inbound IP address or addresses being used by your app, use the `nslookup`

utility from your local computer, as in the following example:

```
nslookup <APP_NAME>.azurewebsites.net
```


In this example, replace `<APP_NAME>`

with your function app name. If your app uses a [custom domain name](../app-service/app-service-web-tutorial-custom-domain), use `nslookup`

for that custom domain name instead.

## Function app outbound IP addresses

Each function app has a set of available outbound IP addresses. Any outbound connection from a function, such as to a back-end database, uses one of the available outbound IP addresses as the origin IP address. You can't know beforehand which IP address a given connection uses. For this reason, your back-end service must open its firewall to all of the function app's outbound IP addresses.

Tip

For some platform-level features such as [Key Vault references](../app-service/app-service-key-vault-references), the origin IP might not be one of the outbound IPs, and you shouldn't configure the target resource to rely on these specific addresses. We recommend that the app instead uses a virtual network integration, because the platform routes traffic to the target resource through that network.

To find the outbound IP addresses available to a function app:

- Sign in to the
[Azure Resource Explorer](https://resources.azure.com). - Select
**subscriptions**> {your subscription} >**providers**>**Microsoft.Web**>**sites**. - In the JSON panel, find the site with an
`id`

property that ends in the name of your function app. - See
`outboundIpAddresses`

and`possibleOutboundIpAddresses`

.

The set of `outboundIpAddresses`

is currently available to the function app. The set of `possibleOutboundIpAddresses`

includes IP addresses that are available only if the function app [scales to other pricing tiers](#outbound-ip-address-changes).

Note

When a function app that runs on the [Consumption plan](consumption-plan) or the [Premium plan](functions-premium-plan) is scaled, a new range of outbound IP addresses might be assigned. When running on either of these plans, you can't rely on the reported outbound IP addresses to create a definitive allowlist. To be able to include all potential outbound addresses used during dynamic scaling, you need to add the entire data center to your allowlist.

## Data center outbound IP addresses

If you need to add the outbound IP addresses used by your function apps to an allowlist, another option is to add the function apps' data center (Azure region) to an allowlist. You can [download a JSON file that lists IP addresses for all Azure data centers](https://www.microsoft.com/en-us/download/details.aspx?id=56519). Then find the JSON fragment that applies to the region that your function app runs in.

For example, the following JSON fragment is what the allowlist for Western Europe might look like:

```
{
"name": "AzureCloud.westeurope",
"id": "AzureCloud.westeurope",
"properties": {
"changeNumber": 9,
"region": "westeurope",
"platform": "Azure",
"systemService": "",
"addressPrefixes": [
"13.69.0.0/17",
"13.73.128.0/18",
... Some IP addresses not shown here
"213.199.180.192/27",
"213.199.183.0/24"
]
}
}
```


For information about when this file is updated and when the IP addresses change, expand the **Details** section of the [Download Center page](https://www.microsoft.com/en-us/download/details.aspx?id=56519).

## Inbound IP address changes

The inbound IP address **might** change when you:

- Delete a function app and recreate it in a different resource group.
- Delete the last function app in a resource group and region combination, and re-create it.
- Delete a TLS binding, such as during
[certificate renewal](../app-service/configure-ssl-certificate#renew-an-expiring-certificate).

When your function app runs in a [Consumption plan](consumption-plan) or in a [Premium plan](functions-premium-plan), the inbound IP address might also change even when you haven't taken any actions such as the ones here.

## Outbound IP address changes

The relative stability of the outbound IP address depends on the hosting plan.

### Consumption and Premium plans

Because of autoscaling behaviors, the outbound IP can change at any time when running on a [Consumption plan](consumption-plan) or in a [Premium plan](functions-premium-plan).

If you need to control the outbound IP address of your function app, such as when you need to add it to an allowlist, consider implementing a [virtual network NAT gateway](#virtual-network-nat-gateway-for-outbound-static-ip) while running in a Premium hosting plan. You can also do this by running in a Dedicated (App Service) plan.

### Dedicated plans

When a function app runs on Dedicated (App Service) plans, the set of available outbound IP addresses for a function app might change when you:

- Take any action that can change the inbound IP address.
- Change your Dedicated (App Service) plan pricing tier. The list of all possible outbound IP addresses your app can use, for all pricing tiers, is in the
`possibleOutboundIPAddresses`

property. See[Find outbound IPs](#find-outbound-ip-addresses).

#### Forcing an outbound IP address change

Use the following procedure to deliberately force an outbound IP address change in a Dedicated (App Service) plan:

Scale your App Service plan up or down between Standard and Premium v2 pricing tiers.

Wait 10 minutes.

Scale back to where you started.


## IP address restrictions

You can configure a list of IP addresses that you want to allow or deny access to a function app. For more information, see [Azure App Service access restrictions](../app-service/app-service-ip-restrictions).

## Dedicated IP addresses

There are several strategies to explore when your function app requires static, dedicated IP addresses.

### Virtual network NAT gateway for outbound static IP

You can control the IP address of outbound traffic from your functions by using a virtual network NAT gateway to direct traffic through a static public IP address. You can use this topology when running in a [Premium plan](functions-premium-plan) or in a [Dedicated hosting plan](dedicated-plan). To learn more, see [Tutorial: Control Azure Functions outbound IP with an Azure virtual network NAT gateway](functions-how-to-use-nat-gateway).

### App Service Environments

For full control over the IP addresses, both inbound and outbound, we recommend [App Service Environments](../app-service/environment/intro) (the [Isolated tier](https://azure.microsoft.com/pricing/details/app-service/) of App Service plans). For more information, see [App Service Environment overview](../app-service/environment/overview).

To find out if your function app runs in an App Service Environment:

- Sign in to the
[Azure portal](https://portal.azure.com). - Navigate to the function app.
- Select the
**Overview**tab. - The App Service plan tier appears under
**App Service plan/pricing tier**. The App Service Environment pricing tier is**Isolated**.

The App Service Environment `sku`

is `Isolated`

.

## Next steps

A common cause of IP changes is function app scale changes. [Learn more about function app scaling](functions-scale).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-triggers-bindings -->

# Azure Functions triggers and bindings

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn the high-level concepts surrounding triggers and bindings for functions.

Triggers cause a function to run. A trigger defines how a function is invoked, and a function must have exactly one trigger. Triggers can also pass data into your function, as you would with method calls.

Binding to a function is a way of declaratively connecting your functions to other resources. Bindings either pass data into your function (an *input binding*) or enable you to write data out from your function (an *output binding*) by using *binding parameters*. Your function trigger is essentially a special type of input binding.

You can mix and match bindings to suit your function's specific scenario. Bindings are optional, and a function might have one or multiple input and/or output bindings.

Triggers and bindings let you avoid hardcoding access to other services. Your function receives data (for example, the content of a queue message) in function parameters. You send data (for example, to create a queue message) by using the return value of the function.

Consider the following examples of how you could implement functions:

| Example scenario | Trigger | Input binding | Output binding |
|---|---|---|---|
| A new queue message arrives, which runs a function to write to another queue. | Queue* |
None |
Queue* |
| A scheduled job reads Azure Blob Storage contents and creates a new Azure Cosmos DB document. | Timer | Blob Storage | Azure Cosmos DB |
| Azure Event Grid is used to read an image from Blob Storage and a document from Azure Cosmos DB to send an email. | Event Grid | Blob Storage and Azure Cosmos DB | SendGrid |

* Represents different queues.

These examples aren't meant to be exhaustive, but they illustrate how you can use triggers and bindings together. For a more comprehensive set of scenarios, see [Azure Functions scenarios](functions-scenarios).

Tip

Azure Functions doesn't require you to use input and output bindings to connect to Azure services. You can always create an Azure SDK client in your code and use it instead for your data transfers. For more information, see [Connect to services](functions-reference#connect-to-services).

## Trigger and binding definitions

The following example shows an HTTP-triggered function with an output binding that writes a message to an Azure Storage queue.

For C# class library functions, you configure triggers and bindings by decorating methods and parameters with C# attributes. The specific attribute that you apply might depend on the C# runtime model:

The HTTP trigger (`HttpTrigger`

) is defined on the `Run`

method for a function named `HttpExample`

that returns a `MultiResponse`

object:

```
[Function("HttpExample")]
public static MultiResponse Run([HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequestData req,
FunctionContext executionContext)
{
```


This example shows the `MultiResponse`

object definition. The object definition returns `HttpResponse`

to the HTTP request and writes a message to a storage queue by using a `QueueOutput`

binding:

```
public class MultiResponse
{
[QueueOutput("outqueue",Connection = "AzureWebJobsStorage")]
public string[] Messages { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
```


For more information, see the [C# guide for isolated worker models](dotnet-isolated-process-guide#methods-recognized-as-functions).

Legacy C# script functions use a `function.json`

definition file. For more information, see the [Azure Functions C# script (.csx) developer reference](functions-reference-csharp).

For Java functions, you configure triggers and bindings by annotating specific methods and parameters. This HTTP trigger (`@HttpTrigger`

) is defined on the `run`

method for a function named `HttpExample`

. The function writes to a storage queue named `outqueue`

that the `@QueueOutput`

annotation defines on the `msg`

parameter:

```
@FunctionName("HttpExample")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@QueueOutput(name = "msg", queueName = "outqueue",
connection = "AzureWebJobsStorage") OutputBinding<String> msg,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
```


For more information, see the [Java developer guide](functions-reference-java#triggers-and-annotations).

The way that you define triggers and bindings for Node.js functions depends on the specific version of Node.js for Azure Functions:

In Node.js for Azure Functions version 4, you configure triggers and bindings by using objects exported from the `@azure/functions`

module. For more information, see the [Node.js developer guide](functions-reference-node?pivots=nodejs-model-v4#inputs-and-outputs).

The `http`

method on the exported `app`

object defines an HTTP trigger. The `storageQueue`

method on `output`

defines an output binding on this trigger.

```
const { app, output } = require('@azure/functions');
const queueOutput = output.storageQueue({
queueName: 'outqueue',
connection: 'MyStorageConnectionAppSetting',
});
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraOutputs: [queueOutput],
handler: async (request, context) => {
const body = await request.text();
context.extraOutputs.set(queueOutput, body);
return { body: 'Created queue item.' };
},
});
```


The `http`

method on the exported `app`

object defines an HTTP trigger. The `storageQueue`

method on `output`

defines an output binding on this trigger.

```
import { app, HttpRequest, HttpResponseInit, InvocationContext, output } from '@azure/functions';
const queueOutput = output.storageQueue({
queueName: 'outqueue',
connection: 'MyStorageConnectionAppSetting',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
const body = await request.text();
context.extraOutputs.set(queueOutput, body);
return { body: 'Created queue item.' };
}
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraOutputs: [queueOutput],
handler: httpTrigger1,
});
```


This example `function.json`

file defines the function:

```
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "Request",
"methods": [
"get",
"post"
]
},
{
"type": "http",
"direction": "out",
"name": "Response"
},
{
"type": "queue",
"direction": "out",
"name": "msg",
"queueName": "outqueue",
"connection": "AzureWebJobsStorage"
}
]
}
```


For more information, see the [PowerShell developer guide](functions-reference-powershell#bindings).

The way that the function is defined depends on the version of Python for Azure Functions:

In Python for Azure Functions version 2, you define the function directly in code by using decorators:

```
app = func.FunctionApp(http_auth_level=func.AuthLevel.ANONYMOUS)
@app.route(route="HttpExample")
@app.queue_output(arg_name="msg", queue_name="outqueue", connection="AzureWebJobsStorage")
def HttpExample(req: func.HttpRequest, msg: func.Out [func.QueueMessage]) -> func.HttpResponse:
logging.info('Python HTTP trigger function processed a request.')
```


## Binding considerations

Not all services support both input and output bindings. See your specific binding extension for

[specific code examples for bindings](#code-examples-for-bindings).Triggers and bindings are defined differently depending on the development language. Make sure to select your language at the

[top](#top)of this article.Trigger and binding names are limited to alphanumeric characters and

`_`

, the underscore.

## Task to add bindings to a function

You can connect your function to other services by using input or output bindings. Add a binding by adding its specific definitions to your function. To learn how, see [Add bindings to an existing function in Azure Functions](add-bindings-existing-function).

Azure Functions supports multiple bindings, which must be configured correctly. For example, a function can read data from a queue (input binding) and write data to a database (output binding) simultaneously.

## Supported bindings

This table shows the bindings that are supported in the major versions of the Azure Functions runtime:

| Type | 4.x1 |
1.x2 |
Trigger | Input | Output |
|---|---|---|---|---|---|
|

[Azure Cosmos DB](functions-bindings-cosmosdb-v2)[Azure Data Explorer](functions-bindings-azure-data-explorer)[Azure SQL](functions-bindings-azure-sql)[Dapr](functions-bindings-dapr)4[Event Grid](functions-bindings-event-grid)[Event Hubs](functions-bindings-event-hubs)[HTTP and webhooks](functions-bindings-http-webhook)[IoT Hub](functions-bindings-event-iot)[Kafka](functions-bindings-kafka)3[Mobile Apps](functions-bindings-mobile-apps)[Model Context Protocol](functions-bindings-mcp)[Notification Hubs](functions-bindings-notification-hubs)[Queue Storage](functions-bindings-storage-queue)[Redis](functions-bindings-cache)[RabbitMQ](functions-bindings-rabbitmq)3[SendGrid](functions-bindings-sendgrid)[Service Bus](functions-bindings-service-bus)[Azure SignalR Service](functions-bindings-signalr-service)[Table Storage](functions-bindings-storage-table)[Timer](functions-bindings-timer)[Twilio](functions-bindings-twilio)- Register all bindings except HTTP and timer. See
[Register Azure Functions binding extensions](functions-bindings-register). This step isn't required when using version 1.x of the Functions runtime. [Support ends for version 1.x of the Azure Functions runtime on September 14, 2026](https://aka.ms/azure-functions-retirements/hostv1).[Migrate your apps to version 4.x](migrate-version-1-version-4)for full support.- Triggers aren't supported in the Consumption plan. This binding type requires
[runtime-driven triggers](functions-networking-options#elastic-premium-plan-with-virtual-network-triggers). - This binding type is supported in Kubernetes, Azure IoT Edge, and other self-hosted modes only.

For information about which bindings are in preview or are approved for production use, see [Supported languages](supported-languages).

Specific versions of binding extensions are supported only while the underlying service SDK is supported. Changes to support in the underlying service SDK version affect the support for the consuming extension.

## SDK types

Azure Functions binding extensions use Azure service SDKs to connect to Azure services. The specific SDK types used by bindings can affect how you work with the data in your functions. Some bindings support SDK-specific types that provide richer functionality and better integration with the service, while others use more generic types like strings or byte arrays. When available, using SDK-specific types can provide benefits such as better type safety, easier data manipulation, and access to service-specific features.

This table indicates binding extensions that currently support SDK types:

| Extension | Types | Support level |
|---|---|---|
|

`BlobClient`

`BlobContainerClient`

`BlockBlobClient`

`PageBlobClient`

`AppendBlobClient`

Input: GA

[Azure Cosmos DB](functions-bindings-cosmosdb-v2?tabs=isolated-process,extensionv4&pivots=programming-language-csharp#binding-types)`CosmosClient`

`Database`

`Container`

[Azure Event Grid](functions-bindings-event-grid?tabs=isolated-process,extensionv3&pivots=programming-language-csharp#binding-types)`CloudEvent`

`EventGridEvent`

[Azure Event Hubs](functions-bindings-event-hubs?tabs=isolated-process,extensionv5&pivots=programming-language-csharp#binding-types)`EventData`

`EventHubProducerClient`

[Azure Queue Storage](functions-bindings-storage-queue?tabs=isolated-process,extensionv5&pivots=programming-language-csharp#binding-types)`QueueClient`

`QueueMessage`

[Azure Service Bus](functions-bindings-service-bus?tabs=isolated-process,extensionv5&pivots=programming-language-csharp#binding-types)`ServiceBusClient`

`ServiceBusReceiver`

`ServiceBusSender`

`ServiceBusMessage`

[Azure Table Storage](functions-bindings-storage-table?tabs=isolated-process,table-api&pivots=programming-language-csharp#binding-types)`TableClient`

`TableEntity`

Considerations for SDK types:

- When using
[binding expressions](functions-bindings-expressions-patterns)that rely on trigger data, SDK types for the trigger itself cannot be used. - For output scenarios where you might use an SDK type, create and work with SDK clients directly instead of using an output binding.
- The Azure Cosmos DB trigger uses the
[Azure Cosmos DB change feed](/en-us/azure/cosmos-db/change-feed)and exposes change feed items as JSON-serializable types. As a result, SDK types aren't supported for this trigger.

For more information, see [SDK types](dotnet-isolated-process-guide#sdk-types) in the C# developer guide.

| Extension | Types | Support level | Samples |
|---|---|---|---|
|

`BlobClient`

`ContainerClient`

`StorageStreamDownloader`

Input: GA

[Quickstart](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-python)`BlobClient`

`ContainerClient`

`StorageStreamDownloader`

[Azure Cosmos DB](functions-bindings-cosmosdb-v2)`CosmosClient`

`DatabaseProxy`

`ContainerProxy`

[Quickstart](https://github.com/Azure-Samples/azure-functions-cosmosdb-sdk-bindings-python)`ContainerProxy`

`CosmosClient`

`DatabaseProxy`

[Azure Event Hubs](functions-bindings-event-hubs)`EventData`

[Quickstart](https://github.com/Azure-Samples/azure-functions-eventhub-sdk-bindings-python)`EventData`

[Azure Service Bus](functions-bindings-service-bus)`ServiceBusReceivedMessage`

[Quickstart](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-servicebus/samples/README.md)`ServiceBusReceivedMessage`

Considerations for SDK types:

- For output scenarios where you might use an SDK type, create and work with SDK clients directly instead of using an output binding.
- The Azure Cosmos DB trigger uses the
[Azure Cosmos DB change feed](/en-us/azure/cosmos-db/change-feed)and exposes change feed items as JSON-serializable types. As a result, SDK types aren't supported for this trigger.

SDK types are supported only when using the Python v2 programming model. For more information, see [SDK type bindings](functions-reference-python#sdk-type-bindings) in the Python developer guide.

| Extension | Types | Support level |
|---|---|---|
|

`BlobClient`

`ContainerClient`

`ReadableStream`

[Azure Service Bus](functions-bindings-service-bus)`ServiceBusClient`

`ServiceBusReceiver`

`ServiceBusSender`

`ServiceBusMessage`

SDK types are supported only when using the Node v4 programming model. For more information, see [SDK types](functions-reference-node#sdk-types) in the Node.js developer guide.

| Extension | Types | Support level |
|---|---|---|
|

`BlobClient`

`BlobContainerClient`

For more information, see [SDK types](functions-reference-java#sdk-types) in the Java developer guide.

Important

SDK types aren't currently supported for PowerShell apps.

## Code examples for bindings

Use the following table to find more examples of specific binding types that show you how to work with bindings in your functions. First, choose the language tab that corresponds to your project.

Binding code for C# depends on the [specific process model](dotnet-isolated-process-guide#benefits-of-the-isolated-worker-model).

| Service | Examples | Samples |
|---|---|---|
| Blob Storage |
|

[Link](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/storage/Microsoft.Azure.WebJobs.Extensions.Storage.Blobs)[Trigger](functions-bindings-cosmosdb-v2-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Input](functions-bindings-cosmosdb-v2-input?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-cosmosdb-v2-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/dev/sample/ExtensionsSample/Samples)[Input](functions-bindings-azure-data-explorer-input?pivots=programming-language-csharp#examples)[Output](functions-bindings-azure-data-explorer-output?pivots=programming-language-csharp#examples)[Link](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-csharp)[Trigger](functions-bindings-azure-sql-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Input](functions-bindings-azure-sql-input?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-azure-sql-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](/en-us/samples/azure-samples/azure-sql-binding-func-dotnet-todo/todo-backend-dotnet-azure-sql-bindings-azure-functions/)[Trigger](functions-bindings-event-grid-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-event-grid-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/dev/sample/ExtensionsSample/Samples)[Trigger](functions-bindings-event-hubs-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-event-hubs-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Trigger](functions-bindings-event-iot-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-event-iot-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Trigger](functions-bindings-http-webhook-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd)[Trigger](functions-bindings-storage-queue-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-storage-queue-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/storage/Microsoft.Azure.WebJobs.Extensions.Storage.Queues/samples/functionapp)[Trigger](functions-bindings-rabbitmq-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-rabbitmq-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-sendgrid?tabs=isolated-process&pivots=programming-language-csharp#example)[Trigger](functions-bindings-service-bus-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-service-bus-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/servicebus/Microsoft.Azure.WebJobs.Extensions.ServiceBus)[Trigger](functions-bindings-signalr-service-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Input](functions-bindings-signalr-service-input?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-signalr-service-output?tabs=isolated-process&pivots=programming-language-csharp)[Input](functions-bindings-storage-table-input?tabs=isolated-process&pivots=programming-language-csharp)[Output](functions-bindings-storage-table-output?tabs=isolated-process&pivots=programming-language-csharp)[Trigger](functions-bindings-timer?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/dev/sample/ExtensionsSample/Samples)[Output](functions-bindings-twilio?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/dev/sample/ExtensionsSample/Samples)| Service | Examples | Samples |
|---|---|---|
| Blob Storage |
|

[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Trigger](functions-bindings-cosmosdb-v2-trigger?pivots=programming-language-java#example)[Input](functions-bindings-cosmosdb-v2-input?pivots=programming-language-java#example)[Output](functions-bindings-cosmosdb-v2-output?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/java-functions-eventhub-cosmosdb)[Input](functions-bindings-azure-data-explorer-input?pivots=programming-language-java#examples)[Output](functions-bindings-azure-data-explorer-output?pivots=programming-language-java#examples)[Link](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-java)[Trigger](functions-bindings-azure-sql-trigger?pivots=programming-language-java#example)[Input](functions-bindings-azure-sql-input?pivots=programming-language-java#example)[Output](functions-bindings-azure-sql-output?pivots=programming-language-java#example)[Trigger](functions-bindings-event-grid-trigger?pivots=programming-language-java#example)[Output](functions-bindings-event-grid-output?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Trigger](functions-bindings-event-hubs-trigger?pivots=programming-language-java#example)[Output](functions-bindings-event-hubs-output?pivots=programming-language-java#example)[Trigger](functions-bindings-event-iot-trigger?pivots=programming-language-java#example)[Output](functions-bindings-event-iot-output?pivots=programming-language-java#example)[Trigger](functions-bindings-http-webhook-trigger?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Trigger](functions-bindings-storage-queue-trigger?pivots=programming-language-java#example)[Output](functions-bindings-storage-queue-output?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Trigger](functions-bindings-rabbitmq-trigger?pivots=programming-language-java#example)[Output](functions-bindings-rabbitmq-output?pivots=programming-language-java#example)[Output](functions-bindings-sendgrid?pivots=programming-language-java#example)[Trigger](functions-bindings-service-bus-trigger?pivots=programming-language-java#example)[Output](functions-bindings-service-bus-output?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Trigger](functions-bindings-signalr-service-trigger?pivots=programming-language-java#example)[Input](functions-bindings-signalr-service-input?pivots=programming-language-java#example)[Output](functions-bindings-signalr-service-output?pivots=programming-language-java)[Input](functions-bindings-storage-table-input?pivots=programming-language-java)[Output](functions-bindings-storage-table-output?pivots=programming-language-java)[Trigger](functions-bindings-timer?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Output](functions-bindings-twilio?pivots=programming-language-java#example)| Service | Examples | Samples |
|---|---|---|
| Blob Storage |
|

[Link](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-nodejs)[Trigger](functions-bindings-cosmosdb-v2-trigger?pivots=programming-language-javascript#example)[Input](functions-bindings-cosmosdb-v2-input?pivots=programming-language-javascript#example)[Output](functions-bindings-cosmosdb-v2-output?pivots=programming-language-javascript#example)[Link](https://github.com/Azure-Samples/functions-docs-javascript/tree/master/functions-add-output-binding-cosmosdb-cli-v4-programming-model)[Input](functions-bindings-azure-data-explorer-input?pivots=programming-language-javascript#examples)[Output](functions-bindings-azure-data-explorer-output?pivots=programming-language-javascript#examples)[Trigger](functions-bindings-azure-sql-trigger?pivots=programming-language-javascript#example)[Input](functions-bindings-azure-sql-input?pivots=programming-language-javascript#example)[Output](functions-bindings-azure-sql-output?pivots=programming-language-javascript#example)[Link](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-node)[Trigger](functions-bindings-event-grid-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-event-grid-output?pivots=programming-language-javascript#example)[Trigger](functions-bindings-event-hubs-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-event-hubs-output?pivots=programming-language-javascript#example)[Trigger](functions-bindings-event-iot-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-event-iot-output?pivots=programming-language-javascript#example)[Trigger](functions-bindings-http-webhook-trigger?pivots=programming-language-javascript#example)[Link](https://github.com/Azure-Samples/functions-docs-javascript/tree/master/functions-typescript)[Trigger](functions-bindings-storage-queue-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-storage-queue-output?pivots=programming-language-javascript#example)[Link](https://github.com/Azure-Samples/functions-docs-javascript/tree/master/functions-add-output-binding-storage-queue-cli-v4-programming-model)[Trigger](functions-bindings-rabbitmq-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-rabbitmq-output?pivots=programming-language-javascript#example)[Output](functions-bindings-sendgrid?pivots=programming-language-javascript#example)[Trigger](functions-bindings-service-bus-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-service-bus-output?pivots=programming-language-javascript#example)[Link](https://github.com/Azure-Samples/azure-functions-servicebus-sdk-bindings-nodejs/tree/main/serviceBusSampleWithComplete)[Trigger](functions-bindings-signalr-service-trigger?pivots=programming-language-javascript#example)[Input](functions-bindings-signalr-service-input?pivots=programming-language-javascript#example)[Output](functions-bindings-signalr-service-output?pivots=programming-language-javascript)[Input](functions-bindings-storage-table-input?pivots=programming-language-javascript)[Output](functions-bindings-storage-table-output?pivots=programming-language-javascript)[Trigger](functions-bindings-timer?pivots=programming-language-javascript#example)[Output](functions-bindings-twilio?pivots=programming-language-javascript#example)| Service | Examples | Samples |
|---|---|---|
| Blob Storage |
|

[Trigger](functions-bindings-cosmosdb-v2-trigger?pivots=programming-language-powershell#example)[Input](functions-bindings-cosmosdb-v2-input?pivots=programming-language-powershell#example)[Output](functions-bindings-cosmosdb-v2-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-azure-sql-trigger?pivots=programming-language-powershell#example)[Input](functions-bindings-azure-sql-input?pivots=programming-language-powershell#example)[Output](functions-bindings-azure-sql-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-event-grid-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-event-grid-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-event-hubs-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-event-hubs-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-event-iot-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-event-iot-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-http-webhook-trigger?pivots=programming-language-powershell#example)[Link](https://github.com/Azure-Samples/functions-quickstart-powershell-azd)[Trigger](functions-bindings-storage-queue-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-storage-queue-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-rabbitmq-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-rabbitmq-output?pivots=programming-language-powershell#example)[Output](functions-bindings-sendgrid?pivots=programming-language-powershell#example)[Trigger](functions-bindings-service-bus-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-service-bus-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-signalr-service-trigger?pivots=programming-language-powershell#example)[Input](functions-bindings-signalr-service-input?pivots=programming-language-powershell#example)[Output](functions-bindings-signalr-service-output?pivots=programming-language-powershell)[Input](functions-bindings-storage-table-input?pivots=programming-language-powershell)[Output](functions-bindings-storage-table-output?pivots=programming-language-powershell)[Trigger](functions-bindings-timer?pivots=programming-language-powershell#example)[Output](functions-bindings-twilio?pivots=programming-language-powershell#example)Binding code for Python depends on the Python model version.

| Service | Examples | Samples |
|---|---|---|
| Blob Storage |
|

[Link](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-python)[Trigger](functions-bindings-cosmosdb-v2-trigger?tabs=python-v2&pivots=programming-language-python#example)[Input](functions-bindings-cosmosdb-v2-input?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-cosmosdb-v2-output?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure-Samples/functions-quickstart-python-azd-cosmosdb)[Input](functions-bindings-azure-data-explorer-input?pivots=programming-language-python#examples)[Output](functions-bindings-azure-data-explorer-output?pivots=programming-language-python#examples)[Trigger](functions-bindings-azure-sql-trigger?tabs=python-v2&pivots=programming-language-python#example)[Input](functions-bindings-azure-sql-input?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-azure-sql-output?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-python)[Trigger](functions-bindings-event-grid-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-event-grid-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-event-hubs-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-event-hubs-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-event-iot-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-event-iot-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-http-webhook-trigger?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure-Samples/functions-quickstart-python-http-azd)[Trigger](functions-bindings-storage-queue-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-storage-queue-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-rabbitmq-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-rabbitmq-output?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-sendgrid?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-service-bus-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-service-bus-output?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure-Samples/functions-quickstart-python-azd-service-bus)[Trigger](functions-bindings-signalr-service-trigger?tabs=python-v2&pivots=programming-language-python#example)[Input](functions-bindings-signalr-service-input?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-signalr-service-output?tabs=python-v2&pivots=programming-language-python)[Input](functions-bindings-storage-table-input?tabs=python-v2&pivots=programming-language-python)[Output](functions-bindings-storage-table-output?tabs=python-v2&pivots=programming-language-python)[Trigger](functions-bindings-timer?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-twilio?tabs=python-v2&pivots=programming-language-python#example)## Custom bindings

You can create custom input and output bindings. Bindings must be authored in .NET, but they can be consumed from any supported language. For more information about creating custom bindings, see [Creating custom input and output bindings](https://github.com/Azure/azure-webjobs-sdk/wiki/Creating-custom-input-and-output-bindings).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-service-bus-trigger -->

# Azure Service Bus trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the Service Bus trigger to respond to messages from a Service Bus queue or topic. Starting with extension version 3.1.0, you can trigger on a session-enabled queue or topic.

For information on setup and configuration details, see the [overview](functions-bindings-service-bus).

Service Bus scaling decisions for the Consumption and Premium plans are made based on target-based scaling. For more information, see [Target-based scaling](functions-target-based-scaling).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

## Example

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

This code defines and initializes the `ILogger`

:

```
private readonly ILogger<ServiceBusReceivedMessageFunctions> _logger;
public ServiceBusReceivedMessageFunctions(ILogger<ServiceBusReceivedMessageFunctions> logger)
{
_logger = logger;
}
```


This example shows a [C# function](dotnet-isolated-process-guide) that receives a single Service Bus queue message and writes it to the logs:

```
[Function(nameof(ServiceBusReceivedMessageFunction))]
[ServiceBusOutput("outputQueue", Connection = "ServiceBusConnection")]
public string ServiceBusReceivedMessageFunction(
[ServiceBusTrigger("queue", Connection = "ServiceBusConnection")] ServiceBusReceivedMessage message)
{
_logger.LogInformation("Message ID: {id}", message.MessageId);
_logger.LogInformation("Message Body: {body}", message.Body);
_logger.LogInformation("Message Content-Type: {contentType}", message.ContentType);
var outputMessage = $"Output message created at {DateTime.Now}";
return outputMessage;
}
```


This example shows a [C# function](dotnet-isolated-process-guide) that receives multiple Service Bus queue messages in a single batch and writes each to the logs:

```
[Function(nameof(ServiceBusReceivedMessageBatchFunction))]
public void ServiceBusReceivedMessageBatchFunction(
[ServiceBusTrigger("queue", Connection = "ServiceBusConnection", IsBatched = true)] ServiceBusReceivedMessage[] messages)
{
foreach (ServiceBusReceivedMessage message in messages)
{
_logger.LogInformation("Message ID: {id}", message.MessageId);
_logger.LogInformation("Message Body: {body}", message.Body);
_logger.LogInformation("Message Content-Type: {contentType}", message.ContentType);
}
}
```


This example shows a [C# function](dotnet-isolated-process-guide) that receives multiple Service Bus queue messages, writes it to the logs, and then settles the message as completed:

```
[Function(nameof(ServiceBusMessageActionsFunction))]
public async Task ServiceBusMessageActionsFunction(
[ServiceBusTrigger("queue", Connection = "ServiceBusConnection", AutoCompleteMessages = false)]
ServiceBusReceivedMessage message,
ServiceBusMessageActions messageActions)
{
_logger.LogInformation("Message ID: {id}", message.MessageId);
_logger.LogInformation("Message Body: {body}", message.Body);
_logger.LogInformation("Message Content-Type: {contentType}", message.ContentType);
// Complete the message
await messageActions.CompleteMessageAsync(message);
}
```


The following Java function uses the `@ServiceBusQueueTrigger`

annotation from the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime) to describe the configuration for a Service Bus queue trigger. The function grabs the message placed on the queue and adds it to the logs.

```
@FunctionName("sbprocessor")
public void serviceBusProcess(
@ServiceBusQueueTrigger(name = "msg",
queueName = "myqueuename",
connection = "myconnvarname") String message,
final ExecutionContext context
) {
context.getLogger().info(message);
}
```


Java functions can also be triggered when a message is added to a Service Bus topic. The following example uses the `@ServiceBusTopicTrigger`

annotation to describe the trigger configuration.

```
@FunctionName("sbtopicprocessor")
public void run(
@ServiceBusTopicTrigger(
name = "message",
topicName = "mytopicname",
subscriptionName = "mysubscription",
connection = "ServiceBusConnection"
) String message,
final ExecutionContext context
) {
context.getLogger().info(message);
}
```


This example uses the SDK type [ ServiceBusReceivedMessage](/en-us/javascript/api/@azure/service-bus/servicebusreceivedmessage) obtained from

`ServiceBusMessageContext`

provided by the Service Bus trigger:```
import '@azure/functions-extensions-servicebus'; // Ensure the Service Bus extension is imported
import { app, InvocationContext } from '@azure/functions';
import { ServiceBusMessageContext } from '@azure/functions-extensions-servicebus';
//This a SDKbinding = true
export async function serviceBusQueueTrigger(
serviceBusMessageContext: ServiceBusMessageContext,
context: InvocationContext
): Promise<void> {
const message = serviceBusMessageContext.messages[0];
context.log(message);
// Get current retry count from custom properties, default to 0
const currentRetryCount = message.applicationProperties?.retryCnt ? parseInt(message.applicationProperties.retryCnt as string) : 0;
context.log(`Current retry count: ${currentRetryCount}`);
if (currentRetryCount >= 3) {
// After 3 retries, complete the message to remove it from the queue
context.log(`Maximum retry count (3) reached. Completing message to prevent infinite loop.`);
await serviceBusMessageContext.actions.complete(message);
context.log('Message completed after maximum retries');
} else {
// Abandon with updated retry count
const newRetryCount = currentRetryCount + 1;
const propertiesToModify = {
retryCnt: newRetryCount.toString(),
lastRetryTime: new Date().toISOString(),
errorMessage: "Processing failed"
};
context.log(`Abandoning message with retry count: ${newRetryCount}`);
await serviceBusMessageContext.actions.abandon(message, propertiesToModify);
}
context.log('triggerMetadata: ', context.triggerMetadata);
context.log('Message body:', message.body);
}
app.serviceBusQueue('serviceBusQueueTrigger1', {
connection: 'ServiceBusConnection',
queueName: 'testqueue',
sdkBinding: true,
autoCompleteMessages: false,
cardinality: 'many',
handler: serviceBusQueueTrigger,
});
```


For another example using SDK types see the [exponential backoff strategy sample](https://github.com/Azure/azure-functions-nodejs-extensions/blob/main/azure-functions-nodejs-extensions-servicebus/samples/serviceBusTriggerExponentialBackOff/src/functions/serviceBusTopicTrigger.ts).

For more information, see [SDK types](functions-reference-node#sdk-types) in the Node.js reference article.

The following example shows a Service Bus trigger [TypeScript function](functions-reference-node?tabs=typescript). The function reads [message metadata](#message-metadata) and logs a Service Bus queue message.

```
import { app, InvocationContext } from '@azure/functions';
export async function serviceBusQueueTrigger1(message: unknown, context: InvocationContext): Promise<void> {
context.log('Service bus queue function processed message:', message);
context.log('EnqueuedTimeUtc =', context.triggerMetadata.enqueuedTimeUtc);
context.log('DeliveryCount =', context.triggerMetadata.deliveryCount);
context.log('MessageId =', context.triggerMetadata.messageId);
}
app.serviceBusQueue('serviceBusQueueTrigger1', {
connection: 'MyServiceBusConnection',
queueName: 'testqueue',
handler: serviceBusQueueTrigger1,
});
```


The following example shows a Service Bus trigger [JavaScript function](functions-reference-node). The function reads [message metadata](#message-metadata) and logs a Service Bus queue message.

```
const { app } = require('@azure/functions');
app.serviceBusQueue('serviceBusQueueTrigger1', {
connection: 'MyServiceBusConnection',
queueName: 'testqueue',
handler: (message, context) => {
context.log('Service bus queue function processed message:', message);
context.log('EnqueuedTimeUtc =', context.triggerMetadata.enqueuedTimeUtc);
context.log('DeliveryCount =', context.triggerMetadata.deliveryCount);
context.log('MessageId =', context.triggerMetadata.messageId);
},
});
```


The following example shows a Service Bus trigger binding in a *function.json* file and a [PowerShell function](functions-reference-powershell) that uses the binding.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"name": "mySbMsg",
"type": "serviceBusTrigger",
"direction": "in",
"topicName": "mytopic",
"subscriptionName": "mysubscription",
"connection": "AzureServiceBusConnectionString"
}
]
}
```


Here's the function that runs when a Service Bus message is sent.

```
param([string] $mySbMsg, $TriggerMetadata)
Write-Host "PowerShell ServiceBus queue trigger function processed message: $mySbMsg"
```


This example uses SDK types to directly access the underlying [ ServiceBusReceivedMessage](/en-us/python/api/azure-servicebus/azure.servicebus.servicebusreceivedmessage) object provided by the Service Bus trigger:

```
import logging
import azure.functions as func
import azurefunctions.extensions.bindings.servicebus as servicebus
app = func.FunctionApp(http_auth_level=func.AuthLevel.FUNCTION)
@app.service_bus_queue_trigger(arg_name="receivedmessage",
queue_name="QUEUE_NAME",
connection="SERVICEBUS_CONNECTION")
def servicebus_queue_trigger(receivedmessage: servicebus.ServiceBusReceivedMessage):
logging.info("Python ServiceBus queue trigger processed message.")
logging.info("Receiving: %s\n"
"Body: %s\n"
"Enqueued time: %s\n"
"Lock Token: %s\n"
"Message ID: %s\n"
"Sequence number: %s\n",
receivedmessage,
receivedmessage.body,
receivedmessage.enqueued_time_utc,
receivedmessage.lock_token,
receivedmessage.message_id,
receivedmessage.sequence_number)
```


The function reads various properties of the `ServiceBusReceivedMessage`

type and logs them.

For more examples using Service Bus SDK types, see the [ ServiceBusReceivedMessage](https://github.com/Azure/azure-functions-python-extensions/tree/dev/azurefunctions-extensions-bindings-servicebus/samples/servicebus_samples_single) samples. For a step-by-step tutorial on how to include SDK-type bindings in your function app, follow the

[Python SDK Bindings for Service Bus Sample](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-servicebus/samples/README.md).

Note

Known limitations include:

- The
`message`

property is not supported. - Batch message support requires version 4.1039 or later of the Functions runtime.

To learn more, including what other SDK type bindings are supported, see [SDK type bindings](functions-reference-python#sdk-type-bindings).

This example demonstrates how to read a Service Bus queue message via a trigger. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="ServiceBusQueueTrigger1")
@app.service_bus_queue_trigger(arg_name="msg",
queue_name="<QUEUE_NAME>",
connection="<CONNECTION_SETTING>")
def test_function(msg: func.ServiceBusMessage):
logging.info('Python ServiceBus queue trigger processed message: %s',
msg.get_body().decode('utf-8'))
```


The following example demonstrates how to read a Service Bus queue topic via a trigger.

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="ServiceBusTopicTrigger1")
@app.service_bus_topic_trigger(arg_name="message",
topic_name="TOPIC_NAME",
connection="CONNECTION_SETTING",
subscription_name="SUBSCRIPTION_NAME")
def test_function(message: func.ServiceBusMessage):
message_body = message.get_body().decode("utf-8")
logging.info("Python ServiceBus topic trigger processed message.")
logging.info("Message Body: " + message_body)
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the [ServiceBusTriggerAttribute](https://github.com/Azure/azure-functions-servicebus-extension/blob/master/src/Microsoft.Azure.WebJobs.Extensions.ServiceBus/ServiceBusTriggerAttribute.cs) attribute to define the function trigger. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#service-bus-trigger).

The following table explains the properties you can set using this trigger attribute:

| Property | Description |
|---|---|
QueueName |
Name of the queue to monitor. Set only if monitoring a queue, not for a topic. |
TopicName |
Name of the topic to monitor. Set only if monitoring a topic, not for a queue. |
SubscriptionName |
Name of the subscription to monitor. Set only if monitoring a topic, not for a queue. |
Connection |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

**IsBatched****IsSessionsEnabled**`true`

if connecting to a [session-aware](../service-bus-messaging/message-sessions)queue or subscription.`false`

otherwise, which is the default value.**AutoCompleteMessages**`true`

if the trigger should automatically complete the message after a successful invocation. `false`

if it should not, such as when you are [handling message settlement in code](#usage). If not explicitly set, the behavior is based on the[.](functions-bindings-service-bus#hostjson-settings)`autoCompleteMessages`

configuration in `host.json`

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, the following properties on the `service_bus_queue_trigger`

:

| Property | Description |
|---|---|
`arg_name` |
The name of the variable that represents the queue or topic message in function code. |
`queue_name` |
Name of the queue to monitor. Set only if monitoring a queue, not for a topic. |
`connection` |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

The `ServiceBusQueueTrigger`

annotation allows you to create a function that runs when a Service Bus queue message is created. Configuration options available include the following properties:

| Property | Description |
|---|---|
name |
The name of the variable that represents the queue or topic message in function code. |
queueName |
Name of the queue to monitor. Set only if monitoring a queue, not for a topic. |
topicName |
Name of the topic to monitor. Set only if monitoring a topic, not for a queue. |
subscriptionName |
Name of the subscription to monitor. Set only if monitoring a topic, not for a queue. |
connection |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

The `ServiceBusTopicTrigger`

annotation allows you to designate a topic and subscription to target what data triggers the function.

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

See the trigger [example](#example) for more detail.

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `app.serviceBusQueue()`

or `app.serviceBusTopic()`

methods.

| Property | Description |
|---|---|
queueName |
Name of the queue to monitor. Set only if monitoring a queue, not for a topic. |
topicName |
Name of the topic to monitor. Set only if monitoring a topic, not for a queue. |
subscriptionName |
Name of the subscription to monitor. Set only if monitoring a topic, not for a queue. |
connection |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

**accessRights**`manage`

and `listen`

. The default is `manage`

, which indicates that the `connection`

has the **Manage**permission. If you use a connection string that does not have the**Manage**permission, set`accessRights`

to "listen". Otherwise, the Functions runtime might fail trying to do operations that require manage rights. In Azure Functions version 2.x and higher, this property is not available because the latest version of the Service Bus SDK doesn't support manage operations.**isSessionsEnabled**`true`

if connecting to a [session-aware](../service-bus-messaging/message-sessions)queue or subscription.`false`

otherwise, which is the default value.**autoComplete**`true`

for non-C# functions, which means that the trigger should either automatically call complete after processing, or the function code manually calls complete.When set to

`true`

, the trigger completes the message automatically if the function execution completes successfully, and abandons the message otherwise.Exceptions in the function results in the runtime call

`abandonAsync`

in the background. If no exception occurs, then `completeAsync`

is called in the background. This property is available only in Azure Functions 2.x and higher.When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `serviceBusTrigger` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to "in". This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that represents the queue or topic message in function code. |
queueName |
Name of the queue to monitor. Set only if monitoring a queue, not for a topic. |
topicName |
Name of the topic to monitor. Set only if monitoring a topic, not for a queue. |
subscriptionName |
Name of the subscription to monitor. Set only if monitoring a topic, not for a queue. |
connection |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

**accessRights**`manage`

and `listen`

. The default is `manage`

, which indicates that the `connection`

has the **Manage**permission. If you use a connection string that does not have the**Manage**permission, set`accessRights`

to "listen". Otherwise, the Functions runtime might fail trying to do operations that require manage rights. In Azure Functions version 2.x and higher, this property is not available because the latest version of the Service Bus SDK doesn't support manage operations.**isSessionsEnabled**`true`

if connecting to a [session-aware](../service-bus-messaging/message-sessions)queue or subscription.`false`

otherwise, which is the default value.**autoComplete**`true`

for non-C# functions, which means that the trigger should either automatically call complete after processing, or the function code manually calls complete.When set to

`true`

, the trigger completes the message automatically if the function execution completes successfully, and abandons the message otherwise.Exceptions in the function results in the runtime call

`abandonAsync`

in the background. If no exception occurs, then `completeAsync`

is called in the background. This property is available only in Azure Functions 2.x and higher.When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

See the [Example section](#example) for complete examples.

## Usage

The following parameter types are supported by all C# modalities and extension versions:

| Type | Description |
|---|---|
|
Use when the message is simple text. |
byte[] |
Use for binary data messages. |
Object |
When a message contains JSON, Functions tries to deserialize the JSON data into known plain-old CLR object type. |

Messaging-specific parameter types contain additional message metadata. The specific types supported by the Service Bus trigger depend on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to process a single message, the Service Bus trigger can bind to the following types:

| Type | Description |
|---|---|
`string` |
The message as a string. Use when the message is simple text. |
`byte[]` |
The bytes of the message. |
| JSON serializable types | When an event contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

When binding to

`ServiceBusReceivedMessage`

, you can optionally also include a parameter of type [ServiceBusMessageActions](https://github.com/Azure/azure-functions-dotnet-worker/blob/main/extensions/Worker.Extensions.ServiceBus/src/ServiceBusMessageActions.cs)1,2to perform[message settlement](../service-bus-messaging/message-transfers-locks-settlement#peeklock)actions.When you want the function to process a batch of messages, the Service Bus trigger can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single message types |
An array of events from the batch. Each entry represents one event. When binding to `ServiceBusReceivedMessage[]` , you can optionally also include a parameter of type
1,2 to perform
|

1 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.ServiceBus 5.14.1 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.ServiceBus/5.14.1) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

2 When using `ServiceBusMessageActions`

, set the [ AutoCompleteMessages property of the trigger attribute](functions-bindings-service-bus-trigger#attributes) to

`false`

. This prevents the runtime from attempting to complete messages after a successful function invocation.When the `Connection`

property isn't defined, Functions looks for an app setting named `AzureWebJobsServiceBus`

, which is the default name for the Service Bus connection string. You can also set the `Connection`

property to specify the name of an application setting that contains the Service Bus connection string to use.

The incoming Service Bus message is available via a `ServiceBusQueueMessage`

or `ServiceBusTopicMessage`

parameter.

The Service Bus instance is available via the parameter configured in the *function.json* file's name property.

The queue message is available to the function via a parameter typed as `func.ServiceBusMessage`

. The Service Bus message is passed into the function as either a string or JSON object.

Functions also support Python SDK type bindings for Azure Service Bus, which lets you work with data using these underlying SDK types:

Important

Support for Service Bus SDK types support in Python is in Preview and is only supported for the Python v2 programming model. For more information, see [SDK types in Python](functions-reference-python#sdk-type-bindings).

For a complete example, see [the examples section](#example).

## Connections

The `connection`

property is a reference to environment configuration which specifies how the app should connect to Service Bus. It may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections).

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

To obtain a connection string, follow the steps shown at [Get the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues#get-the-connection-string). The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.

This connection string should be stored in an application setting with a name matching the value specified by the `connection`

property of the binding configuration.

If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name. For example, if you set `connection`

to "MyServiceBus", the Functions runtime looks for an app setting that is named "AzureWebJobsMyServiceBus". If you leave `connection`

empty, the Functions runtime uses the default Service Bus connection string in the app setting that is named "AzureWebJobsServiceBus".

### Identity-based connections

If you are using [version 5.x or higher of the extension](functions-bindings-service-bus?extensionv5), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). To do this, you would define settings under a common prefix which maps to the `connection`

property in the trigger and binding configuration.

In this mode, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Fully Qualified Namespace | `<CONNECTION_NAME_PREFIX>__fullyQualifiedNamespace` |
The fully qualified Service Bus namespace. | <service_bus_namespace>.servicebus.windows.net |

Additional properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

Note

When using [Azure App Configuration](../azure-app-configuration/quickstart-azure-functions-csharp) or [Key Vault](/en-us/azure/key-vault/general/overview) to provide settings for Managed Identity connections, setting names should use a valid key separator such as `:`

or `/`

in place of the `__`

to ensure names are resolved correctly.

For example, `<CONNECTION_NAME_PREFIX>:fullyQualifiedNamespace`

.

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

You'll need to create a role assignment that provides access to your topics and queues at runtime. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) aren't sufficient. The following table shows built-in roles that are recommended when using the Service Bus extension in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles |
|---|---|
Trigger1 |
|

[Azure Service Bus Data Sender](../role-based-access-control/built-in-roles#azure-service-bus-data-sender)1 For triggering from Service Bus topics, the role assignment needs to have effective scope over the Service Bus subscription resource. If only the topic is included, an error will occur. Some clients, such as the Azure portal, don't expose the Service Bus subscription resource as a scope for role assignment. In such cases, the Azure CLI may be used instead. To learn more, see [Azure built-in roles for Azure Service Bus](../service-bus-messaging/service-bus-managed-service-identity#resource-scope).

## Poison messages

Poison message handling can't be controlled or configured in Azure Functions. Service Bus handles poison messages itself.

## PeekLock behavior

The Functions runtime receives a message in [PeekLock mode](../service-bus-messaging/service-bus-performance-improvements#receive-mode).

By default, the runtime calls `Complete`

on the message if the function finishes successfully, or calls `Abandon`

if the function fails. You can disable automatic completion through with the [ autoCompleteMessages property in host.json](functions-bindings-service-bus#hostjson-settings).


By default, the runtime calls `Complete`

on the message if the function finishes successfully, or calls `Abandon`

if the function fails. You can disable automatic completion through with the [ autoCompleteMessages property in host.json](functions-bindings-service-bus#hostjson-settings) or through a


[property on the trigger attribute](#attributes). You should disable automatic completion if your function code handles message settlement.

If the function runs longer than the `PeekLock`

timeout, the lock is automatically renewed as long as the function is running. The `maxAutoRenewDuration`

is configurable in *host.json*, which maps to [ServiceBusProcessor.MaxAutoLockRenewalDuration](/en-us/dotnet/api/azure.messaging.servicebus.servicebusprocessor.maxautolockrenewalduration). The default value of this setting is 5 minutes.

## Message metadata

Messaging-specific types let you easily retrieve [metadata as properties of the object](functions-bindings-expressions-patterns#trigger-metadata). These properties depend on the Functions runtime version, the extension package version, and the C# modality used.

These properties are members of the [ServiceBusReceivedMessage](/en-us/dotnet/api/azure.messaging.servicebus.servicebusreceivedmessage) class.

| Property | Type | Description |
|---|---|---|
`ApplicationProperties` |
`ApplicationProperties` |
Properties set by the sender. |
`ContentType` |
`string` |
A content type identifier utilized by the sender and receiver for application-specific logic. |
`CorrelationId` |
`string` |
The correlation ID. |
`DeliveryCount` |
`Int32` |
The number of deliveries. |
`EnqueuedTime` |
`DateTime` |
The enqueued time in UTC. |
`ScheduledEnqueueTimeUtc` |
`DateTime` |
The scheduled enqueued time in UTC. |
`ExpiresAt` |
`DateTime` |
The expiration time in UTC. |
`MessageId` |
`string` |
A user-defined value that Service Bus can use to identify duplicate messages, if enabled. |
`ReplyTo` |
`string` |
The reply to queue address. |
`Subject` |
`string` |
The application-specific label which can be used in place of the `Label` metadata property. |
`To` |
`string` |
The send to address. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/create-first-function-azure-developer-cli -->

# Quickstart: Build a scalable web API using Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you use Azure Developer command-line tools to build a scalable web API with function endpoints that respond to HTTP requests. After testing the code locally, you deploy it to a new serverless function app you create running in a Flex Consumption plan in Azure Functions.

The project source uses the Azure Developer CLI (azd) to simplify deploying your code to Azure. This deployment follows current best practices for secure and scalable Azure Functions deployments.

By default, the Flex Consumption plan follows a *pay-for-what-you-use* billing model, which means completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

[Java 17 Developer Kit](/en-us/azure/developer/java/fundamentals/java-support-on-azure)- If you use another
[supported version of Java](supported-languages?pivots=programming-language-java#languages-by-runtime-version), you must update the project's pom.xml file. - The
`JAVA_HOME`

environment variable must be set to the install location of the correct version of the Java Development Kit (JDK).

- If you use another
[Apache Maven 3.8.x](https://maven.apache.org)

- A
[secure HTTP test tool](functions-develop-local#http-test-tools)for sending requests with JSON payloads to your function endpoints. This article uses`curl`

.

## Initialize the project

Use the `azd init`

command to create a local Azure Functions code project from a template.

In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-dotnet-azd -e httpendpoint-dotnet`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also used in the name of the resource group you create in Azure.Run this command to navigate to the

`http`

app folder:`cd http`

Create a file named

*local.settings.json*in the`http`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "dotnet-isolated" } }`

This file is required when running locally.


In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template azure-functions-java-flex-consumption-azd -e httpendpoint-java`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/azure-functions-java-flex-consumption-azd)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also used in the name of the resource group you create in Azure.Run this command to navigate to the

`http`

app folder:`cd http`

Create a file named

*local.settings.json*in the`http`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "java" } }`

This file is required when running locally.


In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-javascript-azd -e httpendpoint-js`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-javascript-azd)and initializes the project in the root folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also used in the name of the resource group you create in Azure.Create a file named

*local.settings.json*in the root folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "node" } }`

This file is required when running locally.


In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-powershell-azd -e httpendpoint-ps`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-powershell-azd)and initializes the project in the root folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also used in the name of the resource group you create in Azure.Run this command to navigate to the

`src`

app folder:`cd src`

Create a file named

*local.settings.json*in the`src`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "powershell", "FUNCTIONS_WORKER_RUNTIME_VERSION": "7.2" } }`

This file is required when running locally.


In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-typescript-azd -e httpendpoint-ts`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-typescript-azd)and initializes the project in the root folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name is also used in the name of the resource group you create in Azure.Create a file named

*local.settings.json*in the root folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "node" } }`

This file is required when running locally.


In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-python-http-azd -e httpendpoint-py`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-python-http-azd)and initializes the project in the root folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name is also used in the name of the resource group you create in Azure.Create a file named

*local.settings.json*in the root folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "python" } }`

This file is required when running locally.


## Create and activate a virtual environment

In the root folder, run these commands to create and activate a virtual environment named `.venv`

:

```
python3 -m venv .venv
source .venv/bin/activate
```


If Python doesn't install the venv package on your Linux distribution, run the following command:

```
sudo apt-get install python3-venv
```


## Run in your local environment

Run this command from your app folder in a terminal or command prompt:

`func start`

`mvn clean package mvn azure-functions:run`

`npm install func start`

`npm install npm start`

When the Functions host starts in your local project folder, it writes the URL endpoints of your HTTP triggered functions to the terminal output.

Note

Because access key authorization isn't enforced when running locally, the function URL returned doesn't include the access key value and you don't need it to call your function.

In your browser, go to the

`httpget`

endpoint, which should look like this URL:From a new terminal or command prompt window, run this

`curl`

command to send a POST request with a JSON payload to the`httppost`

endpoint:`curl -i http://localhost:7071/api/httppost -H "Content-Type: text/json" -d @testdata.json`

`curl -i http://localhost:7071/api/httppost -H "Content-Type: text/json" -d "@src/functions/testdata.json"`

This command reads JSON payload data from the

`testdata.json`

project file. You can find examples of both HTTP requests in the`test.http`

project file.When you're done, press Ctrl+C in the terminal window to stop the

`func.exe`

host process.

- Run
`deactivate`

to shut down the virtual environment.

## Review the code (optional)

You can review the code that defines the two HTTP trigger function endpoints:

```
[Function("httpget")]
public IActionResult Run([HttpTrigger(AuthorizationLevel.Function, "get")]
HttpRequest req,
string name)
{
var returnValue = string.IsNullOrEmpty(name)
? "Hello, World."
: $"Hello, {name}.";
_logger.LogInformation($"C# HTTP trigger function processed a request for {returnValue}.");
return new OkObjectResult(returnValue);
}
```


```
@FunctionName("httpget")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.FUNCTION)
HttpRequestMessage<Optional<String>> request,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
// Parse query parameter
String name = Optional.ofNullable(request.getQueryParameters().get("name")).orElse("World");
return request.createResponseBuilder(HttpStatus.OK).body("Hello, " + name).build();
}
```


```
const { app } = require('@azure/functions');
app.http('httpget', {
methods: ['GET'],
authLevel: 'function',
handler: async (request, context) => {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || await request.text() || 'world';
return { body: `Hello, ${name}!` };
}
});
```


```
import { app, HttpRequest, HttpResponseInit, InvocationContext } from "@azure/functions";
export async function httpGetFunction(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || await request.text() || 'world';
return { body: `Hello, ${name}!` };
};
app.http('httpget', {
methods: ['GET'],
authLevel: 'function',
handler: httpGetFunction
});
```


This `function.json`

file defines the `httpget`

function:

```
{
"bindings": [
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "Request",
"methods": [
"get"
],
"route": "httpget"
},
{
"type": "http",
"direction": "out",
"name": "Response"
}
]
}
```


This `run.ps1`

file implements the function code:

```
using namespace System.Net
# Input bindings are passed in via param block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell HTTP trigger function processed a request."
# Interact with query parameters
$name = $Request.Query.name
$body = "This HTTP triggered function executed successfully. Pass a name in the query string for a personalized response."
if ($name) {
$body = "Hello, $name. This HTTP triggered function executed successfully."
}
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $body
})
```


```
@app.route(route="httpget", methods=["GET"])
def http_get(req: func.HttpRequest) -> func.HttpResponse:
name = req.params.get("name", "World")
logging.info(f"Processing GET request. Name: {name}")
return func.HttpResponse(f"Hello, {name}!")
```


You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd).

You can review the complete template project [here](https://github.com/Azure-Samples/azure-functions-java-flex-consumption-azd).

You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-javascript-azd).

You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-typescript-azd).

You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-powershell-azd).

You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-python-http-azd).

After you verify your functions locally, it's time to publish them to Azure.

## Deploy to Azure

This project is configured to use the `azd up`

command to deploy this project to a new function app in a Flex Consumption plan in Azure.

Tip

The project includes a set of Bicep files (in the `infra`

folder) that `azd`

uses to create a secure deployment to a Flex consumption plan that follows best practices.

Run this command to have

`azd`

create the required Azure resources in Azure and deploy your code project to the new function app:`azd up`

The root folder contains the

`azure.yaml`

definition file required by`azd`

.If you're not already signed in, you're asked to authenticate with your Azure account.

When prompted, provide these required deployment parameters:

Parameter Description *Azure subscription*Subscription in which your resources are created. *Azure location*Azure region in which to create the resource group that contains the new Azure resources. Only regions that currently support the Flex Consumption plan are shown. *vnetEnabled*Choose *False*. When set to*True*the deployment creates your function app in a new virtual network.The

`azd up`

command uses your responses to these prompts with the Bicep configuration files to complete these deployment tasks:Create and configure these required Azure resources (equivalent to

`azd provision`

):- Flex Consumption plan and function app
- Azure Storage (required) and Application Insights (recommended)
- Access policies and roles for your account
- Service-to-service connections using managed identities (instead of stored connection strings)
- (Option) Virtual network to securely run both the function app and the other Azure resources

Package and deploy your code to the deployment container (equivalent to

`azd deploy`

). The app is then started and runs in the deployed package.

After the command completes successfully, you see links to the resources you created.


## Invoke the function on Azure

You can now invoke your function endpoints in Azure by making HTTP requests to their URLs by using your HTTP test tool or from the browser (for GET requests). When your functions run in Azure, access key authorization is enforced, and you must provide a function access key with your request.

You can use the Core Tools to get the URL endpoints of your functions running in Azure.

In your local terminal or command prompt, run these commands to get the URL endpoint values:

`$APP_NAME = azd env get-value AZURE_FUNCTION_NAME func azure functionapp list-functions $APP_NAME --show-keys`

The

`azd env get-value`

command gets your function app name from the local environment. When you use the`--show-keys`

option with`func azure functionapp list-functions`

, the returned**Invoke URL:**value for each endpoint includes a function-level access key.As before, use your HTTP test tool to validate these URLs in your function app running in Azure.


## Redeploy your code

Run the `azd up`

command as many times as you need to both provision your Azure resources and deploy code updates to your function app.

Note

Deployed code files are always overwritten by the latest deployment package.

Your initial responses to `azd`

prompts and any environment variables generated by `azd`

are stored locally in your named environment. Use the `azd env get-values`

command to review all of the variables in your environment that you used when creating Azure resources.

## Clean up resources

When you're done working with your function app and related resources, use this command to delete the function app and its related resources from Azure and avoid incurring any further costs:

```
azd down --no-prompt
```


Note

The `--no-prompt`

option instructs `azd`

to delete your resource group without a confirmation from you.

This command doesn't affect your local code project.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/scenario-host-mcp-server-sdks -->

# Quickstart: Host servers built with MCP SDKs on Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you learn how to host on Azure Functions Model Context Protocol (MCP) servers that you create by using official MCP SDKs. Flex Consumption plan hosting lets you take advantage of Azure Functions' serverless scale, pay-for-what-you-use billing model, and built-in security features. It's perfect for MCP servers that use the streamable-http transport.

This article uses a sample MCP server project built by using official MCP SDKs.

Tip

Functions also provides an MCP extension that enables you to create MCP servers by using Azure Functions programming model. For more information, see [Quickstart: Build a custom remote MCP server using Azure Functions](scenario-custom-remote-mcp-server).

Because the new server runs in a Flex Consumption plan, which follows a *pay-for-what-you-use* billing model, completing this quickstart incurs a small cost of a few cents or less in your Azure account.

Important

While [hosting your MCP servers using Custom Handlers](self-hosted-mcp-servers) is supported for all languages, this quickstart scenario currently only has examples for C#, Python, and TypeScript. To complete this quickstart, select one of these supported languages at the top of the article.

## Prerequisites

[Node.js 22](https://nodejs.org/)or above

[Python 3.11](https://www.python.org/)or above[uv](https://docs.astral.sh/uv/getting-started/installation/)for Python package management

[Visual Studio Code](https://code.visualstudio.com/)with these extensions:[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions). This extension requires[Azure Functions Core Tools](functions-run-local)v4.5.0 or above and attempts to install it when not available.

[Azure Developer CLI](/en-us/azure/developer/azure-developer-cli/install-azd)v1.17.2 or above[Azure CLI](/en-us/cli/azure/install-azure-cli). You can also run Azure CLI commands in[Azure Cloud Shell](../cloud-shell/overview).An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

Note

This sample requires that you have permission to create a [Microsoft Entra app](https://docs.azure.cn/entra/fundamentals/what-is-entra) in the Azure subscription you use.

## Get started with a sample project

The easiest way to get started is to clone an MCP server sample project built with official MCP SDKs:

- In Visual Studio Code, open a folder or workspace where you want to create your project.

In the Terminal, run this command to initialize the .NET sample:

`azd init --template mcp-sdk-functions-hosting-dotnet -e mcpsdkserver-dotnet`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/mcp-sdk-functions-hosting-dotnet)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also used in names of the resources you create in Azure.

In the Terminal, run this command to initialize the TypeScript sample:

`azd init --template mcp-sdk-functions-hosting-node -e mcpsdkserver-node`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/mcp-sdk-functions-hosting-node)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also used in names of the resources you create in Azure.

In the Terminal, run this command to initialize the Python sample:

`azd init --template mcp-sdk-functions-hosting-python -e mcpsdkserver-python`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/mcp-sdk-functions-hosting-java)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also used in names of the resources you create in Azure.

The code project template is for an MCP server with tools that access public weather APIs.

## Run the MCP server locally

Visual Studio Code integrates with [Azure Functions Core Tools](functions-run-local) to let you run this project on your local development computer.

- Open Terminal in the editor (
`Ctrl+Shift+``

)

- In the root directory, run
`func start`

to start the server. The**Terminal**panel displays the output from Core Tools.

- In the root directory, run
`npm install`

to install dependencies, then run`npm run build`

. - To start the server, run
`func start`

.

- In the root directory, run
`uv run func start`

to create virtual environment, install dependencies, and start the server.

## Test server by using GitHub Copilot

To verify your server by using GitHub Copilot in Visual Studio Code, follow these steps:

Open the

`mcp.json`

file in the`.vscode`

directory.Start the server by selecting the

**Start**button above the`local-mcp-server`

configuration.In the Copilot

**Chat**window, make sure that the**Agent**model is selected, select the**Configure tools**icon, and verify that`MCP Server:local-mcp-server`

is enabled in the chat.Run this prompt in chat:

`Return the weather forecast for New York City using #local-mcp-server`

Copilot should call one of the weather tools to help answer this question. When prompted to run the tool, select

**Allow in this Workspace**so you don't have to keep regranting this permission.

After you verify the tool functionality locally, you can stop the server and deploy the project code to Azure.

## Deploy to Azure

This project is configured to use the `azd up`

command to deploy this project to a new function app in a Flex Consumption plan in Azure. The project includes a set of Bicep files that `azd`

uses to create a secure deployment that follows best practices.

Sign in to Azure:

`azd login`

Configure Visual Studio Code as a preauthorized client application:

`azd env set PRE_AUTHORIZED_CLIENT_IDS aebc6443-996d-45c2-90f0-388ff96faa56`

A preauthorized application can authenticate to and access your MCP server without requiring more consent prompts.

In Visual Studio Code, press

`F1`to open the command palette. Search for and run the command`Azure Developer CLI (azd): Package, Provision and Deploy (up)`

. Then, sign in by using your Azure account.When prompted, provide these required deployment parameters:

Parameter Description *Azure subscription*Subscription in which your resources are created. *Azure location*Azure region in which to create the resource group that contains the new Azure resources. Only regions that currently support the Flex Consumption plan are shown. After the command completes successfully, you see links to the resources you created and the endpoint for your deployed MCP server. Make a note of your function app name, which you need for the next section.

Tip

If an error occurs when running the

`azd up`

command, just rerun the command. You can run`azd up`

repeatedly because it skips creating any resources that already exist. You can also call`azd up`

again when deploying updates to your service.

## Connect to the remote MCP server

Your MCP server is now running in Azure. To connect GitHub Copilot to your remote server, configure it in your workspace settings.

In the

`mcp.json`

file, switch to the remote server by selecting**Stop**for the`local-mcp-server`

configuration and**Start**on the`remote-mcp-server`

configuration.When prompted for

**The domain of the function app**, enter the name of your function app you noted in the previous section. When prompted to authenticate to Microsoft, select**Allow**then choose your Azure account.Verify the remote server by asking a question like:

`Return the weather forecast for Seattle using #remote-mcp-server.`

Copilot calls one of the weather tools to answer the query.


Tip

You can see output of a server by selecting **More...** > **Show Output**. The output provides useful information about possible connection failures. You can also select the gear icon to change log levels to **Traces** to get more details on the interactions between the client (Visual Studio Code) and the server.

## Review the code (optional)

You can review the code that defines the MCP server:

The MCP server code is defined in the project root. The server uses the official C# MCP SDK to define these weather-related tools:

```
using ModelContextProtocol;
using ModelContextProtocol.Server;
using System.ComponentModel;
using System.Globalization;
using System.Text.Json;
namespace QuickstartWeatherServer.Tools;
[McpServerToolType]
public sealed class WeatherTools
{
[McpServerTool, Description("Get weather alerts for a US state.")]
public static async Task<string> GetAlerts(
HttpClient client,
[Description("The US state to get alerts for. Use the 2 letter abbreviation for the state (e.g. NY).")] string state)
{
using var jsonDocument = await client.ReadJsonDocumentAsync($"/alerts/active/area/{state}");
var jsonElement = jsonDocument.RootElement;
var alerts = jsonElement.GetProperty("features").EnumerateArray();
if (!alerts.Any())
{
return "No active alerts for this state.";
}
return string.Join("\n--\n", alerts.Select(alert =>
{
JsonElement properties = alert.GetProperty("properties");
return $"""
Event: {properties.GetProperty("event").GetString()}
Area: {properties.GetProperty("areaDesc").GetString()}
Severity: {properties.GetProperty("severity").GetString()}
Description: {properties.GetProperty("description").GetString()}
Instruction: {properties.GetProperty("instruction").GetString()}
""";
}));
}
[McpServerTool, Description("Get weather forecast for a location.")]
public static async Task<string> GetForecast(
HttpClient client,
[Description("Latitude of the location.")] double latitude,
[Description("Longitude of the location.")] double longitude)
{
var pointUrl = string.Create(CultureInfo.InvariantCulture, $"/points/{latitude},{longitude}");
using var jsonDocument = await client.ReadJsonDocumentAsync(pointUrl);
var forecastUrl = jsonDocument.RootElement.GetProperty("properties").GetProperty("forecast").GetString()
?? throw new Exception($"No forecast URL provided by {client.BaseAddress}points/{latitude},{longitude}");
using var forecastDocument = await client.ReadJsonDocumentAsync(forecastUrl);
var periods = forecastDocument.RootElement.GetProperty("properties").GetProperty("periods").EnumerateArray();
return string.Join("\n---\n", periods.Select(period => $"""
{period.GetProperty("name").GetString()}
Temperature: {period.GetProperty("temperature").GetInt32()}°F
Wind: {period.GetProperty("windSpeed").GetString()} {period.GetProperty("windDirection").GetString()}
Forecast: {period.GetProperty("detailedForecast").GetString()}
"""));
}
}
```


You can view the complete project template in the [Azure Functions .NET MCP SDK hosting](https://github.com/Azure-Samples/mcp-sdk-functions-hosting-dotnet) GitHub repository.

The MCP server code is defined in the `server.py`

file. The server uses the official Python MCP SDK to define weather-related tools. This is the definition of the `get_forecast`

tool:

```
import os
import sys
import warnings
import logging
from typing import Any
from pathlib import Path
import httpx
from azure.identity import OnBehalfOfCredential, ManagedIdentityCredential
from mcp.server.fastmcp import FastMCP
from fastmcp.server.dependencies import get_http_request
from starlette.requests import Request
from starlette.responses import HTMLResponse
# Initialize FastMCP server
mcp = FastMCP("weather", stateless_http=True)
# Constants
NWS_API_BASE = "https://api.weather.gov"
USER_AGENT = "weather-app/1.0"
@mcp.tool()
async def get_forecast(latitude: float, longitude: float) -> str:
"""Get weather forecast for a location.
Args:
latitude: Latitude of the location
longitude: Longitude of the location
"""
# First get the forecast grid endpoint
points_url = f"{NWS_API_BASE}/points/{latitude},{longitude}"
points_data = await make_nws_request(points_url)
if not points_data:
return "Unable to fetch forecast data for this location."
# Get the forecast URL from the points response
forecast_url = points_data["properties"]["forecast"]
forecast_data = await make_nws_request(forecast_url)
if not forecast_data:
return "Unable to fetch detailed forecast."
# Format the periods into a readable forecast
periods = forecast_data["properties"]["periods"]
forecasts = []
for period in periods[:5]: # Only show next 5 periods
forecast = f"""
{period['name']}:
Temperature: {period['temperature']}°{period['temperatureUnit']}
Wind: {period['windSpeed']} {period['windDirection']}
Forecast: {period['detailedForecast']}
"""
forecasts.append(forecast)
return "\n---\n".join(forecasts)
```


You can view the complete project template in the [Azure Functions Python MCP SDK hosting](https://github.com/Azure-Samples/mcp-sdk-functions-hosting-python) GitHub repository.

The MCP server code is defined in the `src`

folder. The server uses the official Node.js MCP SDK to define weather-related tools. This is the definition of the `get-forecast`

tool:

```
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { z } from "zod";
import { ManagedIdentityCredential, OnBehalfOfCredential } from '@azure/identity';
const NWS_API_BASE = "https://api.weather.gov";
const USER_AGENT = "weather-app/1.0";
// Function to create a new server instance for each request (stateless)
export const createServer = () => {
const server = new McpServer({
name: "weather",
version: "1.0.0",
});
server.registerTool(
"get-forecast",
{
title: "Get Weather Forecast",
description: "Get weather forecast for a location",
inputSchema: {
latitude: z.number().min(-90).max(90).describe("Latitude of the location"),
longitude: z
.number()
.min(-180)
.max(180)
.describe("Longitude of the location"),
},
outputSchema: z.object({
forecast: z.string(),
}),
},
async ({ latitude, longitude }) => {
// Get grid point data
const pointsUrl = `${NWS_API_BASE}/points/${latitude.toFixed(4)},${longitude.toFixed(4)}`;
const pointsData = await makeNWSRequest<PointsResponse>(pointsUrl);
if (!pointsData) {
const output = { forecast: `Failed to retrieve grid point data for coordinates: ${latitude}, ${longitude}. This location may not be supported by the NWS API (only US locations are supported).` };
return {
content: [{ type: "text", text: JSON.stringify(output) }],
structuredContent: output,
};
}
const forecastUrl = pointsData.properties?.forecast;
if (!forecastUrl) {
const output = { forecast: "Failed to get forecast URL from grid point data" };
return {
content: [{ type: "text", text: JSON.stringify(output) }],
structuredContent: output,
};
}
// Get forecast data
const forecastData = await makeNWSRequest<ForecastResponse>(forecastUrl);
if (!forecastData) {
const output = { forecast: "Failed to retrieve forecast data" };
return {
content: [{ type: "text", text: JSON.stringify(output) }],
structuredContent: output,
};
}
const periods = forecastData.properties?.periods || [];
if (periods.length === 0) {
const output = { forecast: "No forecast periods available" };
return {
content: [{ type: "text", text: JSON.stringify(output) }],
structuredContent: output,
};
}
// Format forecast periods
const formattedForecast = periods.map((period: ForecastPeriod) =>
[
`${period.name || "Unknown"}:`,
`Temperature: ${period.temperature || "Unknown"}°${period.temperatureUnit || "F"}`,
`Wind: ${period.windSpeed || "Unknown"} ${period.windDirection || ""}`,
`${period.shortForecast || "No forecast available"}`,
"---",
].join("\n"),
);
const forecastText = `Forecast for ${latitude}, ${longitude}:\n\n${formattedForecast.join("\n")}`;
const output = { forecast: forecastText };
return {
content: [{ type: "text", text: forecastText }],
structuredContent: output,
};
},
);
return server;
}
```


You can view the complete project template in the [Azure Functions TypeScript MCP SDK hosting](https://github.com/Azure-Samples/mcp-sdk-functions-hosting-node) GitHub repository.

## Clean up resources

When you're done working with your MCP server and related resources, use this command to delete the function app and its related resources from Azure to avoid incurring further costs:

```
azd down
```

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-iot-output -->

# Azure Event Hubs output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to work with [Azure Event Hubs](../event-hubs/event-hubs-about) bindings for Azure Functions. Azure Functions supports trigger and output bindings for Event Hubs.

For information on setup and configuration details, see the [overview](functions-bindings-event-hubs).

Use the Event Hubs output binding to write events to an event stream. You must have send permission to an event hub to write events to it.

Make sure the required package references are in place before you try to implement an output binding.

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

## Example

The following example shows a [C# function](dotnet-isolated-process-guide) that writes a message string to an event hub, using the method return value as the output:

```
[Function(nameof(EventHubFunction))]
[FixedDelayRetry(5, "00:00:10")]
[EventHubOutput("dest", Connection = "EventHubConnection")]
public string EventHubFunction(
[EventHubTrigger("src", Connection = "EventHubConnection")] string[] input,
FunctionContext context)
{
_logger.LogInformation("First Event Hubs triggered message: {msg}", input[0]);
var message = $"Output message created at {DateTime.Now}";
return message;
}
```


The following example shows a timer triggered [TypeScript function](functions-reference-node?tabs=typescript) that sends a single message to an event hub:

```
import { app, InvocationContext, output, Timer } from '@azure/functions';
export async function timerTrigger1(myTimer: Timer, context: InvocationContext): Promise<string> {
const timeStamp = new Date().toISOString();
return `Message created at: ${timeStamp}`;
}
app.timer('timerTrigger1', {
schedule: '0 */5 * * * *',
return: output.eventHub({
eventHubName: 'myeventhub',
connection: 'MyEventHubSendAppSetting',
}),
handler: timerTrigger1,
});
```


To output multiple messages, return an array instead of a single object. For example:

```
const timeStamp = new Date().toISOString();
const message = `Message created at: ${timeStamp}`;
return [`1: ${message}`, `2: ${message}`];
```


The following example shows a timer triggered [JavaScript function](functions-reference-node) that sends a single message to an event hub:

```
const { app, output } = require('@azure/functions');
const eventHubOutput = output.eventHub({
eventHubName: 'myeventhub',
connection: 'MyEventHubSendAppSetting',
});
app.timer('timerTrigger1', {
schedule: '0 */5 * * * *',
return: eventHubOutput,
handler: (myTimer, context) => {
const timeStamp = new Date().toISOString();
return `Message created at: ${timeStamp}`;
},
});
```


To output multiple messages, return an array instead of a single object. For example:

```
const timeStamp = new Date().toISOString();
const message = `Message created at: ${timeStamp}`;
return [`1: ${message}`, `2: ${message}`];
```


Complete PowerShell examples are pending.

The following example shows an event hub trigger binding and a Python function that uses the binding. The function writes a message to an event hub. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="eventhub_output")
@app.route(route="eventhub_output")
@app.event_hub_output(arg_name="event",
event_hub_name="<EVENT_HUB_NAME>",
connection="<CONNECTION_SETTING>")
def eventhub_output(req: func.HttpRequest, event: func.Out[str]):
body = req.get_body()
if body is not None:
event.set(body.decode('utf-8'))
else:
logging.info('req body is none')
return 'ok'
```


Here's Python code that sends multiple messages:

```
import logging
import azure.functions as func
from typing import List
app = func.FunctionApp()
@app.function_name(name="eventhub_output")
@app.route(route="eventhub_output")
@app.event_hub_output(arg_name="event",
event_hub_name="<EVENT_HUB_NAME>",
connection="<CONNECTION_SETTING>")
def eventhub_output(req: func.HttpRequest, event: func.Out[List[str]]) -> func.HttpResponse:
my_messages=["message1", "message2","message3"]
event.set(my_messages)
return func.HttpResponse(f"Messages sent")
```


The following example shows a Java function that writes a message containing the current time to an event hub.

```
@FunctionName("sendTime")
@EventHubOutput(name = "event", eventHubName = "samples-workitems", connection = "AzureEventHubConnection")
public String sendTime(
@TimerTrigger(name = "sendTimeTrigger", schedule = "0 */5 * * * *") String timerInfo) {
return LocalDateTime.now().toString();
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@EventHubOutput`

annotation on parameters whose value would be published to Event Hubs. The parameter should be of type `OutputBinding<T>`

, where `T`

is a POJO or any native Java type.

## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attribute to configure the binding. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#event-hubs-output).

Use the [EventHubOutputAttribute] to define an output binding to an event hub, which supports the following properties.

| Parameters | Description |
|---|---|
EventHubName |
The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. |
Connection |
The name of an app setting or setting collection that specifies how to connect to Event Hubs. To learn more, see
|

## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, these properties are supported for `event_hub_output`

:

| Property | Description |
|---|---|
`arg_name` |
The variable name used in function code that represents the event. |
`event_hub_name` |
he name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. |
`connection` |
The name of an app setting or setting collection that specifies how to connect to Event Hubs. To learn more, see
|

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the [EventHubOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.eventhuboutput) annotation on parameters whose value would be published to Event Hubs. The following settings are supported on the annotation:

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `output.eventHub()`

method.

| Property | Description |
|---|---|
eventHubName |
The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. |
connection |
The name of an app setting or setting collection that specifies how to connect to Event Hubs. To learn more, see
|

The following table explains the binding configuration properties that you set in the *function.json* file, which differs by runtime version.

| function.json property | Description |
|---|---|
type |
Must be set to `eventHub` . |
direction |
Must be set to `out` . This parameter is set automatically when you create the binding in the Azure portal. |
name |
The variable name used in function code that represents the event. |
eventHubName |
Functions 2.x and higher. The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. |
connection |
The name of an app setting or setting collection that specifies how to connect to Event Hubs. To learn more, see
|

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

The parameter type supported by the Event Hubs output binding depends on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to write a single event, the Event Hubs output binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The event as a string. Use when the event is simple text. |
`byte[]` |
The bytes of the event. |
| JSON serializable types | An object representing the event. Functions tries to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write multiple events, the Event Hubs output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single event types |
An array containing multiple events. Each entry represents one event. |

For other output scenarios, create and use an [EventHubProducerClient](/en-us/dotnet/api/azure.messaging.eventhubs.producer.eventhubproducerclient) with other types from [Azure.Messaging.EventHubs](/en-us/dotnet/api/azure.messaging.eventhubs) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

There are two options for outputting an Event Hubs message from a function by using the [EventHubOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.eventhuboutput) annotation:

**Return value**: By applying the annotation to the function itself, the return value of the function is persisted as an Event Hubs message.**Imperative**: To explicitly set the message value, apply the annotation to a specific parameter of the type, where`OutputBinding<T>`

`T`

is a POJO or any native Java type. With this configuration, passing a value to the`setValue`

method persists the value as an Event Hubs message.

Complete PowerShell examples are pending.

There are two options for outputting an Event Hubs message from a function:

**Return value**: Set the`name`

property in*function.json*to`$return`

. With this configuration, the function's return value is persisted as an Event Hubs message.**Imperative**: Pass a value to the[set](/en-us/python/api/azure-functions/azure.functions.out#set-val--t-----none)method of the parameter declared as an[Out](/en-us/python/api/azure-functions/azure.functions.out)type. The value passed to`set`

is persisted as an Event Hubs message.

The output function parameter must be defined as `func.Out[func.EventHubEvent]`

or `func.Out[List[func.EventHubEvent]]`

. Refer to the [output example](#example) for details.

## Connections

The `connection`

property is a reference to environment configuration which specifies how the app should connect to Event Hubs. It may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections).

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

Obtain this connection string by clicking the **Connection Information** button for the [namespace](../event-hubs/event-hubs-create#create-an-event-hubs-namespace), not the event hub itself. The connection string must be for an Event Hubs namespace, not the event hub itself.

When used for triggers, the connection string must have at least "read" permissions to activate the function. When used for output bindings, the connection string must have "send" permissions to send messages to the event stream.

This connection string should be stored in an application setting with a name matching the value specified by the `connection`

property of the binding configuration.

### Identity-based connections

If you are using [version 5.x or higher of the extension](functions-bindings-event-hubs?tabs=extensionv5), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). To do this, you would define settings under a common prefix which maps to the `connection`

property in the trigger and binding configuration.

In this mode, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Fully Qualified Namespace | `<CONNECTION_NAME_PREFIX>__fullyQualifiedNamespace` |
The fully qualified Event Hubs namespace. | `myeventhubns.servicebus.windows.net` |

Additional properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

Note

When using [Azure App Configuration](../azure-app-configuration/quickstart-azure-functions-csharp) or [Key Vault](/en-us/azure/key-vault/general/overview) to provide settings for Managed Identity connections, setting names should use a valid key separator such as `:`

or `/`

in place of the `__`

to ensure names are resolved correctly.

For example, `<CONNECTION_NAME_PREFIX>:fullyQualifiedNamespace`

.

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

You will need to create a role assignment that provides access to your event hub at runtime. The scope of the role assignment can be for an Event Hubs namespace, or the event hub itself. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) are not sufficient. The following table shows built-in roles that are recommended when using the Event Hubs extension in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles |
|---|---|
| Trigger |
|

[Azure Event Hubs Data Sender](../role-based-access-control/built-in-roles#azure-event-hubs-data-sender)## Exceptions and return codes

| Binding | Reference |
|---|---|
| Event Hubs |
|

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-hubs-output -->

# Azure Event Hubs output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to work with [Azure Event Hubs](../event-hubs/event-hubs-about) bindings for Azure Functions. Azure Functions supports trigger and output bindings for Event Hubs.

For information on setup and configuration details, see the [overview](functions-bindings-event-hubs).

Use the Event Hubs output binding to write events to an event stream. You must have send permission to an event hub to write events to it.

Make sure the required package references are in place before you try to implement an output binding.

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

## Example

The following example shows a [C# function](dotnet-isolated-process-guide) that writes a message string to an event hub, using the method return value as the output:

```
[Function(nameof(EventHubFunction))]
[FixedDelayRetry(5, "00:00:10")]
[EventHubOutput("dest", Connection = "EventHubConnection")]
public string EventHubFunction(
[EventHubTrigger("src", Connection = "EventHubConnection")] string[] input,
FunctionContext context)
{
_logger.LogInformation("First Event Hubs triggered message: {msg}", input[0]);
var message = $"Output message created at {DateTime.Now}";
return message;
}
```


The following example shows a timer triggered [TypeScript function](functions-reference-node?tabs=typescript) that sends a single message to an event hub:

```
import { app, InvocationContext, output, Timer } from '@azure/functions';
export async function timerTrigger1(myTimer: Timer, context: InvocationContext): Promise<string> {
const timeStamp = new Date().toISOString();
return `Message created at: ${timeStamp}`;
}
app.timer('timerTrigger1', {
schedule: '0 */5 * * * *',
return: output.eventHub({
eventHubName: 'myeventhub',
connection: 'MyEventHubSendAppSetting',
}),
handler: timerTrigger1,
});
```


To output multiple messages, return an array instead of a single object. For example:

```
const timeStamp = new Date().toISOString();
const message = `Message created at: ${timeStamp}`;
return [`1: ${message}`, `2: ${message}`];
```


The following example shows a timer triggered [JavaScript function](functions-reference-node) that sends a single message to an event hub:

```
const { app, output } = require('@azure/functions');
const eventHubOutput = output.eventHub({
eventHubName: 'myeventhub',
connection: 'MyEventHubSendAppSetting',
});
app.timer('timerTrigger1', {
schedule: '0 */5 * * * *',
return: eventHubOutput,
handler: (myTimer, context) => {
const timeStamp = new Date().toISOString();
return `Message created at: ${timeStamp}`;
},
});
```


To output multiple messages, return an array instead of a single object. For example:

```
const timeStamp = new Date().toISOString();
const message = `Message created at: ${timeStamp}`;
return [`1: ${message}`, `2: ${message}`];
```


Complete PowerShell examples are pending.

The following example shows an event hub trigger binding and a Python function that uses the binding. The function writes a message to an event hub. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="eventhub_output")
@app.route(route="eventhub_output")
@app.event_hub_output(arg_name="event",
event_hub_name="<EVENT_HUB_NAME>",
connection="<CONNECTION_SETTING>")
def eventhub_output(req: func.HttpRequest, event: func.Out[str]):
body = req.get_body()
if body is not None:
event.set(body.decode('utf-8'))
else:
logging.info('req body is none')
return 'ok'
```


Here's Python code that sends multiple messages:

```
import logging
import azure.functions as func
from typing import List
app = func.FunctionApp()
@app.function_name(name="eventhub_output")
@app.route(route="eventhub_output")
@app.event_hub_output(arg_name="event",
event_hub_name="<EVENT_HUB_NAME>",
connection="<CONNECTION_SETTING>")
def eventhub_output(req: func.HttpRequest, event: func.Out[List[str]]) -> func.HttpResponse:
my_messages=["message1", "message2","message3"]
event.set(my_messages)
return func.HttpResponse(f"Messages sent")
```


The following example shows a Java function that writes a message containing the current time to an event hub.

```
@FunctionName("sendTime")
@EventHubOutput(name = "event", eventHubName = "samples-workitems", connection = "AzureEventHubConnection")
public String sendTime(
@TimerTrigger(name = "sendTimeTrigger", schedule = "0 */5 * * * *") String timerInfo) {
return LocalDateTime.now().toString();
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@EventHubOutput`

annotation on parameters whose value would be published to Event Hubs. The parameter should be of type `OutputBinding<T>`

, where `T`

is a POJO or any native Java type.

## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attribute to configure the binding. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#event-hubs-output).

Use the [EventHubOutputAttribute] to define an output binding to an event hub, which supports the following properties.

| Parameters | Description |
|---|---|
EventHubName |
The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. |
Connection |
The name of an app setting or setting collection that specifies how to connect to Event Hubs. To learn more, see
|

## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, these properties are supported for `event_hub_output`

:

| Property | Description |
|---|---|
`arg_name` |
The variable name used in function code that represents the event. |
`event_hub_name` |
he name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. |
`connection` |
The name of an app setting or setting collection that specifies how to connect to Event Hubs. To learn more, see
|

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the [EventHubOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.eventhuboutput) annotation on parameters whose value would be published to Event Hubs. The following settings are supported on the annotation:

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `output.eventHub()`

method.

| Property | Description |
|---|---|
eventHubName |
The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. |
connection |
The name of an app setting or setting collection that specifies how to connect to Event Hubs. To learn more, see
|

The following table explains the binding configuration properties that you set in the *function.json* file, which differs by runtime version.

| function.json property | Description |
|---|---|
type |
Must be set to `eventHub` . |
direction |
Must be set to `out` . This parameter is set automatically when you create the binding in the Azure portal. |
name |
The variable name used in function code that represents the event. |
eventHubName |
Functions 2.x and higher. The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. |
connection |
The name of an app setting or setting collection that specifies how to connect to Event Hubs. To learn more, see
|

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

The parameter type supported by the Event Hubs output binding depends on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to write a single event, the Event Hubs output binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The event as a string. Use when the event is simple text. |
`byte[]` |
The bytes of the event. |
| JSON serializable types | An object representing the event. Functions tries to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write multiple events, the Event Hubs output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single event types |
An array containing multiple events. Each entry represents one event. |

For other output scenarios, create and use an [EventHubProducerClient](/en-us/dotnet/api/azure.messaging.eventhubs.producer.eventhubproducerclient) with other types from [Azure.Messaging.EventHubs](/en-us/dotnet/api/azure.messaging.eventhubs) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

There are two options for outputting an Event Hubs message from a function by using the [EventHubOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.eventhuboutput) annotation:

**Return value**: By applying the annotation to the function itself, the return value of the function is persisted as an Event Hubs message.**Imperative**: To explicitly set the message value, apply the annotation to a specific parameter of the type, where`OutputBinding<T>`

`T`

is a POJO or any native Java type. With this configuration, passing a value to the`setValue`

method persists the value as an Event Hubs message.

Complete PowerShell examples are pending.

There are two options for outputting an Event Hubs message from a function:

**Return value**: Set the`name`

property in*function.json*to`$return`

. With this configuration, the function's return value is persisted as an Event Hubs message.**Imperative**: Pass a value to the[set](/en-us/python/api/azure-functions/azure.functions.out#set-val--t-----none)method of the parameter declared as an[Out](/en-us/python/api/azure-functions/azure.functions.out)type. The value passed to`set`

is persisted as an Event Hubs message.

The output function parameter must be defined as `func.Out[func.EventHubEvent]`

or `func.Out[List[func.EventHubEvent]]`

. Refer to the [output example](#example) for details.

## Connections

The `connection`

property is a reference to environment configuration which specifies how the app should connect to Event Hubs. It may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections).

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

Obtain this connection string by clicking the **Connection Information** button for the [namespace](../event-hubs/event-hubs-create#create-an-event-hubs-namespace), not the event hub itself. The connection string must be for an Event Hubs namespace, not the event hub itself.

When used for triggers, the connection string must have at least "read" permissions to activate the function. When used for output bindings, the connection string must have "send" permissions to send messages to the event stream.

This connection string should be stored in an application setting with a name matching the value specified by the `connection`

property of the binding configuration.

### Identity-based connections

If you are using [version 5.x or higher of the extension](functions-bindings-event-hubs?tabs=extensionv5), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). To do this, you would define settings under a common prefix which maps to the `connection`

property in the trigger and binding configuration.

In this mode, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Fully Qualified Namespace | `<CONNECTION_NAME_PREFIX>__fullyQualifiedNamespace` |
The fully qualified Event Hubs namespace. | `myeventhubns.servicebus.windows.net` |

Additional properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

Note

When using [Azure App Configuration](../azure-app-configuration/quickstart-azure-functions-csharp) or [Key Vault](/en-us/azure/key-vault/general/overview) to provide settings for Managed Identity connections, setting names should use a valid key separator such as `:`

or `/`

in place of the `__`

to ensure names are resolved correctly.

For example, `<CONNECTION_NAME_PREFIX>:fullyQualifiedNamespace`

.

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

You will need to create a role assignment that provides access to your event hub at runtime. The scope of the role assignment can be for an Event Hubs namespace, or the event hub itself. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) are not sufficient. The following table shows built-in roles that are recommended when using the Event Hubs extension in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles |
|---|---|
| Trigger |
|

[Azure Event Hubs Data Sender](../role-based-access-control/built-in-roles#azure-event-hubs-data-sender)## Exceptions and return codes

| Binding | Reference |
|---|---|
| Event Hubs |
|

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-run-local -->

# Develop Azure Functions locally using Core Tools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions Core Tools lets you develop and test your functions on your local computer. When you're ready, you can also use Core Tools to deploy your code project to Azure and work with application settings.

You're viewing the C# version of this article. Make sure to select your preferred Functions programming language at the top of the article.


If you want to get started right away, complete the [Core Tools quickstart article](how-to-create-function-azure-cli?pivots=programming-language-csharp).

You're viewing the Java version of this article. Make sure to select your preferred Functions programming language at the top of the article.


If you want to get started right away, complete the [Core Tools quickstart article](how-to-create-function-azure-cli?pivots=programming-language-java).

You're viewing the JavaScript version of this article. Make sure to select your preferred Functions programming language at the top of the article.


If you want to get started right away, complete the [Core Tools quickstart article](how-to-create-function-azure-cli?pivots=programming-language-javascript).

You're viewing the PowerShell version of this article. Make sure to select your preferred Functions programming language at the top of the article.


If you want to get started right away, complete the [Core Tools quickstart article](how-to-create-function-azure-cli?pivots=programming-language-powershell).

You're viewing the Python version of this article. Make sure to select your preferred Functions programming language at the top of the article.


If you want to get started right away, complete the [Core Tools quickstart article](how-to-create-function-azure-cli?pivots=programming-language-python).

You're viewing the TypeScript version of this article. Make sure to select your preferred Functions programming language at the top of the article.


If you want to get started right away, complete the [Core Tools quickstart article](how-to-create-function-azure-cli?pivots=programming-language-typescript).

## Install the Azure Functions Core Tools

The recommended way to install Core Tools depends on the operating system of your local development computer.

The following steps use a Windows installer (MSI) to install Core Tools v4.x. For more information about other package-based installers, see the [Core Tools readme](https://github.com/Azure/azure-functions-core-tools/blob/v4.x/README.md#windows).

Download and run the Core Tools installer, based on your version of Windows:

[v4.x - Windows 64-bit](https://go.microsoft.com/fwlink/?linkid=2174087)(Recommended.[Visual Studio Code debugging](functions-develop-vs-code#debugging-functions-locally)requires 64-bit.)[v4.x - Windows 32-bit](https://go.microsoft.com/fwlink/?linkid=2174159)

If you previously used Windows installer (MSI) to install Core Tools on Windows, you should uninstall the old version from Add Remove Programs before installing the latest version.

Tip

To install Core Tools on [Windows Subsystem for Linux (WSL)](/en-us/windows/wsl/install), follow the instructions on the Linux tab.

For help with version-related issues, see [Core Tools versions](#v2).

## Create your local project

Important

For Python, you must run Core Tools commands in a virtual environment. For more information, see [Quickstart: Create a Python function in Azure from the command line](how-to-create-function-azure-cli?pivots=programming-language-python#create-venv).

In the terminal window or from a command prompt, run the following command to create a project in the `MyProjFolder`

folder:

```
func init MyProjFolder --worker-runtime dotnet-isolated
```


By default this command creates a project that runs in-process with the Functions host on the current [Long-Term Support (LTS) version of .NET Core](https://dotnet.microsoft.com/platform/support/policy/dotnet-core#lifecycle). You can use the `--target-framework`

option to target a specific supported version of .NET, including .NET Framework. For more information, see the [ func init](functions-core-tools-reference#func-init) reference.

For a comparison between the two .NET process models, see the [process mode comparison article](dotnet-isolated-in-process-differences).

Java uses a Maven archetype to create the local project, along with your first HTTP triggered function. Rather than using `func init`

and `func new`

, you should instead follow the steps in the [Command line quickstart](how-to-create-function-azure-cli?pivots=programming-language-java).

This command creates a JavaScript project that uses the desired [programming model version](functions-reference-node).

This command creates a TypeScript project that uses the desired [programming model version](functions-reference-node).

```
func init MyProjFolder --worker-runtime powershell
```


This command creates a Python project that uses the desired [programming model version](functions-reference-python#programming-model).

When you run `func init`

without the `--worker-runtime`

option, you're prompted to choose your project language. To learn more about the available options for the `func init`

command, see the [ func init](functions-core-tools-reference#func-init) reference.

## Create a function

To add a function to your project, run the `func new`

command using the `--template`

option to select your trigger template. The following example creates an HTTP trigger named `MyHttpTrigger`

:

```
func new --template "Http Trigger" --name MyHttpTrigger
```


This example creates a Queue Storage trigger named `MyQueueTrigger`

:

```
func new --template "Azure Queue Storage Trigger" --name MyQueueTrigger
```


The following considerations apply when adding functions:

When you run

`func new`

without the`--template`

option, you're prompted to choose a template.Use the

command to see the complete list of available templates for your language.`func templates list`

When you add a trigger that connects to a service, you'll also need to add an application setting that references a connection string or a managed identity to the local.settings.json file. Using app settings in this way prevents you from having to embed credentials in your code. For more information, see

[Work with app settings locally](#local-settings).

- Core Tools also adds a reference to the specific binding extension to your C# project.

To learn more about the available options for the `func new`

command, see the [ func new](functions-core-tools-reference#func-new) reference.

## Add a binding to your function

Functions provides a set of service-specific input and output bindings, which make it easier for your function to connection to other Azure services without having to use the service-specific client SDKs. For more information, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings).

To add an input or output binding to an existing function, you must manually update the function definition.

The following example shows the function definition after adding a [Queue Storage output binding](functions-bindings-storage-queue-output) to an [HTTP triggered function](functions-bindings-http-webhook-trigger):

Because an HTTP triggered function also returns an HTTP response, the function returns a `MultiResponse`

object, which represents both the HTTP and queue output.

```
[Function("HttpExample")]
public static MultiResponse Run([HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequest req,
FunctionContext executionContext)
{
```


This example is the definition of the `MultiResponse`

object that includes the output binding:

```
public class MultiResponse
{
[QueueOutput("outqueue",Connection = "AzureWebJobsStorage")]
public string[] Messages { get; set; }
public IActionResult HttpResponse { get; set; }
}
```


When applying that example to your own project, you might need to change `HttpRequest`

to `HttpRequestData`

and `IActionResult`

to `HttpResponseData`

, depending on if you are using [ASP.NET Core integration](dotnet-isolated-process-guide#aspnet-core-integration) or not.

Messages are sent to the queue when the function completes. The way you define the output binding depends on your process model. For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=csharp#manually-add-bindings-based-on-examples).

```
@FunctionName("HttpExample")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@QueueOutput(name = "msg", queueName = "outqueue",
connection = "AzureWebJobsStorage") OutputBinding<String> msg,
final ExecutionContext context) {
```


For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=java#manually-add-bindings-based-on-examples).

```
const { app, output } = require('@azure/functions');
const sendToQueue = output.storageQueue({
queueName: 'outqueue',
connection: 'AzureWebJobsStorage',
});
app.http('HttpExample', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraOutputs: [sendToQueue],
handler: async (request, context) => {
try {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text());
context.log(`Name: ${name}`);
if (name) {
const msg = `Name passed to the function ${name}`;
context.extraOutputs.set(sendToQueue, [msg]);
return { body: msg };
} else {
context.log('Missing required data');
return { status: 404, body: 'Missing required data' };
}
} catch (error) {
context.log(`Error: ${error}`);
return { status: 500, body: 'Internal Server Error' };
}
},
});
```


The way you define the output binding depends on the version of your Node.js model. For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=javascript#manually-add-bindings-based-on-examples).

```
$outputMsg = $name
Push-OutputBinding -name msg -Value $outputMsg
```


For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=powershell#manually-add-bindings-based-on-examples).

```
@app.route(route="HttpExample")
@app.queue_output(arg_name="msg", queue_name="outqueue", connection="AzureWebJobsStorage")
def HttpExample(req: func.HttpRequest, msg: func.Out [func.QueueMessage]) -> func.HttpResponse:
logging.info('Python HTTP trigger function processed a request.')
```


The way you define the output binding depends on the version of your Python model. For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=python#manually-add-bindings-based-on-examples).

```
import {
app,
output,
HttpRequest,
HttpResponseInit,
InvocationContext,
StorageQueueOutput,
} from '@azure/functions';
const sendToQueue: StorageQueueOutput = output.storageQueue({
queueName: 'outqueue',
connection: 'AzureWebJobsStorage',
});
export async function HttpExample(
request: HttpRequest,
context: InvocationContext,
): Promise<HttpResponseInit> {
try {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text());
context.log(`Name: ${name}`);
if (name) {
const msg = `Name passed to the function ${name}`;
context.extraOutputs.set(sendToQueue, [msg]);
return { body: msg };
} else {
context.log('Missing required data');
return { status: 404, body: 'Missing required data' };
}
} catch (error) {
context.log(`Error: ${error}`);
return { status: 500, body: 'Internal Server Error' };
}
}
app.http('HttpExample', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: HttpExample,
});
```


The way you define the output binding depends on the version of your Node.js model. For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=typescript#manually-add-bindings-based-on-examples).

The following considerations apply when adding bindings to a function:

- For languages that define functions using the
*function.json*configuration file, Visual Studio Code simplifies the process of adding bindings to an existing function definition. For more information, see[Connect functions to Azure services using bindings](add-bindings-existing-function#visual-studio-code).

- When you add bindings that connect to a service, you must also add an application setting that references a connection string or managed identity to the local.settings.json file. For more information, see
[Work with app settings locally](#local-settings).

- When you add a supported binding, the extension should already be installed when your app uses extension bundle. For more information, see
[extension bundles](extension-bundles).

- When you add a binding that requires a new binding extension, you must also add a reference to that specific binding extension in your C# project.

For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=csharp#manually-add-bindings-based-on-examples).

For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=java#manually-add-bindings-based-on-examples).

For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=javascript#manually-add-bindings-based-on-examples).

For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=powershell#manually-add-bindings-based-on-examples).

For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=python#manually-add-bindings-based-on-examples).

For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=typescript#manually-add-bindings-based-on-examples).

## Start the Functions runtime

Before you can run or debug the functions in your project, you need to start the Functions host from the root directory of your project. The host enables triggers for all functions in the project. Use this command to start the local runtime:

```
mvn clean package
mvn azure-functions:run
```


```
func start
```


```
func start
```


```
npm install
npm start
```


This command must be [run in a virtual environment](how-to-create-function-azure-cli?pivots=programming-language-python).

When the Functions host starts, it outputs a list of functions in the project, including the URLs of any HTTP-triggered functions, like in this example:

Found the following functions: Host.Functions.MyHttpTrigger Job host started Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger

How your functions are loaded depends on your project configuration. To learn more, see [Registering a function](functions-reference-node#registering-a-function).

Keep in mind the following considerations when running your functions locally:

By default, authorization isn't enforced locally for HTTP endpoints. This means that all local HTTP requests are handled as

`authLevel = "anonymous"`

. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth). You can use the`--enableAuth`

option to require authorization when running locally. For more information, see`func start`

You can use the local Azurite emulator when locally running functions that require access to Azure Storage services (Queue Storage, Blob Storage, and Table Storage) without having to connect to these services in Azure. When using local emulation, make sure to start Azurite before starting the local host (func.exe). For more information, see

[Local storage emulation](functions-develop-local#local-storage-emulator).

- You can use local Azurite emulation to meet the storage requirement of the Python v2 worker.

You can trigger non-HTTP functions locally without connecting to a live service. For more information, see

[Run a local function](functions-run-local?tabs=non-http-trigger#run-a-local-function).When you include your Application Insights connection information in the local.settings.json file, local log data is written to the specific Application Insights instance. To keep local telemetry data separate from production data, consider using a separate Application Insights instance for development and testing.


- When using version 1.x of the Core Tools, instead use the
`func host start`

command to start the local runtime.

## Run a local function

With your local Functions host (func.exe) running, you can now trigger individual functions to run and debug your function code. The way in which you execute an individual function depends on its trigger type.

Note

Examples in this topic use the cURL tool to send HTTP requests from the terminal or a command prompt. You can use a tool of your choice to send HTTP requests to the local server. The cURL tool is available by default on Linux-based systems and Windows 10 build 17063 and later. On older Windows, you must first download and install the [cURL tool](https://curl.haxx.se/).

HTTP triggers are started by sending an HTTP request to the local endpoint and port as displayed in the func.exe output, which has this general format:

```
http://localhost:<PORT>/api/<FUNCTION_NAME>
```


In this URL template, `<FUNCTION_NAME>`

is the name of the function or route and `<PORT>`

is the local port on which func.exe is listening.

For example, this cURL command triggers the `MyHttpTrigger`

quickstart function from a GET request with the *name* parameter passed in the query string:

```
curl --get http://localhost:7071/api/MyHttpTrigger?name=Azure%20Rocks
```


This example is the same function called from a POST request passing *name* in the request body, shown for both Bash shell and Windows command line:

```
curl --request POST http://localhost:7071/api/MyHttpTrigger --data '{"name":"Azure Rocks"}'
```


```
curl --request POST http://localhost:7071/api/MyHttpTrigger --data "{'name':'Azure Rocks'}"
```


The following considerations apply when calling HTTP endpoints locally:

You can make GET requests from a browser passing data in the query string. For all other HTTP methods, you must use an HTTP testing tool that also keeps your data secure. For more information, see

[HTTP test tools](functions-develop-local#http-test-tools).Make sure to use the same server name and port that the Functions host is listening on. You see an endpoint like this in the output generated when starting the Function host. You can call this URL using any HTTP method supported by the trigger.


## Publish to Azure

The Azure Functions Core Tools supports three types of deployment:

| Deployment type | Command | Description |
|---|---|---|
| Project files |
`func azure functionapp publish` |

[zip deployment](functions-deployment-technologies#zip-deploy).`func azurecontainerapps deploy`

`func kubernetes deploy`

You must have either the [Azure CLI](/en-us/cli/azure/install-azure-cli) or [Azure PowerShell](/en-us/powershell/azure/install-azure-powershell) installed locally to be able to publish to Azure from Core Tools. By default, Core Tools uses these tools to authenticate with your Azure account.

If you don't have these tools installed, you need to instead [get a valid access token](/en-us/cli/azure/account#az-account-get-access-token) to use during deployment. You can present an access token using the `--access-token`

option in the deployment commands.

## Deploy project files

To publish your local code to a function app in Azure, use the [ func azure functionapp publish](functions-core-tools-reference#func-azure-functionapp-publish) command, as in the following example:

```
func azure functionapp publish <FunctionAppName>
```


This command publishes project files from the current directory to the `<FunctionAppName>`

as a .zip deployment package. If the project requires compilation, it's done remotely during deployment.

Java uses Maven to publish your local project to Azure instead of Core Tools. Use the following Maven command to publish your project to Azure:

```
mvn azure-functions:deploy
```


When you run this command, Azure resources are created during the initial deployment based on the settings in your *pom.xml* file. For more information, see [Deploy the function project to Azure](how-to-create-function-azure-cli?pivots=programming-language-java#deploy-the-function-project-to-azure).

The following considerations apply to this kind of deployment:

Publishing overwrites existing files in the remote function app deployment.

You must have already

[created a function app in your Azure subscription](functions-cli-samples#create). Core Tools deploys your project code to this function app resource. To learn how to create a function app from the command prompt or terminal window using the Azure CLI or Azure PowerShell, see[Create a Function App for serverless execution](scripts/functions-cli-create-serverless). You can also[create these resources in the Azure portal](functions-create-function-app-portal#create-a-function-app). You get an error when you try to publish to a`<FunctionAppName>`

that doesn't exist in your subscription.A project folder may contain language-specific files and directories that shouldn't be published. Excluded items are listed in a .funcignore file in the root project folder.

By default, your project is deployed so that it

[runs from the deployment package](run-functions-from-deployment-package). To disable this recommended deployment mode, use the.`--nozip`

optionA

[remote build](functions-deployment-technologies#remote-build)is performed on compiled projects. This can be controlled by using the.`--no-build`

optionUse the

option to automatically create app settings in your function app based on values in the local.settings.json file.`--publish-local-settings`

To publish to a specific named slot in your function app, use the

.`--slot`

option

## Deploy containers

Core Tools lets you deploy your [containerized function app](functions-create-container-registry) to both managed Azure Container Apps environments and Kubernetes clusters that you manage.

Use the following [ func azurecontainerapps deploy](functions-core-tools-reference#func-azurecontainerapps-deploy) command to deploy an existing container image to a Container Apps environment:

```
func azurecontainerapps deploy --name <APP_NAME> --environment <ENVIRONMENT_NAME> --storage-account <STORAGE_CONNECTION> --resource-group <RESOURCE_GROUP> --image-name <IMAGE_NAME> [--registry-password] [--registry-server] [--registry-username]
```


When you deploy to an Azure Container Apps environment, the following considerations apply:

The environment and storage account must already exist. The storage account connection string you provide is used by the deployed function app.

You don't need to create a separate function app resource when deploying to Container Apps.

Storage connection strings and other service credentials are important secrets. Make sure to securely store any script files using

`func azurecontainerapps deploy`

and don't store them in any publicly accessible source control systems. You can[encrypt the local.settings.json file](#encrypt-the-local-settings-file)for added security.

For more information, see [Azure Container Apps hosting of Azure Functions](functions-container-apps-hosting).

## Work with app settings locally

When your function app runs in Azure, settings required by your functions are [stored encrypted in app settings](functions-how-to-use-azure-function-app-settings#settings). During local development, these settings are instead added to the `Values`

collection in the *local.settings.json* file. The *local.settings.json* file also stores settings used by local development tools.

Items in the `Values`

collection in your project's *local.settings.json* file are intended to mirror items in your function app's [application settings](functions-how-to-use-azure-function-app-settings#settings) in Azure.

The following considerations apply when working with the local settings file:

Because the local.settings.json may contain secrets, such as connection strings, you should never store it in a remote repository. Core Tools helps you encrypt this local settings file for improved security. For more information, see

[Local settings file](functions-develop-local#local-settings-file). You can also[encrypt the local.settings.json file](#encrypt-the-local-settings-file)for added security.By default, local settings aren't migrated automatically when the project is published to Azure. Use the

option when you publish your project files to make sure these settings are added to the function app in Azure. Values in the`--publish-local-settings`

`ConnectionStrings`

section are never published. You can also[upload settings from the local.settings.json file](#upload-local-settings-to-azure)at any time.You can download and overwrite settings in your local.settings.json file with settings from your function app in Azure. For more information, see

[Download application settings](#download-application-settings).

- The function app settings values can also be read in your code as environment variables. For more information, see
[Environment variables](functions-dotnet-class-library#environment-variables).

- The function app settings values can also be read in your code as environment variables. For more information, see
[Environment variables](functions-reference-java#environment-variables).

- The function app settings values can also be read in your code as environment variables. For more information, see
[Environment variables](functions-reference-node#environment-variables).

- The function app settings values can also be read in your code as environment variables. For more information, see
[Environment variables](functions-reference-powershell#environment-variables).

- The function app settings values can also be read in your code as environment variables. For more information, see
[Environment variables](functions-reference-python#environment-variables).

- When no valid storage connection string is set for
and a local storage emulator isn't being used, an error is shown. You can use Core Tools to`AzureWebJobsStorage`

[download a specific connection string](#download-a-storage-connection-string)from any of your Azure Storage accounts.

### Download application settings

From the project root, use the following command to download all application settings from the `myfunctionapp12345`

app in Azure:

```
func azure functionapp fetch-app-settings myfunctionapp12345
```


This command overwrites any existing settings in the local.settings.json file with values from Azure. When not already present, new items are added to the collection. For more information, see the [ func azure functionapp fetch-app-settings](functions-core-tools-reference#func-azure-functionapp-fetch-app-settings) command.

### Download a storage connection string

Core Tools also make it easy to get the connection string of any storage account to which you have access. From the project root, use the following command to download the connection string from a storage account named `mystorage12345`

.

```
func azure storage fetch-connection-string mystorage12345
```


This command adds a setting named `mystorage12345_STORAGE`

to the local.settings.json file, which contains the connection string for the `mystorage12345`

account. For more information, see the [ func azure storage fetch-connection-string](functions-core-tools-reference#func-azure-storage-fetch-connection-string) command.

For improved security during development, consider [encrypting the local.settings.json file](#encrypt-the-local-settings-file).

### Upload local settings to Azure

When you publish your project files to Azure without using the `--publish-local-settings`

option, settings in the local.settings.json file aren't set in your function app. You can always rerun the `func azure functionapp publish`

with the `--publish-settings-only`

option to upload just the settings without republishing the project files.

The following example uploads just settings from the `Values`

collection in the local.settings.json file to the function app in Azure named `myfunctionapp12345`

:

```
func azure functionapp publish myfunctionapp12345 --publish-settings-only
```


### Encrypt the local settings file

To improve security of connection strings and other valuable data in your local settings, Core Tools lets you encrypt the local.settings.json file. When this file is encrypted, the runtime automatically decrypts the settings when needed the same way it does with application setting in Azure. You can also decrypt a locally encrypted file to work with the settings.

Use the following command to encrypt the local settings file for the project:

```
func settings encrypt
```


Use the following command to decrypt an encrypted local setting, so that you can work with it:

```
func settings decrypt
```


When the settings file is encrypted and decrypted, the file's `IsEncrypted`

setting also gets updated.

## Configure binding extensions

[Functions triggers and bindings](functions-triggers-bindings) are implemented as .NET extension (NuGet) packages. To be able to use a specific binding extension, that extension must be installed in the project.

This section doesn't apply to version 1.x of the Functions runtime. In version 1.x, supported bindings were included in the core product extension.

For C# class library projects, add references to the specific NuGet packages for the binding extensions required by your functions. C# script (.csx) project must use [extension bundles](extension-bundles).

Functions provides *extension bundles* to make is easy to work with binding extensions in your project. Extension bundles, which are versioned and defined in the host.json file, install a complete set of compatible binding extension packages for your app. Your host.json should already have extension bundles enabled. If for some reason you need to add or update the extension bundle in the host.json file, see [Extension bundles](extension-bundles).

If you must use a binding extension or an extension version not in a supported bundle, you need to manually install extensions. For such rare scenarios, see the [ func extensions install](functions-core-tools-reference#func-extensions-install) command.

## Core Tools versions

Major versions of Azure Functions Core Tools are linked to specific major versions of the Azure Functions runtime. For example, version 4.x of Core Tools supports version 4.x of the Functions runtime. This version is the recommended major version of both the Functions runtime and Core Tools. You can determine the latest release version of Core Tools in the [Azure Functions Core Tools repository](https://github.com/Azure/azure-functions-core-tools/releases/latest).

[
Starting with version 4.0.6517 of the Core Tools, in-process model projects must reference ][version 4.5.0 or later of Microsoft.NET.Sdk.Functions](https://www.nuget.org/packages/Microsoft.NET.Sdk.Functions/4.5.0). If an earlier version is used, the

`func start`

command will error.Run the following command to determine the version of your current Core Tools installation:

```
func --version
```


Unless otherwise noted, the examples in this article are for version 4.x.

The following considerations apply to Core Tools installations:

You can only install one version of Core Tools on a given computer.

When upgrading to the latest version of Core Tools, you should use the same method that you used for original installation to perform the upgrade. For example, if you used an MSI on Windows, uninstall the current MSI and install the latest one. Or if you used npm, rerun the

`npm install command`

.Version 2.x and 3.x of Core Tools were used with versions 2.x and 3.x of the Functions runtime, which have reached their end of support. For more information, see

[Azure Functions runtime versions overview](functions-versions).

- Version 1.x of Core Tools is required when using version 1.x of the Functions Runtime, which is still supported. This version of Core Tools can only be run locally on Windows computers. If you're currently running on version 1.x, you should consider
[migrating your app to version 4.x](migrate-version-1-version-4)today.

## Next steps

Learn how to [develop, test, and publish Azure functions by using Azure Functions core tools](/en-us/training/modules/develop-test-deploy-azure-functions-with-core-tools/). Azure Functions Core Tools is [open source and hosted on GitHub](https://github.com/azure/azure-functions-cli). To file a bug or feature request, [open a GitHub issue](https://github.com/azure/azure-functions-cli/issues).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/dotnet-isolated-in-process-differences -->

# Differences between the isolated worker model and the in-process model for .NET on Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

There are two execution models for .NET functions:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

This article describes the current state of the functional and behavioral differences between the two models. To migrate from the in-process model to the isolated worker model, see [Migrate .NET apps from the in-process model to the isolated worker model](migrate-dotnet-to-isolated-model).

## Execution model comparison table

Use the following table to compare feature and functional differences between the two models:

| Feature/behavior | Isolated worker model | In-process model3 |
|---|---|---|
|

Standard Term Support (STS) versions,

.NET Framework

[Microsoft.Azure.Functions.Worker](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker/)[Microsoft.Azure.Functions.Worker.Sdk](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Sdk)[Microsoft.NET.Sdk.Functions](https://www.nuget.org/packages/Microsoft.NET.Sdk.Functions/)[Microsoft.Azure.Functions.Worker.Extensions.*](https://www.nuget.org/packages?q=Microsoft.Azure.Functions.Worker.Extensions)[Microsoft.Azure.WebJobs.Extensions.*](https://www.nuget.org/packages?q=Microsoft.Azure.WebJobs.Extensions)[Supported](durable/durable-functions-dotnet-isolated-overview)[Supported](durable/durable-functions-overview)JSON serializable types

Arrays/enumerations

[Service SDK types](dotnet-isolated-process-guide#sdk-types)4[JSON serializable](/en-us/dotnet/api/system.text.json.jsonserializeroptions)typesArrays/enumerations

Service SDK types

4[HttpRequestData](/en-us/dotnet/api/microsoft.azure.functions.worker.http.httprequestdata?view=azure-dotnet&preserve-view=true)/[HttpResponseData](/en-us/dotnet/api/microsoft.azure.functions.worker.http.httpresponsedata?view=azure-dotnet&preserve-view=true)[HttpRequest](/en-us/dotnet/api/microsoft.aspnetcore.http.httprequest)/[IActionResult](/en-us/dotnet/api/microsoft.aspnetcore.mvc.iactionresult)(using[ASP.NET Core integration](dotnet-isolated-process-guide#aspnet-core-integration))5[HttpRequest](/en-us/dotnet/api/microsoft.aspnetcore.http.httprequest)/[IActionResult](/en-us/dotnet/api/microsoft.aspnetcore.mvc.iactionresult)5[HttpRequestMessage](/en-us/dotnet/api/system.net.http.httprequestmessage)/[HttpResponseMessage](/en-us/dotnet/api/system.net.http.httpresponsemessage)- single or

[multiple outputs](dotnet-isolated-process-guide#multiple-output-bindings)- arrays of outputs

`out`

parameters,`IAsyncCollector`

1[work with SDK types directly](dotnet-isolated-process-guide#register-azure-clients)[Supported](functions-dotnet-class-library#binding-at-runtime)[Supported](dotnet-isolated-process-guide#dependency-injection)(improved model consistent with .NET ecosystem)[Supported](functions-dotnet-dependency-injection)[Supported](dotnet-isolated-process-guide#middleware)[/](/en-us/dotnet/api/microsoft.extensions.logging.logger-1)`ILogger<T>`

[obtained from](/en-us/dotnet/api/microsoft.extensions.logging.ilogger)`ILogger`

[FunctionContext](/en-us/dotnet/api/microsoft.azure.functions.worker.functioncontext)or by using[dependency injection](dotnet-isolated-process-guide#dependency-injection)[passed to the function](/en-us/dotnet/api/microsoft.extensions.logging.ilogger)`ILogger`

[by using](/en-us/dotnet/api/microsoft.extensions.logging.logger-1)`ILogger<T>`

[dependency injection](functions-dotnet-dependency-injection)[Supported](dotnet-isolated-process-guide#application-insights)[Supported](functions-monitoring#dependencies)[Supported](dotnet-isolated-process-guide#cancellation-tokens)[Supported](functions-dotnet-class-library#cancellation-tokens)2[Configurable optimizations](dotnet-isolated-process-guide#performance-optimizations)[Supported](dotnet-isolated-process-guide#readytorun)[Supported](functions-dotnet-class-library#readytorun)[Supported](flex-consumption-plan#supported-language-stack-versions)[Preview](dotnet-aspire-integration)- When you need to interact with a service using parameters determined at runtime, using the corresponding service SDKs directly is recommended over using imperative bindings. The SDKs are less verbose, cover more scenarios, and have advantages for error handling and debugging purposes. This recommendation applies to both models.
- Cold start times could be additionally affected on Windows when using some preview versions of .NET due to just-in-time loading of preview frameworks. This impact applies to both the in-process and isolated worker models but can be noticeable when comparing across different versions. This delay for preview versions isn't present on Linux plans.
- C# Script functions also run in-process and use the same libraries as in-process class library functions. For more information, see the
[Azure Functions C# script (.csx) developer reference](functions-reference-csharp). - Service SDK types include types from the
[Azure SDK for .NET](/en-us/dotnet/azure/sdk/azure-sdk-for-dotnet)such as[BlobClient](/en-us/dotnet/api/azure.storage.blobs.blobclient). - ASP.NET Core types aren't supported for .NET Framework.

## Supported versions

Versions of the Functions runtime support specific versions of .NET. To learn more about Functions versions, see [Azure Functions runtime versions overview](functions-versions). Version support also depends on whether your functions run in-process or isolated worker process.

Note

To learn how to change the Functions runtime version used by your function app, see [view and update the current runtime version](set-runtime-version#view-the-current-runtime-version).

The following table shows the highest level of .NET or .NET Framework that can be used with a specific version of Functions.

| Functions runtime version |
|
|---|

[In-process model](functions-dotnet-class-library)

4

15.NET 9.0

.NET 8.0

.NET Framework 4.8

231 .NET 6 was previously supported on both models but reached the [end of official support](https://dotnet.microsoft.com/platform/support/policy) on November 12, 2024. .NET 7 was previously supported on the isolated worker model but reached the [end of official support](https://dotnet.microsoft.com/platform/support/policy) on May 14, 2024.

2 The build process also requires the [.NET SDK](https://dotnet.microsoft.com/download).

3 Support ends for version 1.x of the Azure Functions runtime on September 14, 2026. For more information, see [this support announcement](https://aka.ms/azure-functions-retirements/hostv1). For continued full support, you should [migrate your apps to version 4.x](migrate-version-1-version-4).

4 Support ends for the in-process model on November 10, 2026. For more information, see [this support announcement](https://aka.ms/azure-functions-retirements/in-process-model). For continued full support, you should [migrate your apps to the isolated worker model](migrate-dotnet-to-isolated-model).

5 You can't run .NET 10 apps on Linux in the Consumption plan. To run on Linux, you should instead use the [Flex Consumption plan](flex-consumption-plan). For step-by-step migration instructions, see [Migrate Consumption plan apps to the Flex Consumption plan](migration/migrate-plan-consumption-to-flex?pivots=platform-linux).

For the latest news about Azure Functions releases, including the removal of specific older minor versions, monitor [Azure App Service announcements](https://github.com/Azure/app-service-announcements/issues).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-table -->

# Azure Tables bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions integrates with [Azure Tables](/en-us/azure/cosmos-db/table/introduction) via [triggers and bindings](functions-triggers-bindings). Integrating with Azure Tables allows you to build functions that read and write data using [Azure Cosmos DB for Table](/en-us/azure/cosmos-db/table/introduction) and [Azure Table Storage](../storage/tables/table-storage-overview).

| Action | Type |
|---|---|
| Read table data in a function |
|

[Output binding](functions-bindings-storage-table-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The process for installing the extension varies depending on the extension version:

This version introduces the ability to [connect using an identity instead of a secret](functions-reference#configure-an-identity-based-connection). For a tutorial on configuring your function apps with managed identities, see the [creating a function app with identity-based connections tutorial](functions-identity-based-connections-tutorial).

This version allows you to bind to types from [ Azure.Data.Tables](/en-us/dotnet/api/azure.data.tables). It also introduces the ability to use Azure Cosmos DB for Table.

This extension is available by installing the [Microsoft.Azure.Functions.Worker.Extensions.Tables NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Tables) into a project using version 5.x or higher of the extensions for [blobs](functions-bindings-storage-blob?tabs=isolated-process,extensionv5) and [queues](functions-bindings-storage-queue?tabs=isolated-process,extensionv5).

Using the .NET CLI:

```
# Install the Azure Tables extension
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Tables --version 1.0.0
# Update the combined Azure Storage extension (to a version which no longer includes Azure Tables)
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Storage --version 5.0.0
```


Note

Azure Blobs, Azure Queues, and Azure Tables now use separate extensions and are referenced individually. For example, to use the triggers and bindings for all three services in your .NET isolated-process app, you should add the following packages to your project:

[Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs)[Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues)[Microsoft.Azure.Functions.Worker.Extensions.Tables](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Tables)

Previously, the extensions shipped together as [Microsoft.Azure.Functions.Worker.Extensions.Storage, version 4.x](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage/4.0.4). This same package also has a [5.x version](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage/5.0.0), which references the split packages for blobs and queues only. When upgrading your package references from older versions, you may therefore need to additionally reference the new [Microsoft.Azure.Functions.Worker.Extensions.Tables](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Tables) NuGet package. Also, when referencing these newer split packages, make sure you are not referencing an older version of the combined storage package, as this will result in conflicts from two definitions of the same bindings.

If you're writing your application using F#, you must also configure this extension as part of the app's [startup configuration](dotnet-isolated-process-guide#start-up-and-configuration). In the call to `ConfigureFunctionsWorkerDefaults()`

or `ConfigureFunctionsWebApplication()`

, add a delegate that takes an `IFunctionsWorkerApplication`

parameter. Then within the body of that delegate, call `ConfigureTablesExtension()`

on the object:

```
let hostBuilder = new HostBuilder()
hostBuilder.ConfigureFunctionsWorkerDefaults(fun (context: HostBuilderContext) (appBuilder: IFunctionsWorkerApplicationBuilder) ->
appBuilder.ConfigureTablesExtension() |> ignore
) |> ignore
```


## Install bundle

To be able to use this binding extension in your app, make sure that the *host.json* file in the root of your project contains this `extensionBundle`

reference:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.0.0, 5.0.0)"
}
}
```


In this example, the `version`

value of `[4.0.0, 5.0.0)`

instructs the Functions host to use a bundle version that is at least `4.0.0`

but less than `5.0.0`

, which includes all potential versions of 4.x. This notation effectively maintains your app on the latest available minor version of the v4.x extension bundle.

When possible, you should use the latest extension bundle major version and allow the runtime to automatically maintain the latest minor version. You can view the contents of the latest bundle on the [extension bundles release page](https://github.com/Azure/azure-functions-extension-bundles/releases/latest). For more information, see [Azure Functions extension bundles](extension-bundles).

## Binding types

The binding types supported for .NET depend on both the extension version and C# execution mode, which can be one of the following:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see binding type details for the mode and version.

The isolated worker process supports parameter types according to the tables below. Support for binding to types from [Azure.Data.Tables](/en-us/dotnet/api/azure.data.tables) is in preview.

**Azure Tables input binding**

When working with a single table entity, the Azure Tables input binding can bind to the following types:

| Type | Description |
|---|---|
| A JSON serializable type that implements
|

[ITableEntity](/en-us/dotnet/api/azure.data.tables.itableentity)or have a string`RowKey`

property and a string `PartitionKey`

property.[TableEntity](/en-us/dotnet/api/azure.data.tables.tableentity)1When working with multiple entities from a query, the Azure Tables input binding can bind to the following types:

| Type | Description |
|---|---|
`IEnumerable<T>` where `T` implements
|
An enumeration of entities returned by the query. Each entry represents one entity. The type `T` must implement
`RowKey` property and a string `PartitionKey` property. |
1 |

1 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.Tables 1.2.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Tables/1.2.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

**Azure Tables output binding**

When you want the function to write to a single entity, the Azure Tables output binding can bind to the following types:

| Type | Description |
|---|---|
| A JSON serializable type that implements [ITableEntity] | Functions attempts to serialize a plain-old CLR object (POCO) type as the entity. The type must implement [ITableEntity] or have a string `RowKey` property and a string `PartitionKey` property. |

When you want the function to write to multiple entities, the Azure Tables output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single entity types |
An array containing multiple entities. Each entry represents one entity. |

For other output scenarios, create and use a [TableClient](/en-us/dotnet/api/azure.data.tables.tableclient) with other types from [Azure.Data.Tables](/en-us/dotnet/api/azure.data.tables) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-storage-blob-triggered-function -->

# Create a function in Azure that's triggered by Blob storage

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Learn how to create a function triggered when files are uploaded to or updated in a Blob storage container.

Note

In-portal editing is only supported for JavaScript, PowerShell, and C# Script functions.
Python in-portal editing is supported only when running in the Consumption plan.
To create a C# Script app that supports in-portal editing, you must choose a runtime **Version** that supports the **in-process model**.

When possible, you should [develop your functions locally](functions-develop-local).

To learn more about the limitations on editing function code in the Azure portal, see [Development limitations in the Azure portal](functions-how-to-use-azure-function-app-settings#development-limitations-in-the-azure-portal).

## Prerequisites

- An Azure subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

## Create an Azure Function app

From the Azure portal menu or the

**Home**page, select**Create a resource**.In the

**New**page, select**Function App**.Under

**Select a hosting option**, select**Consumption**>**Select**to create your app in the default**Consumption**plan. In this[serverless](https://azure.microsoft.com/overview/serverless-computing/)hosting option, you pay only for the time your functions run.[Premium plan](functions-premium-plan)also offers dynamic scaling. When you run in an App Service plan, you must manage the[scaling of your function app](functions-scale).On the

**Basics**page, use the function app settings as specified in the following table:Setting Suggested value Description **Subscription**Your subscription The subscription under which you create your new function app. [Resource Group](../azure-resource-manager/management/overview)*myResourceGroup*Name for the new resource group in which you create your function app. You should create a new resource group because there are [known limitations when creating new function apps in an existing resource group](functions-scale#limitations-for-creating-new-function-apps-in-an-existing-resource-group).**Function App name**Globally unique name Name that identifies your new function app. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

. To guarantee a unique app name, you can optionally enable**Secure unique default hostname**, which is currently in preview.**Runtime stack**Preferred language Choose a runtime that supports your favorite function programming language. In-portal editing is only available for JavaScript, PowerShell, Python, TypeScript, and C# script.

To create a C# Script app that supports in-portal editing, you must choose a runtime**Version**that supports the**in-process model**.

C# class library and Java functions must be[developed locally](functions-develop-local#local-development-environments).**Version**Version number Choose the version of your installed runtime. **Region**Preferred region Select a [region](https://azure.microsoft.com/regions/)that's near you or near other services that your functions can access.**Operating system**Windows An operating system is preselected for you based on your runtime stack selection, but you can change the setting if necessary. In-portal editing is only supported on Windows. Accept the default options in the remaining tabs, including the default behavior of creating a new storage account on the

**Storage**tab and a new Application Insight instance on the**Monitoring**tab. You can also choose to use an existing storage account or Application Insights instance.Select

**Review + create**to review the app configuration you chose, and then select**Create**to provision and deploy the function app.Select the

**Notifications**icon in the upper-right corner of the portal and watch for the**Deployment succeeded**message.Select

**Go to resource**to view your new function app. You can also select**Pin to dashboard**. Pinning makes it easier to return to this function app resource from your dashboard.

You've successfully created your new function app. Next, you create a function in the new function app.

## Create an Azure Blob storage triggered function

In your function app, select

**Overview**, and then select**+ Create**under**Functions**.Under

**Select a template**, choose the**Blob trigger**template and select**Next**.In

**Template details**, configure the new trigger with the settings as specified in this table, then select**Create**:Setting Suggested value Description **Job type**Append to app You only see this setting for a Python v2 app. **New Function**Unique in your function app Name of this blob triggered function. **Path**samples-workitems/{name} Location in Blob storage being monitored. The file name of the blob is passed in the binding as the *name*parameter.**Storage account connection**AzureWebJobsStorage You can use the storage account connection already being used by your function app, or create a new one. Azure creates the Blob Storage triggered function based on the provided values. Next, create the

**samples-workitems**container.

## Create the container

Return to the

**Overview**page for your function app, select your**Resource group**, then find and select the storage account in your resource group.In the storage account page, select

**Data storage**>**Containers**>**+ Container**.In the

**Name**field, type`samples-workitems`

, and then select**Create**to create a container.Select the new

`samples-workitems`

container, which you use to test the function by uploading a file to the container.

## Test the function

In a new browser window, return to your function app page and select

**Log stream**, which displays real-time logging for your app.From the

`samples-workitems`

container page, select**Upload**>**Browse for files**, browse to a file on your local computer (such as an image file), and choose the file.Select

**Open**and then**Upload**.Go back to your function app logs and verify that the blob has been read.

Note

When your function app runs in the default Consumption plan, there may be a delay of up to several minutes between the blob being added or updated and the function being triggered. If you need low latency in your blob triggered functions, consider one of these

[other blob trigger options](storage-considerations#trigger-on-a-blob-container).

## Clean up resources

Other quickstarts in this collection build upon this quickstart. If you plan to work with subsequent quickstarts, tutorials, or with any of the services you've created in this quickstart, don't clean up the resources.

*Resources* in Azure refer to function apps, functions, storage accounts, and so forth. They're grouped into *resource groups*, and you can delete everything in a group by deleting the group.

You've created resources to complete these quickstarts. You might be billed for these resources, depending on your [account status](https://azure.microsoft.com/account/) and [service pricing](https://azure.microsoft.com/pricing/). If you don't need the resources anymore, here's how to delete them:

In the Azure portal, go to the

**Resource group**page.To get to that page from the function app page, select the

**Overview**tab, and then select the link under**Resource group**.To get to that page from the dashboard, select

**Resource groups**, and then select the resource group that you used for this article.In the

**Resource group**page, review the list of included resources, and verify that they're the ones you want to delete.Select

**Delete resource group**and follow the instructions.Deletion might take a couple of minutes. When it's done, a notification appears for a few seconds. You can also select the bell icon at the top of the page to view the notification.


## Next steps

You have created a function that runs when a blob is added to or updated in Blob storage. For more information about Blob storage triggers, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob).

Now that you've created your first function, let's add an output binding to the function that writes a message to a Storage queue.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-mcp -->

# Model Context Protocol bindings for Azure Functions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The [Model Context Protocol (MCP)](https://github.com/modelcontextprotocol) is a client-server protocol intended to enable language models and agents to more efficiently discover and use external data sources and tools.

The Azure Functions MCP extension allows you to use Azure Functions to create remote MCP servers. These servers can host MCP tool trigger functions, which MCP clients, such as language models and agents, can query and access to do specific tasks.

| Action | Type |
|---|---|
| Run a function from an MCP tool call request |
|

Important

The MCP extension doesn't currently support PowerShell apps.

## Prerequisites

- When you use the SSE transport, the MCP extension relies on Azure Queue storage provided by the
[default host storage account](storage-considerations)(`AzureWebJobsStorage`

). When using identity-based connections, make sure that your function app has at least the equivalent of these role-based permissions in the host storage account:[Storage Queue Data Reader](/en-us/azure/role-based-access-control/built-in-roles#storage-queue-data-reader)and[Storage Queue Data Message Processor](/en-us/azure/role-based-access-control/built-in-roles#storage-queue-data-message-processor). - When running locally, the MCP extension requires version 4.0.7030 of the
[Azure Functions Core Tools](functions-run-local), or a later version.

- Requires version 2.1.0 or later of the
`Microsoft.Azure.Functions.Worker`

package. - Requires version 2.0.2 or later of the
`Microsoft.Azure.Functions.Worker.Sdk`

package.

## Install extension

Note

For C#, the Azure Functions MCP extension supports only the [isolated worker model](dotnet-isolated-process-guide).

Add the extension to your project by installing this [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Mcp) in your preferred way:

`Microsoft.Azure.Functions.Worker.Extensions.Mcp`


- Requires version 3.2.2 or later of the
.`azure-functions-java-library`

dependency - Requires version 1.40.0 or later of the
.`azure-functions-maven-plugin`

dependency

- Requires version 4.9.0 or later of the
`@azure/functions`

dependency

- Requires version 1.24.0 or later of the
.`azure-functions`

package

## Install bundle

To be able to use this binding extension in your app, make sure that the *host.json* file in the root of your project contains this `extensionBundle`

reference:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.0.0, 5.0.0)"
}
}
```


In this example, the `version`

value of `[4.0.0, 5.0.0)`

instructs the Functions host to use a bundle version that is at least `4.0.0`

but less than `5.0.0`

, which includes all potential versions of 4.x. This notation effectively maintains your app on the latest available minor version of the v4.x extension bundle.

When possible, you should use the latest extension bundle major version and allow the runtime to automatically maintain the latest minor version. You can view the contents of the latest bundle on the [extension bundles release page](https://github.com/Azure/azure-functions-extension-bundles/releases/latest). For more information, see [Azure Functions extension bundles](extension-bundles).

## host.json settings

This section describes the configuration settings available for this binding in version 2.x and later. Settings in the host.json file apply to all functions in a function app instance. For more information about function app configuration settings, see [host.json reference for Azure Functions](functions-host-json).

You can use the `extensions.mcp`

section in `host.json`

to define MCP server information.

```
{
"version": "2.0",
"extensions": {
"mcp": {
"instructions": "Some test instructions on how to use the server",
"serverName": "TestServer",
"serverVersion": "2.0.0",
"encryptClientState": true,
"messageOptions": {
"useAbsoluteUriForEndpoint": false
},
"system": {
"webhookAuthorizationLevel": "System"
}
}
}
}
```


| Property | Description |
|---|---|
instructions |
Describes to clients how to access the remote MCP server. |
serverName |
A friendly name for the remote MCP server. |
serverVersion |
Current version of the remote MCP server. |
encryptClientState |
Determines if client state is encrypted. Defaults to true. Setting to false may be useful for debugging and test scenarios but isn't recommended for production. |
messageOptions |
Options object for the message endpoint in the SSE transport. |
messageOptions.UseAbsoluteUriForEndpoint |
Defaults to `false` . Only applicable to the server-sent events (SSE) transport; this setting doesn't affect the Streamable HTTP transport. If set to `false` , the message endpoint is provided as a relative URI during initial connections over the SSE transport. If set to `true` , the message endpoint is returned as an absolute URI. Using a relative URI isn't recommended unless you have a specific reason to do so. |
system |
Options object for system-level configuration. |
system.webhookAuthorizationLevel |
Defines the authorization level required for the webhook endpoint. Defaults to "System". Allowed values are "System" and "Anonymous". When you set the value to "Anonymous", an access key is no longer required for requests. Regardless of if a key is required or not, you can use
|

## Connect to your MCP server

To connect to the MCP server exposed by your function app, you need to provide an MCP client with the appropriate endpoint and transport information. The following table shows the transports supported by the Azure Functions MCP extension, along with their corresponding connection endpoint.

| Transport | Endpoint |
|---|---|
| Streamable HTTP | `/runtime/webhooks/mcp` |
Server-Sent Events (SSE)1 |
`/runtime/webhooks/mcp/sse` |

1 Newer protocol versions deprecated the Server-Sent Events transport. Unless your client specifically requires it, you should use the Streamable HTTP transport instead.

When hosted in Azure, by default, the endpoints exposed by the extension also require the [system key](function-keys-how-to) named `mcp_extension`

. If it isn't provided in the `x-functions-key`

HTTP header or in the `code`

query string parameter, your client receives a `401 Unauthorized`

response. You can remove this requirement by setting the `system.webhookAuthorizationLevel`

property in `host.json`

to `Anonymous`

. For more information, see the [host.json settings](#hostjson-settings) section.

You can retrieve the key using any of the methods described in [Get your function access keys](function-keys-how-to#get-your-function-access-keys). The following example shows how to get the key with the Azure CLI:

```
az functionapp keys list --resource-group <RESOURCE_GROUP> --name <APP_NAME> --query systemKeys.mcp_extension --output tsv
```


MCP clients accept this configuration in various ways. Consult the documentation for your chosen client. The following example shows an `mcp.json`

file like you might use to [configure MCP servers for GitHub Copilot in Visual Studio Code](https://code.visualstudio.com/docs/copilot/customization/mcp-servers#_configuration-format). The example sets up two servers, both using the Streamable HTTP transport. The first is for local testing with the Azure Functions Core Tools. The second is for a function app hosted in Azure. The configuration takes input parameters for which Visual Studio Code prompts you when you first run the remote server. Using inputs ensures that secrets like the system key aren't saved to the file and checked into source control.

```
{
"inputs": [
{
"type": "promptString",
"id": "functions-mcp-extension-system-key",
"description": "Azure Functions MCP Extension System Key",
"password": true
},
{
"type": "promptString",
"id": "functionapp-host",
"description": "The host domain of the function app."
}
],
"servers": {
"local-mcp-function": {
"type": "http",
"url": "http://localhost:7071/runtime/webhooks/mcp"
},
"remote-mcp-function": {
"type": "http",
"url": "https://${input:functionapp-host}/runtime/webhooks/mcp",
"headers": {
"x-functions-key": "${input:functions-mcp-extension-system-key}"
}
}
}
}
```
