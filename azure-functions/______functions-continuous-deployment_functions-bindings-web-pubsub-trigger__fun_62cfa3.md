---
merged_at: 2026-02-02T16:24:03.405996
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
<!-- Source: N/A -->

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
<!-- Source: N/A -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/dotnet-isolated-process-guide -->

# Guide for running C# Azure Functions in the isolated worker model

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article introduces working with Azure Functions in .NET using the isolated worker model. This model lets your project target versions of .NET independently of other runtime components. For information about specific .NET versions supported, see [supported version](#supported-versions).

Use the following links to get started right away building .NET isolated worker model functions.

| Getting started | Concepts | Samples |
|---|---|---|

To learn about deploying an isolated worker model project to Azure, see [Deploy to Azure Functions](#deploy-to-azure-functions).

## Benefits of the isolated worker model

You can run your .NET class library functions in two modes: either [in the same process](functions-dotnet-class-library) as the Functions host runtime (*in-process*) or in an isolated worker process. When your .NET functions run in an isolated worker process, you can take advantage of the following benefits:

**Fewer conflicts:**Because your functions run in a separate process, assemblies used in your app don't conflict with different versions of the same assemblies used by the host process.**Full control of the process**: You control the start-up of the app, which means that you can manage the configurations used and the middleware started.**Standard dependency injection:**Because you have full control of the process, you can use current .NET behaviors for dependency injection and incorporating middleware into your function app.**.NET version flexibility:**Running outside of the host process means that your functions can run on versions of .NET not natively supported by the Functions runtime, including the .NET Framework.

If you have an existing C# function app that runs in-process, you need to migrate your app to take advantage of these benefits. For more information, see [Migrate .NET apps from the in-process model to the isolated worker model](migrate-dotnet-to-isolated-model).

For a comprehensive comparison between the two modes, see [Differences between in-process and isolate worker process .NET Azure Functions](dotnet-isolated-in-process-differences).

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

## Project structure

A .NET project for Azure Functions that uses the isolated worker model is basically a .NET console app project that targets a supported .NET runtime. The following files are the basic files required in any .NET isolated project:

- C# project file (.csproj) that defines the project and dependencies.
- Program.cs file that's the entry point for the app.
- Any code files
[defining your functions](#methods-recognized-as-functions). [host.json](functions-host-json)file that defines configuration shared by functions in your project.[local.settings.json](functions-develop-local#local-settings-file)file that defines environment variables used by your project when run locally on your machine.

For complete examples, see the [.NET 8 sample project](https://github.com/Azure/azure-functions-dotnet-worker/tree/main/samples/FunctionApp) and the [.NET Framework 4.8 sample project](https://github.com/Azure/azure-functions-dotnet-worker/tree/main/samples/NetFxWorker).

## Package references

A .NET project for Azure Functions that uses the isolated worker model uses a unique set of packages for both core functionality and binding extensions.

### Core packages

To run your .NET functions in an isolated worker process, you need the following packages:

The minimum versions of these packages depend on your target .NET version:

| .NET version | `Microsoft.Azure.Functions.Worker` |
`Microsoft.Azure.Functions.Worker.Sdk` |
|---|---|---|
| .NET 10 | 2.50.0 or later | 2.0.5 or later |
| .NET 9 | 2.0.0 or later | 2.0.0 or later |
| .NET 8 | 1.16.0 or later | 1.11.0 or later |
| .NET Framework | 1.16.0 or later | 1.11.0 or later |

#### Version 2.x

The 2.x versions of the core packages change the supported frameworks and bring in support for new .NET APIs from these later versions. When updating to the 2.x versions, note the following changes:

- Starting with version 2.0.0 of
[Microsoft.Azure.Functions.Worker.Sdk](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Sdk/):- The SDK includes default configurations for
[SDK container builds](/en-us/dotnet/core/docker/publish-as-container). - The SDK includes support for
when the`dotnet run`

[Azure Functions Core Tools](functions-develop-local)is installed. On Windows, install the Core Tools through a mechanism other than NPM.

- The SDK includes default configurations for
- Starting with version 2.0.0 of
[Microsoft.Azure.Functions.Worker](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker/):- This version adds support for
`IHostApplicationBuilder`

. Some examples in this guide include tabs to show alternatives using`IHostApplicationBuilder`

. These examples require the 2.x versions. - Service provider scope validation is included by default if run in a development environment. This behavior matches ASP.NET Core.
- The
`EnableUserCodeException`

option is enabled by default. The property is now marked as obsolete. - The
`IncludeEmptyEntriesInMessagePayload`

option is enabled by default. With this option enabled, trigger payloads that represent collections always include empty entries. For example, if a message is sent without a body, an empty entry is still present in`string[]`

for the trigger data. The inclusion of empty entries facilitates cross-referencing with metadata arrays which the function may also reference. You can disable this behavior by setting`IncludeEmptyEntriesInMessagePayload`

to`false`

in the`WorkerOptions`

service configuration. - The
`ILoggerExtensions`

class is renamed to`FunctionsLoggerExtensions`

. The rename prevents an ambiguous call error when using`LogMetric()`

on an`ILogger`

instance. - For apps that use
`HttpResponseData`

, the`WriteAsJsonAsync()`

method no longer sets the status code to`200 OK`

. In 1.x, this behavior overrode other error codes that you set.

- This version adds support for
- The 2.x versions drop .NET 5 TFM support.

### Extension packages

Because .NET isolated worker process functions use different binding types, they require a unique set of binding extension packages.

You find these extension packages under [Microsoft.Azure.Functions.Worker.Extensions](https://www.nuget.org/packages?q=Microsoft.Azure.Functions.Worker.Extensions).

## Start-up and configuration

When you use the isolated worker model, you have access to the start-up of your function app, which is usually in `Program.cs`

. You're responsible for creating and starting your own host instance. As such, you also have direct access to the configuration pipeline for your app. With .NET Functions isolated worker process, you can much more easily add configurations, inject dependencies, and run your own middleware.

*To use IHostApplicationBuilder, your app must use version 2.x or later of the core packages.*

The following code shows an example of an [IHostApplicationBuilder](/en-us/dotnet/api/microsoft.extensions.hosting.ihostapplicationbuilder) pipeline:

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Builder;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
var builder = FunctionsApplication.CreateBuilder(args);
builder.Services
.AddApplicationInsightsTelemetryWorkerService()
.ConfigureFunctionsApplicationInsights();
builder.Logging.Services.Configure<LoggerFilterOptions>(options =>
{
// The Application Insights SDK adds a default logging filter that instructs ILogger to capture only Warning and more severe logs. Application Insights requires an explicit override.
// Log levels can also be configured using appsettings.json. For more information, see https://learn.microsoft.com/azure/azure-monitor/app/worker-service#ilogger-logs
LoggerFilterRule defaultRule = options.Rules.FirstOrDefault(rule => rule.ProviderName
== "Microsoft.Extensions.Logging.ApplicationInsights.ApplicationInsightsLoggerProvider");
if (defaultRule is not null)
{
options.Rules.Remove(defaultRule);
}
});
var host = builder.Build();
```


Before calling `Build()`

on the `IHostApplicationBuilder`

, you should:

- If you want to use
[ASP.NET Core integration](#aspnet-core-integration), call`builder.ConfigureFunctionsWebApplication()`

. - If you're writing your application using F#, you might need to register some binding extensions. See the setup documentation for the
[Blobs extension](functions-bindings-storage-blob#install-extension), the[Tables extension](functions-bindings-storage-table#install-extension), and the[Cosmos DB extension](functions-bindings-cosmosdb-v2#install-extension)when you plan to use these extensions in an F# app. - Configure any services or app configuration your project requires. See
[Configuration](#configuration)for details. - If you're planning to use Application Insights, you need to call
`AddApplicationInsightsTelemetryWorkerService()`

and`ConfigureFunctionsApplicationInsights()`

against the builder's`Services`

property. See[Application Insights](#application-insights)for details.

If your project targets .NET Framework 4.8, you also need to add `FunctionsDebugger.Enable();`

before creating the HostBuilder. It should be the first line of your `Main()`

method. For more information, see [Debugging when targeting .NET Framework](#debugging-when-targeting-net-framework).

The [IHostApplicationBuilder](/en-us/dotnet/api/microsoft.extensions.hosting.ihostapplicationbuilder) is used to build and return a fully initialized [ IHost](/en-us/dotnet/api/microsoft.extensions.hosting.ihost) instance, which you run asynchronously to start your function app.

```
await host.RunAsync();
```


### Configuration

The type of builder you use determines how you configure the application.

Use the `FunctionsApplication.CreateBuilder()`

method to add the settings required for the function app to run. The method includes the following functionality:

- Default set of converters.
- Set the default
[JsonSerializerOptions](/en-us/dotnet/api/system.text.json.jsonserializeroptions)to ignore casing on property names. - Integrate with Azure Functions logging.
- Output binding middleware and features.
- Function execution middleware.
- Default gRPC support.
- Apply other defaults from
[Host.CreateDefaultBuilder()](/en-us/dotnet/api/microsoft.extensions.hosting.host.createdefaultbuilder).

You have access to the builder pipeline, so you can set any app-specific configurations during initialization. You can call extension methods on the builder's `Configuration`

property to add any configuration sources required by your code. For more information about app configuration, see [Configuration in ASP.NET Core](/en-us/aspnet/core/fundamentals/configuration).

These configurations only apply to the worker code you author. They don't directly influence the configuration of the Functions host or triggers and bindings. To make changes to the functions host or trigger and binding configuration, use the [host.json file](functions-host-json).

Note

Custom configuration sources can't be used for configuration of triggers and bindings. Trigger and binding configuration must be available to the Functions platform, and not just your application code. You can provide this configuration through the [application settings](../app-service/configure-common#configure-app-settings), [Key Vault references](../app-service/app-service-key-vault-references?toc=/azure/azure-functions/toc.json), or [App Configuration references](../app-service/app-service-configuration-references?toc=/azure/azure-functions/toc.json) features.

### Dependency injection

The isolated worker model uses standard .NET mechanisms for injecting services.

When you use an `IHostApplicationBuilder`

, use its `Services`

property to access the [IServiceCollection](/en-us/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection). The following example injects a singleton service dependency:

```
builder.Services.AddSingleton<IHttpResponderService, DefaultHttpResponderService>();
```


This code requires `using Microsoft.Extensions.DependencyInjection;`

. To learn more, see [Dependency injection in ASP.NET Core](/en-us/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-5.0&preserve-view=true).

#### Register Azure clients

Use dependency injection to interact with other Azure services. You can inject clients from the [Azure SDK for .NET](/en-us/dotnet/azure/sdk/azure-sdk-for-dotnet) by using the [Microsoft.Extensions.Azure](https://www.nuget.org/packages/Microsoft.Extensions.Azure) package. After installing the package, [register the clients](/en-us/dotnet/azure/sdk/dependency-injection#register-clients) by calling `AddAzureClients()`

on the service collection in `Program.cs`

. The following example configures a [named client](/en-us/dotnet/azure/sdk/dependency-injection#configure-multiple-service-clients-with-different-names) for Azure Blobs:

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Builder;
using Microsoft.Extensions.Azure;
using Microsoft.Extensions.Hosting;
var builder = FunctionsApplication.CreateBuilder(args);
builder.Services
.AddAzureClients(clientBuilder =>
{
clientBuilder.AddBlobServiceClient(builder.Configuration.GetSection("MyStorageConnection"))
.WithName("copierOutputBlob");
});
builder.Build().Run();
```


The following example shows how you can use this registration and [SDK types](#sdk-types) to copy blob contents as a stream from one container to another by using an injected client:

```
using Microsoft.Extensions.Azure;
using Microsoft.Extensions.Logging;
namespace MyFunctionApp
{
public class BlobCopier
{
private readonly ILogger<BlobCopier> _logger;
private readonly BlobContainerClient _copyContainerClient;
public BlobCopier(ILogger<BlobCopier> logger, IAzureClientFactory<BlobServiceClient> blobClientFactory)
{
_logger = logger;
_copyContainerClient = blobClientFactory.CreateClient("copierOutputBlob").GetBlobContainerClient("samples-workitems-copy");
_copyContainerClient.CreateIfNotExists();
}
[Function("BlobCopier")]
public async Task Run([BlobTrigger("samples-workitems/{name}", Connection = "MyStorageConnection")] Stream myBlob, string name)
{
await _copyContainerClient.UploadBlobAsync(name, myBlob);
_logger.LogInformation($"Blob {name} copied!");
}
}
}
```


The [ ILogger<T>](/en-us/dotnet/api/microsoft.extensions.logging.ilogger-1) in this example is also obtained through dependency injection, so it's registered automatically. To learn more about configuration options for logging, see

[Logging](#logging).

Tip

The example uses a literal string for the name of the client in both `Program.cs`

and the function. Instead, consider using a shared constant string defined on the function class. For example, you could add `public const string CopyStorageClientName = nameof(_copyContainerClient);`

and then reference `BlobCopier.CopyStorageClientName`

in both locations. You could similarly define the configuration section name with the function rather than in `Program.cs`

.

### Middleware

The isolated worker model also supports middleware registration, again by using a model similar to what exists in ASP.NET. This model gives you the ability to inject logic into the invocation pipeline, and before and after functions execute.

The [ConfigureFunctionsWorkerDefaults](/en-us/dotnet/api/microsoft.extensions.hosting.workerhostbuilderextensions.configurefunctionsworkerdefaults?view=azure-dotnet&preserve-view=true#Microsoft_Extensions_Hosting_WorkerHostBuilderExtensions_ConfigureFunctionsWorkerDefaults_Microsoft_Extensions_Hosting_IHostBuilder_) extension method has an overload that lets you register your own middleware, as you see in the following example.

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Builder;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
var builder = FunctionsApplication.CreateBuilder(args);
// Register our custom middlewares with the worker
builder
.UseMiddleware<ExceptionHandlingMiddleware>()
.UseMiddleware<MyCustomMiddleware>()
.UseWhen<StampHttpHeaderMiddleware>((context) =>
{
// We want to use this middleware only for http trigger invocations.
return context.FunctionDefinition.InputBindings.Values
.First(a => a.Type.EndsWith("Trigger")).Type == "httpTrigger";
});
builder.Build().Run();
```


The `UseWhen`

extension method registers a middleware that executes conditionally. You must pass a predicate that returns a boolean value to this method. The middleware participates in the invocation processing pipeline when the predicate returns `true`

.

The following extension methods on [FunctionContext](/en-us/dotnet/api/microsoft.azure.functions.worker.functioncontext?view=azure-dotnet&preserve-view=true) make it easier to work with middleware in the isolated model.

| Method | Description |
|---|---|
`GetHttpRequestDataAsync` |
Gets the `HttpRequestData` instance when called by an HTTP trigger. This method returns an instance of `ValueTask<HttpRequestData?>` , which is useful when you want to read message data, such as request headers and cookies. |
`GetHttpResponseData` |
Gets the `HttpResponseData` instance when called by an HTTP trigger. |
`GetInvocationResult` |
Gets an instance of `InvocationResult` , which represents the result of the current function execution. Use the `Value` property to get or set the value as needed. |
`GetOutputBindings` |
Gets the output binding entries for the current function execution. Each entry in the result of this method is of type `OutputBindingData` . You can use the `Value` property to get or set the value as needed. |
`BindInputAsync` |
Binds an input binding item for the requested `BindingMetadata` instance. For example, use this method when you have a function with a `BlobInput` input binding that needs to be used by your middleware. |

This example shows a middleware implementation that reads the `HttpRequestData`

instance and updates the `HttpResponseData`

instance during function execution:

```
internal sealed class StampHttpHeaderMiddleware : IFunctionsWorkerMiddleware
{
public async Task Invoke(FunctionContext context, FunctionExecutionDelegate next)
{
var requestData = await context.GetHttpRequestDataAsync();
string correlationId;
if (requestData!.Headers.TryGetValues("x-correlationId", out var values))
{
correlationId = values.First();
}
else
{
correlationId = Guid.NewGuid().ToString();
}
await next(context);
context.GetHttpResponseData()?.Headers.Add("x-correlationId", correlationId);
}
}
```


This middleware checks for the presence of a specific request header (`x-correlationId`

). When the header is present, the middleware uses the header value to stamp a response header. Otherwise, it generates a new GUID value and uses that value for stamping the response header.

Tip

The pattern shown earlier of setting response headers after `await next(context)`

might not work reliably in all scenarios. This issue is particularly true when using ASP.NET Core integration or in certain runtime configurations where the response stream might have already been sent. To ensure headers are set correctly, consider retrieving the response from `context.GetInvocationResult().Value`

and setting headers before the response is returned from your function, rather than attempting to modify them in middleware after function execution completes.

For a more complete example of using custom middleware in your function app, see the [custom middleware reference sample](https://github.com/Azure/azure-functions-dotnet-worker/blob/main/samples/CustomMiddleware).

### Customizing JSON serialization

The isolated worker model uses `System.Text.Json`

by default. You can customize the behavior of the serializer by configuring services as part of your `Program.cs`

file. This section covers general-purpose serialization and doesn't influence [HTTP trigger JSON serialization with ASP.NET Core integration](#json-serialization-with-aspnet-core-integration), which you must configure separately.

```
using Microsoft.Azure.Functions.Worker.Builder;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
var builder = FunctionsApplication.CreateBuilder(args);
builder.ConfigureFunctionsWebApplication();
builder.Services.Configure<JsonSerializerOptions>(jsonSerializerOptions =>
{
jsonSerializerOptions.PropertyNamingPolicy = JsonNamingPolicy.CamelCase;
jsonSerializerOptions.DefaultIgnoreCondition = JsonIgnoreCondition.WhenWritingNull;
jsonSerializerOptions.ReferenceHandler = ReferenceHandler.Preserve;
// override the default value
jsonSerializerOptions.PropertyNameCaseInsensitive = false;
});
builder.Build().Run();
```


To use JSON.NET (`Newtonsoft.Json`

) for serialization, install the [ Microsoft.Azure.Core.NewtonsoftJson](https://www.nuget.org/packages/Microsoft.Azure.Core.NewtonsoftJson) package. Then, in your service registration, reassign the

`Serializer`

property on the `WorkerOptions`

configuration. The following example shows this configuration by using `ConfigureFunctionsWebApplication`

, but it also works for `ConfigureFunctionsWorkerDefaults`

:```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Builder;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
var builder = FunctionsApplication.CreateBuilder(args);
builder.ConfigureFunctionsWebApplication();
builder.Services.Configure<WorkerOptions>(workerOptions =>
{
var settings = NewtonsoftJsonObjectSerializer.CreateJsonSerializerSettings();
settings.ContractResolver = new CamelCasePropertyNamesContractResolver();
settings.NullValueHandling = NullValueHandling.Ignore;
workerOptions.Serializer = new NewtonsoftJsonObjectSerializer(settings);
});
builder.Build().Run();
```


## Methods recognized as functions

A function method is a public method of a public class with a `Function`

attribute applied to the method and a trigger attribute applied to an input parameter, as shown in the following example:

```
[Function(nameof(QueueInputOutputFunction))]
[QueueOutput("output-queue")]
public string[] QueueInputOutputFunction([QueueTrigger("input-queue")] Album myQueueItem, FunctionContext context)
```


The trigger attribute specifies the trigger type and binds input data to a method parameter. The preceding example function is triggered by a queue message, and the queue message is passed to the method in the `myQueueItem`

parameter.

The `Function`

attribute marks the method as a function entry point. The name must be unique within a project, start with a letter, and only contain letters, numbers, `_`

, and `-`

, up to 127 characters in length. Project templates often create a method named `Run`

, but the method name can be any valid C# method name. The method must be a public member of a public class. It should generally be an instance method so that services can be passed in via [dependency injection](#dependency-injection).

## Function parameters

Here are some of the parameters that you can include as part of a function method signature:

[Bindings](#bindings), which are marked as such by decorating the parameters as attributes. The function must contain exactly one trigger parameter.- An
[execution context object](#execution-context), which provides information about the current invocation. - A
[cancellation token](#cancellation-tokens), used for graceful shutdown.

### Execution context

In the isolated worker model, the worker process passes a [FunctionContext](/en-us/dotnet/api/microsoft.azure.functions.worker.functioncontext?view=azure-dotnet&preserve-view=true) object to your function methods. This object lets you get an [ ILogger](/en-us/dotnet/api/microsoft.extensions.logging.ilogger) instance to write to the logs by calling the

[GetLogger](/en-us/dotnet/api/microsoft.azure.functions.worker.functioncontextloggerextensions.getlogger)method and supplying a

`categoryName`

string. You can use this context to obtain an [without having to use dependency injection. For more information, see](/en-us/dotnet/api/microsoft.extensions.logging.ilogger)

`ILogger`

[Logging](#logging).

### Cancellation tokens

A function can accept a [cancellationToken](/en-us/dotnet/api/system.threading.cancellationtoken) parameter, which enables the operating system to notify your code when the function is about to be terminated. You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.

.NET functions that run in an isolated worker process support cancellation tokens. The following example raises an exception when a cancellation request is received:

```
[Function(nameof(ThrowOnCancellation))]
public async Task ThrowOnCancellation(
[EventHubTrigger("sample-workitem-1", Connection = "EventHubConnection")] string[] messages,
FunctionContext context,
CancellationToken cancellationToken)
{
_logger.LogInformation("C# EventHub {functionName} trigger function processing a request.", nameof(ThrowOnCancellation));
foreach (var message in messages)
{
cancellationToken.ThrowIfCancellationRequested();
await Task.Delay(6000); // task delay to simulate message processing
_logger.LogInformation("Message '{msg}' was processed.", message);
}
}
```


The following example performs clean-up actions when a cancellation request is received:

```
[Function(nameof(HandleCancellationCleanup))]
public async Task HandleCancellationCleanup(
[EventHubTrigger("sample-workitem-2", Connection = "EventHubConnection")] string[] messages,
FunctionContext context,
CancellationToken cancellationToken)
{
_logger.LogInformation("C# EventHub {functionName} trigger function processing a request.", nameof(HandleCancellationCleanup));
foreach (var message in messages)
{
if (cancellationToken.IsCancellationRequested)
{
_logger.LogInformation("A cancellation token was received, taking precautionary actions.");
// Take precautions like noting how far along you are with processing the batch
_logger.LogInformation("Precautionary activities complete.");
break;
}
await Task.Delay(6000); // task delay to simulate message processing
_logger.LogInformation("Message '{msg}' was processed.", message);
}
}
```


#### Scenarios that lead to cancellation

The cancellation token is signaled when the function invocation is canceled. Several reasons could lead to a cancellation, and those reasons vary depending on the trigger type being used. Some common reasons are:

- Client disconnect: The client that is invoking your function disconnects. This reason is most likely for HTTP trigger functions.
- Function app restart: You or the platform restart (or stop) the function app around the same time an invocation is requested. A restart can occur due to worker instance movements, worker instance updates, or scaling.

#### Cancellation considerations

Invocations in-flight during a restart event might be retried depending on how they were triggered. For more information, see the

[retry documentation](functions-bindings-error-pages#retries).The host sends the invocation through to the worker

*even*if the cancellation token is canceled*before*the host is able to send the invocation request to the worker.If you don't want pre-canceled invocations to be sent to the worker, add the

`SendCanceledInvocationsToWorker`

property to your`host.json`

file to disable this behavior.This example shows a

`host.json`

file that uses this property:`{ "version": "2.0", "SendCanceledInvocationsToWorker": "false" }`

Setting

`SendCanceledInvocationsToWorker`

to`false`

might lead to a`FunctionInvocationCanceled`

exception with the following log:Cancellation has been requested. The invocation request with id '{invocationId}' is canceled and won't be sent to the worker.

This exception occurs when the cancellation token is canceled (as a result of one of the events described earlier)

*before*the host sends an incoming invocation request to the worker. This exception can be safely ignored and is expected when`SendCanceledInvocationsToWorker`

is`false`

.

## Bindings

Define bindings by using attributes on methods, parameters, and return types. Bindings can provide data as strings, arrays, and serializable types, such as plain old class objects (POCOs). For some binding extensions, you can also [bind to service-specific types](#sdk-types) defined in service SDKs.

For HTTP triggers, see the [HTTP trigger](#http-trigger) section.

For a complete set of reference samples that use triggers and bindings with isolated worker process functions, see the [binding extensions reference sample](https://github.com/Azure/azure-functions-dotnet-worker/blob/main/samples/Extensions).

### Input bindings

A function can have zero or more input bindings that pass data to the function. Like triggers, you define input bindings by applying a binding attribute to an input parameter. When the function executes, the runtime tries to get data specified in the binding. The data being requested often depends on information provided by the trigger through binding parameters.

### Output bindings

To write to an output binding, you must apply an output binding attribute to the function method. This attribute defines how to write to the bound service. The method's return value is written to the output binding. For example, the following example writes a string value to a message queue named `output-queue`

by using an output binding:

```
[Function(nameof(QueueInputOutputFunction))]
[QueueOutput("output-queue")]
public string[] QueueInputOutputFunction([QueueTrigger("input-queue")] Album myQueueItem, FunctionContext context)
{
// Use a string array to return more than one message.
string[] messages = {
$"Album name = {myQueueItem.Name}",
$"Album songs = {myQueueItem.Songs}"};
_logger.LogInformation("{msg1},{msg2}", messages[0], messages[1]);
// Queue Output messages
return messages;
}
```


### Multiple output bindings

The data written to an output binding is always the return value of the function. If you need to write to more than one output binding, you must create a custom return type. This return type must have the output binding attribute applied to one or more properties of the class. The following example is an HTTP-triggered function that uses [ASP.NET Core integration](#aspnet-core-integration) and writes to both the HTTP response and a queue output binding:

```
public class MultipleOutputBindings
{
private readonly ILogger<MultipleOutputBindings> _logger;
public MultipleOutputBindings(ILogger<MultipleOutputBindings> logger)
{
_logger = logger;
}
[Function("MultipleOutputBindings")]
public MyOutputType Run([HttpTrigger(AuthorizationLevel.Function, "post")] HttpRequest req)
{
_logger.LogInformation("C# HTTP trigger function processed a request.");
var myObject = new MyOutputType
{
Result = new OkObjectResult("C# HTTP trigger function processed a request."),
MessageText = "some output"
};
return myObject;
}
public class MyOutputType
{
[HttpResult]
public IActionResult Result { get; set; }
[QueueOutput("myQueue")]
public string MessageText { get; set; }
}
}
```


When you use custom return types for multiple output bindings with ASP.NET Core integration, you must add the `[HttpResult]`

attribute to the property that provides the result. The `HttpResult`

attribute is available when using [SDK 1.17.3-preview2 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Sdk/1.17.3-preview2) along with [version 3.2.0 or later of the HTTP extension](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Http/3.2.0) and [version 1.3.0 or later of the ASP.NET Core extension](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Http.AspNetCore/1.3.0).

### SDK types

For some service-specific binding types, you can provide binding data by using types from service SDKs and frameworks. These types offer capabilities beyond what a serialized string or plain-old CLR object (POCO) can provide. To use the newer types, update your project to use newer versions of core dependencies.

| Dependency | Version requirement |
|---|---|
|

[Microsoft.Azure.Functions.Worker.Sdk](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Sdk/)When testing SDK types locally on your machine, you also need to use [Azure Functions Core Tools](functions-run-local), version 4.0.5000 or later. You can check your current version by using the `func --version`

command.

Each binding extension also has its own minimum version requirement, which is described in the extension reference articles. These binding extensions currently support SDK types:

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

## HTTP trigger

[HTTP triggers](functions-bindings-http-webhook-trigger) allow a function to be invoked by an HTTP request. You can use two different approaches:

- An
[ASP.NET Core integration model](#aspnet-core-integration)that uses concepts familiar to ASP.NET Core developers - A
[built-in model](#built-in-http-model), which doesn't require extra dependencies and uses custom types for HTTP requests and responses. This approach is maintained for backward compatibility with previous .NET isolated worker apps.

### ASP.NET Core integration

This section shows how to work with the underlying HTTP request and response objects by using types from ASP.NET Core, including [HttpRequest](/en-us/dotnet/api/microsoft.aspnetcore.http.httprequest), [HttpResponse](/en-us/dotnet/api/microsoft.aspnetcore.http.httpresponse), and [IActionResult](/en-us/dotnet/api/microsoft.aspnetcore.mvc.iactionresult). This model isn't available to [apps targeting .NET Framework](#supported-versions), which should instead use the [built-in model](#built-in-http-model).

Note

This model doesn't expose all features of ASP.NET Core. Specifically, it doesn't provide access to the ASP.NET Core middleware pipeline and routing capabilities. ASP.NET Core integration requires you to use updated packages.

To enable ASP.NET Core integration for HTTP:

Add a reference in your project to the

[Microsoft.Azure.Functions.Worker.Extensions.Http.AspNetCore](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Http.AspNetCore/)package, version 1.0.0 or later.Update your project to use these specific package versions:

[Microsoft.Azure.Functions.Worker.Sdk](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Sdk/), version 1.11.0. or later[Microsoft.Azure.Functions.Worker](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker/), version 1.16.0 or later.

In your

`Program.cs`

file, update the host builder configuration to call`ConfigureFunctionsWebApplication()`

. This method replaces`ConfigureFunctionsWorkerDefaults()`

if you would use that method otherwise. The following example shows a minimal setup without other customizations:Note

Your application must reference version 2.0.0 or later of

[Microsoft.Azure.Functions.Worker.Extensions.Http.AspNetCore](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Http.AspNetCore/)to use ASP.NET Core integration with`IHostApplicationBuilder`

.`using Microsoft.Azure.Functions.Worker.Builder; using Microsoft.Extensions.Hosting; var builder = FunctionsApplication.CreateBuilder(args); builder.ConfigureFunctionsWebApplication(); builder.Build().Run();`

Update any existing HTTP-triggered functions to use the ASP.NET Core types. This example shows the standard

`HttpRequest`

and an`IActionResult`

used for a simple "hello, world" function:`[Function("HttpFunction")] public IActionResult Run( [HttpTrigger(AuthorizationLevel.Anonymous, "get")] HttpRequest req) { return new OkObjectResult($"Welcome to Azure Functions, {req.Query["name"]}!"); }`


#### JSON serialization with ASP.NET Core integration

ASP.NET Core has its own serialization layer, and it isn't affected by [customizing general serialization configuration](#customizing-json-serialization). To customize the serialization behavior used for your HTTP triggers, you need to include an `.AddMvc()`

call as part of service registration. The returned `IMvcBuilder`

can be used to modify ASP.NET Core's JSON serialization settings.

You can continue to use `HttpRequestData`

and `HttpResponseData`

while using ASP.NET integration, though for most apps, it's better to instead use `HttpRequest`

and `IActionResult`

. Using `HttpRequestData`

/`HttpResponseData`

doesn't invoke the ASP.NET Core serialization layer and instead relies upon the [general worker serialization configuration](#customizing-json-serialization) for the app. However, when ASP.NET Core integration is enabled, you might still need to add configuration. The default behavior from ASP.NET Core is to disallow synchronous IO. To use a custom serializer that doesn't support asynchronous IO, such as `NewtonsoftJsonObjectSerializer`

, you need to enable synchronous IO for your application by configuring the `KestrelServerOptions`

.

The following example shows how to configure JSON.NET (`Newtonsoft.Json`

) and the [Microsoft.AspNetCore.Mvc.NewtonsoftJson NuGet package](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.NewtonsoftJson) for serialization using this approach:

```
using Microsoft.AspNetCore.Server.Kestrel.Core;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Builder;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
var builder = FunctionsApplication.CreateBuilder(args);
builder.ConfigureFunctionsWebApplication();
builder.Services
.AddApplicationInsightsTelemetryWorkerService()
.ConfigureFunctionsApplicationInsights();
builder.Services.AddMvc().AddNewtonsoftJson();
// Only needed if using HttpRequestData/HttpResponseData and a serializer that doesn't support asynchronous IO
// builder.Services.Configure<KestrelServerOptions>(options => options.AllowSynchronousIO = true);
builder.Build().Run();
```


### Built-in HTTP model

In the built-in model, the system translates the incoming HTTP request message into an [HttpRequestData](/en-us/dotnet/api/microsoft.azure.functions.worker.http.httprequestdata?view=azure-dotnet&preserve-view=true) object that it passes to the function. This object provides data from the request, including `Headers`

, `Cookies`

, `Identities`

, `URL`

, and optionally a message `Body`

. This object represents the HTTP request but isn't directly connected to the underlying HTTP listener or the received message.

Important

If you use `HttpRequestData`

, the body of the HTTP request can't be a stream. For example, if the request has the `Transfer-Encoding: chunked`

header and no `Content-Length`

header, the `HttpRequestData`

object's `Body`

property will be a null stream. If you need to work with streaming HTTP requests, consider using the [ASP.NET Core integration model](#aspnet-core-integration) instead.

Likewise, the function returns an [HttpResponseData](/en-us/dotnet/api/microsoft.azure.functions.worker.http.httpresponsedata?view=azure-dotnet&preserve-view=true) object, which provides data used to create the HTTP response, including message `StatusCode`

, `Headers`

, and optionally a message `Body`

.

The following example demonstrates the use of `HttpRequestData`

and `HttpResponseData`

:

```
[Function(nameof(HttpFunction))]
public static HttpResponseData Run([HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)] HttpRequestData req,
FunctionContext executionContext)
{
var logger = executionContext.GetLogger(nameof(HttpFunction));
logger.LogInformation("message logged");
var response = req.CreateResponse(HttpStatusCode.OK);
response.Headers.Add("Content-Type", "text/plain; charset=utf-8");
response.WriteString("Welcome to .NET isolated worker !!");
return response;
}
```


## Logging

You can write to logs by using an [ ILogger<T>](/en-us/dotnet/api/microsoft.extensions.logging.ilogger-1) or

[instance. You can get the logger through](/en-us/dotnet/api/microsoft.extensions.logging.ilogger)

`ILogger`

[dependency injection](#dependency-injection)of an

[or of an](/en-us/dotnet/api/microsoft.extensions.logging.ilogger-1)

`ILogger<T>`

[ILoggerFactory](/en-us/dotnet/api/microsoft.extensions.logging.iloggerfactory):

```
public class MyFunction {
private readonly ILogger<MyFunction> _logger;
public MyFunction(ILogger<MyFunction> logger) {
_logger = logger;
}
[Function(nameof(MyFunction))]
public void Run([BlobTrigger("samples-workitems/{name}", Connection = "")] string myBlob, string name)
{
_logger.LogInformation($"C# Blob trigger function Processed blob\n Name: {name} \n Data: {myBlob}");
}
}
```


You can also get the logger from a [FunctionContext](/en-us/dotnet/api/microsoft.azure.functions.worker.functioncontext?view=azure-dotnet&preserve-view=true) object passed to your function. Call the [GetLogger<T>](/en-us/dotnet/api/microsoft.azure.functions.worker.functioncontextloggerextensions.getlogger#microsoft-azure-functions-worker-functioncontextloggerextensions-getlogger-1) or [GetLogger](/en-us/dotnet/api/microsoft.azure.functions.worker.functioncontextloggerextensions.getlogger) method, passing a string value that is the name for the category in which the logs are written. The category is usually the name of the specific function from which the logs are written. For more information about categories, see the [monitoring article](functions-monitoring#log-levels-and-categories).

Use the methods of [ ILogger<T>](/en-us/dotnet/api/microsoft.extensions.logging.ilogger-1) and

[to write various log levels, such as](/en-us/dotnet/api/microsoft.extensions.logging.ilogger)

`ILogger`

`LogWarning`

or `LogError`

. For more information about log levels, see the [monitoring article](functions-monitoring#log-levels-and-categories). You can customize the log levels for components added to your code by registering filters:

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Builder;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;
var builder = FunctionsApplication.CreateBuilder(args);
builder.ConfigureFunctionsWebApplication();
// Registers IHttpClientFactory.
// By default this sends a lot of Information-level logs.
builder.Services.AddHttpClient();
// Disable IHttpClientFactory Informational logs.
// Note -- you can also remove the handler that does the logging: https://github.com/aspnet/HttpClientFactory/issues/196#issuecomment-432755765
builder.Logging.AddFilter("System.Net.Http.HttpClient", LogLevel.Warning);
builder.Build().Run();
```


As part of configuring your app in `Program.cs`

, you can also define the behavior for how errors are surfaced to your logs. The default behavior depends on the type of builder you're using.

When you use an `IHostApplicationBuilder`

, exceptions thrown by your code flow through the system without changes. You don't need any other configuration.

### Application Insights

You can configure your isolated process application to send logs directly to [Application Insights](/en-us/azure/azure-monitor/app/app-insights-overview?tabs=net). This configuration replaces the default behavior of [relaying logs through the host](configure-monitoring#custom-application-logs). Unless you're using [Aspire](#aspire), configure direct Application Insights integration because it gives you control over how those logs are emitted.

Application Insights integration isn't enabled by default in all setup experiences. Some templates create Functions projects with the necessary packages and startup code commented out. If you want to use Application Insights integration, uncomment these lines in `Program.cs`

and the project's `.csproj`

file. The instructions in the rest of this section also describe how to enable the integration.

If your project is part of an [Aspire orchestration](#aspire), it uses OpenTelemetry for monitoring instead. Don't enable direct Application Insights integration within Aspire projects. Instead, configure the Azure Monitor OpenTelemetry exporter as part of the [service defaults project](/en-us/dotnet/aspire/fundamentals/service-defaults#opentelemetry-configuration). If your Functions project uses Application Insights integration in an Aspire context, the application errors on startup.

#### Install packages

To write logs directly to Application Insights from your code, add references to these packages in your project:

[Microsoft.Azure.Functions.Worker.ApplicationInsights](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.ApplicationInsights/), version 1.0.0 or later.[Microsoft.ApplicationInsights.WorkerService](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WorkerService).

Run the following commands to add these references to your project:

```
dotnet add package Microsoft.ApplicationInsights.WorkerService
dotnet add package Microsoft.Azure.Functions.Worker.ApplicationInsights
```


#### Configure startup

After installing the packages, call `AddApplicationInsightsTelemetryWorkerService()`

and `ConfigureFunctionsApplicationInsights()`

during service configuration in your `Program.cs`

file, as shown in the following example:

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Builder;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
var builder = FunctionsApplication.CreateBuilder(args);
builder.Services
.AddApplicationInsightsTelemetryWorkerService()
.ConfigureFunctionsApplicationInsights();
builder.Build().Run();
```


The call to `ConfigureFunctionsApplicationInsights()`

adds an `ITelemetryModule`

that listens to a Functions-defined `ActivitySource`

. This module creates the dependency telemetry required to support distributed tracing. For more information about `AddApplicationInsightsTelemetryWorkerService()`

and how to use it, see [Application Insights for Worker Service applications](/en-us/azure/azure-monitor/app/worker-service).

#### Manage log levels

Important

The Functions host and the isolated process worker have separate configuration for log levels. Any [Application Insights configuration in host.json](functions-host-json#applicationinsights) doesn't affect logging from the worker, and similarly, configuration in your worker code doesn't impact logging from the host. Apply changes in both places if your scenario requires customization at both layers.

The rest of your application continues to work with `ILogger`

and `ILogger<T>`

. However, by default, the Application Insights SDK adds a logging filter that instructs the logger to capture only warnings and more severe logs. You can configure log levels in the isolated worker process in one of these ways:

| Configuration method | Benefits |
|---|---|
| In your code | Promotes a clearer separation between host-side and worker-side configurations. |
Using `appsettings.json` |
Useful when you want to set different log levels for different categories without having to modify your code. |

To disable the default behavior and capture all log levels, remove the filter rule as part of service configuration:

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Builder;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;
var builder = FunctionsApplication.CreateBuilder(args);
builder.Services
.AddApplicationInsightsTelemetryWorkerService()
.ConfigureFunctionsApplicationInsights();
builder.Logging.Services.Configure<LoggerFilterOptions>(options =>
{
LoggerFilterRule defaultRule = options.Rules.FirstOrDefault(rule => rule.ProviderName
== "Microsoft.Extensions.Logging.ApplicationInsights.ApplicationInsightsLoggerProvider");
if (defaultRule is not null)
{
options.Rules.Remove(defaultRule);
}
});
builder.Build().Run();
```


For more information about configuring logging, see [Logging in .NET](/en-us/dotnet/core/extensions/logging) and [Application Insights for Worker Service applications](/en-us/azure/azure-monitor/app/worker-service#ilogger-logs).

## Performance optimizations

This section outlines options you can enable that improve performance around [cold start](event-driven-scaling#cold-start).

In general, your app should use the latest versions of its core dependencies. At a minimum, update your project as follows:

- Upgrade
[Microsoft.Azure.Functions.Worker](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker/)to version 1.19.0 or later. - Upgrade
[Microsoft.Azure.Functions.Worker.Sdk](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Sdk/)to version 1.16.4 or later. - Add a framework reference to
`Microsoft.AspNetCore.App`

, unless your app targets .NET Framework.

The following snippet shows this configuration in the context of a project file:

```
<ItemGroup>
<FrameworkReference Include="Microsoft.AspNetCore.App" />
<PackageReference Include="Microsoft.Azure.Functions.Worker" Version="1.21.0" />
<PackageReference Include="Microsoft.Azure.Functions.Worker.Sdk" Version="1.16.4" />
</ItemGroup>
```


### Placeholders

Placeholders are a platform capability that improves cold start for apps targeting .NET 6 or later. To use this optimization, you must explicitly enable placeholders by following these steps:

Update your project configuration to use the latest dependency versions, as detailed in the previous section.

Set the

application setting to`WEBSITE_USE_PLACEHOLDER_DOTNETISOLATED`

`1`

. Use this[az functionapp config appsettings set](/en-us/cli/azure/functionapp/config/appsettings#az-functionapp-config-appsettings-set)command:`az functionapp config appsettings set -g <groupName> -n <appName> --settings 'WEBSITE_USE_PLACEHOLDER_DOTNETISOLATED=1'`

In this example, replace

`<groupName>`

with the name of the resource group, and replace`<appName>`

with the name of your function app.Make sure that the

property of the function app matches your project's target framework, which must be .NET 6 or later. Use this`netFrameworkVersion`

[az functionapp config set](/en-us/cli/azure/functionapp/config#az-functionapp-config-set)command:`az functionapp config set -g <groupName> -n <appName> --net-framework-version <framework>`

In this example, also replace

`<framework>`

with the appropriate version string, such as`v8.0`

, according to your target .NET version.Make sure that your function app is configured to use a 64-bit process. Use this

[az functionapp config set](/en-us/cli/azure/functionapp/config#az-functionapp-config-set)command:`az functionapp config set -g <groupName> -n <appName> --use-32bit-worker-process false`


Important

When setting the [ WEBSITE_USE_PLACEHOLDER_DOTNETISOLATED](functions-app-settings#website_use_placeholder_dotnetisolated) to

`1`

, you must set all other function app configurations correctly. Otherwise, your function app might fail to start.### Optimized executor

The function executor is a component of the platform that causes invocations to run. An optimized version of this component is enabled by default starting with version 1.16.2 of the SDK. No other configuration is required.

### ReadyToRun

You can compile your function app as [ReadyToRun binaries](/en-us/dotnet/core/deploying/ready-to-run). ReadyToRun is a form of ahead-of-time compilation that can improve startup performance to help reduce the effect of cold starts when running in a [Consumption plan](consumption-plan). ReadyToRun is available in .NET 6 and later versions and requires [version 4.0 or later](functions-versions) of the Azure Functions runtime.

ReadyToRun requires you to build the project against the runtime architecture of the hosting app. When these architectures aren't aligned, your app encounters an error at startup. Select your runtime identifier from this table:

| Operating System | App is 32-bit1 |
Runtime identifier |
|---|---|---|
| Windows | True | `win-x86` |
| Windows | False | `win-x64` |
| Linux | True | N/A (not supported) |
| Linux | False | `linux-x64` |

1 Only 64-bit apps are eligible for some other performance optimizations.

To check if your Windows app is 32-bit or 64-bit, run the following CLI command, substituting `<group_name>`

with the name of your resource group and `<app_name>`

with the name of your application. An output of "true" indicates that the app is 32-bit, and "false" indicates 64-bit.

```
az functionapp config show -g <group_name> -n <app_name> --query "use32BitWorkerProcess"
```


You can change your application to 64-bit with the following command, using the same substitutions:

```
az functionapp config set -g <group_name> -n <app_name> --use-32bit-worker-process false`
```


To compile your project as ReadyToRun, update your project file by adding the `<PublishReadyToRun>`

and `<RuntimeIdentifier>`

elements. The following example shows a configuration for publishing to a Windows 64-bit function app.

```
<PropertyGroup>
<TargetFramework>net8.0</TargetFramework>
<AzureFunctionsVersion>v4</AzureFunctionsVersion>
<RuntimeIdentifier>win-x64</RuntimeIdentifier>
<PublishReadyToRun>true</PublishReadyToRun>
</PropertyGroup>
```


If you don't want to set the `<RuntimeIdentifier>`

as part of the project file, you can also configure this setting as part of the publishing gesture itself. For example, with a Windows 64-bit function app, the .NET CLI command is:

```
dotnet publish --runtime win-x64
```


In Visual Studio, set the **Target Runtime** option in the publish profile to the correct runtime identifier. When set to the default value of **Portable**, ReadyToRun isn't used.

## Deploy to Azure Functions

When you deploy your function code project to Azure, it must run in either a function app or in a Linux container. You must create the function app and other required Azure resources before you deploy your code.

You can also deploy your function app in a Linux container. For more information, see [Working with containers and Azure Functions](functions-how-to-custom-container).

### Create Azure resources

You can create your function app and other required resources in Azure by using one of these methods:

[Visual Studio](functions-develop-vs#publish-to-azure): Visual Studio can create resources for you during the code publishing process.[Visual Studio Code](functions-develop-vs-code#publish-to-azure): Visual Studio Code can connect to your subscription, create the resources needed by your app, and then publish your code.[Azure CLI](how-to-create-function-azure-cli?pivots=programming-language-csharp#create-supporting-azure-resources-for-your-function): Use the Azure CLI to create the required resources in Azure.[Azure PowerShell](create-resources-azure-powershell#create-a-serverless-function-app-for-c): Use Azure PowerShell to create the required resources in Azure.[Deployment templates](functions-infrastructure-as-code): Use ARM templates and Bicep files to automate the deployment of the required resources to Azure. Make sure your template includes any[required settings](#deployment-requirements).[Azure portal](functions-create-function-app-portal): Create the required resources in the[Azure portal](https://portal.azure.com).

### Publish your application

After creating your function app and other required resources in Azure, deploy the code project to Azure by using one of these methods:

[Visual Studio](functions-develop-vs#publish-to-azure): Simple manual deployment during development.[Visual Studio Code](functions-develop-vs-code?tabs=isolated-process&pivots=programming-language-csharp#republish-project-files): Simple manual deployment during development.[Azure Functions Core Tools](functions-run-local?tabs=linuxisolated-process&pivots=programming-language-csharp#project-file-deployment): Deploy project file from the command line.[Continuous deployment](functions-continuous-deployment): Useful for ongoing maintenance, frequently to a[staging slot](functions-deployment-slots).[Deployment templates](functions-infrastructure-as-code#zip-deployment-package): You can use ARM templates or Bicep files to automate package deployments.

For more information, see [Deployment technologies in Azure Functions](functions-deployment-technologies).

#### Deployment payload

Many of the deployment methods use a zip archive. If you create the zip archive yourself, it must follow the structure outlined in this section. If it doesn't, your app might experience errors at startup.

The deployment payload should match the output of a `dotnet publish`

command, though without the enclosing parent folder. The zip archive should be made from the following files:

`.azurefunctions/`

`extensions.json`

`functions.metadata`

`host.json`

`worker.config.json`

- Your project executable (a console app)
- Other supporting files and directories peer to that executable

The build process generates these files, and you shouldn't edit them directly.

Tip

You can use the `func pack`

command in Core Tools to correctly generate a zip archive for deployment. Support for `func pack`

is currently in preview.

When preparing a zip archive for deployment, compress only the contents of the output directory, not the enclosing directory itself. When the archive is extracted into the current working directory, the files listed earlier need to be immediately visible.

### Deployment requirements

To run .NET functions in the isolated worker model in Azure, you need to meet a few requirements. The requirements depend on the operating system:

- Set
[FUNCTIONS_WORKER_RUNTIME](functions-app-settings#functions_worker_runtime)to`dotnet-isolated`

. - Set
[netFrameworkVersion](functions-app-settings#netframeworkversion)to the desired version.

When you create your function app in Azure using the methods in the previous section, these required settings are added for you. When you create these resources [by using ARM templates or Bicep files for automation](functions-infrastructure-as-code), you must make sure to set them in the template.

Aspire

[Aspire](/en-us/dotnet/aspire/get-started/aspire-overview) is an opinionated stack that simplifies development of distributed applications in the cloud. You can enlist isolated worker model projects in Aspire 13 orchestrations. See [Azure Functions with Aspire](dotnet-aspire-integration) for more information.

## Debugging

When running locally using Visual Studio or Visual Studio Code, you're able to debug your .NET isolated worker project as normal. However, there are two debugging scenarios that don't work as expected.

### Remote Debugging using Visual Studio

Because your isolated worker process app runs outside the Functions runtime, you need to attach the remote debugger to a separate process. To learn more about debugging using Visual Studio, see [Remote Debugging](functions-develop-vs?tabs=isolated-process#remote-debugging).

### Debugging when targeting .NET Framework

If your isolated project targets .NET Framework 4.8, you need to take manual steps to enable debugging. These steps aren't required if using another target framework.

Your app should start with a call to `FunctionsDebugger.Enable();`

as its first operation. This occurs in the `Main()`

method before initializing a HostBuilder. Your `Program.cs`

file should look similar to this:

```
using System;
using System.Diagnostics;
using Microsoft.Extensions.Hosting;
using Microsoft.Azure.Functions.Worker;
using NetFxWorker;
namespace MyDotnetFrameworkProject
{
internal class Program
{
static void Main(string[] args)
{
FunctionsDebugger.Enable();
var host = FunctionsApplication
.CreateBuilder(args)
.Build();
host.Run();
}
}
}
```


Next, you need to manually attach to the process using a .NET Framework debugger. Visual Studio doesn't do this automatically for isolated worker process .NET Framework apps yet, and the "Start Debugging" operation should be avoided.

In your project directory (or its build output directory), run:

```
func host start --dotnet-isolated-debug
```


This starts your worker, and the process stops with the following message:

```
Azure Functions .NET Worker (PID: <process id>) initialized in debug mode. Waiting for debugger to attach...
```


Where `<process id>`

is the ID for your worker process. You can now use Visual Studio to manually attach to the process. For instructions on this operation, see [How to attach to a running process](/en-us/visualstudio/debugger/attach-to-running-processes-with-the-visual-studio-debugger#BKMK_Attach_to_a_running_process).

After the debugger is attached, the process execution resumes, and you'll be able to debug.

## Preview .NET versions

Before a generally available release, a .NET version might be released in a *Preview* or *Go-live* state. See the [.NET Official Support Policy](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) for details on these states.

While it might be possible to target a given release from a local Functions project, function apps hosted in Azure might not have that release available. Azure Functions can only be used with Preview or Go-live releases noted in this section.

Azure Functions doesn't currently work with any "Preview" or "Go-live" .NET releases. See [Supported versions](#supported-versions) for a list of generally available releases that you can use.

### Using a preview .NET SDK

To use Azure Functions with a preview version of .NET, you need to update your project by:

- Installing the relevant .NET SDK version in your development
- Changing the
`TargetFramework`

setting in your`.csproj`

file

When you deploy to your function app in Azure, you also need to ensure that the framework is made available to the app. During the preview period, some tools and experiences may not surface the new preview version as an option. If you don't see the preview version included in the Azure portal, for example, you can use the REST API, Bicep files, or the Azure CLI to configure the version manually.

For apps hosted on Windows, use the following Azure CLI command. Replace `<groupName>`

with the name of the resource group, and replace `<appName>`

with the name of your function app. Replace `<framework>`

with the appropriate version string, such as `v8.0`

.

```
az functionapp config set -g <groupName> -n <appName> --net-framework-version <framework>
```


### Considerations for using .NET preview versions

Keep these considerations in mind when using Functions with preview versions of .NET:

When you author your functions in Visual Studio, you must use

[Visual Studio Insiders](https://visualstudio.microsoft.com/insiders/), which supports building Azure Functions projects with .NET preview SDKs.Make sure you have the latest Functions tools and templates. To update your tools:

- Navigate to
**Tools**>**Options**, choose**Azure Functions**under**Projects and Solutions**>**More Settings**. - Select
**Check for updates**and install updates as prompted.

- Navigate to
During a preview period, your development environment might have a more recent version of the .NET preview than the hosted service. This can cause your function app to fail when deployed. To address this, you can specify the version of the SDK to use in

.`global.json`

- Run the
`dotnet --list-sdks`

command and note the preview version you're currently using during local development. - Run the
`dotnet new globaljson --sdk-version <SDK_VERSION> --force`

command, where`<SDK_VERSION>`

is the version you're using locally. For example,`dotnet new globaljson --sdk-version dotnet-sdk-10.0.100-preview.5.25277.114 --force`

causes the system to use the .NET 10 Preview 5 SDK when building your project.

- Run the

Note

Because of the just-in-time loading of preview frameworks, function apps running on Windows can experience increased cold start times when compared against earlier GA versions.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-compare-logic-apps-ms-flow-webjobs -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache-input -->

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
<!-- Source: N/A -->

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

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-reference -->

# Azure Functions developer guide

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure Functions, all functions share some core technical concepts and components, regardless of your preferred language or development environment. This article is language-specific. Choose your preferred language at the top of the article.

This article assumes that you've already read the [Azure Functions overview](functions-overview).

If you prefer to jump right in, you can complete a quickstart tutorial using [Visual Studio](functions-create-your-first-function-visual-studio), [Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-csharp), or from the [command prompt](how-to-create-function-azure-cli?pivots=programming-language-csharp).

If you prefer to jump right in, you can complete a quickstart tutorial using [Maven](how-to-create-function-azure-cli?pivots=programming-language-java) (command line), [Eclipse](functions-create-maven-eclipse), [IntelliJ IDEA](functions-create-maven-intellij), [Gradle](functions-create-first-java-gradle), [Quarkus](functions-create-first-quarkus), [Spring Cloud](/en-us/azure/developer/java/spring-framework/getting-started-with-spring-cloud-function-in-azure?toc=/azure/azure-functions/toc.json), or [Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-java).

If you prefer to jump right in, you can complete a quickstart tutorial using [Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-javascript) or from the [command prompt](how-to-create-function-azure-cli?pivots=programming-language-javascript).

If you prefer to jump right in, you can complete a quickstart tutorial using [Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-typescript) or from the [command prompt](how-to-create-function-azure-cli?pivots=programming-language-typescript).

If you prefer to jump right in, you can complete a quickstart tutorial using [Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-powershell) or from the [command prompt](how-to-create-function-azure-cli?pivots=programming-language-powershell).

If you prefer to jump right in, you can complete a quickstart tutorial using [Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-python) or from the [command prompt](how-to-create-function-azure-cli?pivots=programming-language-python).

## Code project

At the core of Azure Functions is a language-specific code project that implements one or more units of code execution called *functions*. Functions are simply methods that run in the Azure cloud based on events, in response to HTTP requests, or on a schedule. Think of your Azure Functions code project as a mechanism for organizing, deploying, and collectively managing your individual functions in the project when they're running in Azure. For more information, see [Organize your functions](functions-best-practices#organize-your-functions).

The way that you lay out your code project and how you indicate which methods in your project are functions depends on the development language of your project. For detailed language-specific guidance, see the [C# developers guide](dotnet-isolated-process-guide).

The way that you lay out your code project and how you indicate which methods in your project are functions depends on the development language of your project. For language-specific guidance, see the [Java developers guide](functions-reference-java).

The way that you lay out your code project and how you indicate which methods in your project are functions depends on the development language of your project. For language-specific guidance, see the [Node.js developers guide](functions-reference-node).

The way that you lay out your code project and how you indicate which methods in your project are functions depends on the development language of your project. For language-specific guidance, see the [PowerShell developers guide](functions-reference-powershell).

The way that you lay out your code project and how you indicate which methods in your project are functions depends on the development language of your project. For language-specific guidance, see the [Python developers guide](functions-reference-python).

All functions must have a trigger, which defines how the function starts and can provide input to the function. Your functions can optionally define input and output bindings. These bindings simplify connections to other services without you having to work with client SDKs. For more information, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings).

Azure Functions provides a set of language-specific project and function templates that make it easy to create new code projects and add functions to your project. You can use any of the tools that support Azure Functions development to generate new apps and functions using these templates.

## Development tools

The following tools provide an integrated development and publishing experience for Azure Functions in your preferred language:

[Azure Functions Core Tools](functions-develop-local)(command prompt)

These tools integrate with [Azure Functions Core Tools](functions-develop-local) so that you can run and debug on your local computer using the Functions runtime. For more information, see [Code and test Azure Functions locally](functions-develop-local).

[ There's also an editor in the Azure portal that lets you update your code and your ]*function.json* definition file directly in the portal. You should only use this editor for small changes or creating proof-of-concept functions. You should always develop your functions locally, when possible. For more information, see [Create your first function in the Azure portal](functions-create-function-app-portal).

Portal editing is only supported for [Node.js version 3](functions-reference-node?pivots=nodejs-model-v3), which uses the function.json file.

## Deployment

When you publish your code project to Azure, you're essentially deploying your project to an existing function app resource. A function app provides an execution context in Azure in which your functions run. As such, it's the unit of deployment and management for your functions. From an Azure Resource perspective, a function app is equivalent to a site resource (`Microsoft.Web/sites`

) in Azure App Service, which is equivalent to a web app.

A function app is composed of one or more individual functions that are managed, deployed, and scaled together. All of the functions in a function app share the same [pricing plan](functions-scale), [deployment method](functions-deployment-technologies), and [runtime version](functions-versions). For more information, see [How to manage a function app](functions-how-to-use-azure-function-app-settings).

When the function app and any other required resources don't already exist in Azure, you first need to create these resources before you can deploy your project files. You can create these resources in one of these ways:

- During
[Visual Studio](functions-develop-vs#publish-to-azure)publishing

Using

[Visual Studio Code](functions-develop-vs-code#publish-to-azure)Programmatically using

[Azure CLI](scripts/functions-cli-create-serverless),[Azure PowerShell](create-resources-azure-powershell#create-a-serverless-function-app-for-c),[ARM templates](functions-create-first-function-resource-manager), or[Bicep files](functions-create-first-function-bicep)In the

[Azure portal](functions-create-function-app-portal)

In addition to tool-based publishing, Functions supports other technologies for deploying source code to an existing function app. For more information, see [Deployment technologies in Azure Functions](functions-deployment-technologies).

## Connect to services

A major requirement of any cloud-based compute service is reading data from and writing data to other cloud services. Functions provides an extensive set of bindings that makes it easier for you to connect to services without having to work with client SDKs.

Whether you use the binding extensions provided by Functions or you work with client SDKs directly, you securely store connection data and do not include it in your code. For more information, see [Connections](#connections).

### Bindings

Functions provides bindings for many Azure services and a few third-party services, which are implemented as extensions. For more information, see the [complete list of supported bindings](functions-triggers-bindings#supported-bindings).

Binding extensions can support both inputs and outputs, and many triggers also act as input bindings. Bindings let you configure the connection to services so that the Functions host can handle the data access for you. For more information, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings).

If you're having issues with errors coming from bindings, see the [Azure Functions Binding Error Codes](functions-bindings-error-pages) documentation.

### Client SDKs

While Functions provides bindings to simplify data access in your function code, you're still able to use a client SDK in your project to directly access a given service, if you prefer. You might need to use client SDKs directly should your functions require a functionality of the underlying SDK that's not supported by the binding extension.

When using client SDKs, you should use the same process for [storing and accessing connection strings](#connections) used by binding extensions.

When you create a client SDK instance in your functions, you should get the connection info required by the client from [Environment variables](functions-dotnet-class-library#environment-variables).

When you create a client SDK instance in your functions, you should get the connection info required by the client from [Environment variables](functions-reference-java#environment-variables).

When you create a client SDK instance in your functions, you should get the connection info required by the client from [Environment variables](functions-reference-node#environment-variables).

When you create a client SDK instance in your functions, you should get the connection info required by the client from [Environment variables](functions-reference-powershell#environment-variables).

When you create a client SDK instance in your functions, you should get the connection info required by the client from [Environment variables](functions-reference-python#environment-variables).

## Connections

As a security best practice, Azure Functions takes advantage of the application settings functionality of Azure App Service to help you more securely store strings, keys, and other tokens required to connect to other services. Application settings in Azure are stored encrypted and can be accessed at runtime by your app as environment variable `name`

`value`

pairs. For triggers and bindings that require a connection property, you set the application setting name instead of the actual connection string. You can't configure a binding directly with a connection string or key.

For example, consider a trigger definition that has a `connection`

property. Instead of the connection string, you set `connection`

to the name of an environment variable that contains the connection string. Using this secrets access strategy both makes your apps more secure and makes it easier for you to change connections across environments. For even more security, you can use identity-based connections.

The default configuration provider uses environment variables. These variables are defined in [application settings](functions-how-to-use-azure-function-app-settings?tabs=portal#settings) when running in the Azure and in the [local settings file](functions-develop-local#local-settings-file) when developing locally.

### Connection values

When the connection name resolves to a single exact value, the runtime identifies the value as a *connection string*, which typically includes a secret. The details of a connection string depend on the service to which you connect.

However, a connection name can also refer to a collection of multiple configuration items, useful for configuring [identity-based connections](#configure-an-identity-based-connection). Environment variables can be treated as a collection by using a shared prefix that ends in double underscores `__`

. The group can then be referenced by setting the connection name to this prefix.

For example, the `connection`

property for an Azure Blob trigger definition might be `Storage1`

. As long as there's no single string value configured by an environment variable named `Storage1`

, an environment variable named `Storage1__blobServiceUri`

could be used to inform the `blobServiceUri`

property of the connection. The connection properties are different for each service. Refer to the documentation for the component that uses the connection.

Note

When using [Azure App Configuration](../azure-app-configuration/quickstart-azure-functions-csharp) or [Key Vault](/en-us/azure/key-vault/general/overview) to provide settings for Managed Identity connections, setting names should use a valid key separator such as `:`

or `/`

in place of the `__`

to ensure names are resolved correctly.

For example, `Storage1:blobServiceUri`

.

### Configure an identity-based connection

Some connections in Azure Functions can be configured to use an identity instead of a secret. Support depends on the runtime version and the extension using the connection. In some cases, a connection string may still be required in Functions even though the service to which you're connecting supports identity-based connections. For a tutorial on configuring your function apps with managed identities, see the [creating a function app with identity-based connections tutorial](functions-identity-based-connections-tutorial).

Note

When running in a Consumption or Elastic Premium plan, your app uses the [ WEBSITE_AZUREFILESCONNECTIONSTRING](functions-app-settings#website_contentazurefileconnectionstring) and

[settings when connecting to Azure Files on the storage account used by your function app. Azure Files doesn't support using managed identity when accessing the file share. For more information, see](functions-app-settings#website_contentshare)

`WEBSITE_CONTENTSHARE`

[Azure Files supported authentication scenarios](../storage/files/storage-files-active-directory-overview#supported-authentication-scenarios)

Identity-based connections are only supported on Functions 4.x, If you are using version 1.x, you must first [migrate to version 4.x](migrate-version-1-version-4).

The following components support identity-based connections:

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

Choose one of these tabs to learn about permissions for each component:

-
[Azure Blobs extension](#tabpanel_1_blob) -
[Azure Queues extension](#tabpanel_1_queue) -
[Azure Tables extension](#tabpanel_1_table) -
[Event Hubs extension](#tabpanel_1_eventhubs) -
[Service Bus extension](#tabpanel_1_servicebus) -
[Event Grid extension](#tabpanel_1_eventgrid) -
[Azure Cosmos DB extension](#tabpanel_1_cosmos) -
[Azure SignalR extension](#tabpanel_1_signalr) -
[Azure Web PubSub extension](#tabpanel_1_web-pubsub) -
[Durable Functions storage provider](#tabpanel_1_durable) -
[Functions host storage](#tabpanel_1_azurewebjobsstorage)

You need to create a role assignment that provides access to your blob container at runtime. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) aren't sufficient. The following table shows built-in roles that are recommended when using the Blob Storage extension in normal operation. Your application may require further permissions based on the code you write.

| Binding type | Example built-in roles |
|---|---|
| Trigger |
and
1Extra permissions must also be granted to the AzureWebJobsStorage connection. 2 |

[Storage Blob Data Reader](../role-based-access-control/built-in-roles#storage-blob-data-reader)[Storage Blob Data Owner](../role-based-access-control/built-in-roles#storage-blob-data-owner)1 The blob trigger handles failure across multiple retries by writing [poison blobs](functions-bindings-storage-blob-trigger#poison-blobs) to a queue on the storage account specified by the connection.

2 The AzureWebJobsStorage connection is used internally for blobs and queues that enable the trigger. If it's configured to use an identity-based connection, it needs extra permissions beyond the default requirement. The required permissions are covered by the [Storage Blob Data Owner](../role-based-access-control/built-in-roles#storage-blob-data-owner), [Storage Queue Data Contributor](../role-based-access-control/built-in-roles#storage-queue-data-contributor), and [Storage Account Contributor](../role-based-access-control/built-in-roles#storage-account-contributor) roles. To learn more, see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity).

#### Common properties for identity-based connections

An identity-based connection for an Azure service accepts the following common properties, where `<CONNECTION_NAME_PREFIX>`

is the value of your `connection`

property in the trigger or binding definition:

| Property | Environment variable template | Description |
|---|---|---|
| Token Credential | `<CONNECTION_NAME_PREFIX>__credential` |
This property determines how a token should be obtained for the connection. The property shouldn't be set in
`managedidentity` . When you intend to
`managedidentityasfederatedidentity` . |

`<CONNECTION_NAME_PREFIX>__clientId`

`credential`

is set to `managedidentity`

, this property can be set to specify the user-assigned identity to be used when obtaining a token. The property accepts a client ID corresponding to a user-assigned identity assigned to the application. It's invalid to specify both a resource ID and a client ID. If neither are specified, the system-assigned identity is used.This property is used differently in cross-tenant scenarios. See the

[cross-tenant scenarios](#connecting-to-a-resource-in-another-tenant)section.This property is used differently in

[local development scenarios](#local-development-with-identity-based-connections), when`credential`

shouldn't be set.`<CONNECTION_NAME_PREFIX>__managedIdentityResourceId`

`credential`

is set to `managedidentity`

, this property can be set to specify the user-assigned identity to be used when obtaining a token. The property accepts a resource identifier corresponding to a user-assigned identity assigned to the application. It's invalid to specify both a resource ID and a client ID. If neither are specified, the system-assigned identity is used.Other options may be supported for a given connection type. Refer to the documentation for the component making the connection.

##### Azure SDK Environment Variables

Caution

Use of the Azure SDK's [ EnvironmentCredential](/en-us/dotnet/api/azure.identity.environmentcredential) environment variables is not recommended due to the potentially unintentional impact on other connections. They also are not fully supported when deployed to Azure Functions.

The environment variables associated with the Azure SDK's [ EnvironmentCredential](/en-us/dotnet/api/azure.identity.environmentcredential) can also be set, but these are not processed by the Functions service for scaling in Consumption plans. These environment variables are not specific to any one connection and will apply as a default unless a corresponding property is not set for a given connection. For example, if

`AZURE_CLIENT_ID`

is set, this would be used as if `<CONNECTION_NAME_PREFIX>__clientId`

had been configured. Explicitly setting `<CONNECTION_NAME_PREFIX>__clientId`

would override this default.##### Local development with identity-based connections

Note

Local development with identity-based connections requires version `4.0.3904`

of [Azure Functions Core Tools](functions-run-local), or a later version.

When you're running your function project locally, the above configuration tells the runtime to use your local developer identity. The connection attempts to get a token from the following locations, in order:

- A local cache shared between Microsoft applications
- The current user context in Visual Studio
- The current user context in Visual Studio Code
- The current user context in the Azure CLI

If none of these options are successful, an error occurs.

Your identity may already have some role assignments against Azure resources used for development, but those roles may not provide the necessary data access. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) aren't sufficient. Double-check what permissions are required for connections for each component, and make sure that you have them assigned to yourself.

In some cases, you may wish to specify use of a different identity. You can add configuration properties for the connection that point to the alternate identity based on a client ID and client Secret for a Microsoft Entra service principal. **This configuration option is not supported when hosted in the Azure Functions service.** To use an ID and secret on your local machine, define the connection with the following extra properties:

| Property | Environment variable template | Description |
|---|---|---|
| Tenant ID | `<CONNECTION_NAME_PREFIX>__tenantId` |
The Microsoft Entra tenant (directory) ID. |
| Client ID | `<CONNECTION_NAME_PREFIX>__clientId` |
The client (application) ID of an app registration in the tenant. |
| Client secret | `<CONNECTION_NAME_PREFIX>__clientSecret` |
A client secret that was generated for the app registration. |

Here's an example of `local.settings.json`

properties required for identity-based connection to Azure Blobs:

```
{
"IsEncrypted": false,
"Values": {
"<CONNECTION_NAME_PREFIX>__blobServiceUri": "<blobServiceUri>",
"<CONNECTION_NAME_PREFIX>__queueServiceUri": "<queueServiceUri>",
"<CONNECTION_NAME_PREFIX>__tenantId": "<tenantId>",
"<CONNECTION_NAME_PREFIX>__clientId": "<clientId>",
"<CONNECTION_NAME_PREFIX>__clientSecret": "<clientSecret>"
}
}
```


#### Connecting to host storage with an identity

The Azure Functions host uses the storage connection set in [ AzureWebJobsStorage](functions-app-settings#azurewebjobsstorage) to enable core behaviors such as coordinating singleton execution of timer triggers and default app key storage. This connection can also be configured to use an identity.

Caution

Other components in Functions rely on `AzureWebJobsStorage`

for default behaviors. You should not move it to an identity-based connection if you are using older versions of extensions that do not support this type of connection, including triggers and bindings for Azure Blobs, Event Hubs, and Durable Functions. Similarly, `AzureWebJobsStorage`

is used for deployment artifacts when using server-side build in Linux Consumption, and if you enable this, you will need to deploy via [an external deployment package](run-functions-from-deployment-package).

In addition, your function app might be reusing `AzureWebJobsStorage`

for other storage connections in their triggers, bindings, and/or function code. Make sure that all uses of `AzureWebJobsStorage`

are able to use the identity-based connection format before changing this connection from a connection string.

To use an identity-based connection for `AzureWebJobsStorage`

, configure the following app settings:

| Setting | Description | Example value |
|---|---|---|
`AzureWebJobsStorage__blobServiceUri` |
The data plane URI of the blob service of the storage account, using the HTTPS scheme. | https://<storage_account_name>.blob.core.windows.net |
`AzureWebJobsStorage__queueServiceUri` |
The data plane URI of the queue service of the storage account, using the HTTPS scheme. | https://<storage_account_name>.queue.core.windows.net |
`AzureWebJobsStorage__tableServiceUri` |
The data plane URI of a table service of the storage account, using the HTTPS scheme. | https://<storage_account_name>.table.core.windows.net |

[Common properties for identity-based connections](#common-properties-for-identity-based-connections) may also be set as well.

If you're configuring `AzureWebJobsStorage`

using a storage account that uses the default DNS suffix and service name for global Azure, following the `https://<accountName>.[blob|queue|file|table].core.windows.net`

format, you can instead set `AzureWebJobsStorage__accountName`

to the name of your storage account. The endpoints for each storage service are inferred for this account. This doesn't work when the storage account is in a sovereign cloud or has a custom DNS.

| Setting | Description | Example value |
|---|---|---|
`AzureWebJobsStorage__accountName` |
The account name of a storage account, valid only if the account isn't in a sovereign cloud and doesn't have a custom DNS. This syntax is unique to `AzureWebJobsStorage` and can't be used for other identity-based connections. |
<storage_account_name> |

You need to create a role assignment that provides access to the storage account for "AzureWebJobsStorage" at runtime. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) aren't sufficient. The [Storage Blob Data Owner](../role-based-access-control/built-in-roles#storage-blob-data-owner) role covers the basic needs of Functions host storage - the runtime needs both read and write access to blobs and the ability to create containers. Several extensions use this connection as a default location for blobs, queues, and tables, and these uses may add requirements as noted in the table below. You may also need other permissions if you use "AzureWebJobsStorage" for any other purposes.

| Extension | Roles required | Explanation |
|---|---|---|
No extension (host only) |
|

This scenario represents the minimum set of permissions for normal operation, but it doesn't include support for diagnostic events

1.*No extension (host only), with support for diagnostic events*1[Storage Blob Data Owner](../role-based-access-control/built-in-roles#storage-blob-data-owner),[Storage Table Data Contributor](../role-based-access-control/built-in-roles#storage-table-data-contributor)[Storage Account Contributor](../role-based-access-control/built-in-roles#storage-account-contributor),[Storage Blob Data Owner](../role-based-access-control/built-in-roles#storage-blob-data-owner),[Storage Queue Data Contributor](../role-based-access-control/built-in-roles#storage-queue-data-contributor)[blob receipts](functions-bindings-storage-blob-trigger#blob-receipts). It uses the AzureWebJobsStorage connection for these purposes, regardless of the connection configured for the trigger.[Storage Blob Data Owner](../role-based-access-control/built-in-roles#storage-blob-data-owner)[Storage Blob Data Owner](../role-based-access-control/built-in-roles#storage-blob-data-owner)[Storage Blob Data Contributor](../role-based-access-control/built-in-roles#storage-blob-data-contributor),[Storage Queue Data Contributor](../role-based-access-control/built-in-roles#storage-queue-data-contributor),[Storage Table Data Contributor](../role-based-access-control/built-in-roles#storage-table-data-contributor)[Durable Functions extension configuration](durable/durable-functions-bindings#host-json).1 For some types of issues, Azure Functions can raise a diagnostic event that can assist with troubleshooting, even when the issue prevents the function app from starting. If [Storage Table Data Contributor](../role-based-access-control/built-in-roles#storage-table-data-contributor) isn't assigned, you might see warnings in your logs about the inability to write these events.

#### Connecting to a resource in another tenant

If your function needs to connect to a resource in a different Microsoft Entra tenant, your connection needs to use a *federated identity credential*. This requires a user-assigned managed identity and a multi-tenant Entra ID app registration. You cannot use a system-assigned managed identity for cross-tenant connections.

Important

When you configure a trigger for a cross-tenant connection in the Consumption or Flex Consumption plan types, the platform no longer scales the function app based on that trigger.

To configure a cross-tenant identity-based connection, you first need to set up your infrastructure using the following steps:

- In the tenant where your function app is deployed,
[create a new user-assigned managed identity](/en-us/entra/identity/managed-identities-azure-resources/how-manage-user-assigned-managed-identities#create-a-user-assigned-managed-identity). [Assign that identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json#add-a-user-assigned-identity)to the function app.- In the same tenant,
[create a multi-tenant Entra app registration](/en-us/entra/workload-id/workload-identity-federation-config-app-trust-managed-identity#configure-a-multi-tenant-app-registration)that represents the cross-tenant resource you want to access. [Add the managed identity as a federated identity credential for the app registration.](/en-us/entra/workload-id/workload-identity-federation-config-app-trust-managed-identity)- In the tenant where the resource is deployed,
[create an enterprise application for the app registration](/en-us/entra/identity/enterprise-apps/create-service-principal-cross-tenant). - Assign permissions for the enterprise application to access the resource.

A cross-tenant identity-based connection uses the following properties, where `<CONNECTION_NAME_PREFIX>`

is the value of your `connection`

property in the trigger or binding definition:

| Property | Environment variable template | Description |
|---|---|---|
| Token Credential | `<CONNECTION_NAME_PREFIX>__credential` |
Required. When connecting to a resource in another tenant, set this property to `managedidentityasfederatedidentity` . |
| Azure Cloud | `<CONNECTION_NAME_PREFIX>__azureCloud` |
Required. This property determines the Azure cloud environment. Allowed values are "public" for Azure Public Cloud, "usgov" for Azure US Government Cloud, and "china" for Azure operated by 21Vianet. |
| Client ID | `<CONNECTION_NAME_PREFIX>__clientId` |
Required. When `credential` is set to `managedidentityasfederatedidentity` , set this property to the client ID (app ID) of the app registration.This property is used differently in single-tenant identity-based connections. See the
This property is used differently in
`credential` shouldn't be set. |
| Tenant ID | `<CONNECTION_NAME_PREFIX>__tenantId` |
Required. When `credential` is set to `managedidentityasfederatedidentity` , set this property to the tenant ID of the resource tenant.This property is used differently in
`credential` shouldn't be set. |
| Managed Identity Client ID | `<CONNECTION_NAME_PREFIX>__managedIdentityClientId` |
When `credential` is set to `managedidentityasfederatedidentity` , this property specifies the user-assigned identity that you configured as a federated identity credential and assigned to the application.1 The property accepts a client ID corresponding to that user-assigned identity. |
| Managed Identity Object ID | `<CONNECTION_NAME_PREFIX>__managedIdentityObjectId` |
When `credential` is set to `managedidentityasfederatedidentity` , this property specifies the user-assigned identity that you configured as a federated identity credential and assigned to the application.1 The property accepts an object ID (principal ID) corresponding to that user-assigned identity. |
| Managed Identity Resource ID | `<CONNECTION_NAME_PREFIX>__managedIdentityResourceId` |
When `credential` is set to `managedidentityasfederatedidentity` , this property specifies the user-assigned identity that you configured as a federated identity credential and assigned to the application.1 The property accepts a resource identifier corresponding to that user-assigned identity. |

1 When `credential`

is set to `managedidentityasfederatedidentity`

, your connection must specify exactly one of `managedIdentityClientId`

, `managedIdentityObjectId`

, or `managedIdentityResourceId`

.

This is also [documented by the Azure SDK](/en-us/dotnet/azure/sdk/authentication/create-token-credentials-from-configuration?tabs=client-id#managed-identity-as-a-federated-identity-credential) in a JSON format.

## Reporting Issues

| Item | Description | Link |
|---|---|---|
| Runtime | Script Host, Triggers & Bindings, Language Support |
|

[File an Issue](https://github.com/Azure/azure-webjobs-sdk-templates/issues)## Open source repositories

The code for Azure Functions is open source, and you can find key components in these GitHub repositories:

## Next steps

For more information, see the following resources:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/monitor-functions-opentelemetry-distributed-tracing -->

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

This article currently doesn't support PowerShell.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

[Java Developer Kit (JDK)](/en-us/azure/developer/java/fundamentals/java-support-on-azure), version 11 or later[Apache Maven](https://maven.apache.org/), version 3.0 or later

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

command in an empty folder:`azd init --template functions-quickstart-javascript-azd-otel -e flexquickstart-otel`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-javascript-azd-otel)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name also appears in the name of the resource group you create in Azure.

In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-dotnet-azd-otel -e flexquickstart-otel`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-otel)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name also appears in the name of the resource group you create in Azure.

In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-java-azd-otel -e flexquickstart-otel`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-java-azd-otel)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name also appears in the name of the resource group you create in Azure.

## Review the code

The template creates a complete distributed tracing scenario with three functions that work together. Review the key OpenTelemetry-related aspects.

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

The `host.json`

file enables OpenTelemetry for the Functions host:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
},
"telemetryMode": "OpenTelemetry"
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

The `src/otel-sample/package.json`

file includes the necessary packages for OpenTelemetry integration:

```
{
"dependencies": {
"@azure/functions": "4.7.0",
"@azure/functions-opentelemetry-instrumentation": "^0.2.0",
"@azure/monitor-opentelemetry-exporter": "^1.0.0-beta.32",
"@opentelemetry/api": "^1.9.0",
"@opentelemetry/auto-instrumentations-node": "^0.67.0",
"axios": "^1.12.0"
}
}
```


The `@azure/functions-opentelemetry-instrumentation`

and `@azure/monitor-opentelemetry-exporter`

packages provide the OpenTelemetry integration with Application Insights. The `@opentelemetry/auto-instrumentations-node`

package provides automatic instrumentation for Node.js libraries.

The `.csproj`

file includes the necessary packages for OpenTelemetry integration:

```
<PackageReference Include="Azure.Monitor.OpenTelemetry.Exporter" Version="1.4.0" />
<PackageReference Include="Microsoft.Azure.Functions.Worker.OpenTelemetry" Version="1.4.0" />
<PackageReference Include="OpenTelemetry.Instrumentation.Http" Version="1.10.0" />
```


These packages provide the OpenTelemetry integration with Application Insights and HTTP instrumentation for distributed tracing.

The `pom.xml`

file includes the necessary dependencies for OpenTelemetry integration:

```
<dependency>
<groupId>com.microsoft.azure.functions</groupId>
<artifactId>azure-functions-java-library</artifactId>
<version>3.1.0</version>
</dependency>
<dependency>
<groupId>com.microsoft.azure.functions</groupId>
<artifactId>azure-functions-java-opentelemetry</artifactId>
<version>1.1.0</version>
</dependency>
<dependency>
<groupId>io.opentelemetry</groupId>
<artifactId>opentelemetry-api</artifactId>
<version>1.49.0</version>
</dependency>
```


The `azure-functions-java-opentelemetry`

package provides the OpenTelemetry integration, while the `opentelemetry-api`

package provides the core OpenTelemetry API for distributed tracing.

The project also uses the Maven dependency plugin to download the OpenTelemetry Java agent during the build process:

```
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-dependency-plugin</artifactId>
<version>3.6.0</version>
<executions>
<execution>
<id>copy-otel-agent</id>
<phase>package</phase>
<goals>
<goal>copy</goal>
</goals>
<configuration>
<artifactItems>
<artifactItem>
<groupId>io.opentelemetry.javaagent</groupId>
<artifactId>opentelemetry-javaagent</artifactId>
<version>2.11.0</version>
<type>jar</type>
<outputDirectory>${project.build.directory}/azure-functions/${functionAppName}</outputDirectory>
<destFileName>opentelemetry-javaagent.jar</destFileName>
</artifactItem>
</artifactItems>
</configuration>
</execution>
</executions>
</plugin>
```


This agent is automatically attached to the Java runtime for distributed tracing instrumentation.

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


The OpenTelemetry configuration is set up in `src/otel-sample/src/index.js`

:

```
const { AzureFunctionsInstrumentation } = require('@azure/functions-opentelemetry-instrumentation');
const { AzureMonitorLogExporter, AzureMonitorTraceExporter } = require('@azure/monitor-opentelemetry-exporter');
const { getNodeAutoInstrumentations, getResourceDetectors } = require('@opentelemetry/auto-instrumentations-node');
const { registerInstrumentations } = require('@opentelemetry/instrumentation');
const { detectResources } = require('@opentelemetry/resources');
const { LoggerProvider, SimpleLogRecordProcessor } = require('@opentelemetry/sdk-logs');
const { NodeTracerProvider, SimpleSpanProcessor } = require('@opentelemetry/sdk-trace-node');
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
const { app } = require("@azure/functions");
const axios = require("axios");
async function firstHttpFunction(request, context) {
context.log("JavaScript HTTP trigger function (first) processed a request.");
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
context.log("Successfully called second function");
return {
status: 200,
body: JSON.stringify(result),
headers: { "Content-Type": "application/json" },
};
} catch (error) {
context.log("Error occurred:", error);
return {
status: 500,
body: JSON.stringify({ error: "Failed to process request" }),
};
}
}
app.http("first_http_function", {
methods: ["GET", "POST"],
authLevel: "anonymous",
handler: firstHttpFunction,
});
```


#### Second HTTP Function

```
const { app, output } = require("@azure/functions");
const serviceBusOutput = output.serviceBusQueue({
queueName: "%ServiceBusQueueName%",
connection: "ServiceBusConnection",
});
async function secondHttpFunction(request, context) {
context.log("JavaScript HTTP trigger function (second) processed a request.");
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
app.http("second_http_function", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs: [serviceBusOutput],
handler: secondHttpFunction,
});
```


#### Service Bus Queue Trigger

```
const { app } = require("@azure/functions");
async function serviceBusQueueTrigger(message, context) {
context.log(
"JavaScript ServiceBus Queue trigger start processing a message:",
message
);
// Simulate processing time
await new Promise((resolve) => setTimeout(resolve, 5000));
context.log("JavaScript ServiceBus Queue trigger end processing a message");
}
app.serviceBusQueue("servicebus_queue_trigger", {
queueName: "%ServiceBusQueueName%",
connection: "ServiceBusConnection",
handler: serviceBusQueueTrigger,
});
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


You define the functions in separate Java class files under `src/main/java/com/function`

:

#### First HTTP Function

```
public class FirstHttpTrigger {
@FunctionName("first_http_function")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<String> request,
final ExecutionContext context) {
context.getLogger().info("first_http_function function processed a request.");
// Build base URI from the incoming request
URI requestUri = request.getUri();
String incomingUrl = requestUri.toString();
String baseUrl = incomingUrl.split("/api/")[0] + "/api";
String targetUri = baseUrl + "/second_http_function";
try {
var client = HttpClient.newBuilder()
.connectTimeout(Duration.ofSeconds(5))
.build();
var requestBuilder = HttpRequest.newBuilder(URI.create(targetUri))
.timeout(Duration.ofSeconds(60))
.GET();
// Get trace context from ExecutionContext and propagate it
TraceContext traceContext = context.getTraceContext();
if (traceContext != null) {
String traceparent = traceContext.getTraceparent();
String tracestate = traceContext.getTracestate();
if (traceparent != null && !traceparent.isEmpty()) {
context.getLogger().info("Propagating traceparent: " + traceparent);
requestBuilder.header("traceparent", traceparent);
}
if (tracestate != null && !tracestate.isEmpty()) {
requestBuilder.header("tracestate", tracestate);
}
}
var httpReq = requestBuilder.build();
var resp = client.send(httpReq, HttpResponse.BodyHandlers.ofString());
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "text/plain")
.body("Called second_http_function, status: " + resp.statusCode() + ", content: " + resp.body())
.build();
} catch (Exception e) {
context.getLogger().severe("Call to second_http_function failed: " + e);
return request.createResponseBuilder(HttpStatus.INTERNAL_SERVER_ERROR)
.body("Failed to call second_http_function: " + e.getMessage())
.build();
}
}
}
```


#### Second HTTP Function

```
public class SecondHttpTrigger {
@FunctionName("second_http_function")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<String> request,
@ServiceBusQueueOutput(
name = "message",
queueName = "%ServiceBusQueueName%",
connection = "ServiceBusConnection")
OutputBinding<String[]> serviceBusMessages,
final ExecutionContext context) {
context.getLogger().info("second_http_function function processed a request.");
// Send message to Service Bus queue
serviceBusMessages.setValue(new String[] { "Hello" });
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "text/plain")
.body("Hello from second_http_function!")
.build();
}
}
```


#### Service Bus Queue Trigger

```
public class ServiceBusQueueTriggerFunction {
@FunctionName("servicebus_queue_trigger")
public void run(
@ServiceBusQueueTrigger(
name = "message",
queueName = "%ServiceBusQueueName%",
connection = "ServiceBusConnection")
String message,
final ExecutionContext context
) {
context.getLogger().info("Message Body: " + message);
}
}
```


### Distributed tracing flow

This architecture creates a complete distributed tracing scenario, with this behavior:

**First HTTP function**receives an HTTP request and calls the second HTTP function**Second HTTP function**responds and sends a message to Service Bus**Service Bus trigger**processes the message with a delay to simulate processing work

Key aspects of the OpenTelemetry implementation:

**OpenTelemetry integration**: The`index.js`

file configures OpenTelemetry with Azure Monitor exporters for traces and logs**Function chaining**: The first function calls the second using axios with automatic trace propagation**Service Bus integration**: The second function outputs to Service Bus using output bindings, which triggers the third function**Managed identity**: All Service Bus connections use managed identity instead of connection strings**Processing simulation**: The 5-second delay in the Service Bus trigger simulates message processing work

You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-javascript-azd-otel).

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

**OpenTelemetry integration**: The`host.json`

file enables OpenTelemetry with`"telemetryMode": "OpenTelemetry"`

and the OpenTelemetry Java agent is packaged with the deployment**Function chaining**: The first function calls the second using Java's built-in HttpClient with manual trace context propagation**Trace context propagation**: The`TraceContext`

from`ExecutionContext`

provides`traceparent`

and`tracestate`

headers for W3C trace context propagation**Service Bus integration**: The second function outputs to Service Bus using output bindings, which triggers the third function

You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-java-azd-otel).

After you verify your functions locally, it's time to publish them to Azure.

## Deploy to Azure

This project is configured to use the `azd up`

command to deploy this project to a new function app in a Flex Consumption plan in Azure with OpenTelemetry support.

Tip

This project includes a set of Bicep files that `azd`

uses to create a secure deployment to a Flex consumption plan that follows best practices, including managed identity connections.

Run the command to have

`azd`

create the required Azure resources in Azure and deploy your code project to the new function app:`azd up`

The root folder contains the

`azure.yaml`

definition file required by`azd`

.If you're not already signed in, you're asked to authenticate by using your Azure account.

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

You can invoke your function endpoints in Azure by making HTTP requests to their URLs. Since the HTTP functions in this template are configured with anonymous access, you don't need any function keys.

In your local terminal or command prompt, run this command to get the function app name and construct the URL:

`APP_NAME=$(azd env get-value AZURE_FUNCTION_NAME) echo "Function URL: https://$APP_NAME.azurewebsites.net/api/first_http_function"`

The

`azd env get-value`

command gets your function app name from the local environment.Test the function in your browser by going to the URL:

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

prompts and any environment variables that `azd`

generates are stored locally in your named environment. Use the `azd env get-values`

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/set-runtime-version -->

# How to target Azure Functions runtime versions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

A function app runs on a specific version of the Azure Functions runtime. By default, function apps are created in the latest 4.x version of the Functions runtime. Your function apps are supported only when they run on a [supported major version](functions-versions). This article explains how to configure a function app in Azure to target, or *pin* to, a specific version when required.

The way that you target a specific version depends on whether you're running Windows or Linux. This version of the article supports Windows. Choose your operating system at the top of the article.

The way that you target a specific version depends on whether you're running Windows or Linux. This version of the article supports Linux. Choose your operating system at the top of the article.

Important

When possible, always run your functions on the latest supported version of the Azure Functions runtime. You should only pin your app to a specific version if you're instructed to do so due to an issue with the latest version. Always move up to the latest runtime version as soon as your functions can run correctly.

During local development, your installed version of Azure Functions Core Tools must match the major runtime version used by the function app in Azure. For more information, see [Core Tools versions](functions-run-local#v2).

## Update your runtime version

When possible, you should always run your function apps on the latest supported version of the Azure Functions runtime. If your function app is currently running on an older version of the runtime, you should migrate your app to version 4.x

When your app has existing functions, you must take precautions before moving to a later major runtime version. The following articles detail breaking changes between major versions, including language-specific breaking changes. They also provide you with step-by-step instructions for a successful migration of your existing function app.

To determine your current runtime version, see [View the current runtime version](#view-the-current-runtime-version).

## View the current runtime version

You can view the current runtime version of your function app in one of these ways:

To view and update the runtime version currently used by a function app, follow these steps:

In the

[Azure portal](https://portal.azure.com), browse to your function app.Expand

**Settings**, and then select**Configuration**.In the

**Function runtime settings**tab, note the**Runtime version**. In this example, the version is set to`~4`

.

## Pin to a specific version

Azure Functions lets you use the `FUNCTIONS_EXTENSION_VERSION`

app setting to target the runtime version used by a given function app. If you specify only the major version (`~4`

), the function app is automatically updated to new minor versions of the runtime as they become available. Minor version updates are done automatically because new minor versions aren't likely to introduce changes that would break your functions.

Linux apps use the [ linuxFxVersion site setting](functions-app-settings#linuxfxversion) along with

`FUNCTIONS_EXTENSION_VERSION`

to determine the correct Linux base image in which to run your functions. When you create a new function app on Linux, the runtime automatically chooses the correct base image for you based on the runtime version of your language stack.Pinning to a specific runtime version causes your function app to restart.

When you specify a specific minor version (such as `4.0.12345`

) in `FUNCTIONS_EXTENSION_VERSION`

, the function app is pinned to that specific version of the runtime until you explicitly choose to move back to automatic version updates. You should only pin to a specific minor version long enough to resolve any issues with your function app that prevent you from targeting the major version. Older minor versions are regularly removed from the production environment. When your function app is pinned to a minor version that is later removed, your function app is instead run on the closest existing version instead of the version set in `FUNCTIONS_EXTENSION_VERSION`

. Minor version removals are announced in [App Service announcements](https://github.com/Azure/app-service-announcements/issues).

Note

When you try to publish from Visual Studio to an app that is pinned to a specific minor version of the runtime, a dialog prompts you to update to the latest version or cancel the publish. To avoid this check when you must use a specific minor version, add the `<DisableFunctionExtensionVersionUpdate>true</DisableFunctionExtensionVersionUpdate>`

property in your `.csproj`

file.

Use one of these methods to temporarily pin your app to a specific version of the runtime:

To view and update the runtime version currently used by a function app, follow these steps:

In the

[Azure portal](https://portal.azure.com), browse to your function app.Expand

**Settings**, and then select**Configuration**.In the

**Function runtime settings**tab, note the**Runtime version**. In this example, the version is set to`~4`

.

To pin your app to a specific minor version, in the left pane, expand

**Settings**, and then select**Environment variables**.From the

**App settings**tab, select**FUNCTIONS_EXTENSION_VERSION**, change**Value**to your required minor version, and then select**Apply**.Select

**Apply**, and then select**Confirm**to apply the changes and restart the app.

The function app restarts after the change is made to the application setting.

To pin your function app to a specific runtime version on Linux, you set a version-specific base image URL in the [ linuxFxVersion site setting](functions-app-settings#linuxfxversion) in the format

`DOCKER|<PINNED_VERSION_IMAGE_URI>`

.Important

Pinned function apps on Linux don't receive regular security and host functionality updates. Unless recommended by a support professional, use the [ FUNCTIONS_EXTENSION_VERSION](functions-app-settings#functions_extension_version) setting and a standard

[value for your language and version, such as](functions-app-settings#linuxfxversion)

`linuxFxVersion`

`Python|3.12`

. For valid values, see the [.](functions-app-settings#linuxfxversion)

`linuxFxVersion`

reference articlePinning to a specific runtime isn't currently supported for Linux function apps running in a Consumption plan.

The following example shows the [ linuxFxVersion](functions-app-settings#linuxfxversion) value required to pin a Node.js 16 function app to a specific runtime version of 4.14.0.3:

`DOCKER|mcr.microsoft.com/azure-functions/node:4.14.0.3-node16`


When needed, a support professional can provide you with a valid base image URI for your application.

Use the following Azure CLI commands to view and set the [ linuxFxVersion](functions-app-settings#linuxfxversion). You can't currently set

[in the portal or by using Azure PowerShell:](functions-app-settings#linuxfxversion)

`linuxFxVersion`

To view the current runtime version, use the

[az functionapp config show](/en-us/cli/azure/functionapp/config)command:`az functionapp config show --name <function_app> \ --resource-group <my_resource_group> --query 'linuxFxVersion' -o tsv`

In this code, replace

`<function_app>`

with the name of your function app. Also, replace`<my_resource_group>`

with the name of the resource group for your function app. The current value ofis returned.`linuxFxVersion`

To update the

setting in the function app, use the`linuxFxVersion`

[az functionapp config set](/en-us/cli/azure/functionapp/config)command:`az functionapp config set --name <FUNCTION_APP> \ --resource-group <RESOURCE_GROUP> \ --linux-fx-version <LINUX_FX_VERSION>`

Replace

`<FUNCTION_APP>`

with the name of your function app. Also, replace`<RESOURCE_GROUP>`

with the name of the resource group for your function app. Finally, replace`<LINUX_FX_VERSION>`

with the value of a specific image provided to you by a support professional.

You can run these commands from the [Azure Cloud Shell](../cloud-shell/overview) by choosing **Open Cloud Shell** in the preceding code examples. You can also use the [Azure CLI locally](/en-us/cli/azure/install-azure-cli) to execute this command after executing [ az login](/en-us/cli/azure/reference-index#az-login) to sign in.

The function app restarts after the change is made to the site config.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai-assistantquery-input -->

# Azure OpenAI assistant query input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Azure OpenAI extension for Azure Functions is currently in preview.

The Azure OpenAI assistant query input binding allows you to integrate Assistants API queries into your code executions.

For information on setup and configuration details of the Azure OpenAI extension, see [Azure OpenAI extensions for Azure Functions](functions-bindings-openai). To learn more about Azure OpenAI assistants, see [Azure OpenAI Assistants API](/en-us/azure/ai-services/openai/concepts/assistants).

Note

References and examples are only provided for the [Node.js v4 model](functions-reference-node?pivots=nodejs-model-v4).

Note

References and examples are only provided for the [Python v2 model](functions-reference-python?pivots=python-mode-decorators#programming-model).

Note

While both C# process models are supported, only [isolated worker model](dotnet-isolated-process-guide) examples are provided.

## Example

This example demonstrates the creation process, where the HTTP GET function that queries the conversation history of the assistant chat bot. The response to the prompt is returned in the HTTP response.

```
/// <summary>
/// HTTP GET function that queries the conversation history of the assistant chat bot.
/// </summary>
[Function(nameof(GetChatState))]
public static IActionResult GetChatState(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "assistants/{assistantId}")] HttpRequestData req,
string assistantId,
[AssistantQueryInput("{assistantId}", TimestampUtc = "{Query.timestampUTC}", ChatStorageConnectionSetting = DefaultChatStorageConnectionSetting, CollectionName = DefaultCollectionName)] AssistantState state)
{
return new OkObjectResult(state);
}
```


This example demonstrates the creation process, where the HTTP GET function that queries the conversation history of the assistant chat bot. The response to the prompt is returned in the HTTP response.

```
/*
* HTTP GET function that queries the conversation history of the assistant chat bot.
*/
@FunctionName("GetChatState")
public HttpResponseMessage getChatState(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "assistants/{assistantId}")
HttpRequestMessage<Optional<String>> request,
@BindingName("assistantId") String assistantId,
@AssistantQuery(name = "AssistantState", id = "{assistantId}", timestampUtc = "{Query.timestampUTC}", chatStorageConnectionSetting = DEFAULT_CHATSTORAGE, collectionName = DEFAULT_COLLECTION) AssistantState state,
final ExecutionContext context) {
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(state)
.build();
}
```


This example demonstrates the creation process, where the HTTP GET function that queries the conversation history of the assistant chat bot. The response to the prompt is returned in the HTTP response.

```
const { app, input, output } = require("@azure/functions");
const chatBotQueryInput = input.generic({
type: 'assistantQuery',
id: '{assistantId}',
timestampUtc: '{Query.timestampUTC}',
chatStorageConnectionSetting: CHAT_STORAGE_CONNECTION_SETTING,
collectionName: COLLECTION_NAME
})
app.http('GetChatState', {
methods: ['GET'],
route: 'assistants/{assistantId}',
authLevel: 'anonymous',
extraInputs: [chatBotQueryInput],
handler: async (_, context) => {
const state = context.extraInputs.get(chatBotQueryInput)
return { status: 200, jsonBody: state }
}
})
```


This example demonstrates the creation process, where the HTTP GET function that queries the conversation history of the assistant chat bot. The response to the prompt is returned in the HTTP response.

```
import { HttpRequest, InvocationContext, app, input, output } from "@azure/functions"
const chatBotQueryInput = input.generic({
type: 'assistantQuery',
id: '{assistantId}',
timestampUtc: '{Query.timestampUTC}',
chatStorageConnectionSetting: CHAT_STORAGE_CONNECTION_SETTING,
collectionName: COLLECTION_NAME
})
app.http('GetChatState', {
methods: ['GET'],
route: 'assistants/{assistantId}',
authLevel: 'anonymous',
extraInputs: [chatBotQueryInput],
handler: async (_, context) => {
const state: any = context.extraInputs.get(chatBotQueryInput)
return { status: 200, jsonBody: state }
}
})
```


This example demonstrates the creation process, where the HTTP GET function that queries the conversation history of the assistant chat bot. The response to the prompt is returned in the HTTP response.

Here's the *function.json* file for Get Chat State:

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
"get"
]
},
{
"type": "http",
"direction": "out",
"name": "Response"
},
{
"name": "State",
"type": "assistantQuery",
"direction": "in",
"dataType": "string",
"id": "{assistantId}",
"timestampUtc": "{Query.timestampUTC}",
"chatStorageConnectionSetting": "AzureWebJobsStorage",
"collectionName": "ChatState"
}
]
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

```
using namespace System.Net
param($Request, $TriggerMetadata, $State)
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $State
Headers = @{
"Content-Type" = "application/json"
}
})
```


This example demonstrates the creation process, where the HTTP GET function that queries the conversation history of the assistant chat bot. The response to the prompt is returned in the HTTP response.

```
@apis.function_name("GetChatState")
@apis.route(route="assistants/{assistantId}", methods=["GET"])
@apis.assistant_query_input(
arg_name="state",
id="{assistantId}",
timestamp_utc="{Query.timestampUTC}",
chat_storage_connection_setting=DEFAULT_CHAT_STORAGE_SETTING,
collection_name=DEFAULT_CHAT_COLLECTION_NAME,
)
def get_chat_state(req: func.HttpRequest, state: str) -> func.HttpResponse:
return func.HttpResponse(state, status_code=200, mimetype="application/json")
```


## Attributes

Apply the `AssistantQuery`

attribute to define an assistant query input binding, which supports these parameters:

| Parameter | Description |
|---|---|
Id |
Gets the ID of the assistant to query. |
TimeStampUtc |
Optional. Gets or sets the timestamp of the earliest message in the chat history to fetch. The timestamp should be in ISO 8601 format - for example, 2023-08-01T00:00:00Z. |

## Annotations

The `assistantQuery`

annotation enables you to define an assistant query input binding, which supports these parameters:

| Element | Description |
|---|---|
name |
Gets or sets the name of the input binding. |
id |
Gets the ID of the assistant to query. |
timeStampUtc |
Optional. Gets or sets the timestamp of the earliest message in the chat history to fetch. The timestamp should be in ISO 8601 format - for example, 2023-08-01T00:00:00Z. |

## Decorators

During the preview, define the input binding as a `generic_input_binding`

binding of type `assistantQuery`

, which supports these parameters:

| Parameter | Description |
|---|---|
arg_name |
The name of the variable that represents the binding parameter. |
id |
Gets the ID of the assistant to query. |
time_stamp_utc |
Optional. Gets or sets the timestamp of the earliest message in the chat history to fetch. The timestamp should be in ISO 8601 format - for example, 2023-08-01T00:00:00Z. |

## Configuration

The binding supports these configuration properties that you set in the function.json file.

| Property | Description |
|---|---|
type |
Must be `assistantQuery` . |
direction |
Must be `in` . |
name |
The name of the input binding. |
id |
Gets the ID of the assistant to query. |
timeStampUtc |
Optional. Gets or sets the timestamp of the earliest message in the chat history to fetch. The timestamp should be in ISO 8601 format - for example, 2023-08-01T00:00:00Z. |

## Configuration

The binding supports these properties, which are defined in your code:

| Property | Description |
|---|---|
id |
Gets the ID of the assistant to query. |
timeStampUtc |
Optional. Gets or sets the timestamp of the earliest message in the chat history to fetch. The timestamp should be in ISO 8601 format - for example, 2023-08-01T00:00:00Z. |

## Usage

See the [Example section](#example) for complete examples.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/legacy-proxies -->

# Work with legacy proxies

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Azure Functions proxies is a legacy feature for [versions 1.x through 3.x](functions-versions) of the Azure Functions runtime. Proxies can be re-enabled temporarily in version 4.x for you to successfully upgrade your function apps to the latest runtime version. As soon as possible, you should switch to integrating your function apps with Azure API Management. API Management lets you take advantage of a more complete set of features for defining, securing, managing, and monetizing your Functions-based APIs. For more information, see [API Management integration](functions-proxies#api-management-integration).

To learn how to temporarily re-enable proxies support in Functions version 4.x, see [Re-enable proxies in Functions v4.x](legacy-proxies#re-enable-proxies-in-functions-v4x).

To help make it easier to migrate from existing proxy implementations, this article links to equivalent API Management content, when available.


This article explains how to configure and work with Azure Functions Proxies. With this feature, you can specify endpoints on your function app that are implemented by another resource. You can use these proxies to break a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.

Standard Functions billing applies to proxy executions. For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).

## Re-enable proxies in Functions v4.x

After [migrating your function app to version 4.x of the Functions runtime](migrate-version-3-version-4), you'll need to specifically reenable proxies. You should still switch to integrating your function apps with [Azure API Management](functions-proxies#api-management-integration) as soon as possible, and not just rely on proxies.

Re-enabling proxies requires you to set a flag in the `AzureWebJobsFeatureFlags`

application setting in one of the following ways:

If the

`AzureWebJobsFeatureFlags`

setting doesn't already exists, add this setting to your function app with a value of`EnableProxies`

.If this setting already exists, add

`,EnableProxies`

to the end of the existing value.

[ AzureWebJobsFeatureFlags](functions-app-settings#azurewebjobsfeatureflags) is a comma-delimited array of flags used to enable preview and other temporary features. To learn more about how to create and modify application settings, see

[Work with application settings](functions-how-to-use-azure-function-app-settings#settings).

Note

Even when re-enabled using the `EnableProxies`

flag, you can't work with proxies in the Azure portal. Instead, you must work directly with the *proxies.json* file for your function app. For more information, see [Advanced configuration](#advanced-configuration).

## Create a proxy

Important

For equivalent content using API Management, see [Expose serverless APIs from HTTP endpoints using Azure API Management](functions-openapi-definition).

Proxies are defined in the *proxies.json* file in the root of your function app. The steps in this section show you how to use the Azure portal to create this file in your function app. Not all languages and operating system combinations support in-portal editing. If you can't modify your function app files in the portal, you can instead create and deploy the equivalent `proxies.json`

file from the root of your local project folder. To learn more about portal editing support, see [Language support details](supported-languages#language-support-details).

- Open the
[Azure portal](https://portal.azure.com), and then go to your function app. - In the left pane, select
**Proxies**and then select**+Add**. - Provide a name for your proxy.
- Configure the endpoint that's exposed on this function app by specifying the
**route template**and**HTTP methods**. These parameters behave according to the rules for[HTTP triggers](functions-bindings-http-webhook). - Set the
**backend URL**to another endpoint. This endpoint could be a function in another function app, or it could be any other API. The value doesn't need to be static, and it can reference[application settings](#use-appsettings)and[parameters from the original client request](#request-parameters). - Select
**Create**.

Your proxy now exists as a new endpoint on your function app. From a client perspective, it's the same as an HttpTrigger in Functions. You can try out your new proxy by copying the **Proxy URL** and testing it with your favorite HTTP client.

## Modify requests and responses

Important

API Management lets you can change API behavior through configuration using policies. Policies are a collection of statements that are run sequentially on the request or response of an API. For more information about API Management policies, see [Policies in Azure API Management](../api-management/api-management-howto-policies).

With proxies, you can modify requests to and responses from the back-end. These transformations can use variables as defined in [Use variables](#using-variables).

### Modify the back-end request

By default, the back-end request is initialized as a copy of the original request. In addition to setting the back-end URL, you can make changes to the HTTP method, headers, and query string parameters. The modified values can reference [application settings](#use-appsettings) and [parameters from the original client request](#request-parameters).

Back-end requests can be modified in the portal by expanding the *request override* section of the proxy detail page.

### Modify the response

By default, the client response is initialized as a copy of the back-end response. You can make changes to the response's status code, reason phrase, headers, and body. The modified values can reference [application settings](#use-appsettings), [parameters from the original client request](#request-parameters), and [parameters from the back-end response](#response-parameters).

Back-end responses can be modified in the portal by expanding the *response override* section of the proxy detail page.

## Use variables

The configuration for a proxy doesn't need to be static. You can condition it to use variables from the original client request, the back-end response, or application settings.

### Reference local functions

You can use `localhost`

to reference a function inside the same function app directly, without a roundtrip proxy request.

`"backendUri": "https://localhost/api/httptriggerC#1"`

will reference a local HTTP triggered function at the route `/api/httptriggerC#1`


Note

If your function uses *function, admin or sys* authorization levels, you will need to provide the code and clientId, as per the original function URL. In this case the reference would look like: `"backendUri": "https://localhost/api/httptriggerC#1?code=<keyvalue>&clientId=<keyname>"`

We recommend storing these keys in [application settings](#use-appsettings) and referencing those in your proxies. This avoids storing secrets in your source code.

### Reference request parameters

You can use request parameters as inputs to the back-end URL property or as part of modifying requests and responses. Some parameters can be bound from the route template that's specified in the base proxy configuration, and others can come from properties of the incoming request.

#### Route template parameters

Parameters that are used in the route template are available to be referenced by name. The parameter names are enclosed in braces ({}).

For example, if a proxy has a route template, such as `/pets/{petId}`

, the back-end URL can include the value of `{petId}`

, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`

. If the route template terminates in a wildcard, such as `/api/{*restOfPath}`

, the value `{restOfPath}`

is a string representation of the remaining path segments from the incoming request.

#### Additional request parameters

In addition to the route template parameters, the following values can be used in config values:

**{request.method}**: The HTTP method that's used on the original request.**{request.headers.<HeaderName>}**: A header that can be read from the original request. Replace*<HeaderName>*with the name of the header that you want to read. If the header isn't included on the request, the value will be the empty string.**{request.querystring.<ParameterName>}**: A query string parameter that can be read from the original request. Replace*<ParameterName>*with the name of the parameter that you want to read. If the parameter isn't included on the request, the value will be the empty string.

### Reference back-end response parameters

Response parameters can be used as part of modifying the response to the client. The following values can be used in config values:

**{backend.response.statusCode}**: The HTTP status code that's returned on the back-end response.**{backend.response.statusReason}**: The HTTP reason phrase that's returned on the back-end response.**{backend.response.headers.<HeaderName>}**: A header that can be read from the back-end response. Replace*<HeaderName>*with the name of the header you want to read. If the header isn't included on the response, the value will be the empty string.

### Reference application settings

You can also reference [application settings defined for the function app](functions-how-to-use-azure-function-app-settings) by surrounding the setting name with percent signs (%).

For example, a back-end URL of *https://%ORDER_PROCESSING_HOST%/api/orders* would have "%ORDER_PROCESSING_HOST%" replaced with the value of the ORDER_PROCESSING_HOST setting.

Tip

Use application settings for back-end hosts when you have multiple deployments or test environments. That way, you can make sure that you are always talking to the right back-end for that environment.

## Troubleshoot Proxies

By adding the flag `"debug":true`

to any proxy in your `proxies.json`

, you'll enable debug logging. Logs are stored in `D:\home\LogFiles\Application\Proxies\DetailedTrace`

and accessible through the advanced tools (kudu). Any HTTP responses will also contain a `Proxy-Trace-Location`

header with a URL to access the log file.

You can debug a proxy from the client side by adding a `Proxy-Trace-Enabled`

header set to `true`

. This will also log a trace to the file system, and return the trace URL as a header in the response.

### Block proxy traces

For security reasons you may not want to allow anyone calling your service to generate a trace. They won't be able to access the trace contents without your sign-in credentials, but generating the trace consumes resources and exposes that you're using Function Proxies.

Disable traces altogether by adding `"debug":false`

to any particular proxy in your `proxies.json`

.

## Advanced configuration

The proxies that you configure are stored in a *proxies.json* file, which is located in the root of a function app directory. You can manually edit this file and deploy it as part of your app when you use any of the [deployment methods](functions-continuous-deployment) that Functions supports.

Tip

If you have not set up one of the deployment methods, you can also work with the *proxies.json* file in the portal. Go to your function app, select **Platform features**, and then select **App Service Editor**. By doing so, you can view the entire file structure of your function app and then make changes.

*Proxies.json* is defined by a proxies object, which is composed of named proxies and their definitions. Optionally, if your editor supports it, you can reference a [JSON schema](http://json.schemastore.org/proxies) for code completion. An example file might look like the following:

```
{
"$schema": "http://json.schemastore.org/proxies",
"proxies": {
"proxy1": {
"matchCondition": {
"methods": [ "GET" ],
"route": "/api/{test}"
},
"backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>"
}
}
}
```


Each proxy has a friendly name, such as *proxy1* in the preceding example. The corresponding proxy definition object is defined by the following properties:

**matchCondition**: Required--an object defining the requests that trigger the execution of this proxy. It contains two properties that are shared with[HTTP triggers](functions-bindings-http-webhook):*methods*: An array of the HTTP methods that the proxy responds to. If it isn't specified, the proxy responds to all HTTP methods on the route.*route*: Required--defines the route template, controlling which request URLs your proxy responds to. Unlike in HTTP triggers, there's no default value.

**backendUri**: The URL of the back-end resource to which the request should be proxied. This value can reference application settings and parameters from the original client request. If this property isn't included, Azure Functions responds with an HTTP 200 OK.**requestOverrides**: An object that defines transformations to the back-end request. See[Define a requestOverrides object](#requestOverrides).**responseOverrides**: An object that defines transformations to the client response. See[Define a responseOverrides object](#responseOverrides).

Note

The *route* property in Azure Functions Proxies does not honor the *routePrefix* property of the Function App host configuration. If you want to include a prefix such as `/api`

, it must be included in the *route* property.

### Disable individual proxies

You can disable individual proxies by adding `"disabled": true`

to the proxy in the `proxies.json`

file. This will cause any requests meeting the matchCondition to return 404.

```
{
"$schema": "http://json.schemastore.org/proxies",
"proxies": {
"Root": {
"disabled":true,
"matchCondition": {
"route": "/example"
},
"backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>"
}
}
}
```


### Application Settings

The proxy behavior can be controlled by several app settings. They're all outlined in the [Functions App Settings reference](functions-app-settings)

### Reserved Characters (string formatting)

Proxies read all strings out of a JSON file, using \ as an escape symbol. Proxies also interpret curly braces. See a full set of examples below.

| Character | Escaped Character | Example |
|---|---|---|
| { or } | {{ or }} | `{{ example }}` --> `{ example }` |
| \ | \\ | `example.com\\text.html` --> `example.com\text.html` |
| " | \" | `\"example\"` --> `"example"` |

### Define a requestOverrides object

The requestOverrides object defines changes made to the request when the back-end resource is called. The object is defined by the following properties:

**backend.request.method**: The HTTP method that's used to call the back-end.**backend.request.querystring.<ParameterName>**: A query string parameter that can be set for the call to the back-end. Replace*<ParameterName>*with the name of the parameter that you want to set. If an empty string is provided, the parameter is still included on the back-end request.**backend.request.headers.<HeaderName>**: A header that can be set for the call to the back-end. Replace*<HeaderName>*with the name of the header that you want to set. If an empty string is provided, the parameter is still included on the back-end request.

Values can reference application settings and parameters from the original client request.

An example configuration might look like the following:

```
{
"$schema": "http://json.schemastore.org/proxies",
"proxies": {
"proxy1": {
"matchCondition": {
"methods": [ "GET" ],
"route": "/api/{test}"
},
"backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>",
"requestOverrides": {
"backend.request.headers.Accept": "application/xml",
"backend.request.headers.x-functions-key": "%ANOTHERAPP_API_KEY%"
}
}
}
}
```


### Define a responseOverrides object

The requestOverrides object defines changes that are made to the response that's passed back to the client. The object is defined by the following properties:

**response.statusCode**: The HTTP status code to be returned to the client.**response.statusReason**: The HTTP reason phrase to be returned to the client.**response.body**: The string representation of the body to be returned to the client.**response.headers.<HeaderName>**: A header that can be set for the response to the client. Replace*<HeaderName>*with the name of the header that you want to set. If you provide the empty string, the header isn't included on the response.

Values can reference application settings, parameters from the original client request, and parameters from the back-end response.

An example configuration might look like the following:

```
{
"$schema": "http://json.schemastore.org/proxies",
"proxies": {
"proxy1": {
"matchCondition": {
"methods": [ "GET" ],
"route": "/api/{test}"
},
"responseOverrides": {
"response.body": "Hello, {test}",
"response.headers.Content-Type": "text/plain"
}
}
}
}
```


Note

In this example, the response body is set directly, so no `backendUri`

property is needed. The example shows how you might use Azure Functions Proxies for mocking APIs.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/flex-consumption-how-to -->

# Create and manage function apps in the Flex Consumption plan

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to create function apps hosted in the [Flex Consumption plan](flex-consumption-plan) in Azure Functions. It also shows you how to manage certain features of a Flex Consumption plan hosted app.

Function app resources are langauge-specific. Make sure to choose your preferred code development language at the beginning of the article.

## Prerequisites

An Azure account with an active subscription. If you don't already have one, you can

[create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).: used to create and manage resources in Azure. When using the Azure CLI on your local computer, make sure to use version 2.60.0, or a later version. You can also use[Azure CLI](/en-us/cli/azure/install-azure-cli)[Azure Cloud Shell](../cloud-shell/overview), which has the correct Azure CLI version.: used to create and develop apps, create Azure resources, and deploy code projects to Azure. When using Visual Studio Code, make sure to also install the latest[Visual Studio Code](functions-develop-vs-code)[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions). You can also install the[Azure Tools extension pack](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack).While not required to create a Flex Consumption plan app, you need a code project to be able to deploy to and validate a new function app. Complete the first part of one of these quickstart articles, where you create a code project with an HTTP triggered function:

[Create an Azure Functions project from the command line](how-to-create-function-azure-cli)[Create an Azure Functions project using Visual Studio Code](how-to-create-function-vs-code)

To create an app in a new Flex Consumption plan during a Maven deployment, you must create your local app project and then update the project's pom.xml file. For more information, see

[Create a Java Flex Consumption app using Maven](#create-and-deploy-your-app-using-maven)Return to this article after you create and run the local project, but before you're asked to create Azure resources. You create the function app and other Azure resources in the next section.


## Create a Flex Consumption app

This section shows you how to create a function app in the Flex Consumption plan by using either the Azure CLI, Azure portal, or Visual Studio Code. For an example of creating an app in a Flex Consumption plan using Bicep/ARM templates, see the [Flex Consumption repository](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/README.md#iac-samples-overview).

You can skip this section if you choose to instead [create and deploy your app using Maven](#create-and-deploy-your-app-using-maven).

To support your function code, you need to create three resources:

- A
[resource group](../azure-resource-manager/management/overview), which is a logical container for related resources. - A
[Storage account](../storage/common/storage-account-create), which is used to maintain state and other information about your functions. - A function app in the Flex Consumption plan, which provides the environment for executing your function code. A function app maps to your local function project and lets you group functions as a logical unit for easier management, deployment, and sharing of resources in the Flex Consumption plan.

If you haven't done so already, sign in to Azure:

`az login`

The

command signs you into your Azure account.`az login`

Use the

`az functionapp list-flexconsumption-locations`

command to review the list of regions that currently support Flex Consumption in alphabetical order.`az functionapp list-flexconsumption-locations --query "sort_by(@, &name)[].{Region:name}" -o table`


Create a resource group in one of the currently supported regions listed by the command in the previous step.

`az group create --name <RESOURCE_GROUP> --location <REGION>`

In the previous command, replace

`<RESOURCE_GROUP>`

with a value that's unique in your subscription and`<REGION>`

with one of the currently supported regions. The[az group create](/en-us/cli/azure/group#az-group-create)command creates a resource group.Create a general-purpose storage account in your resource group and region:

`az storage account create --name <STORAGE_NAME> --location <REGION> --resource-group <RESOURCE_GROUP> --sku Standard_LRS --allow-blob-public-access false`

In the previous example, replace

`<STORAGE_NAME>`

with a name that's appropriate to you and unique in Azure Storage. Names must contain three to 24 characters consisting of numbers and lowercase letters only.`Standard_LRS`

specifies a general-purpose account that Azure Functions supports according to[storage account requirements](storage-considerations#storage-account-requirements). The[az storage account create](/en-us/cli/azure/storage/account#az-storage-account-create)command creates the storage account.Important

The storage account is used to store important app data, sometimes including the application code itself. You should limit access from other apps and users to the storage account.

Create the function app in Azure:

`az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage-account <STORAGE_NAME> --flexconsumption-location <REGION> --runtime dotnet-isolated --runtime-version 8.0`

[C# apps that run in-process](functions-dotnet-class-library)aren't currently supported when running in a Flex Consumption plan.`az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage-account <STORAGE_NAME> --flexconsumption-location <REGION> --runtime java --runtime-version 17`

For Java apps, Java 11 is also currently supported.

`az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage-account <STORAGE_NAME> --flexconsumption-location <REGION> --runtime node --runtime-version 20`

`az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage-account <STORAGE_NAME> --flexconsumption-location <REGION> --runtime python --runtime-version 3.11`

For Python apps, Python 3.10 is also currently supported.

`az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage-account <STORAGE_NAME> --flexconsumption-location <REGION> --runtime powershell --runtime-version 7.4`

In this example, replace both

`<RESOURCE_GROUP>`

and`<STORAGE_NAME>`

with the resource group and the name of the account you used in the previous step, respectively. Also replace`<APP_NAME>`

with a globally unique name appropriate to you. The`<APP_NAME>`

is also the default domain name server (DNS) domain for the function app. Thecommand creates the function app in Azure.`az functionapp create`

This command creates a function app running in the Flex Consumption plan.

Because you created the app without specifying

[always ready instances](#set-always-ready-instance-counts), your app only incurs costs when actively executing functions. The command also creates an associated Azure Application Insights instance in the same resource group, with which you can monitor your function app and view logs. For more information, see[Monitor Azure Functions](functions-monitoring).

## Deploy your code project

For deployment, Flex Consumption plan apps use a Blob storage container to host .zip package files that contain your project code and all libraries that are required for your app to run. For more information, see [Deployment](flex-consumption-plan#deployment).

You can skip this section if you choose to instead [create and deploy your app using Maven](#create-and-deploy-your-app-using-maven).

You can choose to deploy your project code to an existing function app using various tools:

You can use the Azure CLI to upload a deployment package file to the deployment share for a function app in Azure. To make this deployment, you must produce a .zip package file that can run when the package is mounted to your app.

This package file must contain all of the build output files and referenced libraries required for your project to run.

For projects with a large number of libraries, you should package the root of your project file and request a [remote build](functions-deployment-technologies#remote-build).

For Python projects, you should package the root of your project file and always request a [remote build](functions-deployment-technologies#remote-build). Using a remote build prevents potential issues that can occur when you build a project on Windows to be deployed on Linux.

Using your preferred development tool, build the code project.

Create a .zip file that contains the output of the build directory. For more information, see

[Project structure](dotnet-isolated-process-guide#project-structure).When required, sign in to your Azure account and select the active subscription using the

command.`az login`

`az login`

Run the

command to deploy the application package located in the relative`az functionapp deployment source config-zip`

`<FILE_PATH>`

.`az functionapp deployment source config-zip --src <FILE_PATH> --name <APP_NAME> --resource-group <RESOURCE_GROUP>`


Using your preferred development tool, build the code project.

Create a .zip file that contains the output of the build directory. For more information, see

[Folder structure](functions-reference-java#folder-structure).When required, sign in to your Azure account and select the active subscription using the

command.`az login`

`az login`

Run the

command to deploy the application package located in the relative`az functionapp deployment source config-zip`

`<FILE_PATH>`

.`az functionapp deployment source config-zip --src <FILE_PATH> --name <APP_NAME> --resource-group <RESOURCE_GROUP>`


Create a .zip file that contains the root directory of your code project. For more information, see

[Folder structure](functions-reference-powershell#folder-structure).When required, sign in to your Azure account and select the active subscription using the

command.`az login`

`az login`

Run the

command to deploy the application package located in the relative`az functionapp deployment source config-zip`

`<FILE_PATH>`

.`az functionapp deployment source config-zip --src <FILE_PATH> --name <APP_NAME> --resource-group <RESOURCE_GROUP>`


Create a .zip file that contains the root directory of your code project. For more information, see

[Folder structure](functions-reference-node#folder-structure).When required, sign in to your Azure account and select the active subscription using the

command.`az login`

`az login`

Run the

command to deploy the application package located in the relative`az functionapp deployment source config-zip`

`<FILE_PATH>`

.`az functionapp deployment source config-zip --src <FILE_PATH> --name <APP_NAME> --resource-group <RESOURCE_GROUP> --build-remote true`

Make sure to set

`--build-remote true`

to perform a[remote build](functions-deployment-technologies#remote-build).

Create a .zip file that contains the root directory of your code project. For more information, see

[Folder structure](functions-reference-python#folder-structure).When required, sign in to your Azure account and select the active subscription using the

command.`az login`

`az login`

Run the

command to deploy the application package located in the relative`az functionapp deployment source config-zip`

`<FILE_PATH>`

.`az functionapp deployment source config-zip --src <FILE_PATH> --name <APP_NAME> --resource-group <RESOURCE_GROUP> --build-remote true`

Make sure to set

`--build-remote true`

to perform a[remote build](functions-deployment-technologies#remote-build).

## Create and deploy your app using Maven

You can use Maven to create a Flex Consumption hosted function app and required resources during deployment by modifying the pom.xml file.

Create a Java code project by completing the first part of one of these quickstart articles:

In your Java code project, open the pom.xml file and make these changes to create your function app in the Flex Consumption plan:

Change the value of

`<properties>.<azure.functions.maven.plugin.version>`

to`1.34.0`

.In the

`<plugin>.<configuration>`

section for the`azure-functions-maven-plugin`

, add or uncomment the`<pricingTier>`

element as follows:`<pricingTier>Flex Consumption</pricingTier>`


(Optional) Customize the Flex Consumption plan in your Maven deployment by also including these elements in the

`<plugin>.<configuration>`

section: .`<instanceSize>`

- sets the[instance memory](flex-consumption-plan#instance-sizes)size for the function app. The default value is`2048`

.`<maximumInstances>`

- sets the highest value for the maximum instances count of the function app.`<alwaysReadyInstances>`

- sets the[always ready instance counts](flex-consumption-plan#always-ready-instances)with child elements for HTTP trigger groups (`<http>`

), Durable Functions groups (`<durable>`

), and other specific triggers (`<my_function>`

). When you set any instance count greater than zero, you're charged for these instances whether your functions execute or not. For more information, see[Billing](flex-consumption-plan#billing).

Before you can deploy, sign in to your Azure subscription using the Azure CLI.

`az login`

The

command signs you into your Azure account.`az login`

Use the following command to deploy your code project to a new function app in Flex Consumption.

`mvn azure-functions:deploy`

Maven uses settings in the pom.xml template to create your function app in a Flex Consumption plan in Azure, along with the other required resources. Should these resources already exist, the code is deployed to your function app, overwriting any existing code.


## Enable virtual network integration

You can enable [virtual network integration](functions-networking-options#virtual-network-integration) for your app in a Flex Consumption plan. The examples in this section assume that your account already contains a [virtual network and subnet](../virtual-network/quick-create-cli#create-a-virtual-network-and-subnet). You can enable virtual network integration when you create your app or at a later time.

Important

The Flex Consumption plan currently doesn't support subnets with names that contain underscore (`_`

) characters.

To enable virtual networking when you create your app:

You can enable virtual network integration by running the [ az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create) command and including the

`--vnet`

and `--subnet`

parameters.[Create the virtual network and subnet](../virtual-network/quick-create-cli#create-a-virtual-network-and-subnet), if you don't have one already.Complete steps 1-4 in

[Create a Flex Consumption app](#create-a-flex-consumption-app)to create the resources required by your app.Run the

command, including the`az functionapp create`

`--vnet`

and`--subnet`

parameters, as in this example:`az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage-account <STORAGE_NAME> --flexconsumption-location <REGION> --runtime <RUNTIME_NAME> --runtime-version <RUNTIME_VERSION> --vnet <VNET_RESOURCE_ID> --subnet <SUBNET_NAME>`

The

`<VNET_RESOURCE_ID>`

value is the resource ID for the virtual network, which is in the format:`/subscriptions/<SUBSCRIPTION_ID>/resourceGroups/<RESOURCE_GROUP>/providers/Microsoft.Network/virtualNetworks/<VNET_NAME>`

. You can use this command to get a list of virtual network IDs, filtered by`<RESOURCE_GROUP>`

:`az network vnet list --resource-group <RESOURCE_GROUP> --output tsv --query "[]".id`

.

For end-to-end examples of how to create apps in Flex Consumption with virtual network integration see these resources:

[Flex Consumption: HTTP to Event Hubs using virtual network integration](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/README.md)[Flex Consumption: triggered from Service Bus using virtual network integration](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/README.md)

To modify or delete virtual network integration in an existing app:

Use the [ az functionapp vnet-integration add](/en-us/cli/azure/functionapp/vnet-integration#az-functionapp-vnet-integration-add) command to enable virtual network integration to an existing function app:

```
az functionapp vnet-integration add --resource-group <RESOURCE_GROUP> --name <APP_NAME> --vnet <VNET_RESOURCE_ID> --subnet <SUBNET_NAME>
```


Use the [ az functionapp vnet-integration remove](/en-us/cli/azure/functionapp/vnet-integration#az-functionapp-vnet-integration-remove) command to disable virtual network integration in your app:

```
az functionapp vnet-integration remove --resource-group <RESOURCE_GROUP> --name <APP_NAME>
```


Use the [ az functionapp vnet-integration list](/en-us/cli/azure/functionapp/vnet-integration#az-functionapp-vnet-integration-list) command to list the current virtual network integrations for your app:

```
az functionapp vnet-integration list --resource-group <RESOURCE_GROUP> --name <APP_NAME>
```


When you're choosing a subnet, these considerations apply:

- The subnet you choose can't already be used for other purposes, such as with private endpoints or service endpoints, or be delegated to any other hosting plan or service.
- You can't share the same subnet between a Container Apps environment and a Flex Consumption app.
- You can share the same subnet with more than one app running in a Flex Consumption plan. Because the networking resources are shared across all apps, one function app might affect the performance of others on the same subnet.
- In a Flex Consumption plan, a single function app might use up to 40 IP addresses, even when the app scales beyond 40 instances. While this rule of thumb is helpful when estimating the subnet size you need, it isn't strictly enforced.

## Configure deployment settings

In the Flex Consumption plan, the deployment package that contains your app's code is maintained in an Azure Blob Storage container. By default, deployments use the same storage account (`AzureWebJobsStorage`

) and connection string value used by the Functions runtime to maintain your app. The connection string is stored in the `DEPLOYMENT_STORAGE_CONNECTION_STRING`

application setting. However, you can instead designate a blob container in a separate storage account as the deployment source for your code. You can also change the authentication method used to access the container.

A customized deployment source should meet this criteria:

- The storage account must already exist.
- The container to use for deployments must also exist.
- When more than one app uses the same storage account, each should have its own deployment container. Using a unique container for each app prevents the deployment packages from being overwritten, which would happen if apps shared the same container.

When configuring deployment storage authentication, keep these considerations in mind:

- As a security best practice, you should use managed identities when connecting to Azure Storage from your apps. For more information, see
[Connections](functions-reference#connections). - When you use a connection string to connect to the deployment storage account, the application setting that contains the connection string must already exist.
- When you use a user-assigned managed identity, the provided identity gets linked to the function app. The
`Storage Blob Data Contributor`

role scoped to the deployment storage account also gets assigned to the identity. - When you use a system-assigned managed identity, an identity gets created when a valid system-assigned identity doesn't already exist in your app. When a system-assigned identity does exists, the
`Storage Blob Data Contributor`

role scoped to the deployment storage account also gets assigned to the identity.

To configure deployment settings when you create your function app in the Flex Consumption plan:

Use the [ az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create) command and supply these extra options that customize deployment storage:

| Parameter | Description |
|---|---|
`--deployment-storage-name` |
The name of the deployment storage account. |
`--deployment-storage-container-name` |
The name of the container in the account to contain your app's deployment package. |
`--deployment-storage-auth-type` |
The authentication type to use for connecting to the deployment storage account. Accepted values include `StorageAccountConnectionString` , `UserAssignedIdentity` , and `SystemAssignedIdentity` . |
`--deployment-storage-auth-value` |
When using `StorageAccountConnectionString` , this parameter is set to the name of the application setting that contains the connection string to the deployment storage account. When you set `UserAssignedIdentity` , this parameter is set to the name of the resource ID of the identity you want to use. |

This example creates a function app in the Flex Consumption plan with a separate deployment storage account and user assigned identity:

```
az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage <STORAGE_NAME> --runtime dotnet-isolated --runtime-version 8.0 --flexconsumption-location "<REGION>" --deployment-storage-name <DEPLOYMENT_ACCOUNT_NAME> --deployment-storage-container-name <DEPLOYMENT_CONTAINER_NAME> --deployment-storage-auth-type UserAssignedIdentity --deployment-storage-auth-value <MI_RESOURCE_ID>
```


You can also modify the deployment storage configuration for an existing app.

Use the [ az functionapp deployment config set](/en-us/cli/azure/functionapp/deployment/config#az-functionapp-deployment-config-set) command to modify the deployment storage configuration:

```
az functionapp deployment config set --resource-group <RESOURCE_GROUP> --name <APP_NAME> --deployment-storage-name <DEPLOYMENT_ACCOUNT_NAME> --deployment-storage-container-name <DEPLOYMENT_CONTAINER_NAME>
```


## Configure instance memory

The instance memory size used by your Flex Consumption plan can be explicitly set when you create your app. For more information about supported sizes, see [Instance sizes](flex-consumption-plan#instance-sizes).

To set an instance memory size that's different from the default when creating your app:

Specify the `--instance-memory`

parameter in your [ az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create) command. This example creates a C# app with an instance size of

`4096`

:```
az functionapp create --instance-memory 4096 --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage-account <STORAGE_NAME> --flexconsumption-location <REGION> --runtime dotnet-isolated --runtime-version 8.0
```


At any point, you can change the instance memory size setting used by your app.

This example uses the [ az functionapp scale config set](/en-us/cli/azure/functionapp/scale/config#az-functionapp-scale-config-set) command to change the instance memory size setting to 512 MB:

```
az functionapp scale config set --resource-group <resourceGroup> --name <APP_NAME> --instance-memory 512
```


## Set always ready instance counts

You can set a specific number of always ready instances for the [Per-function scaling](flex-consumption-plan#per-function-scaling) groups or individual functions, to keep your functions loaded and ready to execute. There are three special groups, as in per-function scaling:

`http`

- All of the HTTP triggered functions in the app scale together into their own instances.`durable`

- All of the Durable triggered functions (Orchestration, Activity, Entity) in the app scale together into their own instances.`blob`

- All of the blob (Event Grid) triggered functions in the app scale together into their own instances.

Use `http`

, `durable`

, or `blob`

as the name for the name value pair setting to configure always ready counts for these groups. For all other functions in the app you need to configure always ready for each individual function using the format `function:<FUNCTION_NAME>=n`

.

To define one or more always ready instance designations, use the `--always-ready-instances`

parameter with the [ az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create) command. This example sets the always ready instance count for all HTTP triggered functions to

`10`

:```
az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage <STORAGE_NAME> --runtime <LANGUAGE_RUNTIME> --runtime-version <RUNTIME_VERSION> --flexconsumption-location <REGION> --always-ready-instances http=10
```


This example sets the always ready instance count for all Durable trigger functions to `3`

and sets the always ready instance count to `2`

for a service bus triggered function named `function5`

:

```
az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage <STORAGE_NAME> --runtime <LANGUAGE_RUNTIME> --runtime-version <RUNTIME_VERSION> --flexconsumption-location <REGION> --always-ready-instances durable=3 function:function5=2
```


You can also modify always ready instances on an existing app by adding or removing instance designations or by changing existing instance designation counts.

This example uses the [ az functionapp scale config always-ready set](/en-us/cli/azure/functionapp/scale/config/always-ready#az-functionapp-scale-config-always-ready-set) command to change the always ready instance count for the HTTP triggers group to

`10`

:```
az functionapp scale config always-ready set --resource-group <RESOURCE_GROUP> --name <APP_NAME> --settings http=10
```


To remove always ready instances, use the [ az functionapp scale config always-ready delete](/en-us/cli/azure/functionapp/scale/config/always-ready#az-functionapp-scale-config-always-ready-delete) command, as in this example that removes all always ready instances from both the HTTP triggers group and also a function named

`hello_world`

:```
az functionapp scale config always-ready delete --resource-group <RESOURCE_GROUP> --name <APP_NAME> --setting-names http function:hello_world
```


## Set HTTP concurrency limits

Unless you set specific limits, HTTP concurrency defaults for Flex Consumption plan apps are determined based on your instance size setting. For more information, see [HTTP trigger concurrency](functions-concurrency#http-trigger-concurrency).

Here's how you can set HTTP concurrency limits for an existing app:

Use the [ az functionapp scale config set](/en-us/cli/azure/functionapp/scale/config#az-functionapp-scale-config-set) command to set specific HTTP concurrency limits for your app, regardless of instance size.

```
az functionapp scale config set --resource-group <RESOURCE_GROUP> --name <APP_NAME> --trigger-type http --trigger-settings perInstanceConcurrency=10
```


This example sets the HTTP trigger concurrency level to `10`

. After you specifically set an HTTP concurrency value, that value is maintained despite any changes in your app's instance size setting.

## Set site update strategy

The Flex Consumption plan uniquely supports two different site update strategies that control how your function app handles code deployments and configuration changes. By default, Flex Consumption plan apps use the `Recreate`

strategy, which terminates currently executing functions during deployments. To enable zero-downtime deployments, you can configure the `RollingUpdate`

strategy instead. For more information, see [Site update strategies in Flex Consumption](flex-consumption-site-updates).

Note

Site update strategy configuration is currently in public preview and is only available through Bicep or ARM templates. You can't configure this setting using the Azure CLI, Azure portal, or Visual Studio Code.

Site update strategy configuration isn't currently supported in the Azure CLI. Use Bicep or ARM templates as described in [Configure site update strategy](flex-consumption-site-updates#configure-your-update-strategy).

## View currently supported regions

To view the list of regions that currently support Flex Consumption plans:

If you haven't done so already, sign in to Azure:

`az login`

The

command signs you into your Azure account.`az login`

Use the

`az functionapp list-flexconsumption-locations`

command to review the list of regions that currently support Flex Consumption in alphabetical order.`az functionapp list-flexconsumption-locations --query "sort_by(@, &name)[].{Region:name}" -o table`


When you create an app in the [Azure portal](flex-consumption-how-to?tabs=azure-portal#create-a-flex-consumption-app) or by using [Visual Studio Code](flex-consumption-how-to?tabs=vs-code#create-a-flex-consumption-app), currently unsupported regions are filtered out of the region list.

## Monitor your app in Azure

Azure Monitor provides these distinct sets of metrics to help you better understand how your function app runs in Azure:

- Platform metrics: provides infrastructure-level insights
- Application Insights: provides code-level insights, including traces and errors logs.

If you [enable Application Insights in your app](configure-monitoring#enable-application-insights-integration), you're able to:

- Track detailed execution times and dependencies
- Monitor individual function performance
- Analyze failures and exceptions
- Correlate platform metrics with application behavior with custom queries

For more information, see [Monitor Azure Functions](monitor-functions).

### Supported metrics

Run this script to view all of the platform metrics that are currently available your app:

```
appId=$(az functionapp show --name <APP_NAME> --resource-group <RESOURCE_GROUP> --query id -o tsv)
az monitor metrics list-definitions --resource $appId --query "[].{Name:name.localizedValue,Value:name.value}" -o table
```


In this example, replace `<RESOURCE_GROUP>`

and `<APP_NAME>`

with your resource group and function app names, respectively. This script gets the fully qualified app ID and returns the available platform metrics in a table.

### View metrics

You can review current metrics either in the Azure portal or by using the Azure CLI.

In the Azure portal, you can also create metrics alerts and pin charts and other reports to dashboards in the portal.

Use this script to generate a report of the current metrics for your app:

```
appId=$(az functionapp show --name <APP_NAME> --resource-group <RESOURCE_GROUP> --query id -o tsv)
appId=$(az functionapp show --name func-fuxigh6c255de --resource-group exampleRG --query id -o tsv)
echo -e "\nAlways-ready and on-emand execution counts..."
az monitor metrics list --resource $appId --metric "AlwaysReadyFunctionExecutionCount" --interval PT1H --output table
az monitor metrics list --resource $appId --metric "OnDemandFunctionExecutionCount" --interval PT1H --output table
echo -e "\nExecution units (MB-ms) in always-ready and on-emand execution counts..."
az monitor metrics list --resource $appId --metric "AlwaysReadyFunctionExecutionUnits" --interval PT1H --output table
az monitor metrics list --resource $appId --metric "OnDemandFunctionExecutionUnits" --interval PT1H --output table
echo -e "\nAlways-ready resource utilization..."
az monitor metrics list --resource $appId --metric "AlwaysReadyUnits" --interval PT1H --output table
echo -e "\nMemory utilization..."
az monitor metrics list --resource $appId --metric "AverageMemoryWorkingSet" --interval PT1H --output table
az monitor metrics list --resource $appId --metric "MemoryWorkingSet" --interval PT1H --output table
echo -e "\nInstance count and CPU utilization..."
az monitor metrics list --resource $appId --metric "InstanceCount" --interval PT1H --output table
az monitor metrics list --resource $appId --metric "CpuPercentage" --interval PT1H --output table
```


To learn more about metrics for Azure Functions, see [Monitor Azure Functions](monitor-functions).

### View logs

When your app is connected to Application Insights, you can better analyze your app performance and troubleshoot problems during execution.

- Use "Performance" to analyze response times and dependencies
- Use "Failures" to identify any errors occurring after migration
- Create custom queries in "Logs" to analyze function behavior. For example:

Use this query to compare success rates by instance:

```
requests
| where timestamp > ago(7d)
| summarize successCount=countif(success == true), failureCount=countif(success == false) by bin(timestamp, 1h), cloud_RoleName
| render timechart
```


Use this query to analyze the number of instances that were actively processing your function:

```
let _startTime = ago(20m); //Adjust start time as needed
let _endTime = now(); //Adjust end time as needed
let bins = 1s; //Adjust bin as needed - this will give per second results
requests
| where operation_Name == 'EventHubsTrigger' //Replace with the name of the function in the function app that you are analyzing
| where timestamp between(_startTime .. _endTime)
| make-series dcount(cloud_RoleInstance) default=0 on timestamp from _startTime to _endTime step bins
| render columnchart
```


### View costs

Because you can tune your app to adjust performance versus operating costs, it's important to track the costs associated with running your app in the Flex Consumption plan.

To view the current costs:

In your function app page in the

[Azure portal](https://portal.azure.com), select the resource group link.In the resource group page, select

**Cost Management**>**Cost analysis**.Review the current costs and cost trajectory of the app itself.

Optionally, select

**Cost Management**>**Alerts**and then**+ Add**to create a new alert for the app.

## Fine-tune your app

The Flex Consumption plan provides several settings that you can tune to refine the performance of your app. Actual performance and costs can vary based on your app-specific workload patterns and configuration. For example, higher [memory instance sizes](flex-consumption-plan#instance-sizes) can improve performance for memory-intensive operations but at a higher cost per active period.

Here are some adjustments you can make to fine-tune performance versus cost:

[Adjust concurrency settings](functions-concurrency)to maximize throughput per instance.[Choose the appropriate memory size](#configure-instance-memory)for your workload. Higher memory sizes cost more but can improve performance.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/scenario-blob-storage-events -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai-embeddings-input -->

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
