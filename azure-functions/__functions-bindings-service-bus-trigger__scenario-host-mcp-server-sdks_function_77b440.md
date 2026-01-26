---
merged_at: 2026-01-26T21:02:36.319445
merged_files: 2
---


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
<!-- Source: N/A -->

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
<!-- Source: N/A -->

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
