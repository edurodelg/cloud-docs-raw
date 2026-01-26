---
merged_at: 2026-01-26T21:02:36.350677
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-signalr-service-input -->

# SignalR Service input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Before a client can connect to Azure SignalR Service, it must retrieve the service endpoint URL and a valid access token. The *SignalRConnectionInfo* input binding produces the SignalR Service endpoint URL and a valid token that are used to connect to the service. The token is time-limited and can be used to authenticate a specific user to a connection. Therefore, you shouldn't cache the token or share it between clients. Usually you use *SignalRConnectionInfo* with HTTP trigger for clients to retrieve the connection information.

For more information on how to use this binding to create a "negotiate" function that is compatible with a SignalR client SDK, see [Azure Functions development and configuration with Azure SignalR Service](../azure-signalr/signalr-concept-serverless-development-config).

When not explicitly declared, assume that examples are using the default connection setting value of `AzureSignalRConnectionString`

. For information on setup and configuration details, see the [overview](functions-bindings-signalr-service).

## Example

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The following example shows a [C# function](dotnet-isolated-process-guide) that acquires SignalR connection information using the input binding and returns it over HTTP.

```
[Function(nameof(Negotiate))]
public static string Negotiate([HttpTrigger(AuthorizationLevel.Anonymous)] HttpRequestData req,
[SignalRConnectionInfoInput(HubName = "serverless")] string connectionInfo)
{
// The serialization of the connection info object is done by the framework. It should be camel case. The SignalR client respects the camel case response only.
return connectionInfo;
}
```


The following example shows a SignalR connection info input binding in a *function.json* file and a function that uses the binding to return the connection information.

Here's binding data for the example in the *function.json* file:

```
{
"type": "signalRConnectionInfo",
"name": "connectionInfo",
"hubName": "hubName1",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "in"
}
```


Here's the JavaScript code:

```
const { app, input } = require('@azure/functions');
const inputSignalR = input.generic({
type: 'signalRConnectionInfo',
name: 'connectionInfo',
hubName: 'hubName1',
connectionStringSetting: 'AzureSignalRConnectionString',
});
app.post('negotiate', {
authLevel: 'function',
handler: (request, context) => {
return { body: JSON.stringify(context.extraInputs.get(inputSignalR)) }
},
route: 'negotiate',
extraInputs: [inputSignalR],
});
```


Complete PowerShell examples are pending.

The following example shows a SignalR connection info input binding in a *function.json* file and a [Python function](functions-reference-python) that uses the binding to return the connection information.

Here's the Python code:

```
def main(req: func.HttpRequest, connectionInfoJson: str) -> func.HttpResponse:
return func.HttpResponse(
connectionInfoJson,
status_code=200,
headers={
'Content-type': 'application/json'
}
)
```


The following example shows a [Java function](functions-reference-java) that acquires SignalR connection information using the input binding and returns it over HTTP.

```
@FunctionName("negotiate")
public SignalRConnectionInfo negotiate(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST },
authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> req,
@SignalRConnectionInfoInput(
name = "connectionInfo",
HubName = "hubName1") SignalRConnectionInfo connectionInfo) {
return connectionInfo;
}
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attribute to define the function. C# script instead uses a function.json configuration file.

The following table explains the properties of the `SignalRConnectionInfoInput`

attribute:

| Attribute property | Description |
|---|---|
HubName |
Required. The hub name. |
ConnectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |
UserId |
Optional. The user identifier of a SignalR connection. You can use a
|

**IdToken****ClaimTypeList**. You can use a[binding expression](#binding-expressions-for-http-trigger)to bind the value to an HTTP request header or query.**ClaimTypeList****IdToken**.## Annotations

The following table explains the supported settings for the `SignalRConnectionInfoInput`

annotation.

| Setting | Description |
|---|---|
name |
Variable name used in function code for connection info object. |
hubName |
Required. The hub name. |
connectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |
userId |
Optional. The user identifier of a SignalR connection. You can use a
|

**idToken****claimTypeList**. You can use a[binding expression](#binding-expressions-for-http-trigger)to bind the value to an HTTP request header or query.**claimTypeList****idToken**.## Annotations

The following table explains the supported settings for the `SignalRConnectionInfoInput`

annotation.

| Setting | Description |
|---|---|
name |
Variable name used in function code for connection info object. |
hubName |
Required. The hub name. |
connectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |
userId |
Optional. The user identifier of a SignalR connection. You can use a
|

**idToken****claimTypeList**. You can use a[binding expression](#binding-expressions-for-http-trigger)to bind the value to an HTTP request header or query.**claimTypeList****idToken**.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `signalRConnectionInfo` . |
direction |
Must be set to `in` . |
hubName |
Required. The hub name. |
connectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |
userId |
Optional. The user identifier of a SignalR connection. You can use a
|

**idToken****claimTypeList**. You can use a[binding expression](#binding-expressions-for-http-trigger)to bind the value to an HTTP request header or query.**claimTypeList****idToken**.Warning

For the simplicity, we omit the authentication and authorization parts in this sample. As a result, this endpoint is publicly accessible without any restrictions. To ensure the security of your negotiation endpoint, you should implement appropriate authentication and authorization mechanisms based on your specific requirements. For guidance on protecting your HTTP endpoints, see the following articles:

## Usage

### Managed identity-based connections

For optimal security, your function app should use managed identities when connecting to the Azure SignalR service instead of using a connection string, which contains a shared secret key. For more information, see [Authorize requests to Azure SignalR Service resources with Microsoft Entra managed identities](../azure-signalr/signalr-howto-authorize-managed-identity#azure-signalr-service-bindings-in-azure-functions).

### Authenticated tokens

When an authenticated client triggers the function, you can add a user ID claim to the generated token. You can easily add authentication to a function app using [App Service Authentication](../app-service/overview-authentication-authorization).

App Service authentication sets HTTP headers named `x-ms-client-principal-id`

and `x-ms-client-principal-name`

that contain the authenticated user's client principal ID and name, respectively.

You can set the `UserId`

property of the binding to the value from either header using a [binding expression](#binding-expressions-for-http-trigger): `{headers.x-ms-client-principal-id}`

or `{headers.x-ms-client-principal-name}`

.

```
[Function("Negotiate")]
public static string Negotiate([HttpTrigger(AuthorizationLevel.Anonymous)] HttpRequestData req,
[SignalRConnectionInfoInput(HubName = "hubName1", UserId = "{headers.x-ms-client-principal-id}")] string connectionInfo)
{
// The serialization of the connection info object is done by the framework. It should be camel case. The SignalR client respects the camel case response only.
return connectionInfo;
}
```


```
@FunctionName("negotiate")
public SignalRConnectionInfo negotiate(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST, HttpMethod.GET },
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> req,
@SignalRConnectionInfoInput(name = "connectionInfo", hubName = "hubName1", userId = "{headers.x-ms-signalr-userid}") SignalRConnectionInfo connectionInfo) {
return connectionInfo;
}
```


Here's binding data in the *function.json* file:

```
{
"type": "signalRConnectionInfo",
"name": "connectionInfo",
"hubName": "hubName1",
"userId": "{headers.x-ms-client-principal-id}",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "in"
}
```


Here's the JavaScript code:

```
const { app, input } = require('@azure/functions');
const inputSignalR = input.generic({
type: 'signalRConnectionInfo',
name: 'connectionInfo',
hubName: 'hubName1',
connectionStringSetting: 'AzureSignalRConnectionString',
userId: '{headers.x-ms-client-principal-id}',
});
app.post('negotiate', {
authLevel: 'function',
handler: (request, context) => {
return { body: JSON.stringify(context.extraInputs.get(inputSignalR)) }
},
route: 'negotiate',
extraInputs: [inputSignalR],
});
```


Complete PowerShell examples are pending.

Here's the Python code:

```
def main(req: func.HttpRequest, connectionInfo: str) -> func.HttpResponse:
# connectionInfo contains an access key token with a name identifier
# claim set to the authenticated user
return func.HttpResponse(
connectionInfo,
status_code=200,
headers={
'Content-type': 'application/json'
}
)
```


```
@FunctionName("negotiate")
public SignalRConnectionInfo negotiate(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST },
authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> req,
@SignalRConnectionInfoInput(
name = "connectionInfo",
HubName = "hubName1",
userId = "{headers.x-ms-client-principal-id}") SignalRConnectionInfo connectionInfo) {
return connectionInfo;
}
```


### Binding expressions for HTTP trigger

[
It's a common scenario that the values of some attributes of SignalR input binding come from HTTP requests. Therefore, we show how to bind values from HTTP requests to SignalR input binding attributes via ][binding expression](functions-bindings-expressions-patterns#trigger-metadata).

| HTTP metadata type | Binding expression format | Description | Example |
|---|---|---|---|
| HTTP request query | `{query.QUERY_PARAMETER_NAME}` |
Binds the value of corresponding query parameter to an attribute | `{query.userName}` |
| HTTP request header | `{headers.HEADER_NAME}` |
Binds the value of a header to an attribute | `{headers.token}` |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-your-first-function-visual-studio -->

# Quickstart: Create your first C# function in Azure using Visual Studio

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions lets you use Visual Studio to create local C# function projects and then easily publish this project to run in a scalable serverless environment in Azure. If you prefer to develop your C# apps locally using Visual Studio Code, you should instead consider the [Visual Studio Code-based version](how-to-create-function-vs-code?pivot=programming-language-csharp) of this article.

By default, this article shows you how to create C# functions that run on .NET 8 in an [isolated worker process](dotnet-isolated-process-guide). Function apps that run in an isolated worker process are supported on all versions of .NET that are supported by Functions. For more information, see [Supported versions](dotnet-isolated-process-guide#supported-versions).

In this article, you learn how to:

- Use Visual Studio to create a C# class library project.
- Create a function that responds to HTTP requests.
- Run your code locally to verify function behavior.
- Deploy your code project to Azure Functions.

Completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

This video shows you how to create a C# function in Azure.

The steps in the video are also described in the following sections.

## Prerequisites

[Visual Studio 2022](https://visualstudio.microsoft.com/vs/). Make sure to select the**Azure development**workload during installation.[Azure subscription](../guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing). If you don't already have an account,[create a free one](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

## Create a function app project

The Azure Functions project template in Visual Studio creates a C# class library project that you can publish to a function app in Azure. You can use a function app to group functions as a logical unit for easier management, deployment, scaling, and sharing of resources.

From the Visual Studio menu, select

**File**>**New**>**Project**.In

**Create a new project**, enter*functions*in the search box, choose the**Azure Functions**template, and then select**Next**.In

**Configure your new project**, enter a**Project name**for your project, and then select**Next**. The function app name must be valid as a C# namespace, so don't use underscores, hyphens, or any other nonalphanumeric characters.For the remaining

**Additional information**settings,Setting Value Description **Functions worker****.NET 8.0 Isolated (Long Term Support)**Your functions run on .NET 8 in an isolated worker process. **Function****HTTP trigger**This value creates a function triggered by an HTTP request. **Use Azurite for runtime storage account (AzureWebJobsStorage)**Enable Because a function app in Azure requires a storage account, one is assigned or created when you publish your project to Azure. An HTTP trigger doesn't use an Azure Storage account connection string; all other trigger types require a valid Azure Storage account connection string. When you select this option, the [Azurite emulator](../storage/common/storage-use-azurite?tabs=visual-studio)is used.**Authorization level****Anonymous**The created function can be triggered by any client without providing a key. This authorization setting makes it easy to test your new function. For more information, see [Authorization level](functions-bindings-http-webhook-trigger#http-auth).Make sure you set the

**Authorization level**to**Anonymous**. If you choose the default level of**Function**, you're required to present the[function key](function-keys-how-to)in requests to access your function endpoint in Azure.Select

**Create**to create the function project and HTTP trigger function.

Visual Studio creates a project and class that contains boilerplate code for the HTTP trigger function type. The boilerplate code sends an HTTP response that includes a value from the request body or query string. The `HttpTrigger`

attribute specifies that the function is triggered by an HTTP request.

## Rename the function

The `Function`

method attribute sets the name of the function, which by default is generated as `Function1`

. Since the tooling doesn't let you override the default function name when you create your project, take a minute to create a better name for the function class, file, and metadata.

In

**File Explorer**, right-click the Function1.cs file and rename it to`HttpExample.cs`

.In the code, rename the Function1 class to

`HttpExample`

.In the method named

`Run`

, rename the`Function`

method attribute to`HttpExample`

.

Your function definition should now look like the following code:

```
[Function("HttpExample")]
public IActionResult Run([HttpTrigger(AuthorizationLevel.Anonymous, "get", "post")] HttpRequest req)
{
_logger. LogInformation("C# HTTP trigger function processed a request.");
return new OkObjectResult("Hello, functions");
}
```


Now that you've renamed the function, you can test it on your local computer.

## Run the function locally

Visual Studio integrates with Azure Functions Core Tools so that you can test your functions locally using the full Azure Functions runtime.

To run your function, press

`F5`in Visual Studio. You might need to enable a firewall exception so that the tools can handle HTTP requests. Authorization levels are never enforced when you run a function locally.Copy the URL of your function from the Azure Functions runtime output.

Paste the URL for the HTTP request into your browser's address bar and run the request. The following image shows the response in the browser to the local GET request returned by the function:

To stop debugging, press

`Shift`+`F5`in Visual Studio.

After you've verified that the function runs correctly on your local computer, it's time to publish the project to Azure.

## Publish the project to Azure

Visual Studio can publish your local project to Azure. Before you can publish your project, you must have a function app in your Azure subscription. If you don't already have a function app in Azure, Visual Studio can help you create one before you publish your project. In this article, you create a function app that runs on Linux in a Flex Consumption plan, which is the recommended plan for event-driven and secure serverless functions.

In

**Solution Explorer**, right-click the project and then select**Publish**.On the

**Publish**page, make the following selections:- On
**Target**, select**Azure**, and then select**Next**. - On
**Specific target**, select**Azure Function App**, and then select**Next**. - On
**Functions instance**, select**Create new**.

- On
Create a new instance by using the values specified in the following table:

Setting Value Description **Name**A globally unique name The name must uniquely identify your new function app. Accept the suggested name or enter a new name. The following characters are valid: `a-z`

,`0-9`

, and`-`

.**Subscription name**The name of your subscription The function app is created in an Azure subscription. Accept the default subscription or select a different one from the list. [Resource group](../azure-resource-manager/management/overview)The name of your resource group The function app is created in a resource group. Select **New**to create a new resource group. You can also select an existing resource group from the list.[Plan Type](functions-scale)**Flex Consumption**When you publish your project to a function app that runs in a [Flex Consumption plan](flex-consumption-plan), you might pay only for executions of your functions app. Other hosting plans can incur higher costs.**IMPORTANT:**

When creating a Flex Consumption plan, you must first select**App service plan**and then reselect**Flex Consumption**to clear an issue with the dialog.**Operating system****Linux**The Flex Consumption plan currently requires Linux. **Location**The location of the app service Select a location in an [Azure region supported by the Flex Consumption plan](flex-consumption-how-to#view-currently-supported-regions). When an unsupported region is selected, the**Create**button is grayed-out.**Instance memory size****2048**The [memory size of the virtual machine instances](flex-consumption-plan#instance-sizes)in which the app runs is unique to the Flex Consumption plan.[Azure Storage](storage-considerations)A general-purpose storage account The Functions runtime requires a Storage account. Select **New**to configure a general-purpose storage account. You can also use an existing account that meets the[storage account requirements](storage-considerations#storage-account-requirements).[Application Insights](functions-monitoring)An Application Insights instance You should turn on Application Insights integration for your function app. Select **New**to create a new instance, either in a new or in an existing Log Analytics workspace. You can also use an existing instance.Select

**Create**to create a function app and its related resources in Azure. The status of resource creation is shown in the lower-left corner of the window.Select

**Finish**. The**Publish profile creation progress**window appears. When the profile is created, select**Close**.On the publish profile page, select

**Publish**to deploy the package that contains your project files to your new function app in Azure.When deployment is complete, the root URL of the function app in Azure is shown on the publish profile page.

On the publish profile page, go to the

**Hosting**section. Select the ellipsis (**...**), and then select**Open in Azure portal**. The new function app Azure resource opens in the Azure portal.

## Verify your function in Azure

In the Azure portal, you should be in the

**Overview**page for your new functions app.Under

**Functions**, select your new function named**HttpExample**, then in the function page select**Get function URL**and then the**Copy to clipboard icon**.In the address bar in your browser, paste the URL you copied and run the request.

The URL that calls your HTTP trigger function is in the following format:

`https://<APP_NAME>.azurewebsites.net/api/HttpExample?name=Functions`

Go to this URL and you see a response in the browser to the remote GET request returned by the function, which looks like the following example:


## Clean up resources

*Resources* in Azure refer to function apps, functions, storage accounts, and so forth. They're grouped into *resource groups*, and you can delete everything in a group by deleting the group.

You created Azure resources to complete this quickstart. You could be billed for these resources, depending on your [account status](https://azure.microsoft.com/account/) and [service pricing](https://azure.microsoft.com/pricing/). Other quickstarts in this collection build upon this quickstart. If you plan to work with subsequent quickstarts, tutorials, or with any of the services you've created in this quickstart, don't clean up the resources.

Use the following steps to delete the function app and its related resources to avoid incurring any further costs.

In the Visual Studio Publish dialogue, in the Hosting section, select

**Open in Azure portal**.In the function app page, select the

**Overview**tab and then select the link under**Resource group**.In the

**Resource group**page, review the list of included resources, and verify that they're the ones you want to delete.Select

**Delete resource group**, and follow the instructions.Deletion may take a couple of minutes. When it's done, a notification appears for a few seconds. You can also select the bell icon at the top of the page to view the notification.


## Next steps

In this quickstart, you used Visual Studio to create and publish a C# function app in Azure with a simple HTTP trigger function.

To learn more about working with C# functions that run in an isolated worker process, see the [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide). Check out [.NET supported versions](functions-dotnet-class-library#supported-versions) to see other versions of supported .NET versions in an isolated worker process.

Advance to the next article to learn how to add an Azure Storage queue binding to your function:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2-output -->

# Azure Cosmos DB output binding for Azure Functions 2.x and higher

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Cosmos DB output binding lets you write a new document to an Azure Cosmos DB database using the SQL API.

For information on setup and configuration details, see the [overview](functions-bindings-cosmosdb-v2).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

## Example

Unless otherwise noted, examples in this article target version 3.x of the [Azure Cosmos DB extension](functions-bindings-cosmosdb-v2). For use with extension version 4.x, you need to replace the string `collection`

in property and attribute names with `container`

and `connection_string_setting`

with `connection`

.

The following code defines a `MyDocument`

type:

```
public class MyDocument
{
public string? Id { get; set; }
public string? Text { get; set; }
public int Number { get; set; }
public bool Boolean { get; set; }
}
```


In the following example, the return type is an [ IReadOnlyList<T>](/en-us/dotnet/api/system.collections.generic.ireadonlylist-1), which is a modified list of documents from trigger binding parameter:

```
using System.Collections.Generic;
using System.Linq;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.Logging;
namespace SampleApp
{
public class CosmosDBFunction
{
private readonly ILogger<CosmosDBFunction> _logger;
public CosmosDBFunction(ILogger<CosmosDBFunction> logger)
{
_logger = logger;
}
//<docsnippet_exponential_backoff_retry_example>
[Function(nameof(CosmosDBFunction))]
[ExponentialBackoffRetry(5, "00:00:04", "00:15:00")]
[CosmosDBOutput("%CosmosDb%", "%CosmosContainerOut%", Connection = "CosmosDBConnection", CreateIfNotExists = true)]
public object? Run(
[CosmosDBTrigger(
"%CosmosDb%",
"%CosmosContainerIn%",
Connection = "CosmosDBConnection",
LeaseContainerName = "leases",
CreateLeaseContainerIfNotExists = true)] IReadOnlyList<MyDocument> input,
FunctionContext context)
{
if (input != null && input.Any())
{
foreach (var doc in input)
{
_logger.LogInformation("Doc Id: {id}", doc.Id);
}
// Cosmos Output
return input.Select(p => new { id = p.Id });
}
return null;
}
//</docsnippet_exponential_backoff_retry_example>
}
```


[Queue trigger, save message to database via return value](#queue-trigger-save-message-to-database-via-return-value-java)[HTTP trigger, save one document to database via return value](#http-trigger-save-one-document-to-database-via-return-value-java)[HTTP trigger, save one document to database via OutputBinding](#http-trigger-save-one-document-to-database-via-outputbinding-java)[HTTP trigger, save multiple documents to database via OutputBinding](#http-trigger-save-multiple-documents-to-database-via-outputbinding-java)

### Queue trigger, save message to database via return value

The following example shows a Java function that adds a document to a database with data from a message in Queue storage.

```
@FunctionName("getItem")
@CosmosDBOutput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
connectionStringSetting = "AzureCosmosDBConnection")
public String cosmosDbQueryById(
@QueueTrigger(name = "msg",
queueName = "myqueue-items",
connection = "AzureWebJobsStorage")
String message,
final ExecutionContext context) {
return "{ id: \"" + System.currentTimeMillis() + "\", Description: " + message + " }";
}
```


#### HTTP trigger, save one document to database via return value

The following example shows a Java function whose signature is annotated with `@CosmosDBOutput`

and has return value of type `String`

. The JSON document returned by the function is automatically written to the corresponding Azure Cosmos DB collection.

```
@FunctionName("WriteOneDoc")
@CosmosDBOutput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
connectionStringSetting = "Cosmos_DB_Connection_String")
public String run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
final ExecutionContext context) {
// Item list
context.getLogger().info("Parameters are: " + request.getQueryParameters());
// Parse query parameter
String query = request.getQueryParameters().get("desc");
String name = request.getBody().orElse(query);
// Generate random ID
final int id = Math.abs(new Random().nextInt());
// Generate document
final String jsonDocument = "{\"id\":\"" + id + "\", " +
"\"description\": \"" + name + "\"}";
context.getLogger().info("Document to be saved: " + jsonDocument);
return jsonDocument;
}
```


### HTTP trigger, save one document to database via OutputBinding

The following example shows a Java function that writes a document to Azure Cosmos DB via an `OutputBinding<T>`

output parameter. In this example, the `outputItem`

parameter needs to be annotated with `@CosmosDBOutput`

, not the function signature. Using `OutputBinding<T>`

lets your function take advantage of the binding to write the document to Azure Cosmos DB while also allowing returning a different value to the function caller, such as a JSON or XML document.

```
@FunctionName("WriteOneDocOutputBinding")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@CosmosDBOutput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
connectionStringSetting = "Cosmos_DB_Connection_String")
OutputBinding<String> outputItem,
final ExecutionContext context) {
// Parse query parameter
String query = request.getQueryParameters().get("desc");
String name = request.getBody().orElse(query);
// Item list
context.getLogger().info("Parameters are: " + request.getQueryParameters());
// Generate random ID
final int id = Math.abs(new Random().nextInt());
// Generate document
final String jsonDocument = "{\"id\":\"" + id + "\", " +
"\"description\": \"" + name + "\"}";
context.getLogger().info("Document to be saved: " + jsonDocument);
// Set outputItem's value to the JSON document to be saved
outputItem.setValue(jsonDocument);
// return a different document to the browser or calling client.
return request.createResponseBuilder(HttpStatus.OK)
.body("Document created successfully.")
.build();
}
```


### HTTP trigger, save multiple documents to database via OutputBinding

The following example shows a Java function that writes multiple documents to Azure Cosmos DB via an `OutputBinding<T>`

output parameter. In this example, the `outputItem`

parameter is annotated with `@CosmosDBOutput`

, not the function signature. The output parameter, `outputItem`

has a list of `ToDoItem`

objects as its template parameter type. Using `OutputBinding<T>`

lets your function take advantage of the binding to write the documents to Azure Cosmos DB while also allowing returning a different value to the function caller, such as a JSON or XML document.

```
@FunctionName("WriteMultipleDocsOutputBinding")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@CosmosDBOutput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
connectionStringSetting = "Cosmos_DB_Connection_String")
OutputBinding<List<ToDoItem>> outputItem,
final ExecutionContext context) {
// Parse query parameter
String query = request.getQueryParameters().get("desc");
String name = request.getBody().orElse(query);
// Item list
context.getLogger().info("Parameters are: " + request.getQueryParameters());
// Generate documents
List<ToDoItem> items = new ArrayList<>();
for (int i = 0; i < 5; i ++) {
// Generate random ID
final int id = Math.abs(new Random().nextInt());
// Create ToDoItem
ToDoItem item = new ToDoItem(String.valueOf(id), name);
items.add(item);
}
// Set outputItem's value to the list of POJOs to be saved
outputItem.setValue(items);
context.getLogger().info("Document to be saved: " + items);
// return a different document to the browser or calling client.
return request.createResponseBuilder(HttpStatus.OK)
.body("Documents created successfully.")
.build();
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@CosmosDBOutput`

annotation on parameters that is written to Azure Cosmos DB. The annotation parameter type should be `OutputBinding<T>`

, where `T`

is either a native Java type or a POJO.

The following example shows a storage queue triggered [TypeScript function](functions-reference-node?tabs=typescript) for a queue that receives JSON in the following format:

```
{
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


The function creates Azure Cosmos DB documents in the following format for each record:

```
{
"id": "John Henry-123456",
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


Here's the TypeScript code:

```
import { app, InvocationContext, output } from '@azure/functions';
interface MyQueueItem {
name: string;
employeeId: string;
address: string;
}
interface MyCosmosItem {
id: string;
name: string;
employeeId: string;
address: string;
}
export async function storageQueueTrigger1(queueItem: MyQueueItem, context: InvocationContext): Promise<MyCosmosItem> {
return {
id: `${queueItem.name}-${queueItem.employeeId}`,
name: queueItem.name,
employeeId: queueItem.employeeId,
address: queueItem.address,
};
}
app.storageQueue('storageQueueTrigger1', {
queueName: 'inputqueue',
connection: 'MyStorageConnectionAppSetting',
return: output.cosmosDB({
databaseName: 'MyDatabase',
collectionName: 'MyCollection',
createIfNotExists: true,
connectionStringSetting: 'MyAccount_COSMOSDB',
}),
handler: storageQueueTrigger1,
});
```


To output multiple documents, return an array instead of a single object. For example:

```
return [
{
id: 'John Henry-123456',
name: 'John Henry',
employeeId: '123456',
address: 'A town nearby',
},
{
id: 'John Doe-123457',
name: 'John Doe',
employeeId: '123457',
address: 'A town far away',
},
];
```


The following example shows a storage queue triggered [JavaScript function](functions-reference-node) for a queue that receives JSON in the following format:

```
{
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


The function creates Azure Cosmos DB documents in the following format for each record:

```
{
"id": "John Henry-123456",
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


Here's the JavaScript code:

```
const { app, output } = require('@azure/functions');
const cosmosOutput = output.cosmosDB({
databaseName: 'MyDatabase',
collectionName: 'MyCollection',
createIfNotExists: true,
connectionStringSetting: 'MyAccount_COSMOSDB',
});
app.storageQueue('storageQueueTrigger1', {
queueName: 'inputqueue',
connection: 'MyStorageConnectionAppSetting',
return: cosmosOutput,
handler: (queueItem, context) => {
return {
id: `${queueItem.name}-${queueItem.employeeId}`,
name: queueItem.name,
employeeId: queueItem.employeeId,
address: queueItem.address,
};
},
});
```


To output multiple documents, return an array instead of a single object. For example:

```
return [
{
id: 'John Henry-123456',
name: 'John Henry',
employeeId: '123456',
address: 'A town nearby',
},
{
id: 'John Doe-123457',
name: 'John Doe',
employeeId: '123457',
address: 'A town far away',
},
];
```


The following example shows how to write data to Azure Cosmos DB using an output binding. The binding is declared in the function's configuration file (*functions.json*), and takes data from a queue message and writes out to an Azure Cosmos DB document.

```
{
"name": "EmployeeDocument",
"type": "cosmosDB",
"databaseName": "MyDatabase",
"collectionName": "MyCollection",
"createIfNotExists": true,
"connectionStringSetting": "MyStorageConnectionAppSetting",
"direction": "out"
}
```


In the *run.ps1* file, the object returned from the function is mapped to an `EmployeeDocument`

object, which is persisted in the database.

```
param($QueueItem, $TriggerMetadata)
Push-OutputBinding -Name EmployeeDocument -Value @{
id = $QueueItem.name + '-' + $QueueItem.employeeId
name = $QueueItem.name
employeeId = $QueueItem.employeeId
address = $QueueItem.address
}
```


The following example demonstrates how to write a document to an Azure Cosmos DB database as the output of a function. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.route()
@app.cosmos_db_output(arg_name="documents",
database_name="DB_NAME",
collection_name="COLLECTION_NAME",
create_if_not_exists=True,
connection_string_setting="CONNECTION_SETTING")
def main(req: func.HttpRequest, documents: func.Out[func.Document]) -> func.HttpResponse:
request_body = req.get_body()
documents.set(func.Document.from_json(request_body))
return 'OK'
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#azure-cosmos-db-v2-output).

| Attribute property | Description |
|---|---|
Connection |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see
|

**DatabaseName****ContainerName****CreateIfNotExists***false*because new containers are created with reserved throughput, which has cost implications. For more information, see the[pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).**PartitionKey**`CreateIfNotExists`

is true, it defines the partition key path for the created container. May include binding parameters.**ContainerThroughput**`CreateIfNotExists`

is true, it defines the [throughput](/en-us/azure/cosmos-db/set-throughput)of the created container.**PreferredLocations**`East US,South Central US,North Europe`

.## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, the following properties on the `cosmos_db_output`

:

| Property | Description |
|---|---|
`arg_name` |
The variable name used in function code that represents the list of documents with changes. |
`database_name` |
The name of the Azure Cosmos DB database with the container being monitored. |
`container_name` |
The name of the Azure Cosmos DB container being monitored. |
`create_if_not_exists` |
A Boolean value that indicates whether the database and collection should be created if they do not exist. |
`connection_string_setting` |
The connection string of the Azure Cosmos DB being monitored. |

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

From the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@CosmosDBOutput`

annotation on parameters that write to Azure Cosmos DB. The annotation supports the following properties:

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the binding configuration properties that you set in the *function.json* file, where properties differ by extension version:

| function.json property | Description |
|---|---|
connection |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see
|

**databaseName****containerName****createIfNotExists***false*because new containers are created with reserved throughput, which has cost implications. For more information, see the[pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).**partitionKey**`createIfNotExists`

is true, it defines the partition key path for the created container. May include binding parameters.**containerThroughput**`createIfNotExists`

is true, it defines the [throughput](/en-us/azure/cosmos-db/set-throughput)of the created container.**preferredLocations**`East US,South Central US,North Europe`

.See the [Example section](#example) for complete examples.

## Usage

By default, when you write to the output parameter in your function, a document is created in your database. You should specify the document ID of the output document by specifying the `id`

property in the JSON object passed to the output parameter.

Note

When you specify the ID of an existing document, it gets overwritten by the new output document.

The output function parameter must be defined as `func.Out[func.Document]`

. Refer to the [output example](#example) for details.

The parameter type supported by the Cosmos DB output binding depends on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to write to a single document, the Cosmos DB output binding can bind to the following types:

| Type | Description |
|---|---|
| JSON serializable types | An object representing the JSON content of a document. Functions attempts to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write to multiple documents, the Cosmos DB output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is JSON serializable type |
An array containing multiple documents. Each entry represents one document. |

For other output scenarios, create and use a [CosmosClient](/en-us/dotnet/api/microsoft.azure.cosmos.cosmosclient) with other types from [Microsoft.Azure.Cosmos](/en-us/dotnet/api/microsoft.azure.cosmos) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

## Connections

The `connectionStringSetting`

/`connection`

and `leaseConnectionStringSetting`

/`leaseConnection`

properties are references to environment configuration which specifies how the app should connect to Azure Cosmos DB. They may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections). This option is only available for the`connection`

and`leaseConnection`

versions from[version 4.x or higher of the extension](functions-bindings-cosmosdb-v2?tabs=extensionv4).

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

The connection string for your database account should be stored in an application setting with a name matching the value specified by the connection property of the binding configuration.

### Identity-based connections

If you are using [version 4.x or higher of the extension](functions-bindings-cosmosdb-v2?tabs=extensionv4), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). To do this, you would define settings under a common prefix which maps to the connection property in the trigger and binding configuration.

In this mode, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Account Endpoint | `<CONNECTION_NAME_PREFIX>__accountEndpoint` |
The Azure Cosmos DB account endpoint URI. | https://<database_account_name>.documents.azure.com:443/ |

Additional properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

Cosmos DB does not use Azure RBAC for data operations. Instead, it uses a [Cosmos DB built-in RBAC system](/en-us/azure/cosmos-db/how-to-setup-rbac) which is built on similar concepts. You will need to create a role assignment that provides access to your database account at runtime. Azure RBAC Management roles like [Owner](../role-based-access-control/built-in-roles#owner) are not sufficient. The following table shows built-in roles that are recommended when using the Azure Cosmos DB extension in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles1 |
|---|---|
Trigger2 |
|

[Cosmos DB Built-in Data Reader](/en-us/azure/cosmos-db/how-to-setup-rbac#built-in-role-definitions)[Cosmos DB Built-in Data Contributor](/en-us/azure/cosmos-db/how-to-setup-rbac#built-in-role-definitions)1 These roles cannot be used in an Azure RBAC role assignment. See the [Cosmos DB built-in RBAC system](/en-us/azure/cosmos-db/how-to-setup-rbac) documentation for details on how to assign these roles.

2 When using identity, Cosmos DB treats container creation as a management operation. It is not available as a data-plane operation for the trigger. You will need to ensure that you create the containers needed by the trigger (including the lease container) before setting up your function.

## Exceptions and return codes

| Binding | Reference |
|---|---|
| Azure Cosmos DB |
|

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/add-bindings-existing-function -->

# Connect functions to Azure services using bindings

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create a function, language-specific trigger code is added in your project from a set of trigger templates. If you want to connect your function to other services by using input or output bindings, you have to add specific binding definitions in your function. To learn more about bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings).

## Local development

When you develop functions locally, you need to update the function code to add bindings. For languages that use function.json, [Visual Studio Code](#visual-studio-code) provides tooling to add bindings to a function.

### Manually add bindings based on examples

When adding a binding to an existing function, you need to add binding-specific attributes to the function definition in code.

When adding a binding to an existing function, you need to add binding-specific annotations to the function definition in code.

When adding a binding to an existing function, you need to update the function code and add a definition to the function.json configuration file.

When adding a binding to an existing function, you need update the function definition, depending on your model:

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

Use the following table to find examples of specific binding types that you can use to guide you in updating an existing function. First, choose the language tab that corresponds to your project.

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

[Link](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-python)[Trigger](functions-bindings-cosmosdb-v2-trigger?tabs=python-v2&pivots=programming-language-python#example)[Input](functions-bindings-cosmosdb-v2-input?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-cosmosdb-v2-output?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure-Samples/functions-quickstart-python-azd-cosmosdb)[Input](functions-bindings-azure-data-explorer-input?pivots=programming-language-python#examples)[Output](functions-bindings-azure-data-explorer-output?pivots=programming-language-python#examples)[Trigger](functions-bindings-azure-sql-trigger?tabs=python-v2&pivots=programming-language-python#example)[Input](functions-bindings-azure-sql-input?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-azure-sql-output?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-python)[Trigger](functions-bindings-event-grid-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-event-grid-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-event-hubs-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-event-hubs-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-event-iot-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-event-iot-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-http-webhook-trigger?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure-Samples/functions-quickstart-python-http-azd)[Trigger](functions-bindings-storage-queue-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-storage-queue-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-rabbitmq-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-rabbitmq-output?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-sendgrid?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-service-bus-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-service-bus-output?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure-Samples/functions-quickstart-python-azd-service-bus)[Trigger](functions-bindings-signalr-service-trigger?tabs=python-v2&pivots=programming-language-python#example)[Input](functions-bindings-signalr-service-input?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-signalr-service-output?tabs=python-v2&pivots=programming-language-python)[Input](functions-bindings-storage-table-input?tabs=python-v2&pivots=programming-language-python)[Output](functions-bindings-storage-table-output?tabs=python-v2&pivots=programming-language-python)[Trigger](functions-bindings-timer?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-twilio?tabs=python-v2&pivots=programming-language-python#example)### Visual Studio Code

When you use Visual Studio Code to develop your function and your function uses a function.json file, the Azure Functions extension can automatically add a binding to an existing function.json file. To learn more, see [Add input and output bindings](functions-develop-vs-code#add-input-and-output-bindings).

## Azure portal

When you develop your functions in the [Azure portal](https://portal.azure.com), you add input and output bindings in the **Integrate** tab for a given function. The new bindings are added to either the function.json file or to the method attributes, depending on your language. The following articles show examples of how to add bindings to an existing function in the portal:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-blob -->

# Azure Blob storage bindings for Azure Functions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions integrates with [Azure Storage](../storage/) via [triggers and bindings](functions-triggers-bindings). Integrating with Blob storage allows you to build functions that react to changes in blob data as well as read and write values.

| Action | Type |
|---|---|
| Run a function as blob storage data changes |
|

[Input binding](functions-bindings-storage-blob-input)[Output binding](functions-bindings-storage-blob-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

This version introduces the ability to [connect using an identity instead of a secret](functions-reference#configure-an-identity-based-connection). For a tutorial on configuring your function apps with managed identities, see the [creating a function app with identity-based connections tutorial](functions-identity-based-connections-tutorial).

This version allows you to bind to types from [Azure.Storage.Blobs](/en-us/dotnet/api/azure.storage.blobs). Learn more about how these new types are different from `WindowsAzure.Storage`

and `Microsoft.Azure.Storage`

and how to migrate to them from the [Azure.Storage.Blobs Migration Guide](https://github.com/Azure/azure-sdk-for-net/blob/main/sdk/storage/Azure.Storage.Blobs/AzureStorageNetMigrationV12.md).

This version supports configuration of triggers and bindings through [.NET Aspire integration](dotnet-aspire-integration#connection-configuration-with-aspire).

Add the extension to your project by installing the [Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs), version 5.x or later.

Using the .NET CLI:

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs
```


Note

Azure Blobs, Azure Queues, and Azure Tables now use separate extensions and are referenced individually. For example, to use the triggers and bindings for all three services in your .NET isolated-process app, you should add the following packages to your project:

[Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs)[Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues)[Microsoft.Azure.Functions.Worker.Extensions.Tables](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Tables)

Previously, the extensions shipped together as [Microsoft.Azure.Functions.Worker.Extensions.Storage, version 4.x](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage/4.0.4). This same package also has a [5.x version](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage/5.0.0), which references the split packages for blobs and queues only. When upgrading your package references from older versions, you may therefore need to additionally reference the new [Microsoft.Azure.Functions.Worker.Extensions.Tables](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Tables) NuGet package. Also, when referencing these newer split packages, make sure you are not referencing an older version of the combined storage package, as this will result in conflicts from two definitions of the same bindings.

If you're writing your application using F#, you must also configure this extension as part of the app's [startup configuration](dotnet-isolated-process-guide#start-up-and-configuration). In the call to `ConfigureFunctionsWorkerDefaults()`

or `ConfigureFunctionsWebApplication()`

, add a delegate that takes an `IFunctionsWorkerApplication`

parameter. Then within the body of that delegate, call `ConfigureBlobStorageExtension()`

on the object:

```
let hostBuilder = new HostBuilder()
hostBuilder.ConfigureFunctionsWorkerDefaults(fun (context: HostBuilderContext) (appBuilder: IFunctionsWorkerApplicationBuilder) ->
appBuilder.ConfigureBlobStorageExtension() |> ignore
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

The isolated worker process supports parameter types according to the tables below.

**Blob trigger**

The blob trigger can bind to the following types:

| Type | Description |
|---|---|
`string` |
The blob content as a string. Use when the blob content is simple text. |
`byte[]` |
The bytes of the blob content. |
| JSON serializable types | When a blob contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

[BlobClient](/en-us/dotnet/api/azure.storage.blobs.blobclient)1,[BlockBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blockblobclient)1,[PageBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.pageblobclient)1,[AppendBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.appendblobclient)1,[BlobBaseClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blobbaseclient)11 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs 6.0.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs/) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

**Blob input binding**

When you want the function to process a single blob, the blob input binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The blob content as a string. Use when the blob content is simple text. |
`byte[]` |
The bytes of the blob content. |
| JSON serializable types | When a blob contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

[BlobClient](/en-us/dotnet/api/azure.storage.blobs.blobclient)1,[BlockBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blockblobclient)1,[PageBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.pageblobclient)1,[AppendBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.appendblobclient)1,[BlobBaseClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blobbaseclient)1When you want the function to process multiple blobs from a container, the blob input binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` or `List<T>` where `T` is one of the single blob input binding types |
An array or list of multiple blobs. Each entry represents one blob from the container. You can also bind to any interfaces implemented by these types, such as `IEnumerable<T>` . |
1 |

1 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs 6.0.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs/6.0.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

**Blob output binding**

When you want the function to write to a single blob, the blob output binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The blob content as a string. Use when the blob content is simple text. |
`byte[]` |
The bytes of the blob content. |
| JSON serializable types | An object representing the content of a JSON blob. Functions attempts to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write to multiple blobs, the blob output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single blob output binding types |
An array containing content for multiple blobs. Each entry represents the content of one blob. |

For other output scenarios, create and use a [BlobClient](/en-us/dotnet/api/azure.storage.blobs.blobclient) or [BlobContainerClient](/en-us/dotnet/api/azure.storage.blobs.blobcontainerclient) with other types from [Azure.Storage.Blobs](/en-us/dotnet/api/azure.storage.blobs) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

## SDK Binding Types

SDK Types for Azure Storage Blob are generally available! Follow the [Python SDK Bindings for Blob Sample](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-python) to get started with SDK Types for Blob in Python.

Important

Using SDK type bindings requires the [Python v2 programming model](functions-reference-python?pivots=python-mode-decorators#sdk-type-bindings).

| Binding | Parameter types | Samples |
|---|---|---|
| Blob trigger |
|

[,](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_blobclient/function_app.py)`BlobClient`

[,](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_containerclient/function_app.py)`ContainerClient`

`StorageStreamDownloader`

[BlobClient](/en-us/dotnet/api/azure.storage.blobs.blobclient),[ContainerClient](/en-us/python/api/azure-storage-blob/azure.storage.blob.containerclient),[StorageStreamDownloader](/en-us/python/api/azure-storage-blob/azure.storage.blob.storagestreamdownloader)[,](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_blobclient/function_app.py)`BlobClient`

[,](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_containerclient/function_app.py)`ContainerClient`

`StorageStreamDownloader`

## host.json settings

This section describes the function app configuration settings available for functions that use this binding. These settings only apply when using extension version 5.0.0 and higher. The example host.json file below contains only the version 2.x+ settings for this binding. For more information about function app configuration settings in versions 2.x and later versions, see [host.json reference for Azure Functions](functions-host-json).

Note

This section doesn't apply to extension versions before 5.0.0. For those earlier versions, there aren't any function app-wide configuration settings for blobs.

```
{
"version": "2.0",
"extensions": {
"blobs": {
"maxDegreeOfParallelism": 4,
"poisonBlobThreshold": 1
}
}
}
```


| Property | Default | Description |
|---|---|---|
| maxDegreeOfParallelism | 8 * (the number of available cores) | The integer number of concurrent invocations allowed for all blob-triggered functions in a given function app. The minimum allowed value is 1. |
| poisonBlobThreshold | 5 | The integer number of times to try processing a message before moving it to the poison queue. The minimum allowed value is 1. |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/container-concepts -->

# Linux container support in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you plan and develop your individual functions to run in Azure Functions, you're typically focused on the code itself. Azure Functions makes it easy to deploy just your code project to a function app in Azure. When you deploy your project to a Linux function app, your code runs in a container that is created for you automatically and seamlessly integrates with Functions management tools.

Functions also supports containerized function app deployments. In a containerized deployment, you create your own function app instance in a local Docker container from a supported based image. You can then deploy this *containerized* function app to a hosting environment in Azure. Creating your own function app container lets you customize or otherwise control the immediate runtime environment of your function code.

Important

When you create your own containers, you're required to keep the base image of your container updated to the latest supported base image. Supported base images for Azure Functions are language-specific. See the [Azure Functions base image repos](https://mcr.microsoft.com/catalog?search=functions).

The Functions team is committed to publishing monthly updates for these base images. Regular updates include the latest minor version updates and security fixes for both the Functions runtime and languages. You should regularly update your container from the latest base image and redeploy the updated version of your container. For more information, see [Maintaining custom containers](container-concepts#maintaining-custom-containers).

## Container hosting options

There are several options for hosting your containerized function apps in Azure:

| Hosting option | Benefits |
|---|---|
|
Azure Functions provides integrated support for developing, deploying, and managing containerized function apps on
Recommended hosting option for containerized function apps n Azure. |

**Azure Arc-enabled Kubernetes clusters (preview)***Hosting Azure Functions containers on Azure Arc-enabled Kubernetes clusters is currently in preview.*For more information, see[Working with containers and Azure Functions](functions-how-to-custom-container?pivots=azure-arc).[Azure Functions](functions-how-to-custom-container?pivots=azure-functions#azure-portal-create-using-containers)[Elastic Premium](functions-premium-plan)or an[App Service (Dedicated)](dedicated-plan)plan. Use Container Apps hosting for rich container support from Container Apps. Premium plan hosting provides you with the benefits of dynamic scaling. You might want to use Dedicated plan hosting to take advantage of existing unused App Service plan resources.[Kubernetes](functions-kubernetes-keda)[KEDA](https://keda.sh)(Kubernetes-based Event Driven Autoscaling) pairs seamlessly with the Azure Functions runtime and tooling to provide event driven scale in Kubernetes.**Important:**Kubernetes hosting of your containerized function apps, either by using KEDA or by direct deployment, is an open-source effort that you can use free of cost.*Best-effort*support for this hosting scenario is provided only by contributors and by the community. You're responsible for maintaining your own function app containers in a cluster, even when deploying them to Azure Kubernetes Service (AKS).## Feature support comparison

The degree to which various features and behaviors of Azure Functions are supported when running your function app in a container depends on the container hosting option you choose.

| Feature/behavior |
|
|---|

[Container Apps (direct)](../container-apps/overview)

[Premium plan](functions-premium-plan)

[Dedicated plan](dedicated-plan)

[Kubernetes](functions-kubernetes-keda)

[Event-driven scaling](event-driven-scaling)5[scale rules](../container-apps/scale-app#scale-rules))1123[Scale-to-zero instances](event-driven-scaling#scale-in-behaviors)6678[Core Tools deployment](functions-run-local#deploy-containers)`func kubernetes`

[Revisions](../container-apps/revisions)[Yes](../container-apps/revisions)[Deployment slots](functions-deployment-slots)[Streaming logs](streaming-logs)[Yes](../container-apps/log-streaming)[Yes](../container-apps/log-streaming)[Console access](../container-apps/container-console)[Yes](../container-apps/container-console)[Kudu](functions-how-to-custom-container#enable-ssh-connections))[Kudu](functions-how-to-custom-container#enable-ssh-connections))[using](https://kubernetes.io/docs/reference/kubectl/))`kubectl`

[Scale rules](../container-apps/scale-app#scale-rules)[Always-ready/pre-warmed instances](functions-premium-plan#eliminate-cold-starts)[App Service authentication](../app-service/overview-authentication-authorization)[Yes](../container-apps/authentication)[Custom domain names](../app-service/app-service-web-tutorial-custom-domain)[Yes](../container-apps/custom-domains-certificates)[Private key certificates](../app-service/overview-tls)[Yes](../container-apps/custom-domains-certificates)[Yes](../container-apps/networking)[Yes](/en-us/azure/reliability/reliability-azure-container-apps)[Yes](../container-apps/troubleshooting#use-the-diagnose-and-solve-problems-tool)[Yes](../container-apps/troubleshooting#use-the-diagnose-and-solve-problems-tool)[Yes](functions-diagnostics)[Yes](functions-diagnostics)[workload profiles](../container-apps/workload-profiles-overview))[workload profiles](../container-apps/workload-profiles-overview))[workload profiles](../container-apps/workload-profiles-overview))[workload profiles](../container-apps/workload-profiles-overview))[Configurable memory/CPU count](../container-apps/workload-profiles-overview)[Yes](../container-apps/billing#consumption-plan)[Yes](../container-apps/billing#consumption-plan)[Container Apps billing](../container-apps/billing)[Container Apps billing](../container-apps/billing)[Premium plan billing](functions-premium-plan#billing)[Dedicated plan billing](dedicated-plan#billing)[AKS pricing](/en-us/azure/aks/free-standard-pricing-tiers)- On Container Apps, the default is 10 instances, but you can set the
[maximum number of replicas](../container-apps/scale-app#scale-definition), which has an overall maximum of 1000. This setting is honored as long as there's enough cores quota available. When you create your function app from the Azure portal, you're limited to 300 instances. - In some regions, Linux apps on a Premium plan can scale to 100 instances. For more information, see the
[Premium plan article](functions-premium-plan#region-max-scale-out). - For specific limits for the various App Service plan options, see the
[App Service plan limits](../azure-resource-manager/management/azure-subscription-service-limits#azure-app-service-limits). - Requires
[KEDA](functions-kubernetes-keda); supported by most triggers. To learn which triggers support event-driven scaling, see[Considerations for Container Apps hosting](functions-container-apps-hosting#considerations-for-container-apps-hosting). - When the
[minimum number of replicas](../container-apps/scale-app#scale-definition)is set to zero, the default timeout depends on the specific triggers used in the app. - There's no maximum execution timeout duration enforced. However, the grace period given to a function execution is 60 minutes
[during scale in](event-driven-scaling#scale-in-behaviors), and a grace period of 10 minutes is given during platform updates. - Requires the App Service plan be set to
[Always On](dedicated-plan#always-on). A grace period of 10 minutes is given during platform updates.

## Maintaining custom containers

When creating your own containers, you're required to keep the base image of your container updated to the latest supported base image. Supported base images for Azure Functions are language-specific and are found in the [Azure Functions base image repos](https://mcr.microsoft.com/catalog?search=functions).

The Functions team is committed to publishing monthly updates for these base images. Regular updates include the latest minor version updates and security fixes for both the Functions runtime and languages. You should regularly update your container from the latest base image and redeploy the updated version of your container.

Choose your base image based on the language stack you're using in your function app. The following table provides examples for each stack. In general, the tag should start with `4-`

to indicate the V4 Functions runtime. When new minor versions are released, this tag will be updated to point to the new version. As you periodically rebuild your custom image, you will pull the new versions through that same tag, allowing your app to have the same updates. You shouldn't use tags that specify minor runtime versions, as these will not receive updates, and your app will potentially remain on an unpatched version, no matter how often you rebuild your custom image.

| Language Stack | Example recommended base image tags |
|---|---|
| .NET (isolated worker model) | `mcr.microsoft.com/azure-functions/dotnet-isolated:4-dotnet-isolated8.0` or`mcr.microsoft.com/azure-functions/dotnet-isolated:4-dotnet-isolated8.0-appservice` (These examples target .NET 8. Select the appropriate image for the .NET version you need.) |
| .NET (legacy in-process model) | `mcr.microsoft.com/azure-functions/dotnet:4-dotnet8.0` or`mcr.microsoft.com/azure-functions/dotnet:4-dotnet8.0-appservice` (Support will end for the in-process model on November 10, 2026. You should
|
| Java | `mcr.microsoft.com/azure-functions/java:4-java21` or`mcr.microsoft.com/azure-functions/java:4-java21-appservice` (These examples target Java 21. Select the appropriate image for the Java version you need.) |
| Node.js (JavaScript or TypeScript) | `mcr.microsoft.com/azure-functions/node:4-node22` or`mcr.microsoft.com/azure-functions/node:4-node22-appservice` (These examples target Node.js 22. Select the appropriate image for the Node.js version you need.) |
| PowerShell | `mcr.microsoft.com/azure-functions/powershell:4-powershell7.4` or`mcr.microsoft.com/azure-functions/powershell:4-powershell7.4-appservice` (These examples target PowerShell 7.4. Select the appropriate image for the PowerShell version you need.) |
| Python | `mcr.microsoft.com/azure-functions/python:4-python3.12` or`mcr.microsoft.com/azure-functions/python:4-python3.12-appservice` (These examples target Python 3.12. Select the appropriate image for the Python version you need.) |
| Custom handlers / other | `mcr.microsoft.com/azure-functions/base:4` or`mcr.microsoft.com/azure-functions/base:4-appservice` |

Base images ending in `-appservice`

enable SSH and remote debugging from the platform. Unless you need these capabilities, you can use the base images without the `-appservice`

suffix.

Important

It isn't sufficient to just have one of the above tags in your Dockerfile. You need to regularly pull the latest image from that tag so that your custom image can be rebuilt to include the latest updates. If you don't pull the latest image and rebuild, your app will continue to run on the old base image.

When you create or deploy your own containerized app using a custom image, you're responsible for making sure that your custom image staying up-to-date with our released base images. In addition to new features and improvements, these base image updates can also include security updates that are critical for your app. To ensure your app is protected, make sure you're staying up to date. You should regularly pull the latest version of the base image, rebuild your custom container image, and redeploy your app to use it.

In some cases, we're required to make platform-level changes that could mean that an app in a custom container using an old base image might stop working properly. For such major changes, we roll out updated images well in advance so that apps that take regular updates aren't negatively impacted. To avoid potential problems with your apps running in custom containers, make sure you don't fall too far behind the latest minor version released. During a support case, should we determine that your app is experiencing problems because it's on an older or unsupported version, we do request that you update your container to the latest base image version before continuing with support.

## Getting started

Use these links to get started working with Azure Functions in Linux containers:

| I want to... | See article: |
|---|---|
| Create my first containerized functions |
|

---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _security-baseline__functions-bindings-openai-assistantcreate-output_flex-consum_9f6e58.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: security-baseline.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/security-baseline -->

# Azure security baseline for Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This security baseline applies guidance from the [Microsoft cloud security benchmark version 1.0](/en-us/security/benchmark/azure/overview) to Functions. The Microsoft cloud security benchmark provides recommendations on how you can secure your cloud solutions on Azure. The content is grouped by the security controls defined by the Microsoft cloud security benchmark and the related guidance applicable to Functions.

You can monitor this security baseline and its recommendations using Microsoft Defender for Cloud. Azure Policy definitions will be listed in the Regulatory Compliance section of the Microsoft Defender for Cloud portal page.

When a feature has relevant Azure Policy Definitions, they are listed in this baseline to help you measure compliance with the Microsoft cloud security benchmark controls and recommendations. Some recommendations may require a paid Microsoft Defender plan to enable certain security scenarios.

Note

**Features** not applicable to Functions have been excluded. To see how Functions completely maps to the Microsoft cloud security benchmark, see the ** full Functions security baseline mapping file**.

## Security profile

The security profile summarizes high-impact behaviors of Functions, which may result in increased security considerations.

| Service Behavior Attribute | Value |
|---|---|
| Product Category | Compute, Web |
| Customer can access HOST / OS | No Access |
| Service can be deployed into customer's virtual network | True |
| Stores customer content at rest | True |

## Network security

*For more information, see the Microsoft cloud security benchmark: Network security.*

### NS-1: Establish network segmentation boundaries

#### Features

##### Virtual Network Integration

**Description**: Service supports deployment into customer's private Virtual Network (VNet). [Learn more](/en-us/azure/virtual-network/virtual-network-for-azure-services#services-that-can-be-deployed-into-a-virtual-network).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Configuration Guidance**: Deploy the service into a virtual network. Assign private IPs to the resource (where applicable) unless there is a strong reason to assign public IPs directly to the resource.

**Note**: Networking features are exposed by the service but need to be configured for the application. By default, public network access is allowed.

**Reference**: [Azure Functions networking options](/en-us/azure/azure-functions/functions-networking-options)

##### Network Security Group Support

**Description**: Service network traffic respects Network Security Groups rule assignment on its subnets. [Learn more](/en-us/azure/virtual-network/network-security-groups-overview).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Configuration Guidance**: Use network security groups (NSG) to restrict or monitor traffic by port, protocol, source IP address, or destination IP address. Create NSG rules to restrict your service's open ports (such as preventing management ports from being accessed from untrusted networks). Be aware that by default, NSGs deny all inbound traffic but allow traffic from virtual network and Azure Load Balancers.

**Reference**: [Azure Functions networking options](/en-us/azure/azure-functions/functions-networking-options)

### NS-2: Secure cloud services with network controls

#### Features

##### Azure Private Link

**Description**: Service native IP filtering capability for filtering network traffic (not to be confused with NSG or Azure Firewall). [Learn more](/en-us/azure/private-link/private-link-overview).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Configuration Guidance**: Deploy private endpoints for all Azure resources that support the Private Link feature, to establish a private access point for the resources.

**Reference**: [Azure Functions networking options](/en-us/azure/azure-functions/functions-networking-options)

##### Disable Public Network Access

**Description**: Service supports disabling public network access either through using service-level IP ACL filtering rule (not NSG or Azure Firewall) or using a 'Disable Public Network Access' toggle switch. [Learn more](/en-us/security/benchmark/azure/security-controls-v3-network-security#ns-2-secure-cloud-services-with-network-controls).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Feature notes**: Azure Functions can be configured with private endpoints, but there is not presently a single toggle for disabling public network access absent configuring private endpoints.

**Configuration Guidance**: Disable public network access either using the service-level IP ACL filtering rule or a toggling switch for public network access.

## Identity management

*For more information, see the Microsoft cloud security benchmark: Identity management.*

### IM-1: Use centralized identity and authentication system

#### Features

##### Azure AD Authentication Required for Data Plane Access

**Description**: Service supports using Azure AD authentication for data plane access. [Learn more](/en-us/azure/active-directory/authentication/overview-authentication).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Feature notes**: Customer-owned endpoints may be configured to require Azure AD authentication requirements. System-provided endpoints for deployment operations and advanced developer tools support Azure AD but by default have the ability to alternatively use publishing credentials. These publishing credentials can be disabled. Some data plane endpoints on the app may be accessed by administrative keys configured in the Functions host, and these are not configurable with Azure AD requirements at this time.

**Configuration Guidance**: Use Azure Active Directory (Azure AD) as the default authentication method to control your data plane access.

**Reference**: [Configure deployment credentials - disable basic authentication](/en-us/azure/app-service/deploy-configure-credentials#disable-basic-authentication)

##### Local Authentication Methods for Data Plane Access

**Description**: Local authentications methods supported for data plane access, such as a local username and password. [Learn more](/en-us/azure/app-service/overview-authentication-authorization).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | True | Microsoft |

**Feature notes**: Deployment credentials are created by default, but they can be disabled. Some operations exposed by the application runtime may be performed using an administrative key, which cannot presently be disabled. This key can be stored in Azure Key Vault, and it can be regenerated at any time. Avoid the usage of local authentication methods or accounts, these should be disabled wherever possible. Instead use Azure AD to authenticate where possible.

**Configuration Guidance**: No additional configurations are required as this is enabled on a default deployment.

**Reference**: [Disable basic authentication](/en-us/azure/app-service/deploy-configure-credentials?tabs=cli#disable-basic-authentication)

### IM-3: Manage application identities securely and automatically

#### Features

##### Managed Identities

**Description**: Data plane actions support authentication using managed identities. [Learn more](/en-us/azure/active-directory/managed-identities-azure-resources/overview).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Configuration Guidance**: Use Azure managed identities instead of service principals when possible, which can authenticate to Azure services and resources that support Azure Active Directory (Azure AD) authentication. Managed identity credentials are fully managed, rotated, and protected by the platform, avoiding hard-coded credentials in source code or configuration files.

**Reference**: [How to use managed identities for App Service and Azure Functions](/en-us/azure/app-service/overview-managed-identity?toc=%2Fazure%2Fazure-functions%2Ftoc.json)

##### Service Principals

**Description**: Data plane supports authentication using service principals. [Learn more](/en-us/powershell/azure/create-azure-service-principal-azureps).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Configuration Guidance**: There is no current Microsoft guidance for this feature configuration. Please review and determine if your organization wants to configure this security feature.

#### Microsoft Defender for Cloud monitoring

**Azure Policy built-in definitions - Microsoft.Web**:

Name(Azure portal) |
Description | Effect(s) | Version(GitHub) |
|---|---|---|---|
|

[3.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/App%20Service/UseManagedIdentity_WebApp_Audit.json)### IM-7: Restrict resource access based on conditions

#### Features

##### Conditional Access for Data Plane

**Description**: Data plane access can be controlled using Azure AD Conditional Access Policies. [Learn more](/en-us/azure/active-directory/conditional-access/overview).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Feature notes**: For data plane endpoints which are not defined by the application, conditional access would need to be configured against Azure Service Management.

**Configuration Guidance**: Define the applicable conditions and criteria for Azure Active Directory (Azure AD) conditional access in the workload. Consider common use cases such as blocking or granting access from specific locations, blocking risky sign-in behavior, or requiring organization-managed devices for specific applications.

### IM-8: Restrict the exposure of credential and secrets

#### Features

##### Service Credential and Secrets Support Integration and Storage in Azure Key Vault

**Description**: Data plane supports native use of Azure Key Vault for credential and secrets store. [Learn more](/en-us/azure/key-vault/secrets/about-secrets).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Configuration Guidance**: Ensure that secrets and credentials are stored in secure locations such as Azure Key Vault, instead of embedding them into code or configuration files.

**Reference**: [Use Key Vault references for App Service and Azure Functions](/en-us/azure/app-service/app-service-key-vault-references?toc=%2Fazure%2Fazure-functions%2Ftoc.json)

## Privileged access

*For more information, see the Microsoft cloud security benchmark: Privileged access.*

### PA-1: Separate and limit highly privileged/administrative users

#### Features

##### Local Admin Accounts

**Description**: Service has the concept of a local administrative account. [Learn more](/en-us/security/benchmark/azure/security-controls-v3-privileged-access#pa-1-separate-and-limit-highly-privilegedadministrative-users).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| False | Not Applicable | Not Applicable |

**Configuration Guidance**: This feature is not supported to secure this service.

### PA-7: Follow just enough administration (least privilege) principle

#### Features

##### Azure RBAC for Data Plane

**Description**: Azure Role-Based Access Control (Azure RBAC) can be used to managed access to service's data plane actions. [Learn more](/en-us/azure/role-based-access-control/overview).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Feature notes**: The only data-plane actions which can leverage Azure RBAC are the Kudu/SCM/deployment endpoints. These require permission over the `Microsoft.Web/sites/publish/Action`

operation. Endpoints exposed by the customer application itself are not covered by Azure RBAC.

**Configuration Guidance**: Use Azure role-based access control (Azure RBAC) to manage Azure resource access through built-in role assignments. Azure RBAC roles can be assigned to users, groups, service principals, and managed identities.

**Reference**: [RBAC permissions required to access Kudu](/en-us/azure/app-service/resources-kudu#rbac-permissions-required-to-access-kudu)

### PA-8: Determine access process for cloud provider support

#### Features

##### Customer Lockbox

**Description**: Customer Lockbox can be used for Microsoft support access. [Learn more](/en-us/azure/security/fundamentals/customer-lockbox-overview).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Configuration Guidance**: In support scenarios where Microsoft needs to access your data, use Customer Lockbox to review, then approve or reject each of Microsoft's data access requests.

## Data protection

*For more information, see the Microsoft cloud security benchmark: Data protection.*

### DP-2: Monitor anomalies and threats targeting sensitive data

#### Features

##### Data Leakage/Loss Prevention

**Description**: Service supports DLP solution to monitor sensitive data movement (in customer's content). [Learn more](/en-us/security/benchmark/azure/security-controls-v3-data-protection#dp-2-monitor-anomalies-and-threats-targeting-sensitive-data).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| False | Not Applicable | Not Applicable |

**Configuration Guidance**: This feature is not supported to secure this service.

### DP-3: Encrypt sensitive data in transit

#### Features

##### Data in Transit Encryption

**Description**: Service supports data in-transit encryption for data plane. [Learn more](/en-us/azure/security/fundamentals/double-encryption#data-in-transit).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Feature notes**: Function apps are created by default to support TLS 1.2 as a minimum version, but an app can be configured with a lower version through a configuration setting. HTTPS is not required of incoming requests by default, but this can also be set via a configuration setting, at which point any HTTP request will be automatically redirected to use HTTPS.

**Configuration Guidance**: Enable secure transfer in services where there is a native data in transit encryption feature built in. Enforce HTTPS on any web applications and services and ensure TLS v1.2 or later is used. Legacy versions such as SSL 3.0, TLS v1.0 should be disabled. For remote management of Virtual Machines, use SSH (for Linux) or RDP/TLS (for Windows) instead of an unencrypted protocol.

**Reference**: [Add and manage TLS/SSL certificates in Azure App Service](/en-us/azure/app-service/configure-ssl-certificate?toc=%2Fazure%2Fazure-functions%2Ftoc.json&tabs=apex%2Cportal)

#### Microsoft Defender for Cloud monitoring

**Azure Policy built-in definitions - Microsoft.Web**:

Name(Azure portal) |
Description | Effect(s) | Version(GitHub) |
|---|---|---|---|
|

[4.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/App%20Service/Webapp_AuditHTTP_Audit.json)### DP-4: Enable data at rest encryption by default

#### Features

##### Data at Rest Encryption Using Platform Keys

**Description**: Data at-rest encryption using platform keys is supported, any customer content at rest is encrypted with these Microsoft managed keys. [Learn more](/en-us/azure/security/fundamentals/encryption-atrest#encryption-at-rest-in-microsoft-cloud-services).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | True | Microsoft |

**Configuration Guidance**: No additional configurations are required as this is enabled on a default deployment.

### DP-5: Use customer-managed key option in data at rest encryption when required

#### Features

##### Data at Rest Encryption Using CMK

**Description**: Data at-rest encryption using customer-managed keys is supported for customer content stored by the service. [Learn more](/en-us/azure/security/fundamentals/encryption-models).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Feature notes**: Azure Functions does not directly support this feature, but an application can be configured to leverage services which do, in place of any possible data storage in Functions. Azure Files may be mounted as the file system, all App Settings, including secrets, may be stored in Azure Key Vault, and deployment options such as run-from-package may pull content from Azure Blob storage.

**Configuration Guidance**: If required for regulatory compliance, define the use case and service scope where encryption using customer-managed keys are needed. Enable and implement data at rest encryption using customer-managed key for those services.

**Reference**: [Encrypt your application data at rest using customer-managed keys](/en-us/azure/azure-functions/configure-encrypt-at-rest-using-cmk)

### DP-6: Use a secure key management process

#### Features

##### Key Management in Azure Key Vault

**Description**: The service supports Azure Key Vault integration for any customer keys, secrets, or certificates. [Learn more](/en-us/azure/key-vault/general/overview).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Configuration Guidance**: Use Azure Key Vault to create and control the life cycle of your encryption keys, including key generation, distribution, and storage. Rotate and revoke your keys in Azure Key Vault and your service based on a defined schedule or when there is a key retirement or compromise. When there is a need to use customer-managed key (CMK) in the workload, service, or application level, ensure you follow the best practices for key management: Use a key hierarchy to generate a separate data encryption key (DEK) with your key encryption key (KEK) in your key vault. Ensure keys are registered with Azure Key Vault and referenced via key IDs from the service or application. If you need to bring your own key (BYOK) to the service (such as importing HSM-protected keys from your on-premises HSMs into Azure Key Vault), follow recommended guidelines to perform initial key generation and key transfer.

**Reference**: [Use Key Vault references for App Service and Azure Functions](/en-us/azure/app-service/app-service-key-vault-references?toc=%2Fazure%2Fazure-functions%2Ftoc.json)

### DP-7: Use a secure certificate management process

#### Features

##### Certificate Management in Azure Key Vault

**Description**: The service supports Azure Key Vault integration for any customer certificates. [Learn more](/en-us/azure/key-vault/certificates/certificate-scenarios).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Configuration Guidance**: Use Azure Key Vault to create and control the certificate lifecycle, including creation, importing, rotation, revocation, storage, and purging of the certificate. Ensure the certificate generation follows defined standards without using any insecure properties, such as: insufficient key size, overly long validity period, insecure cryptography. Setup automatic rotation of the certificate in Azure Key Vault and the Azure service (if supported) based on a defined schedule or when there is a certificate expiration. If automatic rotation is not supported in the application, ensure they are still rotated using manual methods in Azure Key Vault and the application.

**Reference**: [Add a TLS/SSL certificate in Azure App Service](/en-us/azure/app-service/configure-ssl-certificate)

## Asset management

*For more information, see the Microsoft cloud security benchmark: Asset management.*

### AM-2: Use only approved services

#### Features

##### Azure Policy Support

**Description**: Service configurations can be monitored and enforced via Azure Policy. [Learn more](/en-us/azure/governance/policy/tutorials/create-and-manage).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Configuration Guidance**: Use Microsoft Defender for Cloud to configure Azure Policy to audit and enforce configurations of your Azure resources. Use Azure Monitor to create alerts when there is a configuration deviation detected on the resources. Use Azure Policy [deny] and [deploy if not exists] effects to enforce secure configuration across Azure resources.

## Logging and threat detection

*For more information, see the Microsoft cloud security benchmark: Logging and threat detection.*

### LT-1: Enable threat detection capabilities

#### Features

##### Microsoft Defender for Service / Product Offering

**Description**: Service has an offering-specific Microsoft Defender solution to monitor and alert on security issues. [Learn more](/en-us/azure/security-center/azure-defender).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Feature notes**: Defender for App Service includes Azure Functions. If this solution is enabled, function apps under the enablement scope will be included.

**Configuration Guidance**: Use Azure Active Directory (Azure AD) as the default authentication method to control your management plane access. When you get an alert from Microsoft Defender for Key Vault, investigate and respond to the alert.

**Reference**: [Defender for App Service](/en-us/azure/defender-for-cloud/defender-for-app-service-introduction)

### LT-4: Enable logging for security investigation

#### Features

##### Azure Resource Logs

**Description**: Service produces resource logs that can provide enhanced service-specific metrics and logging. The customer can configure these resource logs and send them to their own data sink like a storage account or log analytics workspace. [Learn more](/en-us/azure/azure-monitor/platform/platform-logs-overview).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Configuration Guidance**: Enable resource logs for the service. For example, Key Vault supports additional resource logs for actions that get a secret from a key vault or and Azure SQL has resource logs that track requests to a database. The content of resource logs varies by the Azure service and resource type.

**Reference**: [Monitoring Azure Functions with Azure Monitor Logs](/en-us/azure/azure-functions/functions-monitor-log-analytics)

## Backup and recovery

*For more information, see the Microsoft cloud security benchmark: Backup and recovery.*

### BR-1: Ensure regular automated backups

#### Features

##### Azure Backup

**Description**: The service can be backed up by the Azure Backup service. [Learn more](/en-us/azure/backup/backup-overview).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| False | Not Applicable | Not Applicable |

**Feature notes**: A feature for backing up an application is available if hosted on a Standard, Premium, or Isolated App Service plan. This feature does not leverage Azure Backup and does not include event sources or externally linked storage. See /azure/app-service/manage-backup for more details.

**Configuration Guidance**: This feature is not supported to secure this service.

##### Service Native Backup Capability

**Description**: Service supports its own native backup capability (if not using Azure Backup). [Learn more](/en-us/security/benchmark/azure/security-controls-v3-backup-recovery#br-1-ensure-regular-automated-backups).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Feature notes**: A backup feature is available to apps running on Standard, Premium, and Isolated App Service plans. This does not include backing up event sources or externally provided storage.

**Configuration Guidance**: There is no current Microsoft guidance for this feature configuration. Please review and determine if your organization wants to configure this security feature.

**Reference**: [Back up and restore your app in Azure App Service](/en-us/azure/app-service/manage-backup)

## Next steps

- See the
[Microsoft cloud security benchmark overview](../overview) - Learn more about
[Azure security baselines](../security-baselines-overview)


---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-openai-assistantcreate-output_flex-consumption-site-updates.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-openai-assistantcreate-output.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai-assistantcreate-output -->

# Azure OpenAI assistant create output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Azure OpenAI extension for Azure Functions is currently in preview.

The Azure OpenAI assistant create output binding allows you to create a new assistant chat bot from your function code execution.

For information on setup and configuration details of the Azure OpenAI extension, see [Azure OpenAI extensions for Azure Functions](functions-bindings-openai). To learn more about Azure OpenAI assistants, see [Azure OpenAI Assistants API](/en-us/azure/ai-services/openai/concepts/assistants).

Note

References and examples are only provided for the [Node.js v4 model](functions-reference-node?pivots=nodejs-model-v4).

Note

References and examples are only provided for the [Python v2 model](functions-reference-python?pivots=python-mode-decorators#programming-model).

Note

While both C# process models are supported, only [isolated worker model](dotnet-isolated-process-guide) examples are provided.

## Example

This example demonstrates the creation process, where the HTTP PUT function that creates a new assistant chat bot with the specified ID. The response to the prompt is returned in the HTTP response.

```
/// <summary>
/// HTTP PUT function that creates a new assistant chat bot with the specified ID.
/// </summary>
[Function(nameof(CreateAssistant))]
public static async Task<CreateChatBotOutput> CreateAssistant(
[HttpTrigger(AuthorizationLevel.Anonymous, "put", Route = "assistants/{assistantId}")] HttpRequestData req,
string assistantId)
{
string instructions =
"""
Don't make assumptions about what values to plug into functions.
Ask for clarification if a user request is ambiguous.
""";
using StreamReader reader = new(req.Body);
string request = await reader.ReadToEndAsync();
return new CreateChatBotOutput
{
HttpResponse = new ObjectResult(new { assistantId }) { StatusCode = 201 },
ChatBotCreateRequest = new AssistantCreateRequest(assistantId, instructions)
{
ChatStorageConnectionSetting = DefaultChatStorageConnectionSetting,
CollectionName = DefaultCollectionName,
},
};
}
public class CreateChatBotOutput
{
[AssistantCreateOutput()]
public AssistantCreateRequest? ChatBotCreateRequest { get; set; }
[HttpResult]
public IActionResult? HttpResponse { get; set; }
}
```


This example demonstrates the creation process, where the HTTP PUT function that creates a new assistant chat bot with the specified ID. The response to the prompt is returned in the HTTP response.

```
/**
* The default storage account setting for the table storage account.
* This constant is used to specify the connection string for the table storage
* account
* where chat data will be stored.
*/
final String DEFAULT_CHATSTORAGE = "AzureWebJobsStorage";
/**
* The default collection name for the table storage account.
* This constant is used to specify the collection name for the table storage
* account
* where chat data will be stored.
*/
final String DEFAULT_COLLECTION = "ChatState";
/*
* HTTP PUT function that creates a new assistant chat bot with the specified ID.
*/
@FunctionName("CreateAssistant")
public HttpResponseMessage createAssistant(
@HttpTrigger(
name = "req",
methods = {HttpMethod.PUT},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "assistants/{assistantId}")
HttpRequestMessage<Optional<String>> request,
@BindingName("assistantId") String assistantId,
@AssistantCreate(name = "AssistantCreate") OutputBinding<AssistantCreateRequest> message,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
String instructions = "Don't make assumptions about what values to plug into functions.\n" +
"Ask for clarification if a user request is ambiguous.";
AssistantCreateRequest assistantCreateRequest = new AssistantCreateRequest(assistantId, instructions);
assistantCreateRequest.setChatStorageConnectionSetting(DEFAULT_CHATSTORAGE);
assistantCreateRequest.setCollectionName(DEFAULT_COLLECTION);
message.setValue(assistantCreateRequest);
JSONObject response = new JSONObject();
response.put("assistantId", assistantId);
return request.createResponseBuilder(HttpStatus.CREATED)
.header("Content-Type", "application/json")
.body(response.toString())
.build();
}
```


This example demonstrates the creation process, where the HTTP PUT function that creates a new assistant chat bot with the specified ID. The response to the prompt is returned in the HTTP response.

```
const { app, input, output } = require("@azure/functions");
const CHAT_STORAGE_CONNECTION_SETTING = "AzureWebJobsStorage";
const COLLECTION_NAME = "ChatState";
const chatBotCreateOutput = output.generic({
type: 'assistantCreate'
})
app.http('CreateAssistant', {
methods: ['PUT'],
route: 'assistants/{assistantId}',
authLevel: 'anonymous',
extraOutputs: [chatBotCreateOutput],
handler: async (request, context) => {
const assistantId = request.params.assistantId
const instructions =
`
Don't make assumptions about what values to plug into functions.
Ask for clarification if a user request is ambiguous.
`
const createRequest = {
id: assistantId,
instructions: instructions,
chatStorageConnectionSetting: CHAT_STORAGE_CONNECTION_SETTING,
collectionName: COLLECTION_NAME
}
context.extraOutputs.set(chatBotCreateOutput, createRequest)
return { status: 202, jsonBody: { assistantId: assistantId } }
}
})
```


```
import { HttpRequest, InvocationContext, app, input, output } from "@azure/functions"
const CHAT_STORAGE_CONNECTION_SETTING = "AzureWebJobsStorage";
const COLLECTION_NAME = "ChatState";
const chatBotCreateOutput = output.generic({
type: 'assistantCreate'
})
app.http('CreateAssistant', {
methods: ['PUT'],
route: 'assistants/{assistantId}',
authLevel: 'anonymous',
extraOutputs: [chatBotCreateOutput],
handler: async (request: HttpRequest, context: InvocationContext) => {
const assistantId = request.params.assistantId
const instructions =
`
Don't make assumptions about what values to plug into functions.
Ask for clarification if a user request is ambiguous.
`
const createRequest = {
id: assistantId,
instructions: instructions,
chatStorageConnectionSetting: CHAT_STORAGE_CONNECTION_SETTING,
collectionName: COLLECTION_NAME
}
context.extraOutputs.set(chatBotCreateOutput, createRequest)
return { status: 202, jsonBody: { assistantId: assistantId } }
}
})
```


This example demonstrates the creation process, where the HTTP PUT function that creates a new assistant chat bot with the specified ID. The response to the prompt is returned in the HTTP response.

Here's the *function.json* file for Create Assistant:

```
{
"bindings": [
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "Request",
"route": "assistants/{assistantId}",
"methods": [
"put"
]
},
{
"type": "http",
"direction": "out",
"name": "Response"
},
{
"type": "assistantCreate",
"direction": "out",
"dataType": "string",
"name": "Requests"
}
]
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

{{This comes from the example code comment}}

```
using namespace System.Net
param($Request, $TriggerMetadata)
$assistantId = $Request.params.assistantId
$instructions = "Don't make assumptions about what values to plug into functions."
$instructions += "\nAsk for clarification if a user request is ambiguous."
$create_request = @{
"id" = $assistantId
"instructions" = $instructions
"chatStorageConnectionSetting" = "AzureWebJobsStorage"
"collectionName" = "ChatState"
}
Push-OutputBinding -Name Requests -Value (ConvertTo-Json $create_request)
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::Accepted
Body = (ConvertTo-Json @{ "assistantId" = $assistantId})
Headers = @{
"Content-Type" = "application/json"
}
})
```


This example demonstrates the creation process, where the HTTP PUT function that creates a new assistant chat bot with the specified ID. The response to the prompt is returned in the HTTP response.

```
DEFAULT_CHAT_STORAGE_SETTING = "AzureWebJobsStorage"
DEFAULT_CHAT_COLLECTION_NAME = "ChatState"
@apis.function_name("CreateAssistant")
@apis.route(route="assistants/{assistantId}", methods=["PUT"])
@apis.assistant_create_output(arg_name="requests")
def create_assistant(
req: func.HttpRequest, requests: func.Out[str]
) -> func.HttpResponse:
assistantId = req.route_params.get("assistantId")
instructions = """
Don't make assumptions about what values to plug into functions.
Ask for clarification if a user request is ambiguous.
"""
create_request = {
"id": assistantId,
"instructions": instructions,
"chatStorageConnectionSetting": DEFAULT_CHAT_STORAGE_SETTING,
"collectionName": DEFAULT_CHAT_COLLECTION_NAME,
}
requests.set(json.dumps(create_request))
response_json = {"assistantId": assistantId}
return func.HttpResponse(
json.dumps(response_json), status_code=202, mimetype="application/json"
)
```


## Attributes

Apply the `CreateAssistant`

attribute to define an assistant create output binding, which supports these parameters:

| Parameter | Description |
|---|---|
Id |
The identifier of the assistant to create. |
Instructions |
Optional. The instructions that are provided to assistant to follow. |
ChatStorageConnectionSetting |
Optional. The configuration section name for the table settings for chat storage. The default value is `AzureWebJobsStorage` . |
CollectionName |
Optional. The table collection name for chat storage. The default value is `ChatState` . |

## Annotations

The `CreateAssistant`

annotation enables you to define an assistant create output binding, which supports these parameters:

| Element | Description |
|---|---|
name |
Gets or sets the name of the output binding. |
id |
The identifier of the assistant to create. |
instructions |
Optional. The instructions that are provided to assistant to follow. |
chatStorageConnectionSetting |
Optional. The configuration section name for the table settings for chat storage. The default value is `AzureWebJobsStorage` . |
collectionName |
Optional. The table collection name for chat storage. The default value is `ChatState` . |

## Decorators

During the preview, define the output binding as a `generic_output_binding`

binding of type `createAssistant`

, which supports these parameters:

| Parameter | Description |
|---|---|
arg_name |
The name of the variable that represents the binding parameter. |
id |
The identifier of the assistant to create. |
instructions |
Optional. The instructions that are provided to assistant to follow. |
chat_storage_connection_setting |
Optional. The configuration section name for the table settings for chat storage. The default value is `AzureWebJobsStorage` . |
collection_name |
Optional. The table collection name for chat storage. The default value is `ChatState` . |

## Configuration

The binding supports these configuration properties that you set in the function.json file.

| Property | Description |
|---|---|
type |
Must be `CreateAssistant` . |
direction |
Must be `out` . |
name |
The name of the output binding. |
id |
The identifier of the assistant to create. |
instructions |
Optional. The instructions that are provided to assistant to follow. |
chatStorageConnectionSetting |
Optional. The configuration section name for the table settings for chat storage. The default value is `AzureWebJobsStorage` . |
collectionName |
Optional. The table collection name for chat storage. The default value is `ChatState` . |

## Configuration

The binding supports these properties, which are defined in your code:

| Property | Description |
|---|---|
id |
The identifier of the assistant to create. |
instructions |
Optional. The instructions that are provided to assistant to follow. |
chatStorageConnectionSetting |
Optional. The configuration section name for the table settings for chat storage. The default value is `AzureWebJobsStorage` . |
collectionName |
Optional. The table collection name for chat storage. The default value is `ChatState` . |

## Usage

See the [Example section](#example) for complete examples.


---

<!-- DOCUMENTO FUSIONADO: flex-consumption-site-updates.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/flex-consumption-site-updates -->

# Site update strategies in Flex Consumption

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you host your app with Azure Functions in the [Flex Consumption plan](flex-consumption-plan), you can control how updates are deployed to running instances. A site update occurs whenever you deploy code, modify application settings, or change other configuration properties. The Flex Consumption plan provides a site configuration setting (`SiteUpdateStrategy`

) that you can use to control whether your function app experiences downtime during these updates and how in-progress executions are handled.

The Flex Consumption plan currently supports these update strategies:

**Recreate**: Functions restarts all running instances after replacing your code with the latest version. This approach might cause brief downtime while instances are recycled and preserves the default behavior from other Azure Functions hosting plans.**Rolling update**(preview): Provides zero-downtime deployments by draining and replacing instances in batches. In-progress executions complete naturally without forced termination.

Important

The rolling update strategy is currently in preview and isn't recommended for production apps. Review the current [limitations and considerations](flex-consumption-site-updates#rolling-update-strategy-considerations) before enabling this strategy in any production app.

## Strategy comparison

This table compares the two site update strategies:

| Consideration | Recreate | Rolling update |
|---|---|---|
| Downtime | Brief downtime as your app scales out from zero after the restart | No period of downtime |
| In-progress executions | Forcefully terminated | Allowed to complete within the
|

✔ Brief downtime is acceptable.

✔ You're deploying breaking changes and need a clean restart.

✔ Your functions are stateless and can handle interruptions.

✔ You have long-running or critical functions that can't be interrupted.

✔ Your changes are backward-compatible.

✔ You must preserve in-progress executions.

## Update strategy behaviors

This table compares the update process of the two strategies:

**Recreate strategy**:

**Rolling update strategy**:

- A site update (code or configuration changes) is applied to your function app.
- The recreate strategy is triggered to update running instances with the new changes.
- The platform forcefully restarts all live and draining instances.
- The scaling system immediately begins provisioning new instances with the updated version (original instances might still be deprovisioning in the background).

- A site update (code or configuration changes) is applied to your function app.
- The rolling update strategy is triggered to update running instances with the new changes.
- The platform assigns all live instances to batches.
- At regular intervals, the platform drains one batch of instances. Draining prevents instances from accepting new events while allowing in-progress executions to complete (up to the one hour maximum execution time).
- Simultaneously, the scaling platform provisions new instances running the updated version to replace the draining capacity.
- This process continues until all live instances are running the updated version.

This table compares the key characteristics of the two strategies:

**Recreate strategy**:

**Rolling update strategy**:

**Brief downtime**: Your app is unavailable while instances restart and scale out**Execution interruption**: In-progress executions are terminated immediately**No completion signal**: Monitor instance logs to track when original instances stop emitting logs

**Zero downtime**: deployments are done in batches so that executions complete without forced termination.**Asynchronous operations**: Draining and scale-out happen simultaneously without waiting for each other to complete. The scale-out isn't guaranteed to occur before the next drain interval.**Overlapping updates**: You can initiate additional rolling updates while one is in progress. All non-latest instances are drained, and only the newest version is scaled out.**Dynamic scaling**: The platform adjusts instance count based on current demand during the update.**Platform managed capacity**: When demand increases, the platform provisions more instances than it drains. When demand decreases, it creates only the necessary instances to meet current needs. This approach ensures continuous availability while optimizing resource usage.

## Rolling update strategy considerations

Keep these current behaviors and limitations in mind when using the rolling update strategy. This list is maintained during the preview period and could change as the feature approaches general availability (GA).

**Platform-managed parameters**: The platform controls the parameters (such as batch count, instances per batch, number of batches, and drain intervals) that determine rolling update behaviors. These parameters might change before GA to optimize performance and reliability.**No real-time monitoring**: There's currently no visibility into how many instances are draining, how many batches remain, or current progress percentages.**No completion signal**: However, you can monitor instance logs to estimate when an update completes.**Single-instance scenarios**: Apps running on one instance experience brief downtime similar to recreate, though in-progress executions still complete.**Durable Functions**: Because mixing versions during updates can cause unexpected behavior in a Durable orchestration, use an explicit[orchestration version match strategy](durable/durable-functions-orchestration-versioning).**Infrastructure as Code**: Deploying code and configuration changes together triggers multiple rolling updates that might overlap.**Backward compatibility**: Make sure that your changes work with the previous version during the rolling update transition period.

## Configure your update strategy

You can set the update strategy for your app using the `SiteUpdateStrategy`

site setting, which is a child of `functionAppConfig`

. By default, `SiteUpdateStrategy.type`

is set to `Recreate`

. Currently, only Bicep and ARM templates with API version `2023-12-01`

or later support changing this property.

```
functionAppConfig: {
...
siteUpdateStrategy: {
type: 'RollingUpdate'
}
...
}
```


Changes to the site update strategy take effect at the next site update. For example, changing `type`

from `Recreate`

to `RollingUpdate`

uses the recreate strategy for that update. All subsequent site updates then use rolling updates.

## Monitoring site updates

During the public preview, there's no built-in completion signal for site updates. You can use KQL queries in Application Insights as a best-effort approach to estimate rolling update progress.

### Monitoring rolling update progress

These KQL queries provide a best-effort estimate of rolling update progress by tracking instance turnover in Application Insights logs. This approach has significant limitations and shouldn't be relied upon for production automation:

```
// Rolling update completion check
let deploymentStart = datetime('2025-10-30T19:00:00Z'); // Set to your deployment start time
let checkInterval = 10s; // How often you run this query
let buffer = 30s; // Safety buffer for instance detection
//
// Get original instances (active before deployment)
let originalInstances =
traces
| where timestamp between ((deploymentStart - buffer) .. deploymentStart)
| where cloud_RoleInstance != ""
| summarize by InstanceId = cloud_RoleInstance;
//
// Get currently active instances
let currentInstances =
traces
| where timestamp >= now() - checkInterval
| where cloud_RoleInstance != ""
| summarize by InstanceId = cloud_RoleInstance;
//
// Check completion status
currentInstances
| join kind=leftouter (originalInstances | extend IsOriginal = true) on InstanceId
| extend IsOriginal = isnotnull(IsOriginal)
| summarize
OriginalStillActiveInstances = make_set_if(InstanceId, IsOriginal),
NewInstances = make_set_if(InstanceId, not(IsOriginal)),
OriginalStillActiveCount = countif(IsOriginal),
NewCount = countif(not(IsOriginal)),
TotalOriginal = toscalar(originalInstances | count)
| extend
RollingUpdateComplete = iff(OriginalStillActiveCount == 0, "YES", "NO"),
PercentComplete = round(100.0 * (1.0 - todouble(OriginalStillActiveCount) / todouble(TotalOriginal)), 1)
| project RollingUpdateComplete, PercentComplete, OriginalStillActiveCount, NewCount
```


How to use this query for estimation:

- Paste this query in the Logs blade of the Application Insights resource associated with your function app.
- Set
`deploymentStart`

to the timestamp when your site update returns success. - Run the query periodically to estimate progress. Set the polling interval to be at least as long as your average function execution time, and ensure the
`checkInterval`

variable in the query matches this polling frequency. - The query returns approximate values:
`RollingUpdateComplete`

: Best estimate of whether all original instances are replaced`PercentComplete`

: Estimated percentage of original instances that are replaced`OriginalStillActiveCount`

: Estimated number of original instances still running`NewCount`

: Number of new instances currently active


Keep these limitations in mind when using these queries:

**Timing gap**: The`deploymentStart`

time represents when your site update returns success, but the actual rolling update might not start immediately. During this gap, any scale-out events provision instances running the original version. Since the query only tracks instances active at`deploymentStart`

, it doesn't monitor these new original-version instances, potentially causing false completion signals.**Log-based detection**: This approach relies on application logs to infer instance state rather than directly querying instance status. Instances might be running but not actively logging, leading to false completion signals when original instances are still active but didn't emit logs within the`checkInterval`

window.

**Recommendation for production**: Use rolling updates when zero-downtime deployments are critical. Ensure your deployment pipelines don't require waiting for update completion before proceeding to subsequent steps. Use recreate when you need faster, more predictable update timing and can tolerate brief downtime.

## FAQ

**I'm used to deployment slots for zero downtime deployments. How do rolling updates differ?**

- Unlike deployment slots, rolling updates require no additional infrastructure. Set
`siteUpdateStrategy.type`

to`"RollingUpdate"`

for zero-downtime deployments. - Rolling updates preserve in-progress executions, while deployment slots terminate them during swaps.
[Certain site properties](functions-deployment-slots#manage-settings)and sticky settings can't be swapped and require modifying the production slot directly. - Unlike deployment slots, rolling updates don't provide a separate environment for you to canary test changes or route a percentage of live traffic to. If you need these features, use a plan that supports deployment slots, like Elastic Premium, or manage separate Flex Consumption apps behind a traffic manager.

**How do I roll back a site update?**

- There's currently no feature to roll back a site update. If a rollback is necessary, initiate another site update with the previous state of code or configuration.

**How are timer triggers handled?**

- Timer triggers maintain their singleton nature. Once a timer-triggered function app is marked for drain, new timer functions run on the latest version.

**I'm seeing runtime errors during the rolling update...what went wrong?**

- If new instances fail to start or encounter runtime errors, the issue is likely in the application code, dependencies, configuration settings, or environment variables that you modified.
- To resolve the issue, redeploy your last known healthy version to restore the runtime. Then test your proposed changes in a development or staging environment before reattempting. Review error logs to identify what specific change caused the issue.


---

<!-- DOCUMENTO FUSIONADO: _storage-considerations_functions-bindings-cosmosdb-v2-output.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: storage-considerations.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/storage-considerations -->

# Storage considerations for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create a function app instance in Azure, you must provide access to a default Azure Storage account. The following diagram and table detail how Azure Functions uses services in the default storage account:


| Storage service | Functions usage |
|---|---|
|

1.Deployment source for apps that run in a

[Flex Consumption plan](flex-consumption-plan).Used by default for

[task hubs in Durable Functions](durable/durable-functions-task-hubs).Can be used to store function app code for

[Linux Consumption remote build](functions-deployment-technologies#remote-build)or as part of[external package URL deployments](functions-deployment-technologies#external-package-url).[Azure Files](../storage/files/storage-files-introduction)2[Consumption Plan](consumption-plan)and[Premium Plan](functions-premium-plan).Maintain

[extension bundles](extension-bundles).Store deployment logs.

Supports

[Managed dependencies in PowerShell](functions-reference-powershell#managed-dependencies-feature).[Azure Queue storage](../storage/queues/storage-queues-introduction)[task hubs in Durable Functions](durable/durable-functions-task-hubs). Used for failure and retry handling in[specific Azure Functions triggers](functions-bindings-storage-blob-trigger). Used for object tracking by the[Blob storage trigger](functions-bindings-storage-blob-trigger).[Azure Table storage](../storage/tables/table-storage-overview)[task hubs in Durable Functions](durable/durable-functions-task-hubs).Used for tracking

[diagnostic events](functions-diagnostics).- Blob storage is the default store for function keys, but you can
[configure an alternate store](function-keys-how-to#manage-key-storage). - Azure Files is set up by default, but you can
[create an app without Azure Files](#create-an-app-without-azure-files)under certain conditions.

## Important considerations

You must strongly consider the following facts regarding the storage accounts used by your function apps:

When your function app is hosted on the Consumption plan or Premium plan, your function code and configuration files are stored in Azure Files in the linked storage account. When you delete this storage account, the content is deleted and can't be recovered. For more information, see

[Storage account was deleted](functions-recover-storage-account#storage-account-was-deleted).Important data, such as function code,

[access keys](function-keys-how-to), and other important service-related data, persist in the storage account. You must carefully manage access to the storage accounts used by function apps in the following ways:Audit and limit the access of apps and users to the storage account based on a least-privilege model. Permissions to the storage account can come from

[data actions in the assigned role](../role-based-access-control/role-definitions#control-and-data-actions)or through permission to perform the[listKeys operation](/en-us/rest/api/storagerp/storage-accounts/list-keys).Monitor both control plane activity (such as retrieving keys) and data plane operations (such as writing to a blob) in your storage account. Consider maintaining storage logs in a location other than Azure Storage. For more information, see

[Storage logs](#storage-logs).


## Storage account requirements

Storage accounts that you create during the function app creation process in the Azure portal work with the new function app. When you choose to use an existing storage account, the list provided doesn't include certain unsupported storage accounts. The following restrictions apply to storage accounts used by your function app. Make sure an existing storage account meets these requirements:

The account type must support Blob, Queue, and Table storage. Some storage accounts don't support queues and tables. These accounts include blob-only storage accounts and Azure Premium Storage. To learn more about storage account types, see

[Storage account overview](../storage/common/storage-account-overview).You can't use a network-secured storage account when your function app is hosted in the

[Consumption plan](consumption-plan).When you create your function app in the Azure portal, you can only choose an existing storage account in the same region as the function app that you create. This requirement is a performance optimization and not a strict limitation. To learn more, see

[Storage account location](#storage-account-location).When you create your function app on a plan with

[availability zone support](/en-us/azure/reliability/reliability-functions#availability-zone-support)enabled, only[zone-redundant storage accounts](../storage/common/storage-redundancy#zone-redundant-storage)are supported.

When you use deployment automation to create your function app with a network-secured storage account, you must include specific networking configurations in your ARM template or Bicep file. If you don't include these settings and resources, your automated deployment might fail in validation. For ARM template and Bicep guidance, see [Secured deployments](functions-infrastructure-as-code#secured-deployments). For an overview on configuring storage accounts with networking, see [How to use a secured storage account with Azure Functions](configure-networking-how-to).

## Storage account guidance

Every function app requires a storage account to operate. When you delete that account, your function app stops running. To troubleshoot storage-related issues, see [How to troubleshoot storage-related issues](functions-recover-storage-account). The following considerations apply to the storage account used by function apps.

### Storage account location

For best performance, your function app should use a storage account in the same region, which reduces latency. The Azure portal enforces this best practice. If you need to use a storage account in a region different from your function app, you must create your function app outside of the Azure portal.

The storage account must be accessible to the function app. If you need to use a secured storage account, consider [restricting your storage account to a virtual network](functions-networking-options#restrict-your-storage-account-to-a-virtual-network).

### Storage account connection setting

By default, function apps configure the `AzureWebJobsStorage`

connection as a connection string stored in the [AzureWebJobsStorage application setting](functions-app-settings#azurewebjobsstorage). You can also [configure AzureWebJobsStorage to use an identity-based connection](functions-reference#connecting-to-host-storage-with-an-identity) without a secret.

Function apps running in a Consumption plan (Windows only) or an Elastic Premium plan (Windows or Linux) can use Azure Files to store the images required to enable dynamic scaling. For these plans, set the connection string for the storage account in the [WEBSITE_CONTENTAZUREFILECONNECTIONSTRING](functions-app-settings#website_contentazurefileconnectionstring) setting and the name of the file share in the [WEBSITE_CONTENTSHARE](functions-app-settings#website_contentshare) setting. This value is usually the same account used for `AzureWebJobsStorage`

. You can also [create a function app that doesn't use Azure Files](#create-an-app-without-azure-files), but scaling might be limited.

Note

You must update a storage account connection string when you regenerate storage keys. For more information, see [Create an Azure storage account](../storage/common/storage-account-create).

### Shared storage accounts

Multiple function apps can share the same storage account without any problems. For example, in Visual Studio, you can develop multiple apps by using the [Azurite storage emulator](functions-develop-local#local-storage-emulator). In this case, the emulator acts like a single storage account. The same storage account that your function app uses can also store your application data. However, this approach isn't always a good idea in a production environment.

You might need to use separate storage accounts to [avoid host ID collisions](#avoiding-host-id-collisions).

### Lifecycle management policy considerations

Don't apply [lifecycle management policies](../storage/blobs/lifecycle-management-overview) to your Blob Storage account used by your function app. Functions uses Blob storage to persist important information, such as [function access keys](function-keys-how-to). Policies could remove blobs, such as keys, needed by the Functions host. If you must use policies, exclude containers used by Functions, which are prefixed with `azure-webjobs`

or `scm`

.

### Storage logs

Because function code and keys might be persisted in the storage account, logging of activity against the storage account is a good way to monitor for unauthorized access. Azure Monitor resource logs can be used to track events against the storage data plane. See [Monitoring Azure Storage](../storage/blobs/monitor-blob-storage) for details on how to configure and examine these logs.

The [Azure Monitor activity log](/en-us/azure/azure-monitor/essentials/activity-log) shows control plane events, including the [listKeys operation](/en-us/rest/api/storagerp/storage-accounts/list-keys). However, you should also configure resource logs for the storage account to track subsequent use of keys or other identity-based data plane operations. You should have at least the [StorageWrite log category](../storage/blobs/monitor-blob-storage#collection-and-routing) enabled to be able to identify modifications to the data outside of normal Functions operations.

To limit the potential impact of any broadly scoped storage permissions, consider using a nonstorage destination for these logs, such as Log Analytics. For more information, see [Monitoring Azure Blob Storage](../storage/blobs/monitor-blob-storage).

### Optimize storage performance

To maximize performance, use a separate storage account for each function app. This approach is particularly important when you have Durable Functions or Event Hubs triggered functions, which both generate a high volume of storage transactions. When your application logic interacts with Azure Storage, either directly (using the Storage SDK) or through one of the storage bindings, you should use a dedicated storage account. For example, if you have an event hub-triggered function writing some data to blob storage, use two storage accounts: one for the function app and another for the blobs that the function stores.

### Consistent routing through virtual networks

Multiple function apps hosted in the same plan can also use the same storage account for the Azure Files content share, defined by `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

. When you secure this storage account by using a virtual network, all of these apps (including slots) should use the same value for `vnetContentShareEnabled`

(formerly `WEBSITE_CONTENTOVERVNET`

) and the same virtual network integration configuration to ensure that traffic routes consistently through the intended virtual network. A mismatch in this setting between apps that use the same Azure Files storage account might result in traffic routing through public networks. In this configuration, storage account network rules block access.

## Working with blobs

A key scenario for Functions is file processing of files in a blob container, such as for image processing or sentiment analysis. To learn more, see [Process file uploads](functions-scenarios#process-file-uploads).

### Trigger on a blob container

There are several ways to run your function code based on changes to blobs in a storage container, as indicated by this diagram:


Use the following table to determine which function trigger best fits your needs for processing added or updated blobs in a container:

| Strategy | Blob trigger (polling) | Blob trigger (event-driven) | Queue trigger | Event Grid trigger |
|---|---|---|---|---|
| Latency | High (up to 10 min) | Low | Medium | Low |
|

[Blob storage](functions-bindings-storage-blob-trigger)[Blob storage](functions-bindings-storage-blob-trigger)[Queue storage](functions-bindings-storage-queue-trigger)[Event Grid](functions-bindings-event-grid-trigger)[Blob name pattern](functions-bindings-storage-blob-trigger#blob-name-patterns)[Event filters](../storage/blobs/storage-blob-event-overview#filtering-events)[Event filters](../storage/blobs/storage-blob-event-overview#filtering-events)[event subscription](../event-grid/concepts#event-subscriptions)[Flex Consumption plan](flex-consumption-plan)[inbound access restrictions](functions-networking-options#inbound-access-restrictions)3[Blob storage trigger reference](functions-bindings-storage-blob-trigger#example).`Source`

parameter value of `EventGrid`

. For more information, see [Tutorial: Trigger Azure Functions on blob containers using an event subscription](functions-event-grid-blob-trigger).[How to work with Event Grid triggers and bindings in Azure Functions](event-grid-how-tos).- Blob storage input and output bindings support blob-only accounts.
- High scale can be loosely defined as containers that have more than 100,000 blobs in them or storage accounts that have more than 100 blob updates per second.
- You can work around inbound access restrictions by having the event subscription deliver events over an encrypted channel in public IP space using a known user identity. For more information, see
[Deliver events securely using managed identities](../event-grid/deliver-events-using-managed-identity).

## Storage data encryption

Azure Storage encrypts all data in a storage account at rest. For more information, see [Azure Storage encryption for data at rest](../storage/common/storage-service-encryption).

By default, data is encrypted with Microsoft-managed keys. For more control over encryption keys, you can supply customer-managed keys to use for encryption of blob and file data. These keys must be present in Azure Key Vault for Functions to be able to access the storage account. To learn more, see [Encrypt your application data at rest using customer-managed keys](configure-encrypt-at-rest-using-cmk).

### In-region data residency

When all customer data must remain within a single region, the storage account associated with the function app must be one with [in-region redundancy](../storage/common/storage-redundancy). An in-region redundant storage account also must be used with [Azure Durable Functions](durable/durable-functions-azure-storage-provider#storage-account-selection).

Other platform-managed customer data is only stored within the region when hosting in an internally load-balanced App Service Environment (ASE). To learn more, see [ASE zone redundancy](../app-service/environment/zone-redundancy#in-region-data-residency).

## Host ID considerations

Note

The Host ID considerations in this section don't apply when your app runs in a [Flex Consumption plan](flex-consumption-plan). In this hosting plan, the Host ID value is created in a way that avoids these potential issues.

Functions uses a host ID value as a way to uniquely identify a particular function app in stored artifacts. By default, this ID is autogenerated from the name of the function app, truncated to the first 32 characters. This ID is then used when storing per-app correlation and tracking information in the linked storage account. When you have function apps with names longer than 32 characters and when the first 32 characters are identical, this truncation can result in duplicate host ID values. When two function apps with identical host IDs use the same storage account, you get a host ID collision because stored data can't be uniquely linked to the correct function app.

Note

This same kind of host ID collision can occur between a function app in a production slot and the same function app in a staging slot, when both slots use the same storage account.

In version 4.x of the Functions runtime, an error is logged and the host is stopped, resulting in a hard failure. For more information, see [HostID Truncation can cause collisions](https://github.com/Azure/azure-functions-host/issues/2015).

### Avoiding host ID collisions

You can use the following strategies to avoid host ID collisions:

- Use a separate storage account for each function app or slot involved in the collision.
- Rename one of your function apps to a value fewer than 32 characters in length, which changes the computed host ID for the app and removes the collision.
- Set an explicit host ID for one or more of the colliding apps. To learn more, see
[Override the host ID](#override-the-host-id).

Important

Changing the storage account associated with an existing function app or changing the app's host ID can affect the behavior of existing functions. For example, a Blob storage trigger tracks whether it's processed individual blobs by writing receipts under a specific host ID path in storage. When the host ID changes or you point to a new storage account, previously processed blobs could be reprocessed.

### Override the host ID

You can explicitly set a specific host ID for your function app in the application settings by using the `AzureFunctionsWebHost__hostid`

setting. For more information, see [AzureFunctionsWebHost__hostid](functions-app-settings#azurefunctionswebhost__hostid).

When the collision occurs between slots, you must set a specific host ID for each slot, including the production slot. You must also mark these settings as [deployment settings](functions-deployment-slots#create-a-deployment-setting) so they don't get swapped. To learn how to create app settings, see [Work with application settings](functions-how-to-use-azure-function-app-settings#settings).

## Azure Arc-enabled clusters

When your function app is deployed to an Azure Arc-enabled Kubernetes cluster, your function app might not require a storage account. In this case, functions only require a storage account when your function app uses a trigger that requires storage. The following table indicates which triggers might require a storage account and which don't.

| Not required | might require storage |
|---|---|
| •
•
•
•
•
|

[Azure SQL](functions-bindings-azure-sql)•

[Blob storage](functions-bindings-storage-blob)•

[Event Grid](functions-bindings-event-grid)•

[Event Hubs](functions-bindings-event-hubs)•

[IoT Hub](functions-bindings-event-iot)•

[Queue storage](functions-bindings-storage-queue)•

[SendGrid](functions-bindings-sendgrid)•

[SignalR](functions-bindings-signalr-service)•

[Table storage](functions-bindings-storage-table)•

[Timer](functions-bindings-timer)•

[Twilio](functions-bindings-twilio)To create a function app on an Azure Arc-enabled Kubernetes cluster without storage, you must use the Azure CLI command [az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create). The version of the Azure CLI must include version 0.1.7 or a later version of the [appservice-kube extension](/en-us/cli/azure/appservice/kube). Use the `az --version`

command to verify that the extension is installed and is the correct version.

Creating your function app resources using methods other than the Azure CLI requires an existing storage account. If you plan to use any triggers that require a storage account, you should create the account before you create the function app.

## Create an app without Azure Files

The Azure Files service provides a shared file system that supports high-scale scenarios. When your function app runs in an Elastic Premium plan or on Windows in a Consumption plan, an Azure Files share is created by default in your storage account. This share is used by Functions to enable certain features, like log streaming. It's also used as a shared package deployment location, which guarantees the consistency of your deployed function code across all instances.

By default, function apps hosted in Premium and Consumption plans use [zip deployment](deployment-zip-push), with deployment packages stored in this Azure file share. This section is only relevant to these hosting plans.

Using Azure Files requires the use of a connection string, which is stored in your app settings as [ WEBSITE_CONTENTAZUREFILECONNECTIONSTRING](functions-app-settings#website_contentazurefileconnectionstring). Azure Files doesn't currently support identity-based connections. If your scenario requires you to not store any secrets in app settings, you must remove your app's dependency on Azure Files. You can avoid this dependency by creating your app without the default Azure Files dependency.

Note

You should also consider running your function app in the Flex Consumption plan, which provides greater control over the deployment package, including the ability use managed identity connections. For more information, see [Configure deployment settings](flex-consumption-how-to#configure-deployment-settings).

To run your app without the Azure file share, you must meet the following requirements:

- You must
[deploy your package to a remote Azure Blob storage container](run-functions-from-deployment-package)and then set the URL that provides access to that package as theapp setting. This approach lets you store your app content in Blob storage instead of Azure Files, which does support`WEBSITE_RUN_FROM_PACKAGE`

[managed identities](run-functions-from-deployment-package#fetch-a-package-from-azure-blob-storage-using-a-managed-identity).

You must manually update the deployment package and maintain the deployment package URL, which likely contains a shared access signature (SAS).

You should also note the following considerations:

- The app can't use version 1.x of the Functions runtime.
- Your app can't rely on a shared writeable file system.
- Portal editing isn't supported.
- Log streaming experiences in clients such as the Azure portal default to file system logs. You should instead rely on Application Insights logs.

If the preceding requirements suit your scenario, you can proceed to create a function app without Azure Files. Create an app without the `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

and `WEBSITE_CONTENTSHARE`

app settings in one of these ways:

- Bicep/ARM templates: remove the two app settings from the ARM template or Bicep file and then deploy the app using the modified template.
- The Azure portal: unselect
**Add an Azure Files connection**in the**Storage**tab when you create the app in the Azure portal.

Azure Files is used to enable dynamic scale-out for Functions. Scaling could be limited when you run your app without Azure Files in the Elastic Premium plan and Consumption plans running on Windows.

## Mount file shares

*This functionality is current only available when running on Linux.*

You can mount existing Azure Files shares to your Linux function apps. By mounting a share to your Linux function app, you can use existing machine learning models or other data in your functions.

Important

After 30 September 2028, the option to host your function app on Linux in a Consumption plan is retired. To avoid disruptions, migrate your existing Consumption plan apps that run on Linux to the [Flex Consumption plan](flex-consumption-plan) before that date. Apps running on Windows in a Consumption plan aren't affected by this change.
For more information, see the [Linux Consumption plan retirement notice](https://go.microsoft.com/fwlink/?linkid=2335809).

You can use the following command to mount an existing share to your Linux function app.

[az webapp config storage-account add](/en-us/cli/azure/webapp/config/storage-account#az-webapp-config-storage-account-add)

In this command, `share-name`

is the name of the existing Azure Files share. `custom-id`

can be any string that uniquely defines the share when mounted to the function app. Also, `mount-path`

is the path from which the share is accessed in your function app. `mount-path`

must be in the format `/dir-name`

, and it can't start with `/home`

.

For a complete example, see [Create a Python function app and mount an Azure Files share](scripts/functions-cli-mount-files-storage-linux).

Currently, only a `storage-type`

of `AzureFiles`

is supported. You can only mount five shares to a given function app. Mounting a file share can increase the cold start time by at least 200-300 ms, or even more when the storage account is in a different region.

The mounted share is available to your function code at the `mount-path`

specified. For example, when `mount-path`

is `/path/to/mount`

, you can access the target directory by file system APIs, as in the following Python example:

```
import os
...
files_in_share = os.listdir("/path/to/mount")
```


## Related article

Learn more about Azure Functions hosting options.


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-cosmosdb-v2-output.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2-output -->

# Azure Cosmos DB output binding for Azure Functions 2.x and higher

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Cosmos DB output binding lets you write a new document to an Azure Cosmos DB database using the SQL API.

For information on setup and configuration details, see the [overview](functions-bindings-cosmosdb-v2).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

## Example

Unless otherwise noted, examples in this article target version 3.x of the [Azure Cosmos DB extension](functions-bindings-cosmosdb-v2). For use with extension version 4.x, you need to replace the string `collection`

in property and attribute names with `container`

and `connection_string_setting`

with `connection`

.

The following code defines a `MyDocument`

type:

```
public class MyDocument
{
public string? Id { get; set; }
public string? Text { get; set; }
public int Number { get; set; }
public bool Boolean { get; set; }
}
```


In the following example, the return type is an [ IReadOnlyList<T>](/en-us/dotnet/api/system.collections.generic.ireadonlylist-1), which is a modified list of documents from trigger binding parameter:

```
using System.Collections.Generic;
using System.Linq;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.Logging;
namespace SampleApp
{
public class CosmosDBFunction
{
private readonly ILogger<CosmosDBFunction> _logger;
public CosmosDBFunction(ILogger<CosmosDBFunction> logger)
{
_logger = logger;
}
//<docsnippet_exponential_backoff_retry_example>
[Function(nameof(CosmosDBFunction))]
[ExponentialBackoffRetry(5, "00:00:04", "00:15:00")]
[CosmosDBOutput("%CosmosDb%", "%CosmosContainerOut%", Connection = "CosmosDBConnection", CreateIfNotExists = true)]
public object? Run(
[CosmosDBTrigger(
"%CosmosDb%",
"%CosmosContainerIn%",
Connection = "CosmosDBConnection",
LeaseContainerName = "leases",
CreateLeaseContainerIfNotExists = true)] IReadOnlyList<MyDocument> input,
FunctionContext context)
{
if (input != null && input.Any())
{
foreach (var doc in input)
{
_logger.LogInformation("Doc Id: {id}", doc.Id);
}
// Cosmos Output
return input.Select(p => new { id = p.Id });
}
return null;
}
//</docsnippet_exponential_backoff_retry_example>
}
```


[Queue trigger, save message to database via return value](#queue-trigger-save-message-to-database-via-return-value-java)[HTTP trigger, save one document to database via return value](#http-trigger-save-one-document-to-database-via-return-value-java)[HTTP trigger, save one document to database via OutputBinding](#http-trigger-save-one-document-to-database-via-outputbinding-java)[HTTP trigger, save multiple documents to database via OutputBinding](#http-trigger-save-multiple-documents-to-database-via-outputbinding-java)

### Queue trigger, save message to database via return value

The following example shows a Java function that adds a document to a database with data from a message in Queue storage.

```
@FunctionName("getItem")
@CosmosDBOutput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
connectionStringSetting = "AzureCosmosDBConnection")
public String cosmosDbQueryById(
@QueueTrigger(name = "msg",
queueName = "myqueue-items",
connection = "AzureWebJobsStorage")
String message,
final ExecutionContext context) {
return "{ id: \"" + System.currentTimeMillis() + "\", Description: " + message + " }";
}
```


#### HTTP trigger, save one document to database via return value

The following example shows a Java function whose signature is annotated with `@CosmosDBOutput`

and has return value of type `String`

. The JSON document returned by the function is automatically written to the corresponding Azure Cosmos DB collection.

```
@FunctionName("WriteOneDoc")
@CosmosDBOutput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
connectionStringSetting = "Cosmos_DB_Connection_String")
public String run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
final ExecutionContext context) {
// Item list
context.getLogger().info("Parameters are: " + request.getQueryParameters());
// Parse query parameter
String query = request.getQueryParameters().get("desc");
String name = request.getBody().orElse(query);
// Generate random ID
final int id = Math.abs(new Random().nextInt());
// Generate document
final String jsonDocument = "{\"id\":\"" + id + "\", " +
"\"description\": \"" + name + "\"}";
context.getLogger().info("Document to be saved: " + jsonDocument);
return jsonDocument;
}
```


### HTTP trigger, save one document to database via OutputBinding

The following example shows a Java function that writes a document to Azure Cosmos DB via an `OutputBinding<T>`

output parameter. In this example, the `outputItem`

parameter needs to be annotated with `@CosmosDBOutput`

, not the function signature. Using `OutputBinding<T>`

lets your function take advantage of the binding to write the document to Azure Cosmos DB while also allowing returning a different value to the function caller, such as a JSON or XML document.

```
@FunctionName("WriteOneDocOutputBinding")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@CosmosDBOutput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
connectionStringSetting = "Cosmos_DB_Connection_String")
OutputBinding<String> outputItem,
final ExecutionContext context) {
// Parse query parameter
String query = request.getQueryParameters().get("desc");
String name = request.getBody().orElse(query);
// Item list
context.getLogger().info("Parameters are: " + request.getQueryParameters());
// Generate random ID
final int id = Math.abs(new Random().nextInt());
// Generate document
final String jsonDocument = "{\"id\":\"" + id + "\", " +
"\"description\": \"" + name + "\"}";
context.getLogger().info("Document to be saved: " + jsonDocument);
// Set outputItem's value to the JSON document to be saved
outputItem.setValue(jsonDocument);
// return a different document to the browser or calling client.
return request.createResponseBuilder(HttpStatus.OK)
.body("Document created successfully.")
.build();
}
```


### HTTP trigger, save multiple documents to database via OutputBinding

The following example shows a Java function that writes multiple documents to Azure Cosmos DB via an `OutputBinding<T>`

output parameter. In this example, the `outputItem`

parameter is annotated with `@CosmosDBOutput`

, not the function signature. The output parameter, `outputItem`

has a list of `ToDoItem`

objects as its template parameter type. Using `OutputBinding<T>`

lets your function take advantage of the binding to write the documents to Azure Cosmos DB while also allowing returning a different value to the function caller, such as a JSON or XML document.

```
@FunctionName("WriteMultipleDocsOutputBinding")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@CosmosDBOutput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
connectionStringSetting = "Cosmos_DB_Connection_String")
OutputBinding<List<ToDoItem>> outputItem,
final ExecutionContext context) {
// Parse query parameter
String query = request.getQueryParameters().get("desc");
String name = request.getBody().orElse(query);
// Item list
context.getLogger().info("Parameters are: " + request.getQueryParameters());
// Generate documents
List<ToDoItem> items = new ArrayList<>();
for (int i = 0; i < 5; i ++) {
// Generate random ID
final int id = Math.abs(new Random().nextInt());
// Create ToDoItem
ToDoItem item = new ToDoItem(String.valueOf(id), name);
items.add(item);
}
// Set outputItem's value to the list of POJOs to be saved
outputItem.setValue(items);
context.getLogger().info("Document to be saved: " + items);
// return a different document to the browser or calling client.
return request.createResponseBuilder(HttpStatus.OK)
.body("Documents created successfully.")
.build();
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@CosmosDBOutput`

annotation on parameters that is written to Azure Cosmos DB. The annotation parameter type should be `OutputBinding<T>`

, where `T`

is either a native Java type or a POJO.

The following example shows a storage queue triggered [TypeScript function](functions-reference-node?tabs=typescript) for a queue that receives JSON in the following format:

```
{
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


The function creates Azure Cosmos DB documents in the following format for each record:

```
{
"id": "John Henry-123456",
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


Here's the TypeScript code:

```
import { app, InvocationContext, output } from '@azure/functions';
interface MyQueueItem {
name: string;
employeeId: string;
address: string;
}
interface MyCosmosItem {
id: string;
name: string;
employeeId: string;
address: string;
}
export async function storageQueueTrigger1(queueItem: MyQueueItem, context: InvocationContext): Promise<MyCosmosItem> {
return {
id: `${queueItem.name}-${queueItem.employeeId}`,
name: queueItem.name,
employeeId: queueItem.employeeId,
address: queueItem.address,
};
}
app.storageQueue('storageQueueTrigger1', {
queueName: 'inputqueue',
connection: 'MyStorageConnectionAppSetting',
return: output.cosmosDB({
databaseName: 'MyDatabase',
collectionName: 'MyCollection',
createIfNotExists: true,
connectionStringSetting: 'MyAccount_COSMOSDB',
}),
handler: storageQueueTrigger1,
});
```


To output multiple documents, return an array instead of a single object. For example:

```
return [
{
id: 'John Henry-123456',
name: 'John Henry',
employeeId: '123456',
address: 'A town nearby',
},
{
id: 'John Doe-123457',
name: 'John Doe',
employeeId: '123457',
address: 'A town far away',
},
];
```


The following example shows a storage queue triggered [JavaScript function](functions-reference-node) for a queue that receives JSON in the following format:

```
{
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


The function creates Azure Cosmos DB documents in the following format for each record:

```
{
"id": "John Henry-123456",
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


Here's the JavaScript code:

```
const { app, output } = require('@azure/functions');
const cosmosOutput = output.cosmosDB({
databaseName: 'MyDatabase',
collectionName: 'MyCollection',
createIfNotExists: true,
connectionStringSetting: 'MyAccount_COSMOSDB',
});
app.storageQueue('storageQueueTrigger1', {
queueName: 'inputqueue',
connection: 'MyStorageConnectionAppSetting',
return: cosmosOutput,
handler: (queueItem, context) => {
return {
id: `${queueItem.name}-${queueItem.employeeId}`,
name: queueItem.name,
employeeId: queueItem.employeeId,
address: queueItem.address,
};
},
});
```


To output multiple documents, return an array instead of a single object. For example:

```
return [
{
id: 'John Henry-123456',
name: 'John Henry',
employeeId: '123456',
address: 'A town nearby',
},
{
id: 'John Doe-123457',
name: 'John Doe',
employeeId: '123457',
address: 'A town far away',
},
];
```


The following example shows how to write data to Azure Cosmos DB using an output binding. The binding is declared in the function's configuration file (*functions.json*), and takes data from a queue message and writes out to an Azure Cosmos DB document.

```
{
"name": "EmployeeDocument",
"type": "cosmosDB",
"databaseName": "MyDatabase",
"collectionName": "MyCollection",
"createIfNotExists": true,
"connectionStringSetting": "MyStorageConnectionAppSetting",
"direction": "out"
}
```


In the *run.ps1* file, the object returned from the function is mapped to an `EmployeeDocument`

object, which is persisted in the database.

```
param($QueueItem, $TriggerMetadata)
Push-OutputBinding -Name EmployeeDocument -Value @{
id = $QueueItem.name + '-' + $QueueItem.employeeId
name = $QueueItem.name
employeeId = $QueueItem.employeeId
address = $QueueItem.address
}
```


The following example demonstrates how to write a document to an Azure Cosmos DB database as the output of a function. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.route()
@app.cosmos_db_output(arg_name="documents",
database_name="DB_NAME",
collection_name="COLLECTION_NAME",
create_if_not_exists=True,
connection_string_setting="CONNECTION_SETTING")
def main(req: func.HttpRequest, documents: func.Out[func.Document]) -> func.HttpResponse:
request_body = req.get_body()
documents.set(func.Document.from_json(request_body))
return 'OK'
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#azure-cosmos-db-v2-output).

| Attribute property | Description |
|---|---|
Connection |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see
|

**DatabaseName****ContainerName****CreateIfNotExists***false*because new containers are created with reserved throughput, which has cost implications. For more information, see the[pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).**PartitionKey**`CreateIfNotExists`

is true, it defines the partition key path for the created container. May include binding parameters.**ContainerThroughput**`CreateIfNotExists`

is true, it defines the [throughput](/en-us/azure/cosmos-db/set-throughput)of the created container.**PreferredLocations**`East US,South Central US,North Europe`

.## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, the following properties on the `cosmos_db_output`

:

| Property | Description |
|---|---|
`arg_name` |
The variable name used in function code that represents the list of documents with changes. |
`database_name` |
The name of the Azure Cosmos DB database with the container being monitored. |
`container_name` |
The name of the Azure Cosmos DB container being monitored. |
`create_if_not_exists` |
A Boolean value that indicates whether the database and collection should be created if they do not exist. |
`connection_string_setting` |
The connection string of the Azure Cosmos DB being monitored. |

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

From the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@CosmosDBOutput`

annotation on parameters that write to Azure Cosmos DB. The annotation supports the following properties:

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the binding configuration properties that you set in the *function.json* file, where properties differ by extension version:

| function.json property | Description |
|---|---|
connection |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see
|

**databaseName****containerName****createIfNotExists***false*because new containers are created with reserved throughput, which has cost implications. For more information, see the[pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).**partitionKey**`createIfNotExists`

is true, it defines the partition key path for the created container. May include binding parameters.**containerThroughput**`createIfNotExists`

is true, it defines the [throughput](/en-us/azure/cosmos-db/set-throughput)of the created container.**preferredLocations**`East US,South Central US,North Europe`

.See the [Example section](#example) for complete examples.

## Usage

By default, when you write to the output parameter in your function, a document is created in your database. You should specify the document ID of the output document by specifying the `id`

property in the JSON object passed to the output parameter.

Note

When you specify the ID of an existing document, it gets overwritten by the new output document.

The output function parameter must be defined as `func.Out[func.Document]`

. Refer to the [output example](#example) for details.

The parameter type supported by the Cosmos DB output binding depends on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to write to a single document, the Cosmos DB output binding can bind to the following types:

| Type | Description |
|---|---|
| JSON serializable types | An object representing the JSON content of a document. Functions attempts to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write to multiple documents, the Cosmos DB output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is JSON serializable type |
An array containing multiple documents. Each entry represents one document. |

For other output scenarios, create and use a [CosmosClient](/en-us/dotnet/api/microsoft.azure.cosmos.cosmosclient) with other types from [Microsoft.Azure.Cosmos](/en-us/dotnet/api/microsoft.azure.cosmos) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

## Connections

The `connectionStringSetting`

/`connection`

and `leaseConnectionStringSetting`

/`leaseConnection`

properties are references to environment configuration which specifies how the app should connect to Azure Cosmos DB. They may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections). This option is only available for the`connection`

and`leaseConnection`

versions from[version 4.x or higher of the extension](functions-bindings-cosmosdb-v2?tabs=extensionv4).

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

The connection string for your database account should be stored in an application setting with a name matching the value specified by the connection property of the binding configuration.

### Identity-based connections

If you are using [version 4.x or higher of the extension](functions-bindings-cosmosdb-v2?tabs=extensionv4), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). To do this, you would define settings under a common prefix which maps to the connection property in the trigger and binding configuration.

In this mode, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Account Endpoint | `<CONNECTION_NAME_PREFIX>__accountEndpoint` |
The Azure Cosmos DB account endpoint URI. | https://<database_account_name>.documents.azure.com:443/ |

Additional properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

Cosmos DB does not use Azure RBAC for data operations. Instead, it uses a [Cosmos DB built-in RBAC system](/en-us/azure/cosmos-db/how-to-setup-rbac) which is built on similar concepts. You will need to create a role assignment that provides access to your database account at runtime. Azure RBAC Management roles like [Owner](../role-based-access-control/built-in-roles#owner) are not sufficient. The following table shows built-in roles that are recommended when using the Azure Cosmos DB extension in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles1 |
|---|---|
Trigger2 |
|

[Cosmos DB Built-in Data Reader](/en-us/azure/cosmos-db/how-to-setup-rbac#built-in-role-definitions)[Cosmos DB Built-in Data Contributor](/en-us/azure/cosmos-db/how-to-setup-rbac#built-in-role-definitions)1 These roles cannot be used in an Azure RBAC role assignment. See the [Cosmos DB built-in RBAC system](/en-us/azure/cosmos-db/how-to-setup-rbac) documentation for details on how to assign these roles.

2 When using identity, Cosmos DB treats container creation as a management operation. It is not available as a data-plane operation for the trigger. You will need to ensure that you create the containers needed by the trigger (including the lease container) before setting up your function.

## Exceptions and return codes

| Binding | Reference |
|---|---|
| Azure Cosmos DB |
|
