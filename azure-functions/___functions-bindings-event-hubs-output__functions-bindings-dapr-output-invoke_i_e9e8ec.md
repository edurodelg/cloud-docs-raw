---
merged_at: 2026-01-26T21:02:36.322346
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-event-hubs-output__functions-bindings-dapr-output-invoke_ip-_f61211.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-event-hubs-output.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-hubs-output -->

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

<!-- DOCUMENTO FUSIONADO: _functions-bindings-dapr-output-invoke_ip-addresses.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-dapr-output-invoke.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr-output-invoke -->

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

<!-- DOCUMENTO FUSIONADO: ip-addresses.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/ip-addresses -->

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

<!-- DOCUMENTO FUSIONADO: functions-core-tools-reference.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-core-tools-reference -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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
