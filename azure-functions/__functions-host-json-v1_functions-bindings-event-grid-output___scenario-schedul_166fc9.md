---
merged_at: 2026-01-26T23:29:57.713849
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-host-json-v1 -->

# host.json reference for Azure Functions 1.x

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The *host.json* metadata file contains configuration options that affect all functions in a function app instance. This article lists the settings that are available for the version 1.x runtime. The JSON schema is at [http://json.schemastore.org/host](http://json.schemastore.org/host).

Note

This article is for Azure Functions 1.x. For a reference of host.json in Functions 2.x and later, see [host.json reference for Azure Functions 2.x](functions-host-json).

Other function app configuration options are managed in your [app settings](functions-app-settings).

Some host.json settings are only used when running locally in the [local.settings.json](functions-develop-local#local-settings-file) file.

## Sample host.json file

The following sample *host.json* files have all possible options specified.

```
{
"aggregator": {
"batchSize": 1000,
"flushTimeout": "00:00:30"
},
"applicationInsights": {
"sampling": {
"isEnabled": true,
"maxTelemetryItemsPerSecond" : 5
}
},
"documentDB": {
"connectionMode": "Gateway",
"protocol": "Https",
"leaseOptions": {
"leasePrefix": "prefix"
}
},
"eventHub": {
"maxBatchSize": 64,
"prefetchCount": 256,
"batchCheckpointFrequency": 1
},
"functions": [ "QueueProcessor", "GitHubWebHook" ],
"functionTimeout": "00:05:00",
"healthMonitor": {
"enabled": true,
"healthCheckInterval": "00:00:10",
"healthCheckWindow": "00:02:00",
"healthCheckThreshold": 6,
"counterThreshold": 0.80
},
"http": {
"routePrefix": "api",
"maxOutstandingRequests": 20,
"maxConcurrentRequests": 10,
"dynamicThrottlesEnabled": false
},
"id": "9f4ea53c5136457d883d685e57164f08",
"logger": {
"categoryFilter": {
"defaultLevel": "Information",
"categoryLevels": {
"Host": "Error",
"Function": "Error",
"Host.Aggregator": "Information"
}
}
},
"queues": {
"maxPollingInterval": 2000,
"visibilityTimeout" : "00:00:30",
"batchSize": 16,
"maxDequeueCount": 5,
"newBatchThreshold": 8
},
"sendGrid": {
"from": "Contoso Group <admin@contoso.com>"
},
"serviceBus": {
"maxConcurrentCalls": 16,
"prefetchCount": 100,
"autoRenewTimeout": "00:05:00",
"autoComplete": true
},
"singleton": {
"lockPeriod": "00:00:15",
"listenerLockPeriod": "00:01:00",
"listenerLockRecoveryPollingInterval": "00:01:00",
"lockAcquisitionTimeout": "00:01:00",
"lockAcquisitionPollingInterval": "00:00:03"
},
"tracing": {
"consoleLevel": "verbose",
"fileLoggingMode": "debugOnly"
},
"watchDirectories": [ "Shared" ],
}
```


The following sections of this article explain each top-level property. All are optional unless otherwise indicated.

## aggregator

Specifies how many function invocations are aggregated when [calculating metrics for Application Insights](configure-monitoring#configure-the-aggregator).

```
{
"aggregator": {
"batchSize": 1000,
"flushTimeout": "00:00:30"
}
}
```


| Property | Default | Description |
|---|---|---|
| batchSize | 1000 | Maximum number of requests to aggregate. |
| flushTimeout | 00:00:30 | Maximum time period to aggregate. |

Function invocations are aggregated when the first of the two limits are reached.

## applicationInsights

Controls the [sampling feature in Application Insights](configure-monitoring#configure-sampling).

```
{
"applicationInsights": {
"sampling": {
"isEnabled": true,
"maxTelemetryItemsPerSecond" : 5
}
}
}
```


| Property | Default | Description |
|---|---|---|
| isEnabled | true | Enables or disables sampling. |
| maxTelemetryItemsPerSecond | 5 | The threshold at which sampling begins. |

## DocumentDB

Configuration settings for the [Azure Cosmos DB trigger and bindings](functions-bindings-cosmosdb).

```
{
"documentDB": {
"connectionMode": "Gateway",
"protocol": "Https",
"leaseOptions": {
"leasePrefix": "prefix1"
}
}
}
```


| Property | Default | Description |
|---|---|---|
| GatewayMode | Gateway | The connection mode used by the function when connecting to the Azure Cosmos DB service. Options are `Direct` and `Gateway` |
| Protocol | Https | The connection protocol used by the function when connection to the Azure Cosmos DB service. Read
|

## durableTask

Configuration settings for [Durable Functions](durable/durable-functions-overview).

Note

All major versions of Durable Functions are supported on all versions of the Azure Functions runtime. However, the schema of the *host.json* configuration differs slightly depending on the version of the Azure Functions runtime and the version of the Durable Functions extension that you use.

The following code provides two examples of `durableTask`

settings in *host.json*: one for Durable Functions 2.x and one for Durable Functions 1.x. You can use both examples with Azure Functions 2.0 and 3.0. With Azure Functions 1.0, the available settings are the same, but the `durableTask`

section of *host.json* is located in the root of the *host.json* configuration instead of being a field under `extensions`

.

```
{
"extensions": {
"durableTask": {
"hubName": "MyTaskHub",
"defaultVersion": "1.0",
"versionMatchStrategy": "CurrentOrOlder",
"versionFailureStrategy": "Reject",
"storageProvider": {
"connectionStringName": "AzureWebJobsStorage",
"controlQueueBatchSize": 32,
"controlQueueBufferThreshold": 256,
"controlQueueVisibilityTimeout": "00:05:00",
"FetchLargeMessagesAutomatically": true,
"maxQueuePollingInterval": "00:00:30",
"partitionCount": 4,
"trackingStoreConnectionStringName": "TrackingStorage",
"trackingStoreNamePrefix": "DurableTask",
"useLegacyPartitionManagement": false,
"useTablePartitionManagement": true,
"workItemQueueVisibilityTimeout": "00:05:00",
"QueueClientMessageEncoding": "UTF8"
},
"tracing": {
"traceInputsAndOutputs": false,
"traceReplayEvents": false,
},
"httpSettings":{
"defaultAsyncRequestSleepTimeMilliseconds": 30000,
"useForwardedHost": false,
},
"notifications": {
"eventGrid": {
"topicEndpoint": "https://topic_name.westus2-1.eventgrid.azure.net/api/events",
"keySettingName": "EventGridKey",
"publishRetryCount": 3,
"publishRetryInterval": "00:00:30",
"publishEventTypes": [
"Started",
"Completed",
"Failed",
"Terminated"
]
}
},
"maxConcurrentActivityFunctions": 10,
"maxConcurrentOrchestratorFunctions": 10,
"maxConcurrentEntityFunctions": 10,
"extendedSessionsEnabled": false,
"extendedSessionIdleTimeoutInSeconds": 30,
"useAppLease": true,
"useGracefulShutdown": false,
"maxEntityOperationBatchSize": 50,
"maxOrchestrationActions": 100000,
"storeInputsInOrchestrationHistory": false
}
}
}
```


| Property | Default value | Description |
|---|---|---|
| hubName | TestHubName (DurableFunctionsHub in v1.x) | The name of the hub that stores the current state of a function app. Task hub names must start with a letter and consist of only letters and numbers. If you don't specify a name, the default value is used. Alternate task hub names can be used to isolate multiple Durable Functions applications from each other, even if they use the same storage back end. For more information, see
|

[orchestration versioning](durable/durable-functions-orchestration-versioning)feature to enable scenarios like zero-downtime deployments with breaking changes. You can use any string value for the version.`None`

, `Strict`

, and `CurrentOrOlder`

. For detailed explanations, see [Orchestration versioning](durable/durable-functions-orchestration-versioning).`defaultVersion`

value. Valid values are `Reject`

and `Fail`

. For detailed explanations, see [Orchestration versioning](durable/durable-functions-orchestration-versioning).**Consumption plan for Python**: 32**Consumption plan for other languages**: 128**Dedicated or Premium plan**: 256*hh:mm:ss*format.*hh:mm:ss*format.`true`

, large messages that exceed the queue size limit are retrieved. When this setting is `false`

, a blob URL that points to each large message is retrieved.**Consumption plan**: 10**Dedicated or Premium plan**: 10 times the number of processors on the current machine**Consumption plan**: 5**Dedicated or Premium plan**: 10 times the number of processors on the current machine**Consumption plan**: 5**Dedicated or Premium plan**: 10 times the number of processors on the current machine[durable task scheduler](durable/durable-task-scheduler/durable-task-scheduler). Otherwise, the maximum number of concurrent entity executions is limited to the`maxConcurrentOrchestratorFunctions`

value.*hh:mm:ss*format. Higher values can result in higher message processing latencies. Lower values can result in higher storage costs because of increased storage transactions.connectionStringName (v2.x)

azureStorageConnectionStringName (v1.x)

trackingStoreConnectionStringName

`connectionStringName`

value (v2.x) or `azureStorageConnectionStringName`

value (v1.x) connection is used.`trackingStoreConnectionStringName`

is specified. If you don't specify a prefix, the default value of `DurableTask`

is used. If `trackingStoreConnectionStringName`

isn't specified, the History and Instances tables use the `hubName`

value as their prefix, and the `trackingStoreNamePrefix`

setting is ignored.`true`

, the entire contents of function inputs and outputs are logged.`EventGridTopicEndpoint`

URL.*hh:mm:ss*format.`Started`

, `Completed`

, `Failed`

, and `Terminated`

.`extendedSessionsEnabled`

setting is `true`

.[Disaster recovery and geo-distribution in Durable Functions](durable/durable-functions-disaster-recovery-geo-distribution). This setting is available starting in v2.3.0.`false`

, an algorithm is used that reduces the possibility of duplicate function execution when scaling out. This setting is available starting in v2.3.0. **Setting this value to**.`true`

isn't recommendedIn v2.x: false

`true`

, an algorithm is used that's designed to reduce costs for Azure Storage v2 accounts. This setting is available starting in WebJobs.Extensions.DurableTask v2.10.0. Using this setting with a managed identity requires WebJobs.Extensions.DurableTask v3.x or later, or Worker.Extensions.DurableTask v1.2.x or later.**Consumption plan**: 50**Dedicated or Premium plan**: 5,000[batch](durable/durable-functions-perf-and-scale#entity-operation-batching). If this value is 1, batching is disabled, and a separate function invocation processes each operation message. This setting is available starting in v2.6.1.`true`

, the Durable Task Framework saves activity inputs in the History table, and activity function inputs appear in orchestration history query results.`DurableTaskClient`

uses the gRPC client to manage orchestration instances. This setting applies to Durable Functions .NET isolated worker and Java apps.*hh:mm:ss*format for the HTTP client used by the gRPC client in Durable Functions. The client is currently supported for .NET isolated worker apps (.NET 6 and later versions) and for Java apps.Many of these settings are for optimizing performance. For more information, see [Performance and scale](durable/durable-functions-perf-and-scale).

## eventHub

Configuration settings for [Event Hub triggers and bindings](functions-bindings-event-hubs?tabs=functionsv1#hostjson-settings).

## functions

A list of functions that the job host runs. An empty array means run all functions. Intended for use only when [running locally](functions-run-local). In function apps in Azure, you should instead follow the steps in [How to disable functions in Azure Functions](disable-function) to disable specific functions rather than using this setting.

```
{
"functions": [ "QueueProcessor", "GitHubWebHook" ]
}
```


## functionTimeout

Indicates the timeout duration for all functions. In a serverless Consumption plan, the valid range is from 1 second to 10 minutes, and the default value is 5 minutes. In an App Service plan, there is no overall limit and the default is *null*, which indicates no timeout.

```
{
"functionTimeout": "00:05:00"
}
```


## healthMonitor

Configuration settings for [Host health monitor](https://github.com/Azure/azure-webjobs-sdk-script/wiki/Host-Health-Monitor).

```
{
"healthMonitor": {
"enabled": true,
"healthCheckInterval": "00:00:10",
"healthCheckWindow": "00:02:00",
"healthCheckThreshold": 6,
"counterThreshold": 0.80
}
}
```


| Property | Default | Description |
|---|---|---|
| enabled | true | Specifies whether the feature is enabled. |
| healthCheckInterval | 10 seconds | The time interval between the periodic background health checks. |
| healthCheckWindow | 2 minutes | A sliding time window used with the `healthCheckThreshold` setting. |
| healthCheckThreshold | 6 | Maximum number of times the health check can fail before a host recycle is initiated. |
| counterThreshold | 0.80 | The threshold at which a performance counter will be considered unhealthy. |

## http

Configuration settings for [http triggers and bindings](functions-bindings-http-webhook).

```
{
"http": {
"routePrefix": "api",
"maxOutstandingRequests": 200,
"maxConcurrentRequests": 100,
"dynamicThrottlesEnabled": true
}
}
```


| Property | Default | Description |
|---|---|---|
| dynamicThrottlesEnabled | false | When enabled, this setting causes the request processing pipeline to periodically check system performance counters like connections/threads/processes/memory/cpu/etc. and if any of those counters are over a built-in high threshold (80%), requests are rejected with a 429 "Too Busy" response until the counter(s) return to normal levels. |
| maxConcurrentRequests | unbounded (`-1` ) |
The maximum number of HTTP functions that will be executed in parallel. This allows you to control concurrency, which can help manage resource utilization. For example, you might have an HTTP function that uses a lot of system resources (memory/cpu/sockets) such that it causes issues when concurrency is too high. Or you might have a function that makes outbound requests to a third party service, and those calls need to be rate limited. In these cases, applying a throttle here can help. |
| maxOutstandingRequests | unbounded (`-1` ) |
The maximum number of outstanding requests that are held at any given time. This limit includes requests that are queued but have not started executing, and any in progress executions. Any incoming requests over this limit are rejected with a 429 "Too Busy" response. That allows callers to employ time-based retry strategies, and also helps you to control maximum request latencies. This only controls queuing that occurs within the script host execution path. Other queues such as the ASP.NET request queue will still be in effect and unaffected by this setting. |
| routePrefix | api | The route prefix that applies to all routes. Use an empty string to remove the default prefix. |

## id

The unique ID for a job host. Can be a lower case GUID with dashes removed. Required when running locally. When running in Azure, we recommend that you not set an ID value. An ID is generated automatically in Azure when `id`

is omitted.

If you share a Storage account across multiple function apps, make sure that each function app has a different `id`

. You can omit the `id`

property or manually set each function app's `id`

to a different value. The timer trigger uses a storage lock to ensure that there will be only one timer instance when a function app scales out to multiple instances. If two function apps share the same `id`

and each uses a timer trigger, only one timer runs.

```
{
"id": "9f4ea53c5136457d883d685e57164f08"
}
```


## logger

Controls filtering for logs written by an [ILogger](functions-dotnet-class-library#ilogger) object or by [context.log](functions-reference-node#contextlog-method).

```
{
"logger": {
"categoryFilter": {
"defaultLevel": "Information",
"categoryLevels": {
"Host": "Error",
"Function": "Error",
"Host.Aggregator": "Information"
}
}
}
}
```


| Property | Default | Description |
|---|---|---|
| categoryFilter | n/a | Specifies filtering by category |
| defaultLevel | Information | For any categories not specified in the `categoryLevels` array, send logs at this level and above to Application Insights. |
| categoryLevels | n/a | An array of categories that specifies the minimum log level to send to Application Insights for each category. The category specified here controls all categories that begin with the same value, and longer values take precedence. In the preceding sample host.json file, all categories that begin with "Host.Aggregator" log at `Information` level. All other categories that begin with "Host", such as "Host.Executor", log at `Error` level. |

## queues

Configuration settings for [Storage queue triggers and bindings](functions-bindings-storage-queue).

```
{
"queues": {
"maxPollingInterval": 2000,
"visibilityTimeout" : "00:00:30",
"batchSize": 16,
"maxDequeueCount": 5,
"newBatchThreshold": 8
}
}
```


| Property | Default | Description |
|---|---|---|
| maxPollingInterval | 60000 | The maximum interval in milliseconds between queue polls. |
| visibilityTimeout | 0 | The time interval between retries when processing of a message fails. |
| batchSize | 16 | The number of queue messages that the Functions runtime retrieves simultaneously and processes in parallel. When the number being processed gets down to the `newBatchThreshold` , the runtime gets another batch and starts processing those messages. So the maximum number of concurrent messages being processed per function is `batchSize` plus `newBatchThreshold` . This limit applies separately to each queue-triggered function. If you want to avoid parallel execution for messages received on one queue, you can set `batchSize` to 1. However, this setting eliminates concurrency only so long as your function app runs on a single virtual machine (VM). If the function app scales out to multiple VMs, each VM could run one instance of each queue-triggered function.The maximum `batchSize` is 32. |
| maxDequeueCount | 5 | The number of times to try processing a message before moving it to the poison queue. |
| newBatchThreshold | batchSize/2 | Whenever the number of messages being processed concurrently gets down to this number, the runtime retrieves another batch. |

## SendGrid

Configuration setting for the [SendGrind output binding](functions-bindings-sendgrid)

```
{
"sendGrid": {
"from": "Contoso Group <admin@contoso.com>"
}
}
```


| Property | Default | Description |
|---|---|---|
| from | n/a | The sender's email address across all functions. |

## serviceBus

Configuration setting for [Service Bus triggers and bindings](functions-bindings-service-bus).

```
{
"serviceBus": {
"maxConcurrentCalls": 16,
"prefetchCount": 100,
"autoRenewTimeout": "00:05:00",
"autoComplete": true
}
}
```


| Property | Default | Description |
|---|---|---|
| maxConcurrentCalls | 16 | The maximum number of concurrent calls to the callback that the message pump should initiate. By default, the Functions runtime processes multiple messages concurrently. To direct the runtime to process only a single queue or topic message at a time, set `maxConcurrentCalls` to 1. |
| prefetchCount | n/a | The default PrefetchCount that will be used by the underlying ServiceBusReceiver. |
| autoRenewTimeout | 00:05:00 | The maximum duration within which the message lock will be renewed automatically. |
| autoComplete | true | When true, the trigger completes the message processing automatically on successful execution of the operation. When false, it is the responsibility of the function to complete the message before returning. |

## singleton

Configuration settings for Singleton lock behavior. For more information, see [GitHub issue about singleton support](https://github.com/Azure/azure-webjobs-sdk-script/issues/912).

```
{
"singleton": {
"lockPeriod": "00:00:15",
"listenerLockPeriod": "00:01:00",
"listenerLockRecoveryPollingInterval": "00:01:00",
"lockAcquisitionTimeout": "00:01:00",
"lockAcquisitionPollingInterval": "00:00:03"
}
}
```


| Property | Default | Description |
|---|---|---|
| lockPeriod | 00:00:15 | The period that function level locks are taken for. The locks auto-renew. |
| listenerLockPeriod | 00:01:00 | The period that listener locks are taken for. |
| listenerLockRecoveryPollingInterval | 00:01:00 | The time interval used for listener lock recovery if a listener lock couldn't be acquired on startup. |
| lockAcquisitionTimeout | 00:01:00 | The maximum amount of time the runtime tries to acquire a lock. |
| lockAcquisitionPollingInterval | n/a | The interval between lock acquisition attempts. |

## tracing

*Version 1.x*

Configuration settings for logs that you create by using a `TraceWriter`

object. To learn more, see [C# Logging].

```
{
"tracing": {
"consoleLevel": "verbose",
"fileLoggingMode": "debugOnly"
}
}
```


| Property | Default | Description |
|---|---|---|
| consoleLevel | info | The tracing level for console logging. Options are: `off` , `error` , `warning` , `info` , and `verbose` . |
| fileLoggingMode | debugOnly | The tracing level for file logging. Options are `never` , `always` , `debugOnly` . |

## watchDirectories

A set of [shared code directories](functions-reference-csharp#watched-directories) that should be monitored for changes. Ensures that when code in these directories is changed, the changes are picked up by your functions.

```
{
"watchDirectories": [ "Shared" ]
}
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-grid-output -->

# Azure Event Grid output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the Event Grid output binding to write events to a custom topic. You must have a valid [access key for the custom topic](../event-grid/security-authenticate-publishing-clients). The Event Grid output binding doesn't support shared access signature (SAS) tokens.

For information on setup and configuration details, see [How to work with Event Grid triggers and bindings in Azure Functions](event-grid-how-tos).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

Important

The Event Grid output binding is only available for Functions 2.x and higher.

## Example

The type of the output parameter used with an Event Grid output binding depends on the Functions runtime version, the binding extension version, and the modality of the C# function. The C# function can be created using one of the following C# modes:

[In-process class library](functions-dotnet-class-library): compiled C# function that runs in the same process as the Functions runtime.[Isolated worker process class library](dotnet-isolated-process-guide): compiled C# function that runs in a worker process isolated from the runtime.

The following example shows how the custom type is used in both the trigger and an Event Grid output binding:

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.Logging;
namespace SampleApp
{
public static class EventGridFunction
{
[Function(nameof(EventGridFunction))]
[EventGridOutput(TopicEndpointUri = "MyEventGridTopicUriSetting", TopicKeySetting = "MyEventGridTopicKeySetting")]
public static MyEventType Run([EventGridTrigger] MyEventType input, FunctionContext context)
{
var logger = context.GetLogger(nameof(EventGridFunction));
logger.LogInformation(input.Data?.ToString());
var outputEvent = new MyEventType()
{
Id = "unique-id",
Subject = "abc-subject",
Data = new Dictionary<string, object>
{
{ "myKey", "myValue" }
}
};
return outputEvent;
}
}
public class MyEventType
{
public string? Id { get; set; }
public string? Topic { get; set; }
public string? Subject { get; set; }
public string? EventType { get; set; }
public DateTime EventTime { get; set; }
public IDictionary<string, object>? Data { get; set; }
}
}
```


The following example shows a Java function that writes a message to an Event Grid custom topic. The function uses the binding's `setValue`

method to output a string.

```
public class Function {
@FunctionName("EventGridTriggerTest")
public void run(@EventGridTrigger(name = "event") String content,
@EventGridOutput(name = "outputEvent", topicEndpointUri = "MyEventGridTopicUriSetting", topicKeySetting = "MyEventGridTopicKeySetting") OutputBinding<String> outputEvent,
final ExecutionContext context) {
context.getLogger().info("Java EventGrid trigger processed a request." + content);
final String eventGridOutputDocument = "{\"id\": \"1807\", \"eventType\": \"recordInserted\", \"subject\": \"myapp/cars/java\", \"eventTime\":\"2017-08-10T21:03:07+00:00\", \"data\": {\"make\": \"Ducati\",\"model\": \"Monster\"}, \"dataVersion\": \"1.0\"}";
outputEvent.setValue(eventGridOutputDocument);
}
}
```


You can also use a POJO class to send Event Grid messages.

```
public class Function {
@FunctionName("EventGridTriggerTest")
public void run(@EventGridTrigger(name = "event") String content,
@EventGridOutput(name = "outputEvent", topicEndpointUri = "MyEventGridTopicUriSetting", topicKeySetting = "MyEventGridTopicKeySetting") OutputBinding<EventGridEvent> outputEvent,
final ExecutionContext context) {
context.getLogger().info("Java EventGrid trigger processed a request." + content);
final EventGridEvent eventGridOutputDocument = new EventGridEvent();
eventGridOutputDocument.setId("1807");
eventGridOutputDocument.setEventType("recordInserted");
eventGridOutputDocument.setEventTime("2017-08-10T21:03:07+00:00");
eventGridOutputDocument.setDataVersion("1.0");
eventGridOutputDocument.setSubject("myapp/cars/java");
eventGridOutputDocument.setData("{\"make\": \"Ducati\",\"model\":\"monster\"");
outputEvent.setValue(eventGridOutputDocument);
}
}
class EventGridEvent {
private String id;
private String eventType;
private String subject;
private String eventTime;
private String dataVersion;
private String data;
public String getId() {
return id;
}
public String getData() {
return data;
}
public void setData(String data) {
this.data = data;
}
public String getDataVersion() {
return dataVersion;
}
public void setDataVersion(String dataVersion) {
this.dataVersion = dataVersion;
}
public String getEventTime() {
return eventTime;
}
public void setEventTime(String eventTime) {
this.eventTime = eventTime;
}
public String getSubject() {
return subject;
}
public void setSubject(String subject) {
this.subject = subject;
}
public String getEventType() {
return eventType;
}
public void setEventType(String eventType) {
this.eventType = eventType;
}
public void setId(String id) {
this.id = id;
}
}
```


The following example shows a timer triggered [TypeScript function](functions-reference-node?tabs=typescript) that outputs a single event:

```
import { app, EventGridPartialEvent, InvocationContext, output, Timer } from '@azure/functions';
export async function timerTrigger1(myTimer: Timer, context: InvocationContext): Promise<EventGridPartialEvent> {
const timeStamp = new Date().toISOString();
return {
id: 'message-id',
subject: 'subject-name',
dataVersion: '1.0',
eventType: 'event-type',
data: {
name: 'John Henry',
},
eventTime: timeStamp,
};
}
app.timer('timerTrigger1', {
schedule: '0 */5 * * * *',
return: output.eventGrid({
topicEndpointUri: 'MyEventGridTopicUriSetting',
topicKeySetting: 'MyEventGridTopicKeySetting',
}),
handler: timerTrigger1,
});
```


To output multiple events, return an array instead of a single object. For example:

```
const timeStamp = new Date().toISOString();
return [
{
id: 'message-id',
subject: 'subject-name',
dataVersion: '1.0',
eventType: 'event-type',
data: {
name: 'John Henry',
},
eventTime: timeStamp,
},
{
id: 'message-id-2',
subject: 'subject-name',
dataVersion: '1.0',
eventType: 'event-type',
data: {
name: 'John Doe',
},
eventTime: timeStamp,
},
];
```


The following example shows a timer triggered [JavaScript function](functions-reference-node) that outputs a single event:

```
const { app, output } = require('@azure/functions');
const eventGridOutput = output.eventGrid({
topicEndpointUri: 'MyEventGridTopicUriSetting',
topicKeySetting: 'MyEventGridTopicKeySetting',
});
app.timer('timerTrigger1', {
schedule: '0 */5 * * * *',
return: eventGridOutput,
handler: (myTimer, context) => {
const timeStamp = new Date().toISOString();
return {
id: 'message-id',
subject: 'subject-name',
dataVersion: '1.0',
eventType: 'event-type',
data: {
name: 'John Henry',
},
eventTime: timeStamp,
};
},
});
```


To output multiple events, return an array instead of a single object. For example:

```
const timeStamp = new Date().toISOString();
return [
{
id: 'message-id',
subject: 'subject-name',
dataVersion: '1.0',
eventType: 'event-type',
data: {
name: 'John Henry',
},
eventTime: timeStamp,
},
{
id: 'message-id-2',
subject: 'subject-name',
dataVersion: '1.0',
eventType: 'event-type',
data: {
name: 'John Doe',
},
eventTime: timeStamp,
},
];
```


The following example demonstrates how to configure a function to output an Event Grid event message. The section where `type`

is set to `eventGrid`

configures the values needed to establish an Event Grid output binding.

```
{
"bindings": [
{
"type": "eventGrid",
"name": "outputEvent",
"topicEndpointUri": "MyEventGridTopicUriSetting",
"topicKeySetting": "MyEventGridTopicKeySetting",
"direction": "out"
},
{
"authLevel": "anonymous",
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
}
]
}
```


In your function, use the `Push-OutputBinding`

to send an event to a custom topic through the Event Grid output binding.

```
using namespace System.Net
# Input bindings are passed in via param block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell HTTP trigger function processed a request."
# Interact with query parameters or the body of the request.
$message = $Request.Query.Message
Push-OutputBinding -Name outputEvent -Value @{
id = "1"
eventType = "testEvent"
subject = "testapp/testPublish"
eventTime = "2020-08-27T21:03:07+00:00"
data = @{
Message = $message
}
dataVersion = "1.0"
}
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = 200
Body = "OK"
})
```


The following example shows a trigger binding and a Python function that uses the binding. It then sends in an event to the custom topic, as specified by the `topicEndpointUri`

. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

Here's the function in the function_app.py file:

```
import logging
import azure.functions as func
import datetime
app = func.FunctionApp()
@app.function_name(name="eventgrid_output")
@app.event_grid_trigger(arg_name="eventGridEvent")
@app.event_grid_output(
arg_name="outputEvent",
topic_endpoint_uri="MyEventGridTopicUriSetting",
topic_key_setting="MyEventGridTopicKeySetting")
def eventgrid_output(eventGridEvent: func.EventGridEvent,
outputEvent: func.Out[func.EventGridOutputEvent]) -> None:
logging.log("eventGridEvent: ", eventGridEvent)
outputEvent.set(
func.EventGridOutputEvent(
id="test-id",
data={"tag1": "value1", "tag2": "value2"},
subject="test-subject",
event_type="test-event-1",
event_time=datetime.datetime.utcnow(),
data_version="1.0"))
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attribute to configure the binding. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#event-grid-output).

The attribute's constructor takes the name of an application setting that contains the name of the custom topic, and the name of an application setting that contains the topic key.

The following table explains the parameters for the `EventGridOutputAttribute`

.

| Parameter | Description |
|---|---|
TopicEndpointUri |
The name of an app setting that contains the URI for the custom topic, such as `MyTopicEndpointUri` . |
TopicKeySetting |
The name of an app setting that contains an access key for the custom topic. |
connection* |
The value of the common prefix for the setting that contains the topic endpoint URI. For more information about the naming format of this application setting, see
|

## Annotations

For Java classes, use the [EventGridAttribute](https://github.com/Azure/azure-functions-java-library/blob/dev/src/main/java/com/microsoft/azure/functions/annotation/EventGridOutput.java) attribute.

The attribute's constructor takes the name of an app setting that contains the name of the custom topic, and the name of an app setting that contains the topic key. For more information about these settings, see [Output - configuration](#configuration). Here's an `EventGridOutput`

attribute example:

```
public class Function {
@FunctionName("EventGridTriggerTest")
public void run(@EventGridTrigger(name = "event") String content,
@EventGridOutput(name = "outputEvent", topicEndpointUri = "MyEventGridTopicUriSetting", topicKeySetting = "MyEventGridTopicKeySetting") OutputBinding<String> outputEvent, final ExecutionContext context) {
...
}
}
```


## Configuration

The following table explains the properties that you can set on the `options`

object passed to the `output.eventGrid()`

method.

| Property | Description |
|---|---|
topicEndpointUri |
The name of an app setting that contains the URI for the custom topic, such as `MyTopicEndpointUri` . |
topicKeySetting |
The name of an app setting that contains an access key for the custom topic. |
connection* |
The value of the common prefix for the setting that contains the topic endpoint URI. When setting the `connection` property, the `topicEndpointUri` and `topicKeySetting` properties shouldn't be set. For more information about the naming format of this application setting, see
|

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `eventGrid` . |
direction |
Must be set to `out` . This parameter is set automatically when you create the binding in the Azure portal. |
name |
The variable name used in function code that represents the event. |
topicEndpointUri |
The name of an app setting that contains the URI for the custom topic, such as `MyTopicEndpointUri` . |
topicKeySetting |
The name of an app setting that contains an access key for the custom topic. |
connection* |
The value of the common prefix for the setting that contains the topic endpoint URI. For more information about the naming format of this application setting, see
|

*Support for identity-based connections requires version 3.3.x or higher of the extension.

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

Important

Make sure that you set the value of `TopicEndpointUri`

to the name of an app setting that contains the URI of the custom topic. Don't specify the URI of the custom topic directly in this property. The same applies when using `Connection`

.

See the [Example section](#example) for complete examples.

## Usage

The parameter type supported by the Event Grid output binding depends on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to write a single event, the Event Grid output binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The event as a string. |
`byte[]` |
The bytes of the event message. |
| JSON serializable types | An object representing a JSON event. Functions tries to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write multiple events, the Event Grid output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single event types |
An array containing multiple events. Each entry represents one event. |

For other output scenarios, create and use an [EventGridPublisherClient](/en-us/dotnet/api/azure.messaging.eventgrid.eventgridpublisherclient) with other types from [Azure.Messaging.EventGrid](/en-us/dotnet/api/azure.messaging.eventgrid) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

Send individual messages by calling a method parameter such as `out EventGridOutput paramName`

, and write multiple messages with `ICollector<EventGridOutput>`

.

Access the output event by using the `Push-OutputBinding`

cmdlet to send an event to the Event Grid output binding.

There are two options for outputting an Event Grid message from a function:

**Return value**: Set the`name`

property in*function.json*to`$return`

. With this configuration, the function's return value is persisted as an Event Grid message.**Imperative**: Pass a value to the[set](/en-us/python/api/azure-functions/azure.functions.out#set-val--t-----none)method of the parameter declared as an[Out](/en-us/python/api/azure-functions/azure.functions.out)type. The value passed to`set`

is persisted as an Event Grid message.

The output function parameter must be defined as `func.Out[str]`

, `func.Out[bytes]`

, `func.Out[func.EventGridOutputEvent]`

, or `func.Out[List[func.EventGridOutputEvent]]`

. Refer to the [output example](#example) for details.

## Connections

There are two ways of authenticating to an Event Grid topic when using the Event Grid output binding:

| Authentication method | Description |
|---|---|
| Using a topic key | Set the `TopicEndpointUri` and `TopicKeySetting` properties, as described in
|
| Using an identity | Set the `Connection` property to the name of a shared prefix for multiple application settings, together defining
|

### Use a topic key

Use the following steps to configure a topic key:

Follow the steps in

[Get access keys](../event-grid/get-access-keys)to obtain the topic key for your Event Grid topic.In your application settings, create a setting that defines the topic key value. Use the name of this setting for the

`TopicKeySetting`

property of the binding.In your application settings, create a setting that defines the topic endpoint. Use the name of this setting for the

`TopicEndpointUri`

property of the binding.

### Identity-based authentication

When using version 3.3.x or higher of the extension, you can connect to an Event Grid topic using an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis) to avoid having to obtain and work with topic keys.

You need to create an application setting that returns the topic endpoint URI. The name of the setting should combine a *unique common prefix* (for example, `myawesometopic`

) with the value `__topicEndpointUri`

. Then, you must use that common prefix (in this case, `myawesometopic`

) when you define the `Connection`

property in the binding.

In this mode, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Topic Endpoint URI | `<CONNECTION_NAME_PREFIX>__topicEndpointUri` |
The topic endpoint. | `https://<topic-name>.centralus-1.eventgrid.azure.net/api/events` |

More properties can be used to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

Note

When using [Azure App Configuration](../azure-app-configuration/quickstart-azure-functions-csharp) or [Key Vault](/en-us/azure/key-vault/general/overview) to provide settings for managed identity-based connections, setting names should use a valid key separator such as `:`

or `/`

in place of the `__`

to ensure names are resolved correctly.

For example, `<CONNECTION_NAME_PREFIX>:topicEndpointUri`

.

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

You must create a role assignment that provides access to your Event Grid topic at runtime. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) are not sufficient. The following table shows built-in roles that are recommended when using the Event Hubs extension in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles |
|---|---|
| Output binding |
|

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/scenario-scheduled-tasks -->

# Quickstart: Run scheduled tasks using Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you use the Azure Developer CLI (`azd`

) to create a Timer trigger function to run a scheduled task in Azure Functions. After verifying the code locally, you deploy it to a new serverless function app you create running in a Flex Consumption plan in Azure Functions.

The project source uses `azd`

to create the function app and related resources and to deploy your code to Azure. This deployment follows current best practices for secure and scalable Azure Functions deployments.

By default, the Flex Consumption plan follows a *pay-for-what-you-use* billing model, which means you can complete this article and only incur a small cost of a few USD cents or less in your Azure account.

Important

While [running scheduled tasks](functions-bindings-timer) is supported for all languages, this quickstart scenario currently only has examples for C#, Python, and TypeScript. To complete this quickstart, select one of these supported languages at the top of the article.

## Prerequisites

[Node.js 22](https://nodejs.org/)or above

[Python 3.11](https://www.python.org/)or above

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Initialize the project

Use the `azd init`

command to create a local Azure Functions code project from a template.

In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-dotnet-azd-timer -e scheduled-dotnet`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-timer)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name is also used in the name of the resource group you create in Azure.Run this command to navigate to the app folder:

`cd src`

Create a file named

*local.settings.json*in the`src`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "dotnet-isolated", "TIMER_SCHEDULE": "*/30 * * * * *" } }`

This file is required when running locally.


In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-typescript-azd-timer -e scheduled-ts`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-timer)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name is also used in the name of the resource group you create in Azure.Create a file named

*local.settings.json*in the`src`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "node", "TIMER_SCHEDULE": "*/30 * * * * *" } }`

This file is required when running locally.


In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-python-azd-timer -e scheduled-py`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-python-azd-timer)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name is also used in the name of the resource group you create in Azure.Create a file named

*local.settings.json*in the`src`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "python", "TIMER_SCHEDULE": "*/30 * * * * *" } }`

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


Run this command from your app folder in a terminal or command prompt:

`npm install npm start`


When the Functions host starts in your local project folder, it writes information about your Timer triggered function to the terminal output. You should see your Timer triggered function execute based on the schedule defined in your code.

The default schedule is

`*/30 * * * * *`

, which runs every 30 seconds.When you're done, press Ctrl+C in the terminal window to stop the

`func.exe`

host process.

- Run
`deactivate`

to shut down the virtual environment.

## Review the code (optional)

You can review the code that defines the Timer trigger function:

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.Timer;
using Microsoft.Extensions.Logging;
namespace Company.Function
{
public class timerFunction
{
private readonly ILogger _logger;
public timerFunction(ILoggerFactory loggerFactory)
{
_logger = loggerFactory.CreateLogger<timerFunction>();
}
[Function("timerFunction")]
public void Run(
[TimerTrigger("%TIMER_SCHEDULE%", RunOnStartup = true)] TimerInfo myTimer,
FunctionContext context
)
{
_logger.LogInformation($"C# Timer trigger function executed at: {DateTime.Now}");
if (myTimer.IsPastDue)
{
_logger.LogWarning("The timer is running late!");
}
}
}
}
```


You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-timer).

```
import { app, InvocationContext, Timer } from '@azure/functions';
export async function timerFunction(myTimer: Timer, context: InvocationContext): Promise<void> {
context.log(`TypeScript Timer trigger function executed at: ${new Date().toISOString()}`);
if (myTimer.isPastDue) {
context.warn("The timer is running late!");
}
}
app.timer('timerFunction', {
schedule: '%TIMER_SCHEDULE%',
runOnStartup: true,
handler: timerFunction
});
```


You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-timer).

```
import datetime
import logging
import azure.functions as func
# Create the function app instance
app = func.FunctionApp()
@app.timer_trigger(schedule="%TIMER_SCHEDULE%",
arg_name="mytimer",
run_on_startup=True,
use_monitor=False)
def timer_function(mytimer: func.TimerRequest) -> None:
utc_timestamp = datetime.datetime.now(datetime.timezone.utc).isoformat()
logging.info(f'Python timer trigger function executed at: {utc_timestamp}')
if mytimer.past_due:
logging.warning('The timer is running late!')
```


You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-python-azd-timer).

After you verify your function locally, it's time to publish it to Azure.

## Deploy to Azure

This project is configured to use the `azd up`

command to deploy your code to a new function app in a Flex Consumption plan in Azure.

Tip

This project includes a set of Bicep files that `azd`

uses to create a secure deployment to a Flex consumption plan that follows best practices.

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

):- Flex Consumption plan and function app
- Azure Storage (required) and Application Insights (recommended)
- Access policies and roles for your account
- Service-to-service connections using managed identities (instead of stored connection strings)
- Virtual network to securely run both the function app and the other Azure resources

Package and deploy your code to the deployment container (equivalent to

`azd deploy`

). The app is then started and runs in the deployed package.

After the command completes successfully, you see links to the resources you created.


## Verify deployment

After deployment completes, your Timer trigger function automatically starts running in Azure based on its schedule.

In the

[Azure portal](https://portal.azure.com), go to your new function app.Select

**Log stream**from the left menu to monitor your function executions in real-time.You should see log entries that show your Timer trigger function executing according to its schedule.


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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-node-upgrade-v4 -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/monitor-functions-reference -->

# Azure Functions monitoring data reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article contains all the monitoring reference information for this service.

See [Monitor Azure Functions](monitor-functions) for details on the data you can collect for Azure Functions and how to use it.

See [Monitor executions in Azure Functions](functions-monitoring) for details on using Application Insights to collect and analyze log data from individual functions in your function app.

## Metrics

This section lists all the automatically collected platform metrics for this service. These metrics are also part of the global list of [all platform metrics supported in Azure Monitor](/en-us/azure/azure-monitor/reference/supported-metrics/metrics-index#supported-metrics-per-resource-type).

For information on metric retention, see [Azure Monitor Metrics overview](/en-us/azure/azure-monitor/essentials/data-platform-metrics#retention-of-metrics).

Hosting plans that allow your apps to scale dynamically support extra Functions-specific metrics:

These metrics are used to estimate the costs associated with *on demand* and *always ready* meters used for billing in a [Flex Consumption plan](flex-consumption-plan):

| Metric | Description | Meter calculation |
|---|---|---|
On Demand Function Execution Count |
Total number of function executions in on demand instances. | `OnDemandFunctionExecutionCount` relates to the On Demand Total Executions meter. |
Always Ready Function Execution Count |
Total number of function executions in always ready instances. | `AlwaysReadyFunctionExecutionCount` relates to the Always Ready Total Executions meter. |
On Demand Function Execution Units |
Total MB-milliseconds from on demand instances while actively executing functions. | `OnDemandFunctionExecutionUnits / 1,024,000` is the On Demand Execution Time meter, in GB-seconds. |
Always Ready Function Execution Units |
Total MB-milliseconds from always ready instances while actively executing functions. | `AlwaysReadyFunctionExecutionUnits / 1,024,000` is the Always Ready Execution Time meter, in GB-seconds. |
Always Ready Units |
The total MB-milliseconds of always ready instances assigned to the app, whether or not functions are actively executing. | `AlwaysReadyUnits / 1,024,000` is the Always Ready Baseline meter, in GB-seconds. |

In this table, all execution units are calculated by multiplying the fixed instance memory size, such as 512 MB or 2,048 MB, by total execution times, in milliseconds.

These metrics are used to monitor the performance and scaling behavior of your function app in a Flex Consumption plan:

| Metric | Description |
|---|---|
Automatic Scaling Instance Count |
The number of instances on which this app is running. Note that this is emitted every 30 seconds, and given Flex Consumption scales out and in fast, the number will be an aggregate of all new instances the app used in this time period. Make sure to change the aggregation to the minimum possible in the graph and the aggregation to "count". |
Memory working set |
The current amount of memory used by the app, in MB. Can be further filtered for each instance of the app. |
Average memory working set |
The average amount of memory used by the app, in megabytes (MB). Can be further filtered for each instance of the app. |
CPU Percentage |
The average percentage of CPU being used. Can be further filtered for each instance of the app. This is currently rolling out and might not be available for apps in all regions yet. |

These performance metrics help you understand resource utilization and scaling patterns in your Flex Consumption function app. The instance count metric is particularly useful for monitoring the dynamic scaling behavior, while memory and CPU metrics provide insights into resource consumption patterns.

### Supported metrics for Microsoft.Web/sites

The following table lists the metrics available for the Microsoft.Web/sites resource type. Most of these metrics apply to both function app and web apps, which both run on App Service.

Note

These metrics aren't available when your function app runs on Linux in a [Consumption plan](consumption-plan).

- All columns might not be present in every table.
- Some columns might be beyond the viewing area of the page. Select
**Expand table**to view all available columns.

**Table headings**

**Category**- The metrics group or classification.**Metric**- The metric display name as it appears in the Azure portal.**Name in REST API**- The metric name as referred to in the[REST API](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough).**Unit**- Unit of measure.**Aggregation**- The default[aggregation](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained)type. Valid values: Average (Avg), Minimum (Min), Maximum (Max), Total (Sum), Count.**Dimensions**-[Dimensions](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#dimensions-splitting-and-filtering)available for the metric.**Time Grains**-[Intervals](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#granularity)at which the metric is sampled. For example,`PT1M`

indicates that the metric is sampled every minute,`PT30M`

every 30 minutes,`PT1H`

every hour, and so on.**DS Export**- Whether the metric is exportable to Azure Monitor Logs via diagnostic settings. For information on exporting metrics, see[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings?tabs=portal).

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Always Ready Function Execution CountAlways Ready Function Execution Count. For Flex Consumption FunctionApps only. |
`AlwaysReadyFunctionExecutionCount` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Always Ready Function Execution UnitsAlways Ready Function Execution Units. For Flex Consumption FunctionApps only. |
`AlwaysReadyFunctionExecutionUnits` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Always Ready UnitsAlways Ready Units. For Flex Consumption FunctionApps only. |
`AlwaysReadyUnits` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
ConnectionsThe number of bound sockets existing in the sandbox (w3wp.exe and its child processes). A bound socket is created by calling bind()/connect() APIs and remains until said socket is closed with CloseHandle()/closesocket(). For WebApps and FunctionApps. |
`AppConnections` |
Count | Average, Count, Maximum, Minimum | `Instance` |
PT1M | Yes |
Average memory working setThe average amount of memory used by the app, in megabytes (MiB). For WebApps and FunctionApps. |
`AverageMemoryWorkingSet` |
Bytes | Average | `Instance` |
PT1M | Yes |
Average Response Time (deprecated)The average time taken for the app to serve requests, in seconds. For WebApps and FunctionApps. |
`AverageResponseTime` |
Seconds | Average | `Instance` |
PT1M | Yes |
Data InThe amount of incoming bandwidth consumed by the app, in MiB. For WebApps and FunctionApps. |
`BytesReceived` |
Bytes | Total (Sum) | `Instance` |
PT1M | Yes |
Data OutThe amount of outgoing bandwidth consumed by the app, in MiB. For WebApps and FunctionApps. |
`BytesSent` |
Bytes | Total (Sum) | `Instance` |
PT1M | Yes |
Percentage CPUThe average percentage of CPU being used. For Flex Consumption function apps only. |
`CpuPercentage` |
Percent | Average | `Instance` |
PT1M | Yes |
CPU TimeThe amount of CPU consumed by the app, in seconds. For more information about this metric. Please see
|
`CpuTime` |
Seconds | Count, Total (Sum), Minimum, Maximum | `Instance` |
PT1M | Yes |
Current AssembliesThe current number of Assemblies loaded across all AppDomains in this application. For WebApps and FunctionApps. |
`CurrentAssemblies` |
Count | Average | `Instance` |
PT1M | Yes |
File System UsagePercentage of filesystem quota consumed by the app. For WebApps and FunctionApps. |
`FileSystemUsage` |
Bytes | Average | <none> | PT6H, PT12H, P1D | Yes |
Function Execution CountFunction Execution Count. For FunctionApps only. |
`FunctionExecutionCount` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Function Execution UnitsFunction Execution Units. For FunctionApps only. |
`FunctionExecutionUnits` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Gen 0 Garbage CollectionsThe number of times the generation 0 objects are garbage collected since the start of the app process. Higher generation GCs include all lower generation GCs. For WebApps and FunctionApps. |
`Gen0Collections` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Gen 1 Garbage CollectionsThe number of times the generation 1 objects are garbage collected since the start of the app process. Higher generation GCs include all lower generation GCs. For WebApps and FunctionApps. |
`Gen1Collections` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Gen 2 Garbage CollectionsThe number of times the generation 2 objects are garbage collected since the start of the app process. For WebApps and FunctionApps. |
`Gen2Collections` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Handle CountThe total number of handles currently open by the app process. For WebApps and FunctionApps. |
`Handles` |
Count | Average | `Instance` |
PT1M | Yes |
Health check statusHealth check status. For WebApps and FunctionApps. |
`HealthCheckStatus` |
Count | Average | `Instance` |
PT5M, PT1H, P1D | Yes |
Http 101The count of requests resulting in an HTTP status code 101. For WebApps and FunctionApps. |
`Http101` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http 2xxThe count of requests resulting in an HTTP status code >= 200 but < 300. For WebApps and FunctionApps. |
`Http2xx` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http 3xxThe count of requests resulting in an HTTP status code >= 300 but < 400. For WebApps and FunctionApps. |
`Http3xx` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http 401The count of requests resulting in HTTP 401 status code. For WebApps and FunctionApps. |
`Http401` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http 403The count of requests resulting in HTTP 403 status code. For WebApps and FunctionApps. |
`Http403` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http 404The count of requests resulting in HTTP 404 status code. For WebApps and FunctionApps. |
`Http404` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http 406The count of requests resulting in HTTP 406 status code. For WebApps and FunctionApps. |
`Http406` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http 4xxThe count of requests resulting in an HTTP status code >= 400 but < 500. For WebApps and FunctionApps. |
`Http4xx` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http Server ErrorsThe count of requests resulting in an HTTP status code >= 500 but < 600. For WebApps and FunctionApps. |
`Http5xx` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Response TimeThe time taken for the app to serve requests, in seconds. For WebApps and FunctionApps. |
`HttpResponseTime` |
Seconds | Average | `Instance` |
PT1M | Yes |
Automatic Scaling Instance CountThe number of instances on which this app is running. |
`InstanceCount` |
Count | Average | <none> | PT1M | Yes |
IO Other Bytes Per SecondThe rate at which the app process is issuing bytes to I/O operations that don't involve data, such as control operations. For WebApps and FunctionApps. |
`IoOtherBytesPerSecond` |
BytesPerSecond | Total (Sum) | `Instance` |
PT1M | Yes |
IO Other Operations Per SecondThe rate at which the app process is issuing I/O operations that aren't read or write operations. For WebApps and FunctionApps. |
`IoOtherOperationsPerSecond` |
BytesPerSecond | Total (Sum) | `Instance` |
PT1M | Yes |
IO Read Bytes Per SecondThe rate at which the app process is reading bytes from I/O operations. For WebApps and FunctionApps. |
`IoReadBytesPerSecond` |
BytesPerSecond | Total (Sum) | `Instance` |
PT1M | Yes |
IO Read Operations Per SecondThe rate at which the app process is issuing read I/O operations. For WebApps and FunctionApps. |
`IoReadOperationsPerSecond` |
BytesPerSecond | Total (Sum) | `Instance` |
PT1M | Yes |
IO Write Bytes Per SecondThe rate at which the app process is writing bytes to I/O operations. For WebApps and FunctionApps. |
`IoWriteBytesPerSecond` |
BytesPerSecond | Total (Sum) | `Instance` |
PT1M | Yes |
IO Write Operations Per SecondThe rate at which the app process is issuing write I/O operations. For WebApps and FunctionApps. |
`IoWriteOperationsPerSecond` |
BytesPerSecond | Total (Sum) | `Instance` |
PT1M | Yes |
Memory working setThe current amount of memory used by the app, in MiB. For WebApps and FunctionApps. |
`MemoryWorkingSet` |
Bytes | Average | `Instance` |
PT1M | Yes |
On Demand Function Execution CountOn Demand Function Execution Count. For Flex Consumption FunctionApps only. |
`OnDemandFunctionExecutionCount` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
On Demand Function Execution UnitsOn Demand Function Execution Units. For Flex Consumption FunctionApps only. |
`OnDemandFunctionExecutionUnits` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Private BytesPrivate Bytes is the current size, in bytes, of memory that the app process has allocated that can't be shared with other processes. For WebApps and FunctionApps. |
`PrivateBytes` |
Bytes | Average | `Instance` |
PT1M | Yes |
RequestsThe total number of requests regardless of their resulting HTTP status code. For WebApps and FunctionApps. |
`Requests` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Requests In Application QueueThe number of requests in the application request queue. For WebApps and FunctionApps. |
`RequestsInApplicationQueue` |
Count | Average | `Instance` |
PT1M | Yes |
Thread CountThe number of threads currently active in the app process. For WebApps and FunctionApps. |
`Threads` |
Count | Average | `Instance` |
PT1M | Yes |
Total App DomainsThe current number of AppDomains loaded in this application. For WebApps and FunctionApps. |
`TotalAppDomains` |
Count | Average | `Instance` |
PT1M | Yes |
Total App Domains UnloadedThe total number of AppDomains unloaded since the start of the application. For WebApps and FunctionApps. |
`TotalAppDomainsUnloaded` |
Count | Average | `Instance` |
PT1M | Yes |
Workflow Action Completed CountWorkflow Action Completed Count. For LogicApps only. |
`WorkflowActionsCompleted` |
Count | Total (Sum) | `workflowName` , `status` |
PT1M | Yes |
Workflow Actions Failure RateWorkflow Actions Failure Rate. For LogicApps only. |
`WorkflowActionsFailureRate` |
Percent | Total (Sum) | `workflowName` |
PT1M | Yes |
Logic App Job Pull Rate Per SecondLogic Job Pull Rate per second. For LogicApps only. |
`WorkflowAppJobPullRate` |
CountPerSecond | Total (Sum) | `accountName` |
PT1M | Yes |
Workflow Job Execution DelayWorkflow Job Execution Delay. For LogicApps only. |
`WorkflowJobExecutionDelay` |
Seconds | Average | `workflowName` |
PT1M | Yes |
Workflow Job Execution DurationWorkflow Job Execution Duration. For LogicApps only. |
`WorkflowJobExecutionDuration` |
Seconds | Average | `workflowName` |
PT1M | Yes |
Workflow Runs Completed CountWorkflow Runs Completed Count. For LogicApps only. |
`WorkflowRunsCompleted` |
Count | Total (Sum) | `workflowName` , `status` |
PT1M | Yes |
Workflow Runs dispatched CountWorkflow Runs Dispatched Count. For LogicApps only. |
`WorkflowRunsDispatched` |
Count | Total (Sum) | `workflowName` |
PT1M | Yes |
Workflow Runs Failure RateWorkflow Runs Failure Rate. For LogicApps only. |
`WorkflowRunsFailureRate` |
Percent | Total (Sum) | `workflowName` |
PT1M | Yes |
Workflow Runs Started CountWorkflow Runs Started Count. For LogicApps only. |
`WorkflowRunsStarted` |
Count | Total (Sum) | `workflowName` |
PT1M | Yes |
Workflow Triggers Completed CountWorkflow Triggers Completed Count. For LogicApps only. |
`WorkflowTriggersCompleted` |
Count | Total (Sum) | `workflowName` , `status` |
PT1M | Yes |
Workflow Triggers Failure RateWorkflow Triggers Failure Rate. For LogicApps only. |
`WorkflowTriggersFailureRate` |
Percent | Total (Sum) | `workflowName` |
PT1M | Yes |

## Metric dimensions

For information about what metric dimensions are, see [Multi-dimensional metrics](/en-us/azure/azure-monitor/platform/data-platform-metrics#multi-dimensional-metrics).

This service doesn't have any metrics that contain dimensions.

## Resource logs

This section lists the types of resource logs you can collect for this service. The section pulls from the list of [all resource logs category types supported in Azure Monitor](/en-us/azure/azure-monitor/platform/resource-logs-schema).

### Supported resource logs for Microsoft.Web/sites

| Category | Category display name | Log table |
|
|---|

[Supports ingestion-time transformation](/en-us/azure/azure-monitor/essentials/data-collection-transformations)

`AppServiceAntivirusScanAuditLogs`

[AppServiceAntivirusScanAuditLogs](/en-us/azure/azure-monitor/reference/tables/appserviceantivirusscanauditlogs)Report on any discovered virus or infected files that have been uploaded to their site.

`AppServiceAppLogs`

[AppServiceAppLogs](/en-us/azure/azure-monitor/reference/tables/appserviceapplogs)Logs generated through your application.

[Queries](/en-us/azure/azure-monitor/reference/queries/appserviceapplogs)`AppServiceAuditLogs`

[AppServiceAuditLogs](/en-us/azure/azure-monitor/reference/tables/appserviceauditlogs)Logs generated when publishing users successfully log on via one of the App Service publishing protocols.

[Queries](/en-us/azure/azure-monitor/reference/queries/appserviceauditlogs)`AppServiceAuthenticationLogs`

[AppServiceAuthenticationLogs](/en-us/azure/azure-monitor/reference/tables/appserviceauthenticationlogs)Logs generated through App Service Authentication for your application.

[Queries](/en-us/azure/azure-monitor/reference/queries/appserviceauthenticationlogs)`AppServiceConsoleLogs`

[AppServiceConsoleLogs](/en-us/azure/azure-monitor/reference/tables/appserviceconsolelogs)Console logs generated from application or container.

[Queries](/en-us/azure/azure-monitor/reference/queries/appserviceconsolelogs)`AppServiceFileAuditLogs`

[AppServiceFileAuditLogs](/en-us/azure/azure-monitor/reference/tables/appservicefileauditlogs)Logs generated when app service content is modified.

[Queries](/en-us/azure/azure-monitor/reference/queries/appservicefileauditlogs)`AppServiceHTTPLogs`

[AppServiceHTTPLogs](/en-us/azure/azure-monitor/reference/tables/appservicehttplogs)Incoming HTTP requests on App Service. Use these logs to monitor application health, performance and usage patterns.

[Queries](/en-us/azure/azure-monitor/reference/queries/appservicehttplogs)`AppServiceIPSecAuditLogs`

[AppServiceIPSecAuditLogs](/en-us/azure/azure-monitor/reference/tables/appserviceipsecauditlogs)Logs generated through your application and pushed to Azure Monitoring.

`AppServicePlatformLogs`

[AppServicePlatformLogs](/en-us/azure/azure-monitor/reference/tables/appserviceplatformlogs)Logs generated through AppService platform for your application.

`FunctionAppLogs`

[FunctionAppLogs](/en-us/azure/azure-monitor/reference/tables/functionapplogs)Log generated by Function Apps. It includes logs emitted by the Functions host and logs emitted by customer code. Use these logs to monitor application health, performance, and behavior.

[Queries](/en-us/azure/azure-monitor/reference/queries/functionapplogs)`WorkflowRuntime`

[LogicAppWorkflowRuntime](/en-us/azure/azure-monitor/reference/tables/logicappworkflowruntime)Logs generated during Logic Apps workflow runtime.

[Queries](/en-us/azure/azure-monitor/reference/queries/logicappworkflowruntime)The log specific to Azure Functions is **FunctionAppLogs**.

For more information, see the [App Service monitoring data reference](/en-us/azure/app-service/monitor-app-service-reference#metrics).

## Azure Monitor Logs tables

This section lists the Azure Monitor Logs tables relevant to this service, which are available for query by Log Analytics using Kusto queries. The tables contain resource log data and possibly more depending on what is collected and routed to them.

### App Services

Microsoft.Web/sites

## Activity log

The linked table lists the operations that can be recorded in the activity log for this service. These operations are a subset of [all the possible resource provider operations in the activity log](/en-us/azure/role-based-access-control/resource-provider-operations).

For more information on the schema of activity log entries, see [Activity Log schema](/en-us/azure/azure-monitor/essentials/activity-log-schema).

The following table lists operations related to Azure Functions that might be created in the activity log.

| Operation | Description |
|---|---|
| Microsoft.web/sites/functions/listkeys/action | Return the
|

[host keys for the function app](function-keys-how-to).[Sync triggers](functions-deployment-technologies#trigger-syncing)operation.You may also find logged operations that relate to the underlying App Service behaviors. For a more complete list, see [Microsoft.Web resource provider operations](/en-us/azure/role-based-access-control/resource-provider-operations#microsoftweb).

## Related content

- See
[Monitor Azure Functions](monitor-functions)for a description of monitoring Azure Functions. - See
[Monitor Azure resources with Azure Monitor](/en-us/azure/azure-monitor/essentials/monitor-azure-resource)for details on monitoring Azure resources.
