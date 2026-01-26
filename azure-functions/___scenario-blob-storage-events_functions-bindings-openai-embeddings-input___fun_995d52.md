---
merged_at: 2026-01-26T21:02:36.325488
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _scenario-blob-storage-events_functions-bindings-openai-embeddings-input.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: scenario-blob-storage-events.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/scenario-blob-storage-events -->

# Quickstart: Respond to blob storage events by using Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you use Visual Studio Code to build an app that responds to events in a Blob Storage container. After testing the code locally by using an emulator, you deploy it to a new serverless function app running in a Flex Consumption plan in Azure Functions.

The project uses the Azure Developer CLI (`azd`

) extension with Visual Studio Code to simplify initializing and verifying your project code locally, as well as deploying your code to Azure. This deployment follows current best practices for secure and scalable Azure Functions deployments.

This article supports version 4 of the Node.js programming model for Azure Functions.

This article supports version 2 of the Python programming model for Azure Functions.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code. This extension requires[Azure Functions Core Tools](functions-run-local). When this tool isn't available locally, the extension tries to install it by using a package-based installer. You can also install or update the Core Tools package by running`Azure Functions: Install or Update Azure Functions Core Tools`

from the command palette. If you don't have npm or Homebrew installed on your local computer, you must instead[manually install or update Core Tools](functions-run-local#install-the-azure-functions-core-tools).

[C# extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)for Visual Studio Code.

The

[Java Development Kit](/en-us/azure/developer/java/fundamentals/java-support-on-azure), version 8, 11, 17 or 21 (Linux).[Apache Maven](https://maven.apache.org), version 3.0 or above.

[Node.js 18.x](https://nodejs.org/en/about/previous-releases)or above. Use the`node --version`

command to check your version.

Python versions that are

[supported by Azure Functions](supported-languages#languages-by-runtime-version). For more information, see[How to install Python](https://wiki.python.org/moin/BeginnersGuide/Download).The

[Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)for Visual Studio Code.

- The
[Azure Developer CLI extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.azure-dev)for Visual Studio Code.

[REST Client extension](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)or an equivalent REST tool you use to securely execute HTTP requests.

## Initialize the project

Use the `azd init`

command from the command palette to create a local Azure Functions code project from a template.

In Visual Studio Code, open a folder or workspace where you want to create your project.

Press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Initialize App (init)`

, then choose**Select a template**.There might be a slight delay while

`azd`

initializes the current folder or workspace.

When prompted, choose

**Select a template**, then search for and select`Azure Functions C# Event Grid Blob Trigger using Azure Developer CLI`

.When prompted in the terminal, enter a unique environment name, such as

`blobevents-dotnet`

.This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-eventgrid-blob)and initializes the project in the current folder or workspace.

When prompted, choose

**Select a template**, then search for and select`Azure Functions Python Event Grid Blob Trigger using Azure Developer CLI`

.When prompted in the terminal, enter a unique environment name, such as

`blobevents-python`

.This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-python-azd-eventgrid-blob)and initializes the project in the current folder or workspace.

When prompted, choose

**Select a template**, then search for and select`Azure Functions TypeScript Event Grid Blob Trigger using Azure Developer CLI`

.When prompted, enter a unique environment name, such as

`blobevents-typescript`

.This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-eventgrid-blob)and initializes the project in the current folder or workspace.

When prompted, choose

**Select a template**, then search for and select`Azure Functions Java Event Grid Blob Trigger using Azure Developer CLI`

.When prompted, enter a unique environment name, such as

`blobevents-java`

.This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-java-azd-eventgrid-blob)and initializes the project in the current folder or workspace.

When prompted, choose

**Select a template**, then search for and select`Azure Functions PowerShell Event Grid Blob Trigger using Azure Developer CLI`

.When prompted, enter a unique environment name, such as

`blobevents-powershell`

.This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-powershell-azd-eventgrid-blob)and initializes the project in the current folder or workspace.

In `azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also part of the name of the resource group you create in Azure.

## Add the local.settings.json file

Functions needs the local.settings.json file to configure the host when running locally.

Run this command to go to the

`src`

app folder:`cd src`


Create a file named

*local.settings.json*in the`src`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "dotnet-isolated", "PDFProcessorSTORAGE": "UseDevelopmentStorage=true" } }`


Create a file named

*local.settings.json*in the`src`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "java", "PDFProcessorSTORAGE": "UseDevelopmentStorage=true" } }`


Create a file named

*local.settings.json*in the`src`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "node", "PDFProcessorSTORAGE": "UseDevelopmentStorage=true" } }`


Create a file named

*local.settings.json*in the`src`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "powershell", "FUNCTIONS_WORKER_RUNTIME_VERSION": "7.2", "PDFProcessorSTORAGE": "UseDevelopmentStorage=true" } }`


Create a file named

*local.settings.json*in the`src`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "python", "PDFProcessorSTORAGE": "UseDevelopmentStorage=true" } }`


## Create and activate a virtual environment

In the `src`

folder, run these commands to create and activate a virtual environment named `.venv`

:

```
python3 -m venv .venv
source .venv/bin/activate
```


If Python doesn't install the venv package on your Linux distribution, run the following command:

```
sudo apt-get install python3-venv
```


## Set up local storage emulator

Use the Azurite emulator to run your code project locally before creating and using Azure resources.

If you haven't already,

[install Azurite](/en-us/azure/storage/common/storage-use-azurite#install-azurite).Press

`F1`. In the command palette, search for and run the command`Azurite: Start`

to start the local storage emulator.In the

**Azure**area, expand**Workspace**>**Attached Storage Accounts**>**Local Emulator**, right-click (Ctrl-click on Mac)**Blob Containers**, select**Create Blob Container...**, and create these two blob storage containers in the local emulator:`unprocessed-pdf`

: container that the trigger monitors for storage events.`processed-pdf`

: container where the function sends processed blobs as output.

Expand

**Blob Containers**, right-click (Ctrl-click on Mac)**unprocessed-pdf**, select**Upload Files...**, press`Enter`to accept the root directory, and upload the PDF files from the`data`

project folder.

When running locally, you can use REST to trigger the function by simulating the function receiving a message from an event subscription.

## Run the function locally

Visual Studio Code integrates with [Azure Functions Core tools](functions-run-local) to let you run this project on your local development computer by using the Azurite emulator. The `PDFProcessorSTORAGE`

environment variable defines the storage account connection, which is also set to `"UseDevelopmentStorage=true"`

in the local.settings.json file when running locally.

Run this command from the

`src`

project folder in a terminal or command prompt:`func start`

`mvn clean package mvn azure-functions:run`

`npm install func start`

`npm install npm start`

When the Functions host starts, it writes the name of the trigger and the trigger type to the terminal output. In Functions, the project root folder contains the host.json file.

With Core Tools still running in

**Terminal**, open the`test.http`

file in your project and select**Send Request**to trigger the`ProcessBlobUpload`

function by sending a test blob event to the blob event webhook.This step simulates receiving an event from an event subscription when running locally, and you should see the request and processed file information written in the logs. If you aren't using

*REST Client*, you must use another secure REST tool to call the endpoint with the payload in`test.http`

.In the Workspace area for the blob container, expand

**processed-pdf**and verify that the function processed the PDF file and copied it with a`processed-`

prefix.When you're done, press Ctrl+C in the terminal window to stop the

`func.exe`

host process.

## Review the code (optional)

You can review the code that defines the Event Grid blob trigger in the [ProcessBlobUpload.cs project file](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-eventgrid-blob/blob/main/src/ProcessBlobUpload.cs). The function demonstrates how to:

- Use
`BlobTrigger`

with`Source = BlobTriggerSource.EventGrid`

for near real-time processing - Bind to
`BlobClient`

for the source blob and`BlobContainerClient`

for the destination - Process blob content and copy it to another container by using streams

You can review the code that defines the Event Grid blob trigger in the [function_app.py project file](https://github.com/Azure-Samples/functions-quickstart-python-azd-eventgrid-blob/blob/main/src/function_app.py). The function demonstrates how to:

- Use
`@app.blob_trigger`

with`source="EventGrid"`

for near real-time processing - Access blob content using the
`InputStream`

parameter - Copy processed files to the destination container using the Azure Storage SDK

You can review the code that defines the Event Grid blob trigger in the [processBlobUpload.ts project file](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-eventgrid-blob/blob/main/src/functions/processBlobUpload.ts). The function demonstrates how to:

- Use
`app.storageBlob()`

with`source: 'EventGrid'`

for near real-time processing - Access blob content using the Node.js Azure Storage SDK
- Process and copy files to the destination container asynchronously

You can review the code that defines the Event Grid blob trigger in the [ProcessBlobUpload.java project file](https://github.com/Azure-Samples/functions-quickstart-java-azd-eventgrid-blob/blob/main/src/src/main/java/com/microsoft/azure/samples/ProcessBlobUpload.java). The function demonstrates how to:

- Use
`@BlobTrigger`

with`source = "EventGrid"`

for near real-time processing - Access blob content using
`BlobInputStream`

parameter - Copy processed files to the destination container using Azure Storage SDK for Java

You can review the code that defines the Event Grid blob trigger in the [ProcessBlobUpload/run.ps1 project file](https://github.com/Azure-Samples/functions-quickstart-powershell-azd-eventgrid-blob/blob/main/src/processBlobUpload/run.ps1) and the corresponding [function.json](https://github.com/Azure-Samples/functions-quickstart-powershell-azd-eventgrid-blob/blob/main/src/processBlobUpload/function.json). The function demonstrates how to:

- Configure blob trigger with
`"source": "EventGrid"`

in function.json for near real-time processing - Access blob content using PowerShell Azure Storage cmdlets
- Process and copy files to the destination container using Azure PowerShell modules

After you review and verify your function code locally, it's time to publish the project to Azure.

## Create Azure resources and deploy

Use the `azd up`

command to create the function app in a Flex Consumption plan along with other required Azure resources, including the event subscription. After the infrastructure is ready, `azd`

also deploys your project code to the new function app in Azure.

In Visual Studio Code, press

`F1`to open the command palette. Search for and run the command`Azure Developer CLI (azd): Sign In with Azure Developer CLI`

, then sign in by using your Azure account.In the project root, press

`F1`to open the command palette. Search for and run the command`Azure Developer CLI (azd): Provision and Deploy (up)`

to create the required Azure resources and deploy your code.When prompted in the Terminal window, provide these required deployment parameters:

Prompt Description Select an Azure Subscription to use Choose the subscription in which you want to create your resources. *Environment name*An environment that's used to maintain a unique deployment context for your app. *Azure location*Azure region in which to create the resource group that contains the new Azure resources. Only regions that currently support the Flex Consumption plan are shown. The

`azd up`

command uses your responses to these prompts with the Bicep configuration files to create and configure these required Azure resources, following the latest best practices:- Flex Consumption plan and function app
- Azure Storage account with blob containers
- Application Insights (recommended)
- Access policies and roles for your account
- Event Grid subscription for blob events
- Service-to-service connections by using managed identities (instead of stored connection strings)

After the command completes successfully, your app runs in Azure with an event subscription configured to trigger your function when blobs are added to the

`unprocessed-pdf`

container.Make a note of the

`AZURE_STORAGE_ACCOUNT_NAME`

and`AZURE_FUNCTION_APP_NAME`

in the output. These names are unique for your storage account and function app in Azure, respectively.

## Verify the deployed function

In Visual Studio Code, press

`F1`. In the command palette, search for and run the command`Azure Storage: Upload Files...`

. Accept the root directory, and as before, upload one or more PDF files from the`data`

project folder.When prompted, select the name of your new storage account (from

`AZURE_STORAGE_ACCOUNT_NAME`

). Select**Blob Containers**>**unprocessed-pdf**.Press

`F1`. In the command palette, search for and run the command`Azure Storage: Open in Explorer`

. Select the same storage account >**Blob Containers**>**processed-pdf**, then**Open in new window**.In the Explorer, verify that the PDF files you uploaded were processed by your function. The output is written to the

`processed-pdf`

container with a`processed-`

prefix.

The Event Grid blob trigger processes files within seconds of upload. This speed demonstrates the near real-time capabilities of this approach compared to traditional polling-based blob triggers.

## Redeploy your code

Run the `azd up`

command as many times as you need to both provision your Azure resources and deploy code updates to your function app.

Note

Deployed code files are always overwritten by the latest deployment package.

Your initial responses to `azd`

prompts and any environment variables generated by `azd`

are stored locally in your named environment. Use the `azd env get-values`

command to review all of the variables in your environment that were used when creating Azure resources.

## Clean up resources

When you're done working with your function app and related resources, use this command to delete the function app and its related resources from Azure. This action helps you avoid incurring any further costs:

```
azd down --no-prompt
```


Note

The `--no-prompt`

option instructs `azd`

to delete your resource group without a confirmation from you.

This command doesn't affect your local code project.


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-openai-embeddings-input.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai-embeddings-input -->

# Azure OpenAI embeddings input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Azure OpenAI extension for Azure Functions is currently in preview.

The Azure OpenAI embeddings input binding allows you to generate embeddings for inputs. The binding can generate embeddings from files or raw text inputs.

For information on setup and configuration details of the Azure OpenAI extension, see [Azure OpenAI extensions for Azure Functions](functions-bindings-openai). To learn more about embeddings in Azure OpenAI Service, see [Understand embeddings in Azure OpenAI Service](/en-us/azure/ai-services/openai/concepts/understand-embeddings).

Note

References and examples are only provided for the [Node.js v4 model](functions-reference-node?pivots=nodejs-model-v4).

Note

References and examples are only provided for the [Python v2 model](functions-reference-python?pivots=python-mode-decorators#programming-model).

Note

While both C# process models are supported, only [isolated worker model](dotnet-isolated-process-guide) examples are provided.

## Example

This example shows how to generate embeddings for a raw text string.

```
internal class EmbeddingsRequest
{
[JsonPropertyName("rawText")]
public string? RawText { get; set; }
[JsonPropertyName("filePath")]
public string? FilePath { get; set; }
[JsonPropertyName("url")]
public string? Url { get; set; }
}
/// <summary>
/// Example showing how to use the <see cref="EmbeddingsAttribute"/> input binding to generate embeddings
/// for a raw text string.
/// </summary>
[Function(nameof(GenerateEmbeddings_Http_RequestAsync))]
public async Task GenerateEmbeddings_Http_RequestAsync(
[HttpTrigger(AuthorizationLevel.Function, "post", Route = "embeddings")] HttpRequestData req,
[EmbeddingsInput("{rawText}", InputType.RawText, EmbeddingsModel = "%EMBEDDING_MODEL_DEPLOYMENT_NAME%")] EmbeddingsContext embeddings)
{
using StreamReader reader = new(req.Body);
string request = await reader.ReadToEndAsync();
EmbeddingsRequest? requestBody = JsonSerializer.Deserialize<EmbeddingsRequest>(request);
this.logger.LogInformation(
"Received {count} embedding(s) for input text containing {length} characters.",
embeddings.Count,
requestBody?.RawText?.Length);
// TODO: Store the embeddings into a database or other storage.
}
```


This example shows how to retrieve embeddings stored at a specified file that is accessible to the function.

```
[Function(nameof(GetEmbeddings_Http_FilePath))]
public async Task GetEmbeddings_Http_FilePath(
[HttpTrigger(AuthorizationLevel.Function, "post", Route = "embeddings-from-file")] HttpRequestData req,
[EmbeddingsInput("{filePath}", InputType.FilePath, MaxChunkLength = 512, EmbeddingsModel = "%EMBEDDING_MODEL_DEPLOYMENT_NAME%")] EmbeddingsContext embeddings)
{
using StreamReader reader = new(req.Body);
string request = await reader.ReadToEndAsync();
EmbeddingsRequest? requestBody = JsonSerializer.Deserialize<EmbeddingsRequest>(request);
this.logger.LogInformation(
"Received {count} embedding(s) for input file '{path}'.",
embeddings.Count,
requestBody?.FilePath);
// TODO: Store the embeddings into a database or other storage.
}
```


This example shows how to generate embeddings for a raw text string.

```
@FunctionName("GenerateEmbeddingsHttpRequest")
public HttpResponseMessage generateEmbeddingsHttpRequest(
@HttpTrigger(
name = "req",
methods = {HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "embeddings")
HttpRequestMessage<EmbeddingsRequest> request,
@EmbeddingsInput(name = "Embeddings", input = "{RawText}", inputType = InputType.RawText, embeddingsModel = "%EMBEDDING_MODEL_DEPLOYMENT_NAME%") String embeddingsContext,
final ExecutionContext context) {
if (request.getBody() == null)
{
throw new IllegalArgumentException(
"Invalid request body. Make sure that you pass in {\"rawText\": value } as the request body.");
}
JSONObject embeddingsContextJsonObject = new JSONObject(embeddingsContext);
context.getLogger().info(String.format("Received %d embedding(s) for input text containing %s characters.",
embeddingsContextJsonObject.get("count"),
request.getBody().getRawText().length()));
// TODO: Store the embeddings into a database or other storage.
return request.createResponseBuilder(HttpStatus.ACCEPTED)
.header("Content-Type", "application/json")
.build();
}
```


This example shows how to retrieve embeddings stored at a specified file that is accessible to the function.

```
@FunctionName("GenerateEmbeddingsHttpFilePath")
public HttpResponseMessage generateEmbeddingsHttpFilePath(
@HttpTrigger(
name = "req",
methods = {HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "embeddings-from-file")
HttpRequestMessage<EmbeddingsRequest> request,
@EmbeddingsInput(name = "Embeddings", input = "{FilePath}", inputType = InputType.FilePath, maxChunkLength = 512, embeddingsModel = "%EMBEDDING_MODEL_DEPLOYMENT_NAME%") String embeddingsContext,
final ExecutionContext context) {
if (request.getBody() == null)
{
throw new IllegalArgumentException(
"Invalid request body. Make sure that you pass in {\"filePath\": value } as the request body.");
}
JSONObject embeddingsContextJsonObject = new JSONObject(embeddingsContext);
context.getLogger().info(String.format("Received %d embedding(s) for input file %s.",
embeddingsContextJsonObject.get("count"),
request.getBody().getFilePath()));
// TODO: Store the embeddings into a database or other storage.
return request.createResponseBuilder(HttpStatus.ACCEPTED)
.header("Content-Type", "application/json")
.build();
}
```


This example shows how to generate embeddings for a raw text string.

```
const embeddingsHttpInput = input.generic({
input: '{rawText}',
inputType: 'RawText',
type: 'embeddings',
embeddingsModel: '%EMBEDDING_MODEL_DEPLOYMENT_NAME%'
})
app.http('generateEmbeddings', {
methods: ['POST'],
route: 'embeddings',
authLevel: 'function',
extraInputs: [embeddingsHttpInput],
handler: async (request, context) => {
let requestBody = await request.json();
let response = context.extraInputs.get(embeddingsHttpInput);
context.log(
`Received ${response.count} embedding(s) for input text containing ${requestBody.RawText.length} characters.`
);
// TODO: Store the embeddings into a database or other storage.
return {status: 202}
}
});
```


```
interface EmbeddingsHttpRequest {
RawText?: string;
}
const embeddingsHttpInput = input.generic({
input: '{rawText}',
inputType: 'RawText',
type: 'embeddings',
embeddingsModel: '%EMBEDDING_MODEL_DEPLOYMENT_NAME%'
})
app.http('generateEmbeddings', {
methods: ['POST'],
route: 'embeddings',
authLevel: 'function',
extraInputs: [embeddingsHttpInput],
handler: async (request, context) => {
let requestBody: EmbeddingsHttpRequest = await request.json();
let response: any = context.extraInputs.get(embeddingsHttpInput);
context.log(
`Received ${response.count} embedding(s) for input text containing ${requestBody.RawText.length} characters.`
);
// TODO: Store the embeddings into a database or other storage.
return {status: 202}
}
});
```


This example shows how to generate embeddings for a raw text string.

```
const embeddingsFilePathInput = input.generic({
input: '{filePath}',
inputType: 'FilePath',
type: 'embeddings',
maxChunkLength: 512,
embeddingsModel: '%EMBEDDING_MODEL_DEPLOYMENT_NAME%'
})
app.http('getEmbeddingsFilePath', {
methods: ['POST'],
route: 'embeddings-from-file',
authLevel: 'function',
extraInputs: [embeddingsFilePathInput],
handler: async (request, context) => {
let requestBody = await request.json();
let response = context.extraInputs.get(embeddingsFilePathInput);
context.log(
`Received ${response.count} embedding(s) for input file ${requestBody.FilePath}.`
);
// TODO: Store the embeddings into a database or other storage.
return {status: 202}
}
});
```


```
interface EmbeddingsFilePath {
FilePath?: string;
}
const embeddingsFilePathInput = input.generic({
input: '{filePath}',
inputType: 'FilePath',
type: 'embeddings',
maxChunkLength: 512,
embeddingsModel: '%EMBEDDING_MODEL_DEPLOYMENT_NAME%'
})
app.http('getEmbeddingsFilePath', {
methods: ['POST'],
route: 'embeddings-from-file',
authLevel: 'function',
extraInputs: [embeddingsFilePathInput],
handler: async (request, context) => {
let requestBody: EmbeddingsFilePath = await request.json();
let response: any = context.extraInputs.get(embeddingsFilePathInput);
context.log(
`Received ${response.count} embedding(s) for input file ${requestBody.FilePath}.`
);
// TODO: Store the embeddings into a database or other storage.
return {status: 202}
}
});
```


This example shows how to generate embeddings for a raw text string.

Here's the *function.json* file for generating the embeddings:

```
{
"bindings": [
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "Request",
"route": "embeddings",
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
"name": "Embeddings",
"type": "embeddings",
"direction": "in",
"inputType": "RawText",
"input": "{rawText}",
"embeddingsModel": "%EMBEDDING_MODEL_DEPLOYMENT_NAME%"
}
]
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

```
using namespace System.Net
param($Request, $TriggerMetadata, $Embeddings)
$input = $Request.Body.RawText
Write-Host "Received $($Embeddings.Count) embedding(s) for input text containing $($input.Length) characters."
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::Accepted
})
```


This example shows how to generate embeddings for a raw text string.

```
@app.function_name("GenerateEmbeddingsHttpRequest")
@app.route(route="embeddings", methods=["POST"])
@app.embeddings_input(
arg_name="embeddings",
input="{rawText}",
input_type="rawText",
embeddings_model="%EMBEDDING_MODEL_DEPLOYMENT_NAME%",
)
def generate_embeddings_http_request(
req: func.HttpRequest, embeddings: str
) -> func.HttpResponse:
user_message = req.get_json()
embeddings_json = json.loads(embeddings)
embeddings_request = {"raw_text": user_message.get("rawText")}
logging.info(
f'Received {embeddings_json.get("count")} embedding(s) for input text '
f'containing {len(embeddings_request.get("raw_text"))} characters.'
)
# TODO: Store the embeddings into a database or other storage.
return func.HttpResponse(status_code=200)
```


## Attributes

Apply the `EmbeddingsInput`

attribute to define an embeddings input binding, which supports these parameters:

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

## Annotations

The `EmbeddingsInput`

annotation enables you to define an embeddings input binding, which supports these parameters:

| Element | Description |
|---|---|
name |
Gets or sets the name of the input binding. |
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

## Decorators

During the preview, define the input binding as a `generic_input_binding`

binding of type `embeddings`

, which supports these parameters: `embeddings`

decorator supports these parameters:

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

## Configuration

The binding supports these configuration properties that you set in the function.json file.

| Property | Description |
|---|---|
type |
Must be `EmbeddingsInput` . |
direction |
Must be `in` . |
name |
The name of the input binding. |
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

See the [Example section](#example) for complete examples.

## Usage

Changing the default embeddings `model`

changes the way that embeddings are stored in the vector database. Changing the default model can cause the lookups to start misbehaving when they don't match the rest of the data that was previously ingested into the vector database. The default model for embeddings is `text-embedding-ada-002`

.

When calculating the maximum character length for input chunks, consider that the maximum input tokens allowed for second-generation input embedding models like `text-embedding-ada-002`

is `8191`

. A single token is approximately four characters in length (in English), which translates to roughly 32,000 (English) characters of input that can fit into a single chunk.


---

<!-- DOCUMENTO FUSIONADO: __functions-compare-logic-apps-ms-flow-webjobs_functions-bindings-cache-input_fu_58b915.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-compare-logic-apps-ms-flow-webjobs_functions-bindings-cache-input.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-compare-logic-apps-ms-flow-webjobs.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-compare-logic-apps-ms-flow-webjobs -->

# Choose the right integration and automation services in Azure

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article compares the following Microsoft cloud services:

[Microsoft Power Automate](https://make.powerautomate.com/)(was Microsoft Flow)[Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/)[Azure Functions](https://azure.microsoft.com/services/functions/)[Azure App Service WebJobs](../app-service/webjobs-create)

All of these services can solve integration problems and automate business processes. They can all define input, actions, conditions, and output. You can run each of them on a schedule or trigger. Each service has unique advantages, and this article explains the differences.

Note

If you're looking for a more general comparison between Azure Functions and other Azure compute options, see the following articles:

For a summary and comparison of automation service options in Azure,
see [Choose the Automation services in Azure](../automation/automation-services).

## Compare Azure Logic Apps and Microsoft Power Automate

These services are both *designer-first* integration platforms where you can build and run automated workflows. Both platforms integrate with various Software-as-a-Service (SaaS) and enterprise applications. Both provide similar workflow designers, and while [their connectors share some overlap](/en-us/connectors/connector-reference/), each platform also offers their own unique connectors.

Power Automate empowers business users, office workers, and citizen developers to build simple integrations without having to work with IT or developers or to write code. One example might be an approval workflow for a SharePoint document library. Azure Logic Apps supports integrations ranging from little-to-no-code scenarios to more advanced, codeful, and complex workflows. Examples include B2B processes or scenarios that require enterprise-level interactions with Azure DevOps. A business workflow can also grow from simple to complete over time.

To help you determine whether you want to use Azure Logic Apps or Power Automate for a specific integration, see the [Capability comparison table](/en-us/azure/logic-apps/power-automate-migration#compare-capability-details).

## Compare Azure Functions and Azure Logic Apps

These Azure services enable you to build and run serverless workloads. Azure Functions is a serverless compute service, while Azure Logic Apps is a serverless workflow integration platform. Both can create complex *orchestrations*. An orchestration is a collection of functions, which are called *actions* in Azure Logic Apps, that you can run to complete a complex task. For example, to process a batch of orders, you might execute many instances of a function in parallel, wait for all instances to finish, and then execute a function that computes a result on the aggregate.

For Azure Functions, you develop orchestrations by writing code and using the [Durable Functions extension](durable/durable-functions-overview). For Azure Logic Apps, you create orchestrations by using a visual designer or by editing Azure Resource Manager templates.

You can mix and match services when you build an orchestration. For example, you can call functions from logic app workflows and call logic app workflows from functions. Choose how to build each orchestration based on the services' capabilities or your personal preference. The following table lists some key differences between these services:

## Compare Functions and WebJobs

Like Azure Functions, Azure App Service WebJobs with the WebJobs SDK is a *code-first* integration service that is designed for developers. Both are built on [Azure App Service](../app-service/overview) and support features such as [source control integration](../app-service/deploy-continuous-deployment), [authentication](../app-service/overview-authentication-authorization), and [monitoring with Application Insights integration](functions-monitoring).

### WebJobs and the WebJobs SDK

You can use the *WebJobs* feature of App Service to run a script or code in the context of an App Service web app. The *WebJobs SDK* is a framework designed for WebJobs that simplifies the code you write to respond to events in Azure services. For example, you might respond to the creation of an image blob in Azure Storage by creating a thumbnail image. The WebJobs SDK runs as a .NET console application, which you can deploy to a WebJob.

WebJobs and the WebJobs SDK work best together, but you can use WebJobs without the WebJobs SDK and vice versa. A WebJob can run any program or script that runs in the App Service sandbox. A WebJobs SDK console application can run anywhere console applications run, such as on-premises servers.

### Comparison table

Azure Functions is built on the WebJobs SDK, so it shares many of the same event triggers and connections to other Azure services. Here are some factors to consider when you're choosing between Azure Functions and WebJobs with the WebJobs SDK:

| Functions | WebJobs with WebJobs SDK | |
|---|---|---|
|
✔ | |
|
✔ | |
|
✔ | |
|
✔ | |
Trigger events |
|

[Timer](functions-bindings-timer)[Azure Storage queues and blobs](functions-bindings-storage-blob)[Azure Service Bus queues and topics](functions-bindings-service-bus)[Azure Cosmos DB](functions-bindings-cosmosdb)[Azure Event Hubs](functions-bindings-event-hubs)[File system](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Files/FileTriggerAttribute.cs)**Supported languages**F#

JavaScript

Java

Python

PowerShell

1**Package managers**21 WebJobs (without the WebJobs SDK) supports languages such as C#, Java, JavaScript, Bash, .cmd, .bat, PowerShell, PHP, TypeScript, Python, and more. A WebJob can run any program or script that can run in the App Service sandbox.

2 WebJobs (without the WebJobs SDK) supports npm and NuGet.

### Summary

Azure Functions offers more developer productivity than Azure App Service WebJobs does. It also offers more options for programming languages, development environments, Azure service integration, and pricing. For most scenarios, it's the best choice.

Here are two scenarios for which WebJobs might be the best choice:

- You need more control over the code that listens for events, the
`JobHost`

object. Functions offers a limited number of ways to customize`JobHost`

behavior in the[host.json](functions-host-json)file. Sometimes you need to do things that you can't specify by using a string in a JSON file. For example, only the WebJobs SDK lets you configure a custom retry policy for Azure Storage. - You have an App Service app for which you want to run code snippets, and you want to manage them together in the same Azure DevOps environment.

For other scenarios where you want to run code snippets for integrating Azure or external services, choose Azure Functions over WebJobs with the WebJobs SDK.

## Power Automate, Logic Apps, Functions, and WebJobs together

You don't have to choose just one of these services. They integrate with each other and with external services.

A Power Automate flow can call an Azure Logic Apps workflow. An Azure Logic Apps workflow can call a function in Azure Functions, and vice versa. For example, see [Create a function that integrates with Azure Logic Apps](functions-twitter-email).

Between Power Automate, Azure Logic Apps, and Functions, the integration experience between these services continues to improve over time. You can build a component in one service and use that component in the other services.

For more information about integration services, see the following articles:

[Leveraging Azure Functions & Azure App Service for integration scenarios by Christopher Anderson](https://www.biztalk360.com/integrate-2016-resources/leveraging-azure-functions-azure-app-service-integration-scenarios/)[Integrations Made Simple by Charles Lamanna](https://www.biztalk360.com/integrate-2016-resources/integrations-made-simple/)[Azure Logic Apps Live webcast](https://aka.ms/logicappslive)[Power Automate frequently asked questions](/en-us/power-automate/frequently-asked-questions)

## Next steps

Get started by creating your first flow, logic app workflow, or function app. Select any of the following links:


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-cache-input.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache-input -->

# Azure Cache for Redis input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When a function runs, the Azure Cache for Redis input binding retrieves data from a cache and passes it to your function as an input parameter.

For information on setup and configuration details, see the [overview](functions-bindings-cache).

## Scope of availability for functions bindings

| Binding Type | Azure Managed Redis | Azure Cache for Redis |
|---|---|---|
| Input | Yes | Yes |

Important

When using Azure Managed Redis or the Enterprise tiers of Azure Cache for Redis, use port 10000 rather than port 6380 or 6379.

Important

The Node.js v4 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Important

The Python v2 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v2 model works, refer to the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

## Example

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

For .NET functions, using the *isolated worker* model is recommended over the *in-process* model. For a comparison of the *in-process* and *isolated worker* models, see differences between the *isolated worker* model and the *in-process* model for .NET on Azure Functions.

The following code uses the key from the pub/sub trigger to obtain and log the value from an input binding using a `GET`

command:

```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.Functions.Worker.Extensions.Redis.Samples.RedisInputBinding
{
public class SetGetter
{
private readonly ILogger<SetGetter> logger;
public SetGetter(ILogger<SetGetter> logger)
{
this.logger = logger;
}
[Function(nameof(SetGetter))]
public void Run(
[RedisPubSubTrigger(Common.connectionStringSetting, "__keyevent@0__:set")] string key,
[RedisInput(Common.connectionStringSetting, "GET {Message}")] string value)
{
logger.LogInformation($"Key '{key}' was set to value '{value}'");
}
}
}
```


More samples for the Azure Cache for Redis input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-redis-extension).

The following code uses the key from the pub/sub trigger to obtain and log the value from an input binding using a `GET`

command:

```
package com.function.RedisInputBinding;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.redis.annotation.*;
public class SetGetter {
@FunctionName("SetGetter")
public void run(
@RedisPubSubTrigger(
name = "key",
connection = "redisConnectionString",
channel = "__keyevent@0__:set")
String key,
@RedisInput(
name = "value",
connection = "redisConnectionString",
command = "GET {Message}")
String value,
final ExecutionContext context) {
context.getLogger().info("Key '" + key + "' was set to value '" + value + "'");
}
}
```


This function.json defines both a pub/sub trigger and an input binding to the GET message on an Azure Cache for Redis instance:

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "__keyevent@0__:set",
"name": "key",
"direction": "in"
},
{
"type": "redis",
"connection": "redisConnectionString",
"command": "GET {Message}",
"name": "value",
"direction": "in"
}
],
"scriptFile": "index.js"
}
```


This JavaScript code (from index.js) retrieves and logs the cached value related to the key provided by the pub/sub trigger.

```
module.exports = async function (context, key, value) {
context.log("Key '" + key + "' was set to value '" + value + "'");
}
```


This function.json defines both a pub/sub trigger and an input binding to the GET message on an Azure Cache for Redis instance:

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "__keyevent@0__:set",
"name": "key",
"direction": "in"
},
{
"type": "redis",
"connection": "redisConnectionString",
"command": "GET {Message}",
"name": "value",
"direction": "in"
}
],
"scriptFile": "run.ps1"
}
```


This PowerShell code (from run.ps1) retrieves and logs the cached value related to the key provided by the pub/sub trigger.

```
param($key, $value, $TriggerMetadata)
Write-Host "Key '$key' was set to value '$value'"
```


The following example uses a pub/sub trigger with an input binding to the GET message on an Azure Cache for Redis instance. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

This function.json defines both a pub/sub trigger and an input binding to the GET message on an Azure Cache for Redis instance:

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "__keyevent@0__:set",
"name": "key",
"direction": "in"
},
{
"type": "redis",
"connection": "redisConnectionString",
"command": "GET {Message}",
"name": "value",
"direction": "in"
}
]
}
```


This Python code (from __init__.py) retrieves and logs the cached value related to the key provided by the pub/sub trigger:

```
import logging
def main(key: str, value: str):
logging.info("Key '" + key + "' was set to value '" + value + "'")
```


The [configuration](#configuration) section explains these properties.

## Attributes

Note

Not all commands are supported for this binding. At the moment, only read commands that return a single output are supported. The full list can be found [here](https://github.com/Azure/azure-functions-redis-extension/blob/main/src/Microsoft.Azure.WebJobs.Extensions.Redis/Bindings/RedisAsyncConverter.cs#L63)

| Attribute property | Description |
|---|---|
`Connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`Command`

`GET key`

, `HGET key field`

.## Annotations

The `RedisInput`

annotation supports these properties:

| Property | Description |
|---|---|
`name` |
The name of the specific input binding. |
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`command`

`GET key`

or `HGET key field`

.## Configuration

The following table explains the binding configuration properties that you set in the function.json file.

| function.json property | Description |
|---|---|
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`command`

`GET key`

, `HGET key field`

.Note

Python v2 and Node.js v4 for Functions don't use function.json to define the function. Both of these new language versions aren't currently supported by Azure Redis Cache bindings.

See the [Example section](#example) for complete examples.

## Usage

The input binding expects to receive a string from the cache.

When you use a custom type as the binding parameter, the extension tries to deserialize a JSON-formatted string into the custom type of this parameter.

Important

For optimal security, your function app should use Microsoft Entra ID with managed identities to authorize requests against your cache, if possible. Authorization by using Microsoft Entra ID and managed identities provides superior security and ease of use over shared access key authorization. For more information about using managed identities with your cache, see [Use Microsoft Entra ID for cache authentication](/en-us/azure/azure-cache-for-redis/cache-azure-active-directory-for-authentication).


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-mcp-trigger.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-mcp-trigger -->

# MCP tool trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the MCP tool trigger to define tool endpoints in a [Model Content Protocol (MCP)](https://github.com/modelcontextprotocol) server. Client language models and agents can use tools to perform specific tasks, such as storing or accessing code snippets.

For information on setup and configuration details, see the [overview](functions-bindings-mcp).

## Example

Note

For C#, the Azure Functions MCP extension supports only the [isolated worker model](dotnet-isolated-process-guide).

This code creates an endpoint to expose a tool named `SaveSnippet`

that tries to persist a named code snippet to blob storage.

```
private const string BlobPath = "snippets/{mcptoolargs.snippetname}.json";
[Function(nameof(SaveSnippet))]
[BlobOutput(BlobPath)]
public string SaveSnippet(
[McpToolTrigger("save_snippet", "Saves a code snippet into your snippet collection.")]
ToolInvocationContext context,
[McpToolProperty("snippetname", "The name of the snippet.", isRequired: true)]
string name,
[McpToolProperty("snippet", "The code snippet.", isRequired: true)]
string snippet
)
{
return snippet;
}
```


This code creates an endpoint to expose a tool named `GetSnippet`

that tries to retrieve a code snippet by name from blob storage.

```
private const string BlobPath = "snippets/{mcptoolargs.snippetname}.json";
[Function(nameof(GetSnippet))]
public object GetSnippet(
[McpToolTrigger("get_snippets", "Gets code snippets from your snippet collection.")]
ToolInvocationContext context,
[BlobInput(BlobPath)] string snippetContent
)
{
return snippetContent;
}
```


The tool properties for the `GetSnippet`

function are configured in `Program.cs`

:

```
var builder = FunctionsApplication.CreateBuilder(args);
builder.ConfigureFunctionsWebApplication();
builder.Services
.AddApplicationInsightsTelemetryWorkerService()
.ConfigureFunctionsApplicationInsights();
builder
.ConfigureMcpTool("get_snippets")
.WithProperty("snippetname", "string", "The name of the snippet.", required: true);
builder.Build().Run();
```


Tip

The example above used literal strings for things like the name of the "get_snippets" tool in both `Program.cs`

and the function. Consider instead using shared constant strings to keep things in sync across your project.

For the complete code example, see [SnippetTool.cs](https://github.com/Azure-Samples/remote-mcp-functions-dotnet/blob/main/src/SnippetsTool.cs).

This code creates an endpoint to expose a tool named `SaveSnippets`

that tries to persist a named code snippet to blob storage.

```
@FunctionName("SaveSnippets")
@StorageAccount("AzureWebJobsStorage")
public String saveSnippet(
@McpToolTrigger(
name = "saveSnippets",
description = "Saves a text snippet to your snippets collection."
)
String mcpToolInvocationContext,
@McpToolProperty(
name = "snippetName",
propertyType = "string",
description = "The name of the snippet.",
required = true
)
String snippetName,
@McpToolProperty(
name = "snippet",
propertyType = "string",
description = "The content of the snippet.",
required = true
)
String snippet,
@BlobOutput(name = "outputBlob", path = "snippets/{mcptoolargs.snippetName}.json")
OutputBinding<String> outputBlob,
final ExecutionContext context
) {
// Log the entire incoming JSON for debugging
context.getLogger().info(mcpToolInvocationContext);
// Log the snippet name and content
context.getLogger().info("Saving snippet with name: " + snippetName);
context.getLogger().info("Snippet content:\n" + snippet);
// Write the snippet content to the output blob
outputBlob.setValue(snippet);
return "Successfully saved snippet '" + snippetName + "' with " + snippet.length() + " characters.";
}
```


This code creates an endpoint to expose a tool named `GetSnippets`

that tries to retrieve a code snippet by name from blob storage.

```
@FunctionName("GetSnippets")
@StorageAccount("AzureWebJobsStorage")
public String getSnippet(
@McpToolTrigger(
name = "getSnippets",
description = "Gets a text snippet from your snippets collection."
)
String mcpToolInvocationContext,
@McpToolProperty(
name = "snippetName",
propertyType = "string",
description = "The name of the snippet.",
required = true
)
String snippetName,
@BlobInput(name = "inputBlob", path = "snippets/{mcptoolargs.snippetName}.json")
String inputBlob,
final ExecutionContext context
) {
// Log the entire incoming JSON for debugging
context.getLogger().info(mcpToolInvocationContext);
// Log the snippet name and the fetched snippet content from the blob
context.getLogger().info("Retrieving snippet with name: " + snippetName);
context.getLogger().info("Snippet content:");
context.getLogger().info(inputBlob);
// Return the snippet content or a not found message
if (inputBlob != null && !inputBlob.trim().isEmpty()) {
return inputBlob;
} else {
return "Snippet '" + snippetName + "' not found.";
}
}
```


For the complete code example, see [Snippets.java](https://github.com/Azure-Samples/remote-mcp-functions-java/blob/main/src/main/java/com/function/Snippets.java).

Example code for JavaScript isn't currently available. See the TypeScript examples for general guidance using Node.js.

This code creates an endpoint to expose a tool named `savesnippet`

that tries to persist a named code snippet to blob storage.

```
import { app, InvocationContext, input, output, arg } from "@azure/functions";
app.mcpTool("saveSnippet", {
toolName: SAVE_SNIPPET_TOOL_NAME,
description: SAVE_SNIPPET_TOOL_DESCRIPTION,
toolProperties: {
[SNIPPET_NAME_PROPERTY_NAME]: arg.string().describe(SNIPPET_NAME_PROPERTY_DESCRIPTION),
[SNIPPET_PROPERTY_NAME]: arg.string().describe(SNIPPET_PROPERTY_DESCRIPTION)
},
extraOutputs: [blobOutputBinding],
handler: saveSnippet,
});
```


This code handles the `savesnippet`

trigger:

```
export async function saveSnippet(
_toolArguments: unknown,
context: InvocationContext
): Promise<string> {
console.info("Saving snippet");
// Get snippet name and content from the tool arguments
const mcptoolargs = context.triggerMetadata.mcptoolargs as {
snippetname?: string;
snippet?: string;
};
const snippetName = mcptoolargs?.snippetname;
const snippet = mcptoolargs?.snippet;
if (!snippetName) {
return "No snippet name provided";
}
if (!snippet) {
return "No snippet content provided";
}
// Save the snippet to blob storage using the output binding
context.extraOutputs.set(blobOutputBinding, snippet);
console.info(`Saved snippet: ${snippetName}`);
return snippet;
}
```


This code creates an endpoint to expose a tool named `getsnippet`

that tries to retrieve a code snippet by name from blob storage.

```
import { app, InvocationContext, input, output, arg } from "@azure/functions";
app.mcpTool("getSnippet", {
toolName: GET_SNIPPET_TOOL_NAME,
description: GET_SNIPPET_TOOL_DESCRIPTION,
toolProperties: {
[SNIPPET_NAME_PROPERTY_NAME]: arg.string().describe(SNIPPET_NAME_PROPERTY_DESCRIPTION)
},
extraInputs: [blobInputBinding],
handler: getSnippet,
});
```


This code handles the `getsnippet`

trigger:

```
export async function getSnippet(
_toolArguments: unknown,
context: InvocationContext
): Promise<string> {
console.info("Getting snippet");
// Get snippet name from the tool arguments
const mcptoolargs = context.triggerMetadata.mcptoolargs as {
snippetname?: string;
};
const snippetName = mcptoolargs?.snippetname;
console.info(`Snippet name: ${snippetName}`);
if (!snippetName) {
return "No snippet name provided";
}
// Get the content from blob binding - properly retrieving from extraInputs
const snippetContent = context.extraInputs.get(blobInputBinding);
if (!snippetContent) {
return `Snippet '${snippetName}' not found`;
}
console.info(`Retrieved snippet: ${snippetName}`);
return snippetContent as string;
}
```


For the complete code example, see [snippetsMcpTool.ts](https://github.com/Azure-Samples/remote-mcp-functions-typescript/blob/main/src/functions/snippetsMcpTool.ts).

This code uses the `mcp_tool_trigger`

decorator to create an endpoint to expose a tool named `save_snippet`

that tries to persist a named code snippet to blob storage.

```
@app.mcp_tool_trigger(
arg_name="context",
tool_name="save_snippet",
description="Save a snippet with a name.",
tool_properties=tool_properties_save_snippets_json,
)
@app.blob_output(arg_name="file", connection="AzureWebJobsStorage", path=_BLOB_PATH)
def save_snippet(file: func.Out[str], context) -> str:
content = json.loads(context)
snippet_name_from_args = content["arguments"][_SNIPPET_NAME_PROPERTY_NAME]
snippet_content_from_args = content["arguments"][_SNIPPET_PROPERTY_NAME]
if not snippet_name_from_args:
return "No snippet name provided"
if not snippet_content_from_args:
return "No snippet content provided"
file.set(snippet_content_from_args)
logging.info(f"Saved snippet: {snippet_content_from_args}")
return f"Snippet '{snippet_content_from_args}' saved successfully"
```


This code uses the `mcp_tool_trigger`

decorator to create an endpoint to expose a tool named `get_snippet`

that tries to retrieve a code snippet by name from blob storage.

```
@app.mcp_tool_trigger(
arg_name="context",
tool_name="get_snippet",
description="Retrieve a snippet by name.",
tool_properties=tool_properties_get_snippets_json,
)
@app.blob_input(arg_name="file", connection="AzureWebJobsStorage", path=_BLOB_PATH)
def get_snippet(file: func.InputStream, context) -> str:
"""
Retrieves a snippet by name from Azure Blob Storage.
Args:
file (func.InputStream): The input binding to read the snippet from Azure Blob Storage.
context: The trigger context containing the input arguments.
Returns:
str: The content of the snippet or an error message.
"""
snippet_content = file.read().decode("utf-8")
logging.info(f"Retrieved snippet: {snippet_content}")
return snippet_content
```


For the complete code example, see [function_app.py](https://github.com/Azure-Samples/remote-mcp-functions-python/blob/main/src/function_app.py).

Important

The MCP extension doesn't currently support PowerShell apps.

## Attributes

C# libraries use `McpToolTriggerAttribute`

to define the function trigger.

The attribute's constructor takes the following parameters:

| Parameter | Description |
|---|---|
ToolName |
(Required) name of the tool that's being exposed by the MCP trigger endpoint. |
Description |
(Optional) friendly description of the tool endpoint for clients. |

See [Usage](#usage) to learn how to define properties of the endpoint as input parameters.

## Annotations

The `@McpToolTrigger`

annotation creates a function that exposes a tool endpoint in your remote MCP server.

The annotation supports the following configuration options:

| Parameter | Description |
|---|---|
name |
(Required) name of the tool that's being exposed by the MCP trigger endpoint. |
description |
(Optional) friendly description of the tool endpoint for clients. |

The `@McpToolProperty`

annotation defines individual properties for your tools. Each property parameter in your function should be annotated with this annotation.

The `@McpToolProperty`

annotation supports the following configuration options:

| Parameter | Description |
|---|---|
name |
(Required) name of the tool property that gets exposed to clients. |
propertyType |
(Required) type of the tool property. Valid types are: `string` , `number` , `integer` , `boolean` , `object` . |
description |
(Optional) description of what the tool property does. |
required |
(Optional) if set to `true` , the tool property is required as an argument for tool calls. Defaults to `false` . |

## Decorators

*Applies only to the Python v2 programming model.*

The `mcp_tool_trigger`

decorator requires version 1.24.0 or later of the [ azure-functions package](https://pypi.org/project/azure-functions/). The following MCP trigger properties are supported on

`mcp_tool_trigger`

:| Property | Description |
|---|---|
arg_name |
The variable name (usually `context` ) used in function code to access the execution context. |
tool_name |
(Required) The name of the MCP server tool exposed by the function endpoint. |
description |
A description of the MCP server tool exposed by the function endpoint. |
tool_properties |
The JSON string representation of one or more property objects that expose properties of the tool to clients. |

## Configuration

The trigger supports these binding options, which are defined in your code:

| Options | Description |
|---|---|
type |
Must be set to `mcpToolTrigger` . Only used with generic definitions. |
toolName |
(Required) The name of the MCP server tool exposed by the function endpoint. |
description |
A description of the MCP server tool exposed by the function endpoint. |
toolProperties |
An array of `toolProperty` objects that expose properties of the tool to clients. |
extraOutputs |
When defined, sends function output to another binding. |
handler |
The method that contains the actual function code. |

See the [Example section](#example) for complete examples.

## Usage

The MCP tool trigger can bind to the following types:

| Type | Description |
|---|---|
|

[define tool properties](#tool-properties).When binding to a JSON serializable type, you can optionally also include a parameter of type

[ToolInvocationContext](https://github.com/Azure/azure-functions-mcp-extension/blob/main/src/Microsoft.Azure.Functions.Worker.Extensions.Mcp/Abstractions/ToolInvocationContext.cs)to access the tool call information.### Tool properties

MCP clients invoke tools with arguments to provide data and context for the tool's operation. The clients know how to collect and pass these arguments based on properties that the tool advertises as part of the protocol. You therefore need to define properties of the tool in your function code.

When you define a tool property, it's optional by default, and the client can omit it when invoking the tool. You need to explicitly mark properties as required if the tool can't operate without them.

Note

Earlier versions of the MCP extension preview made all tool properties required by default. This behavior changed as of version `1.0.0-preview.7`

, and now you must explicitly mark properties as required.

In C#, you can define properties for your tools in several ways. Which approach you use is a matter of code style preference. The options are:

- Your function takes input parameters using the
`McpToolProperty`

attribute. - You define a custom type with the properties, and the function binds to that type.
- You use the
`FunctionsApplicationBuilder`

to define properties in your`Program.cs`

file.

You can define one or more tool properties by applying the `McpToolProperty`

attribute to input binding-style parameters in your function.

The `McpToolPropertyAttribute`

type supports these properties:

| Property | Description |
|---|---|
PropertyName |
Name of the tool property that gets exposed to clients. |
Description |
Description of what the tool property does. |
IsRequired |
(Optional) If set to `true` , the tool property is required as an argument for tool calls. Defaults to `false` . |

The property type is inferred from the type of the parameter to which you apply the attribute. For example `[McpToolProperty("snippetname", "The name of the snippet.", true)] string name`

defines a required tool property named `snippetname`

of type `string`

in MCP messages.

You can see these attributes used in the `SaveSnippet`

tool in the [Examples](#example).

In Java, you define tool properties by using the `@McpToolProperty`

annotation on individual function parameters. Each parameter that represents a tool property should be annotated with this annotation, specifying the property name, type, description, and whether it's required.

You can see these annotations used in the [Examples](#example).

You can configure tool properties in the trigger definition's `toolProperties`

field, which is a string representation of an array of `ToolProperty`

objects.

A `ToolProperty`

object has this structure:

```
{
"propertyName": "Name of the property",
"propertyType": "Type of the property",
"description": "Optional property description",
"isRequired": true|false,
"isArray": true|false
}
```


The fields of a `ToolProperty`

object are:

| Property | Description |
|---|---|
propertyName |
Name of the tool property that gets exposed to clients. |
propertyType |
Type of the tool property. Valid types are: `string` , `number` , `integer` , `boolean` , `object` . See `isArray` for array types. |
description |
Description of what the tool property does. |
isRequired |
(Optional) If set to `true` , the tool property is required as an argument for tool calls. Defaults to `false` . |
isArray |
(Optional) If set to `true` , the tool property is an array of the specified property type. Defaults to `false` . |

You can provide the `toolProperties`

field as an array of `ToolProperty`

objects, or you can use the `arg`

helpers from `@azure/functions`

to define properties in a more type-safe way:

```
toolProperties: {
[SNIPPET_NAME_PROPERTY_NAME]: arg.string().describe(SNIPPET_NAME_PROPERTY_DESCRIPTION)
}
```


For more information, see [Examples](#example).

## host.json settings

The host.json file contains settings that control MCP trigger behaviors. See the [host.json settings](functions-bindings-mcp#hostjson-settings) section for details regarding available settings.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-app-settings -->

# App settings reference for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Application settings in a function app contain configuration options that affect all functions for that function app. These settings are accessed as environment variables. This article lists the app settings that are available in function apps.

There are several ways that you can add, update, and delete function app settings:

Changes to function app settings require your function app to be restarted.

In this article, example connection string values are truncated for readability.

Azure Functions uses the Azure App Service platform for hosting. You might find some settings relevant to hosting your function app in [Environment variables and app settings in Azure App Service](../app-service/reference-app-settings).

## App setting considerations

When you use app settings, you should be aware of the following considerations:

Changing application settings causes your function app to restart by default across all hosting plans. For zero-downtime deployments when changing settings, use the

[Flex Consumption plan](flex-consumption-plan)with[rolling updates as the site update strategy](flex-consumption-site-updates). For other hosting plans, see[optimize deployments](functions-best-practices#optimize-deployments)for guidance on minimizing downtime.In setting names, double-underscore (

`__`

) and colon (`:`

) are considered reserved values. Double-underscores are interpreted as hierarchical delimiters on both Windows and Linux. Colons are interpreted in the same way only on Windows. For example, the setting`AzureFunctionsWebHost__hostid=somehost_123456`

would be interpreted as the following JSON object:`"AzureFunctionsWebHost": { "hostid": "somehost_123456" }`

In this article, only double-underscores are used, since they're supported on both operating systems. Most of the settings that support managed identity connections use double-underscores.

When functions runs locally, app settings are specified in the

`Values`

collection in the[local.settings.json](functions-develop-local#local-settings-file).There are other function app configuration options in the

[host.json](functions-host-json)file and in the[local.settings.json](functions-develop-local#local-settings-file)file.You can use application settings to override host.json setting values without having to change the host.json file itself. This approach is helpful for scenarios where you need to configure or modify specific host.json settings for a specific environment. This approach also lets you change host.json settings without having to republish your project. To learn more, see the

[host.json reference article](functions-host-json#override-hostjson-values).This article documents the settings that are most relevant to your function apps. Because Azure Functions runs on App Service, other application settings are also supported. For more information, see

[Environment variables and app settings in Azure App Service](../app-service/reference-app-settings).Some scenarios also require you to work with settings documented in

[App Service site settings](#app-service-site-settings).Changing any

*read-only*[App Service application settings](../app-service/reference-app-settings#app-environment)can put your function app into an unresponsive state.Take care when updating application settings by using REST APIs, including ARM templates. Because these APIs replace the existing application settings, you must include all existing settings when adding or modifying settings using REST APIs or ARM templates. When possible, use Azure CLI or Azure PowerShell to programmatically work with application settings. For more information, see

[Work with application settings](functions-how-to-use-azure-function-app-settings#settings).

## APPINSIGHTS_INSTRUMENTATIONKEY

The instrumentation key for Application Insights. Don't use both `APPINSIGHTS_INSTRUMENTATIONKEY`

and `APPLICATIONINSIGHTS_CONNECTION_STRING`

. When possible, use `APPLICATIONINSIGHTS_CONNECTION_STRING`

. When Application Insights runs in a sovereign cloud, you must use `APPLICATIONINSIGHTS_CONNECTION_STRING`

. For more information, see [How to configure monitoring for Azure Functions](configure-monitoring).

| Key | Sample value |
|---|---|
| APPINSIGHTS_INSTRUMENTATIONKEY | `55555555-af77-484b-9032-64f83bb83bb` |

Don't use both `APPINSIGHTS_INSTRUMENTATIONKEY`

and `APPLICATIONINSIGHTS_CONNECTION_STRING`

. We recommend that you use `APPLICATIONINSIGHTS_CONNECTION_STRING`

.

## APPLICATIONINSIGHTS_AUTHENTICATION_STRING

Enables access to Application Insights by using Microsoft Entra authentication. Use this setting when you must connect to your Application Insights workspace by using Microsoft Entra authentication. For more information, see [Microsoft Entra authentication for Application Insights](/en-us/azure/azure-monitor/app/azure-ad-authentication).

When you use `APPLICATIONINSIGHTS_AUTHENTICATION_STRING`

, the specific value that you set depends on the type of managed identity:

| Managed identity | Setting value |
|---|---|
| System-assigned | `Authorization=AAD` |
| User-assigned | `Authorization=AAD;ClientId=<USER_ASSIGNED_CLIENT_ID>` |

This authentication requirement is applied to connections from the Functions host, snapshot debugger, profiler, and any language-specific agents. To use this setting, the managed identity must already be available to the function app, with an assigned role equivalent to [Monitoring Metrics Publisher](/en-us/azure/role-based-access-control/built-in-roles/monitor#monitoring-metrics-publisher).

Note

When using `APPLICATIONINSIGHTS_AUTHENTICATION_STRING`

to connect to Application Insights using Microsoft Entra authentication, you should also [Disable local authentication for Application Insights](/en-us/azure/azure-monitor/app/azure-ad-authentication#disable-local-authentication). This configuration requires Microsoft Entra authentication in order for telemetry to be ingested into your workspace.

## APPLICATIONINSIGHTS_CONNECTION_STRING

The connection string for Application Insights. Don't use both `APPINSIGHTS_INSTRUMENTATIONKEY`

and `APPLICATIONINSIGHTS_CONNECTION_STRING`

. We recommend the use of `APPLICATIONINSIGHTS_CONNECTION_STRING`

in all cases. It's a requirement in the following cases:

- When your function app requires the added customizations supported by using the connection string
- When your Application Insights instance runs in a sovereign cloud, which requires a custom endpoint

For more information, see [Connection strings](/en-us/azure/azure-monitor/app/sdk-connection-string).

| Key | Sample value |
|---|---|
| APPLICATIONINSIGHTS_CONNECTION_STRING | `InstrumentationKey=...` |

To connect to Application Insights with Microsoft Entra authentication, you should use [ APPLICATIONINSIGHTS_AUTHENTICATION_STRING](#applicationinsights_authentication_string).

## AZURE_FUNCTION_PROXY_DISABLE_LOCAL_CALL

Important

Azure Functions proxies was a feature of [versions 1.x through 3.x](functions-versions) of the Azure Functions runtime. For more information, see [Functions proxies](functions-proxies).

## AZURE_FUNCTION_PROXY_BACKEND_URL_DECODE_SLASHES

Important

Azure Functions proxies was a feature of [versions 1.x through 3.x](functions-versions) of the Azure Functions runtime. For more information, see [Functions proxies](functions-proxies).

## AZURE_FUNCTIONS_ENVIRONMENT

Configures the runtime [hosting environment](/en-us/dotnet/api/microsoft.extensions.hosting.environments) of the function app when running in Azure. This value is read during initialization. The runtime accepts only these values:

| Value | Description |
|---|---|
`Production` |
Represents a production environment, with reduced logging and full performance optimizations. This value is the default when `AZURE_FUNCTIONS_ENVIRONMENT` either isn't set or is set to an unsupported value. |
`Staging` |
Represents a staging environment, such as when running in a
|

`Development`

`AZURE_FUNCTIONS_ENVIRONMENT`

to `Development`

when running on your local computer. This setting can't be overridden in the local.settings.json file.Use this setting instead of `ASPNETCORE_ENVIRONMENT`

when you need to change the runtime environment in Azure to something other than `Production`

. For more information, see [Environment-based Startup class and methods](/en-us/aspnet/core/fundamentals/environments#environments).

This setting isn't available in version 1.x of the Functions runtime.

## AzureFunctionsJobHost__*

In version 2.x and later versions of the Functions runtime, application settings can override [host.json](functions-host-json) settings in the current environment. These overrides are expressed as application settings named `AzureFunctionsJobHost__path__to__setting`

. For more information, see [Override host.json values](functions-host-json#override-hostjson-values).

## AzureFunctionsWebHost__hostid

Sets the host ID for a given function app, which should be a unique ID. This setting overrides the automatically generated host ID value for your app. Use this setting only when you need to prevent host ID collisions between function apps that share the same storage account.

A host ID must meet the following requirements:

- Be between 1 and 32 characters
- Contain only lowercase letters, numbers, and dashes
- Not start or end with a dash
- Not contain consecutive dashes

An easy way to generate an ID is to take a GUID, remove the dashes, and make it lower case, such as by converting the GUID `1835D7B5-5C98-4790-815D-072CC94C6F71`

to the value `1835d7b55c984790815d072cc94c6f71`

.

| Key | Sample value |
|---|---|
| AzureFunctionsWebHost__hostid | `myuniquefunctionappname123456789` |

For more information, see [Host ID considerations](storage-considerations#host-id-considerations).

## AzureWebJobsDashboard

*This setting is deprecated and is only supported when running on version 1.x of the Azure Functions runtime.*

Optional storage account connection string for storing logs and displaying them in the **Monitor** tab in the Azure portal. The storage account must be a general-purpose one that supports blobs, queues, and tables. To learn more, see [Storage account requirements](storage-considerations#storage-account-requirements).

| Key | Sample value |
|---|---|
| AzureWebJobsDashboard | `DefaultEndpointsProtocol=https;AccountName=...` |

## AzureWebJobsDisableHomepage

A value of `true`

disables the default landing page that is shown for the root URL of a function app. The default value is `false`

.

| Key | Sample value |
|---|---|
| AzureWebJobsDisableHomepage | `true` |

When this app setting is omitted or set to `false`

, a page similar to the following example is displayed in response to the URL `<functionappname>.azurewebsites.net`

.


## AzureWebJobsDotNetReleaseCompilation

`true`

means use `Release`

mode when compiling .NET code. `false`

means use Debug mode. Default is `true`

.

| Key | Sample value |
|---|---|
| AzureWebJobsDotNetReleaseCompilation | `true` |

## AzureWebJobsFeatureFlags

A comma-delimited list of beta features to enable. Beta features enabled by these flags aren't production ready, but can be enabled for experimental use before they go live.

| Key | Sample value |
|---|---|
| AzureWebJobsFeatureFlags | `feature1,feature2,EnableProxies` |

If your app currently has this setting, add new flags to the end of the comma-delineated list.

Currently supported feature flags:

| Flag value | Description |
|---|---|
`EnableProxies` |
Re-enables proxies on version 4.x of the Functions runtime while you plan your migration to Azure API Management. For more information, see
|

`EnableAzureMonitorTimeIsoFormat`

`ISO 8601`

time format in Azure Monitor logs for Linux apps running on a Dedicated (App Service) plan.## AzureWebJobsKubernetesSecretName

Indicates the Kubernetes Secrets resource used for storing keys. Supported only when running in Kubernetes.

| Key | Sample value |
|---|---|
| AzureWebJobsKubernetesSecretName | `<SECRETS_RESOURCE>` |

Considerations when you use a Kubernetes Secrets resource:

- You must also set
`AzureWebJobsSecretStorageType`

to`kubernetes`

. When`AzureWebJobsKubernetesSecretName`

isn't set, the repository is considered read only. In this case, the values must be generated before deployment. - The
[Azure Functions Core Tools](functions-run-local)generates the values automatically when deploying to Kubernetes. [Immutable secrets](https://kubernetes.io/docs/concepts/configuration/secret/#secret-immutable)aren't supported and using them results in runtime errors.

To learn more, see [Manage key storage](function-keys-how-to#manage-key-storage).

## AzureWebJobsSecretStorageKeyVaultClientId

The client ID of the user-assigned managed identity or the app registration used to access the vault where keys are stored. This setting requires you to set `AzureWebJobsSecretStorageType`

to `keyvault`

. Supported in version 4.x and later versions of the Functions runtime.

| Key | Sample value |
|---|---|
| AzureWebJobsSecretStorageKeyVaultClientId | `<CLIENT_ID>` |

To learn more, see [Manage key storage](function-keys-how-to#manage-key-storage).

## AzureWebJobsSecretStorageKeyVaultClientSecret

The secret for client ID of the user-assigned managed identity or the app registration used to access the vault where keys are stored. This setting requires you to set `AzureWebJobsSecretStorageType`

to `keyvault`

. Supported in version 4.x and later versions of the Functions runtime.

| Key | Sample value |
|---|---|
| AzureWebJobsSecretStorageKeyVaultClientSecret | `<CLIENT_SECRET>` |

To learn more, see [Manage key storage](function-keys-how-to#manage-key-storage).

## AzureWebJobsSecretStorageKeyVaultName

*This setting is deprecated and was only used when running on version 3.x of the Azure Functions runtime.*

The name of a key vault instance used to store keys. This setting was only used in version 3.x of the Functions runtime, which is no longer supported. For version 4.x, instead use `AzureWebJobsSecretStorageKeyVaultUri`

. This setting requires you to set `AzureWebJobsSecretStorageType`

to `keyvault`

.

The vault must have an access policy corresponding to the system-assigned managed identity of the hosting resource. The access policy should grant the identity the following secret permissions: `Get`

,`Set`

, `List`

, and `Delete`

.

When your functions run locally, the developer identity is used. Settings must be in the [local.settings.json file](functions-develop-local#local-settings-file).

| Key | Sample value |
|---|---|
| AzureWebJobsSecretStorageKeyVaultName | `<VAULT_NAME>` |

To learn more, see [Manage key storage](function-keys-how-to#manage-key-storage).

## AzureWebJobsSecretStorageKeyVaultTenantId

The tenant ID of the app registration used to access the vault where keys are stored. This setting requires you to set `AzureWebJobsSecretStorageType`

to `keyvault`

. Supported in version 4.x and later versions of the Functions runtime. To learn more, see [Manage key storage](function-keys-how-to#manage-key-storage).

| Key | Sample value |
|---|---|
| AzureWebJobsSecretStorageKeyVaultTenantId | `<TENANT_ID>` |

## AzureWebJobsSecretStorageKeyVaultUri

The URI of a key vault instance used to store keys. Supported in version 4.x and later versions of the Functions runtime. We recommend this setting for using a key vault instance for key storage. This setting requires you to set `AzureWebJobsSecretStorageType`

to `keyvault`

.

The `AzureWebJobsSecretStorageKeyVaultUri`

value should be the full value of **Vault URI** displayed in the **Key Vault overview** tab, including `https://`

.

The vault must have an access policy corresponding to the system-assigned managed identity of the hosting resource. The access policy should grant the identity the following secret permissions: `Get`

,`Set`

, `List`

, and `Delete`

.

When your functions run locally, the developer identity is used, and settings must be in the [local.settings.json file](functions-develop-local#local-settings-file).

| Key | Sample value |
|---|---|
| AzureWebJobsSecretStorageKeyVaultUri | `https://<VAULT_NAME>.vault.azure.net` |

Important

Secrets aren't scoped to individual function apps through the `AzureWebJobsSecretStorageKeyVaultUri`

setting. If multiple function apps are configured to use the same Key Vault they share the same secrets, potentially leading to key collisions or overwrites. To avoid unintended behavior, we recommend that you use a separate Key Vault instance for each function app.

To learn more, see [Manage Key Storage](function-keys-how-to#manage-key-storage).

## AzureWebJobsSecretStorageSas

A Blob Storage SAS URL for a second storage account used for key storage. By default, Functions uses the account set in `AzureWebJobsStorage`

. When using this secret storage option, make sure that `AzureWebJobsSecretStorageType`

isn't explicitly set or is set to `blob`

. To learn more, see [Manage key storage](function-keys-how-to#manage-key-storage).

| Key | Sample value |
|---|---|
| AzureWebJobsSecretStorageSas | `<BLOB_SAS_URL>` |

## AzureWebJobsSecretStorageType

Specifies the repository or provider to use for key storage. Keys are always encrypted before being stored using a secret unique to your function app.

| Key | Value | Description |
|---|---|---|
| AzureWebJobsSecretStorageType | `blob` |
Keys are stored in a Blob storage container in the account provided by the `AzureWebJobsStorage` setting. Blob storage is the default behavior when `AzureWebJobsSecretStorageType` isn't set.To specify a different storage account, use the `AzureWebJobsSecretStorageSas` setting to indicate the SAS URL of a second storage account. |
| AzureWebJobsSecretStorageType | `files` |
Keys are persisted on the file system. This behavior is the default for Functions v1.x. |
| AzureWebJobsSecretStorageType | `keyvault` |
Keys are stored in a key vault instance set by `AzureWebJobsSecretStorageKeyVaultName` . |
| AzureWebJobsSecretStorageType | `kubernetes` |
Supported only when running the Functions runtime in Kubernetes. When `AzureWebJobsKubernetesSecretName` isn't set, the repository is considered read only. In this case, the values must be generated before deployment. The
|

To learn more, see [Manage key storage](function-keys-how-to#manage-key-storage).

## AzureWebJobsStorage

Specifies the connection string for an Azure Storage account that the Functions runtime uses for normal operations. Some uses of this storage account by Functions include key management, timer trigger management, and Event Hubs checkpoints. The storage account must be a general-purpose one that supports blobs, queues, and tables. For more information, see [Storage account requirements](storage-considerations#storage-account-requirements).

| Key | Sample value |
|---|---|
| AzureWebJobsStorage | `DefaultEndpointsProtocol=https;AccountName=...` |

Instead of a connection string, you can use an identity-based connection for this storage account. For more information, see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity).

## AzureWebJobsStorage__accountName

When using an identity-based storage connection, sets the account name of the storage account instead of using the connection string in `AzureWebJobsStorage`

. This syntax is unique to `AzureWebJobsStorage`

and can't be used for other identity-based connections.

| Key | Sample value |
|---|---|
| AzureWebJobsStorage__accountName | `<STORAGE_ACCOUNT_NAME>` |

For sovereign clouds or when using a custom DNS, you must instead use the service-specific `AzureWebJobsStorage__*ServiceUri`

settings.

## AzureWebJobsStorage__blobServiceUri

When using an identity-based storage connection, sets the data plane URI of the blob service of the storage account.

| Key | Sample value |
|---|---|
| AzureWebJobsStorage__blobServiceUri | `https://<STORAGE_ACCOUNT_NAME>.blob.core.windows.net` |

Use this setting instead of `AzureWebJobsStorage__accountName`

in sovereign clouds or when using a custom DNS. For more information, see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity).

## AzureWebJobsStorage__clientId

Sets the client ID of a specific user-assigned identity used to obtain an access token for managed identity authentication. Requires that `AzureWebJobsStorage__credential`

be set to `managedidentity`

. The value is a client ID that corresponds to an identity assigned to the application. You can't set both `AzureWebJobsStorage__managedIdentityResourceId`

and `AzureWebJobsStorage__clientId`

. When not set, the system-assigned identity is used.

## AzureWebJobsStorage__credential

Defines how an access token is obtained for the connection. Use `managedidentity`

for managed identity authentication. When using `managedidentity`

, a managed identity must be available in the hosting environment. Don't set `AzureWebJobsStorage__credential`

in local development scenarios.

## AzureWebJobsStorage__managedIdentityResourceId

Sets the resource identifier of a user-assigned identity used to obtain an access token for managed identity authentication. Requires that `AzureWebJobsStorage__credential`

be set to `managedidentity`

. The value is the resource ID of an identity assigned to the application used for managed identity authentication. You can't set both `AzureWebJobsStorage__managedIdentityResourceId`

and `AzureWebJobsStorage__clientId`

. When not set, the system-assigned identity is used.

## AzureWebJobsStorage__queueServiceUri

When using an identity-based storage connection, sets the data plane URI of the queue service of the storage account.

| Key | Sample value |
|---|---|
| AzureWebJobsStorage__queueServiceUri | `https://<STORAGE_ACCOUNT_NAME>.queue.core.windows.net` |

Use this setting instead of `AzureWebJobsStorage__accountName`

in sovereign clouds or when using a custom DNS. For more information, see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity).

## AzureWebJobsStorage__tableServiceUri

When using an identity-based storage connection, sets data plane URI of a table service of the storage account.

| Key | Sample value |
|---|---|
| AzureWebJobsStorage__tableServiceUri | `https://<STORAGE_ACCOUNT_NAME>.table.core.windows.net` |

Use this setting instead of `AzureWebJobsStorage__accountName`

in sovereign clouds or when using a custom DNS. For more information, see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity).

## AzureWebJobs_TypeScriptPath

Path to the compiler used for TypeScript. Allows you to override the default if you need to.

| Key | Sample value |
|---|---|
| AzureWebJobs_TypeScriptPath | `%HOME%\typescript` |

## DOCKER_REGISTRY_SERVER_PASSWORD

Indicates the password used to access a private container registry. This setting is only required when deploying your containerized function app from a private container registry. For more information, see [Environment variables and app settings in Azure App Service](../app-service/reference-app-settings#custom-containers).

## DOCKER_REGISTRY_SERVER_URL

Indicates the URL of a private container registry. This setting is only required when deploying your containerized function app from a private container registry. For more information, see [Environment variables and app settings in Azure App Service](../app-service/reference-app-settings#custom-containers).

## DOCKER_REGISTRY_SERVER_USERNAME

Indicates the account used to access a private container registry. This setting is only required when deploying your containerized function app from a private container registry. For more information, see [Environment variables and app settings in Azure App Service](../app-service/reference-app-settings#custom-containers).

## DOCKER_SHM_SIZE

Sets the shared memory size (in bytes) when the Python worker is using shared memory. To learn more, see [Shared memory](https://github.com/Azure/azure-functions-python-worker/wiki/Shared-Memory).

| Key | Sample value |
|---|---|
| DOCKER_SHM_SIZE | `268435456` |

The preceding value sets a shared memory size of ~256 MB.

Requires that [FUNCTIONS_WORKER_SHARED_MEMORY_DATA_TRANSFER_ENABLED](#functions_worker_shared_memory_data_transfer_enabled) is set to `1`

.

## ENABLE_ORYX_BUILD

Indicates whether the [Oryx build system](https://github.com/microsoft/Oryx) is used during deployment. `ENABLE_ORYX_BUILD`

must be set to `true`

when doing remote build deployments to Linux. For more information, see [Remote build](functions-deployment-technologies#remote-build).

| Key | Sample value |
|---|---|
| ENABLE_ORYX_BUILD | `true` |

## FUNCTION_APP_EDIT_MODE

Indicates whether you can edit your function app in the Azure portal. Valid values are `readwrite`

and `readonly`

.

| Key | Sample value |
|---|---|
| FUNCTION_APP_EDIT_MODE | `readonly` |

The runtime sets the value based on the language stack and deployment status of your function app. For more information, see [Development limitations in the Azure portal](functions-how-to-use-azure-function-app-settings#development-limitations-in-the-azure-portal).

## FUNCTIONS_EXTENSION_VERSION

The version of the Functions runtime that hosts your function app. A tilde (`~`

) with major version means use the latest version of that major version, for example, `~4`

. When new minor versions of the same major version are available, they're automatically installed in the function app.

| Key | Sample value |
|---|---|
| FUNCTIONS_EXTENSION_VERSION | `~4` |

The following major runtime version values are supported:

| Value | Runtime target | Comment |
|---|---|---|
`~4` |
4.x | Recommended |
`~1` |
1.x | Support ends September 14, 2026 |

A value of `~4`

means that your app runs on version 4.x of the runtime. A value of `~1`

pins your app to version 1.x of the runtime. Runtime versions 2.x and 3.x are no longer supported. For more information, see [Azure Functions runtime versions overview](functions-versions).

If requested by support to pin your app to a specific minor version, use the full version number, for example, `4.0.12345`

. For more information, see [How to target Azure Functions runtime versions](set-runtime-version).

## FUNCTIONS_INPROC_NET8_ENABLED

Indicates whether to an app can use .NET 8 on the in-process model. To use .NET 8 on the in-process model, this value must be set to `1`

. See [Updating to target .NET 8](functions-dotnet-class-library#updating-to-target-net-8) for complete instructions, including other required configuration values.

| Key | Sample value |
|---|---|
| FUNCTIONS_INPROC_NET8_ENABLED | `1` |

Set to `0`

to disable support for .NET 8 on the in-process model.

## FUNCTIONS_NODE_BLOCK_ON_ENTRY_POINT_ERROR

This app setting is a temporary way for Node.js apps to enable a breaking change that makes entry point errors easier to troubleshoot on Node.js v18 or lower. We highly recommend using `true`

, especially for programming model v4 apps, which always use entry point files. The behavior without the breaking change (`false`

) ignores entry point errors and doesn't log them in Application Insights.

Starting with Node.js v20, the app setting has no effect and the breaking change behavior is always enabled.

For Node.js v18 or lower, the app setting is used, and the default behavior depends on if the error happens before or after a model v4 function has been registered:

- If the error is thrown before, the default behavior matches
`false`

. For example, if you're using model v3 or your entry point file doesn't exist. - If the error is thrown after, the default behavior matches
`true`

. For example, if you try to register duplicate model v4 functions.

| Key | Value | Description |
|---|---|---|
| FUNCTIONS_NODE_BLOCK_ON_ENTRY_POINT_ERROR | `true` |
Block on entry point errors and log them in Application Insights. |
| FUNCTIONS_NODE_BLOCK_ON_ENTRY_POINT_ERROR | `false` |
Ignore entry point errors and don't log them in Application Insights. |

## FUNCTIONS_REQUEST_BODY_SIZE_LIMIT

Overrides the default limit on the body size of requests sent to HTTP endpoints. The value is given in bytes, with a default maximum request size of 104,857,600 bytes.

| Key | Sample value |
|---|---|
| FUNCTIONS_REQUEST_BODY_SIZE_LIMIT | `250000000` |

## FUNCTIONS_V2_COMPATIBILITY_MODE

Important

This setting is no longer supported. It was originally provided to enable a short-term workaround for apps that targeted the v2.x runtime. They would be able to instead run on the v3.x runtime while it was still supported. Except for legacy apps that run on version 1.x, all function apps must run on version 4.x of the Functions runtime: `FUNCTIONS_EXTENSION_VERSION=~4`

. For more information, see [Azure Functions runtime versions overview](functions-versions).

## FUNCTIONS_WORKER_PROCESS_COUNT

Specifies the maximum number of language worker processes, with a default value of `1`

. The maximum value allowed is `10`

. Function invocations are evenly distributed among language worker processes. Language worker processes are spawned every 10 seconds until the count set by `FUNCTIONS_WORKER_PROCESS_COUNT`

is reached. Using multiple language worker processes isn't the same as [scaling](functions-scale). Consider using this setting when your workload has a mix of CPU-bound and I/O-bound invocations. This setting applies to all language runtimes, except for .NET running in process (`FUNCTIONS_WORKER_RUNTIME=dotnet`

).

| Key | Sample value |
|---|---|
| FUNCTIONS_WORKER_PROCESS_COUNT | `2` |

## FUNCTIONS_WORKER_RUNTIME

The language or language stack of the worker runtime to load in the function app. This value corresponds to the language being used in your application, for example, `python`

. Starting with version 2.x of the Azure Functions runtime, a given function app can only support a single language.

| Key | Sample value |
|---|---|
| FUNCTIONS_WORKER_RUNTIME | `node` |

Valid values:

| Value | Language/language stack |
|---|---|
`dotnet` |
|

`dotnet-isolated`

[C# (isolated worker process)](dotnet-isolated-process-guide)`java`

[Java](functions-reference-java)`node`

[JavaScript](functions-reference-node?tabs=javascript)[TypeScript](functions-reference-node?tabs=typescript)`powershell`

[PowerShell](functions-reference-powershell)`python`

[Python](functions-reference-python)`custom`

[Other](functions-custom-handlers)## FUNCTIONS_WORKER_SHARED_MEMORY_DATA_TRANSFER_ENABLED

This setting enables the Python worker to use shared memory to improve throughput. Enable shared memory when your Python function app is hitting memory bottlenecks.

| Key | Sample value |
|---|---|
| FUNCTIONS_WORKER_SHARED_MEMORY_DATA_TRANSFER_ENABLED | `1` |

With this setting enabled, you can use the [DOCKER_SHM_SIZE](#docker_shm_size) setting to set the shared memory size. To learn more, see [Shared memory](https://github.com/Azure/azure-functions-python-worker/wiki/Shared-Memory).

## JAVA_APPLICATIONINSIGHTS_ENABLE_TELEMETRY

Indicates whether the Java worker process should output telemetry in an Open Telemetry format to the Application Insights endpoint. Setting this flag to `True`

tells the Functions host to let the Java worker process stream OpenTelemetry logs directly, which prevents duplicate host-level entries. For more information, see [Configure application settings](opentelemetry-howto?pivots=programming-language-java#configure-application-settings).

## JAVA_ENABLE_SDK_TYPES

Enables your function app to use native Azure SDK types in bindings.

Note

Support for binding to SDK types is currently in preview and limited to the Azure Blob Storage SDK. For more information, see [SDK types](functions-reference-java#sdk-types) in the Java reference article.

| Key | Sample value |
|---|---|
| JAVA_ENABLE_SDK_TYPES | `true` |

For more information, see [SDK types](functions-reference-java#sdk-types) in the Java reference article.

## JAVA_OPTS

Used to customize the Java virtual machine (JVM) used to run your Java functions when running on a [Premium plan](functions-premium-plan) or [Dedicated plan](dedicated-plan). When running on a Consumption plan, instead use `languageWorkers__java__arguments`

. For more information, see [Customize JVM](functions-reference-java#customize-jvm).

## languageWorkers__java__arguments

Used to customize the Java virtual machine (JVM) used to run your Java functions when running on a [Consumption plan](functions-premium-plan). This setting does increase the cold start times for Java functions running in a Consumption plan. For a Premium or Dedicated plan, instead use `JAVA_OPTS`

. For more information, see [Customize JVM](functions-reference-java#customize-jvm).

## MDMaxBackgroundUpgradePeriod

Controls the managed dependencies background update period for PowerShell function apps, with a default value of `7.00:00:00`

(weekly).

Each PowerShell worker process initiates checking for module upgrades on the PowerShell Gallery on process start and every `MDMaxBackgroundUpgradePeriod`

after the start. When a new module version is available in the PowerShell Gallery, it's installed to the file system and made available to PowerShell workers. Decreasing this value lets your function app get newer module versions sooner, but it also increases the app resource usage, including network I/O, CPU, and storage. Increasing this value decreases the app's resource usage, but it can also delay delivering new module versions to your app.

| Key | Sample value |
|---|---|
| MDMaxBackgroundUpgradePeriod | `7.00:00:00` |

To learn more, see [Dependency management](functions-reference-powershell#dependency-management).

## MDNewSnapshotCheckPeriod

Specifies how often each PowerShell worker checks whether managed dependency upgrades are installed. The default frequency is `01:00:00`

(hourly).

After new module versions are installed to the file system, every PowerShell worker process must be restarted. Restarting PowerShell workers affects your app availability because it can interrupt current function execution. Until all PowerShell worker processes are restarted, function invocations can use either the old or the new module versions. Restarting all PowerShell workers completes within `MDNewSnapshotCheckPeriod`

.

Within every `MDNewSnapshotCheckPeriod`

, the PowerShell worker checks whether or not managed dependency upgrades are installed. When upgrades are installed, a restart is initiated. Increasing this value decreases the frequency of interruptions because of restarts. However, the increase might also increase the time during which function invocations could use either the old or the new module versions, nondeterministically.

| Key | Sample value |
|---|---|
| MDNewSnapshotCheckPeriod | `01:00:00` |

To learn more, see [Dependency management](functions-reference-powershell#dependency-management).

## MDMinBackgroundUpgradePeriod

The period of time after a previous managed dependency upgrade check before another upgrade check is started, with a default of `1.00:00:00`

(daily).

To avoid excessive module upgrades on frequent Worker restarts, checking for module upgrades isn't performed when any worker already initiated that check in the last `MDMinBackgroundUpgradePeriod`

.

| Key | Sample value |
|---|---|
| MDMinBackgroundUpgradePeriod | `1.00:00:00` |

To learn more, see [Dependency management](functions-reference-powershell#dependency-management).

## OTEL_EXPORTER_OTLP_ENDPOINT

Indicates the URL to which OpenTelemetry-formatted data is exported for ingestion. For more information, see [Use OpenTelemetry with Azure Functions](opentelemetry-howto).

## OTEL_EXPORTER_OTLP_HEADERS

Sets an optional list of headers that are applied to all outgoing data exported to an OpenTelemetry endpoint. You should use this setting when the OpenTelemetry endpoint requires to supply an API key. For more information, see [Use OpenTelemetry with Azure Functions](opentelemetry-howto).

## PIP_INDEX_URL

Overrides the default base URL of the Python Package Index (`https://pypi.org/simple`

) when running a remote build. Because this setting replaces the package index, you might see unexpected behaviour on restore. Only use this setting when you need to use a complete set of custom dependencies. When possible, you should instead use `PIP_EXTRA_URL`

, which lets you reference an additional package index. For more information, see [Custom dependencies](python-build-options#custom-dependencies) in the Python build article.

| Key | Sample value |
|---|---|
| PIP_INDEX_URL | `http://my.custom.package.repo/simple` |

These custom dependencies can be in a package index repository compliant with PEP 503 (the simple repository API) or in a local directory that follows the same format. For more information, see [ pip documentation for --index-url](https://pip.pypa.io/en/stable/cli/pip_wheel/?highlight=index%20url#cmdoption-i).


## PIP_EXTRA_INDEX_URL

The value for this setting indicates an extra index URL for custom packages for Python apps, to use in addition to the `--index-url`

. Use this setting when you need to run a remote build using custom dependencies that are found in an extra package index. For more information, see [Custom dependencies](python-build-options#custom-dependencies) in the Python build article.

| Key | Sample value |
|---|---|
| PIP_EXTRA_INDEX_URL | `http://my.custom.package.repo/simple` |

Should follow the same rules as `--index-url`

. For more information, see [ pip documentation for --extra-index-url](https://pip.pypa.io/en/stable/cli/pip_wheel/?highlight=index%20url#cmdoption-extra-index-url).


## PROJECT

A [continuous deployment](functions-continuous-deployment) setting that tells the Kudu deployment service the folder in a connected repository to location the deployable project.

| Key | Sample value |
|---|---|
| PROJECT | `WebProject/WebProject.csproj` |

## PYTHON_APPLICATIONINSIGHTS_ENABLE_TELEMETRY

Indicates whether the Python worker process should output telemetry in an Open Telemetry format to the Application Insights endpoint. Setting this flag to `True`

tells the Functions host to let the Python worker process export OpenTelemetry data to [Application Insights endpoint](#applicationinsights_connection_string). For more information, see [Configure application settings](opentelemetry-howto?pivots=programming-language-python#configure-application-settings).

## PYTHON_ISOLATE_WORKER_DEPENDENCIES

The configuration is specific to Python function apps. It defines the prioritization of module loading order. By default, this value is set to `0`

.

| Key | Value | Description |
|---|---|---|
| PYTHON_ISOLATE_WORKER_DEPENDENCIES | `0` |
Prioritize loading the Python libraries from internal Python worker's dependencies, which is the default behavior. Non-Microsoft libraries defined in requirements.txt might be shadowed. |
| PYTHON_ISOLATE_WORKER_DEPENDENCIES | `1` |
Prioritize loading the Python libraries from application's package defined in requirements.txt. This value prevents your libraries from colliding with internal Python worker's libraries. |

## PYTHON_ENABLE_DEBUG_LOGGING

Enables debug-level logging in a Python function app. A value of `1`

enables debug-level logging. Without this setting or with a value of `0`

, only information and higher-level logs are sent from the Python worker to the Functions host. Use this setting when debugging or tracing your Python function executions.

When debugging Python functions, make sure to also set a debug or trace [logging level](functions-host-json#logging) in the host.json file, as needed. To learn more, see [How to configure monitoring for Azure Functions](configure-monitoring).

## PYTHON_ENABLE_OPENTELEMETRY

Indicates whether the Python worker process should export telemetry to an Open Telemetry endpoint. Setting this flag to `True`

tells the Functions host to let the Python worker process export OpenTelemetry data to the configured [OTEL_EXPORTER_OTLP_ENDPOINT](#otel_exporter_otlp_endpoint). For more information, see [Configure application settings](opentelemetry-howto?pivots=programming-language-python#configure-application-settings).

## PYTHON_ENABLE_WORKER_EXTENSIONS

The configuration is specific to Python function apps. Setting this value to `1`

allows the worker to load in [Python worker extensions](develop-python-worker-extensions) defined in requirements.txt. It enables your function app to access new features provided by partner packages. It can also change the behavior of function load and invocation in your app. Ensure the extension you choose is trustworthy as you bear the risk of using it. Azure Functions gives no express warranties to any extensions. For how to use an extension, visit the extension's manual page or readme doc. By default, this value sets to `0`

.

| Key | Value | Description |
|---|---|---|
| PYTHON_ENABLE_WORKER_EXTENSIONS | `0` |
Disable any Python worker extension. |
| PYTHON_ENABLE_WORKER_EXTENSIONS | `1` |
Allow Python worker to load extensions from requirements.txt. |

## PYTHON_THREADPOOL_THREAD_COUNT

Specifies the maximum number of threads that a Python language worker would use to run function invocations, with a default value of `1`

for Python version `3.8`

and below. For Python version `3.9`

and above, the value is set to `None`

. This setting doesn't guarantee the number of threads that would be set during executions. The setting allows Python to expand the number of threads to the specified value. The setting only applies to Python functions apps. Additionally, the setting applies to synchronous functions invocation and not for coroutines.

| Key | Sample value | Max value |
|---|---|---|
| PYTHON_THREADPOOL_THREAD_COUNT | 2 | 32 |

## SCALE_CONTROLLER_LOGGING_ENABLED

*This setting is currently in preview.*

This setting controls logging from the Azure Functions scale controller. For more information, see [Scale controller logs](functions-monitoring#scale-controller-logs).

| Key | Sample value |
|---|---|
| SCALE_CONTROLLER_LOGGING_ENABLED | `AppInsights:Verbose` |

The value for this key is supplied in the format `<DESTINATION>:<VERBOSITY>`

, which is defined as follows:

| Property | Description |
|---|---|
`<DESTINATION>` |
The destination to which logs are sent. Valid values are `AppInsights` and `Blob` .When you use `AppInsights` , ensure that the
When you set the destination to `Blob` , logs are created in a blob container named `azure-functions-scale-controller` in the default storage account set in the `AzureWebJobsStorage` application setting. |
`<VERBOSITY>` |
Specifies the level of logging. Supported values are `None` , `Warning` , and `Verbose` .When set to `Verbose` , the scale controller logs a reason for every change in the worker count, and information about the triggers that factor into those decisions. Verbose logs include trigger warnings and the hashes used by the triggers before and after the scale controller runs. |

Tip

Keep in mind that while you leave scale controller logging enabled, it impacts the [potential costs of monitoring your function app](functions-monitoring#application-insights-pricing-and-limits). Consider enabling logging until you collect enough data to understand how the scale controller is behaving, and then disabling it.

## SCM_DO_BUILD_DURING_DEPLOYMENT

Controls remote build behavior during deployment. When `SCM_DO_BUILD_DURING_DEPLOYMENT`

is set to `true`

, the project is built remotely during deployment.

| Key | Sample value |
|---|---|
| SCM_DO_BUILD_DURING_DEPLOYMENT | `true` |

## SCM_LOGSTREAM_TIMEOUT

Controls the timeout, in seconds, when connected to streaming logs. The default value is 7200 (2 hours).

| Key | Sample value |
|---|---|
| SCM_LOGSTREAM_TIMEOUT | `1800` |

The preceding sample value of `1800`

sets a timeout of 30 minutes. For more information, see [Enable streaming execution logs in Azure Functions](streaming-logs).

## WEBSITE_CONTENTAZUREFILECONNECTIONSTRING

Connection string for storage account where the function app code and configuration are stored in event-driven scaling plans. For more information, see [Storage account connection setting](storage-considerations#storage-account-connection-setting).

| Key | Sample value |
|---|---|
| WEBSITE_CONTENTAZUREFILECONNECTIONSTRING | `DefaultEndpointsProtocol=https;AccountName=...` |

This setting is required for both Consumption and Elastic Premium plan apps. It's not required for Dedicated plan apps, which Functions doesn't dynamically scale.

The Flex Consumption plan is now the recommended serverless hosting plan for Azure Functions. It offers faster scaling, reduced cold starts, private networking, and more control over performance and cost. For more information, see [Flex Consumption plan](flex-consumption-plan).

Changing or removing this setting can cause your function app to not start. To learn more, see [this troubleshooting article](functions-recover-storage-account#storage-account-application-settings-were-deleted).

Azure Files doesn't currently support using managed identity when accessing the file share. For more information, see [Azure Files supported authentication scenarios](../storage/files/storage-files-active-directory-overview#supported-authentication-scenarios).

You might use a [KeyVault reference](../app-service/app-service-key-vault-references) for this connection setting. However, additional configuration is required to create and dynamically scale a function app in a Premium or Consumption plan when the storage connection string is maintained in a KeyVault. For more information, see [Considerations for Azure Files mounting](../app-service/app-service-key-vault-references#considerations-for-azure-files-mounting).

## WEBSITE_CONTENTOVERVNET

Important

WEBSITE_CONTENTOVERVNET is a legacy app setting that has been replaced by the [vnetContentShareEnabled](#vnetcontentshareenabled) site property.

A value of `1`

enables your function app to scale across stamps when you have your storage account restricted to a virtual network. You should enable this setting when restricting your storage account to a virtual network. Only required when using `WEBSITE_CONTENTSHARE`

and `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

. To learn more, see [Restrict your storage account to a virtual network](configure-networking-how-to#restrict-your-storage-account-to-a-virtual-network).

| Key | Sample value |
|---|---|
| WEBSITE_CONTENTOVERVNET | `1` |

This app setting is required for cross-stamp scaling on the [Elastic Premium](functions-premium-plan) and [Dedicated (App Service) plans](dedicated-plan) (Standard and higher) when the storage account is VNet-restricted. Without this setting, the function app can only scale within a single stamp (approximately 1-20 instances). Not supported when running on a [Consumption plan](consumption-plan).

Note

You must take special care when routing to the content share in a storage account shared by multiple function apps in the same plan. For more information, see [Consistent routing through virtual networks](storage-considerations#consistent-routing-through-virtual-networks) in the Storage considerations article.

## WEBSITE_CONTENTSHARE

The name of the file share that Functions uses to store function app code and configuration files. This content is required by event-driven scaling plans. Used with `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

. Default is a unique string generated by the runtime, which begins with the function app name. For more information, see [Storage account connection setting](storage-considerations#storage-account-connection-setting).

| Key | Sample value |
|---|---|
| WEBSITE_CONTENTSHARE | `functionapp091999e2` |

This setting is required only for Consumption and Premium plan apps. It's not required for Dedicated plan apps, which aren't dynamically scaled by Functions.

The Flex Consumption plan is now the recommended serverless hosting plan for Azure Functions. It offers faster scaling, reduced cold starts, private networking, and more control over performance and cost. For more information, see [Flex Consumption plan](flex-consumption-plan).

The share is created when your function app is created. Changing or removing this setting can cause your function app to not start. To learn more, see [this troubleshooting article](functions-recover-storage-account#storage-account-application-settings-were-deleted).

The following considerations apply when using an Azure Resource Manager (ARM) template or Bicep file to create a function app during deployment:

- When you don't set a
`WEBSITE_CONTENTSHARE`

value for the main function app or any apps in slots, unique share values are generated for you. Not setting`WEBSITE_CONTENTSHARE`

*is the recommended approach*for an ARM template deployment. - There are scenarios where you must set the
`WEBSITE_CONTENTSHARE`

value to a predefined value, such as when you[use a secured storage account in a virtual network](configure-networking-how-to#restrict-your-storage-account-to-a-virtual-network). In this case, you must set a unique share name for the main function app and the app for each deployment slot. For a storage account secured by a virtual network, you must also create the share itself as part of your automated deployment. For more information, see[Secured deployments](functions-infrastructure-as-code#secured-deployments). - Don't make
`WEBSITE_CONTENTSHARE`

a slot setting. - When you specify
`WEBSITE_CONTENTSHARE`

, the value must follow[this guidance for share names](/en-us/rest/api/storageservices/naming-and-referencing-shares--directories--files--and-metadata#share-names).

## WEBSITE_DNS_SERVER

Sets the DNS server used by an app when resolving IP addresses. This setting is often required when using certain networking functionality, such as [Azure DNS private zones](functions-networking-options#azure-dns-private-zones) and [private endpoints](functions-networking-options#restrict-your-storage-account-to-a-virtual-network).

| Key | Sample value |
|---|---|
| WEBSITE_DNS_SERVER | `168.63.129.16` |

## WEBSITE_ENABLE_BROTLI_ENCODING

Controls whether Brotli encoding is used for compression instead of the default gzip compression. When `WEBSITE_ENABLE_BROTLI_ENCODING`

is set to `1`

, Brotli encoding is used. Otherwise, gzip encoding is used.

## WEBSITE_FUNCTIONS_ARMCACHE_ENABLED

Disables caching when deploying function apps using Azure Resource Manager (ARM) templates.

| Key | Sample value |
|---|---|
| WEBSITE_FUNCTIONS_ARMCACHE_ENABLED | 0 |

## WEBSITE_MAX_DYNAMIC_APPLICATION_SCALE_OUT

The maximum number of instances that the app can scale out to. Default is no limit.

Important

This setting is in preview. An [app property for function max scale out](event-driven-scaling#limit-scale-out) now exists. We recommend this property to limit scale-out.

| Key | Sample value |
|---|---|
| WEBSITE_MAX_DYNAMIC_APPLICATION_SCALE_OUT | `5` |

## WEBSITE_NODE_DEFAULT_VERSION

*Windows only.*
Sets the version of Node.js to use when running your function app on Windows. You should use a tilde (`~`

) to have the runtime use the latest available version of the targeted major version. For example, when set to `~18`

, the latest version of Node.js 18 is used. When a major version is targeted with a tilde, you don't have to manually update the minor version.

| Key | Sample value |
|---|---|
| WEBSITE_NODE_DEFAULT_VERSION | `~18` |

## WEBSITE_OVERRIDE_STICKY_DIAGNOSTICS_SETTINGS

When you perform [a slot swap](functions-deployment-slots#swap-slots) on a function app running on a Premium plan, the swap can fail when the dedicated storage account used by the app is network restricted. This failure is caused by a legacy [application logging feature](../app-service/troubleshoot-diagnostic-logs#enable-application-logging-windows), which both Functions and App Service share. This setting overrides that legacy logging feature and allows the swap to occur.

| Key | Sample value |
|---|---|
| WEBSITE_OVERRIDE_STICKY_DIAGNOSTICS_SETTINGS | `0` |

Add `WEBSITE_OVERRIDE_STICKY_DIAGNOSTICS_SETTINGS`

with a value of `0`

to all slots to make sure that legacy diagnostic settings don't block your swaps. You can also add this setting and value to just the production slot as a [deployment slot ( sticky) setting](functions-deployment-slots#create-a-deployment-setting).

## WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS

By default, the version settings for function apps are specific to each slot. This setting is used when upgrading functions by using [deployment slots](functions-deployment-slots). This approach prevents unanticipated behavior due to changing versions after a swap. Set to `0`

in production and in the slot to make sure that all version settings are also swapped. For more information, see [Upgrade using slots](migrate-version-3-version-4#update-using-slots).

| Key | Sample value |
|---|---|
| WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS | `0` |

## WEBSITE_RUN_FROM_PACKAGE

Enables your function app to run from a package file, which can be locally mounted or deployed to an external URL.

| Key | Sample value |
|---|---|
| WEBSITE_RUN_FROM_PACKAGE | `1` |

Valid values are either a URL that resolves to the location of an external deployment package file, or `1`

. When set to `1`

, the package must be in the `d:\home\data\SitePackages`

folder. When you use zip deployment with `WEBSITE_RUN_FROM_PACKAGE`

enabled, the package is automatically uploaded to this location. For more information, see [Run your functions from a package file](run-functions-from-deployment-package).

When you use `WEBSITE_RUN_FROM_PACKAGE=<URL>`

, the URL must resolve to the package file location in an accessible storage location, such as an Azure Blob Storage container. The container must be private to prevent unauthorized access, which requires you to use either a shared access signature (SAS) in the URL or Microsoft Entra ID authentication to allow access. Using Microsoft Entra ID with managed identities is recommended.

This is an example of setting `WEBSITE_RUN_FROM_PACKAGE`

to the URL of a deployment package in an Azure Blog Storage container:

`WEBSITE_RUN_FROM_PACKAGE=https://contosostorageaccount.blob.core.windows.net/mycontainer/mypackage.zip`


When using SAS, you append the token to the URL as a query parameter.

When you [deploy a package from Azure Blob Storage using a user-assigned managed identity](run-functions-from-deployment-package#fetch-a-package-from-azure-blob-storage-using-a-managed-identity), you must also set [ WEBSITE_RUN_FROM_PACKAGE_BLOB_MI_RESOURCE_ID](#website_run_from_package_blob_mi_resource_id) to the resource ID of the user-assigned managed identity. When you deploy from an external package URL, you must also manually sync triggers. For more information, see

[Trigger syncing](functions-deployment-technologies#trigger-syncing).

## WEBSITE_RUN_FROM_PACKAGE_BLOB_MI_RESOURCE_ID

Indicates the resource ID of a user-assigned managed identity that's used when accessing a deployment package from an external Azure Blob Storage container secured using Microsoft Entra ID. This setting requires that [ WEBSITE_RUN_FROM_PACKAGE](#website_run_from_package) be set to the URL of the deployment package in a private container.

Setting `WEBSITE_RUN_FROM_PACKAGE_BLOB_MI_RESOURCE_ID=SystemAssigned`

is the same as omitting the setting, in which case the system-assigned managed identity for the app is used.

## WEBSITE_SKIP_CONTENTSHARE_VALIDATION

The [WEBSITE_CONTENTAZUREFILECONNECTIONSTRING](#website_contentazurefileconnectionstring) and [WEBSITE_CONTENTSHARE](#website_contentshare) settings have extra validation checks to ensure that the app can be properly started. Creation of application settings fail when the function app can't properly call out to the downstream Storage Account or Key Vault due to networking constraints or other limiting factors. When WEBSITE_SKIP_CONTENTSHARE_VALIDATION is set to `1`

, the validation check is skipped. Otherwise, the value defaults to `0`

and the validation takes place.

| Key | Sample value |
|---|---|
| WEBSITE_SKIP_CONTENTSHARE_VALIDATION | `1` |

If validation is skipped and either the connection string or content share isn't valid, the app isn't able to start properly. In this case, functions return HTTP 500 errors. For more information, see [Troubleshoot error: "Azure Functions Runtime is unreachable"](functions-recover-storage-account).

## WEBSITE_SLOT_NAME

Read-only. Name of the current deployment slot. The name of the production slot is `Production`

.

| Key | Sample value |
|---|---|
| WEBSITE_SLOT_NAME | `Production` |

## WEBSITE_TIME_ZONE

Allows you to set the timezone for your function app.

| Key | OS | Sample value |
|---|---|---|
| WEBSITE_TIME_ZONE | Windows | `Eastern Standard Time` |
| WEBSITE_TIME_ZONE | Linux | `America/New_York` |

The default time zone used with the CRON expressions is Coordinated Universal Time (UTC). To have your CRON expression based on another time zone, create an app setting for your function app named `WEBSITE_TIME_ZONE`

.

The value of this setting depends on the operating system and plan on which your function app runs.

| Operating system | Plan | Value |
|---|---|---|
Windows |
All | Set the value to the name of the desired time zone as given by the second line from each pair given by the Windows command `tzutil.exe /L` |
Linux |
Premium Dedicated |
Set the value to the name of the desired time zone as shown in the
|

Note

`WEBSITE_TIME_ZONE`

and `TZ`

aren't currently supported when running on Linux in a [Flex Consumption](flex-consumption-plan) or [Consumption](consumption-plan) plan. In this case, the setting `WEBSITE_TIME_ZONE`

or `TZ`

can create SSL-related issues and cause metrics to stop working for your app.

For example, Eastern Time in the US (represented by `Eastern Standard Time`

(Windows) or `America/New_York`

(Linux)) currently uses UTC-05:00 during standard time and UTC-04:00 during daylight time. To have a timer trigger fire at 10:00 AM Eastern Time every day, create an app setting for your function app named `WEBSITE_TIME_ZONE`

, set the value to `Eastern Standard Time`

(Windows) or `America/New_York`

(Linux), and then use the following NCRONTAB expression:

```
"0 0 10 * * *"
```


When you use `WEBSITE_TIME_ZONE`

, the time is adjusted for time changes in the specific timezone, including daylight saving time and changes in standard time.

## WEBSITE_USE_PLACEHOLDER

Indicates whether to use a specific [cold start](event-driven-scaling#cold-start) optimization when running on the [Consumption plan](consumption-plan). Set to `0`

to disable the cold-start optimization on the Consumption plan.

| Key | Sample value |
|---|---|
| WEBSITE_USE_PLACEHOLDER | `1` |

## WEBSITE_USE_PLACEHOLDER_DOTNETISOLATED

Indicates whether to use a specific [cold start](event-driven-scaling#cold-start) optimization when running .NET isolated worker process functions on the [Consumption plan](consumption-plan). Set to `0`

to disable the cold-start optimization on the Consumption plan.

| Key | Sample value |
|---|---|
| WEBSITE_USE_PLACEHOLDER_DOTNETISOLATED | `1` |

## WEBSITE_VNET_ROUTE_ALL

Important

WEBSITE_VNET_ROUTE_ALL is a legacy app setting that has been replaced by the [vnetRouteAllEnabled](#vnetrouteallenabled) site setting.

Indicates whether all outbound traffic from the app is routed through the virtual network. A setting value of `1`

indicates that all application traffic is routed through the virtual network. You need this setting when configuring [Regional virtual network integration](functions-networking-options#regional-virtual-network-integration) in the Elastic Premium and Dedicated hosting plans. It's also used when a [virtual network NAT gateway is used to define a static outbound IP address](functions-how-to-use-nat-gateway).

| Key | Sample value |
|---|---|
| WEBSITE_VNET_ROUTE_ALL | `1` |

## WEBSITES_ENABLE_APP_SERVICE_STORAGE

Indicates whether the `/home`

directory is shared across scaled instances, with a default value of `true`

. You should set this value to `false`

when deploying your function app in a container.

## App Service site settings

Some configurations must be maintained at the App Service level as site settings, such as language versions. These settings are managed in the Azure portal, by using REST APIs, or by using Azure CLI or Azure PowerShell. The following are site settings that could be required, depending on your runtime language, OS, and versions.

## AcrUseManagedIdentityCreds

Indicates whether the image is obtained from an Azure Container Registry instance using managed identity authentication. A value of `true`

requires that you use managed identity. We recommend this approach over stored authentication credentials as a security best practice.

## AcrUserManagedIdentityID

Indicates the managed identity to use when obtaining the image from an Azure Container Registry instance. Requires that `AcrUseManagedIdentityCreds`

is set to `true`

. These values are valid:

| Value | Description |
|---|---|
`system` |
The system assigned managed identity of the function app is used. |
`<USER_IDENTITY_RESOURCE_ID>` |
The fully qualified resource ID of a user-assigned managed identity. |

The identity that you specify must be added to the `ACRPull`

role in the container registry. For more information, see [Create and configure a function app on Azure with the image](functions-deploy-container-apps?tabs=acr#create-and-configure-a-function-app-on-azure-with-the-image).

## alwaysOn

On a function app running in a [Dedicated (App Service) plan](dedicated-plan), the Functions runtime goes idle after a few minutes of inactivity, a which point only requests to an HTTP trigger *wakes up* your function app. To make sure that your non-HTTP triggered functions run correctly, including Timer trigger functions, enable Always On for the function app by setting the `alwaysOn`

site setting to a value of `true`

.

## functionsRuntimeAdminIsolationEnabled

Determines whether the built-in administrator (`/admin`

) endpoints in your function app can be accessed. When set to `false`

(the default), the app allows requests to endpoints under `/admin`

when those requests present a [master key](function-keys-how-to#understand-keys) in the request. When `true`

, `/admin`

endpoints can't be accessed, even with a master key.

This property can't be set for apps running on Linux in a Consumption plan. It can't be set for apps running on version 1.x of Azure Functions. If you're using version 1.x, you must first [migrate to version 4.x](migrate-version-1-version-4).

## linuxFxVersion

For function apps running on Linux, `linuxFxVersion`

indicates the language and version for the language-specific worker process. This information is used, along with [ FUNCTIONS_EXTENSION_VERSION](#functions_extension_version), to determine which specific Linux container image is installed to run your function app. This setting can be set to a predefined value or a custom image URI.

This value is set for you when you create your Linux function app. You might need to set it for ARM template and Bicep deployments and in certain upgrade scenarios.

### Valid linuxFxVersion values

You can use the following Azure CLI command to see a table of current `linuxFxVersion`

values, by supported Functions runtime version:

```
az functionapp list-runtimes --os linux --query "[].{stack:join(' ', [runtime, version]), LinuxFxVersion:linux_fx_version, SupportedFunctionsVersions:to_string(supported_functions_versions[])}" --output table
```


The previous command requires you to upgrade to version 2.40 of the Azure CLI.

### Custom images

When you create and maintain your own custom Linux container for your function app, the `linuxFxVersion`

value is instead in the format `DOCKER|<IMAGE_URI>`

, as in the following example:

```
linuxFxVersion = "DOCKER|contoso.com/azurefunctionsimage:v1.0.0"
```


This example indicates the registry source of the deployed container. For more information, see [Working with containers and Azure Functions](functions-how-to-custom-container).

Important

When you create your own containers, you're required to keep the base image of your container updated to the latest supported base image. Supported base images for Azure Functions are language-specific. See the [Azure Functions base image repos](https://mcr.microsoft.com/catalog?search=functions).

The Functions team is committed to publishing monthly updates for these base images. Regular updates include the latest minor version updates and security fixes for both the Functions runtime and languages. You should regularly update your container from the latest base image and redeploy the updated version of your container. For more information, see [Maintaining custom containers](container-concepts#maintaining-custom-containers).

## netFrameworkVersion

Sets the specific version of .NET for C# functions. For more information, see [Update your function app in Azure](migrate-version-3-version-4?pivots=programming-language-csharp#update-your-function-app-in-azure).

## powerShellVersion

Sets the specific version of PowerShell on which your functions run. For more information, see [Changing the PowerShell version](functions-reference-powershell#changing-the-powershell-version).

When running locally, you instead use the [ FUNCTIONS_WORKER_RUNTIME_VERSION](functions-reference-powershell#running-local-on-a-specific-version) setting in the local.settings.json file.

## vnetContentShareEnabled

Apps running in a Premium plan use a file share to store content. The name of this content share is stored in the [ WEBSITE_CONTENTSHARE](#website_contentshare) app setting and its connection string is stored in

[. To route traffic between your function app and content share through a virtual network, you must also set](#website_contentazurefileconnectionstring)

`WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

`vnetContentShareEnabled`

to `true`

. Enabling this site property is required for cross-stamp scaling when [restricting your storage account to a virtual network](configure-networking-how-to#restrict-your-storage-account-to-a-virtual-network)in the Elastic Premium and Dedicated hosting plans. Without this setting, the function app can only scale within a single stamp (approximately 1-20 instances).

Note

You must take special care when routing to the content share in a storage account shared by multiple function apps in the same plan. For more information, see [Consistent routing through virtual networks](storage-considerations#consistent-routing-through-virtual-networks) in the Storage considerations article.

This site property replaces the legacy [ WEBSITE_CONTENTOVERVNET](#website_contentovervnet) setting.

## vnetImagePullEnabled

Functions [supports function apps running in Linux containers](functions-how-to-custom-container). To connect and pull from a container registry inside a virtual network, you must set `vnetImagePullEnabled`

to `true`

. This site property is supported in the Elastic Premium and Dedicated hosting plans. The Flex Consumption plan doesn't rely on site properties or app settings to configure Networking. For more information, see [Flex Consumption plan deprecations](#flex-consumption-plan-deprecations).

## vnetRouteAllEnabled

Indicates whether all outbound traffic from the app is routed through the virtual network. A setting value of `true`

indicates that all application traffic is routed through the virtual network. Use this setting when configuring [Regional virtual network integration](functions-networking-options#regional-virtual-network-integration) in the Elastic Premium and Dedicated plans. It's also used when a [virtual network NAT gateway is used to define a static outbound IP address](functions-how-to-use-nat-gateway). For more information, see [Configure application routing](../app-service/configure-vnet-integration-routing#configure-application-routing).

This site setting replaces the legacy [WEBSITE_VNET_ROUTE_ALL](#website_vnet_route_all) setting.

## Flex Consumption plan deprecations

In the [Flex Consumption plan](flex-consumption-plan), these site properties and application settings are deprecated and shouldn't be used when creating function app resources:

| Setting/property | Reason |
|---|---|
`ENABLE_ORYX_BUILD` |
Replaced by the `remoteBuild` parameter when deploying in Flex Consumption |
`FUNCTIONS_EXTENSION_VERSION` |
App Setting is set by the backend. A value of ~1 can be ignored. |
`FUNCTIONS_WORKER_RUNTIME` |
Replaced by `name` in `properties.functionAppConfig.runtime` |
`FUNCTIONS_WORKER_RUNTIME_VERSION` |
Replaced by `version` in `properties.functionAppConfig.runtime` |
`FUNCTIONS_MAX_HTTP_CONCURRENCY` |
Replaced by scale and concurrency's trigger section |
`FUNCTIONS_WORKER_PROCESS_COUNT` |
Setting not valid |
`FUNCTIONS_WORKER_DYNAMIC_CONCURRENCY_ENABLED` |
Setting not valid |
`SCM_DO_BUILD_DURING_DEPLOYMENT` |
Replaced by the `remoteBuild` parameter when deploying in Flex Consumption |
`WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` |
Replaced by functionAppConfig's deployment section |
`WEBSITE_CONTENTOVERVNET` |
Not used for networking in Flex Consumption |
`WEBSITE_CONTENTSHARE` |
Replaced by functionAppConfig's deployment section |
`WEBSITE_DNS_SERVER` |
DNS is inherited from the integrated virtual network in Flex |
`WEBSITE_MAX_DYNAMIC_APPLICATION_SCALE_OUT` |
Replaced by `maximumInstanceCount` in `properties.functionAppConfig.scaleAndConcurrency` |
`WEBSITE_NODE_DEFAULT_VERSION` |
Replaced by `version` in `properties.functionAppConfig.runtime` |
`WEBSITE_RUN_FROM_PACKAGE` |
Not used for deployments in Flex Consumption |
`WEBSITE_SKIP_CONTENTSHARE_VALIDATION` |
Content share isn't used in Flex Consumption |
`WEBSITE_VNET_ROUTE_ALL` |
Not used for networking in Flex Consumption |
`properties.alwaysOn` |
Not valid |
`properties.containerSize` |
Renamed as `instanceMemoryMB` |
`properties.ftpsState` |
FTPS not supported |
`properties.isReserved` |
Not valid |
`properties.IsXenon` |
Not valid |
`properties.javaVersion` |
Replaced by `version` in `properties.functionAppConfig.runtime` |
`properties.LinuxFxVersion` |
Replaced by `properties.functionAppConfig.runtime` |
`properties.netFrameworkVersion` |
Replaced by `version` in `properties.functionAppConfig.runtime` |
`properties.powerShellVersion` |
Replaced by `version` in `properties.functionAppConfig.runtime` |
`properties.siteConfig.functionAppScaleLimit` |
Renamed as `maximumInstanceCount` |
`properties.siteConfig.preWarmedInstanceCount` |
Renamed as `alwaysReadyInstances` |
`properties.use32BitWorkerProcess` |
32-bit not supported |
`properties.vnetBackupRestoreEnabled` |
Not used for networking in Flex Consumption |
`properties.vnetContentShareEnabled` |
Not used for networking in Flex Consumption |
`properties.vnetImagePullEnabled` |
Not used for networking in Flex Consumption |
`properties.vnetRouteAllEnabled` |
Not used for networking in Flex Consumption |
`properties.windowsFxVersion` |
Not valid |
