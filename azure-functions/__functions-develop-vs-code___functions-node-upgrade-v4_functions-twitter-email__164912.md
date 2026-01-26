---
merged_at: 2026-01-26T21:02:36.342264
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-develop-vs-code.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-develop-vs-code -->

# Develop Azure Functions by using Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The [Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions) lets you develop functions locally and deploy them to Azure. If this experience is your first with Azure Functions, you can learn more at [An introduction to Azure Functions](functions-overview).

The Azure Functions extension provides these benefits:

- Edit, build, and run functions on your local development computer.
- Publish your Azure Functions project directly to Azure.
- Write your functions in various languages while taking advantage of the benefits of Visual Studio Code.

You're viewing the C# version of this article. Make sure to select your preferred Functions programming language at the start of the article.


If you're new to Functions, you might want to first complete the [Visual Studio Code quickstart article](how-to-create-function-vs-code?pivot=programming-language-csharp).

You're viewing the Java version of this article. Make sure to select your preferred Functions programming language at the start of the article.


If you're new to Functions, you might want to first complete the [Visual Studio Code quickstart article](how-to-create-function-vs-code?pivot=programming-language-java).

You're viewing the JavaScript version of this article. Make sure to select your preferred Functions programming language at the start of the article.


If you're new to Functions, you might want to first complete the [Visual Studio Code quickstart article](how-to-create-function-vs-code?pivot=programming-language-javascript).

You're viewing the PowerShell version of this article. Make sure to select your preferred Functions programming language at the start of the article.


If you're new to Functions, you might want to first complete the [Visual Studio Code quickstart article](how-to-create-function-vs-code?pivot=programming-language-powershell).

You're viewing the Python version of this article. Make sure to select your preferred Functions programming language at the start of the article.


If you're new to Functions, you might want to first complete the [Visual Studio Code quickstart article](how-to-create-function-vs-code?pivot=programming-language-python).

You're viewing the TypeScript version of this article. Make sure to select your preferred Functions programming language at the start of the article.


If you're new to Functions, you might want to first complete the [Visual Studio Code quickstart article](how-to-create-function-vs-code?pivot=programming-language-typescript).

Important

Don't mix local development and portal development for a single function app. When you publish from a local project to a function app, the deployment process overwrites any functions that you developed in the portal.

## Prerequisites

[Visual Studio Code](https://code.visualstudio.com/)installed on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions). You can also install the[Azure Tools extension pack](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack), which is recommended for working with Azure resources.An active

[Azure subscription](../guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing). If you don't yet have an account, you can create one from the extension in Visual Studio Code.

You also need these prerequisites to [run and debug your functions locally](#run-functions-locally). They're not required to just create or publish projects to Azure Functions.

- The
[Azure Functions Core Tools](functions-run-local), which enables an integrated local debugging experience. When you have the Azure Functions extension installed, the easiest way to install or update Core Tools is by running the`Azure Functions: Install or Update Azure Functions Core Tools`

command from the command palette.

The

[C# extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)for Visual Studio Code.[.NET (CLI)](/en-us/dotnet/core/tools/), which is included in the .NET SDK.

[Java](/en-us/azure/developer/java/fundamentals/java-support-on-azure), one of the[supported versions](functions-reference-java#java-versions).

[Node.js](https://nodejs.org/), one of the[supported versions](functions-reference-node#node-version). Use the`node --version`

command to check your version.

[PowerShell 7.2](/en-us/powershell/scripting/install/installing-powershell-core-on-windows)recommended. For version information, see[PowerShell versions](functions-reference-powershell#powershell-versions).

[Python](https://www.python.org/downloads/), one of the[supported versions](functions-reference-python#supported-python-versions).[Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)for Visual Studio Code.

## Create an Azure Functions project

The Functions extension lets you create the required function app project at the same time you create your first function. Use these steps to create an HTTP-triggered function in a new project. An [HTTP trigger](functions-bindings-http-webhook) is the simplest function trigger template to demonstrate.

In Visual Studio Code, press

`F1`to open the command palette. Search for and run the command`Azure Functions: Create New Project...`

. Select the directory location for your project workspace, then choose**Select**.You can either create a new folder or choose an empty folder for the project workspace, but don't choose a project folder that's already part of a workspace.

You can instead run the command

`Azure Functions: Create New Containerized Project...`

to also get a Dockerfile generated for the project.When prompted,

**Select a language**for your project. If necessary, choose a specific language version.Select the

**HTTP trigger**function template, or select**Skip for now**to create a project without a function. You can always[add a function to your project](#add-a-function-to-your-project)later.Tip

To view additional templates, select the

**Change template filter**option and set the value to**Core**or**All**.For the function name, enter

**HttpExample**, select Enter, then select**Function**authorization.This authorization level requires that you provide a

[function key](function-keys-how-to)when you call the function endpoint.From the dropdown list, select

**Add to workspace**.In the

**Do you trust the authors of the files in this folder?**window, select**Yes**.

Visual Studio Code creates a function in your chosen language and in the template for an HTTP-triggered function.

### Generated project files

The project template creates a project in your chosen language and installs the required dependencies. For any language, the new project has these files:

**host.json**: Lets you configure the Functions host. These settings apply when you're running functions locally and when you're running them in Azure. For more information, see[host.json reference](functions-host-json).**local.settings.json**: Maintains settings used when you're locally running functions. These settings are used only when you're running functions locally. For more information, see[Local settings file](#local-settings).Important

Because the

**local.settings.json**file can contain secrets, make sure to exclude the file from your project source control.**Dockerfile**(optional): Lets you create a containerized function app from your project by using an approved base image for your project. You only get this file when you run the command`Azure Functions: Create New Containerized Project...`

. You can add a Dockerfile to an existing project by using the`func init --docker-only`

command in[Core Tools](functions-core-tools-reference#func-init).

An HttpExample.cs class library file, the contents of which vary depending on whether your project runs in an [isolated worker process](dotnet-isolated-process-guide#project-structure) or [in-process](functions-dotnet-class-library#functions-class-library-project) with the Functions host.

These files are created:

A pom.xml file in the root folder that defines the project and deployment parameters, including project dependencies and the

[Java version](functions-reference-java#java-versions). The pom.xml also contains information about the Azure resources that are created during a deployment.A

[Functions.java file](functions-reference-java#triggers-and-annotations)in your src path that implements the function.

Files generated depend on the chosen Node.js programming model for Functions:

An HttpExample folder is created that contains:

- The
[function.json definition file](functions-reference-powershell#folder-structure) - A run.ps1 file, which contains the function code.

Files generated depend on the chosen Python programming model for Functions:

At this point, you can [run your HTTP trigger function locally](#run-functions-locally).

## Add a function to your project

You can add a new function to an existing project by using one of the predefined Functions trigger templates. To add a new function trigger, select F1 to open the command palette, then find and run the command **Azure Functions: Create Function**. Follow the prompts to choose your trigger type and define the required attributes of the trigger. If your trigger requires an access key or connection string to connect to a service, get that item ready before you create the function trigger.

This action adds a new C# class library (.cs) file to your project.

This action adds a new Java (.java) file to your project.

This action's results depend on the Node.js model version.

This action creates a new folder in the project. The folder contains a new **function.json** file and the new PowerShell code file.

This action's results depends on the Python model version.

## Connect to services

You can connect your function to other Azure services by adding input and output bindings. Bindings connect your function to other services without you having to write the connection code.

For example, the way that you define an output binding that writes data to a storage queue depends on your process model:

If necessary,

[add a reference to the package that supports your binding extension](#install-binding-extensions).Update the function method to add an attribute that defines the binding parameter, like

`QueueOutput`

for a queue output binding. You can use a`MultiResponse`

object to return multiple messages or multiple output streams.

For example, to add an output binding that writes data to a storage queue, update the function method to add a binding parameter defined by using the [ QueueOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.queueoutput) annotation. The

[object represents the messages that are written to an output binding when the function completes.](/en-us/java/api/com.microsoft.azure.functions.outputbinding)

`OutputBinding<T>`

For example, the way that you define the output binding that writes data to a storage queue depends on your Node.js model version:

Visual Studio Code lets you add bindings to your function.json file by following a convenient set of prompts.

To add a binding, open the command pallet (F1) and type **Azure Functions: add binding...**, choose the function for the new binding, and then follow the prompts, which vary depending on the type of binding being added to the function.

The following are example prompts to define a new storage output binding:

| Prompt | Value | Description |
|---|---|---|
Select binding direction |
`out` |
The binding is an output binding. |
Select binding with direction |
`Azure Queue Storage` |
The binding is an Azure Storage queue binding. |
The name used to identify this binding in your code |
`msg` |
Name that identifies the binding parameter referenced in your code. |
The queue to which the message will be sent |
`outqueue` |
The name of the queue that the binding writes to. When the queueName doesn't exist, the binding creates it on first use. |
Select setting from "local.settings.json" |
`MyStorageConnection` |
The name of an application setting that contains the connection string for the storage account. The `AzureWebJobsStorage` setting contains the connection string for the storage account you created with the function app. |

You can also right-click (Ctrl+click on macOS) directly on the **function.json** file in your function folder, select **Add binding**, and follow the same prompts.

In this example, the following binding is added to the `bindings`

array in your function.json file:

```
{
"type": "queue",
"direction": "out",
"name": "msg",
"queueName": "outqueue",
"connection": "MyStorageConnection"
}
```


For example, the way you define the output binding that writes data to a storage queue depends on your Python model version:

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

## Sign in to Azure

Before you can create Azure resources or publish your app, you must sign in to Azure.

If you aren't already signed in, in the

**Activity bar**, select the Azure icon. Then under**Resources**, select**Sign in to Azure**.If you're already signed in and can see your existing subscriptions, go to the next section. If you don't yet have an Azure account, select

**Create an Azure Account**. Students can select**Create an Azure for Students Account**.When you are prompted in the browser, select your Azure account and sign in by using your Azure account credentials. If you create a new account, you can sign in after your account is created.

After you successfully sign in, you can close the new browser window. The subscriptions that belong to your Azure account are displayed in the side bar.


## Create Azure resources

Before you can publish your Functions project to Azure, you must have a function app and related resources in your Azure subscription to run your code. The function app provides an execution context for your functions. When you publish from Visual Studio Code to a function app in Azure, the project is packaged and deployed to the selected function app in your Azure subscription.

When you create a function app in Azure, you can choose either a quick function app create path using defaults or a path that gives you advanced options, such as using existing Azure resources. This way, you have more control over creating the remote resources.

In this section, you create a function app in the Flex Consumption plan along with related resources in your Azure subscription. Many of the resource creation decisions are made for you based on default behaviors. For more control over the created resources, you must instead [create your function app with advanced options](functions-develop-vs-code?tabs=advanced-options#publish-to-azure).

In Visual Studio Code, select F1 to open the command palette. At the prompt (

`>`

), enter and then select**Azure Functions: Create Function App in Azure**.At the prompts, provide the following information:

Prompt Action **Select subscription**Select the Azure subscription to use. The prompt doesn't appear when you have only one subscription visible under **Resources**.**Enter a new function app name**Enter a globally unique name that's valid in a URL path. The name you enter is validated to make sure that it's unique in Azure Functions. **Select a location for new resources**Select an Azure region. For better performance, select a [region](https://azure.microsoft.com/regions/)near you. Only regions supported by Flex Consumption plans are displayed.**Select a runtime stack**Select the language version you currently run locally. **Select resource authentication type**Select **Managed identity**, which is the most secure option for connecting to the[default host storage account](storage-considerations#storage-account-guidance).In the

**Azure: Activity Log**panel, the Azure extension shows the status of individual resources as they're created in Azure.When the function app is created, the following related resources are created in your Azure subscription. The resources are named based on the name you entered for your function app.

- A
[resource group](../azure-resource-manager/management/overview), which is a logical container for related resources. - A function app, which provides the environment for executing your function code. A function app lets you group functions as a logical unit for easier management, deployment, and sharing of resources within the same hosting plan.
- An Azure App Service plan, which defines the underlying host for your function app.
- A standard
[Azure Storage account](../storage/common/storage-account-create), which is used by the Functions host to maintain state and other information about your function app. - An Application Insights instance that's connected to the function app, and which tracks the use of your functions in the app.
- A user-assigned managed identity that's added to the
[Storage Blob Data Contributor](/en-us/azure/role-based-access-control/built-in-roles/storage#storage-blob-data-contributor)role in the new default host storage account.

A notification is displayed after your function app is created and the deployment package is applied.

Tip

By default, the Azure resources required by your function app are created based on the name you enter for your function app. By default, the resources are created with the function app in the same, new resource group. If you want to customize the names of the associated resources or reuse existing resources,

[publish the project with advanced create options](functions-develop-vs-code?tabs=advanced-options#publish-to-azure).- A

## Create an Azure Container Apps deployment

Important

A new hosting method for running Azure Functions directly in Azure Container Apps is now available. See [Native Azure Functions Support in Azure Container Apps](https://techcommunity.microsoft.com/blog/appsonazureblog/announcing-native-azure-functions-support-in-azure-container-apps/4414039). This integration allows you to use the full features and capabilities of Azure Container Apps. You also benefit from the functions programming model and simplicity of autoscaling provided by Azure Functions.

We recommend this approach for most new workloads. For more information, see [Azure Functions on Azure Container Apps](../container-apps/functions-overview).

Use Visual Studio Code to create Azure resources for a containerized code project. When the extension detects the presence of a Dockerfile during resource creation, it asks if you want to deploy the container image instead of just the code. Visual Studio Code creates an Azure Container Apps environment for your containerized code project that's integrated with Azure Functions. For more information, see [Azure Container Apps hosting of Azure Functions](functions-container-apps-hosting).

Note

Container deployment requires the [Azure Container Apps extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurecontainerapps). This extension is currently in preview.

The create process depends on whether you choose a quick create or you need to use advanced options:

In Visual Studio Code, press

`F1`to open the command palette. Search for and run the command`Azure Functions: Create Function App in Azure...`

.When prompted, choose

**Container image**.Provide the following information at the prompts:

Prompt Selection **Select subscription**(optional)Choose the subscription to use. You won't see this prompt when you have only one subscription visible under **Resources**.**Enter a name for the new function app**Type a name that's valid in a URL path. The name you type is validated to make sure that it's globally unique in Functions. **Select resource authentication type**Select **Managed identity**so that your app connects to remote resources by using Microsoft Entra ID authentication instead of using shared secrets (connection strings and keys), which are less secure.**Select a location for new resources**For better performance, choose a [region](https://azure.microsoft.com/regions/)near you.When prompted,

**Enter a name for the container app environment**.The extension shows the status of individual resources as they're being created in Azure in the

**Azure: Activity Log**panel.

For more information about the resources required to run your containerized functions in Container Apps, see [Required resources](functions-infrastructure-as-code?pivots=container-apps#required-resources).

Note

You can't currently use Visual Studio Code to deploy a containerized function app to an Azure Functions-integrated Container Apps environment. You must instead publish your container image to a container registry and then set that registry image as the deployment source for your Container Apps-hosted function app. For more information, see [Create your function app in a container](functions-how-to-custom-container#create-your-function-app-in-a-container) and [Update an image in the registry](functions-how-to-custom-container#update-an-image-in-the-registry).

## Deploy project files

Set up [continuous deployment](functions-continuous-deployment) so that your function app in Azure updates when you update source files in the connected source location. You can also deploy your project files from Visual Studio Code. When you publish from Visual Studio Code, you can take advantage of the [Zip deploy technology](functions-deployment-technologies#zip-deploy).

Important

Deploying to an existing function app always overwrites the contents of that app in Azure.

In the command palette, enter and then select

**Azure Functions: Deploy to Function App**.Select the function app you just created. When prompted about overwriting previous deployments, select

**Deploy**to deploy your function code to the new function app resource.When deployment is completed, select

**View Output**to view the creation and deployment results, including the Azure resources that you created. If you miss the notification, select the bell icon in the lower-right corner to see it again.

## Get the URL of an HTTP triggered function in Azure

To call an HTTP-triggered function from a client, you need the function's URL, which is available after deployment to your function app. This URL includes any required function keys. You can use the extension to get these URLs for your deployed functions. If you just want to run the remote function in Azure, [use the Execute function now](#run-functions-in-azure) functionality of the extension.

Select F1 to open the command palette, and then find and run the command

**Azure Functions: Copy Function URL**.Follow the prompts to select your function app in Azure and then the specific HTTP trigger that you want to invoke.


The function URL is copied to the clipboard, along with any required keys passed by the `code`

query parameter. Use an HTTP tool to submit POST requests, or a browser to submit GET requests to the remote function.

When the extension gets the URL of a function in Azure, it uses your Azure account to automatically retrieve the keys needed to start the function. [Learn more about function access keys](security-concepts#function-access-keys). Starting non-HTTP triggered functions requires using the admin key.

## Run functions

The Azure Functions extension lets you run individual functions. You can run functions either in your project on your local development computer or in your Azure subscription.

For HTTP trigger functions, the extension calls the HTTP endpoint. For other kinds of triggers, the extension calls administrator APIs to start the function. The message body of the request sent to the function depends on the trigger type. When a trigger requires test data, you're prompted to enter data in a specific JSON format.

### Run functions in Azure

To execute a function in Azure from Visual Studio Code, follow these steps:

In the command palette, enter

**Azure Functions: Execute function now**, and select your Azure subscription.From the list, choose your function app in Azure. If you don't see your function app, make sure you're signed in to the correct subscription.

From the list, choose the function that you want to run. In

**Enter request body**, type the message body of the request, and press Enter to send this request message to your function.The default text in

**Enter request body**indicates the body's format. If your function app has no functions, a notification error is shown with this error.When the function executes in Azure and returns a response, Visual Studio Code shows a notification.


You can also run your function from the **Azure: Functions** area by opening the shortcut menu for the function that you want to run from your function app in your Azure subscription, and then selecting **Execute Function Now...**.

When you run your functions in Azure from Visual Studio Code, the extension uses your Azure account to automatically retrieve the keys needed to start the function. [Learn more about function access keys](security-concepts#function-access-keys). Starting non-HTTP triggered functions requires using the admin key.

### Run functions locally

The local runtime is the same runtime that hosts your function app in Azure. The runtime reads local settings from the [local.settings.json file](#local-settings). To run your Functions project locally, you must meet [more requirements](#prerequisites).

#### Configure the project to run locally

The Functions runtime uses an Azure Storage account internally for all trigger types except HTTP and webhooks. Set the **Values.AzureWebJobsStorage** key to a valid Azure Storage account connection string.

This section uses the [Azure Storage extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurestorage) with [Azure Storage Explorer](https://storageexplorer.com/) to connect to and retrieve the storage connection string.

To set the storage account connection string:

In Visual Studio, open

**Cloud Explorer**, expand**Storage Account**>**Your Storage Account**, then select**Properties**and copy the**Primary Connection String**value.In your project, open the local.settings.json file and set the value of the

**AzureWebJobsStorage**key to the connection string you copied.Repeat the previous step to add unique keys to the

**Values**array for any other connections required by your functions.

For more information, see [Local settings file](#local-settings).

#### Debug functions locally

To debug your functions, select F5. If [Core Tools](functions-run-local) isn't available, you're prompted to install it. When Core Tools is installed and running, output is shown in the Terminal. This step is the same as running the `func start`

Core Tools command from the Terminal, but with extra build tasks and an attached debugger.

When the project is running, you can use the **Execute Function Now...** feature of the extension to trigger your functions as you would when the project is deployed to Azure. With the project running in debug mode, breakpoints are hit in Visual Studio Code as you would expect.

In the command palette, enter

**Azure Functions: Execute function now**and choose**Local project**.Choose the function you want to run in your project and type the message body of the request in

**Enter request body**. Press Enter to send this request message to your function. The default text in**Enter request body**should indicate the format of the body. If your function app has no functions, a notification error is shown with this error.When the function runs locally and after the response is received, a notification is raised in Visual Studio Code. Information about the function execution is shown in

**Terminal**panel.

Keys aren't required when running locally. This rule applies to both function keys and admin-level keys.

## Work with app settings locally

When your function app runs in Azure, settings required by your functions are [stored encrypted in app settings](functions-how-to-use-azure-function-app-settings#settings). During local development, these settings are instead added to the `Values`

collection in the *local.settings.json* file. The *local.settings.json* file also stores settings used by local development tools.

Items in the `Values`

collection in your project's *local.settings.json* file are intended to mirror items in your function app's [application settings](functions-how-to-use-azure-function-app-settings#settings) in Azure.

By default, these settings aren't migrated automatically when you publish the project to Azure. After publishing finishes, you can choose to publish settings from local.settings.json to your function app in Azure. To learn more, see [Publish application settings](#publish-application-settings).

Values in **ConnectionStrings** are never published.

Your code can read the function application settings values as environment variables. For more information, see [Environment variables](functions-dotnet-class-library#environment-variables).

- Your code can read the function app settings values as environment variables. For more information, see
[Environment variables](functions-reference-java#environment-variables).

- Your code can read the function app settings values as environment variables. For more information, see
[Environment variables](functions-reference-node#environment-variables).

- Your code can read the function app settings values as environment variables. For more information, see
[Environment variables](functions-reference-powershell#environment-variables).

- Your code can read the function app settings values as environment variables. For more information, see
[Environment variables](functions-reference-python#environment-variables).

## Application settings in Azure

The settings in the local.settings.json file in your project should match the application settings in the function app in Azure. You must add any new settings to both local.settings.json and the function app in Azure. These settings aren't uploaded automatically when you publish the project. Likewise, you must download any settings that you create in your function app [in the portal](functions-how-to-use-azure-function-app-settings#settings) to your local project.

### Publish application settings

The easiest way to publish the required settings to your function app in Azure is to use the **Upload settings** link that appears after you publish your project:


You can also publish settings by using the **Azure Functions: Upload Local Setting** command in the command palette. You can add individual settings to application settings in Azure by using the **Azure Functions: Add New Setting** command.

Tip

Be sure to save your local.settings.json file before you publish it.

If the local file is encrypted, the process decrypts it, publishes it, and encrypts it again. If conflicting values exist in the two locations, you're prompted to choose how to proceed.

View existing app settings in the **Azure: Functions** area by expanding your subscription, your function app, and **Application Settings**.


### Download settings from Azure

If you create application settings in Azure, you can download them into your local.settings.json file by using the **Azure Functions: Download Remote Settings** command.

As with uploading, if the local file is encrypted, the process decrypts it, updates it, and encrypts it again. If conflicting values exist in the two locations, you're prompted to choose how to proceed.

## Install binding extensions

Except for HTTP and timer triggers, bindings are implemented in extension packages.

You must explicitly install the extension packages for the triggers and bindings that need them. The specific package you install depends on your project's process model.

Run the [dotnet add package](/en-us/dotnet/core/tools/dotnet-add-package) command in the Terminal window to install the extension packages that you need in your project. This template demonstrates how you add a binding for an [isolated-process class library](dotnet-isolated-process-guide):

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.<BINDING_TYPE_NAME> --version <TARGET_VERSION>
```


Replace `<BINDING_TYPE_NAME>`

with the name of the package that contains the binding you need. You can find the desired binding reference article in the [list of supported bindings](functions-triggers-bindings#supported-bindings).

Replace `<TARGET_VERSION>`

in the example with a specific version of the package, such as `3.0.0-beta5`

. Valid versions are listed on the individual package pages at [NuGet.org](https://nuget.org). The major versions that correspond to the current Functions runtime are specified in the reference article for the binding.

Tip

You can also use the **NuGet** commands in [the C# Dev Kit](https://code.visualstudio.com/docs/csharp/package-management#_add-a-package) to install binding extension packages.

C# script uses [extension bundles](extension-bundles).

The easiest way to install binding extensions is to enable [extension bundles](extension-bundles). When you enable bundles, a predefined set of extension packages is automatically installed.

To enable extension bundles, open the host.json file and update its contents to match the following code:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[3.*, 4.0.0)"
}
}
```


If for some reason you can't use an extension bundle to install binding extensions for your project, see [Explicitly install extensions](functions-bindings-register#explicitly-install-extensions).

## Monitoring functions

When you [run functions locally](#run-functions-locally), Core Tools streams log data to the Terminal console. You can also get log data when your Functions project runs in a function app in Azure. You can connect to streaming logs in Azure to see near-real-time log data. You should enable Application Insights for a more complete understanding of how your function app behaves.

### Streaming logs

When you're developing an application, it's often useful to see logging information in near-real time. You can view a stream of log files generated by your functions. Turn on logs from the command pallet with the `Azure Functions: Start streaming logs`

command. This output is an example of streaming logs for a request to an HTTP-triggered function:


To learn more, see [Streaming logs](functions-monitoring?tabs=vs-code#streaming-logs).

### Application Insights

You should monitor the execution of your functions by integrating your function app with Application Insights. When you create a function app in the Azure portal, this integration occurs by default. When you create your function app during Visual Studio publishing, you need to integrate Application Insights yourself. To learn how, see [Enable Application Insights integration](configure-monitoring#enable-application-insights-integration).

To learn more about monitoring using Application Insights, see [Monitor Azure Functions](functions-monitoring).

## C# script projects

By default, all C# projects are created as [C# compiled class library projects](functions-dotnet-class-library). If you prefer to work with C# script projects instead, you must select C# script as the default language in the Azure Functions extension settings:

Select

**File**>**Preferences**>**Settings**.Go to

**User Settings**>**Extensions**>**Azure Functions**.Select

**C#Script**from**Azure Function: Project Language**.

After you complete these steps, calls made to the underlying Core Tools include the `--csx`

option, which generates and publishes C# script (.csx) project files. When you specify this default language, all projects that you create default to C# script projects. You're not prompted to choose a project language when a default is set. To create projects in other languages, you must change this setting or remove it from the user settings.json file. After you remove this setting, you're again prompted to choose your language when you create a project.

## Command palette reference

The Azure Functions extension provides a useful graphical interface for interacting with your function apps in Azure. The same functionality is also available as commands in the command palette (F1). These Azure Functions commands are available:

| Azure Functions command | Description |
|---|---|
Add New Settings |
Creates a new application setting in Azure. To learn more, see
|

**Configure Deployment Source**[Continuous deployment for Azure Functions](functions-continuous-deployment).**Connect to GitHub Repository****Copy Function URL**[Get the URL of the deployed function](#get-the-url-of-the-deployed-function).**Create function app in Azure**[publish to a new function app in Azure](#publish-to-azure).**Decrypt Settings**[local settings](#local-settings)that the**Azure Functions: Encrypt Settings**command encrypted.**Delete Function App**[delete the resource group](functions-add-output-binding-storage-queue-vs-code#clean-up-resources). Your local project isn't affected.**Delete Function**[republishing your project](#republish-project-files).**Delete Proxy**[Work with Azure Functions Proxies](functions-proxies).**Delete Setting****Disconnect from Repo**[continuous deployment](functions-continuous-deployment)connection between a function app in Azure and a source control repository.**Download Remote Settings****Edit settings****Encrypt settings**`Values`

array in the [local settings](#local-settings). In this file,`IsEncrypted`

is also set to `true`

, which specifies that the local runtime decrypt settings before using them. Encrypt local settings to reduce the risk of leaking valuable information. In Azure, application settings are always stored encrypted.**Execute Function Now****Initialize Project for Use with VS Code****Install or Update Azure Functions Core Tools**[Azure Functions Core Tools](functions-run-local), which is used to run functions locally.**Redeploy**[republish your project](#republish-project-files).**Rename Settings**[download those changes to the local project](#download-settings-from-azure).**Restart****Set AzureWebJobsStorage**`AzureWebJobsStorage`

application setting. This setting is required by Azure Functions. It's set when a function app is created in Azure.**Start****Start Streaming Logs**[Streaming logs](#streaming-logs).**Stop****Stop Streaming Logs****Toggle as Slot Setting****Uninstall Azure Functions Core Tools****Upload Local Settings****View Commit in GitHub****View Deployment Logs**## Next steps

To learn more about Azure Functions Core Tools, see [Work with Azure Functions Core Tools](functions-run-local).

To learn more about developing functions as .NET class libraries, see [Azure Functions C# developer reference](functions-dotnet-class-library). This article also provides links to examples of how to use attributes to declare the various types of bindings supported by Azure Functions.


---

<!-- DOCUMENTO FUSIONADO: __functions-node-upgrade-v4_functions-twitter-email_monitor-functions-openteleme_84c39f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-node-upgrade-v4_functions-twitter-email.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-node-upgrade-v4.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-node-upgrade-v4 -->

# Migrate to version 4 of the Node.js programming model for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article discusses the differences between version 3 and version 4 of the Node.js programming model and how to upgrade an existing v3 app. If you want to create a new v4 app instead of upgrading an existing v3 app, see the tutorial for either [Visual Studio Code (VS Code)](how-to-create-function-azure-cli?pivots=programming-language-javascript) or [Azure Functions Core Tools](how-to-create-function-vs-code?pivot=programming-language-javascript). This article uses "tip" alerts to highlight the most important concrete actions that you should take to upgrade your app.
Version 4 is designed to provide Node.js developers with the following benefits:

- Provide a familiar and intuitive experience to Node.js developers.
- Make the file structure flexible with support for full customization.
- Switch to a code-centric approach for defining function configuration.

## Considerations

- The Node.js programming model shouldn't be confused with the Azure Functions runtime:
**Programming model**: Defines how you author your code and is specific to JavaScript and TypeScript.**Runtime**: Defines underlying behavior of Azure Functions and is shared across all languages.

- The version of the programming model is strictly tied to the version of the
npm package. It's versioned independently of the`@azure/functions`

[runtime](functions-versions). Both the runtime and the programming model use the number 4 as their latest major version, but that's a coincidence. - You can't mix the v3 and v4 programming models in the same function app. As soon as you register one v4 function in your app, any v3 functions registered in
*function.json*files are ignored.

## Requirements

Version 4 of the Node.js programming model requires the following minimum versions:

npm package v4.0.0`@azure/functions`

[Node.js](https://nodejs.org/en/about/previous-releases)v18+[Azure Functions Runtime](functions-versions)v4.25+[Azure Functions Core Tools](functions-run-local)v4.0.5382+ (if running locally)

npm package v4.0.0`@azure/functions`

[Node.js](https://nodejs.org/en/about/previous-releases)v18+[TypeScript](https://www.typescriptlang.org/)v4+[Azure Functions Runtime](functions-versions)v4.25+[Azure Functions Core Tools](functions-run-local)v4.0.5382+ (if running locally)

## Include the npm package

In v4, the [ @azure/functions](https://www.npmjs.com/package/@azure/functions) npm package contains the primary source code that backs the Node.js programming model. In previous versions, that code shipped directly in Azure and the npm package had only the TypeScript types. You now need to include this package for both TypeScript and JavaScript apps. You

*can*include the package for existing v3 apps, but it isn't required.

Tip

Make sure the `@azure/functions`

package is listed in the `dependencies`

section (not `devDependencies`

) of your *package.json* file. You can install v4 by using the following command:

```
npm install @azure/functions
```


## Set your app entry point

In v4 of the programming model, you can structure your code however you want. The only files that you need at the root of your app are *host.json* and *package.json*.

Otherwise, you define the file structure by setting the `main`

field in your *package.json* file. You can set the `main`

field to a single file or multiple files by using a [glob pattern](https://wikipedia.org/wiki/Glob_(programming)). The following table shows example values for the `main`

field:

| Example | Description |
|---|---|
`src/index.js` |
Register functions from a single root file. |
`src/functions/*.js` |
Register each function from its own file. |
`src/{index.js,functions/*.js}` |
A combination where you register each function from its own file, but you still have a root file for general app-level code. |

| Example | Description |
|---|---|
`dist/src/index.js` |
Register functions from a single root file. |
`dist/src/functions/*.js` |
Register each function from its own file. |
`dist/src/{index.js,functions/*.js}` |
A combination where you register each function from its own file, but you still have a root file for general app-level code. |

Tip

Make sure you define a `main`

field in your *package.json* file.

## Switch the order of arguments

The trigger input, instead of the invocation context, is now the first argument to your function handler. The invocation context, now the second argument, is simplified in v4 and isn't as required as the trigger input. You can leave it off if you aren't using it.

Tip

Switch the order of your arguments. For example, if you're using an HTTP trigger, switch `(context, request)`

to either `(request, context)`

or just `(request)`

if you aren't using the context.

## Define your function in code

You no longer have to create and maintain those separate *function.json* configuration files. You can now fully define your functions directly in your TypeScript or JavaScript files. In addition, many properties now have defaults so that you don't have to specify them every time.

```
const { app } = require('@azure/functions');
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: async (request, context) => {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text()) || 'world';
return { body: `Hello, ${name}!` };
},
});
```


```
import { app, HttpRequest, HttpResponseInit, InvocationContext } from '@azure/functions';
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text()) || 'world';
return { body: `Hello, ${name}!` };
}
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: httpTrigger1,
});
```


Tip

Move the configuration from your *function.json* file to your code. The type of the trigger corresponds to a method on the `app`

object in the new model. For example, if you use an `httpTrigger`

type in *function.json*, call `app.http()`

in your code to register the function. If you use `timerTrigger`

, call `app.timer()`

.

## Review your usage of context

In v4, the `context`

object is simplified to reduce duplication and to make writing unit tests easier. For example, we streamlined the primary input and output so that they're accessed only as the argument and return value of your function handler.

You can't access the primary input and output on the `context`

object anymore, but you must still access *secondary* inputs and outputs on the `context`

object. For more information about secondary inputs and outputs, see the [Node.js developer guide](functions-reference-node#extra-inputs-and-outputs).

### Get the primary input as an argument

The primary input is also called the *trigger* and is the only required input or output. You must have one (and only one) trigger.

Version 4 supports only one way of getting the trigger input, as the first argument:

```
async function httpTrigger1(request, context) {
const onlyOption = request;
```


```
async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
const onlyOption = request;
```


Tip

Make sure you aren't using `context.req`

or `context.bindings`

to get the input.

### Set the primary output as your return value

Version 4 supports only one way of setting the primary output, through the return value:

```
return {
body: `Hello, ${name}!`
};
```


```
async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
// ...
return {
body: `Hello, ${name}!`
};
}
```


Tip

Make sure you always return the output in your function handler, instead of setting it with the `context`

object.

### Context logging

In v4, logging methods were moved to the root `context`

object as shown in the following example. For more information about logging, see the [Node.js developer guide](functions-reference-node#logging).

```
context.log('This is an info log');
context.error('This is an error');
context.warn('This is an error');
```


### Create a test context

Version 3 doesn't support creating an invocation context outside the Azure Functions runtime, so authoring unit tests can be difficult. Version 4 allows you to create an instance of the invocation context, although the information during tests isn't detailed unless you add it yourself.

```
const testInvocationContext = new InvocationContext({
functionName: 'testFunctionName',
invocationId: 'testInvocationId'
});
```


## Review your usage of HTTP types

The HTTP request and response types are now a subset of the [fetch standard](https://developer.mozilla.org/docs/Web/API/fetch). They're no longer unique to Azure Functions.

The types use the [ undici](https://undici.nodejs.org/) package in Node.js. This package follows the fetch standard and is

[currently being integrated](https://github.com/nodejs/undici/issues/1737)into Node.js core.

### HttpRequest

*Body*. You can access the body by using a method specific to the type that you want to receive:`const body = await request.text(); const body = await request.json(); const body = await request.formData(); const body = await request.arrayBuffer(); const body = await request.blob();`

*Header*:`const header = request.headers.get('content-type');`

*Query parameter*:`const name = request.query.get('name');`


### HttpResponse

*Status*:`return { status: 200 };`

*Body*:Use the

`body`

property to return most types like a`string`

or`Buffer`

:`return { body: "Hello, world!" };`

Use the

`jsonBody`

property for the easiest way to return a JSON response:`return { jsonBody: { hello: "world" } };`

*Header*. You can set the header in two ways, depending on whether you're using the`HttpResponse`

class or the`HttpResponseInit`

interface:`const response = new HttpResponse(); response.headers.set('content-type', 'application/json'); return response;`

`return { headers: { 'content-type': 'application/json' } };`


Tip

Update any logic by using the HTTP request or response types to match the new methods.

Tip

Update any logic by using the HTTP request or response types to match the new methods. You should get TypeScript build errors to help you identify if you're using old methods.

## Troubleshoot

See the [Node.js Troubleshoot guide](functions-node-troubleshoot).


---

<!-- DOCUMENTO FUSIONADO: functions-twitter-email.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-twitter-email -->

# Tutorial: Create a function to integrate with Azure Logic Apps

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions integrates with Azure Logic Apps in the Logic Apps Designer. This integration allows you use the computing power of Functions in orchestrations with other Azure and third-party services.

This tutorial shows you how to create a workflow to analyze X activity. As tweets are evaluated, the workflow sends notifications when positive sentiments are detected.

In this tutorial, you learn to:

- Create an Azure AI services API Resource.
- Create a function that categorizes tweet sentiment.
- Create a logic app that connects to X.
- Add sentiment detection to the logic app.
- Connect the logic app to the function.
- Send an email based on the response from the function.

## Prerequisites

- An active
[X](https://x.com/)account. - An
[Outlook.com](https://outlook.com/)account (for sending notifications).

Note

If you want to use the Gmail connector, only G-Suite business accounts can use this connector without restrictions in logic apps. If you have a Gmail consumer account, you can use the Gmail connector with only specific Google-approved apps and services, or you can [create a Google client app to use for authentication in your Gmail connector](/en-us/connectors/gmail/#authentication-and-bring-your-own-application).

For more information, see [Data security and privacy policies for Google connectors in Azure Logic Apps](../connectors/connectors-google-data-security-privacy-policy).

## Create Text Analytics resource

The Azure AI services APIs are available in Azure as individual resources. Use the Text Analytics API to detect the sentiment of posted tweets.

Sign in to the

[Azure portal](https://portal.azure.com/).Select

**Create a resource**in the upper left-hand corner of the Azure portal.Under

*Categories*, select**AI + Machine Learning**Under

*Text Analytics*, select**Create**.Enter the following values in the

*Create Text Analytics*screen.Setting Value Remarks Subscription Your Azure subscription name Resource group Create a new resource group named **tweet-sentiment-tutorial**Later, you delete this resource group to remove all the resources created during this tutorial. Region Select the region closest to you Name **TweetSentimentApp**Pricing tier Select **Free F0**Select

**Review + create**.Select

**Create**.Once the deployment is complete, select

**Go to Resource**.

## Get Text Analytics settings

With the Text Analytics resource created, you'll copy a few settings and set them aside for later use.

Select

**Keys and Endpoint**.Copy

**Key 1**by clicking on the icon at the end of the input box.Paste the value into a text editor.

Copy the

**Endpoint**by clicking on the icon at the end of the input box.Paste the value into a text editor.


## Create the function app

From the top search box, search for and select

**Function app**.Select

**Create**.Enter the following values.

Setting Suggested Value Remarks Subscription Your Azure subscription name Resource group **tweet-sentiment-tutorial**Use the same resource group name throughout this tutorial. Function App name **TweetSentimentAPI**+ a unique suffixFunction application names are globally unique. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

.Publish **Code**Runtime stack **.NET**The function code provided for you is in C#. Version Select the latest version number Region Select the region closest to you Select

**Review + create**.Select

**Create**.Once the deployment is complete, select

**Go to Resource**.

## Create an HTTP-triggered function

From the left menu of the

*Functions*window, select**Functions**.Select

**Add**from the top menu and enter the following values.Setting Value Remarks Development environment **Develop in portal**Template **HTTP Trigger**New Function **TweetSentimentFunction**This is the name of your function. Authorization level **Function**Select the

**Add**button.Select the

**Code + Test**button.Paste the following code in the code editor window.

`#r "Newtonsoft.Json" using System; using System.Net; using Microsoft.AspNetCore.Mvc; using Microsoft.Extensions.Logging; using Microsoft.Extensions.Primitives; using Newtonsoft.Json; public static async Task<IActionResult> Run(HttpRequest req, ILogger log) { string requestBody = String.Empty; using (StreamReader streamReader = new StreamReader(req.Body)) { requestBody = await streamReader.ReadToEndAsync(); } dynamic score = JsonConvert.DeserializeObject(requestBody); string value = "Positive"; if(score < .3) { value = "Negative"; } else if (score < .6) { value = "Neutral"; } return requestBody != null ? (ActionResult)new OkObjectResult(value) : new BadRequestObjectResult("Pass a sentiment score in the request body."); }`

A sentiment score is passed into the function, which returns a category name for the value.

Select the

**Save**button on the toolbar to save your changes.Note

To test the function, select

**Test/Run**from the top menu. On the*Input*tab, enter a value of`0.9`

in the*Body*input box, and then select**Run**. Verify that a value of*Positive*is returned in the*HTTP response content*box in the*Output*section.

Next, create a logic app that integrates with Azure Functions, X, and the Azure AI services API.

## Create a logic app

From the top search box, search for and select

**Logic Apps**.Select

**Add**.Select

**Consumption**and enter the following values.Setting Suggested Value Subscription Your Azure subscription name Resource group **tweet-sentiment-tutorial**Logic app name **TweetSentimentApp**Region Select the region closest to you, preferably the same region you selected in previous steps. Accept default values for all other settings.

Select

**Review + create**.Select

**Create**.Once the deployment is complete, select

**Go to Resource**.Select the

**Blank Logic App**button.Select the

**Save**button on the toolbar to save your progress.

You can now use the Logic Apps Designer to add services and triggers to your application.

## Connect to X

Create a connection to X so your app can poll for new tweets.

Search for

**X**in the top search box.Select the

**X**icon.Select the

**When a new tweet is posted**trigger.Enter the following values to set up the connection.

Setting Value Connection name **MyXConnection**Authentication Type **Use default shared application**Select

**Sign in**.Follow the prompts in the pop-up window to complete signing in to X.

Next, enter the following values in the

*When a new tweet is posted*box.Setting Value Search text **#my-x-tutorial**How often do you want to check for items? **1**in the textbox, and

**Hour**in the dropdown. You may enter different values but be sure to review the current[limitations](/en-us/connectors/twitterconnector/#limits)of the X connector.Select the

**Save**button on the toolbar to save your progress.

Next, connect to text analytics to detect the sentiment of collected tweets.

## Add Text Analytics sentiment detection

Select

**New step**.Search for

**Text Analytics**in the search box.Select the

**Text Analytics**icon.Select

**Detect Sentiment**and enter the following values.Setting Value Connection name **TextAnalyticsConnection**Account Key Paste in the Text Analytics account key you set aside earlier. Site URL Paste in the Text Analytics endpoint you set aside earlier. Select

**Create**.Click inside the

*Add new parameter*box, and check the box next to**documents**that appears in the pop-up.Click inside the

*documents Id - 1*textbox to open the dynamic content pop-up.In the

*dynamic content*search box, search for**id**, and click on**Tweet id**.Click inside the

*documents Text - 1*textbox to open the dynamic content pop-up.In the

*dynamic content*search box, search for**text**, and click on**Tweet text**.In

**Choose an action**, type**Text Analytics**, and then click the**Detect sentiment**action.Select the

**Save**button on the toolbar to save your progress.

The *Detect Sentiment* box should look like the following screenshot.


## Connect sentiment output to function endpoint

Select

**New step**.Search for

**Azure Functions**in the search box.Select the

**Azure Functions**icon.Search for your function name in the search box. If you followed the guidance above, your function name begins with

**TweetSentimentAPI**.Select the function icon.

Select the

**TweetSentimentFunction**item.Click inside the

*Request Body*box, and select the*Detect Sentiment***score**item from the pop-up window.Select the

**Save**button on the toolbar to save your progress.

## Add conditional step

Select the

**Add an action**button.Click inside the

*Control*box, and search for and select**Control**in the pop-up window.Select

**Condition**.Click inside the

*Choose a value*box, and select the*TweetSentimentFunction***Body**item from the pop-up window.Enter

**Positive**in the*Choose a value*box.Select the

**Save**button on the toolbar to save your progress.

## Add email notifications

Under the

*True*box, select the**Add an action**button.Search for and select

**Office 365 Outlook**in the text box.Search for

**send**and select**Send an email**in the text box.Select the

**Sign in**button.Follow the prompts in the pop-up window to complete signing in to Office 365 Outlook.

Enter your email address in the

*To*box.Click inside the

*Subject*box and click on the**Body**item under*TweetSentimentFunction*. If the*Body*item isn't shown in the list, click the**See more**link to expand the options list.After the

*Body*item in the*Subject*, enter the text**Tweet from:**.After the

*Tweet from:*text, click on the box again and select**User name**from the*When a new tweet is posted*options list.Click inside the

*Body*box and select**Tweet text**under the*When a new tweet is posted*options list. If the*Tweet text*item isn't shown in the list, click the**See more**link to expand the options list.Select the

**Save**button on the toolbar to save your progress.

The email box should now look like this screenshot.


## Run the workflow

From your X account, tweet the following text:

**I'm enjoying #my-x-tutorial**.Return to the Logic Apps Designer and select the

**Run**button.Check your email for a message from the workflow.


## Clean up resources

To clean up all the Azure services and accounts created during this tutorial, delete the resource group.

Search for

**Resource groups**in the top search box.Select the

**tweet-sentiment-tutorial**.Select

**Delete resource group**Enter

**tweet-sentiment-tutorial**in the text box.Select the

**Delete**button.

Optionally, you may want to return to your X account and delete any test tweets from your feed.


---

<!-- DOCUMENTO FUSIONADO: monitor-functions-opentelemetry-distributed-tracing.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/monitor-functions-opentelemetry-distributed-tracing -->

# Tutorial: Monitor Azure Functions with OpenTelemetry distributed tracing

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article demonstrates OpenTelemetry support in Azure Function, which enables distributed tracing across multiple function calls by using integrated Application Insights and OpenTelemetry support. To help you get started, an Azure Developer CLI (`azd`

) template is used to create your code project as well as the Azure deployment in which to run your app.

In this tutorial, you use the `azd`

tool to:

- Initialize an OpenTelemetry-enabled project from a template.
- Review the code that enables OpenTelemetry integration.
- Run and verify your OpenTelemetry-enabled app locally.
- Create a function app and related resources in Azure.
- Deploy your code project to the function app in Azure.
- Verify distributed tracing in Application Insights.

The required Azure resources created by this template follow current best practices for secure and scalable function app deployments in Azure. The same `azd`

command also deploys your code project to your new function app in Azure.

By default, the Flex Consumption plan follows a *pay-for-what-you-use* billing model, which means completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

Important

This article currently supports only C#, Python, and TypeScript. To complete the quickstart, select one of these supported languages at the top of the article.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Initialize the project

Use the `azd init`

command to create a local Azure Functions code project from a template that includes OpenTelemetry distributed tracing.

In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-python-azd-otel -e flexquickstart-otel`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-python-azd-otel)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name also appears in the name of the resource group you create in Azure.

In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-typescript-azd-otel -e flexquickstart-otel`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-otel)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name also appears in the name of the resource group you create in Azure.

In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-dotnet-azd-otel -e flexquickstart-otel`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-otel)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name also appears in the name of the resource group you create in Azure.

## Review the code

The template creates a complete distributed tracing scenario with three functions that work together. Let's review the key OpenTelemetry-related aspects:

### OpenTelemetry configuration

The `src/otel-sample/host.json`

file enables OpenTelemetry for the Functions host:

```
{
"version": "2.0",
"telemetryMode": "OpenTelemetry",
"extensions": {
"serviceBus": {
"maxConcurrentCalls": 10
}
},
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
}
}
```


The key setting `"telemetryMode": "OpenTelemetry"`

enables distributed tracing across function calls.

The `src/OTelSample/host.json`

file enables OpenTelemetry for the Functions host:

```
{
"version": "2.0",
"telemetryMode": "OpenTelemetry",
"logging": {
"OpenTelemetry": {
"logLevel": {
"Host.General": "Warning"
}
}
}
}
```


The key setting `"telemetryMode": "OpenTelemetry"`

enables distributed tracing across function calls.

### Dependencies for OpenTelemetry

The `src/otel-sample/requirements.txt`

file includes the necessary packages for OpenTelemetry integration:

```
azure-functions
azure-monitor-opentelemetry
requests
```


The `azure-monitor-opentelemetry`

package provides the OpenTelemetry integration with Application Insights.

The `src/otel-sample/package.json`

file includes the necessary packages for OpenTelemetry integration:

```
{
"dependencies": {
"@azure/functions": "^4.0.0",
"@azure/functions-opentelemetry-instrumentation": "^0.1.0",
"@azure/monitor-opentelemetry-exporter": "^1.0.0",
"axios": "^1.6.0"
}
}
```


The `@azure/functions-opentelemetry-instrumentation`

and `@azure/monitor-opentelemetry-exporter`

packages provide the OpenTelemetry integration with Application Insights.

The `.csproj`

file includes the necessary packages for OpenTelemetry integration:

```
<PackageReference Include="Azure.Monitor.OpenTelemetry.Exporter" Version="1.4.0" />
<PackageReference Include="Microsoft.Azure.Functions.Worker.OpenTelemetry" Version="1.4.0" />
<PackageReference Include="OpenTelemetry.Instrumentation.Http" Version="1.10.0" />
```


These packages provide the OpenTelemetry integration with Application Insights and HTTP instrumentation for distributed tracing.

### Function implementation

The functions in `src/otel-sample/function_app.py`

demonstrate a distributed tracing flow:

#### First HTTP Function

```
@app.function_name("first_http_function")
@app.route(route="first_http_function", auth_level=func.AuthLevel.ANONYMOUS)
def first_http_function(req: func.HttpRequest) -> func.HttpResponse:
logging.info('Python HTTP trigger function (first) processed a request.')
# Call the second function
base_url = f"{req.url.split('/api/')[0]}/api"
second_function_url = f"{base_url}/second_http_function"
response = requests.get(second_function_url)
second_function_result = response.text
result = {
"message": "Hello from the first function!",
"second_function_response": second_function_result
}
return func.HttpResponse(
json.dumps(result),
status_code=200,
mimetype="application/json"
)
```


#### Second HTTP Function

```
@app.function_name("second_http_function")
@app.route(route="second_http_function", auth_level=func.AuthLevel.ANONYMOUS)
@app.service_bus_queue_output(arg_name="outputsbmsg", queue_name="%ServiceBusQueueName%",
connection="ServiceBusConnection")
def second_http_function(req: func.HttpRequest, outputsbmsg: func.Out[str]) -> func.HttpResponse:
logging.info('Python HTTP trigger function (second) processed a request.')
message = "This is the second function responding."
# Send a message to the Service Bus queue
queue_message = "Message from second HTTP function to trigger ServiceBus queue processing"
outputsbmsg.set(queue_message)
logging.info('Sent message to ServiceBus queue: %s', queue_message)
return func.HttpResponse(
message,
status_code=200
)
```


#### Service Bus Queue Trigger

```
@app.service_bus_queue_trigger(arg_name="azservicebus", queue_name="%ServiceBusQueueName%",
connection="ServiceBusConnection")
def servicebus_queue_trigger(azservicebus: func.ServiceBusMessage):
logging.info('Python ServiceBus Queue trigger start processing a message: %s',
azservicebus.get_body().decode('utf-8'))
time.sleep(5) # Simulate processing work
logging.info('Python ServiceBus Queue trigger end processing a message')
```


The OpenTelemetry configuration is set up in `src/otel-sample/index.ts`

:

```
import { AzureFunctionsInstrumentation } from '@azure/functions-opentelemetry-instrumentation';
import { AzureMonitorTraceExporter, AzureMonitorLogExporter } from '@azure/monitor-opentelemetry-exporter';
import { getNodeAutoInstrumentations, getResourceDetectors } from '@opentelemetry/auto-instrumentations-node';
import { registerInstrumentations } from '@opentelemetry/instrumentation';
import { detectResources } from '@opentelemetry/resources';
import { LoggerProvider, SimpleLogRecordProcessor } from '@opentelemetry/sdk-logs';
import { NodeTracerProvider, SimpleSpanProcessor } from '@opentelemetry/sdk-trace-node';
const resource = detectResources({ detectors: getResourceDetectors() });
const tracerProvider = new NodeTracerProvider({
resource,
spanProcessors: [new SimpleSpanProcessor(new AzureMonitorTraceExporter())]
});
tracerProvider.register();
const loggerProvider = new LoggerProvider({
resource,
processors: [new SimpleLogRecordProcessor(new AzureMonitorLogExporter())],
});
registerInstrumentations({
tracerProvider,
loggerProvider,
instrumentations: [getNodeAutoInstrumentations(), new AzureFunctionsInstrumentation()],
});
```


The functions are defined in the `src/otel-sample/src/functions`

folder:

#### First HTTP Function

```
export async function firstHttpFunction(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log("TypeScript HTTP trigger function (first) processed a request.");
try {
// Call the second function
const baseUrl = request.url.split("/api/")[0];
const secondFunctionUrl = `${baseUrl}/api/second_http_function`;
const response = await axios.get(secondFunctionUrl);
const secondFunctionResult = response.data;
const result = {
message: "Hello from the first function!",
second_function_response: secondFunctionResult,
};
return {
status: 200,
body: JSON.stringify(result),
headers: { "Content-Type": "application/json" },
};
} catch (error) {
return {
status: 500,
body: JSON.stringify({ error: "Failed to process request" }),
};
}
}
```


#### Second HTTP Function

```
export async function secondHttpFunction(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log("TypeScript HTTP trigger function (second) processed a request.");
const message = "This is the second function responding.";
// Send a message to the Service Bus queue
const queueMessage =
"Message from second HTTP function to trigger ServiceBus queue processing";
context.extraOutputs.set(serviceBusOutput, queueMessage);
context.log("Sent message to ServiceBus queue:", queueMessage);
return {
status: 200,
body: message,
};
}
```


#### Service Bus Queue Trigger

```
export async function serviceBusQueueTrigger(
message: unknown,
context: InvocationContext
): Promise<void> {
context.log("TypeScript ServiceBus Queue trigger start processing a message:", message);
// Simulate processing time
await new Promise((resolve) => setTimeout(resolve, 5000));
context.log("TypeScript ServiceBus Queue trigger end processing a message");
}
```


The OpenTelemetry configuration is set up in `src/OTelSample/Program.cs`

:

```
using Azure.Monitor.OpenTelemetry.Exporter;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.OpenTelemetry;
using OpenTelemetry.Trace;
var builder = FunctionsApplication.CreateBuilder(args);
builder.ConfigureFunctionsWebApplication();
builder.Logging.AddOpenTelemetry(logging =>
{
logging.IncludeFormattedMessage = true;
logging.IncludeScopes = true;
});
builder.Services.AddOpenTelemetry()
.WithTracing(tracing =>
{
tracing.AddHttpClientInstrumentation();
});
builder.Services.AddOpenTelemetry().UseAzureMonitorExporter();
builder.Services.AddOpenTelemetry().UseFunctionsWorkerDefaults();
builder.Services.AddHttpClient();
builder.Build().Run();
```


The functions are defined in separate class files:

#### First HTTP Function

```
public class FirstHttpTrigger
{
private readonly ILogger<FirstHttpTrigger> _logger;
private readonly IHttpClientFactory _httpClientFactory;
public FirstHttpTrigger(ILogger<FirstHttpTrigger> logger, IHttpClientFactory httpClientFactory)
{
_logger = logger;
_httpClientFactory = httpClientFactory;
}
[Function("first_http_function")]
public async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", "post")] HttpRequestData req)
{
_logger.LogInformation("first_http_function function processed a request.");
var baseUrl = $"{req.Url.AbsoluteUri.Split("/api/")[0]}/api";
var targetUri = $"{baseUrl}/second_http_function";
var client = _httpClientFactory.CreateClient();
var response = await client.GetAsync(targetUri);
var content = await response.Content.ReadAsStringAsync();
return new OkObjectResult($"Called second_http_function, status: {response.StatusCode}, content: {content}");
}
}
```


#### Second HTTP Function

```
public class SecondHttpTrigger
{
private readonly ILogger<SecondHttpTrigger> _logger;
public SecondHttpTrigger(ILogger<SecondHttpTrigger> logger)
{
_logger = logger;
}
[Function("second_http_function")]
public MultiResponse Run([HttpTrigger(AuthorizationLevel.Anonymous, "get", "post")] HttpRequestData req)
{
_logger.LogInformation("second_http_function function processed a request.");
return new MultiResponse
{
Messages = new string[] { "Hello" },
HttpResponse = req.CreateResponse(System.Net.HttpStatusCode.OK)
};
}
}
public class MultiResponse
{
[ServiceBusOutput("%ServiceBusQueueName%", Connection = "ServiceBusConnection")]
public string[]? Messages { get; set; }
[HttpResult]
public HttpResponseData? HttpResponse { get; set; }
}
```


#### Service Bus Queue Trigger

```
public class ServiceBusQueueTrigger
{
private readonly ILogger<ServiceBusQueueTrigger> _logger;
public ServiceBusQueueTrigger(ILogger<ServiceBusQueueTrigger> logger)
{
_logger = logger;
}
[Function("servicebus_queue_trigger")]
public async Task Run(
[ServiceBusTrigger("%ServiceBusQueueName%", Connection = "ServiceBusConnection")]
ServiceBusReceivedMessage message,
ServiceBusMessageActions messageActions)
{
_logger.LogInformation("Message ID: {id}", message.MessageId);
_logger.LogInformation("Message Body: {body}", message.Body);
// Complete the message
await messageActions.CompleteMessageAsync(message);
}
}
```


### Distributed tracing flow

This architecture creates a complete distributed tracing scenario, with this behavior:

**First HTTP function**receives an HTTP request and calls the second HTTP function**Second HTTP function**responds and sends a message to Service Bus**Service Bus trigger**processes the message with a delay to simulate processing work

Key aspects of the OpenTelemetry implementation:

**OpenTelemetry integration**: The`host.json`

file enables OpenTelemetry with`"telemetryMode": "OpenTelemetry"`

**Function chaining**: The first function calls the second using HTTP requests, creating correlated traces**Service Bus integration**: The second function outputs to Service Bus, which triggers the third function**Anonymous authentication**: The HTTP functions use`auth_level=func.AuthLevel.ANONYMOUS`

, so no function keys are required

You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-python-azd-otel).

**OpenTelemetry integration**: The`index.ts`

file configures OpenTelemetry with Azure Monitor exporters for traces and logs**Function chaining**: The first function calls the second using axios with automatic trace propagation**Service Bus integration**: The second function outputs to Service Bus using output bindings, which triggers the third function**Managed identity**: All Service Bus connections use managed identity instead of connection strings**Processing simulation**: The 5-second delay in the Service Bus trigger simulates message processing work

You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-otel).

**OpenTelemetry integration**: The`Program.cs`

file configures OpenTelemetry with Azure Monitor exporter**Function chaining**: The first function calls the second using HttpClient with OpenTelemetry instrumentation**Service Bus integration**: The second function outputs to Service Bus using output bindings, which triggers the third function**Managed identity**: All Service Bus connections use managed identity instead of connection strings**.NET 8 Isolated Worker**: Uses the latest Azure Functions .NET Isolated Worker model for better performance and flexibility

You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-otel).

After you verify your functions locally, it's time to publish them to Azure.

## Deploy to Azure

This project is configured to use the `azd up`

command to deploy this project to a new function app in a Flex Consumption plan in Azure with OpenTelemetry support.

Tip

This project includes a set of Bicep files that `azd`

uses to create a secure deployment to a Flex consumption plan that follows best practices, including managed identity connections.

Run this command to have

`azd`

create the required Azure resources in Azure and deploy your code project to the new function app:`azd up`

The root folder contains the

`azure.yaml`

definition file required by`azd`

.If you're not already signed in, you're asked to authenticate with your Azure account.

When prompted, provide these required deployment parameters:

Parameter Description *Azure subscription*Subscription in which your resources are created. *Azure location*Azure region in which to create the resource group that contains the new Azure resources. Only regions that currently support the Flex Consumption plan are shown. The

`azd up`

command uses your response to these prompts with the Bicep configuration files to complete these deployment tasks:Create and configure these required Azure resources (equivalent to

`azd provision`

):- Azure Functions Flex Consumption plan and function app with OpenTelemetry enabled
- Azure Storage (required) and Application Insights (recommended)
- Service Bus namespace and queue for distributed tracing demonstration
- Access policies and roles for your account
- Service-to-service connections using managed identities (instead of stored connection strings)

Package and deploy your code to the deployment container (equivalent to

`azd deploy`

). The app is then started and runs in the deployed package.

After the command completes successfully, you see links to the resources you created.


## Test distributed tracing

Now you can test the OpenTelemetry distributed tracing functionality by calling your deployed functions and observing the telemetry in Application Insights.

### Invoke the function on Azure

You can invoke your function endpoints in Azure by making HTTP requests to their URLs. Since the HTTP functions in this template are configured with anonymous access, no function keys are required.

In your local terminal or command prompt, run this command to get the function app name and construct the URL:

`APP_NAME=$(azd env get-value AZURE_FUNCTION_NAME) echo "Function URL: https://$APP_NAME.azurewebsites.net/api/first_http_function"`

The

`azd env get-value`

command gets your function app name from the local environment.Test the function in your browser by navigating to the URL:

`https://your-function-app.azurewebsites.net/api/first_http_function`

Replace

`your-function-app`

with your actual function app name from the previous step. This single request creates a distributed trace that flows through all three functions.

### View distributed tracing in Application Insights

After invoking the function, you can observe the complete distributed trace in Application Insights:

Note

It might take a few minutes for telemetry data to appear in Application Insights after invoking your function. If you don't see data immediately, wait a few minutes and refresh the view.

Go to your Application Insights resource in the Azure portal (you can find it in the same resource group as your function app).

Open the

**Application map**to see the distributed trace across all three functions. You should see the flow from the HTTP request through your functions and to Service Bus.Check the

**Transaction search**to find your request and see the complete trace timeline. Search for transactions from your function app.Select a specific transaction to see the end-to-end trace that shows:

- The HTTP request to
`first_http_function`

- The internal HTTP call to
`second_http_function`

- The Service Bus message being sent
- The
`servicebus_queue_trigger`

processing the message from Service Bus

- The HTTP request to
In the trace details, you can see:

**Timing information**: How long each step took**Dependencies**: The connections between functions**Logs**: Application logs correlated with the trace**Performance metrics**: Response times and throughput


This example demonstrates end-to-end distributed tracing across multiple Azure Functions with OpenTelemetry integration, providing complete visibility into your application's behavior and performance.

## Redeploy your code

Run the `azd up`

command as many times as you need to both provision your Azure resources and deploy code updates to your function app.

Note

The latest deployment package always overwrites deployed code files.

Your initial responses to `azd`

prompts and any environment variables generated by `azd`

are stored locally in your named environment. Use the `azd env get-values`

command to review all of the variables in your environment that the command uses when creating Azure resources.

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-mcp-tutorial -->

# Tutorial: Host an MCP server on Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to host remote [Model Context Protocol](https://modelcontextprotocol.io/docs/getting-started/intro) (MCP) servers on Azure Functions. You also learn how to use built-in authentication to configure server endpoint authorization and better secure your AI tools.

There are two ways to host a remote MCP server in Azure Functions:

| MCP server option | Description | Best for... |
|---|---|---|
MCP extension server |

[Azure Functions MCP extension](functions-bindings-mcp)to create custom MCP servers, where the extension trigger lets you define your tool endpoints. These servers are supported in all Functions languages and are developed, deployed, and managed as any other function app.[bindings-based programming model](functions-triggers-bindings).**Self-hosted server**Note

The ability to have Azure Functions host MCP servers you create using official MCP SDKs is currently in preview.

This tutorial covers both MCP server options supported by Functions. Select the tab that best fits your scenario.

In this tutorial, you use Visual Studio Code to:

- Create an MCP server project using the MCP extension.
- Run and verify your MCP server locally.
- Create a function app in Azure.
- Deploy your MCP server project.
- Enable built-in authentication.

Important

This article currently supports only C#, Python, and TypeScript. To complete the quickstart, select one of these supported languages at the top of the article.

This article supports version 4 of the Node.js programming model for Azure Functions.

This article supports version 2 of the Python programming model for Azure Functions.

## Prerequisites

[Visual Studio Code](https://code.visualstudio.com/)with these extensions:[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions). This extension requires[Azure Functions Core Tools](functions-run-local)and tries to install it when it's not available.

[Azure CLI](/en-us/cli/azure/install-azure-cli). You can also run Azure CLI commands in[Azure Cloud Shell](../cloud-shell/overview).An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Create your MCP server project

Use Visual Studio Code to locally create an MCP server project in your preferred language.

In Visual Studio Code, press

`F1`to open the command palette. Search for and run the command`Azure Functions: Create New Project...`

.Choose the directory location for your project workspace and choose

**Select**. You should either create a new folder or choose an empty folder for the project workspace. Don't choose a project folder that is already part of a workspace.

Provide the following information at the prompts:

Prompt Selection **Select a project type**Choose `C#`

.**Select a .NET runtime**Choose `.NET 8.0 LTS`

.**Select a template for your project's first function**Choose `MCP Tool trigger`

.**Provide a function name**Type `McpTrigger`

.**Provide a namespace**Type `My.Functions`

.**Authorization level**Choose `FUNCTION`

, which requires access key when connecting to the remote MCP server.**Select how you would like to open your project**Choose `Open in current window`

.

Provide the following information at the prompts:

Prompt Selection **Select a project type**Choose `TypeScript`

.**Select a template for your project's first function**Choose `MCP Tool trigger`

.**Provide a function name**Type `mcpToolTrigger`

.**Authorization level**Choose `FUNCTION`

, which requires access key when connecting to the remote MCP server.**Select how you would like to open your project**Choose `Open in current window`

.

Provide the following information at the prompts:

Prompt Selection **Select a project type**Choose `Python`

.**Select a Python interpreter to create a virtual environment**Choose your preferred Python interpreter. If an option isn't shown, type in the full path to your Python binary. **Select a template for your project's first function**Choose `MCP Tool trigger`

.**Name of the function you want to create**Enter `mcp_trigger`

.**Authorization level**Choose `FUNCTION`

, which requires access key when connecting to the remote MCP server.**Select how you would like to open your project**Choose `Open in current window`

.

Using this information, Visual Studio Code generates a code project for an MCP server trigger. You can view the local project files in the Explorer.

## Start the MCP server locally

Function apps need a storage component to run. Before starting the server, start the local storage emulator:

In

*local.setting.json*, ensure you have`"AzureWebJobsStorage": "UseDevelopmentStorage=true"`

.In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azurite: Start`

.Check the bottom bar and verify that Azurite emulation services are running. If so, you can now run the server locally.

To start running locally, press

`F5`.

Function apps need a storage component to run. Before starting the server, start the local storage emulator:

In

*local.setting.json*, ensure you have`"AzureWebJobsStorage": "UseDevelopmentStorage=true"`

.In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azurite: Start`

.Check the bottom bar and verify that Azurite emulation services are running. If so, you can now run the server locally.

To start running locally, press

`F5`.

Function apps need a storage component to run. Before starting the server, start the local storage emulator:

In

*local.setting.json*, ensure you have`"AzureWebJobsStorage": "UseDevelopmentStorage=true"`

.In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azurite: Start`

.Check the bottom bar and verify that Azurite emulation services are running. If so, you can now run the server locally.

To start running locally, press

`F5`.

## Test the server

Find the

`.vscode`

directory and open`mcp.json`

. The editor should add the server's connection info.Start the server by selecting the

**Start**button above server name.When you connect to the server, you see the number of tools available above the server name.

Open Visual Studio Code Copilot chat in agent mode, then ask a question. For example, "Greet with #your-local-server-name". This question ensures Copilot uses the server to help answer the question.

When Copilot requests to run a tool from the local MCP server, select

**Allow**.Disconnect from the server when you finish testing by selecting

**Stop**, and`Cntrl+C`

to stop running it locally.

Tip

In the Copilot chat window, select the tool icon in the bottom to see the list of servers and tools available for the chat. Ensure the local MCP server is checked when testing.

## Remote MCP server authorization

There are two ways to reduce or prevent unauthorized use of your remote MCP server endpoints:

| Method | Description |
|---|---|
| Built-in server authentication (preview) | Functions includes built-in
|

`Anonymous`

access level to disable access keys in your server when using OAuth-based authentication.Note

This tutorial contains detailed configuration instructions for the built-in server authorization and authentication feature, which might also be referred to as *App Service Authentication* in other articles. You can find an overview of the feature and some usage guidance in the [Configure built-in server authorization (preview)](../app-service/configure-authentication-mcp) article.

## Disable key-based authentication

The built-in server authorization feature is a component separate from Azure Functions. When using server authentication, it's best to first disable key-based authentication by allowing anonymous access.

To disable host-based authentication in your MCP server, set `system.webhookAuthorizationLevel`

to `Anonymous`

in the `host.json`

file:

```
{
"version": "2.0",
"extensions": {
"mcp": {
...
"system": {
"webhookAuthorizationLevel": "Anonymous"
}
}
}
}
```


## Create the function app in Azure

Create a function app in the Flex Consumption plan in Azure that hosts your MCP server.

In the

[Azure portal](https://portal.azure.com), from the menu or the**Home**page, select**Create a resource**.Select

**Get started**and then**Create**under**Function App**.Under

**Select a hosting option**, choose**Flex Consumption**>**Select**.On the

**Basics**page, use the function app settings as specified in the following table:Setting Suggested value Description **Subscription**Your subscription The subscription in which you create your new function app. [Resource Group](../azure-resource-manager/management/overview)*myResourceGroup*Name for the new resource group in which you create your function app. **Function App name**Globally unique name Name that identifies your new function app. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

.**Region**Preferred region Select a [region](https://azure.microsoft.com/regions/)that's near you or near other services that your functions can access. Unsupported regions aren't displayed. For more information, see[View currently supported regions](flex-consumption-how-to#view-currently-supported-regions).**Runtime stack**Preferred language Choose one of the supported language runtime stacks. In-portal editing using Visual Studio Code for the Web is currently only available for Node.js, PowerShell, and Python apps. C# class library and Java functions must be [developed locally](functions-develop-local#local-development-environments).**Version**Language version Choose a supported version of your language runtime stack. **Instance size**Default Determines the amount of instance memory allocated for each instance of your app. For more information, see [Instance sizes](flex-consumption-plan#instance-sizes).On the

**Storage**page, accept the default behavior of creating a new[default host storage account](storage-considerations)or choose to use an existing storage account.

On the

**Monitoring**page, make sure that**Enable Application Insights**is selected. Accept the default to create a new Application Insights instance, or else choose to use an existing instance. When you create an Application Insights instance, you're also asked to select a Log Analytics**Workspace**.On the

**Authentication**page, change the**Authentication type**to**Managed identity**for all resources. With this option, a user-assigned managed identity is also created that your app uses to access these Azure resources using Microsoft Entra ID authentication. Managed identities with Microsoft Entra ID provides the highest level of security for connecting to Azure resources.Accept the default options in the remaining tabs and then select

**Review + create**to review the app configuration you chose.When you're satisfied, select

**Create**to provision and deploy the function app and related resources.Select the

**Notifications**icon in the upper-right corner of the portal and watch for the**Deployment succeeded**message.Select

**Go to resource**to view your new function app. You can also select**Pin to dashboard**. Pinning makes it easier to return to this function app resource from your dashboard.

## Deploy the MCP server project

Important

Deploying to an existing function app always overwrites the contents of that app in Azure.

In the command palette, enter and then select

**Azure Functions: Deploy to Function App**.Select the function app you just created. When prompted about overwriting previous deployments, select

**Deploy**to deploy your function code to the new function app resource.When deployment is completed, select

**View Output**to view the creation and deployment results, including the Azure resources that you created. If you miss the notification, select the bell icon in the lower-right corner to see it again.

Python apps also require you to add this app setting:

`PYTHONPATH=/home/site/wwwroot/.python_packages/lib/site-packages`

.

Now you can deploy the server project:

Important

Deploying to an existing function app always overwrites the contents of that app in Azure.

In the command palette, enter and then select

**Azure Functions: Deploy to Function App**.Select the function app you just created. When prompted about overwriting previous deployments, select

**Deploy**to deploy your function code to the new function app resource.When deployment is completed, select

**View Output**to view the creation and deployment results, including the Azure resources that you created. If you miss the notification, select the bell icon in the lower-right corner to see it again.

When deployment finishes, you should see a notification in Visual Studio Code about connecting to the server. Select the **Connect** button to have the editor set up server connection information in `mcp.json`

.

## Enable built-in server authorization and authentication

The following instruction shows how to enable the built-in authorization and authentication feature on the server app and configures Microsoft Entra ID as the identity provider. When done, you test by connecting to the server in Visual Studio Code and see that you're prompted to authenticate before connecting.

### Configure authentication on server app

Open the server app on the Azure portal, and select

**Settings**>**Authentication**from the left menu.Select

**Add identity provider**>**Microsoft**as the identity provider.For

**Choose a tenant for your application and its users**, select**Workforce configuration (current tenant)**.Under

**App registration:**use these settings:Setting Selection **App registration type****Create new app registration****Name**Enter a descriptive name for your app **Client secret expiration****Recommended: 180 days****Supported account types****Current tenant - Single tenant**Under

**Additional checks:**, for**Client application requirement**select**Allow requests from specific client applications**, select the pencil icon, add the Visual Studio Code client ID`aebc6443-996d-45c2-90f0-388ff96faa56`

, and select**OK**. Leave the other sections as they are.Under

**App Service authentication settings**use these settings:Setting Selection **Restrict access****Require authentication****Unauthenticated requests****HTTP 401 Unauthorized: recommended for APIs****Token store**Check the box, which allows token refresh Select

**Add**. After settings propagate, you should see the following result:

### Preauthorize Visual Studio Code as client

Select the name of the Entra app next to

**Microsoft**. This action takes you to the**Overview**of the Entra app resource.On the left menu, find

**Manage -> Expose an API**.Under

**Authorized client applications**, select**+Add a client application**.Enter Visual Studio Code's client ID:

`aebc6443-996d-45c2-90f0-388ff96faa56`

.Select the box in front of the scope that looks like

`api://abcd123-efg456-hijk-7890123/user_impersonation`

.Select

**Add application**.

### Configure protected resource metadata (preview)

In the same

**Expose an API**view, find the**Scopes**section, and copy the scope that allows admins and users to consent to the Entra app. This value looks like`api://abcd123-efg456-hijk-7890123/user_impersonation`

.Run the same command as previous to add the setting

`WEBSITE_AUTH_PRM_DEFAULT_WITH_SCOPES`

:`az functionapp config appsettings set --name <function-app-name> --resource-group <resource-group-name> --settings "WEBSITE_AUTH_PRM_DEFAULT_WITH_SCOPES=<scope>"`

Also in the

**Expose an API**view, find the**Application ID URI**(looks like`api://abcd123-efg456-hijk-7890123`

) on the top and save for later step.

## Connect to server

Open `mcp.json`

inside the `.vscode`

directory.

When you select **Connect** in the pop-up after deployment, Visual Studio Code populates the file with server connection information.

If you miss that step, you can also open **Output** (`Ctrl/Cmd+Shift+U`

) to find the in-line connection button at the end of deployment logs.

You can also manually add connection information:

Get the server domain by running the following command:

`az functionapp show --name <FUNCTION_APP_NAME> --resource-group <RESOURCE_GROUP_NAME> --query "defaultHostName" --output tsv`

In Visual Studio Code, open command palette, search for and run the

**MCP: Add Server...**command, and then follow these prompts:Prompt Suggestion Type of server to be added **HTTP**URL of your MCP server `https://<FUNCTION_APP_NAME>.azurewebsites.azurewebsites.net/runtime/webhooks/mcp`

**Server name****remote-mcp-server**Where to install the server **Workspace**Visual Studio Code opens the

`mcp.json`

setting file for you.

Follow the instructions in the next section to connect to server depending on how you configured the authentication.

### With built-in authentication and authorization

Start the remote server by selecting the

**Start**button above the server name.When prompted about authentication with Microsoft, select

**Allow**, then sign in with your email (the one used to log into Azure portal).When you successfully connect to the server, you see the number of tools available above the server name.

Open Visual Studio Code Copilot chat in agent mode, then ask a question. For example,

`Greet with #your-remote-mcp-server-name`

.Stop server when finish testing.


To understand in detail what happens when Visual Studio Code tries to connect to the remote MCP server, see [Server authorization protocol](#server-authorization-protocol).

### With access key

If you don't enable built-in authentication and authorization and instead want to connect to your MCP server by using an access key, the `mcp.json`

should contain Functions access key in the request headers of a server registration.

Visual Studio automatically populates the access key when you start the server.

The `mcp.json`

file should look like the following example:

```
{
"servers": {
"remote-mcp-server": {
"type": "http",
"url": "https://${input:functionapp-domain}/runtime/webhooks/mcp",
"headers": {
"x-functions-key": "${input:functions-key}"
}
}
},
"inputs": [
{
"type": "promptString",
"id": "functions-key",
"description": "Functions App Key",
"password": true
},
{
"type": "promptString",
"id": "functionapp-domain",
"description": "The domain of the function app.",
"password": false
}
]
}
```


If you want to find the access key yourself, go to the Function app on Azure portal. On the left menu, find **Functions -> App keys**. Under the System keys section, find the one named *mcp_extension*.

Tip

To see connection logs, go to the server name, then select **More** > **Show Output**. For more details on the interaction between the client (Visual Studio Code) and the remote MCP server, select the gear icon and pick **Trace**.


## Configure Azure AI Foundry agent to use your tools

You can configure an [agent on Azure AI Foundry](/en-us/azure/ai-foundry/agents/quickstart) to use tools exposed by MCP servers hosted on Azure Functions.

In the Foundry portal, find the agent you want to configure with MCP servers hosted on Functions.

Under

**Tools**, select the**Add**button, then select**+ Add a new tool**.Select the

**Custom**tab, then select**Model Context Protocol (MCP)**and the**Create**button.Fill in the following information:

- Name: Name of the server
- Remote MCP Server endpoint:
- MCP extension server:
`https://<server domain>/runtime/webhooks/mcp`

- Self-hosted server:
`https://<server domain>/mcp`


- MCP extension server:
- Authentication: Choose "Microsoft Entra"
- Type: Choose "Project Managed Identity"
- Audience: This is the Entra App ID URI from
[Configure protected resource metadata](#configure-protected-resource-metadata-preview)

For example:

Select

**Connect**.Test by asking a question that can be answered with the help of a server tool in the chat window.


## Server authorization protocol

In the debug output from Visual Studio Code, you see a series of requests and responses as the MCP client and server interact. When you use the built-in MCP server authorization, you see the following sequence of events:

- The editor sends an initialization request to the MCP server.
- The MCP server responds with an error indicating that authorization is required. The response includes a pointer to the protected resource metadata (PRM) for the application. The built-in authorization feature generates the PRM for the server app.
- The editor fetches the PRM and uses it to identify the authorization server.
- The editor attempts to obtain authorization server metadata (ASM) from a well-known endpoint on the authorization server.
- Microsoft Entra ID doesn't support ASM on the well-known endpoint, so the editor falls back to using the OpenID Connect metadata endpoint to obtain the ASM. It tries to discover this by inserting the well-known endpoint before any other path information.
- The OpenID Connect specifications actually defined the well-known endpoint as being after path information, and that's where Microsoft Entra ID hosts it. So the editor tries again with that format.
- The editor successfully retrieves the ASM. It then uses this information with its own client ID to perform a sign-in. At this point, the editor prompts you to sign in and consent to the application.
- Assuming you successfully sign in and consent, the editor completes the authentication. It repeats the intialization request to the MCP server, this time including an authorization token in the request. This reattempt isn't visible at the Debug output level, but you can see it in the Trace output level.
- The MCP server validates the token and responds with a successful response to the initialization request. The standard MCP flow continues from this point, ultimately resulting in discovery of the MCP tool defined in this sample.

## Troubleshooting

If you run into trouble, ask GitHub Copilot for help. Here are some specific ideas for troubleshooting:

No other ideas at this time. Remember to ask Copilot chat about any errors that occur.

## Next steps

Learn how to [register Azure Functions-hosted MCP servers on Azure API Center](register-mcp-server-api-center).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-container-registry -->

# Create a function app in a local Linux container

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use Azure Functions Core tools to create your first function in a Linux container on your local computer, verify the function locally, and then publish the containerized function to a container registry. From a container registry, you can easily deploy your containerized functions to Azure.

For a complete example of deploying containerized functions to Azure, which include the steps in this article, see one of the following articles:

[Create your first containerized Azure Functions on Azure Container Apps](../container-apps/functions-usage)[Create your first containerized Azure Functions](functions-deploy-container)

You can also create a function app in the Azure portal by using an existing containerized function app from a container registry. For more information, see [Azure portal create using containers](functions-how-to-custom-container#azure-portal-create-using-containers).

## Choose your development language

First, you use Azure Functions tools to create your project code as a function app in a Docker container using a language-specific Linux base image. Make sure to select your language of choice at the top of the article.

Core Tools automatically generates a Dockerfile for your project that uses the most up-to-date version of the correct base image for your functions language. You should regularly update your container from the latest base image and redeploy from the updated version of your container. For more information, see [Creating containerized function apps](functions-how-to-custom-container#creating-containerized-function-apps).

## Prerequisites

Before you begin, you must have the following requirements in place:

Install the

[.NET 8.0 SDK](https://dotnet.microsoft.com/download).Install

[Azure Functions Core Tools](functions-run-local#v2)version 4.0.5198, or a later version.

- Install
[Azure Functions Core Tools](functions-run-local#v2)version 4.x.

- Install a version of
[Node.js](https://nodejs.org/)that is[supported by Azure Functions](functions-reference-node#supported-versions).

- Install a version of Python that is
[supported by Azure Functions](functions-reference-python#supported-python-versions).

- Install the
[.NET 6 SDK](https://dotnet.microsoft.com/download).

Install a version of the

[Java Developer Kit](/en-us/azure/developer/java/fundamentals/java-jdk-long-term-support)that is[supported by Azure Functions](functions-reference-java#supported-versions).Install

[Apache Maven](https://maven.apache.org)version 3.0 or above.

[Azure CLI](/en-us/cli/azure/install-azure-cli)version 2.4 or a later version.

If you don't have an [Azure subscription](../guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing), create an [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

To publish the containerized function app image you create to a container registry, you need a Docker ID and [Docker](https://docs.docker.com/install/) running on your local computer. If you don't have a Docker ID, you can [create a Docker account](https://hub.docker.com/signup).

You also need to complete the [Create a container registry](/en-us/azure/container-registry/container-registry-get-started-portal#create-a-container-registry) section of the Container Registry quickstart to create a registry instance. Make a note of your fully qualified login server name.

## Create and activate a virtual environment

In a suitable folder, run the following commands to create and activate a virtual environment named `.venv`

. Make sure to use one of the [Python versions](functions-reference-python#supported-python-versions) supported by Azure Functions.

```
python -m venv .venv
```


```
source .venv/bin/activate
```


If Python didn't install the venv package on your Linux distribution, run the following command:

```
sudo apt-get install python3-venv
```


You run all subsequent commands in this activated virtual environment.

## Create and test the local functions project

In a terminal or command prompt, run the following command for your chosen language to create a function app project in the current folder:

```
func init --worker-runtime dotnet-isolated --docker
```


```
func init --worker-runtime node --language javascript --docker
```


```
func init --worker-runtime powershell --docker
```


```
func init --worker-runtime python --docker
```


```
func init --worker-runtime node --language typescript --docker
```


In an empty folder, run the following command to generate the Functions project from a [Maven archetype](https://maven.apache.org/guides/introduction/introduction-to-archetypes.html):

```
mvn archetype:generate -DarchetypeGroupId=com.microsoft.azure -DarchetypeArtifactId=azure-functions-archetype -DjavaVersion=8 -Ddocker
```


The `-DjavaVersion`

parameter tells the Functions runtime which version of Java to use. Use `-DjavaVersion=11`

if you want your functions to run on Java 11. When you don't specify `-DjavaVersion`

, Maven defaults to Java 8. For more information, see [Java versions](functions-reference-java#java-versions).

Important

The `JAVA_HOME`

environment variable must be set to the install location of the correct version of the JDK to complete this article.

Maven asks you for values needed to finish generating the project on deployment. Follow the prompts and provide the following information:

| Prompt | Value | Description |
|---|---|---|
groupId |
`com.fabrikam` |
A value that uniquely identifies your project across all projects, following the
|

**artifactId**`fabrikam-functions`

**version**`1.0-SNAPSHOT`

**package**`com.fabrikam.functions`

Type `Y`

or press Enter to confirm.

Maven creates the project files in a new folder named *artifactId*, which in this example is `fabrikam-functions`

.

The `--docker`

option generates a *Dockerfile* for the project, which defines a suitable container for use with Azure Functions and the selected runtime.

Navigate into the project folder:

```
cd fabrikam-functions
```


Use the following command to add a function to your project, where the `--name`

argument is the unique name of your function and the `--template`

argument specifies the function's trigger. `func new`

creates a C# code file in your project.

```
func new --name HttpExample --template "HTTP trigger"
```


Use the following command to add a function to your project, where the `--name`

argument is the unique name of your function and the `--template`

argument specifies the function's trigger. `func new`

creates a subfolder matching the function name that contains a configuration file named *function.json*.

```
func new --name HttpExample --template "HTTP trigger"
```


To test the function locally, start the local Azure Functions runtime host in the root of the project folder.

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


```
mvn clean package
mvn azure-functions:run
```


After you see the `HttpExample`

endpoint written to the output, navigate to that endpoint. You should see a welcome message in the response output.

After you see the `HttpExample`

endpoint written to the output, navigate to `http://localhost:7071/api/HttpExample?name=Functions`

. The browser must display a "hello" message that echoes back `Functions`

, the value supplied to the `name`

query parameter.

Press **Ctrl**+**C** (**Command**+**C** on macOS) to stop the host.

## Build the container image and verify locally

(Optional) Examine the *Dockerfile* in the root of the project folder. The *Dockerfile* describes the required environment to run the function app on Linux. The complete list of supported base images for Azure Functions can be found in the [Azure Functions base image page](https://hub.docker.com/_/microsoft-azure-functions-base).

In the root project folder, run the [docker build](https://docs.docker.com/engine/reference/commandline/build/) command, provide a name as `azurefunctionsimage`

, and tag as `v1.0.0`

. Replace `<DOCKER_ID>`

with your Docker Hub account ID. This command builds the Docker image for the container.

```
docker build --tag <DOCKER_ID>/azurefunctionsimage:v1.0.0 .
```


When the command completes, you can run the new container locally.

To verify the build, run the image in a local container using the [docker run](https://docs.docker.com/engine/reference/commandline/run/) command, replace `<DOCKER_ID>`

again with your Docker Hub account ID, and add the ports argument as `-p 8080:80`

:

```
docker run -p 8080:80 -it <DOCKER_ID>/azurefunctionsimage:v1.0.0
```


After the image starts in the local container, browse to `http://localhost:8080/api/HttpExample`

, which must display the same greeting message as before. Because the HTTP triggered function you created uses anonymous authorization, you can call the function running in the container without having to obtain an access key. For more information, see [authorization keys](functions-bindings-http-webhook-trigger#authorization-keys).

After the image starts in the local container, browse to `http://localhost:8080/api/HttpExample?name=Functions`

, which must display the same "hello" message as before. Because the HTTP triggered function you created uses anonymous authorization, you can call the function running in the container without having to obtain an access key. For more information, see [authorization keys](functions-bindings-http-webhook-trigger#authorization-keys).

After verifying the function app in the container, press **Ctrl**+**C** (**Command**+**C** on macOS) to stop execution.

## Publish the container image to a registry

To make your container image available for deployment to a hosting environment, you must push it to a container registry. As a security best practice, you should use an Azure Container Registry instance and enforce managed identity-based connections. Docker Hub requires you to authenticate using shared secrets, which make your deployments more vulnerable.

Azure Container Registry is a private registry service for building, storing, and managing container images and related artifacts. You should use a private registry service for publishing your containers to Azure services.

Use this command to sign in to your registry instance using your current Azure credentials:

`az acr login --name <REGISTRY_NAME>`

In the previous command, replace

`<REGISTRY_NAME>`

with the name of your Container Registry instance.Use this command to tag your image with the fully qualified name of your registry login server:

`docker tag <DOCKER_ID>/azurefunctionsimage:v1.0.0 <LOGIN_SERVER>/azurefunctionsimage:v1.0.0`

Replace

`<LOGIN_SERVER>`

with the fully qualified name of your registry login server and`<DOCKER_ID>`

with your Docker ID.Use this command to push the container to your registry instance:

`docker push <LOGIN_SERVER>/azurefunctionsimage:v1.0.0`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/machine-learning-pytorch -->

# Tutorial: Deploy a pre-trained image classification model to Azure Functions with PyTorch

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to use Python, PyTorch, and Azure Functions to load a pre-trained model for classifying an image based on its contents. Because you do all work locally and create no Azure resources in the cloud, there's no cost to complete this tutorial.

- Initialize a local environment for developing Azure Functions in Python.
- Import a pre-trained PyTorch machine learning model into a function app.
- Build a serverless HTTP API for classifying an image as one of 1000 ImageNet
[classes](https://gist.github.com/yrevar/942d3a0ac09ec9e5eb3a). - Consume the API from a web app.

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). [Python 3.7.4 or above](https://www.python.org/downloads/release/python-374/). (Python 3.8.x and Python 3.6.x are also verified with Azure Functions.)- The
[Azure Functions Core Tools](functions-run-local#install-the-azure-functions-core-tools) - A code editor such as
[Visual Studio Code](https://code.visualstudio.com/)

### Prerequisite check

- In a terminal or command window, run
`func --version`

to check that the Azure Functions Core Tools are version 2.7.1846 or later. - Run
`python --version`

(Linux/macOS) or`py --version`

(Windows) to check your Python version reports 3.7.x.

## Clone the tutorial repository

In a terminal or command window, clone the following repository using Git:

`git clone https://github.com/Azure-Samples/functions-python-pytorch-tutorial.git`

Navigate into the folder and examine its contents.

`cd functions-python-pytorch-tutorial`

*start*is your working folder for the tutorial.*end*is the final result and full implementation for your reference.*resources*contains the machine learning model and helper libraries.*frontend*is a website that calls the function app.


## Create and activate a Python virtual environment

Navigate to the *start* folder and run the following commands to create and activate a virtual environment named `.venv`

.

```
cd start
python -m venv .venv
source .venv/bin/activate
```


If Python didn't install the venv package on your Linux distribution, run the following command:

```
sudo apt-get install python3-venv
```


You run all subsequent commands in this activated virtual environment. (To exit the virtual environment, run `deactivate`

.)

## Create a local functions project

In Azure Functions, a function project is a container for one or more individual functions that each responds to a specific trigger. All functions in a project share the same local and hosting configurations. In this section, you create a function project that contains a single boilerplate function named `classify`

that provides an HTTP endpoint. You add more specific code in a later section.

In the

*start*folder, use the Azure Functions Core Tools to initialize a Python function app:`func init --worker-runtime python`

After initialization, the

*start*folder contains various files for the project, including configurations files named[local.settings.json](functions-develop-local#local-settings-file)and[host.json](functions-host-json). Because*local.settings.json*can contain secrets downloaded from Azure, the file is excluded from source control by default in the*.gitignore*file.Tip

Because a function project is tied to a specific runtime, all the functions in the project must be written with the same language.

Add a function to your project by using the following command, where the

`--name`

argument is the unique name of your function and the`--template`

argument specifies the function's trigger.`func new`

create a subfolder matching the function name that contains a code file appropriate to the project's chosen language and a configuration file named*function.json*.`func new --name classify --template "HTTP trigger"`

This command creates a folder matching the name of the function,

*classify*. In that folder are two files:*__init__.py*, which contains the function code, and*function.json*, which describes the function's trigger and its input and output bindings. For details on the contents of these files, see[Programming model](functions-reference-python?pivots=python-mode-configuration#programming-model)in the Python developer guide.

## Run the function locally

Start the function by starting the local Azure Functions runtime host in the

*start*folder:`func start`

Once you see the

`classify`

endpoint appear in the output, navigate to the URL,`http://localhost:7071/api/classify?name=Azure`

. The message "Hello Azure!" should appear in the output.Use

**Ctrl**-**C**to stop the host.

## Import the PyTorch model and add helper code

To modify the `classify`

function to classify an image based on its contents, you use a pre-trained [ResNet](https://arxiv.org/abs/1512.03385) model. The pre-trained model, which comes from [PyTorch](https://pytorch.org/hub/pytorch_vision_resnet/), classifies an image into 1 of 1000 [ImageNet classes](https://gist.github.com/yrevar/942d3a0ac09ec9e5eb3a). You then add some helper code and dependencies to your project.

In the

*start*folder, run the following command to copy the prediction code and labels into the*classify*folder.`cp ../resources/predict.py classify cp ../resources/labels.txt classify`

Verify that the

*classify*folder contains files named*predict.py*and*labels.txt*. If not, check that you ran the command in the*start*folder.Open

*start/requirements.txt*in a text editor and add the dependencies required by the helper code, which should look like:`azure-functions requests -f https://download.pytorch.org/whl/torch_stable.html torch==1.13.0+cpu torchvision==0.14.0+cpu`

Tip

The versions of torch and torchvision must match values listed in the version table of the

[PyTorch vision repo](https://github.com/pytorch/vision).Save

*requirements.txt*, then run the following command from the*start*folder to install the dependencies.`pip install --no-cache-dir -r requirements.txt`


Installation may take a few minutes, during which time you can proceed with modifying the function in the next section.

Tip

On Windows, you may encounter the error, "Could not install packages due to an EnvironmentError: [Errno 2] No such file or directory:" followed by a long pathname to a file like

sharded_mutable_dense_hashtable.cpython-37.pyc. Typically, this error happens because the depth of the folder path becomes too long. In this case, set the registry key`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\FileSystem@LongPathsEnabled`

to`1`

to enable long paths. Alternately, check where your Python interpreter is installed. If that location has a long path, try reinstalling in a folder with a shorter path.

## Update the function to run predictions

Open

*classify/__init__.py*in a text editor and add the following lines after the existing`import`

statements to import the standard JSON library and the*predict*helpers:`import logging import azure.functions as func import json # Import helper script from .predict import predict_image_from_url`

Replace the entire contents of the

`main`

function with the following code:`def main(req: func.HttpRequest) -> func.HttpResponse: image_url = req.params.get('img') logging.info('Image URL received: ' + image_url) results = predict_image_from_url(image_url) headers = { "Content-type": "application/json", "Access-Control-Allow-Origin": "*" } return func.HttpResponse(json.dumps(results), headers = headers)`

This function receives an image URL in a query string parameter named

`img`

. It then calls`predict_image_from_url`

from the helper library to download and classify the image using the PyTorch model. The function then returns an HTTP response with the results.Important

Because this HTTP endpoint is called by a web page hosted on another domain, the response includes an

`Access-Control-Allow-Origin`

header to satisfy the browser's Cross-Origin Resource Sharing (CORS) requirements.In a production application, change

`*`

to the web page's specific origin for added security.Save your changes, then assuming that dependencies have finished installing, start the local function host again with

`func start`

. Be sure to run the host in the*start*folder with the virtual environment activated. Otherwise the host will start, but you'll see errors when invoking the function.`func start`

In a browser, open the following URL to invoke the function with the URL of a Bernese Mountain Dog image and confirm that the returned JSON classifies the image as a Bernese Mountain Dog.

`http://localhost:7071/api/classify?img=https://raw.githubusercontent.com/Azure-Samples/functions-python-pytorch-tutorial/master/resources/assets/Bernese-Mountain-Dog-Temperament-long.jpg`

Keep the host running because you use it in the next step.


### Run the local web app front end to test the function

To test invoking the function endpoint from another web app, there's a simple app in the repository's *frontend* folder.

Open a new terminal or command prompt and activate the virtual environment (as described earlier under

[Create and activate a Python virtual environment](#create-and-activate-a-python-virtual-environment)).Navigate to the repository's

*frontend*folder.Start an HTTP server with Python:

`python -m http.server`

In a browser, navigate to

`localhost:8000`

, then enter one of the following photo URLs into the textbox, or use the URL of any publicly accessible image.`https://raw.githubusercontent.com/Azure-Samples/functions-python-pytorch-tutorial/master/resources/assets/Bernese-Mountain-Dog-Temperament-long.jpg`

`https://github.com/Azure-Samples/functions-python-pytorch-tutorial/blob/master/resources/assets/bald-eagle.jpg?raw=true`

`https://raw.githubusercontent.com/Azure-Samples/functions-python-pytorch-tutorial/master/resources/assets/penguin.jpg`


Select

**Submit**to invoke the function endpoint to classify the image.If the browser reports an error when you submit the image URL, check the terminal in which you're running the function app. If you see an error like "No module found 'PIL'", you may have started the function app in the

*start*folder without first activating the virtual environment you created earlier. If you still see errors, run`pip install -r requirements.txt`

again with the virtual environment activated and look for errors.

## Clean up resources

Because the entirety of this tutorial runs locally on your machine, there are no Azure resources or services to clean up.

## Next steps

In this tutorial, you learned how to build and customize an HTTP API endpoint with Azure Functions to classify images using a PyTorch model. You also learned how to call the API from a web app. You can use the techniques in this tutorial to build out APIs of any complexity, all while running on the serverless compute model provided by Azure Functions.

See also:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-identity-based-connections-tutorial-2 -->

# Tutorial: Use identity-based connections instead of secrets with triggers and bindings

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This tutorial shows you how to configure Azure Functions to connect to Azure Service Bus queues by using managed identities, instead of secrets stored in the function app settings. The tutorial is a continuation of the [Create a function app without default storage secrets in its definition](functions-identity-based-connections-tutorial) tutorial. To learn more about identity-based connections, see [Configure an identity-based connection.](functions-reference#configure-an-identity-based-connection).

While the procedures shown work generally for all languages, this tutorial currently supports C# class library functions on Windows specifically.

In this tutorial, you learn how to:

- Create a Service Bus namespace and queue.
- Configure your function app with a managed identity.
- Create a role assignment granting that identity permission to read from the Service Bus queue.
- Create and deploy a function app with a Service Bus trigger.
- Verify your identity-based connection to the Service Bus.

## Prerequisite

[Azure Functions Core Tools](functions-run-local#v2)version 4.x.Complete the previous tutorial:

[Create a function app with identity-based connections](functions-identity-based-connections-tutorial).

## Create a Service Bus namespace and queue

In the

[Azure portal](https://portal.azure.com), choose**Create a resource (+)**.On the

**Create a resource**page, search for and select**Service Bus**, and then select**Create**.On the

**Basics**page, use the following table to configure the Service Bus namespace settings. Use the default values for the remaining options.Option Suggested value Description **Subscription**Your subscription The subscription under which your resources are created. [Resource group](../azure-resource-manager/management/overview)myResourceGroup The resource group you created with your function app. **Namespace name**Globally unique name The namespace of your instance from which to trigger your function. Because the namespace is publicly accessible, you must use a name that is globally unique across Azure. The name must also be between 6 and 50 characters in length, contain only alphanumeric characters and dashes, and can't start with a number. [Location](https://azure.microsoft.com/regions/)myFunctionRegion The region where you created your function app. **Pricing tier**Basic The basic Service Bus tier. Select

**Review + create**. After validation finishes, select**Create**.After deployment completes, select

**Go to resource**.In your new Service Bus namespace, select

**+ Queue**to add a queue.Enter

**myinputqueue**as the new queue's name and select**Create**.

Now that you have a queue, you can add a role assignment to the managed identity of your function app.

## Configure your Service Bus trigger with a managed identity

To use Service Bus triggers with identity-based connections, you need to add the **Azure Service Bus Data Receiver** role assignment to the managed identity in your function app. This role is required when using managed identities to trigger off of your Service Bus namespace. You can also add your own account to this role, which makes it possible to connect to the Service Bus namespace during local testing.

Note

Role requirements for using identity-based connections vary depending on the service and how you are connecting to it. Needs vary across triggers, input bindings, and output bindings. For more information about specific role requirements, see the trigger and binding documentation for the service.

In your Service Bus namespace that you created, select

**Access control (IAM)**. This page is where you can view and configure who has access to the resource.Select

**+ Add**and select**Add role assignment**.Search for

**Azure Service Bus Data Receiver**, select it, and then select**Next**.On the

**Members**tab, under**Assign access to**, choose**Managed Identity**Select

**Select members**to open the**Select managed identities**panel.Confirm that the

**Subscription**is the one in which you created the resources earlier.In the

**Managed identity**selector, choose**Function App**from the**System-assigned managed identity**category. The**Function App**label might have a number in parentheses next to it, indicating the number of apps in the subscription with system-assigned identities.Your app should appear in a list below the input fields. If you don't see it, you can use the

**Select**box to filter the results with your app's name.Select your application. It should move down into the

**Selected members**section. Select**Select**.Back on the

**Add role assignment**screen, select**Review + assign**. Review the configuration, and then select**Review + assign**.

You've granted your function app access to the Service Bus namespace using managed identities.

## Connect to the Service Bus in your function app

In the portal, search for the function app you created in the

[previous tutorial](functions-identity-based-connections-tutorial), or browse to it in the**Function App**page.In your function app, expand

**Settings**, and then select**Environment variables**.In the

**App settings**tab, select**+ Add**to create a setting. Use the information in the following table to enter the**Name**and**Value**for the new setting:Name Value Description **ServiceBusConnection__fullyQualifiedNamespace**<SERVICE_BUS_NAMESPACE>.servicebus.windows.net This setting connects your function app to the Service Bus using an identity-based connection instead of secrets. Select

**Apply**, and then select**Apply**and**Confirm**to save your changes and restart the app function.

Note

When you use [Azure App Configuration](../azure-app-configuration/quickstart-azure-functions-csharp) or [Key Vault](/en-us/azure/key-vault/general/overview) to provide settings for Managed Identity connections, setting names should use a valid key separator, such as `:`

or `/`

, in place of the `__`

to ensure names are resolved correctly.

For example, `ServiceBusConnection:fullyQualifiedNamespace`

.

Now that you've prepared the function app to connect to the Service Bus namespace using a managed identity, you can add a new function that uses a Service Bus trigger to your local project.

## Add a Service Bus triggered function

Run the

`func init`

command, as follows, to create a functions project in a folder named LocalFunctionProj with the specified runtime:`func init LocalFunctionProj --dotnet`

Navigate to the project folder:

`cd LocalFunctionProj`

In the root project folder, run the following command:

`dotnet add package Microsoft.Azure.WebJobs.Extensions.ServiceBus --version 5.2.0`

This command replaces the default version of the Service Bus extension package with a version that supports managed identities.

Run the following command to add a Service Bus triggered function to the project:

`func new --name ServiceBusTrigger --template ServiceBusQueueTrigger`

This command adds the code for a new Service Bus trigger and a reference to the extension package. You need to add a Service Bus namespace connection setting for this trigger.

Open the new

*ServiceBusTrigger.cs*project file and replace the`ServiceBusTrigger`

class with the following code:`public static class ServiceBusTrigger { [FunctionName("ServiceBusTrigger")] public static void Run([ServiceBusTrigger("myinputqueue", Connection = "ServiceBusConnection")]string myQueueItem, ILogger log) { log.LogInformation($"C# ServiceBus queue trigger function processed message: {myQueueItem}"); } }`

This code sample updates the queue name to

`myinputqueue`

, which is the same name as you queue you created earlier. It also sets the name of the Service Bus connection to`ServiceBusConnection`

. This name is the Service Bus namespace used by the identity-based connection`ServiceBusConnection__fullyQualifiedNamespace`

you configured in the portal.

Note

If you try to run your functions now using `func start`

, you'll receive an error. This is because you don't have an identity-based connection defined locally. If you want to run your function locally, set the app setting `ServiceBusConnection__fullyQualifiedNamespace`

in `local.settings.json`

as you did in [the previous section](#connect-to-the service-bus-in-your-function-app). In addition, you need to assign the role to your developer identity. For more information, see [local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

Note

When using [Azure App Configuration](../azure-app-configuration/quickstart-azure-functions-csharp) or [Key Vault](/en-us/azure/key-vault/general/overview) to provide settings for Managed Identity connections, setting names should use a valid key separator such as `:`

or `/`

in place of the `__`

to ensure names are resolved correctly.

For example, `ServiceBusConnection:fullyQualifiedNamespace`

.

## Publish the updated project

Run the following command to locally generate the files needed for the deployment package:

`dotnet publish --configuration Release`

Browse to the

`\bin\Release\netcoreapp3.1\publish`

subfolder and create a .zip file from its contents.Publish the .zip file by running the following command, replacing the

`FUNCTION_APP_NAME`

,`RESOURCE_GROUP_NAME`

, and`PATH_TO_ZIP`

parameters as appropriate:`az functionapp deploy -n FUNCTION_APP_NAME -g RESOURCE_GROUP_NAME --src-path PATH_TO_ZIP`


Now that you've updated the function app with the new trigger, you can verify that it works using the identity.

## Validate your changes

In the portal, search for

`Application Insights`

and select**Application Insights**under**Services**.In

**Application Insights**, browse or search for your named instance.In your instance, select

**Live Metrics**under**Investigate**.Keep the previous tab open, and open the Azure portal in a new tab. In your new tab, navigate to your Service Bus namespace, select

**Queues**from the left menu.Select your queue named

`myinputqueue`

.Select

**Service Bus Explorer**from the left menu.Send a test message.

Select your open

**Live Metrics**tab and see the Service Bus queue execution.

Congratulations! You have successfully set up your Service Bus queue trigger with a managed identity.

## Clean up resources

In the preceding steps, you created Azure resources in a resource group. If you don't expect to need these resources in the future, you can delete them by deleting the resource group:

From the Azure portal menu or home page, select

**Resource groups**>**myResourceGroup**.On the

**myResourceGroup**pane, make sure that the listed resources are the ones you want to delete.Select

**Delete resource group**. Type**myResourceGroup**in the text box to confirm, and then select**Delete**.

## Next steps

In this tutorial, you created a function app with identity-based connections.

Advance to the next article to learn how to manage identity.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-service-bus -->

# Azure Service Bus bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions integrates with [Azure Service Bus](https://azure.microsoft.com/services/service-bus) via [triggers and bindings](functions-triggers-bindings). Integrating with Service Bus allows you to build functions that react to and send queue or topic messages.

| Action | Type |
|---|---|
| Run a function when a Service Bus queue or topic message is created |
|

[Output binding](functions-bindings-service-bus-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

Add the extension to your project installing this [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.servicebus).

The functionality of the extension varies depending on the extension version:

This version introduces the ability to [connect using an identity instead of a secret](functions-reference#configure-an-identity-based-connection). For a tutorial on configuring your function apps with managed identities, see the [creating a function app with identity-based connections tutorial](functions-identity-based-connections-tutorial).

This version allows you to bind to types from [Azure.Messaging.ServiceBus](/en-us/dotnet/api/azure.messaging.servicebus).

This version supports configuration of triggers and bindings through [.NET Aspire integration](dotnet-aspire-integration#connection-configuration-with-aspire).

Add the extension to your project by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.ServiceBus), version 5.x.

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

**Service Bus trigger**

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

. This prevents the runtime from attempting to complete messages after a successful function invocation.**Service Bus output binding**

When you want the function to write a single message, the Service Bus output binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The message as a string. Use when the message is simple text. |
`byte[]` |
The bytes of the message. |
| JSON serializable types | An object representing the message. Functions attempts to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write multiple messages, the Service Bus output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single message types |
An array containing multiple message. Each entry represents one message. |

For other output scenarios, create and use a [ServiceBusClient](/en-us/dotnet/api/azure.messaging.servicebus.servicebusclient) with other types from [Azure.Messaging.ServiceBus](/en-us/dotnet/api/azure.messaging.servicebus) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

## SDK Binding Types

SDK Types for Azure Service Bus are in Preview. Follow the [Python SDK Bindings for Service Bus Sample](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-servicebus/samples/README.md) to get started with SDK Types for Service Bus in Python.

Important

Using SDK type bindings requires the [Python v2 programming model](functions-reference-python?pivots=python-mode-decorators#sdk-type-bindings).

| Binding | Parameter types | Samples |
|---|---|---|
| ServiceBus trigger |
|

`ServiceBusReceivedMessage`

## host.json settings

This section describes the configuration settings available for this binding, which depends on the runtime and extension version.

```
{
"version": "2.0",
"extensions": {
"serviceBus": {
"clientRetryOptions":{
"mode": "exponential",
"tryTimeout": "00:01:00",
"delay": "00:00:00.80",
"maxDelay": "00:01:00",
"maxRetries": 3
},
"prefetchCount": 0,
"transportType": "amqpWebSockets",
"webProxy": "https://proxyserver:8080",
"autoCompleteMessages": true,
"maxAutoLockRenewalDuration": "00:05:00",
"maxConcurrentCalls": 16,
"maxConcurrentSessions": 8,
"maxMessageBatchSize": 1000,
"minMessageBatchSize": 1,
"maxBatchWaitTime": "00:00:30",
"sessionIdleTimeout": "00:01:00",
"enableCrossEntityTransactions": false
}
}
}
```


The `clientRetryOptions`

settings only apply to interactions with the Service Bus service. They don't affect retries of function executions. For more information, see [Retries](functions-bindings-error-pages#retries).

| Property | Default | Description |
|---|---|---|
mode |
`Exponential` |
The approach to use for calculating retry delays. The default exponential mode retries attempts with a delay based on a back-off strategy where each attempt increases the wait duration before retrying. The `Fixed` mode retries attempts at fixed intervals with each delay having a consistent duration. |
tryTimeout |
`00:01:00` |
The maximum duration to wait for an operation per attempt. |
delay |
`00:00:00.80` |
The delay or back-off factor to apply between retry attempts. |
maxDelay |
`00:01:00` |
The maximum delay to allow between retry attempts |
maxRetries |
`3` |
The maximum number of retry attempts before considering the associated operation to have failed. |
prefetchCount |
`0` |
Gets or sets the number of messages that the message receiver can simultaneously request. |
transportType |
amqpTcp | The protocol and transport that is used for communicating with Service Bus. Available options: `amqpTcp` , `amqpWebSockets` |
webProxy |
n/a | The proxy to use for communicating with Service Bus over web sockets. A proxy cannot be used with the `amqpTcp` transport. |
autoCompleteMessages |
`true` |
Determines whether or not to automatically complete messages after successful execution of the function. |
maxAutoLockRenewalDuration |
`00:05:00` |
The maximum duration within which the message lock will be renewed automatically. This setting only applies for functions that receive a single message at a time and doesn't apply to functions receiving a batch of messages. For batches, the maximum duration is set
|

**maxConcurrentCalls**`16`

`16`

means that the maximum number of concurrent calls per instance is really `32`

(or `2 * 16`

). This setting is used only when the `isSessionsEnabled`

property or attribute on [the trigger](functions-bindings-service-bus-trigger)is set to`false`

. This setting only applies for functions that receive a single message at a time as opposed to in a batch.**maxConcurrentSessions**`8`

`isSessionsEnabled`

property or attribute on [the trigger](functions-bindings-service-bus-trigger)is set to`true`

. This setting only applies for functions that receive a single message at a time.**maxMessageBatchSize**`1000`

**minMessageBatchSize**1`1`

`maxMessageBatchSize`

. The minimum size isn't strictly guaranteed. A partial batch is dispatched when a full batch can't be prepared before the

`maxBatchWaitTime`

has elapsed.**maxBatchWaitTime**1`00:00:30`

`minMessageBatchSize`

is larger than 1 and is ignored otherwise. If less than `minMessageBatchSize`

messages were available before the wait time elapses, the function is invoked with a partial batch. The longest allowed wait time is 50% of the entity message lock duration, meaning the maximum allowed is 2 minutes and 30 seconds. Otherwise, you may get lock exceptions. **NOTE:**This interval is not a strict guarantee for the exact timing on which the function is invoked. There is a small margin of error due to timer precision.**sessionIdleTimeout****enableCrossEntityTransactions**`false`

1 Using `minMessageBatchSize`

and `maxBatchWaitTime`

requires [v5.10.0](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ServiceBus/5.10.0) of the `Microsoft.Azure.WebJobs.Extensions.ServiceBus`

package, or a later version.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/how-to-create-function-vs-code -->

# Quickstart: Create and deploy function code to Azure using Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use Visual Studio Code to create a function that responds to HTTP requests from a template. Use GitHub Copilot to improve the generated function code, verify code updates locally, and then deploy it to the serverless Flex Consumption hosting plan in Azure Functions.

Use Visual Studio Code to create a [custom handler](functions-custom-handlers) function that responds to HTTP requests. After verifying the code locally, you deploy it to the serverless Flex Consumption hosting plan in Azure Functions.

Custom handlers can be used to create functions in any language or runtime by running an HTTP server process. This article supports both Go and Rust.

Completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

Make sure to select your preferred development language at the top of the article.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code.

[C# extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)for Visual Studio Code.

The

[Java Development Kit](/en-us/azure/developer/java/fundamentals/java-support-on-azure), version 8, 11, 17, or 21 (Linux-only).[Apache Maven](https://maven.apache.org), version 3.0 or above.

[Node.js 18.x](https://nodejs.org/en/about/previous-releases)or above. Use the`node --version`

command to check your version.

Python versions that are

[supported by Azure Functions](supported-languages#languages-by-runtime-version). For more information, see[How to install Python](https://wiki.python.org/moin/BeginnersGuide/Download).The

[Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)for Visual Studio Code.

## Install or update Core Tools

The Azure Functions extension for Visual Studio Code integrates with Azure Functions Core Tools so that you can run and debug your functions locally in Visual Studio Code using the Azure Functions runtime. Before getting started, it's a good idea to install Core Tools locally or update an existing installation to use the latest version.

In Visual Studio Code, select F1 to open the command palette, and then search for and run the command **Azure Functions: Install or Update Core Tools**.

This command tries to either start a package-based installation of the latest version of Core Tools or update an existing package-based installation. If you don't have npm or Homebrew installed on your local computer, you must instead [manually install or update Core Tools](functions-run-local#install-the-azure-functions-core-tools).

## Create your local project

In this section, you use Visual Studio Code to create a local Azure Functions project in your preferred language. Later in the article, you update, run, and then publish your function code to Azure.

In Visual Studio Code, press

`F1`to open the command palette. Search for and run the command`Azure Functions: Create New Project...`

.Choose the directory location for your project workspace and choose

**Select**. You should either create a new folder or choose an empty folder for the project workspace. Don't choose a project folder that is already part of a workspace.Provide the following information at the prompts:

Prompt Selection **Select a language**Choose `C#`

.**Select a .NET runtime**Choose `.NET 8.0 LTS`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Provide a namespace**Type `My.Functions`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `Java`

.**Select a version of Java**Choose `Java 8`

,`Java 11`

,`Java 17`

or`Java 21`

, the Java version on which your functions run in Azure. Choose a Java version that you've verified locally.**Provide a group ID**Choose `com.function`

.**Provide an artifact ID**Choose `myFunction`

.**Provide a version**Choose `1.0-SNAPSHOT`

.**Provide a package name**Choose `com.function`

.**Provide an app name**Choose `myFunction-12345`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Select the build tool for Java project**Choose `Maven`

.**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `JavaScript`

.**Select a JavaScript programming model**Choose `Model V4`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `TypeScript`

.**Select a JavaScript programming model**Choose `Model V4`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `Python`

.**Select a Python interpreter to create a virtual environment**Choose your preferred Python interpreter. If an option isn't shown, type in the full path to your Python binary. **Select a template for your project's first function**Choose `HTTP trigger`

.**Name of the function you want to create**Enter `HttpExample`

.**Authorization level**Choose `FUNCTION`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language for your function project**Choose `PowerShell`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language for your function project**Choose `Custom Handler`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Using this information, Visual Studio Code generates a code project for Azure Functions with an HTTP trigger function endpoint. You can view the local project files in the Explorer. To learn more about files that are created, see

[Generated project files](functions-develop-vs-code?tabs=javascript#generated-project-files).

In the local.settings.json file, update the

`AzureWebJobsStorage`

setting as in the following example:`"AzureWebJobsStorage": "UseDevelopmentStorage=true",`

This setting tells the local Functions host to use the storage emulator for the storage connection required by the Python v2 model. When you publish your project to Azure, this setting uses the default storage account instead. If you use an Azure Storage account during local development, set your storage account connection string here.


## Start the emulator

In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azurite: Start`

.Check the bottom bar and verify that Azurite emulation services are running. If so, you can now run your function locally.


## Create and build your function

The *function.json* file in the *HttpExample* folder declares an HTTP trigger function. You complete the function by adding a handler and compiling it into an executable.

Press

`Ctrl + N`(`Cmd + N`on macOS) to create a new file. Save it as*handler.go*in the function app root (in the same folder as*host.json*).In

*handler.go*, add the following code and save the file. This is your Go custom handler.`package main import ( "fmt" "log" "net/http" "os" ) func helloHandler(w http.ResponseWriter, r *http.Request) { message := "This HTTP triggered function executed successfully. Pass a name in the query string for a personalized response.\n" name := r.URL.Query().Get("name") if name != "" { message = fmt.Sprintf("Hello, %s. This HTTP triggered function executed successfully.\n", name) } fmt.Fprint(w, message) } func main() { listenAddr := ":8080" if val, ok := os.LookupEnv("FUNCTIONS_CUSTOMHANDLER_PORT"); ok { listenAddr = ":" + val } http.HandleFunc("/api/HttpExample", helloHandler) log.Printf("About to listen on %s. Go to https://127.0.0.1%s/", listenAddr, listenAddr) log.Fatal(http.ListenAndServe(listenAddr, nil)) }`

Press

`Ctrl + Shift + ``or select*New Terminal*from the*Terminal*menu to open a new integrated terminal in VS Code.Compile your custom handler using the following command. An executable file named

`handler`

(`handler.exe`

on Windows) is output in the function app root folder.`go build handler.go`


## Configure your function app

The function host needs to be configured to run your custom handler binary when it starts.

Open

*host.json*.In the

`customHandler.description`

section, set the value of`defaultExecutablePath`

to`handler`

(on Windows, set it to`handler.exe`

).In the

`customHandler`

section, add a property named`enableForwardingHttpRequest`

and set its value to`true`

. For functions consisting of only an HTTP trigger, this setting simplifies programming by allow you to work with a typical HTTP request instead of the custom handler[request payload](functions-custom-handlers#request-payload).Confirm the

`customHandler`

section looks like this example. Save the file.`"customHandler": { "description": { "defaultExecutablePath": "handler", "workingDirectory": "", "arguments": [] }, "enableForwardingHttpRequest": true }`


The function app is configured to start your custom handler executable.

## Run the function locally

Visual Studio Code integrates with [Azure Functions Core tools](functions-run-local) to let you run this project on your local development computer before you publish to Azure.

To start the function locally, press

`F5`or the**Run and Debug**icon in the left-hand side Activity bar. The**Terminal**panel displays the Output from Core Tools. Your app starts in the**Terminal**panel. You can see the URL endpoint of your HTTP-triggered function running locally.If you have trouble running on Windows, make sure that the default terminal for Visual Studio Code isn't set to

**WSL Bash**.With Core Tools still running in

**Terminal**, choose the Azure icon in the activity bar. In the**Workspace**area, expand**Local Project**>**Functions**. Right-click (Windows) or`Ctrl -`click (macOS) the new function and choose**Execute Function Now...**.In

**Enter request body**you see the request message body value of`{ "name": "Azure" }`

. Press Enter to send this request message to your function.When the function executes locally and returns a response, a notification is raised in Visual Studio Code. Information about the function execution is shown in

**Terminal**panel.With the

**Terminal**panel focused, press`Ctrl + C`to stop Core Tools and disconnect the debugger.

After you verify that the function runs correctly on your local computer, you can optionally use AI tools, such as GitHub Copilot in Visual Studio Code, to update template-generated function code.

## Use AI to normalize and validate input

This example prompt for Copilot Chat updates the existing function code to retrieve parameters from either the query string or JSON body. It applies formatting or type conversions and returns the parameters as JSON in the response:

```
Modify the function to accept name, email, and age from the JSON body of the
request. If any of these parameters are missing from the query string, read
them from the JSON body. Return all three parameters in the JSON response,
applying these rules:
Title-case the name
Lowercase the email
Convert age to an integer if possible, otherwise return "not provided"
Use sensible defaults if any parameter is missing
Make sure that any added packages are compatible with the version of the packages already in the project
```


```
Modify the function to accept name, email, and age from the JSON body of the
request. If any of these parameters are missing from the query string, read
them from the JSON body. Return all three parameters in the JSON response,
applying these rules:
Title-case the name
Lowercase the email
Convert age to an integer if possible, otherwise return "not provided"
Use sensible defaults if any parameter is missing
```


```
Modify the function to accept name, email, and age from the JSON body of the
request. If any of these parameters are missing from the query string, read
them from the JSON body. Return all three parameters in the JSON response,
applying these rules:
Title-case the name
Lowercase the email
Convert age to an integer if possible, otherwise return "not provided"
Use sensible defaults if any parameter is missing
Update the FunctionTest.java file to test the new logic.
```


You can customize your prompt to add specifics as needed. Then run the app again locally and verify that it works as expected after the code changes. This time, use a message body like:

```
{ "name": "devon torres", "email": "torres.devon@contoso.com", "age": "34" }
```


Tip

GitHub Copilot is powered by AI, so surprises and mistakes are possible. If you encounter any errors during execution, paste the error message in the chat window, select **Agent** mode, and ask Copilot to help resolve the error. For more information, see [Copilot FAQs](https://aka.ms/copilot-general-use-faqs).

When running in **Agent** mode, the results of this customization depend on the specific tools available to your agent.

When you're satisfied with your app, use Visual Studio Code to publish the project directly to Azure.

After you verify that the function runs correctly on your local computer, use Visual Studio Code to publish the project directly to Azure.

## Sign in to Azure

Before you can create Azure resources or publish your app, you must sign in to Azure.

If you aren't already signed in, in the

**Activity bar**, select the Azure icon. Then under**Resources**, select**Sign in to Azure**.If you're already signed in and can see your existing subscriptions, go to the next section. If you don't yet have an Azure account, select

**Create an Azure Account**. Students can select**Create an Azure for Students Account**.When you are prompted in the browser, select your Azure account and sign in by using your Azure account credentials. If you create a new account, you can sign in after your account is created.

After you successfully sign in, you can close the new browser window. The subscriptions that belong to your Azure account are displayed in the side bar.


## Create the function app in Azure

In this section, you create a function app in the Flex Consumption plan along with related resources in your Azure subscription. Many of the resource creation decisions are made for you based on default behaviors. For more control over the created resources, you must instead [create your function app with advanced options](functions-develop-vs-code?tabs=advanced-options#publish-to-azure).

In Visual Studio Code, select F1 to open the command palette. At the prompt (

`>`

), enter and then select**Azure Functions: Create Function App in Azure**.At the prompts, provide the following information:

Prompt Action **Select subscription**Select the Azure subscription to use. The prompt doesn't appear when you have only one subscription visible under **Resources**.**Enter a new function app name**Enter a globally unique name that's valid in a URL path. The name you enter is validated to make sure that it's unique in Azure Functions. **Select a location for new resources**Select an Azure region. For better performance, select a [region](https://azure.microsoft.com/regions/)near you. Only regions supported by Flex Consumption plans are displayed.**Select a runtime stack**Select the language version you currently run locally. **Select resource authentication type**Select **Managed identity**, which is the most secure option for connecting to the[default host storage account](storage-considerations#storage-account-guidance).In the

**Azure: Activity Log**panel, the Azure extension shows the status of individual resources as they're created in Azure.When the function app is created, the following related resources are created in your Azure subscription. The resources are named based on the name you entered for your function app.

- A
[resource group](../azure-resource-manager/management/overview), which is a logical container for related resources. - A function app, which provides the environment for executing your function code. A function app lets you group functions as a logical unit for easier management, deployment, and sharing of resources within the same hosting plan.
- An Azure App Service plan, which defines the underlying host for your function app.
- A standard
[Azure Storage account](../storage/common/storage-account-create), which is used by the Functions host to maintain state and other information about your function app. - An Application Insights instance that's connected to the function app, and which tracks the use of your functions in the app.
- A user-assigned managed identity that's added to the
[Storage Blob Data Contributor](/en-us/azure/role-based-access-control/built-in-roles/storage#storage-blob-data-contributor)role in the new default host storage account.

A notification is displayed after your function app is created and the deployment package is applied.

Tip

By default, the Azure resources required by your function app are created based on the name you enter for your function app. By default, the resources are created with the function app in the same, new resource group. If you want to customize the names of the associated resources or reuse existing resources,

[publish the project with advanced create options](functions-develop-vs-code?tabs=advanced-options#publish-to-azure).- A

## Compile the custom handler for Azure

In this section, you compile your project for deployment to Azure in a function app running Linux. In most cases, you need to recompile your binary and adjust your configuration to match the target platform before publishing it to Azure.

## Deploy the project to Azure

Important

Deploying to an existing function app always overwrites the contents of that app in Azure.

In the command palette, enter and then select

**Azure Functions: Deploy to Function App**.Select the function app you just created. When prompted about overwriting previous deployments, select

**Deploy**to deploy your function code to the new function app resource.When deployment is completed, select

**View Output**to view the creation and deployment results, including the Azure resources that you created. If you miss the notification, select the bell icon in the lower-right corner to see it again.

## Run the function in Azure

Press

`F1`to display the command palette, then search for and run the command`Azure Functions:Execute Function Now...`

. If prompted, select your subscription.Select your new function app resource and

`HttpExample`

as your function.In

**Enter request body**type`{ "name": "Contoso", "email": "me@contoso.com", "age": "34" }`

, then press Enter to send this request message to your function.When the function executes in Azure, the response is displayed in the notification area. Expand the notification to review the full response.


## Troubleshooting

Use the following table to resolve the most common issues encountered when using this article.

| Problem | Solution |
|---|---|
| Can't create a local function project? | Make sure you have the
|

[Azure Functions Core Tools installed](functions-run-local?tabs=node).When running on Windows, make sure that the default terminal shell for Visual Studio Code isn't set to WSL Bash.

## Clean up resources

When you continue to the [next step](#next-steps) and add an Azure Storage queue binding to your function, you'll need to keep all your resources in place to build on what you've already done.

Otherwise, you can use the following steps to delete the function app and its related resources to avoid incurring any further costs.

- In Visual Studio Code, select the Azure icon to open the Azure explorer.
- In the Resource Groups section, find your resource group.
- Right-click the resource group and select
**Delete**.

To learn more about Functions costs, see [Estimating Consumption plan costs](functions-consumption-costs).

## Next steps

You used [Visual Studio Code](functions-develop-vs-code) to create a function app with a simple HTTP-triggered function. In the next articles, you expand that function by connecting to either Azure Cosmos DB or Azure Storage. To learn more about connecting to other Azure services, see [Add bindings to an existing function in Azure Functions](add-bindings-existing-function). If you want to learn more about security, see [Securing Azure Functions](security-concepts).
