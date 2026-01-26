---
merged_at: 2026-01-26T21:02:36.321295
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __functions-continuous-deployment_functions-bindings-web-pubsub-trigger_create-f_95f2e2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-continuous-deployment_functions-bindings-web-pubsub-trigger.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-continuous-deployment.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-continuous-deployment -->

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

<!-- DOCUMENTO FUSIONADO: functions-bindings-web-pubsub-trigger.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-web-pubsub-trigger -->

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

<!-- DOCUMENTO FUSIONADO: create-first-function-azure-developer-cli.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/create-first-function-azure-developer-cli -->

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

<!-- DOCUMENTO FUSIONADO: _scenario-host-mcp-server-sdks_functions-bindings-event-iot-output.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: scenario-host-mcp-server-sdks.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/scenario-host-mcp-server-sdks -->

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

<!-- DOCUMENTO FUSIONADO: functions-bindings-event-iot-output.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-iot-output -->

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
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/dedicated-plan -->

# Dedicated hosting plans for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article is about hosting your function app with dedicated resources in an App Service plan, including in an App Service Environment (ASE). For other hosting options, see the [hosting plan article](functions-scale).

An App Service plan defines a set of dedicated compute resources for an app to run. These dedicated compute resources are analogous to the [ server farm](https://wikipedia.org/wiki/Server_farm) in conventional hosting. One or more function apps can be configured to run on the same computing resources (App Service plan) as other App Service apps, such as web apps. The dedicated App Service plans supported for function app hosting include Basic, Standard, Premium, and Isolated SKUs. For details about how the App Service plan works, see the

[Azure App Service plans in-depth overview](../app-service/overview-hosting-plans).

Important

Free and Shared tier App Service plans aren't supported by Azure Functions. For a lower-cost option hosting your function executions, you should instead consider the [Consumption plan](consumption-plan) or the [Flex Consumption plan](flex-consumption-plan), where you are billed based on function executions.

Consider a dedicated App Service plan in the following situations:

- You have existing, underutilized VMs that are already running other App Service instances.
- You want to provide a custom image on which to run your functions.

## Billing

You pay for function apps in an App Service Plan as you would for other App Service resources. This differs from Azure Functions [Consumption plan](consumption-plan) or [Premium plan](functions-premium-plan) hosting, which have consumption-based cost components. You are billed only for the plan, regardless of how many function apps or web apps run in the plan. To learn more, see the [App Service pricing page](https://azure.microsoft.com/pricing/details/app-service/windows/).

## Always On

When you run your app on an App Service plan, you should enable the **Always on** setting so that your function app runs correctly. On an App Service plan, the Functions runtime goes idle after a few minutes of inactivity. The **Always on** setting is available only on an App Service plan. In other plans, the platform activates function apps automatically. If you choose not to enable **Always on**, you can reactivate an idled app in these ways:

- Send a request to an HTTP trigger endpoint or any other endpoint on the app. Even a failed request should wake up your app.
- Access your app in the
[Azure portal](https://portal.azure.com).

Even with **Always on** enabled, the execution timeout for individual functions is controlled by the `functionTimeout`

setting in the [host.json](functions-host-json#functiontimeout) project file.

## Scaling

Using an App Service plan, you can manually scale out by adding more VM instances. You can also enable autoscale, though autoscale will be slower than the elastic scale of the Premium plan. For more information, see [Scale instance count manually or automatically](/en-us/azure/azure-monitor/autoscale/autoscale-get-started?toc=%2fazure%2fapp-service%2ftoc.json). You can also scale up by choosing a different App Service plan. For more information, see [Scale up an app in Azure](../app-service/manage-scale-up).

Note

When running JavaScript (Node.js) functions on an App Service plan, you should choose a plan that has fewer vCPUs. For more information, see [Choose single-core App Service plans](functions-reference-node#choose-single-vcpu-app-service-plans).

## App Service Environments

Running in an App Service Environment (ASE) lets you fully isolate your functions and take advantage of higher numbers of instances than an App Service Plan. To get started, see [Introduction to the App Service Environments](../app-service/environment/overview).

If you just want to run your function app in a virtual network, you can do this using the [Premium plan](functions-premium-plan). To learn more, see [Establish Azure Functions private site access](functions-create-private-site-access).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/supported-languages -->

# Supported languages in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains the levels of support offered for your preferred language when you use Azure Functions. It also describes strategies for creating function apps when you use languages that aren't natively supported.

There are two levels of support:

**Generally available (GA)**- Fully supported and approved for production use.**Preview**- Not yet supported, but expected to reach GA status in the future.

## Languages by runtime version

Make sure to select your preferred development language at the [top of the article](#top).

The following table shows the .NET versions supported by Azure Functions.

The supported version of .NET depends on both your Functions runtime version and your selected execution model.

Your function app code runs in a separate .NET worker process. Use with [supported versions of .NET and .NET Framework](dotnet-isolated-process-guide#supported-versions). For more information, see [Guide for running C# Azure Functions in the isolated worker model](dotnet-isolated-process-guide).

| Supported version | Support level | Expected end-of-support date |
|---|---|---|
| .NET 10 | GA |
|

[November 10, 2026](https://dotnet.microsoft.com/platform/support/policy/dotnet-core#lifecycle)1[November 10, 2026](https://dotnet.microsoft.com/platform/support/policy/dotnet-core#lifecycle)[.NET Framework Support Policy](https://dotnet.microsoft.com/platform/support/policy/dotnet-framework).1 .NET 9 previously had an expected end-of-support date of May 12, 2026. During the .NET 9 service window, the .NET team extended support for STS versions to 24 months, starting with .NET 9. For more information, see [the blog post](https://devblogs.microsoft.com/dotnet/dotnet-sts-releases-supported-for-24-months/).

.NET 6 was previously supported by the isolated worker model but reached the end of official support on [November 12, 2024](https://dotnet.microsoft.com/platform/support/policy/dotnet-core#lifecycle).

.NET 7 was previously supported by the isolated worker model but reached the end of official support on [May 14, 2024](https://dotnet.microsoft.com/platform/support/policy/dotnet-core#lifecycle).

For more information, see [Guide for running C# Azure Functions in the isolated worker model](dotnet-isolated-process-guide).

The following table shows the language versions supported for Java function apps:

| Supported version | Support level | Supported until |
|---|---|---|
Java 25 |
Preview | Pending* |
Java 21 |
GA | See
|

**Java 17**[Release and servicing roadmap](/en-us/java/openjdk/support#release-and-servicing-roadmap).**Java 11**[Release and servicing roadmap](/en-us/java/openjdk/support#release-and-servicing-roadmap).**Java 8**[Temurin support page](https://adoptium.net/support/).*The end-of-support date for Java 25 is determined when general availability (GA) is declared.

For more information on developing and running Java function apps, see [Azure Functions Java developer guide](functions-reference-java).

The following table shows the language versions supported for Node.js function apps:

| Supported version | Support level | Expected end-of-support date |
|---|---|---|
|

[Node.js 22](https://endoflife.date/nodejs)[Node.js 20](https://endoflife.date/nodejs)TypeScript is supported through transpiling to JavaScript. For more information, see [Azure Functions Node.js developer guide](functions-reference-node#supported-versions).

The following table shows the language version supported for PowerShell function apps:

| Supported version | Support level | Expected end-of-support date |
|---|---|---|
|

For more information, see [Azure Functions PowerShell developer guide](functions-reference-powershell).

The following table shows the language versions supported for Python function apps:

| Supported version | Support level | Expected end-of-support date |
|---|---|---|
| Python 3.13 | GA | October 2029 |
| Python 3.12 | GA | October 2028 |
| Python 3.11 | GA | October 2027 |
| Python 3.10 | GA | October 2026 |

For more information, see [Azure Functions Python developer guide](functions-reference-python).

For information about planned changes to language support, see the [Azure roadmap updates](https://techcommunity.microsoft.com/search?q=functions+roadmap).

## Language support details

The following table shows which languages supported by Functions can run on Linux or Windows. It also indicates whether there's support for editing each language in the Azure portal. The language is based on the **Runtime stack** option you select when you [create your function app in the Azure portal](functions-create-function-app-portal#create-a-function-app). This value is the same as the `--worker-runtime`

option that you specify when you use the `func init`

command in Azure Functions Core Tools.

| Language | Runtime stack | Linux | Windows | In-portal editing1 |
|---|---|---|---|---|
|

[C# (in-process model)](functions-dotnet-class-library)2[JavaScript](functions-reference-node?tabs=javascript)[Python](functions-reference-python)1[Java](functions-reference-java)[PowerShell](functions-reference-powershell)[TypeScript](functions-reference-node?tabs=typescript)[Go/Rust/other](functions-custom-handlers)- In-portal editing isn't currently supported when running in the
[Flex Consumption plan](flex-consumption-plan). When in-portal editing isn't available, you must instead[develop your function apps locally](functions-develop-local#local-development-environments). - Although we recommend local development for C# apps, you can use the portal to develop and test C# script functions that use the in-process model. For more information, see
[Create a C# script app](functions-reference-csharp#create-a-c-script-app). - In-portal editing for Python is only supported when running in the Consumption plan.

Important

After 30 September 2028, the option to host your function app on Linux in a Consumption plan is retired. To avoid disruptions, migrate your existing Consumption plan apps that run on Linux to the [Flex Consumption plan](flex-consumption-plan) before that date. Apps running on Windows in a Consumption plan aren't affected by this change.
For more information, see the [Linux Consumption plan retirement notice](https://go.microsoft.com/fwlink/?linkid=2335809).

For more information on operating system and language support, see [Operating system support](functions-scale#operating-systemruntime).

For more information about how to maintain full-support coverage while running your function apps in Azure, see [Azure Functions language stack support policy](language-support-policy).

### Language major version support

Functions provides a guarantee of support for the major versions of supported programming languages. For most languages, there are minor or patch versions released to update a supported major version. Examples of minor or patch versions include Python 3.9.1 and Node 14.17. After new minor versions of supported languages become available, the minor versions used by your function apps are automatically upgraded to these newer minor or patch versions.

Note

Functions can remove the support of older minor versions after a new minor version is available. For this reason, you shouldn't pin your function apps to a specific minor or patch version of a programming language.

## Custom handlers

Custom handlers are lightweight web servers that receive events from the Functions host. You can implement a custom handler in any language that supports HTTP primitives. As a result, you can use custom handlers to create function apps in languages that aren't officially supported. For more information, see [Azure Functions custom handlers](functions-custom-handlers).

## Language extensibility

The Functions runtime is designed to offer [language extensibility](https://github.com/Azure/azure-functions-host/wiki/Language-Extensibility). The JavaScript, Java, and Python languages are built with this extensibility.

## ODBC driver support

The following table lists the support that Open Database Connectivity (ODBC) driver versions offer for Python function apps:

| Driver version | Python version |
|---|---|
| ODBC driver 18 | ≥ Python 3.11 |
| ODBC driver 17 | ≤ Python 3.10 |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-core-tools-reference -->

# Azure Functions Core Tools reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides reference documentation for the Azure Functions Core Tools. With this local runtime and command-line tools, you can develop, manage, and deploy Azure Functions projects from your local computer. To learn more about using Core Tools, see [Work with Azure Functions Core Tools](functions-run-local).

Core Tools commands are organized into the following contexts, each providing a unique set of actions.

| Command context | Description |
|---|---|
`func` |

`func azure`

`func azurecontainerapps`

`func durable`

[Durable Functions](durable/durable-functions-overview).`func extensions`

`func kubernetes`

`func settings`

`func templates`

Before using the commands in this article, you must [install the Core Tools](functions-run-local#install-the-azure-functions-core-tools).

`func init`


Creates a new Functions project in a specific language.

```
func init <PROJECT_FOLDER>
```


When you supply `<PROJECT_FOLDER>`

, the project is created in a new folder with this name. Otherwise, the current folder is used.

`func init`

supports the following options, which don't support version 1.x unless otherwise noted:

| Option | Description |
|---|---|
`--csx` |
Creates .NET functions as C# script, which is the version 1.x behavior. Valid only with `--worker-runtime dotnet` . |
`--docker` |
Creates a Dockerfile for a container using a base image that is based on the chosen `--worker-runtime` . Use this option when you plan to deploy a containerized function app. |
`--docker-only` |
Adds a Dockerfile to an existing project. Prompts for the worker-runtime if not specified or set in local.settings.json. Use this option when you plan to deploy a containerized function app and the project already exists. |
`--force` |
Initialize the project even when there are existing files in the project. This setting overwrites existing files with the same name. Other files in the project folder aren't affected. |
`--language` |
Initializes a language-specific project. Currently supported when `--worker-runtime` set to `node` . Options are `typescript` and `javascript` . You can also use `--worker-runtime javascript` or `--worker-runtime typescript` . |
`--managed-dependencies` |
Installs managed dependencies. Currently, only the PowerShell worker runtime supports this functionality. |
`--model` |
Sets the desired programming model for a target language when more than one model is available. Supported options are `V1` and `V2` for Python and `V3` and `V4` for Node.js. For more information, see the
|
`--source-control` |
Controls whether a git repository is created. By default, a repository isn't created. When `true` , a repository is created. |
`--worker-runtime` |
Sets the language runtime for the project. Supported values are: `csharp` , `dotnet` , `dotnet-isolated` , `javascript` ,`node` (defaults to JavaScript), `powershell` , `python` , and `typescript` . For Java, use
`custom` . When not set, you're prompted to choose your runtime during initialization. |
`--target-framework` |
Sets the target framework for the function app project. Valid only with `--worker-runtime dotnet-isolated` . Supported values are: `net10.0` (preview), `net9.0` , `net8.0` (default), `net6.0` , and `net48` (.NET Framework 4.8). |

Note

When you use either `--docker`

or `--docker-only`

options, Core Tools automatically create the Dockerfile for C#, JavaScript, Python, and PowerShell functions. For Java functions, you must manually create the Dockerfile. For more information, see [Creating containerized function apps](functions-how-to-custom-container#creating-containerized-function-apps).

`func logs`


Gets logs for functions running in a Kubernetes cluster.

```
func logs --platform kubernetes --name <APP_NAME>
```


The `func logs`

action supports the following options:

| Option | Description |
|---|---|
`--platform` |
Hosting platform for the function app. Supported options: `kubernetes` . |
`--name` |
Function app name in Azure. |

For more information, see [Azure Functions on Kubernetes with KEDA](functions-kubernetes-keda).

`func new`


Creates a new function in the current project based on a template.

```
func new
```


When you run `func new`

without the `--template`

option, you're prompted to choose a template. In version 1.x, you must use the `--language`

option to set the language.

The `func new`

action supports the following options:

| Option | Description |
|---|---|
`--authlevel` |
Set the authorization level for an HTTP trigger. Supported values are: `function` , `anonymous` , `admin` . Authorization isn't enforced when running locally. For more information, see
|
`--csx` |
Generates the same C# script (.csx) templates used by version 1.x and in the portal editor. |
, `--language` `-l` |
Reguired only in version 1.x. In all other versions, the language is defined by the `--worker-runtime` value passed to `func init` . |
, `--name` `-n` |
The function name. |
, `--template` `-t` |
Use the `func templates list` command to see the complete list of available templates for each supported language. |

To learn more, see [Create a function](functions-run-local#create-func).

`func pack`


Creates a deployment package that contains your project code in a runnable state. Use this method when you need to manually create a deployment package for your app on your local computer outside of the `func azure functionapp publish`

command. By default, `func pack`

builds your project when required.

```
func pack
```


Run `func pack`

in the directory that contains your `host.json`

project file, which is the root directory of your app. The generated output (.zip) file has the same name as the folder you're packaging. If a .zip file with that name already exists, it's first deleted and then replaced with an updated version.

By default, `func pack`

builds and packages the Functions project in the directory in which it runs. You can run `func pack`

to package a different directory by setting the path to the project root after the command, like `func pack ./myprojectroot`

. When the directory against which `func pack`

runs doesn't contain a `host.json`

file, an error is returned.

By default, `func pack`

builds all projects and installs dependencies for all languages. Use the `--no-build`

and `--skip-install`

options to modify this behavior.

Important

Python app packages built on a Windows computer often have issues being deployed to and running on Linux in Azure Functions. Consider using `--no-build`

with a remote build or `--build-native-deps`

when running `func pack`

for a Python app on Windows.

The `func pack`

action supports these options:

| Option | Description |
|---|---|
`--output` |
Sets a path to the location in which the deployment .zip package file is created. |
`--no-build` |
Project isn't built before packing. For C# apps, use only when you've already generated your binaries. For Node.js apps, both `npm install` and `npm run build` are skipped. You can use this option when requesting a remote build on the package contents. |
`--skip-install` |
Skips running `npm install` when packing Node.js-based function app. Use this option to avoid overwriting custom npm modules. |
`--build-native-deps` |
Installs Python dependencies locally by using an image that matches the environment used in Azure, which requires Docker tools. When enabled, Core Tools starts a Docker container, builds the app inside that container, and creates a .zip file with all dependencies restored in `.python_packages` . Use this option when running on Windows as a way to avoid potential library issues when deployed to Linux in Azure. |

`func run`


*Version 1.x only.*

Use this command to invoke a function directly. This command works like running a function by using the **Test** tab in the Azure portal. This command works only in version 1.x. For later versions, use `func start`

and [call the function endpoint directly](functions-run-local#run-a-local-function).

```
func run
```


The `func run`

command supports the following options:

| Option | Description |
|---|---|
`--content` |
Inline content passed to the function. |
`--debug` |
Attach a debugger to the host process before running the function. |
`--file` |
The file name to use as content. |
`--no-interactive` |
Doesn't prompt for input, which is useful for automation scenarios. |
`--timeout` |
Time to wait (in seconds) until the local Functions host is ready. |

For example, to call an HTTP-triggered function and pass content body, run the following command:

```
func run MyHttpTrigger --content '{\"name\": \"Azure\"}'
```


`func start`


Starts the local runtime host and loads the function project in the current folder.

The specific command depends on the [runtime version](functions-versions).

```
func start
```


`func start`

supports the following options:

| Option | Description |
|---|---|
`--cert` |
The path to a .pfx file that contains a private key. Only supported with `--useHttps` . |
`--cors` |
A comma-separated list of CORS origins, with no spaces. |
`--cors-credentials` |
Allow cross-origin authenticated requests using cookies and the Authentication header. |
`--dotnet-isolated-debug` |
When set to `true` , pauses the .NET worker process until a debugger is attached from the .NET isolated project being debugged. |
`--enable-json-output` |
Emits console logs as JSON, when possible. |
`--enableAuth` |
Enable full authentication handling pipeline, with authorization requirements. |
`--functions` |
A space-separated list of functions to load. |
`--language-worker` |
Arguments to configure the language worker. For example, you can enable debugging for language worker by providing
|

`--no-build`

`false`

.`--password`

`--cert`

.`--port`

`--timeout`

`--useHttps`

`https://localhost:{port}`

rather than to `http://localhost:{port}`

. By default, this option creates a trusted certificate on your computer.With the project running, you can [verify individual function endpoints](functions-run-local#run-a-local-function).

`func azure functionapp`

global options

All `func azure functionapp`

commands support these options:

| Option | Description |
|---|---|
`--slot` |
Target a specific named
|

`--access-token`

`--access-token-stdin `

[.](/en-us/cli/azure/account#az-account-get-access-token)`az account get-access-token`

`--management-url`

`https://management.azure.com`

. Use this option when your function app runs in a sovereign cloud.`--subscription`

`func azure functionapp fetch-app-settings`


Gets settings from a specific function app.

```
func azure functionapp fetch-app-settings <APP_NAME>
```


For more information, see [Download application settings](functions-run-local#download-application-settings).

The command downloads settings into the `local.settings.json`

file for the project. The command masks values on the screen for security. You can protect settings in the `local.settings.json`

file by [enabling local encryption](functions-run-local#encrypt-the-local-settings-file).

`func azure functionapp list-functions`


Returns a list of the functions in the specified function app.

```
func azure functionapp list-functions <APP_NAME>
```


| Option | Description |
|---|---|
`--show-keys` |
The function endpoint URLs that are returned include function-level access key values. |

`func azure functionapp logstream`


Connects the local command prompt to streaming logs for the function app in Azure.

```
func azure functionapp logstream <APP_NAME>
```


The default timeout for the connection is two hours. You can change the timeout by adding an app setting named [SCM_LOGSTREAM_TIMEOUT](functions-app-settings#scm_logstream_timeout), with a timeout value in seconds. This feature isn't yet supported for Linux in a [Flex Consumption](flex-consumption-plan) or [Consumption](consumption-plan) plan. For these apps, use the `--browser`

option to view logs in the portal.

The `deploy`

action supports the following options:

| Option | Description |
|---|---|
`--browser` |
Open Azure Application Insights Live Stream for the function app in the default browser. |

For more information, see [Enable streaming execution logs in Azure Functions](streaming-logs).

`func azure functionapp publish`


Deploys a Functions project to an existing function app resource in Azure.

```
func azure functionapp publish <APP_NAME>
```


For more information, see [Deploy project files](functions-run-local#project-file-deployment).

The following publish options apply, based on version:

| Option | Description |
|---|---|
`--additional-packages` |
List of packages to install when building native dependencies. For example: `python3-dev libevent-dev` . |
, `--build` `-b` |
Performs build action when deploying to a Linux function app. Accepts: `remote` and `local` . |
`--build-native-deps` |
Skips generating the `.wheels` folder when publishing Python function apps. |
`--csx` |
Publish a C# script (.csx) project. |
`--dotnet-cli-params` |
When publishing compiled C# (.csproj) functions, the core tools calls `dotnet build --output bin/publish` . Any parameters passed to this are appended to the command line. |
`--force` |
Ignore prepublishing verification in certain scenarios. |
`--list-ignored-files` |
Displays a list of files that are ignored during publishing, which is based on the `.funcignore` file. |
`--list-included-files` |
Displays a list of files that are published, which is based on the `.funcignore` file. |
`--no-build` |
Project isn't built during publishing. For Python, `pip install` isn't performed. |
`--nozip` |
Turns the default `Run-From-Package` mode off. |
`--overwrite-settings -y` |
Suppress the prompt to overwrite app settings when `--publish-local-settings -i` is used. |
`--publish-local-settings -i` |
Publish settings in local.settings.json to Azure, prompting to overwrite if the setting already exists. If you're using a
|

**,**`--publish-settings-only`

`-o`

`func azure storage fetch-connection-string`


Gets the connection string for the specified Azure Storage account.

```
func azure storage fetch-connection-string <STORAGE_ACCOUNT_NAME>
```


For more information, see [Download a storage connection string](functions-run-local#download-a-storage-connection-string).

`func azurecontainerapps deploy`


Deploys a containerized function app to an Azure Container Apps environment. Both the storage account used by the function app and the environment must already exist. For more information, see [Azure Container Apps hosting of Azure Functions](functions-container-apps-hosting).

```
func azurecontainerapps deploy --name <APP_NAME> --environment <ENVIRONMENT_NAME> --storage-account <STORAGE_CONNECTION> --resource-group <RESOURCE_GROUP> --image-name <IMAGE_NAME> --registry-server <REGISTRY_SERVER> --registry-username <USERNAME> --registry-password <PASSWORD>
```


The following deployment options apply:

| Option | Description |
|---|---|
`--environment` |
The name of an existing Container Apps environment. |
`--image-build` |
When set to `true` , skips the local Docker build. |
`--image-name` |
The image name of an existing container in a container registry. The image name includes the tag name. |
`--location ` |
Region for the deployment. Ideally, this region is the same region as the environment and storage account resources. |
`--name` |
The name used for the function app deployment in the Container Apps environment. This same name is also used when managing the function app in the portal. The name should be unique in the environment. |
`--registry` |
When set, a Docker build runs and the image is pushed to the registry set in `--registry` . You can't use `--registry` with `--image-name` . For Docker Hub, also use `--registry-username` . |
`--registry-password` |
The password or token used to retrieve the image from a private registry. |
`--registry-username` |
The username used to retrieve the image from a private registry. |
`--resource-group` |
The resource group in which to create the functions-related resources. |
`--storage-account` |
The connection string for the storage account to be used by the function app. |
`--worker-runtime` |
Sets the runtime language of the function app. This parameter is only used with `--image-name` and `--image-build` . Otherwise, the language is determined during the local build. Supported values are: `dotnet` , `dotnetIsolated` , `node` , `python` , `powershell` , and `custom` (for customer handlers). |

Important

Storage connection strings and other service credentials are important secrets. Make sure to securely store any script files that use `func azurecontainerapps deploy`

and don't store them in any publicly accessible source control.

`func deploy`


The `func deploy`

command is deprecated. Instead, use [ func kubernetes deploy](#func-kubernetes-deploy).

`func durable delete-task-hub`


Deletes all storage artifacts in the Durable Functions task hub.

```
func durable delete-task-hub
```


The `delete-task-hub`

action supports the following options:

| Option | Description |
|---|---|
`--connection-string-setting` |
Optional name of the setting containing the storage connection string to use. |
`--task-hub-name` |
Optional name of the Durable Task Hub to use. |

For more information, see the [Durable Functions documentation](durable/durable-functions-instance-management#delete-a-task-hub).

`func durable get-history`


Returns the history of the specified orchestration instance.

```
func durable get-history --id <INSTANCE_ID>
```


The `get-history`

action supports the following options:

| Option | Description |
|---|---|
`--id` |
Specifies the ID of an orchestration instance (required). |
`--connection-string-setting` |
Optional name of the setting containing the storage connection string to use. |
`--task-hub-name` |
Optional name of the Durable Task Hub to use. |

For more information, see the [Durable Functions documentation](durable/durable-functions-instance-management#azure-functions-core-tools-1).

`func durable get-instances`


Returns the status of all orchestration instances. Supports paging by using the `top`

parameter.

```
func durable get-instances
```


The `get-instances`

action supports the following options:

| Option | Description |
|---|---|
`--continuation-token` |
Optional token that indicates a specific page or section of the requests to return. |
`--connection-string-setting` |
Optional name of the app setting that contains the storage connection string to use. |
`--created-after` |
Optionally, get the instances created after this date and time (UTC). All ISO 8601 formatted datetimes are accepted. |
`--created-before` |
Optionally, get the instances created before a specific date and time (UTC). All ISO 8601 formatted datetimes are accepted. |
`--runtime-status` |
Optionally, get the instances whose status match a specific status, including `running` , `completed` , and `failed` . You can provide one or more space-separated statuses. |
`--top` |
Optionally limit the number of records returned in a given request. |
`--task-hub-name` |
Optional name of the Durable Functions task hub to use. |

For more information, see the [Durable Functions documentation](durable/durable-functions-instance-management#azure-functions-core-tools-2).

`func durable get-runtime-status`


Returns the status of the specified orchestration instance.

```
func durable get-runtime-status --id <INSTANCE_ID>
```


The `get-runtime-status`

action supports the following options:

| Option | Description |
|---|---|
`--connection-string-setting` |
Optional name of the setting containing the storage connection string to use. |
`--id` |
Specifies the ID of an orchestration instance (required). |
`--show-input` |
When set, the response contains the input of the function. |
`--show-output` |
When set, the response contains the execution history. |
`--task-hub-name` |
Optional name of the Durable Functions task hub to use. |

For more information, see the [Durable Functions documentation](durable/durable-functions-instance-management#azure-functions-core-tools-1).

`func durable purge-history`


Purge orchestration instance state, history, and blob storage for orchestrations older than the specified threshold.

```
func durable purge-history
```


The `purge-history`

action supports the following options:

| Option | Description |
|---|---|
`--connection-string-setting` |
Optional name of the setting containing the storage connection string to use. |
`--created-after` |
Optionally delete the history of instances created after this date/time (UTC). All ISO 8601 formatted datetime values are accepted. |
`--created-before` |
Optionally delete the history of instances created before this date/time (UTC). All ISO 8601 formatted datetime values are accepted. |
`--runtime-status` |
Optionally delete the history of instances whose status match a specific status, including `completed` , `terminated` , `canceled` , and `failed` . You can provide one or more space-separated statuses. If you don't include `--runtime-status` , instance history is deleted regardless of status. |
`--task-hub-name` |
Optional name of the Durable Functions task hub to use. |

To learn more, see the [Durable Functions documentation](durable/durable-functions-instance-management#azure-functions-core-tools-7).

`func durable raise-event`


Raises an event to the specified orchestration instance.

```
func durable raise-event --event-name <EVENT_NAME> --event-data <DATA>
```


The `raise-event`

action supports the following options:

| Option | Description |
|---|---|
`--connection-string-setting` |
Optional name of the setting containing the storage connection string to use. |
`--event-data` |
Data to pass to the event, either inline or from a JSON file (required). For files, prefix the path to the file with an ampersand (`@` ), such as `@path/to/file.json` . |
`--event-name` |
Name of the event to raise (required). |
`--id` |
Specifies the ID of an orchestration instance (required). |
`--task-hub-name` |
Optional name of the Durable Functions task hub to use. |

For more information, see the [Durable Functions documentation](durable/durable-functions-instance-management#azure-functions-core-tools-5).

`func durable rewind`


Rewinds the specified orchestration instance.

```
func durable rewind --id <INSTANCE_ID> --reason <REASON>
```


The `rewind`

action supports the following options:

| Option | Description |
|---|---|
`--connection-string-setting` |
Optional name of the setting containing the storage connection string to use. |
`--id` |
Specifies the ID of an orchestration instance (required). |
`--reason` |
Reason for rewinding the orchestration (required). |
`--task-hub-name` |
Optional name of the Durable Functions task hub to use. |

For more information, see the [Durable Functions documentation](durable/durable-functions-instance-management#azure-functions-core-tools-6).

`func durable start-new`


Starts a new instance of the specified orchestrator function.

```
func durable start-new --id <INSTANCE_ID> --function-name <FUNCTION_NAME> --input <INPUT>
```


The `start-new`

action supports the following options:

| Option | Description |
|---|---|
`--connection-string-setting` |
Optional name of the setting containing the storage connection string to use. |
`--function-name` |
Name of the orchestrator function to start (required). |
`--id` |
Specifies the ID of an orchestration instance (required). |
`--input` |
Input to the orchestrator function, either inline or from a JSON file (required). For files, prefix the path to the file with an ampersand (`@` ), such as `@path/to/file.json` . |
`--task-hub-name` |
Optional name of the Durable Functions task hub to use. |

For more information, see the [Durable Functions documentation](durable/durable-functions-instance-management#azure-functions-core-tools).

`func durable terminate`


Stops the specified orchestration instance.

```
func durable terminate --id <INSTANCE_ID> --reason <REASON>
```


The `terminate`

action supports the following options:

| Option | Description |
|---|---|
`--connection-string-setting` |
Optional name of the setting containing the storage connection string to use. |
`--id` |
Specifies the ID of an orchestration instance (required). |
`--reason` |
Reason for stopping the orchestration (required). |
`--task-hub-name` |
Optional name of the Durable Functions task hub to use. |

For more information, see the [Durable Functions documentation](durable/durable-functions-instance-management#azure-functions-core-tools-4).

`func extensions install`


Manually installs Functions extensions in a non-.NET project or in a C# script project.

```
func extensions install --package Microsoft.Azure.WebJobs.Extensions.<EXTENSION> --version <VERSION>
```


The `install`

action supports the following options:

| Option | Description |
|---|---|
`--configPath` |
Path of the directory containing extensions.csproj file. |
`--csx` |
Supports C# scripting (.csx) projects. |
`--force` |
Update the versions of existing extensions. |
`--output` |
Output path for the extensions. |
`--package` |
Identifier for a specific extension package. When not specified, all referenced extensions are installed, as with `func extensions sync` . |
`--source` |
NuGet feed source when not using NuGet.org. |
`--version` |
Extension package version. |

The following example installs version 5.0.1 of the Event Hubs extension in the local project:

```
func extensions install --package Microsoft.Azure.WebJobs.Extensions.EventHubs --version 5.0.1
```


The following considerations apply when using `func extensions install`

:

For compiled C# projects (both in-process and isolated worker process), instead use standard NuGet package installation methods, such as

`dotnet add package`

.To manually install extensions by using Core Tools, you must have the

[.NET SDK](https://dotnet.microsoft.com/download)installed.When possible, use

[extension bundles](extension-bundles). The following are some reasons why you might need to install extensions manually:- You need to access a specific version of an extension that's not available in a bundle.
- You need to access a custom extension that's not available in a bundle.
- You need to access a specific combination of extensions that's not available in a single bundle.

Before you can manually install extensions, you must first remove the

object from the host.json file that defines the bundle. No action is taken when an extension bundle is already set in your`extensionBundle`

[host.json file](functions-host-json#extensionbundle).The first time you explicitly install an extension, a .NET project file named extensions.csproj is added to the root of your app project. This file defines the set of NuGet packages required by your functions. While you can work with the

[NuGet package references](/en-us/nuget/consume-packages/package-references-in-project-files)in this file, Core Tools lets you install extensions without having to manually edit this C# project file.

`func extensions sync`


Installs all extensions you add to the function app.

The `sync`

action supports the following options:

| Option | Description |
|---|---|
`--configPath` |
Path of the directory containing extensions.csproj file. |
`--csx` |
Supports C# scripting (.csx) projects. |
`--output` |
Output path for the extensions. |

Regenerates a missing extensions.csproj file. If you define an extension bundle in your host.json file, no action is taken.

`func kubernetes deploy`


Deploys a Functions project as a custom Docker container to a Kubernetes cluster.

```
func kubernetes deploy
```


This command builds your project as a custom container and publishes it to a Kubernetes cluster. Custom containers must have a Dockerfile. To create an app with a Dockerfile, use the `--dockerfile`

option with the [ func init](#func-init) command.

The following Kubernetes deployment options are available:

| Option | Description |
|---|---|
`--dry-run` |
Optionally displays the deployment template, without execution. |
`--config-map-name` |
Optional name of an existing config map with
`--use-config-map` . The default behavior is to create settings based on the `Values` object in the
|

`--cooldown-period`

`--ignore-errors`

`--image-name`

`--keda-version`

`v1`

and `v2`

(default).`--keys-secret-name`

[access keys](function-keys-how-to).`--max-replicas`

`--min-replicas`

`--mount-funckeys-as-containervolume`

[access keys](function-keys-how-to)as a container volume.`--name`

`--namespace`

`--no-docker`

`--registry`

`--registry`

with `--image-name`

. For Docker, use your username.`--polling-interval`

`--pull-secret`

`--secret-name`

[function app settings](functions-how-to-use-azure-function-app-settings#settings)to use in the deployment. The default behavior is to create settings based on the`Values`

object in the [local.settings.json file](functions-develop-local#local-settings-file).`--show-service-fqdn`

`--service-type`

`ClusterIP`

, `NodePort`

, and `LoadBalancer`

(default).`--use-config-map`

`ConfigMap`

object (v1) instead of a `Secret`

object (v1) to configure [function app settings](functions-how-to-use-azure-function-app-settings#settings). The map name is set using`--config-map-name`

.Core Tools uses the local Docker CLI to build and publish the image. Make sure your Docker is already installed locally. Run the `docker login`

command to connect to your account.

Azure Functions supports hosting your containerized functions either in Azure Container Apps or in Azure Functions. Running your containers directly in a Kubernetes cluster or in Azure Kubernetes Service (AKS) isn't officially supported by Azure Functions. To learn more, see [Linux container support in Azure Functions](container-concepts).

`func kubernetes install`


Installs KEDA in a Kubernetes cluster.

```
func kubernetes install
```


Installs KEDA to the cluster defined in the kubectl config file.

The `install`

action supports the following options:

| Option | Description |
|---|---|
`--dry-run` |
Displays the deployment template, without execution. |
`--keda-version` |
Sets the version of KEDA to install. Valid options are: `v1` and `v2` (default). |
`--namespace` |
Supports installation to a specific Kubernetes namespace. When not set, the default namespace is used. |

For more information, see [Managing KEDA and functions in Kubernetes](functions-kubernetes-keda#managing-keda-and-functions-in-kubernetes).

`func kubernetes remove`


Removes KEDA from the Kubernetes cluster defined in the kubectl config file.

```
func kubernetes remove
```


Removes KEDA from the cluster defined in the kubectl config file.

The `remove`

action supports the following options:

| Option | Description |
|---|---|
`--namespace` |
Supports uninstall from a specific Kubernetes namespace. When not set, the default namespace is used. |

To learn more, see [Uninstalling KEDA from Kubernetes](functions-kubernetes-keda#uninstalling-keda-from-kubernetes).

`func settings add`


Adds a new setting to the `Values`

collection in the [local.settings.json file](functions-develop-local#local-settings-file).

```
func settings add <SETTING_NAME> <VALUE>
```


Replace `<SETTING_NAME>`

with the name of the app setting and `<VALUE>`

with the value of the setting.

The `add`

action supports the following option:

| Option | Description |
|---|---|
`--connectionString` |
Adds the name-value pair to the `ConnectionStrings` collection instead of the `Values` collection. Only use the `ConnectionStrings` collection when required by certain frameworks. To learn more, see
|

`func settings decrypt`


Decrypts previously encrypted values in the `Values`

collection in the [local.settings.json file](functions-develop-local#local-settings-file).

```
func settings decrypt
```


The command also decrypts connection string values in the `ConnectionStrings`

collection. In local.settings.json, the command sets `IsEncrypted`

to `false`

. Encrypt local settings to reduce the risk of leaking valuable information from local.settings.json. In Azure, application settings are always stored encrypted.

`func settings delete`


Removes an existing setting from the `Values`

collection in the [local.settings.json file](functions-develop-local#local-settings-file).

```
func settings delete <SETTING_NAME>
```


Replace `<SETTING_NAME>`

with the name of the app setting and `<VALUE>`

with the value of the setting.

The `delete`

action supports the following option:

| Option | Description |
|---|---|
`--connectionString` |
Removes the name-value pair from the `ConnectionStrings` collection instead of from the `Values` collection. |

`func settings encrypt`


Encrypts the values of individual items in the `Values`

collection in the [local.settings.json file](functions-develop-local#local-settings-file).

```
func settings encrypt
```


The command also encrypts connection string values in the `ConnectionStrings`

collection. In local.settings.json, the command sets `IsEncrypted`

to `true`

, which specifies that the local runtime decrypts settings before using them. Encrypt local settings to reduce the risk of leaking valuable information from local.settings.json. In Azure, application settings are always stored encrypted.

`func settings list`


Outputs a list of settings in the `Values`

collection in the [local.settings.json file](functions-develop-local#local-settings-file).

```
func settings list
```


Connection strings from the `ConnectionStrings`

collection are also output. By default, values are masked for security. Use the `--showValue`

option to display the actual value.

The `list`

action supports the following option:

| Option | Description |
|---|---|
`--showValue` |
Shows the actual unmasked values in the output. |

`func templates list`


Lists the available function (trigger) templates.

The `list`

action supports the following option:

| Option | Description |
|---|---|
`--language` |
Language for which to filter returned templates. Default is to return all languages. |
