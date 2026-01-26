---
merged_at: 2026-01-26T23:29:57.707297
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-add-output-binding-cosmos-db-vs-code -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-http-webhook -->

# Azure Functions HTTP triggers and bindings overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions may be invoked via HTTP requests to build serverless APIs and respond to [webhooks](https://en.wikipedia.org/wiki/Webhook).

| Action | Type |
|---|---|
| Run a function from an HTTP request |
|

[Output binding](functions-bindings-http-webhook-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

Add the extension to your project by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Http), version 3.x.

Note

An additional extension package is needed for [ASP.NET Core integration in .NET Isolated](dotnet-isolated-process-guide#aspnet-core-integration)

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

Note

For a reference of host.json in Functions 1.x, see [host.json reference for Azure Functions 1.x](functions-host-json-v1#http).

```
{
"extensions": {
"http": {
"routePrefix": "api",
"maxOutstandingRequests": 200,
"maxConcurrentRequests": 100,
"dynamicThrottlesEnabled": true,
"hsts": {
"isEnabled": true,
"maxAge": "10"
},
"customHeaders": {
"X-Content-Type-Options": "nosniff"
}
}
}
}
```


| Property | Default | Description | ||||||||||
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| customHeaders | none | Allows you to set custom headers in the HTTP response. The previous example adds the `X-Content-Type-Options` header to the response to avoid content type sniffing. This custom header applies to all HTTP triggered functions in the function app. |
||||||||||
| dynamicThrottlesEnabled | true* |
When enabled, this setting causes the request processing pipeline to periodically check system performance counters like `connections/threads/processes/memory/cpu/etc` and if any of those counters are over a built-in high threshold (80%), requests will be rejected with a `429 "Too Busy"` response until the counter(s) return to normal levels.*The default in a Consumption plan is `true` . The default in the Premium and Dedicated plans is `false` . |
||||||||||
| hsts | not enabled | When `isEnabled` is set to `true` , the
`HstsOptions` class |

| Property | Description |
|---|---|
| excludedHosts | A string array of host names for which the HSTS header isn't added. |
| includeSubDomains | Boolean value that indicates whether the includeSubDomain parameter of the Strict-Transport-Security header is enabled. |
| maxAge | String that defines the max-age parameter of the Strict-Transport-Security header. |
| preload | Boolean that indicates whether the preload parameter of the Strict-Transport-Security header is enabled. |

**The default for a Consumption plan is 100. The default for the Premium and Dedicated plans is unbounded (`-1`

).**The default for a Consumption plan is 200. The default for the Premium and Dedicated plans is unbounded (`-1`

).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-maven-eclipse -->

# Create your first function with Java and Eclipse

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to create a [serverless](https://azure.microsoft.com/solutions/serverless/) function project with the Eclipse IDE and Apache Maven, test and debug it, then deploy it to Azure Functions.

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Set up your development environment

To develop a functions app with Java and Eclipse, you must have the following installed:

[Java Developer Kit](/en-us/java/openjdk/download#openjdk-17), version 8, 11, 17 or 21. (Java 21 is currently supported only on Linux)[Apache Maven](https://maven.apache.org), version 3.0 or above.[Eclipse](https://www.eclipse.org/downloads/packages/), with Java and Maven support.[Azure CLI](/en-us/cli/azure)

Important

The JAVA_HOME environment variable must be set to the install location of the JDK to complete this quickstart.

It's highly recommended to also install [Azure Functions Core Tools, version 2](functions-run-local#v2), which provide a local environment for running and debugging Azure Functions.

## Create a Functions project

- In Eclipse, select the
**File**menu, then select**New -> Maven Project**. - Accept the defaults in the
**New Maven Project**dialogue and select**Next**. - Find and select the
[azure-functions-archetype](https://mvnrepository.com/artifact/com.microsoft.azure/azure-functions-archetype)and click**Next**. - Be sure to fill in values for all of the fields including
`resourceGroup`

,`appName`

, and`appRegion`

(please use a different appName other than**fabrikam-function-20170920120101928**), and eventually**Finish**.

Maven creates the project files in a new folder with a name of *artifactId*. The generated code in the project is a simple [HTTP triggered](functions-bindings-http-webhook) function that echoes the body of the triggering HTTP request.

## Run functions locally in the IDE

Note

[Azure Functions Core Tools, version 2](functions-run-local#v2) must be installed to run and debug functions locally.

- Right-click on the generated project, then choose
**Run As**and**Maven build**. - In the
**Edit Configuration**dialog, Enter`package`

in the**Goals**, then select**Run**. This will build and package the function code. - Once the build is complete, create another Run configuration as above, using
`azure-functions:run`

as the goal and name. Select**Run**to run the function in the IDE.

Terminate the runtime in the console window when you're done testing your function. Only one function host can be active and running locally at a time.

### Debug the function in Eclipse

In your **Run As** configuration set up in the previous step, change `azure-functions:run`

to `azure-functions:run -DenableDebug`

and run the updated configuration to start the function app in debug mode.

Select the **Run** menu and open **Debug Configurations**. Choose **Remote Java Application** and create a new one. Give your configuration a name and fill in the settings. The port should be consistent with the debug port opened by function host, which by default is `5005`

. After setup, click on `Debug`

to start debugging.

Set breakpoints and inspect objects in your function using the IDE. When finished, stop the debugger and the running function host. Only one function host can be active and running locally at a time.

## Deploy the function to Azure

The deploy process to Azure Functions uses account credentials from the Azure CLI. [Log in with the Azure CLI](/en-us/cli/azure/authenticate-azure-cli) before continuing using your computer's command prompt.

```
az login
```


Deploy your code into a new Function app using the `azure-functions:deploy`

Maven goal in a new **Run As** configuration.

When the deploy is complete, you see the URL you can use to access your Azure function app:

```
[INFO] Successfully deployed Function App with package.
[INFO] Deleting deployment package from Azure Storage...
[INFO] Successfully deleted deployment package fabrikam-function-20170920120101928.20170920143621915.zip
[INFO] Successfully deployed Function App at https://fabrikam-function-20170920120101928.azurewebsites.net
[INFO] ------------------------------------------------------------------------
```


## Next steps

- Review the
[Java Functions developer guide](functions-reference-java)for more information on developing Java functions. - Add additional functions with different triggers to your project using the
`azure-functions:add`

Maven target.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-add-output-binding-storage-queue-vs -->

# Connect functions to Azure Storage using Visual Studio

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions lets you connect Azure services and other resources to functions without having to write your own integration code. These *bindings*, which represent both input and output, are declared within the function definition. Data from bindings is provided to the function as parameters. A *trigger* is a special type of input binding. Although a function has only one trigger, it can have multiple input and output bindings. To learn more, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings).

This article shows you how to use Visual Studio to connect the function you created in the [previous quickstart article](functions-create-your-first-function-visual-studio) to Azure Storage. The output binding that you add to this function writes data from the HTTP request to a message in an Azure Queue storage queue.

Most bindings require a stored connection string that Functions uses to access the bound service. To make it easier, you use the Storage account that you created with your function app. The connection to this account is already stored in an app setting named `AzureWebJobsStorage`

.

## Prerequisites

Before you start this article, you must:

- Complete
[part 1 of the Visual Studio quickstart](functions-create-your-first-function-visual-studio). - Install
[Azure Storage Explorer](https://storageexplorer.com/). Storage Explorer is a tool that you'll use to examine queue messages generated by your output binding. Storage Explorer is supported on macOS, Windows, and Linux-based operating systems. - Sign in to your Azure subscription from Visual Studio.

## Download the function app settings

In the [previous quickstart article](how-to-create-function-vs-code?pivot=programming-language-csharp), you created a function app in Azure along with the required Storage account. The connection string for this account is stored securely in app settings in Azure. In this article, you write messages to a Storage queue in the same account. To connect to your Storage account when running the function locally, you must download app settings to the *local.settings.json* file.

In

**Solution Explorer**, right-click the project and select**Publish**.In the

**Publish**tab under**Hosting**, expand the three dots (**...**) and select**Manage Azure App Service settings**.Under

**AzureWebJobsStorage**, copy the**Remote**string value to**Local**, and then select**OK**.

The storage binding, which uses the `AzureWebJobsStorage`

setting for the connection, can now connect to your Queue storage when running locally.

## Register binding extensions

Because you're using a Queue storage output binding, you need the Storage bindings extension installed before you run the project. Except for HTTP and timer triggers, bindings are implemented as extension packages.

From the

**Tools**menu, select**NuGet Package Manager**>**Package Manager Console**.In the console, run the following

[Install-Package](/en-us/nuget/tools/ps-ref-install-package)command to install the Storage extensions:`Install-Package Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues`


Now, you can add the storage output binding to your project.

## Add an output binding

In a C# project, the bindings are defined as binding attributes on the function method. Specific definitions depend on whether your app runs in-process (C# class library) or in an isolated worker process.

Open the *HttpExample.cs* project file and add the following `MultiResponse`

class:

```
public class MultiResponse
{
[QueueOutput("outqueue",Connection = "AzureWebJobsStorage")]
public string[] Messages { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
```


The `MultiResponse`

class allows you to write to a storage queue named `outqueue`

and an HTTP success message. Multiple messages could be sent to the queue because the `QueueOutput`

attribute is applied to a string array.

The `Connection`

property sets the connection string for the storage account. In this case, you could omit `Connection`

because you're already using the default storage account.

## Add code that uses the output binding

After the binding is defined, you can use the `name`

of the binding to access it as an attribute in the function signature. By using an output binding, you don't have to use the Azure Storage SDK code for authentication, getting a queue reference, or writing data. The Functions runtime and queue output binding do those tasks for you.

Replace the existing `HttpExample`

class with the following code:

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
// Return a response to both HTTP trigger and storage output binding.
return new MultiResponse()
{
// Write a single message.
Messages = new string[] { message },
HttpResponse = response
};
}
}
```


## Run the function locally

To run your function, press

`F5`in Visual Studio. You might need to enable a firewall exception so that the tools can handle HTTP requests. Authorization levels are never enforced when you run a function locally.Copy the URL of your function from the Azure Functions runtime output.

Paste the URL for the HTTP request into your browser's address bar and run the request. The following image shows the response in the browser to the local GET request returned by the function:

To stop debugging, press

`Shift`+`F5`in Visual Studio.

A new queue named `outqueue`

is created in your storage account by the Functions runtime when the output binding is first used. You'll use Storage Explorer to verify that the queue was created along with the new message.

### Connect Storage Explorer to your account

Skip this section if you've already installed Azure Storage Explorer and connected it to your Azure account.

Run the

[Azure Storage Explorer](https://storageexplorer.com/)tool, select the connect icon on the left, and select**Add an account**.In the

**Connect**dialog, choose**Add an Azure account**, choose your**Azure environment**, and then select**Sign in...**.

After you successfully sign in to your account, you see all of the Azure subscriptions associated with your account. Choose your subscription and select **Open Explorer**.

### Examine the output queue

In Storage Explorer, expand the

**Queues**node, and then select the queue named**outqueue**.The queue contains the message that the queue output binding created when you ran the HTTP-triggered function. If you invoked the function with the default

`name`

value of*Azure*, the queue message is*Name passed to the function: Azure*.Run the function again, send another request, and you see a new message in the queue.


Now, it's time to republish the updated function app to Azure.

## Redeploy and verify the updated app

In

**Solution Explorer**, right-click the project and select**Publish**, then choose**Publish**to republish the project to Azure.After deployment completes, you can again use the browser to test the redeployed function. As before, append the query string

`&name=<yourname>`

to the URL.Again

[view the message in the storage queue](#examine-the-output-queue)to verify that the output binding again generates a new message in the queue.

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

You've updated your HTTP triggered function to write data to a Storage queue. To learn more about developing Functions, see [Develop Azure Functions using Visual Studio](functions-develop-vs).

Next, you should enable Application Insights monitoring for your function app:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-develop-vs -->

# Develop Azure Functions using Visual Studio

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Visual Studio provides a way to develop, test, and deploy C# class library functions to Azure. If this experience is your first with Azure Functions, see [Azure Functions overview](functions-overview).

To get started right away, consider completing the [Functions quickstart for Visual Studio](functions-create-your-first-function-visual-studio).

This article provides detailed information about how to use Visual Studio to develop C# class library functions and publish them to Azure.
There are two models for developing C# class library functions: the [isolated worker model](dotnet-isolated-process-guide) and the [in-process model](functions-dotnet-class-library).

You're reading the isolated worker model version of this article. You can select your preferred model at the top of the article.

You're reading the in-process model version of this article. You can select your preferred model at the top of the article.

Important

[Support for the in-process model ends on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We recommend that you [migrate your apps to the isolated worker model](migrate-dotnet-to-isolated-model).

Unless otherwise noted, procedures and examples shown are for Visual Studio 2022. For more information about Visual Studio 2022 releases, see the [release notes](/en-us/visualstudio/releases/2022/release-notes) or the [preview release notes](/en-us/visualstudio/releases/2022/release-notes-preview).

## Prerequisites

Visual Studio 2022, including the

**Azure development**workload.Other resources that you need, such as an Azure Storage account, are created in your subscription during the publishing process.

-
If you don't have an Azure account, create a

[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

## Create an Azure Functions project

The Azure Functions project template in Visual Studio creates a C# class library project that you can publish to a function app in Azure. You can use a function app to group functions as a logical unit for easier management, deployment, scaling, and sharing of resources.

From the Visual Studio menu, select

**File**>**New**>**Project**.In the

**Create a new project**dialog, enter**functions**in the search box, select the**Azure Functions**template, and then select**Next**.In the

**Configure your new project**dialog, for**Project name**, enter a name for your project, and then select**Next**. The function app name must be valid as a C# namespace, so don't use underscores, hyphens, or any other nonalphanumeric characters.In the

**Additional information**dialog, take the actions listed in the following table:Setting Action Description **Functions worker**Select **.NET 8.0 Isolated (Long Term Support)**.Visual Studio creates a function project that runs in an [isolated worker process](dotnet-isolated-process-guide). The isolated worker process also supports other versions of .NET and .NET Framework that don't offer long term support (LTS). For more information, see[Azure Functions runtime versions overview](functions-versions).**Function**Select **Http trigger**.Visual Studio creates a function triggered by an HTTP request. **Use Azurite for runtime storage account (AzureWebJobsStorage)**Select this checkbox. Because a function app in Azure requires a storage account, one is assigned or created when you publish your project to Azure. An HTTP trigger doesn't use a Storage account connection string. All other trigger types require a valid Storage account connection string. **Authorization level**Select **Anonymous**.When you use this authorization setting, any client can trigger the created function without providing a key. This configuration makes it easy to test your new function. For more information, see [Authorization level](functions-bindings-http-webhook-trigger#http-auth).Setting Action Description **Functions worker**Select **.NET 8.0 In-process (Long Term Support)**.Visual Studio creates a function project that runs in-process with version 4.x of the Functions runtime. For more information, see [Azure Functions runtime versions overview](functions-versions).**Function**Select **Http trigger**.Visual Studio creates a function triggered by an HTTP request. **Use Azurite for runtime storage account (AzureWebJobsStorage)**Select this checkbox. Because a function app in Azure requires a storage account, one is assigned or created when you publish your project to Azure. An HTTP trigger doesn't use a Storage account connection string. All other trigger types require a valid Storage account connection string. **Authorization level**Select **Anonymous**When you use this authorization setting, any client can trigger the created function without providing a key. This configuration makes it easy to test your new function. For more information, see [Authorization level](functions-bindings-http-webhook-trigger#http-auth).Make sure you set the

**Authorization level**to**Anonymous**. If you select the default level of**Function**, you're required to present the[function key](function-keys-how-to)in requests to access your function endpoint.Select

**Create**to create the function project and HTTP trigger function.

After you create a Functions project, the project template creates a C# project, installs the `Microsoft.Azure.Functions.Worker`

and `Microsoft.Azure.Functions.Worker.Sdk`

NuGet packages, and sets the target framework.

After you create a Functions project, the project template creates a C# project, installs the `Microsoft.NET.Sdk.Functions`

NuGet package, and sets the target framework.

The new project has the following files:

*host.json*: This file provides a way for you to configure the Functions host. These settings apply both when running locally and in Azure. For more information, see[host.json reference](functions-host-json).*local.settings.json*: This file maintains settings that you use when you run functions locally. These settings aren't used when your app runs in Azure. For more information, see[Work with app settings locally](#local-settings).Important

Because the

*local.settings.json*file can contain secrets, you must exclude it from your project source control. In the**Properties**dialog for this file, make sure the**Copy to Output Directory**setting is set to**Copy if newer**.

For more information, see [Project structure](dotnet-isolated-process-guide#project-structure) in the isolated worker guide.

For more information, see [Functions class library project](functions-dotnet-class-library#functions-class-library-project).

## Work with app settings locally

When your function app runs in Azure, settings required by your functions are [stored encrypted in app settings](functions-how-to-use-azure-function-app-settings#settings). During local development, these settings are instead added to the `Values`

collection in the *local.settings.json* file. The *local.settings.json* file also stores settings used by local development tools.

Items in the `Values`

collection in your project's *local.settings.json* file are intended to mirror items in your function app's [application settings](functions-how-to-use-azure-function-app-settings#settings) in Azure.

Visual Studio doesn't automatically upload the settings in *local.settings.json* when you publish the project. To make sure that these settings also exist in your function app in Azure, upload them after you publish your project. For more information, see [Function app settings](#function-app-settings). The values in a `ConnectionStrings`

collection aren't published.

Your code can also read the function app settings values as environment variables. For more information, see [Environment variables](functions-dotnet-class-library#environment-variables).

## Configure the project for local development

The Functions runtime uses a Storage account internally. During development, you can use a valid Storage account for this internal account, or you can use the [Azurite emulator](../storage/common/storage-use-azurite).

For all trigger types other than HTTP and webhooks, you need to set the value of the `Values.AzureWebJobsStorage`

key in the *local.settings.json* file:

- For a Storage account, set the value to the connection string of your storage account.
- For the emulator, set the value to
`UseDevelopmentStorage=true`

.

If you use the emulator, change this setting to an actual storage account connection string before deployment. For more information, see [Local storage emulator](functions-develop-local#local-storage-emulator).

To set the storage account connection string, take the following steps:

Sign in to the

[Azure portal](https://portal.azure.com), and then go to your storage account.Select

**Security + networking**>**Access keys**. Under**key1**, copy the**Connection string**value.In your Visual Studio project, open the

*local.settings.json*file. Set the value of the`AzureWebJobsStorage`

key to the connection string you copied.Repeat the previous step to add unique keys to the

`Values`

array for any other connections required by your functions.

## Add a function to your project

In C# class library functions, the bindings that the functions use are defined by applying attributes in the code. When you create your function triggers from the provided templates, the trigger attributes are applied for you.

In

**Solution Explorer**, right-click your project node and select**Add**>**New Azure Function**.In the

**Add New Item**dialog, select**Azure Function**, and then select**Add**.Select a trigger, and then set the required binding properties. If you select a Storage service trigger and you want to configure the connection, select the checkbox for configuring the trigger connection. The following example shows the settings for creating a Queue Storage trigger function.

Select

**Add**. If you select the checkbox for configuring a storage connection in the previous step, the**Connect to dependency**page appears. Select an Azurite storage emulator or**Azure Storage**, and then select**Next**.- If you select an Azurite storage emulator, the
**Connect to Storage Azurite emulator**page appears. Take the following steps:- Select
**Next**. - On the
**Summary of changes**page, select**Finish**. Visual Studio configures the dependency and creates the trigger class.

- Select
- If you select
**Azure Storage**, the**Connect to Azure Storage**page appears. Take the following steps:- Select a storage account, and then select
**Next**. Visual Studio tries to connect to your Azure account and retrieve an endpoint. - Select
**Next**. - On the
**Summary of changes**page, select**Finish**. Visual Studio configures the dependency and creates the trigger class.

- Select a storage account, and then select

This trigger example uses an application setting for the storage connection with a key named

`QueueStorage`

. This key, stored in the[local.settings.json file](functions-develop-local#local-settings-file), either references the Azurite emulator or a Storage account.- If you select an Azurite storage emulator, the
Examine the newly added class. For example, the following C# class represents a basic Queue Storage trigger function:

A

`Run()`

method is attributed with`Function`

. This attribute indicates that the method is the entry point for the function.`using System; using Azure.Storage.Queues.Models; using Microsoft.Azure.Functions.Worker; using Microsoft.Extensions.Logging; namespace Company.Function; public class QueueTriggerCSharp { private readonly ILogger<QueueTriggerCSharp> _logger; public QueueTriggerCSharp(ILogger<QueueTriggerCSharp> logger) { _logger = logger; } [Function(nameof(QueueTriggerCSharp))] public void Run([QueueTrigger("PathValue", Connection = "ConnectionValue")] QueueMessage message) { _logger.LogInformation("C# Queue trigger function processed: {messageText}", message.MessageText); } }`

A static

`Run()`

method is attributed with`FunctionName`

. This attribute indicates that the method is the entry point for the function.`using System; using Microsoft.Azure.WebJobs; using Microsoft.Azure.WebJobs.Host; using Microsoft.Extensions.Logging; namespace Company.Function { public class QueueTriggerCSharp { [FunctionName("QueueTriggerCSharp")] public void Run([QueueTrigger("PathValue", Connection = "ConnectionValue")]string myQueueItem, ILogger log) { log.LogInformation($"C# Queue trigger function processed: {myQueueItem}"); } } }`


A binding-specific attribute is applied to each binding parameter supplied to the entry point method. The attribute takes the binding information as parameters.

In the preceding code, the first parameter has a `QueueTrigger`

attribute applied, which indicates a Queue Storage trigger function. The queue name and connection string setting name are passed as parameters to the `QueueTrigger`

attribute. In your class:

- The queue name parameter should match the name of the queue you use in an earlier step to create the trigger, such as
`myqueue-items`

. - The connection string setting name should match the one you use in an earlier step to create the trigger, such as
`QueueStorage`

.

For more information, see [Azure Queue storage trigger for Azure Functions](functions-bindings-storage-queue-trigger).

Use the preceding procedure to add more functions to your function app project. Each function in the project can have a different trigger, but a function must have exactly one trigger. For more information, see [Azure Functions triggers and bindings](functions-triggers-bindings).

## Add bindings

As with triggers, input and output bindings are added to your function as binding attributes. To add bindings to a function, take the following steps:

Make sure you

[configure the project for local development](#configure-the-project-for-local-development).Add the appropriate NuGet extension package for each specific binding. For binding-specific NuGet package requirements, see the reference article for the binding. For example, for package requirements for the Azure Event Hubs trigger, see

[Azure Event Hubs trigger and bindings for Azure Functions](functions-bindings-event-hubs).Use the following command in the Package Manager Console to install a specific package:

`Install-Package Microsoft.Azure.Functions.Worker.Extensions.<BINDING_TYPE> -Version <TARGET_VERSION>`

`Install-Package Microsoft.Azure.WebJobs.Extensions.<BINDING_TYPE> -Version <TARGET_VERSION>`

In this code, replace

`<BINDING_TYPE>`

with the specific name of the binding extension, and replace`<TARGET_VERSION>`

with a specific version of the package, such as`4.0.0`

. Valid versions are listed on the individual package pages at[NuGet.org](https://nuget.org).If there are app settings that the binding needs, add them to the

`Values`

collection in the[local setting file](functions-develop-local#local-settings-file).The function uses these values when it runs locally. When the function runs in the function app in Azure, it uses the

[function app settings](#function-app-settings). Visual Studio makes it easy to[publish local settings to Azure](#function-app-settings).Add the appropriate binding attribute to the method signature. In the following code, a queue message triggers the

`Run`

function. The output binding then creates a new queue message with the same text in a different queue.`public class QueueTrigger { private readonly ILogger _logger; public QueueTrigger(ILoggerFactory loggerFactory) { _logger = loggerFactory.CreateLogger<QueueTrigger>(); } [Function("CopyQueueMessage")] [QueueOutput("myqueue-items-destination", Connection = "QueueStorage")] public string Run([QueueTrigger("myqueue-items-source", Connection = "QueueStorage")] string myQueueItem) { _logger.LogInformation($"C# Queue trigger function processed: {myQueueItem}"); return myQueueItem; } }`

The

`QueueOutput`

attribute defines the binding on the method. For multiple output bindings, you instead place this attribute on a string property of the returned object. For more information, see[Multiple output bindings](dotnet-isolated-process-guide#multiple-output-bindings).`public static class SimpleExampleWithOutput { [FunctionName("CopyQueueMessage")] public static void Run( [QueueTrigger("myqueue-items-source", Connection = "QueueStorage")] string myQueueItem, [Queue("myqueue-items-destination", Connection = "QueueStorage")] out string myQueueItemCopy, ILogger log) { log.LogInformation($"CopyQueueMessage function processed: {myQueueItem}"); myQueueItemCopy = myQueueItem; } }`

The

`Queue`

attribute on the`out`

parameter defines the output binding.The connection to Queue Storage is obtained from the

`QueueStorage`

setting. For more information, see the reference article for the specific binding.

For a full list of the bindings supported by Functions, see [Supported bindings](functions-triggers-bindings?tabs=csharp#supported-bindings). For a more complete example of this scenario, see [Connect functions to Azure Storage using Visual Studio](functions-add-output-binding-storage-queue-vs).

## Run functions locally

You can use Azure Functions Core Tools to run Functions projects on your local development computer. When you select **F5** to debug a Functions project, the local Functions host (`func.exe`

) starts to listen on a local port (usually 7071). Any callable function endpoints are written to the output, and you can use these endpoints for testing your functions. For more information, see [Develop Azure Functions locally using Core Tools](functions-run-local). You're prompted to install these tools the first time you start a function from Visual Studio.

Important

Starting with version 4.0.6517 of the Core Tools, in-process model projects must reference [version 4.5.0 or later of Microsoft.NET.Sdk.Functions](https://www.nuget.org/packages/Microsoft.NET.Sdk.Functions/4.5.0). If you use an earlier version, the

`func start`

command generates an error.To start your function in Visual Studio in debug mode, take the following steps:

Select

**F5**. If prompted, accept the request from Visual Studio to download and install Azure Functions Core Tools. You might also need to turn on a firewall exception so that the tools can handle HTTP requests.When the project runs, test your code the same way you test a deployed function.

When you run Visual Studio in debug mode, breakpoints are hit as expected.


For a more detailed testing scenario that uses Visual Studio, see [Test functions](#test-functions), later in this article.

## Publish to Azure

When you publish your Functions project to Azure, Visual Studio uses [zip deployment](functions-deployment-technologies#zip-deploy) to deploy the project files. When possible, you should also select **Run from package file** so that the project runs in the deployment (.zip) package. For more information, see [Run your functions from a package file in Azure](run-functions-from-deployment-package).

Don't deploy to Functions by using Web Deploy (`msdeploy`

).

Use the following steps to publish your project to a function app in Azure:

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

## Function app settings

Visual Studio doesn't upload app settings automatically when you publish your project. If you add settings to the *local.settings.json* file, you must also add them to the function app in Azure.

The easiest way to upload the required settings to your function app in Azure is to manage them in Visual Studio. On the publish profile page, go to the **Hosting** section. Select the ellipsis (**...**), and then select **Manage Azure App Service settings**.

When you make the selection, the **Application settings** dialog opens for the function app. You can use this dialog to add application settings or modify existing ones.


For each setting, the **Local** value is the value in the *local.settings.json* file, and the **Remote** value is the value in the function app in Azure.

- To create an app setting, select
**Add setting**. - To copy a setting value from the
**Local**field to the**Remote**field, select**Insert value from Local**.

Pending changes are written to the local settings file and the function app when you select **OK**.

Note

By default, the *local.settings.json* file isn't checked into source control. As a result, if you clone a local Functions project from source control, the project doesn't have a *local.settings.json* file. You need to manually create the *local.settings.json* file in the project root so that the **Application settings** dialog works as expected.

You can also manage application settings in one of these other ways:

- Use the
[Azure portal](functions-how-to-use-azure-function-app-settings#settings). - Use the
.`--publish-local-settings`

publish option in the Azure Functions Core Tools - Use the
[Azure CLI](/en-us/cli/azure/functionapp/config/appsettings#az-functionapp-config-appsettings-set).

## Remote debugging

To debug your function app remotely, you must publish a debug configuration of your project. You also need to turn on remote debugging in your function app in Azure.

This section assumes a debug configuration to your function app is published.

### Remote debugging considerations

- Remote debugging isn't recommended on a production service.
- To use remote debugging, you must host your function app in a Premium or App Service plan.
- Remote debugging is currently only supported when running your C# app on Windows.
- If you have the Just My Code feature turned on in Visual Studio, turn it off. For instructions, see
[Enable or disable Just My Code](/en-us/visualstudio/debugger/just-my-code#BKMK_Enable_or_disable_Just_My_Code). - Avoid long stops at breakpoints when you use remote debugging. When a process is stopped for longer than a few minutes, Azure treats it as an unresponsive process and shuts it down.
- While you're debugging, the server sends data to Visual Studio, which can affect bandwidth charges. For information about bandwidth rates, see
[Pricing calculator](https://azure.microsoft.com/pricing/calculator/). - Remote debugging is automatically turned off in your function app after 48 hours. After that point, you need to turn remote debugging back on.

### Attach the debugger

When you debug an isolated worker process app, you currently need to attach the remote debugger to a separate .NET process. Several other configuration steps are also required.

To attach a remote debugger to a function app running in a process separate from the Functions host, take the following steps:

On the publish profile page, go to the

**Hosting**section. Select the ellipsis (**...**), and then select**Attach debugger**.Visual Studio connects to your function app and turns on remote debugging if it's not already turned on.

Note

Because the remote debugger can't connect to the host process, an error message might appear. In any case, the local debugger can't access your breakpoints or provide a way for you to inspect variables or step through code.

On the Visual Studio

**Debug**menu, select**Attach to Process**.In the

**Attach to Process**dialog, take the following steps:- Next to
**Connection type**, select**Microsoft Azure App Services**. - Next to
**Connection target**, select**Find**.

- Next to
In the

**Azure Attach to Process**dialog, search for and select your function app, and then select**OK**.If prompted, allow Visual Studio access through your local firewall.

Back in the

**Attach to Process**dialog, select**Show processes for all users**. Select**dotnet.exe**, and then select**Attach**.

When the operation finishes, you're attached to your C# class library code running in an isolated worker process. At this point, you can debug your function app as normal.

To attach a remote debugger to a function app running in-process with the Functions host, take the following steps.

On the publish profile page, go to the **Hosting** section. Select the ellipsis (**...**), and then select **Attach debugger**.

Visual Studio connects to your function app and turns on remote debugging if it's not already turned on. It also locates and attaches the debugger to the host process for the app. At this point, you can debug your function app as normal.

When you finish debugging, you should [turn off remote debugging](#turn-off-remote-debugging).

### Turn off remote debugging

After you finish remote debugging your code, you should turn off remote debugging in the [Azure portal](https://portal.azure.com). Remote debugging is automatically turned off after 48 hours, in case you forget.

On the publish profile page, go to the

**Hosting**section. Select the ellipsis (**...**), and then select**Open in Azure portal**. The Azure portal opens to the function app your project is deployed to.In the function app, select

**Settings**>**Configuration**, and then go to the**General settings**tab. Next to**Remote debugging**, select**Off**. Select**Save**, and then select**Continue**.

After the function app restarts, you can no longer remotely connect to your remote processes. You can use this same tab in the Azure portal to turn on remote debugging outside of Visual Studio.

## Monitor functions

The recommended way to monitor your functions is by integrating your function app with Application Insights. You should turn on this integration when you create your function app during Visual Studio publishing.

If the integration isn't set up during publishing for some reason, you should still turn on [Application Insights integration](configure-monitoring#enable-application-insights-integration) for your function app in Azure.

For more information about using Application Insights for monitoring, see [Monitor executions in Azure Functions](functions-monitoring).

## Test functions

This section describes how to create a C# in-process model project that you can test by using [xUnit](https://github.com/xunit/xunit), an open-source unit testing tool for .NET.

### Step 1: Setup

Follow these steps to configure the environment, including the app project and functions, required to support your tests:

In Visual Studio, create an Azure Functions project named

**Functions**.Create an HTTP function from the template:

- In
**Solution Explorer**, right-click the**Functions**project, and then select**Add**>**New Azure Function**. - In the
**Add New Item**dialog, select**Azure Function**, and then select**Add**. - Select
**Http trigger**, and then select**Add**. - Rename the new class
*MyHttpTrigger*.

- In
Create a timer function from the template:

- In
**Solution Explorer**, right-click the**Functions**project, and then select**Add**>**New Azure Function**. - In the
**Add New Item**dialog, select**Azure Function**, and then select**Add**. - Select
**Timer trigger**, and then select**Add**. - Rename the new class
*MyTimerTrigger*.

- In
Create an

[xUnit Test app](https://xunit.net/docs/getting-started/v3/getting-started)in the solution:- In
**Solution Explorer**, right-click the solution that contains your**Functions**project, and then select**Add**>**New Project**. - Select the
**xUnit Test Project**template, and then select**Next**. - Name the project
**Functions.Tests**.

- In
Remove the default test files from the

**Functions.Tests**project.Use NuGet to add a reference from the test app to

[Microsoft.AspNetCore.Mvc](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc/). You can use Package Manager Console, or you can take the following steps:- In
**Solution Explorer**, right-click the**Functions.Tests**project, and then select**Manage NuGet Packages**. - Search for and install
**Microsoft.AspNetCore.Mvc**.

- In
In the

**Functions.Tests**app,[add a reference](/en-us/visualstudio/ide/managing-references-in-a-project)to the**Functions**app:- In
**Solution Explorer**, right-click the**Functions.Tests**project, and then select**Add**>**Project Reference**. - Select the
**Functions**project, and then select**OK**.

- In

### Step 2: Create test classes

In this section, you create the classes that you use to run the automated tests.

Each function takes an implementation of [ ILogger](/en-us/dotnet/api/microsoft.extensions.logging.ilogger) to handle message logging. In some tests, no messages are logged, or it doesn't matter how logging is implemented. Other tests need to evaluate logged messages to determine whether a test should pass.

Create a class in your

**Functions.Tests**project named`NullScope`

and add the following code. This class provides a mock scope. In a later step, you create an implementation of`ILogger`

that uses this scope.`using System; namespace Functions.Tests { public class NullScope : IDisposable { public static NullScope Instance { get; } = new NullScope(); private NullScope() { } public void Dispose() { } } }`

Create a class in your

**Functions.Tests**project named`ListLogger`

and add the following code. This class maintains an internal list of messages to evaluate during testing. To implement the required`ILogger`

interface, the class uses the mock scope from the`NullScope`

class. The test cases pass the mock scope to the`ListLogger`

class.`using Microsoft.Extensions.Logging; using System; using System.Collections.Generic; using System.Text; namespace Functions.Tests { public class ListLogger : ILogger { public IList<string> Logs; public IDisposable BeginScope<TState>(TState state) => NullScope.Instance; public bool IsEnabled(LogLevel logLevel) => false; public ListLogger() { this.Logs = new List<string>(); } public void Log<TState>(LogLevel logLevel, EventId eventId, TState state, Exception exception, Func<TState, Exception, string> formatter) { string message = formatter(state, exception); this.Logs.Add(message); } } }`

The

`ListLogger`

class implements the following members, as contracted by the`ILogger`

interface:`BeginScope`

: Scopes add context to your logging. In this case, the test points to the static instance on the`NullScope`

class to allow the test to function.`IsEnabled`

: A default value of`false`

is provided.`Log`

: This method uses the provided`formatter`

function to format the message. The method then adds the resulting text to the`Logs`

collection.

The

`Logs`

collection is an instance of`List<string>`

and is initialized in the constructor.Create a code file in the

**Functions.Tests**project named*LoggerTypes.cs*and add the following code:`namespace Functions.Tests { public enum LoggerTypes { Null, List } }`

This enumeration specifies the type of logger that the tests use.

Create a class in the

**Functions.Tests**project named`TestFactory`

and add the following code:`using Microsoft.AspNetCore.Http; using Microsoft.AspNetCore.Http.Internal; using Microsoft.Extensions.Logging; using Microsoft.Extensions.Logging.Abstractions; using Microsoft.Extensions.Primitives; using System.Collections.Generic; namespace Functions.Tests { public class TestFactory { public static IEnumerable<object[]> Data() { return new List<object[]> { new object[] { "name", "Bernardo" }, new object[] { "name", "Ananya" }, new object[] { "name", "Vlad" } }; } private static Dictionary<string, StringValues> CreateDictionary(string key, string value) { var qs = new Dictionary<string, StringValues> { { key, value } }; return qs; } public static HttpRequest CreateHttpRequest(string queryStringKey, string queryStringValue) { var context = new DefaultHttpContext(); var request = context.Request; request.Query = new QueryCollection(CreateDictionary(queryStringKey, queryStringValue)); return request; } public static ILogger CreateLogger(LoggerTypes type = LoggerTypes.Null) { ILogger logger; if (type == LoggerTypes.List) { logger = new ListLogger(); } else { logger = NullLoggerFactory.Instance.CreateLogger("Null Logger"); } return logger; } } }`

The

`TestFactory`

class implements the following members:`Data`

: This property returns an[IEnumerable](/en-us/dotnet/api/system.collections.ienumerable)collection of sample data. The key-value pairs represent values that are passed into a query string.`CreateDictionary`

: This method accepts a key-value pair as an argument. It returns a new instance of`Dictionary`

that's used to create an instance of`QueryCollection`

to represent query string values.`CreateHttpRequest`

: This method creates an HTTP request that's initialized with the given query string parameters.`CreateLogger`

: This method returns an implementation of`ILogger`

that's used for testing. The`ILogger`

implementation depends on the specified logger type. If a list type is specified, the`ListLogger`

instance keeps track of logged messages that are available for evaluation in tests.

Create a class in the

**Functions.Tests**project named`FunctionsTests`

and add the following code:`using Microsoft.AspNetCore.Mvc; using Microsoft.Extensions.Logging; using Xunit; namespace Functions.Tests { public class FunctionsTests { private readonly ILogger logger = TestFactory.CreateLogger(); [Fact] public async void Http_trigger_should_return_known_string() { var request = TestFactory.CreateHttpRequest("name", "Bernardo"); var response = (OkObjectResult)await MyHttpTrigger.Run(request, logger); Assert.Equal("Hello, Bernardo. This HTTP triggered function executed successfully.", response.Value); } [Theory] [MemberData(nameof(TestFactory.Data), MemberType = typeof(TestFactory))] public async void Http_trigger_should_return_known_string_from_member_data(string queryStringKey, string queryStringValue) { var request = TestFactory.CreateHttpRequest(queryStringKey, queryStringValue); var response = (OkObjectResult)await MyHttpTrigger.Run(request, logger); Assert.Equal($"Hello, {queryStringValue}. This HTTP triggered function executed successfully.", response.Value); } [Fact] public void Timer_should_log_message() { var logger = (ListLogger)TestFactory.CreateLogger(LoggerTypes.List); new MyTimerTrigger().Run(null, logger); var msg = logger.Logs[0]; Assert.Contains("C# Timer trigger function executed at", msg); } } }`

This class implements the following members:

`Http_trigger_should_return_known_string`

: This test uses the query string value`name=Bernardo`

to create a request to an HTTP function. This test checks that the expected response is returned.`Http_trigger_should_return_string_from_member_data`

: This test uses xUnit attributes to provide sample data to the HTTP function.`Timer_should_log_message`

: This test creates an instance of`ListLogger`

and passes it to a timer function. After the function runs, the log is checked to make sure the expected message is present.

To access application settings in your tests, you can

[inject](functions-dotnet-dependency-injection)an`IConfiguration`

implementation with mocked environment variable values into your function.

### Step 3: Run tests

To run the tests in Visual Studio, select **View** > **Test Explorer**. In **Test Explorer**, select **Run** > **Run All Tests in View**.


### Step 4: Debug tests

To debug the tests, set a breakpoint on a test. In **Test Explorer**, select **Run** > **Debug Last Run**.
