---
merged_at: 2026-01-26T23:29:57.729369
merged_files: 2
---


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
