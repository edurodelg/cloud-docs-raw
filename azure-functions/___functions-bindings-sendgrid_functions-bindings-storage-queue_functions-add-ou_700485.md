---
merged_at: 2026-01-25T15:41:11.639224
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __functions-bindings-sendgrid_functions-bindings-storage-queue_functions-add-out_141468.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-sendgrid_functions-bindings-storage-queue.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-sendgrid.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-sendgrid -->

# Azure Functions SendGrid bindings

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to send email by using [SendGrid](https://sendgrid.com/docs/User_Guide/index.html) bindings in Azure Functions. Azure Functions supports an output binding for SendGrid.

This is reference information for Azure Functions developers. If you're new to Azure Functions, start with the following resources:

C# developer references:


## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

Add the extension to your project by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.SendGrid), version 3.x.

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

## Example

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

We don't currently have an example for using the SendGrid binding in a function app running in an isolated worker process.

The following example shows a SendGrid output binding in a *function.json* file and a [JavaScript function](functions-reference-node) that uses the binding.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"name": "$return",
"type": "sendGrid",
"direction": "out",
"apiKey" : "MySendGridKey",
"to": "{ToEmail}",
"from": "{FromEmail}",
"subject": "SendGrid output bindings"
}
]
}
```


The [configuration](#configuration) section explains these properties.

Here's the JavaScript code:

```
module.exports = function (context, input) {
var message = {
"personalizations": [ { "to": [ { "email": "sample@sample.com" } ] } ],
from: { email: "sender@contoso.com" },
subject: "Azure news",
content: [{
type: 'text/plain',
value: input
}]
};
return message;
};
```


Complete PowerShell examples aren't currently available for SendGrid bindings.

The following example shows an HTTP-triggered function that sends an email using the SendGrid binding. You can provide default values in the binding configuration. For instance, the *from* email address is configured in *function.json*.

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"type": "httpTrigger",
"authLevel": "function",
"direction": "in",
"name": "req",
"methods": ["get", "post"]
},
{
"type": "http",
"direction": "out",
"name": "$return"
},
{
"type": "sendGrid",
"name": "sendGridMessage",
"direction": "out",
"apiKey": "SendGrid_API_Key",
"from": "sender@contoso.com"
}
]
}
```


The following function shows how you can provide custom values for optional properties.

```
import logging
import json
import azure.functions as func
def main(req: func.HttpRequest, sendGridMessage: func.Out[str]) -> func.HttpResponse:
value = "Sent from Azure Functions"
message = {
"personalizations": [ {
"to": [{
"email": "user@contoso.com"
}]}],
"subject": "Azure Functions email with SendGrid",
"content": [{
"type": "text/plain",
"value": value }]}
sendGridMessage.set(json.dumps(message))
return func.HttpResponse(f"Sent")
```


The following example uses the `@SendGridOutput`

annotation from the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime) to send an email using the SendGrid output binding.

```
package com.function;
import java.util.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.*;
public class HttpTriggerSendGrid {
@FunctionName("HttpTriggerSendGrid")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = { HttpMethod.GET, HttpMethod.POST },
authLevel = AuthorizationLevel.FUNCTION)
HttpRequestMessage<Optional<String>> request,
@SendGridOutput(
name = "message",
dataType = "String",
apiKey = "SendGrid_API_Key",
to = "user@contoso.com",
from = "sender@contoso.com",
subject = "Azure Functions email with SendGrid",
text = "Sent from Azure Functions")
OutputBinding<String> message,
final ExecutionContext context) {
final String toAddress = "user@contoso.com";
final String value = "Sent from Azure Functions";
StringBuilder builder = new StringBuilder()
.append("{")
.append("\"personalizations\": [{ \"to\": [{ \"email\": \"%s\"}]}],")
.append("\"content\": [{\"type\": \"text/plain\", \"value\": \"%s\"}]")
.append("}");
final String body = String.format(builder.toString(), toAddress, value);
message.setValue(body);
return request.createResponseBuilder(HttpStatus.OK).body("Sent").build();
}
}
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the output binding. C# script instead uses a function.json configuration file.

In [isolated worker process](dotnet-isolated-process-guide) function apps, the `SendGridOutputAttribute`

supports the following parameters:

| Attribute/annotation property | Description |
|---|---|
ApiKey |
The name of an app setting that contains your API key. If not set, the default app setting name is `AzureWebJobsSendGridApiKey` . |
To |
(Optional) The recipient's email address. |
From |
(Optional) The sender's email address. |
Subject |
(Optional) The subject of the email. |
Text |
(Optional) The email content. |

## Annotations

The [SendGridOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.sendgridoutput) annotation allows you to declaratively configure the SendGrid binding by providing the following configuration values.

## Configuration

The following table lists the binding configuration properties available in the *function.json* file and the `SendGrid`

attribute/annotation.

function.json property |
Description |
|---|---|
type |
Must be set to `sendGrid` . |
direction |
Must be set to `out` . |
name |
The variable name used in function code for the request or request body. This value is `$return` when there's only one return value. |
apiKey |
The name of an app setting that contains your API key. If not set, the default app setting name is AzureWebJobsSendGridApiKey. |
to |
(Optional) The recipient's email address. |
from |
(Optional) The sender's email address. |
subject |
(Optional) The subject of the email. |
text |
(Optional) The email content. |

Optional properties may have default values defined in the binding and either added or overridden programmatically.

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## host.json settings

This section describes the configuration settings available for this binding in version 2.x and later. Settings in the host.json file apply to all functions in a function app instance. For more information about function app configuration settings, see [host.json reference for Azure Functions](functions-host-json).

Note

For a reference of host.json in Functions 1.x, see [host.json reference for Azure Functions 1.x](functions-host-json-v1).

```
{
"version": "2.0",
"extensions": {
"sendGrid": {
"from": "Azure Functions <samples@functions.com>"
}
}
}
```


| Property | Default | Description |
|---|---|---|
from |
n/a | The sender's email address across all functions. |


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-storage-queue.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-queue -->

# Azure Queue storage trigger and bindings for Azure Functions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions can run as new Azure Queue storage messages are created and can write queue messages within a function.

| Action | Type |
|---|---|
| Run a function as queue storage data changes |
|

[Output binding](functions-bindings-storage-queue-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

This version introduces the ability to [connect using an identity instead of a secret](functions-reference#configure-an-identity-based-connection). For a tutorial on configuring your function apps with managed identities, see the [creating a function app with identity-based connections tutorial](functions-identity-based-connections-tutorial).

This version allows you to bind to types from [Azure.Storage.Queues](/en-us/dotnet/api/azure.storage.queues).

This version supports configuration of triggers and bindings through [.NET Aspire integration](dotnet-aspire-integration#connection-configuration-with-aspire).

Add the extension to your project by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues), version 5.x.

Using the .NET CLI:

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues
```


Note

Azure Blobs, Azure Queues, and Azure Tables now use separate extensions and are referenced individually. For example, to use the triggers and bindings for all three services in your .NET isolated-process app, you should add the following packages to your project:

[Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs)[Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues)[Microsoft.Azure.Functions.Worker.Extensions.Tables](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Tables)

Previously, the extensions shipped together as [Microsoft.Azure.Functions.Worker.Extensions.Storage, version 4.x](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage/4.0.4). This same package also has a [5.x version](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage/5.0.0), which references the split packages for blobs and queues only. When upgrading your package references from older versions, you may therefore need to additionally reference the new [Microsoft.Azure.Functions.Worker.Extensions.Tables](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Tables) NuGet package. Also, when referencing these newer split packages, make sure you are not referencing an older version of the combined storage package, as this will result in conflicts from two definitions of the same bindings.

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

The isolated worker process supports parameter types according to the tables below. Support for binding to types from [Azure.Storage.Queues](/en-us/dotnet/api/azure.storage.queues) is in preview.

**Queue trigger**

The queue trigger can bind to the following types:

| Type | Description |
|---|---|
`string` |
The message content as a string. Use when the message is simple text.. |
`byte[]` |
The bytes of the message. |
| JSON serializable types | When a queue message contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

[BinaryData](/en-us/dotnet/api/system.binarydata)11 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues 5.2.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues/5.2.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

**Queue output binding**

When you want the function to write a single message, the queue output binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The message content as a string. Use when the message is simple text. |
`byte[]` |
The bytes of the message. |
| JSON serializable types | An object representing the content of a JSON message. Functions tries to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write multiple messages, the queue output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single message types |
An array containing content for multiple messages. Each entry represents one message. |

For other output scenarios, create and use a [QueueClient](/en-us/dotnet/api/azure.storage.queues.queueclient) with other types from [Azure.Storage.Queues](/en-us/dotnet/api/azure.storage.queues) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

## host.json settings

This section describes the configuration settings available for this binding in version 2.x and later. Settings in the host.json file apply to all functions in a function app instance. For more information about function app configuration settings, see [host.json reference for Azure Functions](functions-host-json).

Note

For a reference of host.json in Functions 1.x, see [host.json reference for Azure Functions 1.x](functions-host-json-v1).

```
{
"version": "2.0",
"extensions": {
"queues": {
"maxPollingInterval": "00:00:02",
"visibilityTimeout" : "00:00:30",
"batchSize": 16,
"maxDequeueCount": 5,
"newBatchThreshold": 8,
"messageEncoding": "base64"
}
}
}
```


| Property | Default | Description |
|---|---|---|
| maxPollingInterval | 00:01:00 | The maximum interval between queue polls. The minimum interval is 00:00:00.100 (100 ms). Intervals increment up to `maxPollingInterval` . The default value of `maxPollingInterval` is 00:01:00 (1 min). `maxPollingInterval` must not be less than 00:00:00.100 (100 ms). In Functions 2.x and later, the data type is a `TimeSpan` . In Functions 1.x, it is in milliseconds. |
| visibilityTimeout | 00:00:00 | The time interval between retries when processing of a message fails. |
| batchSize | 16 | The number of queue messages that the Functions runtime retrieves simultaneously and processes in parallel. When the number being processed gets down to the `newBatchThreshold` , the runtime gets another batch and starts processing those messages. So the maximum number of concurrent messages being processed per function is `batchSize` plus `newBatchThreshold` . This limit applies separately to each queue-triggered function. If you want to avoid parallel execution for messages received on one queue, you can set `batchSize` to 1. However, this setting eliminates concurrency as long as your function app runs only on a single virtual machine (VM). If the function app scales out to multiple VMs, each VM could run one instance of each queue-triggered function.The maximum `batchSize` is 32. |
| maxDequeueCount | 5 | The number of times to try processing a message before moving it to the poison queue. |
| newBatchThreshold | N*batchSize/2 | Whenever the number of messages being processed concurrently gets down to this number, the runtime retrieves another batch.`N` represents the number of vCPUs available when running on App Service or Premium Plans. Its value is `1` for the Consumption Plan. |
| messageEncoding | base64 | This setting is only available in
`base64` and `none` . |


---

<!-- DOCUMENTO FUSIONADO: functions-add-output-binding-cosmos-db-vs-code.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-add-output-binding-cosmos-db-vs-code -->

# Connect Azure Functions to Azure Cosmos DB using Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions lets you connect Azure services and other resources to functions without having to write your own integration code. These *bindings*, which represent both input and output, are declared within the function definition. Data from bindings is provided to the function as parameters. A *trigger* is a special type of input binding. Although a function has only one trigger, it can have multiple input and output bindings. To learn more, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings).

This article shows you how to use Visual Studio Code to connect [Azure Cosmos DB](/en-us/azure/cosmos-db/introduction) to the function you created in the previous quickstart article. The output binding that you add to this function writes data from the HTTP request to a JSON document stored in an Azure Cosmos DB container.

Before you begin, you must complete the [quickstart: Create a C# function in Azure using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-csharp). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

Before you begin, you must complete the [quickstart: Create a JavaScript function in Azure using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-javascript?pivot=nodejs-model-v3). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

Note

This article currently only supports [Node.js v3 for Functions](functions-reference-node?pivots=nodejs-model-v3).

Before you begin, you must complete the [quickstart: Create a Python function in Azure using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-python). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

## Configure your environment

Before you get started, make sure to install the [Azure Databases extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-cosmosdb) for Visual Studio Code.

## Create your Azure Cosmos DB account

Now, you create an Azure Cosmos DB account as a [serverless account type](/en-us/azure/cosmos-db/serverless). This consumption-based mode makes Azure Cosmos DB a strong option for serverless workloads.

In Visual Studio Code, select

**View**>**Command Palette...**then in the command palette search for`Azure Databases: Create Server...`

Provide the following information at the prompts:

Prompt Selection **Select an Azure Database Server**Choose **Core (NoSQL)**to create a document database that you can query by using a SQL syntax or a Query Copilot ([Preview](/en-us/azure/cosmos-db/nosql/query/how-to-enable-use-copilot)) converting natural language prompts to queries.[Learn more about the Azure Cosmos DB](/en-us/azure/cosmos-db/introduction).**Account name**Enter a unique name to identify your Azure Cosmos DB account. The account name can use only lowercase letters, numbers, and hyphens (-), and must be between 3 and 31 characters long. **Select a capacity model**Select **Serverless**to create an account in[serverless](/en-us/azure/cosmos-db/serverless)mode.**Select a resource group for new resources**Choose the resource group where you created your function app in the [previous article](how-to-create-function-vs-code?pivot=programming-language-csharp).**Select a location for new resources**Select a geographic location to host your Azure Cosmos DB account. Use the location that's closest to you or your users to get the fastest access to your data. After your new account is provisioned, a message is displayed in notification area.


## Create an Azure Cosmos DB database and container

Select the Azure icon in the Activity bar, expand

**Resources**>**Azure Cosmos DB**, right-click (Ctrl+select on macOS) your account, and select**Create database...**.Provide the following information at the prompts:

Prompt Selection **Database name**Type `my-database`

.**Enter and ID for your collection**Type `my-container`

.**Enter the partition key for the collection**Type `/id`

as the[partition key](/en-us/azure/cosmos-db/partitioning-overview).Select

**OK**to create the container and database.

## Update your function app settings

In the [previous quickstart article](how-to-create-function-vs-code?pivot=programming-language-csharp), you created a function app in Azure. In this article, you update your app to write JSON documents to the Azure Cosmos DB container you've created. To connect to your Azure Cosmos DB account, you must add its connection string to your app settings. You then download the new setting to your local.settings.json file so you can connect to your Azure Cosmos DB account when running locally.

In Visual Studio Code, right-click (Ctrl+select on macOS) on your new Azure Cosmos DB account, and select

**Copy Connection String**.Press

`F1`to open the command palette, then search for and run the command`Azure Functions: Add New Setting...`

.Choose the function app you created in the previous article. Provide the following information at the prompts:

Prompt Selection **Enter new app setting name**Type `CosmosDbConnectionString`

.**Enter value for "CosmosDbConnectionString"**Paste the connection string of your Azure Cosmos DB account you copied. You can also configure [Microsoft Entra identity](functions-bindings-cosmosdb-v2-trigger#connections)as an alternative.This creates an application setting named connection

`CosmosDbConnectionString`

in your function app in Azure. Now, you can download this setting to your local.settings.json file.Press

`F1`again to open the command palette, then search for and run the command`Azure Functions: Download Remote Settings...`

.Choose the function app you created in the previous article. Select

**Yes to all**to overwrite the existing local settings.

This downloads all of the setting from Azure to your local project, including the new connection string setting. Most of the downloaded settings aren't used when running locally.

## Register binding extensions

Because you're using an Azure Cosmos DB output binding, you must have the corresponding bindings extension installed before you run the project.

Except for HTTP and timer triggers, bindings are implemented as extension packages. Run the following [dotnet add package](/en-us/dotnet/core/tools/dotnet-add-package) command in the Terminal window to add the Azure Cosmos DB extension package to your project.

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.CosmosDB
```


Your project has been configured to use [extension bundles](extension-bundles), which automatically installs a predefined set of extension packages.

Extension bundles usage is enabled in the *host.json* file at the root of the project, which appears as follows:

```
{
"version": "2.0",
"logging": {
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"excludedTypes": "Request"
}
}
},
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
},
"concurrency": {
"dynamicConcurrencyEnabled": true,
"snapshotPersistenceEnabled": true
},
"extensions": {
"cosmosDB": {
"connectionMode": "Gateway"
}
}
}
```


Your project has been configured to use [extension bundles](extension-bundles), which automatically installs a predefined set of extension packages.

Extension bundles usage is enabled in the *host.json* file at the root of the project, which appears as follows:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[3.*, 4.0.0)"
}
}
```


Now, you can add the Azure Cosmos DB output binding to your project.

## Add an output binding

In a C# class library project, the bindings are defined as binding attributes on the function method.

Open the *HttpExample.cs* project file and add the following classes:

```
public class MultiResponse
{
[CosmosDBOutput("my-database", "my-container",
Connection = "CosmosDbConnectionSetting", CreateIfNotExists = true)]
public MyDocument Document { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
public class MyDocument {
public string id { get; set; }
public string message { get; set; }
}
```


The `MyDocument`

class defines an object that gets written to the database. The connection string for the Storage account is set by the `Connection`

property. In this case, you could omit `Connection`

because you're already using the default storage account.

The `MultiResponse`

class allows you to both write to the specified collection in the Azure Cosmos DB and return an HTTP success message. Because you need to return a `MultiResponse`

object, you need to also update the method signature.

Specific attributes specify the name of the container and the name of its parent database. The connection string for your Azure Cosmos DB account is set by the `CosmosDbConnectionString`

.

Binding attributes are defined directly in your function code. The [Azure Cosmos DB output configuration](functions-bindings-cosmosdb-v2-output#configuration) describes the fields required for an Azure Cosmos DB output binding.

For this `MultiResponse`

scenario, you need to add an `extraOutputs`

output binding to the function.

```
app.http('HttpExample', {
methods: ['GET', 'POST'],
extraOutputs: [sendToCosmosDb],
handler: async (request, context) => {
```


Add the following properties to the binding configuration:

```
const sendToCosmosDb = output.cosmosDB({
databaseName: 'my-database',
containerName: 'my-container',
createIfNotExists: false,
connection: 'CosmosDBConnectionString',
});
```


Binding attributes are defined directly in the *function_app.py* file. You use the `cosmos_db_output`

decorator to add an [Azure Cosmos DB output binding](functions-bindings-triggers-python#azure-cosmos-db-output-binding):

```
@app.cosmos_db_output(arg_name="outputDocument", database_name="my-database",
container_name="my-container", connection="CosmosDbConnectionString")
```


In this code, `arg_name`

identifies the binding parameter referenced in your code, `database_name`

and `container_name`

are the database and collection names that the binding writes to, and `connection`

is the name of an application setting that contains the connection string for the Azure Cosmos DB account, which is in the `CosmosDbConnectionString`

setting in the *local.settings.json* file.

## Add code that uses the output binding

Replace the existing Run method with the following code:

```
[Function("HttpExample")]
public static MultiResponse Run([HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequestData req,
FunctionContext executionContext)
{
var logger = executionContext.GetLogger("HttpExample");
logger.LogInformation("C# HTTP trigger function processed a request.");
var message = "Welcome to Azure Functions!";
var response = req.CreateResponse(HttpStatusCode.OK);
response.Headers.Add("Content-Type", "text/plain; charset=utf-8");
response.WriteString(message);
// Return a response to both HTTP trigger and Azure Cosmos DB output binding.
return new MultiResponse()
{
Document = new MyDocument
{
id = System.Guid.NewGuid().ToString(),
message = message
},
HttpResponse = response
};
}
```


Add code that uses the `extraInputs`

output binding object on `context`

to send a JSON document to the named output binding function, `sendToCosmosDb`

. Add this code before the `return`

statement.

```
context.extraOutputs.set(sendToCosmosDb, {
// create a random ID
id:
new Date().toISOString() + Math.random().toString().substring(2, 10),
name: name,
});
```


At this point, your function should look as follows:

```
const { app, output } = require('@azure/functions');
const sendToCosmosDb = output.cosmosDB({
databaseName: 'my-database',
containerName: 'my-container',
createIfNotExists: false,
connection: 'CosmosDBConnectionString',
});
app.http('HttpExampleToCosmosDB', {
methods: ['GET', 'POST'],
extraOutputs: [sendToCosmosDb],
handler: async (request, context) => {
try {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text());
if (!name) {
return { status: 404, body: 'Missing required data' };
}
// Output to Database
context.extraOutputs.set(sendToCosmosDb, {
// create a random ID
id:
new Date().toISOString() + Math.random().toString().substring(2, 10),
name: name,
});
const responseMessage = name
? 'Hello, ' +
name +
'. This HTTP triggered function executed successfully.'
: 'This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response.';
// Return to HTTP client
return { body: responseMessage };
} catch (error) {
context.log(`Error: ${error}`);
return { status: 500, body: 'Internal Server Error' };
}
},
});
```


This code now returns a `MultiResponse`

object that contains both a document and an HTTP response.

Update *HttpExample\function_app.py* to match the following code. Add the `outputDocument`

parameter to the function definition and `outputDocument.set()`

under the `if name:`

statement:

```
import azure.functions as func
import logging
app = func.FunctionApp()
@app.function_name(name="HttpTrigger1")
@app.route(route="hello", auth_level=func.AuthLevel.FUNCTION)
@app.queue_output(arg_name="msg", queue_name="outqueue", connection="AzureWebJobsStorage")
@app.cosmos_db_output(arg_name="outputDocument", database_name="my-database", container_name="my-container", connection="CosmosDbConnectionString")
def test_function(req: func.HttpRequest, msg: func.Out[func.QueueMessage],
outputDocument: func.Out[func.Document]) -> func.HttpResponse:
logging.info('Python HTTP trigger function processed a request.')
logging.info('Python Cosmos DB trigger function processed a request.')
name = req.params.get('name')
if not name:
try:
req_body = req.get_json()
except ValueError:
pass
else:
name = req_body.get('name')
if name:
outputDocument.set(func.Document.from_dict({"id": name}))
msg.set(name)
return func.HttpResponse(f"Hello {name}!")
else:
return func.HttpResponse(
"Please pass a name on the query string or in the request body",
status_code=400
)
```


The document `{"id": "name"}`

is created in the database collection specified in the binding.

## Run the function locally

Visual Studio Code integrates with [Azure Functions Core tools](functions-run-local) to let you run this project on your local development computer before you publish to Azure. If you don't already have Core Tools installed locally, you are prompted to install it the first time you run your project.

To call your function, press

`F5`to start the function app project. The**Terminal**panel displays the output from Core Tools. Your app starts in the**Terminal**panel. You can see the URL endpoint of your HTTP-triggered function running locally.If you don't already have Core Tools installed, select

**Install**to install Core Tools when prompted to do so.

If you have trouble running on Windows, make sure that the default terminal for Visual Studio Code isn't set to**WSL Bash**.With the Core Tools running, go to the

**Azure: Functions**area. Under**Functions**, expand**Local Project**>**Functions**. Right-click (Windows) or`Ctrl -`click (macOS) the`HttpExample`

function and choose**Execute Function Now...**.In the

**Enter request body**, press`Enter`to send a request message to your function.When the function executes locally and returns a response, a notification is raised in Visual Studio Code. Information about the function execution is shown in the

**Terminal**panel.Press

`Ctrl + C`to stop Core Tools and disconnect the debugger.

## Run the function locally

As in the previous article, press

`F5`to start the function app project and Core Tools.With Core Tools running, go to the

**Azure: Functions**area. Under**Functions**, expand**Local Project**>**Functions**. Right-click (Ctrl-click on Mac) the`HttpExample`

function and choose**Execute Function Now...**.In

**Enter request body**you see the request message body value of`{ "name": "Azure" }`

. Press Enter to send this request message to your function.After a response is returned, press

`Ctrl + C`to stop Core Tools.

### Verify that a JSON document has been created

On the Azure portal, go back to your Azure Cosmos DB account and select

**Data Explorer**.Expand your database and container, and select

**Items**to list the documents created in your container.Verify that a new JSON document has been created by the output binding.


## Redeploy and verify the updated app

In Visual Studio Code, press F1 to open the command palette. In the command palette, search for and select

`Azure Functions: Deploy to function app...`

.Choose the function app that you created in the first article. Because you're redeploying your project to the same app, select

**Deploy**to dismiss the warning about overwriting files.After deployment completes, you can again use the

**Execute Function Now...**feature to trigger the function in Azure. This command automatically retrieves the function access key and uses it when calling the HTTP trigger endpoint.Again

[check the documents created in your Azure Cosmos DB container](#verify-that-a-json-document-has-been-created)to verify that the output binding again generates a new JSON document.

## Clean up resources

In Azure, *resources* refer to function apps, functions, storage accounts, and so forth. They're grouped into *resource groups*, and you can delete everything in a group by deleting the group.

You created resources to complete these quickstarts. You might be billed for these resources, depending on your [account status](https://azure.microsoft.com/account/) and [service pricing](https://azure.microsoft.com/pricing/). If you don't need the resources anymore, here's how to delete them:

In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azure: Open in portal`

.Choose your function app and press

`Enter`. The function app page opens in the Azure portal.In the

**Overview**tab, select the named link next to**Resource group**.On the

**Resource group**page, review the list of included resources, and verify that they're the ones you want to delete.Select

**Delete resource group**, and follow the instructions.Deletion may take a couple of minutes. When it's done, a notification appears for a few seconds. You can also select the bell icon at the top of the page to view the notification.


## Next steps

You've updated your HTTP triggered function to write JSON documents to an Azure Cosmos DB container. Now you can learn more about developing Functions using Visual Studio Code:


---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-event-iot-trigger_flex-consumption-plan.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-event-iot-trigger.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-iot-trigger -->

# Azure IoT Hub trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to work with Azure Functions bindings for IoT Hub. The IoT Hub support is based on the [Azure Event Hubs Binding](functions-bindings-event-hubs).

For information on setup and configuration details, see the [overview](functions-bindings-event-iot).

Important

While the following code samples use the Event Hub API, the given syntax is applicable for IoT Hub functions.

Use the function trigger to respond to an event sent to an event hub event stream. You need read access to the underlying event hub to set up the trigger. When the function is triggered, the message passed to the function is typed as a string.

Event Hubs scaling decisions for the Consumption and Premium plans are done via Target Based Scaling. For more information, see [Target Based Scaling](functions-target-based-scaling).

For information about how Azure Functions responds to events sent to an event hub event stream using triggers, see [Integrate Event Hubs with serverless functions on Azure](/en-us/azure/architecture/serverless/event-hubs-functions/event-hubs-functions#consuming-events-with-azure-functions).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

## Example

The following example shows a [C# function](dotnet-isolated-process-guide) that is triggered based on an event hub, where the input message string is written to the logs:

```
{
private readonly ILogger<EventHubsFunction> _logger;
public EventHubsFunction(ILogger<EventHubsFunction> logger)
{
_logger = logger;
}
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


The following example shows an Event Hubs trigger [TypeScript function](functions-reference-node?tabs=typescript). The function reads [event metadata](#event-metadata) and logs the message.

```
import { app, InvocationContext } from '@azure/functions';
export async function eventHubTrigger1(message: unknown, context: InvocationContext): Promise<void> {
context.log('Event hub function processed message:', message);
context.log('EnqueuedTimeUtc =', context.triggerMetadata.enqueuedTimeUtc);
context.log('SequenceNumber =', context.triggerMetadata.sequenceNumber);
context.log('Offset =', context.triggerMetadata.offset);
}
app.eventHub('eventHubTrigger1', {
connection: 'myEventHubReadConnectionAppSetting',
eventHubName: 'MyEventHub',
cardinality: 'one',
handler: eventHubTrigger1,
});
```


To receive events in a batch, set `cardinality`

to `many`

, as shown in the following example.

```
import { app, InvocationContext } from '@azure/functions';
export async function eventHubTrigger1(messages: unknown[], context: InvocationContext): Promise<void> {
context.log(`Event hub function processed ${messages.length} messages`);
for (let i = 0; i < messages.length; i++) {
context.log('Event hub message:', messages[i]);
context.log(`EnqueuedTimeUtc = ${context.triggerMetadata.enqueuedTimeUtcArray[i]}`);
context.log(`SequenceNumber = ${context.triggerMetadata.sequenceNumberArray[i]}`);
context.log(`Offset = ${context.triggerMetadata.offsetArray[i]}`);
}
}
app.eventHub('eventHubTrigger1', {
connection: 'myEventHubReadConnectionAppSetting',
eventHubName: 'MyEventHub',
cardinality: 'many',
handler: eventHubTrigger1,
});
```


The following example shows an Event Hubs trigger [JavaScript function](functions-reference-node). The function reads [event metadata](#event-metadata) and logs the message.

```
const { app } = require('@azure/functions');
app.eventHub('eventHubTrigger1', {
connection: 'myEventHubReadConnectionAppSetting',
eventHubName: 'MyEventHub',
cardinality: 'one',
handler: (message, context) => {
context.log('Event hub function processed message:', message);
context.log('EnqueuedTimeUtc =', context.triggerMetadata.enqueuedTimeUtc);
context.log('SequenceNumber =', context.triggerMetadata.sequenceNumber);
context.log('Offset =', context.triggerMetadata.offset);
},
});
```


To receive events in a batch, set `cardinality`

to `many`

, as shown in the following example.

```
const { app } = require('@azure/functions');
app.eventHub('eventHubTrigger1', {
connection: 'myEventHubReadConnectionAppSetting',
eventHubName: 'MyEventHub',
cardinality: 'many',
handler: (messages, context) => {
context.log(`Event hub function processed ${messages.length} messages`);
for (let i = 0; i < messages.length; i++) {
context.log('Event hub message:', messages[i]);
context.log(`EnqueuedTimeUtc = ${context.triggerMetadata.enqueuedTimeUtcArray[i]}`);
context.log(`SequenceNumber = ${context.triggerMetadata.sequenceNumberArray[i]}`);
context.log(`Offset = ${context.triggerMetadata.offsetArray[i]}`);
}
},
});
```


Here's the PowerShell code:

```
param($eventHubMessages, $TriggerMetadata)
Write-Host "PowerShell eventhub trigger function called for message array: $eventHubMessages"
$eventHubMessages | ForEach-Object { Write-Host "Processed message: $_" }
```


This example uses SDK types to directly access the underlying [ EventData](/en-us/python/api/azure-eventhub/azure.eventhub.eventdata) object provided by the Event Hubs trigger:

The function reads the event body and logs it.

```
import logging
import azure.functions as func
import azurefunctions.extensions.bindings.eventhub as eh
app = func.FunctionApp(http_auth_level=func.AuthLevel.FUNCTION)
@app.event_hub_message_trigger(
arg_name="event", event_hub_name="EVENTHUB_NAME", connection="EventHubConnection"
)
def eventhub_trigger(event: eh.EventData):
logging.info(
"Python EventHub trigger processed an event %s",
event.body_as_str()
)
```


For examples of using the EventData type, see the [ EventData](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-eventhub/samples/eventhub_samples_eventdata/function_app.py) samples. For a step-by-step tutorial on how to include SDK-type bindings in your function app, follow the

[Python SDK Bindings for Event Hubs Sample](https://github.com/Azure-Samples/azure-functions-eventhub-sdk-bindings-python).

Note

Known limitations include:

- The
`enqueued_time`

property is not supported. - Batch message support is supported with runtime version 4.1039 or greater.

To learn more, including what other SDK type bindings are supported, see [SDK type bindings](functions-reference-python#sdk-type-bindings).

The following example shows an Event Hubs trigger binding and a Python function that uses the binding. The function reads [event metadata](#event-metadata) and logs the message. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="EventHubTrigger1")
@app.event_hub_message_trigger(arg_name="myhub",
event_hub_name="<EVENT_HUB_NAME>",
connection="<CONNECTION_SETTING>")
def test_function(myhub: func.EventHubEvent):
logging.info('Python EventHub trigger processed an event: %s',
myhub.get_body().decode('utf-8'))
```


The following example shows an Event Hubs trigger binding which logs the message body of the Event Hubs trigger.

```
@FunctionName("ehprocessor")
public void eventHubProcessor(
@EventHubTrigger(name = "msg",
eventHubName = "myeventhubname",
connection = "myconnvarname") String message,
final ExecutionContext context )
{
context.getLogger().info(message);
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `EventHubTrigger`

annotation on parameters whose value comes from the event hub. Parameters with these annotations cause the function to run when an event arrives. This annotation can be used with native Java types, POJOs, or nullable values using `Optional<T>`

.

The following example illustrates extensive use of `SystemProperties`

and other Binding options for further introspection of the Event along with providing a well-formed `BlobOutput`

path that is Date hierarchical.

```
package com.example;
import java.util.Map;
import java.time.ZonedDateTime;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.*;
/**
* Azure Functions with Event Hub trigger.
* and Blob Output using date in path along with message partition ID
* and message sequence number from EventHub Trigger Properties
*/
public class EventHubReceiver {
@FunctionName("EventHubReceiver")
@StorageAccount("bloboutput")
public void run(
@EventHubTrigger(name = "message",
eventHubName = "%eventhub%",
consumerGroup = "%consumergroup%",
connection = "eventhubconnection",
cardinality = Cardinality.ONE)
String message,
final ExecutionContext context,
@BindingName("Properties") Map<String, Object> properties,
@BindingName("SystemProperties") Map<String, Object> systemProperties,
@BindingName("PartitionContext") Map<String, Object> partitionContext,
@BindingName("EnqueuedTimeUtc") Object enqueuedTimeUtc,
@BlobOutput(
name = "outputItem",
path = "iotevents/{datetime:yy}/{datetime:MM}/{datetime:dd}/{datetime:HH}/" +
"{datetime:mm}/{PartitionContext.PartitionId}/{SystemProperties.SequenceNumber}.json")
OutputBinding<String> outputItem) {
var et = ZonedDateTime.parse(enqueuedTimeUtc + "Z"); // needed as the UTC time presented does not have a TZ
// indicator
context.getLogger().info("Event hub message received: " + message + ", properties: " + properties);
context.getLogger().info("Properties: " + properties);
context.getLogger().info("System Properties: " + systemProperties);
context.getLogger().info("partitionContext: " + partitionContext);
context.getLogger().info("EnqueuedTimeUtc: " + et);
outputItem.setValue(message);
}
}
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attribute to configure the trigger. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#event-hubs-trigger).

Use the `EventHubTriggerAttribute`

to define a trigger on an event hub, which supports the following properties.

| Parameters | Description |
|---|---|
EventHubName |
The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. Can be referenced in
`%eventHubName%` |

**ConsumerGroup**[consumer group](../event-hubs/event-hubs-features#event-consumers)used to subscribe to events in the hub. When omitted, the`$Default`

consumer group is used.**Connection**[Connections](#connections).## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, the following properties on the `event_hub_message_trigger`

:

| Property | Description |
|---|---|
`arg_name` |
The name of the variable that represents the event item in function code. |
`event_hub_name` |
The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. |
`connection` |
The name of an app setting or setting collection that specifies how to connect to Event Hubs. See
|

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the [EventHubTrigger](/en-us/java/api/com.microsoft.azure.functions.annotation.eventhubtrigger) annotation, which supports the following settings:

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `app.eventHub()`

method.

| Property | Description |
|---|---|
eventHubName |
The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. Can be referenced via
`%eventHubName%` |

**consumerGroup**[consumer group](../event-hubs/event-hubs-features#event-consumers)used to subscribe to events in the hub. If omitted, the`$Default`

consumer group is used.**cardinality**`many`

in order to enable batching. If omitted or set to `one`

, a single message is passed to the function.**connection**[Connections](#connections).The following table explains the trigger configuration properties that you set in the *function.json* file, which differs by runtime version.

| function.json property | Description |
|---|---|
type |
Must be set to `eventHubTrigger` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to `in` . This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that represents the event item in function code. |
eventHubName |
The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. Can be referenced via
`%eventHubName%` |

**consumerGroup**[consumer group](../event-hubs/event-hubs-features#event-consumers)used to subscribe to events in the hub. If omitted, the`$Default`

consumer group is used.**cardinality**`many`

in order to enable batching. If omitted or set to `one`

, a single message is passed to the function.**connection**[Connections](#connections).When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

To learn more about how Event Hubs trigger and IoT Hub trigger scales, see [Consuming Events with Azure Functions](/en-us/azure/architecture/serverless/event-hubs-functions/event-hubs-functions#consuming-events-with-azure-functions).

Functions also supports Python SDK type bindings for Azure Event Hubs, which lets you work with data using these underlying SDK types:

Important

Support for Event Hubs SDK types in Python is in Preview and is only supported for the Python v2 programming model. For more information, see [SDK types in Python](functions-reference-python#sdk-type-bindings).

The parameter type supported by the Event Hubs output binding depends on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to process a single event, the Event Hubs trigger can bind to the following types:

| Type | Description |
|---|---|
`string` |
The event as a string. Use when the event is simple text. |
`byte[]` |
The bytes of the event. |
| JSON serializable types | When an event contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

If you are migrating from any older versions of the Event Hubs SDKs, note that this version drops support for the legacy

`Body`

type in favor of [EventBody](/en-us/dotnet/api/azure.messaging.eventhubs.eventdata.eventbody).When you want the function to process a batch of events, the Event Hubs trigger can bind to the following types:

| Type | Description |
|---|---|
`string[]` |
An array of events from the batch, as strings. Each entry represents one event. |
`EventData[]` 1 |
An array of events from the batch, as instances of
|

`T[]`

where `T`

is a JSON serializable type11 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.EventHubs 5.5.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventHubs/5.5.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

The parameter type can be one of the following:

- Any native Java types such as int, String, byte[].
- Nullable values using Optional.
- Any POJO type.

To learn more, see the [EventHubTrigger](/en-us/java/api/com.microsoft.azure.functions.annotation.eventhubtrigger) reference.

## Event metadata

The Event Hubs trigger provides several [metadata properties](functions-bindings-expressions-patterns). Metadata properties can be used as part of binding expressions in other bindings or as parameters in your code. The properties come from the [EventData](/en-us/dotnet/api/microsoft.servicebus.messaging.eventdata) class.

| Property | Type | Description |
|---|---|---|
`PartitionContext` |
|

`PartitionContext`

instance.`EnqueuedTimeUtc`

`DateTime`

`Offset`

`string`

`PartitionKey`

`string`

`Properties`

`IDictionary<String,Object>`

`SequenceNumber`

`Int64`

`SystemProperties`

`IDictionary<String,Object>`

See [code examples](#example) that use these properties earlier in this article.

## Connections

The `connection`

property is a reference to environment configuration that contains name of an application setting containing a connection string. You can get this connection string by selecting the **Connection Information** button for the [namespace](../event-hubs/event-hubs-create#create-an-event-hubs-namespace). The connection string must be for an Event Hubs namespace, not the event hub itself.

The connection string must have at least "read" permissions to activate the function.

This connection string should be stored in an application setting with a name matching the value specified by the `connection`

property of the binding configuration.

Note

Identity-based connections aren't supported by the IoT Hub trigger. If you need to use managed identities end-to-end, you can instead use IoT Hub Routing to send data to an event hub you control. In that way, outbound routing can be authenticated with managed identity the event can be read [from that event hub using managed identity](functions-bindings-event-hubs-trigger?tabs=extensionv5#identity-based-connections).

## host.json properties

The [host.json](functions-host-json#eventhub) file contains settings that control Event Hub trigger behavior. See the [host.json settings](functions-bindings-event-iot#hostjson-settings) section for details regarding available settings.


---

<!-- DOCUMENTO FUSIONADO: flex-consumption-plan.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/flex-consumption-plan -->

# Azure Functions Flex Consumption plan hosting

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Flex Consumption is a Linux-based Azure Functions hosting plan that builds on the Consumption *pay for what you use* serverless billing model. It gives you more flexibility and customizability by introducing private networking, instance memory size selection, and fast/large scale-out features still based on a *serverless* model.

You can review end-to-end samples that feature the Flex Consumption plan in the [Flex Consumption plan samples repository](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples).

## Benefits

The Flex Consumption plan builds on the strengths of the serverless Consumption plan, which include dynamic scaling and execution-based billing. With Flex Consumption, you also get these extra features:

**Reduced Cold Start Times**: Enable[always-ready instances](#always-ready-instances)to achieve faster cold-start times compared to the Consumption plan.**Virtual network support**:[Virtual network integration](#virtual-network-integration)enables your serverless app to run in a virtual network.**Per-Function Scaling**: Each function in your app[scales independently based on its workload](#per-function-scaling), potentially resulting in more efficient resource allocation.**Improved Concurrency Handling**: Better handling of concurrent executions with configurable concurrency settings per function.**Flexible Memory Configuration**: Flex Consumption offers multiple[instance sizes](#instance-sizes)size options, allowing you to optimize for your specific workload requirements.

This table helps you directly compare the features of Flex Consumption with the Consumption hosting plan:

| Feature | Consumption | Flex Consumption |
|---|---|---|
| Scale to zero | ✅ Yes | ✅ Yes |
| Scale behavior |
|

[Event driven](event-driven-scaling)(fast)For a complete comparison of the Flex Consumption plan against the Consumption plan and all other plan and hosting types, see [function scale and hosting options](functions-scale).

Tip

If you're migrating from the Linux Consumption plan, see [Migrate Consumption plan apps to the Flex Consumption plan](migration/migrate-plan-consumption-to-flex?pivots=platform-linux) for step-by-step migration instructions and important differences between the plans.

## Virtual network integration

Flex Consumption expands on the traditional benefits of Consumption plan by adding support for [virtual network integration](functions-networking-options#virtual-network-integration). When your apps run in a Flex Consumption plan, they can connect to other Azure services secured inside a virtual network. All while still allowing you to take advantage of serverless billing and scale, together with the scale and throughput benefits of the Flex Consumption plan. For more information, see [Enable virtual network integration](flex-consumption-how-to#enable-virtual-network-integration).

## Instance sizes

When you create your function app in a Flex Consumption plan, you can select the memory size of the instances on which your app runs. See [Billing](#billing) to learn how instance memory sizes affect the costs of your function app.

Currently, Flex Consumption offers these instance size options:

| Instance Memory (MB) | CPU Cores |
|---|---|
| 512 | 0.25 |
| 2048 | 1 |
| 4096 | 2 |

Note

The CPU core values shown are typical allocations for instances with the specified memory size. However, initial instances might be granted slightly different core allocations to improve performance. Each Flex Consumption instance also includes an extra 272 MB of memory allocated by the platform as a buffer for system and host processes. This extra memory doesn't affect billing, and instances are billed based on the configured instance memory size shown in the preceding table.

When deciding on which instance memory size to use with your apps, here are some things to consider:

- The 2,048-MB instance memory size is the default and should be used for most scenarios. The 512 MB and 4,096-MB instance memory sizes are available for scenarios that best suit your application's concurrency or processing power requirements. For more information, see
[Configure instance memory](flex-consumption-how-to#configure-instance-memory). - You can change the instance memory size at any time. For more information, see
[Configure instance memory](flex-consumption-how-to#configure-instance-memory). - Instance resources are shared between your function code and the Functions host.
- The larger the instance memory size, the more each instance can handle as far as concurrent executions or more intensive CPU or memory workloads. Specific scale decisions are workload-specific.
- The default concurrency of HTTP triggers depends on the instance memory size. For more information, see
[HTTP trigger concurrency](functions-concurrency#http-trigger-concurrency). - Available CPUs and network bandwidth are provided proportional to a specific instance size.

## Per-function scaling

[Concurrency](#concurrency) is a key factor that determines how Flex Consumption function apps scale. To improve the scale performance of apps with various trigger types, the Flex Consumption plan provides a more deterministic way of scaling your app on a per-function basis.

This *per-function scaling* behavior is a part of the hosting platform, so you don't need to configure your app or change the code. For more information, see [Per-function scaling](event-driven-scaling#per-function-scaling) in the Event-driven scaling article.

In per-function scaling, decisions are made for certain function triggers based on group aggregations. This table shows the defined set of function scale groups:

| Scale groups | Triggers in group | Settings value |
|---|---|---|
| HTTP triggers |
|

`http`

(Event Grid-based)

[Blob storage trigger](functions-bindings-storage-blob-trigger)`blob`

[Orchestration trigger](durable/durable-functions-bindings#orchestration-trigger)[Activity trigger](durable/durable-functions-bindings#activity-trigger)[Entity trigger](durable/durable-functions-bindings#entity-trigger)`durable`

All other functions in the app are scaled individually in their own set of instances, which are referenced using the convention `function:<NAMED_FUNCTION>`

.

## Always ready instances

Flex Consumption includes an *always ready* feature that lets you choose instances that are always running and assigned to each of your per-function scale groups or functions. Always ready is a great option for scenarios where you need to have a minimum number of instances always ready to handle requests. For example, to reduce your application's cold start latency. The default is 0 (zero).

For example, if you set always ready to 2 for your HTTP group of functions, the platform keeps two instances always running for those functions. Those instances process your function executions first. Depending on concurrency settings, the platform scales beyond those two instances with on-demand instances.

No less than two always-ready instances can be configured per function or function group while [zone redundancy is enabled](/en-us/azure/reliability/reliability-functions?pivots=flex-consumption-plan#availability-zone-support).

To learn how to configure always ready instances, see [Set always ready instance counts](flex-consumption-how-to#set-always-ready-instance-counts).

## Concurrency

Concurrency refers to the number of parallel executions of a function on an instance of your app. You can set a maximum number of concurrent executions that each instance should handle at any given time. Concurrency has a direct effect on how your app scales because at lower concurrency levels, you need more instances to handle the event-driven demand for a function. While you can control and fine tune the concurrency, we provide defaults that work for most cases.

To learn how to set concurrency limits for HTTP trigger functions, see [Set HTTP concurrency limits](flex-consumption-how-to#set-http-concurrency-limits). To learn how to set concurrency limits for non-HTTP trigger functions, see [Target Base Scaling](functions-target-based-scaling).

## Deployment

Deployments in the Flex Consumption plan follow a single path, and there's no longer the need for app settings to influence deployment behavior. Your project code is built and zipped into an application package, then deployed to a blob storage container. On startup, your app gets the package and runs your function code from this package. By default, the same storage account used to store internal host metadata (AzureWebJobsStorage) is also used as the deployment container. However, you can use an alternative storage account or choose your preferred authentication method by [configuring your app's deployment settings](flex-consumption-how-to#configure-deployment-settings).

Tip

A **Flex Function App deployment details** diagnostic tool is available in the Azure portal. Open your Flex Consumption app, select **Diagnose and solve problems**, and search for `Flex Function App deployment details`

. This tool displays detailed information about your deployments, including deployment history, package status, and troubleshooting recommendations.

### Zero-downtime deployments

Note

Zero-downtime deployments with rolling updates are currently in public preview.

Flex Consumption provides zero-downtime deployments through rolling updates as the [site update strategy](flex-consumption-site-updates), which allows code deployments and configuration changes to be applied gradually across instances without interrupting function execution. Other hosting plans use deployment slots to minimize downtime during deployments. For deployment options across all hosting plans, see [optimize deployments](functions-best-practices#optimize-deployments).

## Billing

There are two modes by which your costs are determined when running your apps in the Flex Consumption plan. Each mode is determined on a per-instance basis.

| Billing mode | Description |
|---|---|
On Demand |
When running in on demand mode, you are billed only for the amount of time your function code is executing on your available instances. In on demand mode, no minimum instance count is required. You're billed for:• The total amount of memory provisioned while each on demand instance is actively executing functions (in GB-seconds), minus a free grant of GB-s per month.• The total number of executions, minus a free grant (number) of executions per month. |
Always ready |
You can configure one or more instances, assigned to specific trigger types (HTTP/Durable/Blob) and individual functions, that are always available to handle requests. When you have any always ready instances enabled, you're billed for: • The total amount of memory provisioned across all of your always ready instances, known as the baseline (in GB-seconds).• The total amount of memory provisioned during the time each always ready instance is actively executing functions (in GB-seconds).• The total number of executions. In always ready billing, there are no free grants. |

For the most up-to-date information on execution pricing, always ready baseline costs, and free grants for on demand executions, see the [Azure Functions pricing page](https://azure.microsoft.com/pricing/details/functions/#pricing).

The minimum billable execution period for both execution modes is 1,000 ms. Past that, the billable activity period is rounded up to the nearest 100 ms. You can find details on the Flex Consumption plan billing meters in the [Monitoring reference](monitor-functions-reference?tab=flex-consumption-plan#metrics).

For details about how costs are calculated when you run in a Flex Consumption plan, including examples, see [Consumption-based costs](functions-consumption-costs?tabs=flex-consumption-plan#consumption-based-costs) and [Viewing cost-related data](functions-consumption-costs?tabs=flex-consumption-plan#viewing-and-estimating-costs-from-metrics).

## Supported language stack versions

This table shows the language stack versions that are currently supported for Flex Consumption apps:

| Language stack | Required version |
|---|---|
C# (isolated worker model)1 |
.NET 8, .NET 9, .NET 10 |
| Java | Java 11, Java 17, Java 21 |
| Node.js | Node.js 20, Node.js 22 |
| PowerShell | PowerShell 7.4 |
| Python | Python 3.10, Python 3.11, Python 3.12 |

- The
[C# in-process model](functions-dotnet-class-library)isn't supported. You instead need to[migrate your .NET project to the isolated worker model](migrate-dotnet-to-isolated-model).

## Regional subscription memory quotas

All Flex Consumption apps in a subscription and region share a compute quota, like a shared bucket of resources. This quota applies only to Flex Consumption apps — other hosting plans like Consumption, Premium, and Dedicated don't count against it. The quota limits how much total compute your Flex Consumption apps can use at the same time. If your apps try to exceed the quota, some executions and deployments might be delayed or fail, and scaling is throttled. However, you can still create new apps.

### Default quota

Each region in a subscription has a default quota of **250 cores** (equivalent to **512,000 MB**) for all Flex Consumption app instances combined. You can use any combination of instance sizes and counts, as long as the total cores stay under the quota.

To calculate the cores used, multiply the cores per instance by the number of instances:

| Instance size | Cores per instance | Formula |
|---|---|---|
| 512 MB | 0.25 | instances × 0.25 |
| 2,048 MB | 1 | instances × 1 |
| 4,096 MB | 2 | instances × 2 |

### Quota examples

Each of these scenarios reaches the 250 core quota limit. When the quota is reached, apps in the region stop scaling:

| Scenario | Calculation | Total cores |
|---|---|---|
| One 512-MB app at 1,000 instances | 1,000 × 0.25 | 250 |
| Two 512-MB apps at 250 and 750 instances | (250 + 750) × 0.25 | 250 |
| One 2,048-MB app at 250 instances | 250 × 1 | 250 |
| Two 2,048-MB apps at 100 and 150 instances | (100 + 150) × 1 | 250 |
| One 4,096-MB app at 125 instances | 125 × 2 | 250 |
| One 4,096-MB app at 100 instances + one 2,048-MB app at 50 instances | (100 × 2) + (50 × 1) | 250 |

### Important notes

- Flex Consumption scales rapidly based on
[concurrency](#concurrency)settings, so apps frequently acquire and release cores from the quota as demand changes. - Flex Consumption apps that scale to zero, or instances marked to be scaled in and deleted, don't count against the quota.
- Always ready instances count against quota.
- A
**Flex Consumption Quota tool**is available in the Azure portal. Open any Flex Consumption app in your subscription, select**Diagnose and solve problems**, search for`Flex Consumption Quota`

, then choose a region. The tool displays recommendations, current quota information, and historical usage views. - This quota can be increased pending capacity review. For example, from 250 cores to 1,000 cores or more. To request a larger quota, create a support ticket or contact your Microsoft account team.

## Deprecated properties and settings

In the Flex Consumption plan, many standard application settings and site configuration properties are deprecated or moved. Don't use these settings when you automate function app resource creation. For more information, see [Flex Consumption plan deprecations](functions-app-settings#flex-consumption-plan-deprecations).

## Considerations

Keep these other considerations in mind when using Flex Consumption plan:

**Apps per Plan**: Only one app is allowed per Flex Consumption plan.**Host**: There's a 30-second time-out for app initialization. When your function app takes longer than 30 seconds to start, you might see gRPC-related`System.TimeoutException`

entries logged. You can't currently configure this time-out. For more information, see[this host work item](https://github.com/Azure/azure-functions-host/issues/10482).**Durable Functions**: Azure Storage and Durable Task Scheduler are the only supported[storage providers](durable/durable-functions-storage-providers)for Durable Functions when hosted in the Flex Consumption plan. See[recommendations](durable/durable-functions-azure-storage-provider#flex-consumption-plan)when hosting Durable Functions in the Flex Consumption plan.**Virtual network integration and Resource provider registration**: You must have the`Microsoft.App`

Azure resource provider registered in your subscription to integrate to a virtual network, which is needed for subnet delegation. The Azure portal and Azure CLI enforce registration at app creation time since virtual network integration can be enabled at any point after your app is created. To register this provider,[follow these instructions](/en-us/azure/azure-resource-manager/management/resource-providers-and-types#register-resource-provider). The subnet delegation required by Flex Consumption apps is`Microsoft.App/environments`

.**Triggers**: While all triggers are fully supported in a Flex Consumption plan, the Blob storage trigger only supports the[Event Grid source](functions-event-grid-blob-trigger). Non-C# function apps must use version`[4.0.0, 5.0.0)`

of the[extension bundle](extension-bundles), or a later version.**Regions**: While the Flex Consumption plan is available in many Azure regions, not all regions are currently supported. To learn more, see[View currently supported regions](flex-consumption-how-to#view-currently-supported-regions).**Deployments**: Deployment slots aren't currently supported. For zero downtime deployments with Flex Consumption, see[Site update strategies in Flex Consumption](flex-consumption-site-updates).**Azure Storage as a local share**: Network File System (NFS) file shares aren't available for Flex Consumption. Only Server Message Block (SMB) and Azure Blobs (read-only) are supported.**Scale**: The lowest maximum scale is currently`40`

. The highest currently supported value is`1000`

.**PowerShell Managed dependencies**: Flex Consumption doesn't support[managed dependencies in PowerShell](functions-reference-powershell#managed-dependencies-feature). You must instead[upload modules with app content](functions-reference-powershell#including-modules-in-app-content).**Certificates**: Loading certificates with the WEBSITE_LOAD_CERTIFICATES app setting, managed certificates, app service certificates, and other platform certificate-based features like endToEndEncryptionEnabled are currently not supported.**Timezones**:`WEBSITE_TIME_ZONE`

and`TZ`

app settings aren't currently supported when running on Flex Consumption plan.**Azure Functions Runtime Version and Proxies**: Flex Consumption only supports version 4.x and later of the Azure Functions runtime. Azure Functions proxies was a feature of versions 1.x through 3.x of the Azure Functions runtime and is not available in Flex Consumption.

## Related articles

[Azure Functions hosting options](functions-scale)
[Create and manage function apps in the Flex Consumption plan](flex-consumption-how-to)
