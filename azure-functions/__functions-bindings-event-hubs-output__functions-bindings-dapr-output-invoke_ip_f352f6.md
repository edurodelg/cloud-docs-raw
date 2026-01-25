---
merged_at: 2026-01-25T15:41:11.630365
merged_files: 2
---

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
