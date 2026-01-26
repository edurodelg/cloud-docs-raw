---
merged_at: 2026-01-26T23:29:57.707925
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-iot-trigger -->

# Azure IoT Hub trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to work with Azure Functions bindings for IoT Hub. The IoT Hub support is based on the [Azure Event Hubs Binding](functions-bindings-event-hubs).

For information on setup and configuration details, see the [overview](functions-bindings-event-iot).

Important

While the following code samples use the Event Hub API, the given syntax is applicable for IoT Hub functions.

Use the function trigger to respond to an event sent to an event hub event stream. You need read access to the underlying event hub to set up the trigger. When the function is triggered, the message passed to the function is typed as a string.

Event Hubs scaling decisions for the Consumption and Premium plans are done via Target Based Scaling. For more information, see [Target Based Scaling](functions-target-based-scaling).

For information about how Azure Functions responds to events sent to an event hub event stream using triggers, see [Integrate Event Hubs with serverless functions on Azure](/en-us/azure/architecture/serverless/event-hubs-functions/event-hubs-functions#consuming-events-with-azure-functions).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

## Example

The following example shows a [C# function](dotnet-isolated-process-guide) that is triggered based on an event hub, where the input message string is written to the logs:

```
{
private readonly ILogger<EventHubsFunction> _logger;
public EventHubsFunction(ILogger<EventHubsFunction> logger)
{
_logger = logger;
}
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


The following example shows an Event Hubs trigger [TypeScript function](functions-reference-node?tabs=typescript). The function reads [event metadata](#event-metadata) and logs the message.

```
import { app, InvocationContext } from '@azure/functions';
export async function eventHubTrigger1(message: unknown, context: InvocationContext): Promise<void> {
context.log('Event hub function processed message:', message);
context.log('EnqueuedTimeUtc =', context.triggerMetadata.enqueuedTimeUtc);
context.log('SequenceNumber =', context.triggerMetadata.sequenceNumber);
context.log('Offset =', context.triggerMetadata.offset);
}
app.eventHub('eventHubTrigger1', {
connection: 'myEventHubReadConnectionAppSetting',
eventHubName: 'MyEventHub',
cardinality: 'one',
handler: eventHubTrigger1,
});
```


To receive events in a batch, set `cardinality`

to `many`

, as shown in the following example.

```
import { app, InvocationContext } from '@azure/functions';
export async function eventHubTrigger1(messages: unknown[], context: InvocationContext): Promise<void> {
context.log(`Event hub function processed ${messages.length} messages`);
for (let i = 0; i < messages.length; i++) {
context.log('Event hub message:', messages[i]);
context.log(`EnqueuedTimeUtc = ${context.triggerMetadata.enqueuedTimeUtcArray[i]}`);
context.log(`SequenceNumber = ${context.triggerMetadata.sequenceNumberArray[i]}`);
context.log(`Offset = ${context.triggerMetadata.offsetArray[i]}`);
}
}
app.eventHub('eventHubTrigger1', {
connection: 'myEventHubReadConnectionAppSetting',
eventHubName: 'MyEventHub',
cardinality: 'many',
handler: eventHubTrigger1,
});
```


The following example shows an Event Hubs trigger [JavaScript function](functions-reference-node). The function reads [event metadata](#event-metadata) and logs the message.

```
const { app } = require('@azure/functions');
app.eventHub('eventHubTrigger1', {
connection: 'myEventHubReadConnectionAppSetting',
eventHubName: 'MyEventHub',
cardinality: 'one',
handler: (message, context) => {
context.log('Event hub function processed message:', message);
context.log('EnqueuedTimeUtc =', context.triggerMetadata.enqueuedTimeUtc);
context.log('SequenceNumber =', context.triggerMetadata.sequenceNumber);
context.log('Offset =', context.triggerMetadata.offset);
},
});
```


To receive events in a batch, set `cardinality`

to `many`

, as shown in the following example.

```
const { app } = require('@azure/functions');
app.eventHub('eventHubTrigger1', {
connection: 'myEventHubReadConnectionAppSetting',
eventHubName: 'MyEventHub',
cardinality: 'many',
handler: (messages, context) => {
context.log(`Event hub function processed ${messages.length} messages`);
for (let i = 0; i < messages.length; i++) {
context.log('Event hub message:', messages[i]);
context.log(`EnqueuedTimeUtc = ${context.triggerMetadata.enqueuedTimeUtcArray[i]}`);
context.log(`SequenceNumber = ${context.triggerMetadata.sequenceNumberArray[i]}`);
context.log(`Offset = ${context.triggerMetadata.offsetArray[i]}`);
}
},
});
```


Here's the PowerShell code:

```
param($eventHubMessages, $TriggerMetadata)
Write-Host "PowerShell eventhub trigger function called for message array: $eventHubMessages"
$eventHubMessages | ForEach-Object { Write-Host "Processed message: $_" }
```


This example uses SDK types to directly access the underlying [ EventData](/en-us/python/api/azure-eventhub/azure.eventhub.eventdata) object provided by the Event Hubs trigger:

The function reads the event body and logs it.

```
import logging
import azure.functions as func
import azurefunctions.extensions.bindings.eventhub as eh
app = func.FunctionApp(http_auth_level=func.AuthLevel.FUNCTION)
@app.event_hub_message_trigger(
arg_name="event", event_hub_name="EVENTHUB_NAME", connection="EventHubConnection"
)
def eventhub_trigger(event: eh.EventData):
logging.info(
"Python EventHub trigger processed an event %s",
event.body_as_str()
)
```


For examples of using the EventData type, see the [ EventData](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-eventhub/samples/eventhub_samples_eventdata/function_app.py) samples. For a step-by-step tutorial on how to include SDK-type bindings in your function app, follow the

[Python SDK Bindings for Event Hubs Sample](https://github.com/Azure-Samples/azure-functions-eventhub-sdk-bindings-python).

Note

Known limitations include:

- The
`enqueued_time`

property is not supported. - Batch message support is supported with runtime version 4.1039 or greater.

To learn more, including what other SDK type bindings are supported, see [SDK type bindings](functions-reference-python#sdk-type-bindings).

The following example shows an Event Hubs trigger binding and a Python function that uses the binding. The function reads [event metadata](#event-metadata) and logs the message. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="EventHubTrigger1")
@app.event_hub_message_trigger(arg_name="myhub",
event_hub_name="<EVENT_HUB_NAME>",
connection="<CONNECTION_SETTING>")
def test_function(myhub: func.EventHubEvent):
logging.info('Python EventHub trigger processed an event: %s',
myhub.get_body().decode('utf-8'))
```


The following example shows an Event Hubs trigger binding which logs the message body of the Event Hubs trigger.

```
@FunctionName("ehprocessor")
public void eventHubProcessor(
@EventHubTrigger(name = "msg",
eventHubName = "myeventhubname",
connection = "myconnvarname") String message,
final ExecutionContext context )
{
context.getLogger().info(message);
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `EventHubTrigger`

annotation on parameters whose value comes from the event hub. Parameters with these annotations cause the function to run when an event arrives. This annotation can be used with native Java types, POJOs, or nullable values using `Optional<T>`

.

The following example illustrates extensive use of `SystemProperties`

and other Binding options for further introspection of the Event along with providing a well-formed `BlobOutput`

path that is Date hierarchical.

```
package com.example;
import java.util.Map;
import java.time.ZonedDateTime;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.*;
/**
* Azure Functions with Event Hub trigger.
* and Blob Output using date in path along with message partition ID
* and message sequence number from EventHub Trigger Properties
*/
public class EventHubReceiver {
@FunctionName("EventHubReceiver")
@StorageAccount("bloboutput")
public void run(
@EventHubTrigger(name = "message",
eventHubName = "%eventhub%",
consumerGroup = "%consumergroup%",
connection = "eventhubconnection",
cardinality = Cardinality.ONE)
String message,
final ExecutionContext context,
@BindingName("Properties") Map<String, Object> properties,
@BindingName("SystemProperties") Map<String, Object> systemProperties,
@BindingName("PartitionContext") Map<String, Object> partitionContext,
@BindingName("EnqueuedTimeUtc") Object enqueuedTimeUtc,
@BlobOutput(
name = "outputItem",
path = "iotevents/{datetime:yy}/{datetime:MM}/{datetime:dd}/{datetime:HH}/" +
"{datetime:mm}/{PartitionContext.PartitionId}/{SystemProperties.SequenceNumber}.json")
OutputBinding<String> outputItem) {
var et = ZonedDateTime.parse(enqueuedTimeUtc + "Z"); // needed as the UTC time presented does not have a TZ
// indicator
context.getLogger().info("Event hub message received: " + message + ", properties: " + properties);
context.getLogger().info("Properties: " + properties);
context.getLogger().info("System Properties: " + systemProperties);
context.getLogger().info("partitionContext: " + partitionContext);
context.getLogger().info("EnqueuedTimeUtc: " + et);
outputItem.setValue(message);
}
}
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attribute to configure the trigger. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#event-hubs-trigger).

Use the `EventHubTriggerAttribute`

to define a trigger on an event hub, which supports the following properties.

| Parameters | Description |
|---|---|
EventHubName |
The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. Can be referenced in
`%eventHubName%` |

**ConsumerGroup**[consumer group](../event-hubs/event-hubs-features#event-consumers)used to subscribe to events in the hub. When omitted, the`$Default`

consumer group is used.**Connection**[Connections](#connections).## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, the following properties on the `event_hub_message_trigger`

:

| Property | Description |
|---|---|
`arg_name` |
The name of the variable that represents the event item in function code. |
`event_hub_name` |
The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. |
`connection` |
The name of an app setting or setting collection that specifies how to connect to Event Hubs. See
|

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the [EventHubTrigger](/en-us/java/api/com.microsoft.azure.functions.annotation.eventhubtrigger) annotation, which supports the following settings:

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `app.eventHub()`

method.

| Property | Description |
|---|---|
eventHubName |
The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. Can be referenced via
`%eventHubName%` |

**consumerGroup**[consumer group](../event-hubs/event-hubs-features#event-consumers)used to subscribe to events in the hub. If omitted, the`$Default`

consumer group is used.**cardinality**`many`

in order to enable batching. If omitted or set to `one`

, a single message is passed to the function.**connection**[Connections](#connections).The following table explains the trigger configuration properties that you set in the *function.json* file, which differs by runtime version.

| function.json property | Description |
|---|---|
type |
Must be set to `eventHubTrigger` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to `in` . This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that represents the event item in function code. |
eventHubName |
The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. Can be referenced via
`%eventHubName%` |

**consumerGroup**[consumer group](../event-hubs/event-hubs-features#event-consumers)used to subscribe to events in the hub. If omitted, the`$Default`

consumer group is used.**cardinality**`many`

in order to enable batching. If omitted or set to `one`

, a single message is passed to the function.**connection**[Connections](#connections).When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

To learn more about how Event Hubs trigger and IoT Hub trigger scales, see [Consuming Events with Azure Functions](/en-us/azure/architecture/serverless/event-hubs-functions/event-hubs-functions#consuming-events-with-azure-functions).

Functions also supports Python SDK type bindings for Azure Event Hubs, which lets you work with data using these underlying SDK types:

Important

Support for Event Hubs SDK types in Python is in Preview and is only supported for the Python v2 programming model. For more information, see [SDK types in Python](functions-reference-python#sdk-type-bindings).

The parameter type supported by the Event Hubs output binding depends on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to process a single event, the Event Hubs trigger can bind to the following types:

| Type | Description |
|---|---|
`string` |
The event as a string. Use when the event is simple text. |
`byte[]` |
The bytes of the event. |
| JSON serializable types | When an event contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

If you are migrating from any older versions of the Event Hubs SDKs, note that this version drops support for the legacy

`Body`

type in favor of [EventBody](/en-us/dotnet/api/azure.messaging.eventhubs.eventdata.eventbody).When you want the function to process a batch of events, the Event Hubs trigger can bind to the following types:

| Type | Description |
|---|---|
`string[]` |
An array of events from the batch, as strings. Each entry represents one event. |
`EventData[]` 1 |
An array of events from the batch, as instances of
|

`T[]`

where `T`

is a JSON serializable type11 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.EventHubs 5.5.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventHubs/5.5.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

The parameter type can be one of the following:

- Any native Java types such as int, String, byte[].
- Nullable values using Optional.
- Any POJO type.

To learn more, see the [EventHubTrigger](/en-us/java/api/com.microsoft.azure.functions.annotation.eventhubtrigger) reference.

## Event metadata

The Event Hubs trigger provides several [metadata properties](functions-bindings-expressions-patterns). Metadata properties can be used as part of binding expressions in other bindings or as parameters in your code. The properties come from the [EventData](/en-us/dotnet/api/microsoft.servicebus.messaging.eventdata) class.

| Property | Type | Description |
|---|---|---|
`PartitionContext` |
|

`PartitionContext`

instance.`EnqueuedTimeUtc`

`DateTime`

`Offset`

`string`

`PartitionKey`

`string`

`Properties`

`IDictionary<String,Object>`

`SequenceNumber`

`Int64`

`SystemProperties`

`IDictionary<String,Object>`

See [code examples](#example) that use these properties earlier in this article.

## Connections

The `connection`

property is a reference to environment configuration that contains name of an application setting containing a connection string. You can get this connection string by selecting the **Connection Information** button for the [namespace](../event-hubs/event-hubs-create#create-an-event-hubs-namespace). The connection string must be for an Event Hubs namespace, not the event hub itself.

The connection string must have at least "read" permissions to activate the function.

This connection string should be stored in an application setting with a name matching the value specified by the `connection`

property of the binding configuration.

Note

Identity-based connections aren't supported by the IoT Hub trigger. If you need to use managed identities end-to-end, you can instead use IoT Hub Routing to send data to an event hub you control. In that way, outbound routing can be authenticated with managed identity the event can be read [from that event hub using managed identity](functions-bindings-event-hubs-trigger?tabs=extensionv5#identity-based-connections).

## host.json properties

The [host.json](functions-host-json#eventhub) file contains settings that control Event Hub trigger behavior. See the [host.json settings](functions-bindings-event-iot#hostjson-settings) section for details regarding available settings.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/flex-consumption-plan -->

# Azure Functions Flex Consumption plan hosting

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Flex Consumption is a Linux-based Azure Functions hosting plan that builds on the Consumption *pay for what you use* serverless billing model. It gives you more flexibility and customizability by introducing private networking, instance memory size selection, and fast/large scale-out features still based on a *serverless* model.

You can review end-to-end samples that feature the Flex Consumption plan in the [Flex Consumption plan samples repository](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples).

## Benefits

The Flex Consumption plan builds on the strengths of the serverless Consumption plan, which include dynamic scaling and execution-based billing. With Flex Consumption, you also get these extra features:

**Reduced Cold Start Times**: Enable[always-ready instances](#always-ready-instances)to achieve faster cold-start times compared to the Consumption plan.**Virtual network support**:[Virtual network integration](#virtual-network-integration)enables your serverless app to run in a virtual network.**Per-Function Scaling**: Each function in your app[scales independently based on its workload](#per-function-scaling), potentially resulting in more efficient resource allocation.**Improved Concurrency Handling**: Better handling of concurrent executions with configurable concurrency settings per function.**Flexible Memory Configuration**: Flex Consumption offers multiple[instance sizes](#instance-sizes)size options, allowing you to optimize for your specific workload requirements.

This table helps you directly compare the features of Flex Consumption with the Consumption hosting plan:

| Feature | Consumption | Flex Consumption |
|---|---|---|
| Scale to zero | ✅ Yes | ✅ Yes |
| Scale behavior |
|

[Event driven](event-driven-scaling)(fast)For a complete comparison of the Flex Consumption plan against the Consumption plan and all other plan and hosting types, see [function scale and hosting options](functions-scale).

Tip

If you're migrating from the Linux Consumption plan, see [Migrate Consumption plan apps to the Flex Consumption plan](migration/migrate-plan-consumption-to-flex?pivots=platform-linux) for step-by-step migration instructions and important differences between the plans.

## Virtual network integration

Flex Consumption expands on the traditional benefits of Consumption plan by adding support for [virtual network integration](functions-networking-options#virtual-network-integration). When your apps run in a Flex Consumption plan, they can connect to other Azure services secured inside a virtual network. All while still allowing you to take advantage of serverless billing and scale, together with the scale and throughput benefits of the Flex Consumption plan. For more information, see [Enable virtual network integration](flex-consumption-how-to#enable-virtual-network-integration).

## Instance sizes

When you create your function app in a Flex Consumption plan, you can select the memory size of the instances on which your app runs. See [Billing](#billing) to learn how instance memory sizes affect the costs of your function app.

Currently, Flex Consumption offers these instance size options:

| Instance Memory (MB) | CPU Cores |
|---|---|
| 512 | 0.25 |
| 2048 | 1 |
| 4096 | 2 |

Note

The CPU core values shown are typical allocations for instances with the specified memory size. However, initial instances might be granted slightly different core allocations to improve performance. Each Flex Consumption instance also includes an extra 272 MB of memory allocated by the platform as a buffer for system and host processes. This extra memory doesn't affect billing, and instances are billed based on the configured instance memory size shown in the preceding table.

When deciding on which instance memory size to use with your apps, here are some things to consider:

- The 2,048-MB instance memory size is the default and should be used for most scenarios. The 512 MB and 4,096-MB instance memory sizes are available for scenarios that best suit your application's concurrency or processing power requirements. For more information, see
[Configure instance memory](flex-consumption-how-to#configure-instance-memory). - You can change the instance memory size at any time. For more information, see
[Configure instance memory](flex-consumption-how-to#configure-instance-memory). - Instance resources are shared between your function code and the Functions host.
- The larger the instance memory size, the more each instance can handle as far as concurrent executions or more intensive CPU or memory workloads. Specific scale decisions are workload-specific.
- The default concurrency of HTTP triggers depends on the instance memory size. For more information, see
[HTTP trigger concurrency](functions-concurrency#http-trigger-concurrency). - Available CPUs and network bandwidth are provided proportional to a specific instance size.

## Per-function scaling

[Concurrency](#concurrency) is a key factor that determines how Flex Consumption function apps scale. To improve the scale performance of apps with various trigger types, the Flex Consumption plan provides a more deterministic way of scaling your app on a per-function basis.

This *per-function scaling* behavior is a part of the hosting platform, so you don't need to configure your app or change the code. For more information, see [Per-function scaling](event-driven-scaling#per-function-scaling) in the Event-driven scaling article.

In per-function scaling, decisions are made for certain function triggers based on group aggregations. This table shows the defined set of function scale groups:

| Scale groups | Triggers in group | Settings value |
|---|---|---|
| HTTP triggers |
|

`http`

(Event Grid-based)

[Blob storage trigger](functions-bindings-storage-blob-trigger)`blob`

[Orchestration trigger](durable/durable-functions-bindings#orchestration-trigger)[Activity trigger](durable/durable-functions-bindings#activity-trigger)[Entity trigger](durable/durable-functions-bindings#entity-trigger)`durable`

All other functions in the app are scaled individually in their own set of instances, which are referenced using the convention `function:<NAMED_FUNCTION>`

.

## Always ready instances

Flex Consumption includes an *always ready* feature that lets you choose instances that are always running and assigned to each of your per-function scale groups or functions. Always ready is a great option for scenarios where you need to have a minimum number of instances always ready to handle requests. For example, to reduce your application's cold start latency. The default is 0 (zero).

For example, if you set always ready to 2 for your HTTP group of functions, the platform keeps two instances always running for those functions. Those instances process your function executions first. Depending on concurrency settings, the platform scales beyond those two instances with on-demand instances.

No less than two always-ready instances can be configured per function or function group while [zone redundancy is enabled](/en-us/azure/reliability/reliability-functions?pivots=flex-consumption-plan#availability-zone-support).

To learn how to configure always ready instances, see [Set always ready instance counts](flex-consumption-how-to#set-always-ready-instance-counts).

## Concurrency

Concurrency refers to the number of parallel executions of a function on an instance of your app. You can set a maximum number of concurrent executions that each instance should handle at any given time. Concurrency has a direct effect on how your app scales because at lower concurrency levels, you need more instances to handle the event-driven demand for a function. While you can control and fine tune the concurrency, we provide defaults that work for most cases.

To learn how to set concurrency limits for HTTP trigger functions, see [Set HTTP concurrency limits](flex-consumption-how-to#set-http-concurrency-limits). To learn how to set concurrency limits for non-HTTP trigger functions, see [Target Base Scaling](functions-target-based-scaling).

## Deployment

Deployments in the Flex Consumption plan follow a single path, and there's no longer the need for app settings to influence deployment behavior. Your project code is built and zipped into an application package, then deployed to a blob storage container. On startup, your app gets the package and runs your function code from this package. By default, the same storage account used to store internal host metadata (AzureWebJobsStorage) is also used as the deployment container. However, you can use an alternative storage account or choose your preferred authentication method by [configuring your app's deployment settings](flex-consumption-how-to#configure-deployment-settings).

Tip

A **Flex Function App deployment details** diagnostic tool is available in the Azure portal. Open your Flex Consumption app, select **Diagnose and solve problems**, and search for `Flex Function App deployment details`

. This tool displays detailed information about your deployments, including deployment history, package status, and troubleshooting recommendations.

### Zero-downtime deployments

Note

Zero-downtime deployments with rolling updates are currently in public preview.

Flex Consumption provides zero-downtime deployments through rolling updates as the [site update strategy](flex-consumption-site-updates), which allows code deployments and configuration changes to be applied gradually across instances without interrupting function execution. Other hosting plans use deployment slots to minimize downtime during deployments. For deployment options across all hosting plans, see [optimize deployments](functions-best-practices#optimize-deployments).

## Billing

There are two modes by which your costs are determined when running your apps in the Flex Consumption plan. Each mode is determined on a per-instance basis.

| Billing mode | Description |
|---|---|
On Demand |
When running in on demand mode, you are billed only for the amount of time your function code is executing on your available instances. In on demand mode, no minimum instance count is required. You're billed for:• The total amount of memory provisioned while each on demand instance is actively executing functions (in GB-seconds), minus a free grant of GB-s per month.• The total number of executions, minus a free grant (number) of executions per month. |
Always ready |
You can configure one or more instances, assigned to specific trigger types (HTTP/Durable/Blob) and individual functions, that are always available to handle requests. When you have any always ready instances enabled, you're billed for: • The total amount of memory provisioned across all of your always ready instances, known as the baseline (in GB-seconds).• The total amount of memory provisioned during the time each always ready instance is actively executing functions (in GB-seconds).• The total number of executions. In always ready billing, there are no free grants. |

For the most up-to-date information on execution pricing, always ready baseline costs, and free grants for on demand executions, see the [Azure Functions pricing page](https://azure.microsoft.com/pricing/details/functions/#pricing).

The minimum billable execution period for both execution modes is 1,000 ms. Past that, the billable activity period is rounded up to the nearest 100 ms. You can find details on the Flex Consumption plan billing meters in the [Monitoring reference](monitor-functions-reference?tab=flex-consumption-plan#metrics).

For details about how costs are calculated when you run in a Flex Consumption plan, including examples, see [Consumption-based costs](functions-consumption-costs?tabs=flex-consumption-plan#consumption-based-costs) and [Viewing cost-related data](functions-consumption-costs?tabs=flex-consumption-plan#viewing-and-estimating-costs-from-metrics).

## Supported language stack versions

This table shows the language stack versions that are currently supported for Flex Consumption apps:

| Language stack | Required version |
|---|---|
C# (isolated worker model)1 |
.NET 8, .NET 9, .NET 10 |
| Java | Java 11, Java 17, Java 21 |
| Node.js | Node.js 20, Node.js 22 |
| PowerShell | PowerShell 7.4 |
| Python | Python 3.10, Python 3.11, Python 3.12 |

- The
[C# in-process model](functions-dotnet-class-library)isn't supported. You instead need to[migrate your .NET project to the isolated worker model](migrate-dotnet-to-isolated-model).

## Regional subscription memory quotas

All Flex Consumption apps in a subscription and region share a compute quota, like a shared bucket of resources. This quota applies only to Flex Consumption apps — other hosting plans like Consumption, Premium, and Dedicated don't count against it. The quota limits how much total compute your Flex Consumption apps can use at the same time. If your apps try to exceed the quota, some executions and deployments might be delayed or fail, and scaling is throttled. However, you can still create new apps.

### Default quota

Each region in a subscription has a default quota of **250 cores** (equivalent to **512,000 MB**) for all Flex Consumption app instances combined. You can use any combination of instance sizes and counts, as long as the total cores stay under the quota.

To calculate the cores used, multiply the cores per instance by the number of instances:

| Instance size | Cores per instance | Formula |
|---|---|---|
| 512 MB | 0.25 | instances × 0.25 |
| 2,048 MB | 1 | instances × 1 |
| 4,096 MB | 2 | instances × 2 |

### Quota examples

Each of these scenarios reaches the 250 core quota limit. When the quota is reached, apps in the region stop scaling:

| Scenario | Calculation | Total cores |
|---|---|---|
| One 512-MB app at 1,000 instances | 1,000 × 0.25 | 250 |
| Two 512-MB apps at 250 and 750 instances | (250 + 750) × 0.25 | 250 |
| One 2,048-MB app at 250 instances | 250 × 1 | 250 |
| Two 2,048-MB apps at 100 and 150 instances | (100 + 150) × 1 | 250 |
| One 4,096-MB app at 125 instances | 125 × 2 | 250 |
| One 4,096-MB app at 100 instances + one 2,048-MB app at 50 instances | (100 × 2) + (50 × 1) | 250 |

### Important notes

- Flex Consumption scales rapidly based on
[concurrency](#concurrency)settings, so apps frequently acquire and release cores from the quota as demand changes. - Flex Consumption apps that scale to zero, or instances marked to be scaled in and deleted, don't count against the quota.
- Always ready instances count against quota.
- A
**Flex Consumption Quota tool**is available in the Azure portal. Open any Flex Consumption app in your subscription, select**Diagnose and solve problems**, search for`Flex Consumption Quota`

, then choose a region. The tool displays recommendations, current quota information, and historical usage views. - This quota can be increased pending capacity review. For example, from 250 cores to 1,000 cores or more. To request a larger quota, create a support ticket or contact your Microsoft account team.

## Deprecated properties and settings

In the Flex Consumption plan, many standard application settings and site configuration properties are deprecated or moved. Don't use these settings when you automate function app resource creation. For more information, see [Flex Consumption plan deprecations](functions-app-settings#flex-consumption-plan-deprecations).

## Considerations

Keep these other considerations in mind when using Flex Consumption plan:

**Apps per Plan**: Only one app is allowed per Flex Consumption plan.**Host**: There's a 30-second time-out for app initialization. When your function app takes longer than 30 seconds to start, you might see gRPC-related`System.TimeoutException`

entries logged. You can't currently configure this time-out. For more information, see[this host work item](https://github.com/Azure/azure-functions-host/issues/10482).**Durable Functions**: Azure Storage and Durable Task Scheduler are the only supported[storage providers](durable/durable-functions-storage-providers)for Durable Functions when hosted in the Flex Consumption plan. See[recommendations](durable/durable-functions-azure-storage-provider#flex-consumption-plan)when hosting Durable Functions in the Flex Consumption plan.**Virtual network integration and Resource provider registration**: You must have the`Microsoft.App`

Azure resource provider registered in your subscription to integrate to a virtual network, which is needed for subnet delegation. The Azure portal and Azure CLI enforce registration at app creation time since virtual network integration can be enabled at any point after your app is created. To register this provider,[follow these instructions](/en-us/azure/azure-resource-manager/management/resource-providers-and-types#register-resource-provider). The subnet delegation required by Flex Consumption apps is`Microsoft.App/environments`

.**Triggers**: While all triggers are fully supported in a Flex Consumption plan, the Blob storage trigger only supports the[Event Grid source](functions-event-grid-blob-trigger). Non-C# function apps must use version`[4.0.0, 5.0.0)`

of the[extension bundle](extension-bundles), or a later version.**Regions**: While the Flex Consumption plan is available in many Azure regions, not all regions are currently supported. To learn more, see[View currently supported regions](flex-consumption-how-to#view-currently-supported-regions).**Deployments**: Deployment slots aren't currently supported. For zero downtime deployments with Flex Consumption, see[Site update strategies in Flex Consumption](flex-consumption-site-updates).**Azure Storage as a local share**: Network File System (NFS) file shares aren't available for Flex Consumption. Only Server Message Block (SMB) and Azure Blobs (read-only) are supported.**Scale**: The lowest maximum scale is currently`40`

. The highest currently supported value is`1000`

.**PowerShell Managed dependencies**: Flex Consumption doesn't support[managed dependencies in PowerShell](functions-reference-powershell#managed-dependencies-feature). You must instead[upload modules with app content](functions-reference-powershell#including-modules-in-app-content).**Certificates**: Loading certificates with the WEBSITE_LOAD_CERTIFICATES app setting, managed certificates, app service certificates, and other platform certificate-based features like endToEndEncryptionEnabled are currently not supported.**Timezones**:`WEBSITE_TIME_ZONE`

and`TZ`

app settings aren't currently supported when running on Flex Consumption plan.**Azure Functions Runtime Version and Proxies**: Flex Consumption only supports version 4.x and later of the Azure Functions runtime. Azure Functions proxies was a feature of versions 1.x through 3.x of the Azure Functions runtime and is not available in Flex Consumption.

## Related articles

[Azure Functions hosting options](functions-scale)
[Create and manage function apps in the Flex Consumption plan](flex-consumption-how-to)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-mobile-apps -->

# Mobile Apps bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

Azure Mobile Apps bindings are only available to Azure Functions 1.x. They are not supported in Azure Functions 2.x and higher.

Important

[Support will end for version 1.x of the Azure Functions runtime on September 14, 2026](https://aka.ms/azure-functions-retirements/hostv1). We highly recommend that you [migrate your apps to version 4.x](migrate-version-1-version-4) for full support.

This article explains how to work with [Azure Mobile Apps](/en-us/previous-versions/azure/app-service-mobile/app-service-mobile-value-prop) bindings in Azure Functions. Azure Functions supports input and output bindings for Mobile Apps.

The Mobile Apps bindings let you read and update data tables in mobile apps.

## Packages - Functions 1.x

Mobile Apps bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.MobileApps](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps) NuGet package, version 1.x. Source code for the package is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.MobileApps/) GitHub repository.

The following table lists how to add support for output binding in each development environment.

| Development environment | To add support in Functions 1.x |
|---|---|
| Local development: C# class library |
|

## Input

The Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function. In C# and F# functions, any changes made to the record are automatically sent back to the table when the function exits successfully.

## Input - example

See the language-specific example:

The following example shows a Mobile Apps input binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding. The function is triggered by a queue message that has a record identifier. The function reads the specified record and modifies its `Text`

property.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"name": "myQueueItem",
"queueName": "myqueue-items",
"connection": "",
"type": "queueTrigger",
"direction": "in"
},
{
"name": "record",
"type": "mobileTable",
"tableName": "MyTable",
"id": "{queueTrigger}",
"connection": "My_MobileApp_Url",
"apiKey": "My_MobileApp_Key",
"direction": "in"
}
]
}
```


The [configuration](#input---configuration) section explains these properties.

Here's the C# script code:

```
#r "Newtonsoft.Json"
using Newtonsoft.Json.Linq;
public static void Run(string myQueueItem, JObject record)
{
if (record != null)
{
record["Text"] = "This has changed.";
}
}
```


## Input - attributes

In [C# class libraries](functions-dotnet-class-library), use the [MobileTable](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) attribute.

For information about attribute properties that you can configure, see [the following configuration section](#input---configuration).

## Input - configuration

The following table explains the binding configuration properties that you set in the *function.json* file and the `MobileTable`

attribute.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Must be set to "mobileTable" |
direction |
n/a | Must be set to "in" |
name |
n/a | Name of input parameter in function signature. |
tableName |
TableName |
Name of the mobile app's data table |
id |
Id |
The identifier of the record to retrieve. Can be static or based on the trigger that invokes the function. For example, if you use a queue trigger for your function, then `"id": "{queueTrigger}"` uses the string value of the queue message as the record ID to retrieve. |
connection |
Connection |
The name of an app setting that has the mobile app's URL. The function uses this URL to construct the required REST operations against your mobile app. Create an app setting in your function app that contains the mobile app's URL, then specify the name of the app setting in the `connection` property in your input binding. The URL looks like `https://<appname>.azurewebsites.net` . |
apiKey |
ApiKey |
The name of an app setting that has your mobile app's API key. Provide the API key if you implement an API key in your Node.js mobile app, or implement an API key in your .NET mobile app. To provide the key, create an app setting in your function app that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting. |

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

Important

Don't share the API key with your mobile app clients. It should only be distributed securely to service-side clients, like Azure Functions. Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository. This safeguards your sensitive information.

## Input - usage

In C# functions, when the record with the specified ID is found, it is passed into the named
[JObject](https://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter. When the record is not found, the parameter value is `null`

.

In JavaScript functions, the record is passed into the `context.bindings.<name>`

object. When the record is not found, the parameter value is `null`

.

In C# and F# functions, any changes you make to the input record (input parameter) are automatically sent back to the table when the function exits successfully. You can't modify a record in JavaScript functions.

## Output

Use the Mobile Apps output binding to write a new record to a Mobile Apps table.

## Output - example

The following example shows a [C# function](functions-dotnet-class-library) that is triggered by a queue message and creates a record in a mobile app table.

```
[FunctionName("MobileAppsOutput")]
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run(
[QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem,
TraceWriter log)
{
return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```


## Output - attributes

In [C# class libraries](functions-dotnet-class-library), use the [MobileTable](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) attribute.

For information about attribute properties that you can configure, see [Output - configuration](#output---configuration). Here's a `MobileTable`

attribute example in a method signature:

```
[FunctionName("MobileAppsOutput")]
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run(
[QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem,
TraceWriter log)
{
...
}
```


## Output - configuration

The following table explains the binding configuration properties that you set in the *function.json* file and the `MobileTable`

attribute.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Must be set to "mobileTable" |
direction |
n/a | Must be set to "out" |
name |
n/a | Name of output parameter in function signature. |
tableName |
TableName |
Name of the mobile app's data table |
connection |
MobileAppUriSetting |
The name of an app setting that has the mobile app's URL. The function uses this URL to construct the required REST operations against your mobile app. Create an app setting in your function app that contains the mobile app's URL, then specify the name of the app setting in the `connection` property in your input binding. The URL looks like `https://<appname>.azurewebsites.net` . |
apiKey |
ApiKeySetting |
The name of an app setting that has your mobile app's API key. Provide the API key if you implement an API key in your Node.js mobile app backend, or implement an API key in your .NET mobile app backend. To provide the key, create an app setting in your function app that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting. |

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

Important

Don't share the API key with your mobile app clients. It should only be distributed securely to service-side clients, like Azure Functions. Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository. This safeguards your sensitive information.

## Output - usage

In C# script functions, use a named output parameter of type `out object`

to access the output record. In C# class libraries, the `MobileTable`

attribute can be used with any of the following types:

`ICollector<T>`

or`IAsyncCollector<T>`

, where`T`

is either`JObject`

or any type with a`public string Id`

property.`out JObject`

`out T`

or`out T[]`

, where`T`

is any Type with a`public string Id`

property.

In Node.js functions, use `context.bindings.<name>`

to access the output record.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-reliable-event-processing -->

# Reliable event processing with Azure Functions and Event Hubs

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Learn how to build robust, reliable serverless solutions using Azure Functions with Azure Event Hubs triggers. This article covers best practices for checkpoints, error handling, and implementing circuit breaker patterns to ensure no events are lost and your event-driven applications remain stable and resilient.

## Challenges of event streams in distributed systems

Consider a system that sends events at a constant rate of 100 events per second. At this rate, within minutes multiple parallel instances can consume the incoming 100 events every second.

However, consider these challenges to consuming an event stream:

- An event publisher sends a corrupt event.
- Your function code encounters an unhandled exception.
- A downstream system goes offline and blocks event processing.

Unlike an Azure Queue storage trigger, which locks messages during processing, Azure Event Hubs reads, per partition, from a single point in the stream. This read behavior, which is more like a video player, provides the desired benefits of high-throughput, multiple consumer groups, and replay-ability. Events are read, forward or backward, from a checkpoint, but you must move the pointer to process new events. For more information, see [Checkpoint](../event-hubs/event-processor-balance-partition-load#checkpoint) in the Event Hubs documentation.

When errors occur in a stream and you choose not to advance the pointer, further event processing is blocked. In other words, should you stop the pointer to deal with an issue processing a single event, the unprocessed events begin piling up.

Functions avoids deadlocks by always advancing the stream's pointer, regardless of success or failure. Because the pointer keeps advancing, your functions need to deal with failures appropriately.

## How the Event Hubs trigger consumes events

Azure Functions consumes events from an event hub by cycling through the following steps:

- A pointer is created and persisted in Azure Storage for each partition of the event hub.
- New events are received in a batch (by default), and the host tries to trigger the function supplying a the batch of events for processing.
- When the function completes execution, with or without exceptions, the pointer is advanced and a checkpoint is saved to the default host storage account.
- Should conditions prevent function execution from completing, the host can't advance the pointer. When the pointer can't advance, subsequent executions reprocess the same events.

This behavior reveals a few important points:

Unhandled exceptions might cause you to lose events:

Function executions that raise an exception continue to progress the pointer. Setting a

[retry policy](#retry-policies)or other retry logic delays advancing the pointer until the entire retry completes.Functions guarantees

*at-least-once*delivery:Your code and dependent systems might need to account for the fact that the same event could be processed twice. For more information, see

[Designing Azure Functions for identical input](functions-idempotent).

## Handling exceptions

While all function code should include a [try/catch block](functions-bindings-error-pages) at the highest level of code, having a `catch`

block is even more important for functions that consume Event Hubs events. That way, when an exception is raised, the catch block handles the error before the pointer progresses.

## Retry mechanisms and policies

Because many exceptions in the cloud are transient, the first step in error handling is always to retry the operation. You can apply built-in retry policies or define your own retry logic.

### Retry policies

Functions provides built-in retry policies for Event Hubs. When using retry policies, you simply raise a new exception and the host try to process the event again based on the defined policy. This retry behavior requires version 5.x or later of the Event Hubs extension. For more information, see [Retry policies](functions-bindings-error-pages#retry-policies).

### Custom retry logic

You can also define your own retry logic in the function itself. For example, you could implement a policy that follows a workflow illustrated by the following rules:

- Try to process an event three times (potentially with a delay between retries).
- If the eventual outcome of all retries is a failure, then add an event to a queue so processing can continue on the stream.
- Corrupt or unprocessed events are then handled later.

Note

[Polly](https://github.com/App-vNext/Polly) is an example of a resilience and transient-fault-handling library for C# applications.

## Nonexception errors

Some issues can occur without an exception being raised. For example, consider a case where a request times out or the instance running the function crashes. When a function fails to complete without an exception, the offset pointer is never advanced. If the pointer doesn't advance, then any instance that runs after a failed execution continues to read the same events. This situation provides an *at-least-once* guarantee.

The assurance that every event is processed at least one time implies that some events could be processed more than once. Your function apps need to be aware of this possibility and must be built around the [principles of idempotency](functions-idempotent).

## Handling failure states

Your app might be able to acceptably handle a few errors in event processing. However, you should also be prepared to handle persistent failure state, which might occur as a result of failures in downstream processing. In such a failure state, such as a downstream data store being offline, your function should stop triggering on events until the system reaches a healthy state.

### Circuit breaker pattern

When you implement the *circuit breaker* pattern, your app can effectively pause event processing and then resume it at a later time after issues are resolved.

There are two components required to implement a circuit breaker in an event stream process:

- Shared state across all instances to track and monitor health of the circuit.
- A primary process that can manage the circuit state, as either
`open`

or`closed`

.

Implementation details can vary, but to share state among instances you need a storage mechanism. You can store state in Azure Storage, a Redis cache, or any other persistent service that can be accessed by your function app instances.

Both [Durable Functions](durable/durable-functions-overview) and [Azure Logic Apps](../logic-apps/logic-apps-overview) provide infrastructure to manage workflows and circuit states. This article describes using Logic Apps to pause and restart function executions, giving you the control required to implement the circuit breaker pattern.

### Define a failure threshold across instances

Persisted shared external state is required to monitor the health of the circuit when multiple instances are processing events simultaneously. You can then monitor this persisted state based on rules that indicate a failure state, such as:

When there are more than 100 event failures within a 30-second period across all instances, break the circuit to stop triggering on new events.


The implementation details for this monitoring logic vary depending on your specific app needs, but in general you must create a system that:

- Logs failures to persisted storage.
- Inspect the rolling count when new failures are logged to determine if the event failure threshold is met.
- When this threshold is met, emit an event telling the system to break the circuit.

### Managing circuit state with Azure Logic Apps

Azure Logic Apps comes with built-in connectors to different services, features, and stateful orchestrations, and it's a natural choice to manage circuit state. After detecting when a circuit must break, you can build a logic app to implement this workflow:

- Trigger an Event Grid workflow that stops the function processing.
- Send a notification email that includes an option to restart the workflow.

To learn how to disable and reenable specific functions using app settings, see [How to disable functions in Azure Functions](disable-function).

The email recipient can investigate the health of the circuit and, when appropriate, restart the circuit via a link in the notification email. As the workflow restarts the function, events are processed from the last event hub checkpoint.

When you use this approach, no events are lost, events are processed in order, and you can break the circuit as long as necessary.

## Migration strategies for Event Grid triggers

When you migrate an existing function app between regions or between some plans, you must recreate the app during the migration process. In this case, during the migration process, you might have two apps that are both able to consume from the same event stream and write to the same output destination.

You should consider [using consumer groups](../event-hubs/event-hubs-features#consumer-groups) to avoid event data loss or duplication during the migration process:

Create a new consumer group for the new target app.

Configure the trigger in the new app to use this new consumer group.

This allows both apps to process events independently during validation.

Validate that the new app is processing events correctly.

Stop the original app or remove its subscription/consumer group.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2 -->

# Azure Cosmos DB trigger and bindings for Azure Functions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This set of articles explains how to work with [Azure Cosmos DB](/en-us/azure/cosmos-db/serverless-computing-database) bindings in Azure Functions. Azure Functions supports trigger, input, and output bindings for Azure Cosmos DB. For an end-to-end scenario that uses the Azure Cosmos DB extension, see [Quickstart: Respond to database changes in Azure Cosmos DB using Azure Functions](scenario-database-changes-azure-cosmosdb).

| Action | Type |
|---|---|
| Run a function when an Azure Cosmos DB document is created or modified |
|

[Input binding](functions-bindings-cosmosdb-v2-input)[Output binding](functions-bindings-cosmosdb-v2-output)Important

This version of the Azure Cosmos DB binding extension supports [Azure Functions version 4.x](functions-versions). If your app still uses version 1.x of the Functions runtime, instead see [Azure Cosmos DB bindings for Azure Functions 1.x](functions-bindings-cosmosdb).
In the Functions v1.x runtime, this binding was originally named `DocumentDB`

.

## Supported APIs

This table indicates how to connect to the various Azure Cosmos DB APIs from your function code:

## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The process for installing the extension varies depending on the extension version:

This version of the Azure Cosmos DB bindings extension introduces the ability to [connect using an identity instead of a secret](functions-reference#configure-an-identity-based-connection). For a tutorial on configuring your function apps with managed identities, see the [creating a function app with identity-based connections tutorial](functions-identity-based-connections-tutorial).

Add the extension to your project by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.CosmosDB/), version 4.x.

If you're writing your application using F#, you must also configure this extension as part of the app's [startup configuration](dotnet-isolated-process-guide#start-up-and-configuration). In the call to `ConfigureFunctionsWorkerDefaults()`

or `ConfigureFunctionsWebApplication()`

, add a delegate that takes an `IFunctionsWorkerApplication`

parameter. Then within the body of that delegate, call `ConfigureCosmosDBExtension()`

on the object:

```
let hostBuilder = new HostBuilder()
hostBuilder.ConfigureFunctionsWorkerDefaults(fun (context: HostBuilderContext) (appBuilder: IFunctionsWorkerApplicationBuilder) ->
appBuilder.ConfigureCosmosDBExtension() |> ignore
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

Because of schema changes in the Azure Cosmos DB SDK, version 4.x of the Azure Cosmos DB extension requires [azure-functions-java-library V3.0.0](https://central.sonatype.com/artifact/com.microsoft.azure.functions/azure-functions-java-library/3.0.0) for Java functions.

## Binding types

The binding types supported for .NET depend on both the extension version and C# execution mode, which can be one of the following:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see binding type details for the mode and version.

The isolated worker process supports parameter types according to the tables below. Support for binding to types from [Microsoft.Azure.Cosmos](/en-us/dotnet/api/microsoft.azure.cosmos)is in preview.

**Cosmos DB trigger**

When you want the function to process a single document, the Cosmos DB trigger can bind to the following types:

| Type | Description |
|---|---|
| JSON serializable types | Functions tries to deserialize the JSON data of the document from the Cosmos DB change feed into a plain-old CLR object (POCO) type. |

When you want the function to process a batch of documents, the Cosmos DB trigger can bind to the following types:

| Type | Description |
|---|---|
`IEnumerable<T>` where `T` is a JSON serializable type |
An enumeration of entities included in the batch. Each entry represents one document from the Cosmos DB change feed. |

**Cosmos DB input binding**

When you want the function to process a single document, the Cosmos DB input binding can bind to the following types:

| Type | Description |
|---|---|
| JSON serializable types | Functions attempts to deserialize the JSON data of the document into a plain-old CLR object (POCO) type. |

When you want the function to process multiple documents from a query, the Cosmos DB input binding can bind to the following types:

| Type | Description |
|---|---|
`IEnumerable<T>` where `T` is a JSON serializable type |
An enumeration of entities returned by the query. Each entry represents one document. |
1 |

[Database](/en-us/dotnet/api/microsoft.azure.cosmos.database)1[Container](/en-us/dotnet/api/microsoft.azure.cosmos.container)11 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.CosmosDB 4.4.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.CosmosDB/4.4.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

**Cosmos DB output binding**

When you want the function to write to a single document, the Cosmos DB output binding can bind to the following types:

| Type | Description |
|---|---|
| JSON serializable types | An object representing the JSON content of a document. Functions attempts to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write to multiple documents, the Cosmos DB output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is JSON serializable type |
An array containing multiple documents. Each entry represents one document. |

For other output scenarios, create and use a [CosmosClient](/en-us/dotnet/api/microsoft.azure.cosmos.cosmosclient) with other types from [Microsoft.Azure.Cosmos](/en-us/dotnet/api/microsoft.azure.cosmos) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

## SDK Binding Types

SDK Type support for Azure Cosmos is in Preview. Follow the [Python SDK Bindings for CosmosDB Sample](https://github.com/Azure-Samples/azure-functions-cosmosdb-sdk-bindings-python) to get started with SDK Types for Cosmos in Python.

Important

Using SDK type bindings requires the [Python v2 programming model](functions-reference-python?pivots=python-mode-decorators#sdk-type-bindings).

| Binding | Parameter types | Samples |
|---|---|---|
| CosmosDB input |
|

[,](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-cosmosdb/samples/cosmosdb_samples_containerproxy/function_app.py)`ContainerProxy`

[,](https://github.com/Azure/azure-functions-python-extensions/tree/dev/azurefunctions-extensions-bindings-cosmosdb/samples/cosmosdb_samples_cosmosclient/function_app.py)`CosmosClient`

`DatabaseProxy`

## Exceptions and return codes

| Binding | Reference |
|---|---|
| Azure Cosmos DB |
|

## host.json settings

This section describes the configuration settings available for this binding in version 2.x and later. Settings in the host.json file apply to all functions in a function app instance. For more information about function app configuration settings, see [host.json reference for Azure Functions](functions-host-json).

```
{
"version": "2.0",
"extensions": {
"cosmosDB": {
"connectionMode": "Gateway",
"userAgentSuffix": "MyDesiredUserAgentStamp"
}
}
}
```


| Property | Default | Description |
|---|---|---|
connectionMode |
`Gateway` |
The connection mode used by the function when connecting to the Azure Cosmos DB service. Options: `Direct` connects directly to backend replicas over TCP and can provide lower latency, and `Gateway` routes requests through a front-end gateway over HTTPS. For more information, see
|
userAgentSuffix |
n/a | Adds the specified string value to all requests made by the trigger or binding to the service. This makes it easier for you to track the activity in Azure Monitor, based on a specific function app and filtering by `User Agent` . |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai-assistant-trigger -->

# Azure OpenAI assistant trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Azure OpenAI extension for Azure Functions is currently in preview.

The Azure OpenAI assistant trigger lets you run your code based on custom chat bot or skill request made to an assistant.

For information on setup and configuration details of the Azure OpenAI extension, see [Azure OpenAI extensions for Azure Functions](functions-bindings-openai). To learn more about Azure OpenAI assistants, see [Azure OpenAI Assistants API](/en-us/azure/ai-services/openai/concepts/assistants).

Note

References and examples are only provided for the [Node.js v4 model](functions-reference-node?pivots=nodejs-model-v4).

Note

References and examples are only provided for the [Python v2 model](functions-reference-python?pivots=python-mode-decorators#programming-model).

Note

While both C# process models are supported, only [isolated worker model](dotnet-isolated-process-guide) examples are provided.

## Example

This example demonstrates how to create an assistant that adds a new todo task to a database. The trigger has a static description of `Create a new todo task`

used by the model. The function itself takes a string, which represents a new task to add. When executed, the function adds the task as a new todo item in a custom item store and returns a response from the store.

```
[Function(nameof(AddTodo))]
public Task AddTodo([AssistantSkillTrigger("Create a new todo task")] string taskDescription)
{
if (string.IsNullOrEmpty(taskDescription))
{
throw new ArgumentException("Task description cannot be empty");
}
this.logger.LogInformation("Adding todo: {task}", taskDescription);
string todoId = Guid.NewGuid().ToString()[..6];
return this.todoManager.AddTodoAsync(new TodoItem(todoId, taskDescription));
}
```


This example demonstrates how to create an assistant that adds a new todo task to a database. The trigger has a static description of `Create a new todo task`

used by the model. The function itself takes a string, which represents a new task to add. When executed, the function adds the task as a new todo item in a custom item store and returns a response from the store.

```
/**
* Called by the assistant to create new todo tasks.
*/
@FunctionName("AddTodo")
public void addTodo(
@AssistantSkillTrigger(
name = "assistantSkillCreateTodo",
functionDescription = "Create a new todo task"
) String taskDescription,
final ExecutionContext context) {
if (taskDescription == null || taskDescription.isEmpty()) {
throw new IllegalArgumentException("Task description cannot be empty");
}
context.getLogger().info("Adding todo: " + taskDescription);
String todoId = UUID.randomUUID().toString().substring(0, 6);
TodoItem todoItem = new TodoItem(todoId, taskDescription);
todoManager.addTodo(todoItem);
}
```


This example demonstrates how to create an assistant that adds a new todo task to a database. The trigger has a static description of `Create a new todo task`

used by the model. The function itself takes a string, which represents a new task to add. When executed, the function adds the task as a new todo item in a custom item store and returns a response from the store.

```
const { app, trigger } = require("@azure/functions");
const { TodoItem, CreateTodoManager } = require("../services/todoManager");
const { randomUUID } = require('crypto');
const todoManager = CreateTodoManager()
app.generic('AddTodo', {
trigger: trigger.generic({
type: 'assistantSkillTrigger',
functionDescription: 'Create a new todo task'
}),
handler: async (taskDescription, context) => {
if (!taskDescription) {
throw new Error('Task description cannot be empty')
}
context.log(`Adding todo: ${taskDescription}`)
const todoId = randomUUID().substring(0, 6)
return todoManager.AddTodo(new TodoItem(todoId, taskDescription))
}
})
```


```
import { InvocationContext, app, trigger } from "@azure/functions"
import { TodoItem, ITodoManager, CreateTodoManager } from "../services/todoManager"
import { randomUUID } from 'crypto';
const todoManager: ITodoManager = CreateTodoManager()
app.generic('AddTodo', {
trigger: trigger.generic({
type: 'assistantSkillTrigger',
functionDescription: 'Create a new todo task'
}),
handler: async (taskDescription: string, context: InvocationContext) => {
if (!taskDescription) {
throw new Error('Task description cannot be empty')
}
context.log(`Adding todo: ${taskDescription}`)
const todoId = randomUUID().substring(0, 6)
return todoManager.AddTodo(new TodoItem(todoId, taskDescription))
}
})
```


This example demonstrates how to create an assistant that adds a new todo task to a database. The trigger has a static description of `Create a new todo task`

used by the model. The function itself takes a string, which represents a new task to add. When executed, the function adds the task as a new todo item in a custom item store and returns a response from the store.

Here's the *function.json* file for Add Todo:

```
{
"bindings": [
{
"name": "TaskDescription",
"type": "assistantSkillTrigger",
"dataType": "string",
"direction": "in",
"functionDescription": "Create a new todo task"
}
]
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

```
using namespace System.Net
param($TaskDescription, $TriggerMetadata)
$ErrorActionPreference = "Stop"
if (-not $TaskDescription) {
throw "Task description cannot be empty"
}
Write-Information "Adding todo: $TaskDescription"
$todoID = [Guid]::NewGuid().ToString().Substring(0, 5)
Add-Todo $todoId $TaskDescription
```


This example demonstrates how to create an assistant that adds a new todo task to a database. The trigger has a static description of `Create a new todo task`

used by the model. The function itself takes a string, which represents a new task to add. When executed, the function adds the task as a new todo item in a custom item store and returns a response from the store.

```
@skills.function_name("AddTodo")
@skills.assistant_skill_trigger(
arg_name="taskDescription", function_description="Create a new todo task"
)
def add_todo(taskDescription: str) -> None:
if not taskDescription:
raise ValueError("Task description cannot be empty")
logging.info(f"Adding todo: {taskDescription}")
todo_id = str(uuid.uuid4())[0:6]
todo_manager.add_todo(TodoItem(id=todo_id, task=taskDescription))
return
```


## Attributes

Apply the `AssistantSkillTrigger`

attribute to define an assistant trigger, which supports these parameters:

| Parameter | Description |
|---|---|
FunctionDescription |
Gets the description of the assistant function, which is provided to the model. |
FunctionName |
Optional. Gets or sets the name of the function called by the assistant. |
ParameterDescriptionJson |
Optional. Gets or sets a JSON description of the function parameter, which is provided to the model. For more information, see
|

## Annotations

The `AssistantSkillTrigger`

annotation enables you to define an assistant trigger, which supports these parameters:

| Element | Description |
|---|---|
name |
Gets or sets the name of the input binding. |
functionDescription |
Gets the description of the assistant function, which is provided to the model. |
functionName |
Optional. Gets or sets the name of the function called by the assistant. |
parameterDescriptionJson |
Optional. Gets or sets a JSON description of the function parameter, which is provided to the model. For more information, see
|

## Decorators

During the preview, define the input binding as a `generic_trigger`

binding of type `assistantSkillTrigger`

, which supports these parameters:

| Parameter | Description |
|---|---|
function_description |
Gets the description of the assistant function, which is provided to the model. |
function_name |
Optional. Gets or sets the name of a function called by the assistant. |
parameterDescriptionJson |
Optional. Gets or sets a JSON description of the function parameter, which is provided to the model. For more information, see
|

## Configuration

The binding supports these configuration properties that you set in the function.json file.

| Property | Description |
|---|---|
type |
Must be `AssistantSkillTrigger` . |
direction |
Must be `in` . |
name |
The name of the trigger. |
functionName |
Gets or sets the name of the function called by the assistant. |
functionDescription |
Gets the description of the assistant function, which is provided to the language model. |
parameterDescriptionJson |
Optional. Gets or sets a JSON description of the function parameter, which is provided to the model. For more information, see
|

## Configuration

The binding supports these properties, which are defined in your code:

| Property | Description |
|---|---|
type |
Must be `AssistantSkillTrigger` . |
name |
The name of the trigger. |
functionName |
Gets or sets the name of the function called by the assistant. |
functionDescription |
Gets the description of the assistant function, which is provided to the LLM |
parameterDescriptionJson |
Optional. Gets or sets a JSON description of the function parameter, which is provided to the model. For more information, see
|

See the [Example section](#example) for complete examples.

## Usage

When `parameterDescriptionJson`

JSON value isn't provided, it's autogenerated. For more information on the syntax of this object, see the [OpenAI API documentation](https://platform.openai.com/docs/api-reference/chat/create#chat-create-tools).
