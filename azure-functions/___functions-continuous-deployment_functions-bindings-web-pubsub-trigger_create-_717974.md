---
merged_at: 2026-01-25T15:41:11.623554
merged_files: 2
---

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
