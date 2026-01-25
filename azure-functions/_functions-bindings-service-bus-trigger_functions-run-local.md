---
merged_at: 2026-01-25T15:41:11.221311
merged_files: 2
---

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
