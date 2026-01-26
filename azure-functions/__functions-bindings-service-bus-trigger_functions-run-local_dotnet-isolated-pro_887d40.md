---
merged_at: 2026-01-26T21:02:36.320398
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-service-bus-trigger.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-service-bus-trigger -->

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

<!-- DOCUMENTO FUSIONADO: functions-run-local.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-run-local -->

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
