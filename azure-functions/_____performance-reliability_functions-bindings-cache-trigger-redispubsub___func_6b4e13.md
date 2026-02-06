---
merged_at: 2026-02-06T17:09:02.566061
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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/performance-reliability -->

# Improve the performance and reliability of Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides guidance to improve the performance and reliability of your [serverless](https://azure.microsoft.com/solutions/serverless/) function apps. For a more general set of Azure Functions best practices, see [Azure Functions best practices](functions-best-practices).

The following are best practices in how you build and architect your serverless solutions using Azure Functions.

## Avoid long running functions

Large, long-running functions can cause unexpected timeout issues. To learn more about the timeouts for a given hosting plan, see [function app timeout duration](functions-scale#timeout).

A function can become large because of many Node.js dependencies. Importing dependencies can also cause increased load times that result in unexpected timeouts. Dependencies are loaded both explicitly and implicitly. A single module loaded by your code may load its own additional modules.

Whenever possible, refactor large functions into smaller function sets that work together and return responses fast. For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit; it's common for webhooks to require an immediate response. You can pass the HTTP trigger payload into a queue to be processed by a queue trigger function. This approach lets you defer the actual work and return an immediate response.

## Make sure background tasks complete

When your function starts any tasks, callbacks, threads, processes, they must complete before your function code returns. Because Functions doesn't track these background threads, site shutdown can occur regardless of background thread status, which can cause unintended behavior in your functions.

For example, if a function starts a background task and returns a successful response before the task completes, the Functions runtime considers the execution as having completed successfully, regardless of the result of the background task. If this background task is performing essential work, it may be preempted by site shutdown, leaving that work in an unknown state.

## Cross function communication

[Durable Functions](durable/durable-functions-overview) and [Azure Logic Apps](../logic-apps/logic-apps-overview) are built to manage state transitions and communication between multiple functions.

If not using Durable Functions or Logic Apps to integrate with multiple functions, it's best to use storage queues for cross-function communication. The main reason is that storage queues are cheaper and much easier to provision than other storage options.

Individual messages in a storage queue are limited in size to 64 KB. If you need to pass larger messages between functions, an Azure Service Bus queue could be used to support message sizes up to 256 KB in the Standard tier, and up to 100 MB in the Premium tier.

Service Bus topics are useful if you require message filtering before processing.

Event hubs are useful to support high volume communications.

## Write functions to be stateless

Functions should be stateless and idempotent if possible. Associate any required state information with your data. For example, an order being processed would likely have an associated `state`

member. A function could process an order based on that state while the function itself remains stateless.

Idempotent functions are especially recommended with timer triggers. For example, if you have something that absolutely must run once a day, write it so it can run anytime during the day with the same results. The function can exit when there's no work for a particular day. Also if a previous run failed to complete, the next run should pick up where it left off. This is particularly important for message-based bindings that retry on failure. For more information, see [Designing Azure Functions for identical input](functions-idempotent).

## Write defensive functions

Assume your function could encounter an exception at any time. Design your functions with the ability to continue from a previous fail point during the next execution. Consider a scenario that requires the following actions:

- Query for 10,000 rows in a database.
- Create a queue message for each of those rows to process further down the line.

Depending on how complex your system is, you may have: involved downstream services behaving badly, networking outages, or quota limits reached, etc. All of these can affect your function at any time. You need to design your functions to be prepared for it.

How does your code react if a failure occurs after inserting 5,000 of those items into a queue for processing? Track items in a set that you’ve completed. Otherwise, you might insert them again next time. This double-insertion can have a serious impact on your work flow, so [make your functions idempotent](functions-idempotent).

If a queue item was already processed, allow your function to be a no-op.

Take advantage of defensive measures already provided for components you use in the Azure Functions platform. For example, see **Handling poison queue messages** in the documentation for [Azure Storage Queue triggers and bindings](functions-bindings-storage-queue-trigger#poison-messages).

For HTTP based functions consider [API versioning strategies](/en-us/azure/architecture/reference-architectures/serverless/web-app#api-versioning) with Azure API Management. For example, if you have to update your HTTP based function app, deploy the new update to a separate function app and use API Management revisions or versions to direct clients to the new version or revision. Once all clients are using the version or revision and no more executions are left on the previous function app, you can deprovision the previous function app.

## Function organization best practices

As part of your solution, you may develop and publish multiple functions. These functions are often combined into a single function app, but they can also run in separate function apps. In Premium and dedicated (App Service) hosting plans, multiple function apps can also share the same resources by running in the same plan. How you group your functions and function apps can impact the performance, scaling, configuration, deployment, and security of your overall solution. There aren't rules that apply to every scenario, so consider the information in this section when planning and developing your functions.

### Organize functions for performance and scaling

Each function that you create has a memory footprint. While this footprint is usually small, having too many functions within a function app can lead to slower startup of your app on new instances. It also means that the overall memory usage of your function app might be higher. It's hard to say how many functions should be in a single app, which depends on your particular workload. However, if your function stores a lot of data in memory, consider having fewer functions in a single app.

If you run multiple function apps in a single Premium plan or dedicated (App Service) plan, these apps are all sharing the same resources allocated to the plan. If you have one function app that has a much higher memory requirement than the others, it uses a disproportionate amount of memory resources on each instance to which the app is deployed. Because this could leave less memory available for the other apps on each instance, you might want to run a high-memory-using function app like this in its own separate hosting plan.

Note

When using the [Consumption plan](functions-scale), we recommend you always put each app in its own plan, since apps are scaled independently anyway. For more information, see [Multiple apps in the same plan](consumption-plan#multiple-apps-in-the-same-plan).

Consider whether you want to group functions with different load profiles. For example, if you have a function that processes many thousands of queue messages, and another that is only called occasionally but has high memory requirements, you might want to deploy them in separate function apps so they get their own sets of resources and they scale independently of each other.

### Organize functions for configuration and deployment

Function apps have a `host.json`

file, which is used to configure advanced behavior of function triggers and the Azure Functions runtime. Changes to the `host.json`

file apply to all functions within the app. If you have some functions that need custom configurations, consider moving them into their own function app.

All functions in your local project are deployed together as a set of files to your function app in Azure. You might need to deploy individual functions separately or use features like [deployment slots](functions-deployment-slots) for some functions and not others. In such cases, you should deploy these functions (in separate code projects) to different function apps.

### Organize functions by privilege

Connection strings and other credentials stored in application settings gives all of the functions in the function app the same set of permissions in the associated resource. Consider minimizing the number of functions with access to specific credentials by moving functions that don't use those credentials to a separate function app. You can always use techniques such as [function chaining](/en-us/training/modules/chain-azure-functions-data-using-bindings/) to pass data between functions in different function apps.

## Scalability best practices

There are a number of factors that impact how instances of your function app scale. The details are provided in the documentation for [function scaling](functions-scale). The following are some best practices to ensure optimal scalability of a function app.

### Share and manage connections

Reuse connections to external resources whenever possible. See [how to manage connections in Azure Functions](manage-connections).

### Avoid sharing storage accounts

When you create a function app, you must associate it with a storage account. The storage account connection is maintained in the [AzureWebJobsStorage application setting](functions-app-settings#azurewebjobsstorage).

To maximize performance, use a separate storage account for each function app. This approach is particularly important when you have Durable Functions or Event Hubs triggered functions, which both generate a high volume of storage transactions. When your application logic interacts with Azure Storage, either directly (using the Storage SDK) or through one of the storage bindings, you should use a dedicated storage account. For example, if you have an event hub-triggered function writing some data to blob storage, use two storage accounts: one for the function app and another for the blobs that the function stores.

### Don't mix test and production code in the same function app

Functions within a function app share resources. For example, memory is shared. If you're using a function app in production, don't add test-related functions and resources to it. It can cause unexpected overhead during production code execution.

Be careful what you load in your production function apps. Memory is averaged across each function in the app.

If you have a shared assembly referenced in multiple .NET functions, put it in a common shared folder. Otherwise, you could accidentally deploy multiple versions of the same binary that behave differently between functions.

Don't use verbose logging in production code, which has a negative performance impact.

### Use async code but avoid blocking calls

Asynchronous programming is a recommended best practice, especially when blocking I/O operations are involved.

In C#, always avoid referencing the `Result`

property or calling `Wait`

method on a `Task`

instance. This approach can lead to thread exhaustion.

Tip

If you plan to use the HTTP or WebHook bindings, plan to avoid port exhaustion that can be caused by improper instantiation of `HttpClient`

. For more information, see [How to manage connections in Azure Functions](manage-connections).

### Use multiple worker processes

By default, any host instance for Functions uses a single worker process. To improve performance, especially with single-threaded runtimes like Python, use the [FUNCTIONS_WORKER_PROCESS_COUNT](functions-app-settings#functions_worker_process_count) to increase the number of worker processes per host (up to 10). Azure Functions then tries to evenly distribute simultaneous function invocations across these workers.

The FUNCTIONS_WORKER_PROCESS_COUNT applies to each host that Functions creates when scaling out your application to meet demand.

### Receive messages in batch whenever possible

Some triggers like Event Hub enable receiving a batch of messages on a single invocation. Batching messages has much better performance. You can configure the max batch size in the `host.json`

file as detailed in the [host.json reference documentation](functions-host-json)

For C# functions, you can change the type to a strongly-typed array. For example, instead of `EventData sensorEvent`

the method signature could be `EventData[] sensorEvent`

. For other languages, you'll need to explicitly set the cardinality property in your `function.json`

to `many`

in order to enable batching [as shown here](https://github.com/Azure/azure-webjobs-sdk-templates/blob/df94e19484fea88fc2c68d9f032c9d18d860d5b5/Functions.Templates/Templates/EventHubTrigger-JavaScript/function.json#L10).

### Configure host behaviors to better handle concurrency

The `host.json`

file in the function app allows for configuration of host runtime and trigger behaviors. In addition to batching behaviors, you can manage concurrency for a number of triggers. Often adjusting the values in these options can help each instance scale appropriately for the demands of the invoked functions.

Settings in the host.json file apply across all functions within the app, within a *single instance* of the function. For example, if you had a function app with two HTTP functions and [ maxConcurrentRequests](functions-bindings-http-webhook#hostjson-settings) requests set to 25, a request to either HTTP trigger would count towards the shared 25 concurrent requests. When that function app is scaled to 10 instances, the ten functions effectively allow 250 concurrent requests (10 instances * 25 concurrent requests per instance).

Other host configuration options are found in the [host.json configuration article](functions-host-json).

## Next steps

For more information, see the following resources:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache-trigger-redispubsub -->

# RedisPubSubTrigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Redis features [publish/subscribe functionality](https://redis.io/docs/latest/commands/pubsub/) that enables messages to be sent to Redis and broadcast to subscribers.

For more information about Azure Cache for Redis triggers and bindings, [Redis Extension for Azure Functions](https://github.com/Azure/azure-functions-redis-extension/tree/main).

## Scope of availability for functions triggers

| Trigger Type | Azure Managed Redis | Azure Cache for Redis |
|---|---|---|
| Pub/Sub Trigger | Yes | Yes |

Important

When using Azure Managed Redis or the Enterprise tiers of Azure Cache for Redis, use port 10000 rather than port 6380 or 6379.

Warning

This trigger isn't supported on a [Consumption plan](/en-us/azure/azure-functions/consumption-plan) or a [Flex Consumption plan](/en-us/azure/azure-functions/flex-consumption-plan) plan because Redis PubSub requires clients to always be actively listening to receive all messages. For consumption plans, your function might miss certain messages published to the channel.

Important

The Node.js v4 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Important

The Python v2 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v2 model works, refer to the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

## Examples

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).Important

For .NET functions, using the *isolated worker* model is recommended over the *in-process* model. For a comparison of the *in-process* and *isolated worker* models, see differences between the *isolated worker* model and the *in-process* model for .NET on Azure Functions.

This sample listens to the channel `pubsubTest`

.

```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.Functions.Worker.Extensions.Redis.Samples.RedisPubSubTrigger
{
internal class SimplePubSubTrigger
{
private readonly ILogger<SimplePubSubTrigger> logger;
public SimplePubSubTrigger(ILogger<SimplePubSubTrigger> logger)
{
this.logger = logger;
}
[Function(nameof(SimplePubSubTrigger))]
public void Run(
[RedisPubSubTrigger(Common.connectionStringSetting, "pubsubTest")] string message)
{
logger.LogInformation(message);
}
}
}
```


This sample listens to any keyspace notifications for the key `keyspaceTest`

.

```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.Functions.Worker.Extensions.Redis.Samples.RedisPubSubTrigger
{
internal class KeyspaceTrigger
{
private readonly ILogger<KeyspaceTrigger> logger;
public KeyspaceTrigger(ILogger<KeyspaceTrigger> logger)
{
this.logger = logger;
}
[Function(nameof(KeyspaceTrigger))]
public void Run(
[RedisPubSubTrigger(Common.connectionStringSetting, "__keyspace@0__:keyspaceTest")] string message)
{
logger.LogInformation(message);
}
}
}
```


This sample listens to any `keyevent`

notifications for the delete command [ DEL](https://redis.io/commands/del/).

```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.Functions.Worker.Extensions.Redis.Samples.RedisPubSubTrigger
{
internal class KeyeventTrigger
{
private readonly ILogger<KeyeventTrigger> logger;
public KeyeventTrigger(ILogger<KeyeventTrigger> logger)
{
this.logger = logger;
}
[Function(nameof(KeyeventTrigger))]
public void Run(
[RedisPubSubTrigger(Common.connectionStringSetting, "__keyevent@0__:del")] string message)
{
logger.LogInformation($"Key '{message}' deleted.");
}
}
}
```


This sample listens to the channel `pubsubTest`

.

```
package com.function.RedisPubSubTrigger;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.redis.annotation.*;
public class SimplePubSubTrigger {
@FunctionName("SimplePubSubTrigger")
public void run(
@RedisPubSubTrigger(
name = "req",
connection = "redisConnectionString",
channel = "pubsubTest",
pattern = false)
String message,
final ExecutionContext context) {
context.getLogger().info(message);
}
}
```


This sample listens to any keyspace notifications for the key `myKey`

.

```
package com.function.RedisPubSubTrigger;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.redis.annotation.*;
public class KeyspaceTrigger {
@FunctionName("KeyspaceTrigger")
public void run(
@RedisPubSubTrigger(
name = "req",
connection = "redisConnectionString",
channel = "__keyspace@0__:keyspaceTest",
pattern = false)
String message,
final ExecutionContext context) {
context.getLogger().info(message);
}
}
```


This sample listens to any `keyevent`

notifications for the delete command [ DEL](https://redis.io/commands/del/).

```
package com.function.RedisPubSubTrigger;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.redis.annotation.*;
public class KeyeventTrigger {
@FunctionName("KeyeventTrigger")
public void run(
@RedisPubSubTrigger(
name = "req",
connection = "redisConnectionString",
channel = "__keyevent@0__:del",
pattern = false)
String message,
final ExecutionContext context) {
context.getLogger().info(message);
}
}
```


This sample uses the same `index.js`

file, with binding data in the `function.json`

file determining on which channel the trigger occurs.

Here's the `index.js`

file:

```
module.exports = async function (context, message) {
context.log(message);
}
```


From `function.json`

:

Here's binding data to listen to the channel `pubsubTest`

.

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "pubsubTest",
"pattern": false,
"name": "message",
"direction": "in"
}
],
"scriptFile": "index.js"
}
```


Here's binding data to listen to keyspace notifications for the key `keyspaceTest`

.

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "__keyspace@0__:keyspaceTest",
"pattern": false,
"name": "message",
"direction": "in"
}
],
"scriptFile": "index.js"
}
```


Here's binding data to listen to `keyevent`

notifications for the delete command [ DEL](https://redis.io/commands/del/).

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "__keyevent@0__:del",
"pattern": false,
"name": "message",
"direction": "in"
}
],
"scriptFile": "index.js"
}
```


This sample uses the same `run.ps1`

file, with binding data in the `function.json`

file determining on which channel the trigger occurs.

Here's the `run.ps1`

file:

```
param($message, $TriggerMetadata)
Write-Host $message
```


From `function.json`

:

Here's binding data to listen to the channel `pubsubTest`

.

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "pubsubTest",
"pattern": false,
"name": "message",
"direction": "in"
}
],
"scriptFile": "run.ps1"
}
```


Here's binding data to listen to keyspace notifications for the key `keyspaceTest`

.

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "__keyspace@0__:keyspaceTest",
"pattern": false,
"name": "message",
"direction": "in"
}
],
"scriptFile": "run.ps1"
}
```


Here's binding data to listen to `keyevent`

notifications for the delete command [ DEL](https://redis.io/commands/del/).

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "__keyevent@0__:del",
"pattern": false,
"name": "message",
"direction": "in"
}
],
"scriptFile": "run.ps1"
}
```


The Python v1 programming model requires you to define bindings in a separate *function.json* file in the function folder. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-configuration#programming-model).

This sample uses the same `__init__.py`

file, with binding data in the `function.json`

file determining on which channel the trigger occurs.

Here's the `__init__.py`

file:

```
import logging
def main(message: str):
logging.info(message)
```


From `function.json`

:

Here's binding data to listen to the channel `pubsubTest`

.

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "pubsubTest",
"pattern": false,
"name": "message",
"direction": "in"
}
],
"scriptFile": "__init__.py"
}
```


Here's binding data to listen to keyspace notifications for the key `keyspaceTest`

.

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "__keyspace@0__:keyspaceTest",
"pattern": false,
"name": "message",
"direction": "in"
}
],
"scriptFile": "__init__.py"
}
```


Here's binding data to listen to `keyevent`

notifications for the delete command [ DEL](https://redis.io/commands/del/).

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "__keyevent@0__:del",
"pattern": false,
"name": "message",
"direction": "in"
}
],
"scriptFile": "__init__.py"
}
```


## Attributes

| Parameter | Description | Required | Default |
|---|---|---|---|
`Connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`Channel`

`INameResolver`

.## Annotations

| Parameter | Description | Required | Default |
|---|---|---|---|
`name` |
Name of the variable holding the value returned by the function. | Yes | |
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`channel`

## Configuration

| function.json property | Description | Required | Default |
|---|---|---|---|
`type` |
Trigger type. For the pub sub trigger, the type is `redisPubSubTrigger` . |
Yes | |
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`channel`

`pattern`

`pattern`

is true, then the channel is treated like a *glob-style*pattern instead of as a literal.`name`

`direction`

`in`

.Important

The `connection`

parameter does not hold the Redis cache connection string itself. Instead, it points to the name of the environment variable that holds the connection string. This makes the application more secure. For more information, see [Redis connection string](functions-bindings-cache#redis-connection-string).

## Usage

Redis features [publish/subscribe functionality](https://redis.io/docs/latest/commands/pubsub/) that enables messages to be sent to Redis and broadcast to subscribers. The `RedisPubSubTrigger`

enables Azure Functions to be triggered on pub/sub activity. The `RedisPubSubTrigger`

subscribes to a specific channel pattern using [ PSUBSCRIBE](https://redis.io/commands/psubscribe/), and surfaces messages received on those channels to the function.

### Prerequisites and limitations

- The
`RedisPubSubTrigger`

isn't capable of listening to[keyspace notifications](https://redis.io/docs/latest/develop/pubsub/keyspace-notifications/)on clustered caches. - Basic tier functions don't support triggering on
`keyspace`

or`keyevent`

notifications through the`RedisPubSubTrigger`

. - The
`RedisPubSubTrigger`

isn't supported on a[Consumption plan](/en-us/azure/azure-functions/consumption-plan)or a[Flex Consumption plan](/en-us/azure/azure-functions/flex-consumption-plan)because Redis PubSub requires clients to always be actively listening to receive all messages. For consumption plans, your function might miss certain messages published to the channel. - Functions with the
`RedisPubSubTrigger`

shouldn't be scaled out to multiple instances. Each instance listens and processes each pub sub message, resulting in duplicate processing.

Warning

This trigger isn't supported on a [Consumption plan](/en-us/azure/azure-functions/consumption-plan) or a [Flex Consumption plan](/en-us/azure/azure-functions/flex-consumption-plan) because Redis PubSub requires clients to always be actively listening to receive all messages. For consumption plans, your function might miss certain messages published to the channel.

## Triggering on keyspace notifications

Redis offers a built-in concept called [keyspace notifications](https://redis.io/docs/latest/develop/pubsub/keyspace-notifications/). When enabled, this feature publishes notifications of a wide range of cache actions to a dedicated pub/sub channel. Supported actions include actions that affect specific keys, called *keyspace notifications*, and specific commands, called *keyevent notifications*. A huge range of Redis actions are supported, such as `SET`

, `DEL`

, and `EXPIRE`

. The full list can be found in the [keyspace notification documentation](https://redis.io/docs/latest/develop/pubsub/keyspace-notifications/).

The `keyspace`

and `keyevent`

notifications are published with the following syntax:

```
PUBLISH __keyspace@0__:<affectedKey> <command>
PUBLISH __keyevent@0__:<affectedCommand> <key>
```


Because these events are published on pub/sub channels, the `RedisPubSubTrigger`

is able to pick them up. See the [RedisPubSubTrigger](functions-bindings-cache-trigger-redispubsub) section for more examples.

Important

In Azure Cache for Redis, `keyspace`

events must be enabled before notifications are published. For more information, see [Advanced Settings](/en-us/azure/azure-cache-for-redis/cache-configure#keyspace-notifications-advanced-settings).

| Type | Description |
|---|---|
`string` |
The channel message serialized as JSON (UTF-8 encoded for byte types) in the format that follows. |
`Custom` |
The trigger uses Json.NET serialization to map the message from the channel into the given custom type. |

JSON string format

```
{
"SubscriptionChannel":"__keyspace@0__:*",
"Channel":"__keyspace@0__:mykey",
"Message":"set"
}
```


| Type | Description |
|---|---|
`string` |
The channel message serialized as JSON (UTF-8 encoded for byte types) in the format that follows. |
`Custom` |
The trigger uses Json.NET serialization to map the message from the channel from a `string` into a custom type. |

```
{
"SubscriptionChannel":"__keyspace@0__:*",
"Channel":"__keyspace@0__:mykey",
"Message":"set"
}
```

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-scheduled-function -->

# Create a function in the Azure portal that runs on a schedule

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Learn how to use the Azure portal to create a function that runs [serverless](https://azure.microsoft.com/solutions/serverless/) on Azure based on a schedule that you define.

Note

In-portal editing is only supported for JavaScript, PowerShell, and C# Script functions.
Python in-portal editing is supported only when running in the Consumption plan.
To create a C# Script app that supports in-portal editing, you must choose a runtime **Version** that supports the **in-process model**.

When possible, you should [develop your functions locally](functions-develop-local).

To learn more about the limitations on editing function code in the Azure portal, see [Development limitations in the Azure portal](functions-how-to-use-azure-function-app-settings#development-limitations-in-the-azure-portal).

## Prerequisites

To complete this tutorial:

Ensure that you have an Azure subscription. If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Create a function app

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

Your new function app is ready to use. Next, you create a function in the new function app.


## Create a timer triggered function

In your function app, select

**Overview**, and then select**+ Create**under**Functions**.Under

**Select a template**, scroll down and choose the**Timer trigger**template.In

**Template details**, configure the new trigger with the settings as specified in the table below the image, and then select**Create**.Setting Suggested value Description **Name**Default Defines the name of your timer triggered function. **Schedule**0 */1 * * * * A six field [CRON expression](functions-bindings-timer#ncrontab-expressions)that schedules your function to run every minute.

## Test the function

In your function, select

**Code + Test**and expand the**Logs**.Verify execution by viewing the information written to the logs.


Now, you change the function's schedule so that it runs once every hour instead of every minute.

## Update the timer schedule

In your function, select

**Integration**. Here, you define the input and output bindings for your function and also set the schedule.Select

**Timer (myTimer)**.Update the

**Schedule**value to`0 0 */1 * * *`

, and then select**Save**.

You now have a function that runs once every hour, on the hour.

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

You created a function that runs based on a schedule. For more information about timer triggers, see [Timer trigger for Azure Functions](functions-bindings-timer).

Now that you've created your first function, let's add an output binding to the function that writes a message to a Storage queue.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-sql -->

# Azure SQL bindings for Azure Functions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This set of articles explains how to work with [Azure SQL](/en-us/azure/azure-sql/index) bindings in Azure Functions. Azure Functions supports input bindings, output bindings, and a function trigger for the Azure SQL and SQL Server products.

| Action | Type |
|---|---|
| Trigger a function when a change is detected on a SQL table |
|

[Input binding](functions-bindings-azure-sql-input)[Output binding](functions-bindings-azure-sql-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

Add the extension to your project by installing this [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Sql/).

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Sql
```


To use a preview version of the Microsoft.Azure.Functions.Worker.Extensions.Sql package, add the `--prerelease`

flag to the command. You can view preview functionality on the [Azure Functions SQL Extensions release page](https://github.com/Azure/azure-functions-sql-extension/releases).

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Sql --prerelease
```


Note

Breaking changes between preview releases of the Azure SQL bindings for Azure Functions requires that all Functions targeting the same database use the same version of the SQL extension package.

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

If your app needs to use preview functionality, you should instead reference the latest version of the preview bundle. For more information, see [Work with preview extension bundles](extension-bundles#work-with-preview-extension-bundles).

You can view preview functionality on the [Azure Functions SQL Extensions release page](https://github.com/Azure/azure-functions-sql-extension/releases).

Note

Breaking changes between preview releases of the Azure SQL bindings for Azure Functions requires that all Functions targeting the same database use the same version of the SQL extension package.

## Update packages

Add the [Azure Functions Java SQL Types package](https://mvnrepository.com/artifact/com.microsoft.azure.functions/azure-functions-java-library-sql) to your functions project with an update to the `pom.xml`

file in your project, as in this example:

```
<dependency>
<groupId>com.microsoft.azure.functions</groupId>
<artifactId>azure-functions-java-library-sql</artifactId>
<version>2.1.0</version>
</dependency>
```


## SQL connection string

Azure SQL bindings for Azure Functions have a required property for the connection string on all bindings and triggers. These pass the connection string to the Microsoft.Data.SqlClient library and supports the connection string as defined in the [SqlClient ConnectionString documentation](/en-us/dotnet/api/microsoft.data.sqlclient.sqlconnection.connectionstring?view=sqlclient-dotnet-core-5.0&preserve-view=true#Microsoft_Data_SqlClient_SqlConnection_ConnectionString).

Important

For optimal security, you should use Microsoft Entra ID with managed identities for connections between Functions and Azure SQL Database. Managed identities make your app more secure by eliminating secrets from your application deployments, such as credentials in the connection strings, server names, and ports being used. You can learn how to use managed identities in this tutorial, [Connect a function app to Azure SQL with managed identity and SQL bindings](functions-identity-access-azure-sql-with-managed-identity).

Notable keywords include:

`Authentication`

: allows a function to connect to Azure SQL with Microsoft Entra ID and managed identities. For more information, see[Connect a function app to Azure SQL with managed identity and SQL bindings](functions-identity-access-azure-sql-with-managed-identity).`Command timeout`

: allows a function to wait for specified amount of time in seconds before terminating a query (default 30 seconds)`ConnectRetryCount`

: allows a function to automatically make additional reconnection attempts, especially applicable to Azure SQL Database serverless tier (default 1)`Pooling`

: allows a function to reuse connections to the database, which can improve performance (default`true`

). Additional settings for connection pooling include`Connection Lifetime`

,`Max Pool Size`

, and`Min Pool Size`

. Learn more about connection pooling in the[ADO.NET documentation](/en-us/sql/connect/ado-net/sql-server-connection-pooling)

## Considerations

- Azure SQL binding supports version 4.x and later of the Functions runtime.
- Source code for the Azure SQL bindings can be found in
[this GitHub repository](https://github.com/Azure/azure-functions-sql-extension). - This binding requires connectivity to an Azure SQL or SQL Server database.
- Output bindings against tables with columns of data types
`NTEXT`

,`TEXT`

, or`IMAGE`

aren't supported and data upserts will fail. These types[will be removed](/en-us/sql/t-sql/data-types/ntext-text-and-image-transact-sql)in a future version of SQL Server and aren't compatible with the`OPENJSON`

function used by this Azure Functions binding. - Use
[managed identities](/en-us/azure/azure-sql/database/authentication-azure-ad-user-assigned-managed-identity)instead of usernames and passwords. - Consider using an
[Azure Key Value](/en-us/azure/app-service/app-service-key-vault-references)to store application settings.

## Samples

In addition to the samples for C#, Java, JavaScript, PowerShell, and Python available in the [Azure SQL bindings GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples), more are available in Azure Samples:

[C# ToDo API sample with Azure SQL bindings](/en-us/samples/azure-samples/azure-sql-binding-func-dotnet-todo/todo-backend-dotnet-azure-sql-bindings-azure-functions/)[Use SQL bindings in Azure Stream Analytics](../stream-analytics/sql-database-upsert#option-1-update-by-key-with-the-azure-function-sql-binding)[Send data from Azure SQL with Python](/en-us/samples/azure-samples/sqlbindings-python-datatransfer/sample-load-data-from-sql-using-python-and-azure-functions/)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-add-openai-text-completion -->

# Tutorial: Add Azure OpenAI text completion hints to your functions in Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use Visual Studio Code to add an HTTP endpoint to the function app you created in the previous quickstart article. When triggered, this new HTTP endpoint uses an [Azure OpenAI text completion input binding](functions-bindings-openai-textcompletion-input) to get text completion hints from your data model.

During this tutorial, you learn how to accomplish these tasks:

- Create resources in Azure OpenAI.
- Deploy a model in the OpenAI resource.
- Set access permissions to the model resource.
- Enable your function app to connect to OpenAI.
- Add OpenAI bindings to your HTTP triggered function.

## 1. Check prerequisites

- Complete the steps in
[part 1 of Create a function in Azure using Visual Studio Code](how-to-create-function-vs-code). - Obtain access to Azure OpenAI in your Azure subscription. If you haven't already been granted access, complete
[this form](https://aka.ms/oai/access)to request access.

- Install
[.NET Core CLI tools](/en-us/dotnet/core/tools/?tabs=netcore2x).

- The
[Azurite storage emulator](../storage/common/storage-use-azurite?tabs=npm). While you can also use an actual Azure Storage account, the article assumes you're using this emulator.

## 2. Create your Azure OpenAI resources

The following steps show how to create an Azure OpenAI data model in the Azure portal.

Sign in with your Azure subscription in the

[Azure portal](https://portal.azure.com).Select

**Create a resource**and search for the**Azure OpenAI**. When you locate the service, select**Create**.On the

**Create Azure OpenAI**page, provide the following information for the fields on the**Basics**tab:Field Description **Subscription**Your subscription, which has been onboarded to use Azure OpenAI. **Resource group**The resource group you created for the function app in the previous article. You can find this resource group name by right-clicking the function app in the Azure Resources browser, selecting properties, and then searching for the `resourceGroup`

setting in the returned JSON resource file.**Region**Ideally, the same location as the function app. **Name**A descriptive name for your Azure OpenAI Service resource, such as *mySampleOpenAI*.**Pricing Tier**The pricing tier for the resource. Currently, only the Standard tier is available for the Azure OpenAI Service. For more info on pricing visit the [Azure OpenAI pricing page](https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/)Select

**Next**twice to accept the default values for both the**Network**and**Tags**tabs. The service you create doesn't have any network restrictions, including from the internet.Select

**Next**a final time to move to the final stage in the process:**Review + submit**.Confirm your configuration settings, and select

**Create**.The Azure portal displays a notification when the new resource is available. Select

**Go to resource**in the notification or search for your new Azure OpenAI resource by name.In the Azure OpenAI resource page for your new resource, select

**Click here to view endpoints**under**Essentials**>**Endpoints**. Copy the**endpoint**URL and the**keys**. Save these values, you need them later.

Now that you have the credentials to connect to your model in Azure OpenAI, you need to set these access credentials in application settings.

## 3. Deploy a model

Now you can deploy a model. You can select from one of several available models in Azure OpenAI Studio.

To deploy a model, follow these steps:

Sign in to

[Azure OpenAI Studio](https://oai.azure.com).Choose the subscription and the Azure OpenAI resource you created, and select

**Use resource**.Under

**Management**select**Deployments**.Select

**Create new deployment**and configure the following fields:Field Description **Deployment name**Choose a name carefully. The deployment name is used in your code to call the model by using the client libraries and the REST APIs, so you must save for use later on. **Select a model**Model availability varies by region. For a list of available models per region, see [Model summary table and region availability](/en-us/azure/ai-services/openai/concepts/models#model-summary-table-and-region-availability).Important

When you access the model via the API, you need to refer to the deployment name rather than the underlying model name in API calls, which is one of the key differences between OpenAI and Azure OpenAI. OpenAI only requires the model name. Azure OpenAI always requires deployment name, even when using the model parameter. In our docs, we often have examples where deployment names are represented as identical to model names to help indicate which model works with a particular API endpoint. Ultimately your deployment names can follow whatever naming convention is best for your use case.

Accept the default values for the rest of the setting and select

**Create**.The deployments table shows a new entry that corresponds to your newly created model.


You now have everything you need to add Azure OpenAI-based text completion to your function app.

## 4. Update application settings

In Visual Studio Code, open the local code project you created when you completed the

[previous article](how-to-create-function-vs-code?pivot=programming-language-csharp).In the local.settings.json file in the project root folder, update the

`AzureWebJobsStorage`

setting to`UseDevelopmentStorage=true`

. You can skip this step if the`AzureWebJobsStorage`

setting in*local.settings.json*is set to the connection string for an existing Azure Storage account instead of`UseDevelopmentStorage=true`

.In the local.settings.json file, add these settings values:

: required by the binding extension. Set this value to the endpoint of the Azure OpenAI resource you created earlier.`AZURE_OPENAI_ENDPOINT`

: required by the binding extension. Set this value to the key for the Azure OpenAI resource.`AZURE_OPENAI_KEY`

: used to define the input binding. Set this value to the name you chose for your model deployment.`CHAT_MODEL_DEPLOYMENT_NAME`


Save the file. When you deploy to Azure, you must also add these settings to your function app.


## 5. Register binding extensions

Because you're using an Azure OpenAI output binding, you must have the corresponding bindings extension installed before you run the project.

Except for HTTP and timer triggers, bindings are implemented as extension packages. To add the Azure OpenAI extension package to your project, run this [dotnet add package](/en-us/dotnet/core/tools/dotnet-add-package) command in the **Terminal** window:

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.OpenAI --prerelease
```


## 5. Update the extension bundle

To access the preview Azure OpenAI bindings, you must use a preview version of the extension bundle that contains this extension.

Replace the `extensionBundle`

setting in your current `host.json`

file with this JSON:

```
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle.Preview",
"version": "[4.*, 5.0.0)"
}
```


Now, you can use the Azure OpenAI output binding in your project.

## 6. Return text completion from the model

The code you add creates a `whois`

HTTP function endpoint in your existing project. In this function, data passed in a URL `name`

parameter of a GET request is used to dynamically create a completion prompt. This dynamic prompt is bound to a text completion input binding, which returns a response from the model based on the prompt. The completion from the model is returned in the HTTP response.

In your existing

`HttpExample`

class file, add this`using`

statement:`using Microsoft.Azure.Functions.Worker.Extensions.OpenAI.TextCompletion;`

In the same file, add this code that defines a new HTTP trigger endpoint named

`whois`

:`[Function(nameof(WhoIs))] public IActionResult WhoIs([HttpTrigger(AuthorizationLevel.Function, Route = "whois/{name}")] HttpRequest req, [TextCompletionInput("Who is {name}?", ChatModel = "%CHAT_MODEL_DEPLOYMENT_NAME%")] TextCompletionResponse response) { if(!String.IsNullOrEmpty(response.Content)) { return new OkObjectResult(response.Content); } else { return new NotFoundObjectResult("Something went wrong."); } }`


Update the

`pom.xml`

project file to add this reference to the`properties`

collection:`<azure-functions-java-library-openai>0.5.0-preview</azure-functions-java-library-openai>`

In the same file, add this dependency to the

`dependencies`

collection:`<dependency> <groupId>com.microsoft.azure.functions</groupId> <artifactId>azure-functions-java-library-openai</artifactId> <version>${azure-functions-java-library-openai}</version> </dependency>`

In the existing

`Function.java`

project file, add these`import`

statements:`import com.microsoft.azure.functions.openai.annotation.textcompletion.TextCompletion; import com.microsoft.azure.functions.openai.annotation.textcompletion.TextCompletionResponse;`

In the same file, add this code that defines a new HTTP trigger endpoint named

`whois`

:`@FunctionName("WhoIs") public HttpResponseMessage whoIs( @HttpTrigger( name = "req", methods = {HttpMethod.GET}, authLevel = AuthorizationLevel.ANONYMOUS, route = "whois/{name}") HttpRequestMessage<Optional<String>> request, @BindingName("name") String name, @TextCompletion(prompt = "Who is {name}?", chatModel = "%CHAT_MODEL_DEPLOYMENT_NAME%", name = "response", isReasoningModel = false) TextCompletionResponse response, final ExecutionContext context) { return request.createResponseBuilder(HttpStatus.OK) .header("Content-Type", "application/json") .body(response.getContent()) .build(); }`


In Visual Studio Code, Press F1 and in the command palette type

`Azure Functions: Create Function...`

, select**HTTP trigger**, type the function name`whois`

, and press Enter.In the new

`whois.js`

code file, replace the contents of the file with this code:`const { app, input } = require("@azure/functions"); // This OpenAI completion input requires a {name} binding value. const openAICompletionInput = input.generic({ prompt: 'Who is {name}?', maxTokens: '100', type: 'textCompletion', chatModel: '%CHAT_MODEL_DEPLOYMENT_NAME%' }) app.http('whois', { methods: ['GET'], route: 'whois/{name}', authLevel: 'function', extraInputs: [openAICompletionInput], handler: async (_request, context) => { var response = context.extraInputs.get(openAICompletionInput) return { body: response.content.trim() } } });`


In Visual Studio Code, Press F1 and in the command palette type

`Azure Functions: Create Function...`

, select**HTTP trigger**, type the function name`whois`

, and press Enter.In the new

`whois.ts`

code file, replace the contents of the file with this code:`import { app, input } from "@azure/functions"; // This OpenAI completion input requires a {name} binding value. const openAICompletionInput = input.generic({ prompt: 'Who is {name}?', maxTokens: '100', type: 'textCompletion', chatModel: '%CHAT_MODEL_DEPLOYMENT_NAME%' }) app.http('whois', { methods: ['GET'], route: 'whois/{name}', authLevel: 'function', extraInputs: [openAICompletionInput], handler: async (_request, context) => { var response: any = context.extraInputs.get(openAICompletionInput) return { body: response.content.trim() } } });`


In the existing

`function_app.py`

project file, add this`import`

statement:`import json`

In the same file, add this code that defines a new HTTP trigger endpoint named

`whois`

:`@app.route(route="whois/{name}", methods=["GET"]) @app.text_completion_input( arg_name="response", prompt="Who is {name}?", max_tokens="100", chat_model="%CHAT_MODEL_DEPLOYMENT_NAME%", ) def whois(req: func.HttpRequest, response: str) -> func.HttpResponse: response_json = json.loads(response) return func.HttpResponse(response_json["content"], status_code=200)`


In Visual Studio Code, Press F1 and in the command palette type

`Azure Functions: Create Function...`

, select**HTTP trigger**, type the function name`whois`

, select**Anonymous**, and press Enter.Open the new

`whois/function.json`

code file and replace its contents with this code, which adds a definition for the`TextCompletionResponse`

input binding:`{ "bindings": [ { "authLevel": "function", "type": "httpTrigger", "direction": "in", "name": "Request", "route": "whois/{name}", "methods": [ "get" ] }, { "type": "http", "direction": "out", "name": "Response" }, { "type": "textCompletion", "direction": "in", "name": "TextCompletionResponse", "prompt": "Who is {name}?", "maxTokens": "100", "chatModel": "%CHAT_MODEL_DEPLOYMENT_NAME%" } ] }`

Replace the content of the

`whois/run.ps1`

code file with this code, which returns the input binding response:`using namespace System.Net param($Request, $TriggerMetadata, $TextCompletionResponse) Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{ StatusCode = [HttpStatusCode]::OK Body = $TextCompletionResponse.Content })`


## 7. Run the function

In Visual Studio Code, Press F1 and in the command palette type

`Azurite: Start`

and press Enter to start the Azurite storage emulator.Press

`F5`to start the function app project and Core Tools in debug mode.With the Core Tools running, send a GET request to the

`whois`

endpoint function, with a name in the path, like this URL:`http://localhost:7071/api/whois/<NAME>`

Replace the

`<NAME>`

string with the value you want passed to the`"Who is {name}?"`

prompt. The`<NAME>`

must be the URL-encoded name of a public figure, like`Abraham%20Lincoln`

.The response you see is the text completion response from your Azure OpenAI model.

After a response is returned, press

`Ctrl + C`to stop Core Tools.

## 8. Clean up resources

In Azure, *resources* refer to function apps, functions, storage accounts, and so forth. They're grouped into *resource groups*, and you can delete everything in a group by deleting the group.

You created resources to complete these quickstarts. You could be billed for these resources, depending on your [account status](https://azure.microsoft.com/account/) and [service pricing](https://azure.microsoft.com/pricing/). If you don't need the resources anymore, here's how to delete them:

In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azure: Open in portal`

.Choose your function app and press

`Enter`. The function app page opens in the Azure portal.In the

**Overview**tab, select the named link next to**Resource group**.On the

**Resource group**page, review the list of included resources, and verify that they're the ones you want to delete.Select

**Delete resource group**, and follow the instructions.Deletion may take a couple of minutes. When it's done, a notification appears for a few seconds. You can also select the bell icon at the top of the page to view the notification.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-premium-plan -->

# Azure Functions Premium plan

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Functions Elastic Premium plan is a dynamic scale hosting option for function apps. For other hosting plan options, see [Azure Functions hosting options](functions-scale).

Important

Azure Functions can run on the Azure App Service platform. In the App Service platform, plans that host Premium plan function apps are referred to as *Elastic* Premium plans, with SKU names like `EP1`

. If you choose to run your function app on a Premium plan, make sure to create a plan with an SKU name that starts with "E", such as `EP1`

. App Service plan SKU names that start with "P", such as `P1V2`

(Premium V2 Small plan), are actually [Dedicated hosting plans](dedicated-plan). Because they are Dedicated and not Elastic Premium, plans with SKU names starting with "P" won't scale dynamically and may increase your costs.

Premium plan hosting provides the following benefits for your functions:

*Always ready*and*prewarmed*instances to avoid cold starts- Virtual network connectivity
- Support for
[longer runtime durations](#longer-run-duration) [Choice of Premium instance sizes](#available-instance-skus)- More predictable pricing, compared with the Consumption plan
- High-density app allocation for plans with multiple function apps
- Support for
[Linux container deployments](container-concepts)

When you use the Premium plan, you add and remove instances of the Azure Functions host based on the number of incoming events, just like the [Flex Consumption plan](flex-consumption-plan) and the [Consumption plan](consumption-plan). You can deploy multiple function apps to the same Premium plan. You can configure the compute instance size, base plan size, and maximum plan size.

## Billing

You pay for the Premium plan based on the number of core seconds and memory allocated across instances. This billing model differs from the Consumption plan, which bills you based on per-second resource consumption and executions. The Premium plan has no execution charge. This billing model results in a minimum monthly cost per active plan, whether the function is active or idle. All function apps in a Premium plan share allocated instances. For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).

Note

Every premium plan always has at least one active (billed) instance.

## Create a Premium plan

When you create a function app in the Azure portal, the Consumption plan is the default. To create a function app that runs in a Premium plan, you must explicitly create or choose an Azure Functions Premium hosting plan by using one of the *Elastic Premium* versions. You host the function app you create in this plan. The Azure portal makes it easy to create both the Premium plan and the function app at the same time. You can run more than one function app in the same Premium plan, but they must both run on the same operating system (Windows or Linux).

The following articles show you how to programmatically create a function app with a Premium plan:

## Eliminate cold starts

When events or executions don't occur in the Consumption plan, your app might scale to zero instances. When new events arrive, the system must create a new instance that runs your app. Specializing new instances takes time, depending on the app. This extra latency on the first call is often called a [cold start](event-driven-scaling#cold-start).

The Premium plan provides two features that work together to effectively eliminate cold starts in your functions: *always ready instances* and *prewarmed instances*. Always ready instances are a category of preallocated instances unaffected by scaling, and the prewarmed instances are a buffer as you scale due to HTTP events.

When events begin to trigger the app, the system first routes them to the always ready instances. As the function becomes active due to HTTP events, other instances warm as a buffer. These buffered instances are called prewarmed instances. This buffer reduces cold start for new instances required during scale.

### Always ready instances

In the Premium plan, you can have your app always ready on a specified number of instances. Your app runs continuously on those instances, regardless of load. If load exceeds what your always ready instances can handle, the app adds more instances as necessary, up to your specified maximum.

This app-level setting also controls your plan's minimum instances. For example, consider three function apps in the same Premium plan. When two of your apps have always ready instance count set to one, and the third app is set to five, the minimum number for your whole plan is five. This number also reflects the minimum number of instances for which your plan is billed. The maximum number of always ready instances supported per app is 20.

You can configure the number of always ready instances in the Azure portal by selecting your **Function App**, going to the **App Service plan** > **Scale Out** menu option on the left, and editing the **App Scale out** options. In the function app edit window, always ready instances are specific to that app.

### Prewarmed instances

The prewarmed instance count setting provides warmed instances as a buffer during HTTP scale and activation events. Prewarmed instances continue to buffer until the maximum scale-out limit is reached. The default prewarmed instance count is 1 and, for most scenarios, keep this value as 1.

Consider a less common scenario, such as an app running in a custom container. Because custom containers have a long warm-up time, you might consider increasing this buffer of prewarmed instances. A prewarmed instance becomes active only after all active instances are in use.

You can also define a warmup trigger that runs during the prewarming process. You can use a warmup trigger to preload custom dependencies during the prewarming process so your functions are ready to start processing requests immediately. To learn more, see [Azure Functions warmup trigger](functions-bindings-warmup).

Consider this example that shows how always ready instances and prewarmed instances work together. A premium function app has two always ready instances configured, and the default of one prewarmed instance.


- When the app is idle and no events are triggering, the app is provisioned and running with two instances. At this time, you're billed for the two always ready instances but aren't billed for a prewarmed instance because no prewarmed instance is allocated.
- As your application starts receiving HTTP traffic, requests are load balanced across the two always ready instances. As soon as those two instances start processing events, an instance is added to fill the prewarmed buffer. The app is now running with three provisioned instances: the two always ready instances, and the third prewarmed and inactive buffer. You're billed for the three instances.
- As load increases and your app needs more instances to handle HTTP traffic, that prewarmed instance swaps to an active instance. HTTP load is now routed to all three instances, and a fourth instance is instantly provisioned to fill the prewarmed buffer.
- This sequence of scaling and prewarming continues until the maximum instance count for the app is reached or load decreases causing the platform to scale back in after a period. No instances are prewarmed or activated beyond the maximum.

You can't change the prewarmed instance count setting in the portal. You must instead use the Azure CLI or Azure PowerShell.

### Maximum function app instances

In addition to the [plan maximum burst count](#plan-and-sku-settings), you can configure a per-app maximum. You configure the app maximum by using the [app scale limit](event-driven-scaling#limit-scale-out). The maximum app scale-out limit can't exceed the maximum burst instances of the plan.

## Private network connectivity

Function apps deployed to a Premium plan can take advantage of [virtual network integration for web apps](../app-service/overview-vnet-integration). When configured, your app can communicate with resources within your virtual network or secured via service endpoints. You can also use IP restrictions on the app to restrict incoming traffic.

When assigning a subnet to your function app in a Premium plan, you need a subnet with enough IP addresses for each potential instance. You need an IP block with at least 100 available addresses.

For more information, see [Integrate Azure Functions with a virtual network](functions-create-vnet).

## Rapid elastic scale

The same rapid scaling logic as the Flex Consumption and Consumption plans automatically adds more compute instances for your app. Apps in the same App Service Plan scale independently from one another based on the needs of an individual app. However, Functions apps in the same App Service Plan share VM resources to help reduce costs, when possible. The number of apps associated with a VM depends on the footprint of each app and the size of the VM.

To learn more about how scaling works, see [Event-driven scaling in Azure Functions](event-driven-scaling).

## Longer run duration

Functions in a Consumption plan are limited to 10 minutes for a single execution. In the Premium plan, the run duration defaults to 30 minutes to prevent runaway executions. However, you can [modify the host.json configuration](functions-host-json#functiontimeout) to make the duration unbounded for Premium plan apps, with the following limitations:

- Platform upgrades can trigger a managed shutdown and halt the function execution with a grace period of 10 minutes.
- An idle timer stops the worker after 60 minutes with no new executions.
[Scale-in behavior](event-driven-scaling#scale-in-behaviors)can cause worker shutdown after 60 minutes.[Slot swaps](functions-deployment-slots)can terminate executions on the source and target slots during the swap.

## Migration

If you have an existing function app, you can use Azure CLI commands to migrate your app between a Consumption plan and a Premium plan on Windows. The specific commands depend on the direction of the migration. For more information, see [Plan migration](functions-how-to-use-azure-function-app-settings#plan-migration).

This migration isn't supported on Linux.

## Premium plan settings

When you create the plan, you set two plan size settings: the minimum number of instances (or plan size) and the maximum burst limit.

If your app needs more instances beyond the always ready instances, it can continue to scale out until the number of instances reaches the plan maximum burst limit, or the app maximum scale-out limit if you set it. You pay for instances only while they're running and allocated to you, on a per-second basis. The platform makes its best effort at scaling your app out to the defined maximum limits.

You can configure the plan size in the Azure portal by selecting your **Function App** deployed to that plan, going to the **App Service plan** > **Scale Up** menu options on the left, and choosing a larger plan size. To increase the maximum burst limit, choose the **Scale Out** menu option and edit the **Plan Scale out** > **Maximum burst** option.

The minimum for every Premium plan is at least one instance. The actual minimum number of instances is determined based on the always ready instances requested by apps in the plan. For example, if app A requests five always ready instances, and app B requests two always ready instances in the same plan, the minimum plan size is determined as five. App A runs on all five instances, and app B runs on two.

Important

You're charged for each instance allocated in the minimum instance count whether or not functions are executing.

In most circumstances, this autocalculated minimum is sufficient. However, scaling beyond the minimum occurs at a best effort. It's possible, though unlikely, that at a specific time scale-out could be delayed if other instances are unavailable. By setting a minimum higher than the autocalculated minimum, you reserve instances in advance of scale-out.

You can configure the minimum instances in the Azure portal by selecting your **Function App** deployed to that plan, going to the **App Service plan** > **Scale Out** menu option on the left, and editing the **Plan Scale out** > **Minimum Instances** option.

### Available instance SKUs

When you create or scale your plan, choose from three instance sizes. You're billed for the total number of cores and memory you provision, per second for each instance allocated to you. Your app can automatically scale out to multiple instances as needed.

| SKU | Cores | Memory | Storage |
|---|---|---|---|
| EP1 | 1 | 3.5 GB | 250 GB |
| EP2 | 2 | 7 GB | 250 GB |
| EP3 | 4 | 14 GB | 250 GB |

### Memory usage considerations

Running on a machine with more memory doesn't always mean that your function app uses all available memory.

For example, a JavaScript function app is constrained by the default memory limit in Node.js. To increase this fixed memory limit, add the app setting `languageWorkers:node:arguments`

with a value of `--max-old-space-size=<max memory in MB>`

.

For plans with more than 4 GB of memory, set the Bitness Platform Setting to `64 Bit`

under [General settings](../app-service/configure-common#configure-general-settings).

## Region max scale-out

The following table lists currently supported maximum scale-out values for a single plan in each region and OS configuration:

| Region | Windows | Linux |
|---|---|---|
| Australia Central | 100 | 20 |
| Australia Central 2 | 100 | Not Available |
| Australia East | 100 | 40 |
| Australia Southeast | 100 | 20 |
| Brazil South | 100 | 20 |
| Canada Central | 100 | 100 |
| Central India | 100 | 20 |
| Central US | 100 | 100 |
| China East 2 | 20 | 20 |
| China North 2 | 20 | 20 |
| China North 3 | 20 | 20 |
| East Asia | 100 | 20 |
| East US | 100 | 100 |
| East US 2 | 80 | 100 |
| France Central | 100 | 60 |
| Germany West Central | 100 | 20 |
| Israel Central | 100 | 20 |
| Italy North | 100 | 20 |
| Japan East | 100 | 20 |
| Japan West | 100 | 20 |
| Jio India West | 100 | 20 |
| Korea Central | 100 | 20 |
| Korea South | 40 | 20 |
| Mexico Central | 20 | 20 |
| North Central US | 100 | 20 |
| North Europe | 100 | 100 |
| Norway East | 100 | 20 |
| South Africa North | 100 | 20 |
| South Africa West | 20 | 20 |
| South Central US | 100 | 100 |
| South India | 100 | Not Available |
| Southeast Asia | 100 | 20 |
| Spain Central | 20 | 20 |
| Switzerland North | 100 | 20 |
| Switzerland West | 100 | 20 |
| UAE North | 100 | 100 |
| UK South | 100 | 100 |
| UK West | 100 | 20 |
| USGov Arizona | 20 | 20 |
| USGov Texas | 20 | Not Available |
| USGov Virginia | 80 | 20 |
| West Central US | 100 | 20 |
| West Europe | 100 | 100 |
| West India | 100 | 20 |
| West US | 100 | 100 |
| West US 2 | 100 | 20 |
| West US 3 | 100 | 20 |

For more information, see [Products available by region](https://azure.microsoft.com/global-infrastructure/services/?products=functions).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr-output-state -->

# Dapr State output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Dapr state output binding allows you to save a value to a Dapr state during a function execution.

For information on setup and configuration details of the Dapr extension, see the [Dapr extension overview](functions-bindings-dapr).

## Example

A C# function can be created using one of the following C# modes:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).The following example demonstrates using the Dapr state output binding to persist a new state into the state store.

```
[FunctionName("StateOutputBinding")]
public static async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Function, "post", Route = "state/{key}")] HttpRequest req,
[DaprState("statestore", Key = "{key}")] IAsyncCollector<string> state,
ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
await state.AddAsync(requestBody);
return new OkResult();
}
```


The following example creates a `"CreateNewOrderHttpTrigger"`

function using the `DaprStateOutput`

binding with an `HttpTrigger`

:

```
@FunctionName("CreateNewOrderHttpTrigger")
public String run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@DaprStateOutput(
stateStore = "%StateStoreName%",
key = "product")
OutputBinding<String> product,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger (CreateNewOrderHttpTrigger) processed a request.");
}
```


In the following example, the Dapr state output binding is paired with an HTTP trigger, which is registered by the `app`

object:

```
const { app, trigger } = require('@azure/functions');
app.generic('StateOutputBinding', {
trigger: trigger.generic({
type: 'httpTrigger',
authLevel: 'anonymous',
methods: ['POST'],
route: "state/{key}",
name: "req"
}),
return: daprStateOutput,
handler: async (request, context) => {
context.log("Node HTTP trigger function processed a request.");
const payload = await request.text();
context.log(JSON.stringify(payload));
return { value : payload };
}
});
```


The following examples show Dapr triggers in a *function.json* file and PowerShell code that uses those bindings.

Here's the *function.json* file for `daprState`

output:

```
{
"bindings":
{
"type": "daprState",
"stateStore": "%StateStoreName%",
"direction": "out",
"name": "order",
"key": "order"
}
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

In code:

```
using namespace System
using namespace Microsoft.Azure.WebJobs
using namespace Microsoft.Extensions.Logging
using namespace Microsoft.Azure.WebJobs.Extensions.Dapr
using namespace Newtonsoft.Json.Linq
param (
$payload
)
# C# function processed a CreateNewOrder request from the Dapr Runtime.
Write-Host "PowerShell function processed a CreateNewOrder request from the Dapr Runtime."
# Payload must be of the format { "data": { "value": "some value" } }
# Convert the object to a JSON-formatted string with ConvertTo-Json
$jsonString = $payload| ConvertTo-Json
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name order -Value $payload["data"]
```


The following example shows a Dapr State output binding, which uses the [v2 Python programming model](functions-reference-python). To use `daprState`

in your Python function app code:

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="HttpTriggerFunc")
@app.route(route="req", auth_level=dapp.auth_level.ANONYMOUS)
@app.dapr_state_output(arg_name="state", state_store="statestore", key="newOrder")
def main(req: func.HttpRequest, state: func.Out[str] ) -> str:
# request body must be passed this way '{\"value\": { \"key\": \"some value\" } }'
body = req.get_body()
if body is not None:
state.set(body.decode('utf-8'))
logging.info(body.decode('utf-8'))
else:
logging.info('req body is none')
return 'ok'
```


## Attributes

In the [in-process model](functions-dotnet-class-library), use the `DaprState`

to define a Dapr state output binding, which supports these parameters:

| Parameter | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
StateStore |
The name of the state store to save state. | ✔️ | ❌ |
Key |
The name of the key to save state within the state store. | ✔️ | ✔️ |
Value |
Required. The value being stored. |
❌ | ✔️ |

## Annotations

The `DaprStateOutput`

annotation allows you to function access a state store.

| Element | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
stateStore |
The name of the state store to save state. | ✔️ | ❌ |
key |
The name of the key to save state within the state store. | ✔️ | ✔️ |
value |
Required. The value being stored. |
❌ | ✔️ |

## Configuration

The following table explains the binding configuration properties that you set in the code.

| Property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
stateStore |
The name of the state store to save state. | ✔️ | ❌ |
key |
The name of the key to save state within the state store. | ✔️ | ✔️ |
value |
Required. The value being stored. |
❌ | ✔️ |

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
stateStore |
The name of the state store to save state. | ✔️ | ❌ |
key |
The name of the key to save state within the state store. | ✔️ | ✔️ |
value |
Required. The value being stored. |
❌ | ✔️ |

The following table explains the binding configuration properties for `@dapp.dapr_state_output`

that you set in your Python code.

| Property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
stateStore |
The name of the state store to save state. | ✔️ | ❌ |
key |
The name of the key to save state within the state store. | ✔️ | ✔️ |
value |
Required. The value being stored. |
❌ | ✔️ |

If properties are defined in both Attributes and `RequestBody`

, priority is given to data provided in `RequestBody`

.

See the [Example section](#example) for complete examples.

## Usage

To use the Dapr state output binding, start by setting up a Dapr state store component. You can learn more about which component to use and how to set it up in the official Dapr documentation.

To use the `daprState`

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr-output -->

# Dapr Binding output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Dapr output binding allows you to send a value to a Dapr output binding during a function execution.

For information on setup and configuration details of the Dapr extension, see the [Dapr extension overview](functions-bindings-dapr).

## Example

A C# function can be created using one of the following C# modes:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).The following example demonstrates using a Dapr service invocation trigger and a Dapr output binding to read and process a binding request.

```
[FunctionName("SendMessageToKafka")]
public static async Task Run(
[DaprServiceInvocationTrigger] JObject payload,
[DaprBinding(BindingName = "%KafkaBindingName%", Operation = "create")] IAsyncCollector<object> messages,
ILogger log)
{
log.LogInformation("C# function processed a SendMessageToKafka request.");
await messages.AddAsync(payload);
}
```


The following example creates a `"SendMessageToKafka"`

function using the `DaprBindingOutput`

binding with the [ DaprServiceInvocationTrigger](functions-bindings-dapr-output):

```
@FunctionName("SendMessageToKafka")
public String run(
@DaprServiceInvocationTrigger(
methodName = "SendMessageToKafka")
String payload,
@DaprBindingOutput(
bindingName = "%KafkaBindingName%",
operation = "create")
OutputBinding<String> product,
final ExecutionContext context) {
context.getLogger().info("Java function processed a SendMessageToKafka request.");
product.setValue(payload);
return payload;
}
```


In the following example, the Dapr output binding is paired with the Dapr invoke output trigger, which is registered by the `app`

object:

```
const { app, trigger } = require('@azure/functions');
app.generic('SendMessageToKafka', {
trigger: trigger.generic({
type: 'daprServiceInvocationTrigger',
name: "payload"
}),
return: daprBindingOutput,
handler: async (request, context) => {
context.log("Node function processed a SendMessageToKafka request from the Dapr Runtime.");
context.log(context.triggerMetadata.payload)
return { "data": context.triggerMetadata.payload };
}
});
```


The following examples show Dapr triggers in a *function.json* file and PowerShell code that uses those bindings.

Here's the *function.json* file for `daprBinding`

:

```
{
"bindings":
{
"type": "daprBinding",
"direction": "out",
"bindingName": "%KafkaBindingName%",
"operation": "create",
"name": "messages"
}
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

In code:

```
using namespace System.Net
# Input bindings are passed in via param block.
param($req, $TriggerMetadata)
Write-Host "Powershell SendMessageToKafka processed a request."
$invoke_output_binding_req_body = @{
"data" = $req
}
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name messages -Value $invoke_output_binding_req_body
```


The following example shows a Dapr Binding output binding, which uses the [v2 Python programming model](functions-reference-python). To use `@dapp.dapr_binding_output`

in your Python function app code:

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="SendMessageToKafka")
@app.dapr_service_invocation_trigger(arg_name="payload", method_name="SendMessageToKafka")
@app.dapr_binding_output(arg_name="messages", binding_name="%KafkaBindingName%", operation="create")
def main(payload: str, messages: func.Out[bytes]) -> None:
logging.info('Python processed a SendMessageToKafka request from the Dapr Runtime.')
messages.set(json.dumps({"data": payload}).encode('utf-8'))
```


## Attributes

In the [in-process model](functions-dotnet-class-library), use the `DaprBinding`

to define a Dapr binding output binding, which supports these parameters:

| Parameter | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
BindingName |
The name of the Dapr binding. | ✔️ | ✔️ |
Operation |
The configured binding operation. | ✔️ | ✔️ |
Metadata |
The metadata namespace. | ❌ | ✔️ |
Data |
Required. The data for the binding operation. |
❌ | ✔️ |

## Annotations

The `DaprBindingOutput`

annotation allows you to create a function that sends an output binding.

| Element | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
bindingName |
The name of the Dapr binding. | ✔️ | ✔️ |
output |
The configured binding operation. | ✔️ | ✔️ |
metadata |
The metadata namespace. | ❌ | ✔️ |
data |
Required. The data for the binding operation. |
❌ | ✔️ |

## Configuration

The following table explains the binding configuration properties that you set in the code.

| Property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
bindingName |
The name of the binding. | ✔️ | ✔️ |
operation |
The binding operation. | ✔️ | ✔️ |
metadata |
The metadata namespace. | ❌ | ✔️ |
data |
Required. The data for the binding operation. |
❌ | ✔️ |

The following table explains the binding configuration properties that you set in the function.json file.

| function.json property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
bindingName |
The name of the binding. | ✔️ | ✔️ |
operation |
The binding operation. | ✔️ | ✔️ |
metadata |
The metadata namespace. | ❌ | ✔️ |
data |
Required. The data for the binding operation. |
❌ | ✔️ |

The following table explains the binding configuration properties for `@dapp.dapr_binding_output`

that you set in your Python code.

| Property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
binding_name |
The name of the binding event. | ✔️ | ✔️ |
operation |
The binding operation name/identifier. | ✔️ | ✔️ |
metadata |
The metadata namespace. | ❌ | ✔️ |
data |
Required. The data for the binding operation. |
❌ | ✔️ |

If properties are defined in both Attributes and `RequestBody`

, priority is given to data provided in `RequestBody`

.

See the [Example section](#example) for complete examples.

## Usage

To use the Dapr output binding, start by setting up a Dapr output binding component. You can learn more about which component to use and how to set it up in the official Dapr documentation.

[Dapr output binding component specs](https://docs.dapr.io/reference/components-reference/supported-bindings/)[How to: Use output bindings to interface with external resources](https://docs.dapr.io/developing-applications/building-blocks/bindings/howto-bindings/)

To use the `daprBinding`

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-mysql-input -->

# Azure Database for MySQL input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When a function runs, the Azure Database for MySQL input binding retrieves data from a database and passes it to the input parameter of the function.

For information on setup and configuration, see the [overview](functions-bindings-azure-mysql).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

## Examples

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

More samples for the Azure Database for MySQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples).

This section contains the following examples:

[HTTP trigger, get a row by ID from a query string](#http-trigger-look-up-id-from-query-string-c-oop)[HTTP trigger, get multiple rows from route data](#http-trigger-get-multiple-items-from-route-data-c-oop)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-c-oop)

The examples refer to a `Product`

class and a corresponding database table:

```
namespace AzureMySqlSamples.Common
{
public class Product
{
public int? ProductId { get; set; }
public string Name { get; set; }
public int Cost { get; set; }
public override bool Equals(object obj)
}
}
```


```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


### HTTP trigger, get a row by ID from a query string

The following example shows a C# function that retrieves a single record. The function is [triggered by an HTTP request](functions-bindings-http-webhook-trigger) that uses a query string to specify the ID. That ID is used to retrieve a `Product`

record with the specified query.

Note

The HTTP query string parameter is case-sensitive.

```
using System.Collections.Generic;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.MySql;
using Microsoft.Azure.Functions.Worker.Http;
using AzureMySqlSamples.Common;
namespace AzureMySqlSamples.InputBindingIsolatedSamples
{
public static class GetProductById
{
[Function(nameof(GetProductById))]
public static IEnumerable<Product> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "getproducts/{productId}")]
HttpRequestData req,
[MySqlInput("select * from Products where ProductId = @productId",
"MySqlConnectionString",
parameters: "@ProductId={productId}")]
IEnumerable<Product> products)
{
return products;
}
}
}
```


### HTTP trigger, get multiple rows from a route parameter

The following example shows a [C# function](functions-dotnet-class-library) that retrieves rows that the query returned. The function is [triggered by an HTTP request](functions-bindings-http-webhook-trigger) that uses route data to specify the value of a query parameter. That parameter is used to filter the `Product`

records in the specified query.

```
using System.Collections.Generic;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.MySql;
using Microsoft.Azure.Functions.Worker.Http;
using AzureMySqlSamples.Common;
namespace AzureMySqlSamples.InputBindingIsolatedSamples
{
public static class GetProducts
{
[Function(nameof(GetProducts))]
public static IEnumerable<Product> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "getproducts")]
HttpRequestData req,
[MySqlInput("select * from Products",
"MySqlConnectionString")]
IEnumerable<Product> products)
{
return products;
}
}
}
```


### HTTP trigger, delete rows

The following example shows a [C# function](functions-dotnet-class-library) that executes a stored procedure with input from the HTTP request's query parameter.

The stored procedure `DeleteProductsCost`

must be created on the MySQL database. In this example, the stored procedure deletes a single record or all records, depending on the value of the parameter.

```
DROP PROCEDURE IF EXISTS DeleteProductsCost;
Create Procedure DeleteProductsCost(cost INT)
BEGIN
DELETE from Products where Products.cost = cost;
END
```


```
namespace AzureMySqlSamples.InputBindingSamples
{
public static class GetProductsStoredProcedure
{
[FunctionName(nameof(GetProductsStoredProcedure))]
public static IActionResult Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "getproducts-storedprocedure/{cost}")]
HttpRequest req,
[MySql("DeleteProductsCost",
"MySqlConnectionString",
commandType: System.Data.CommandType.StoredProcedure,
parameters: "@Cost={cost}")]
IEnumerable<Product> products)
{
return new OkObjectResult(products);
}
}
}
```


More samples for the Azure Database for MySQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-java).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-java)[HTTP trigger, get a row by ID from a query string](#http-trigger-look-up-id-from-query-string-java)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-java)

The examples refer to a `Product`

class and a corresponding database table:

```
package com.function.Common;
import com.fasterxml.jackson.annotation.JsonProperty;
public class Product {
@JsonProperty("ProductId")
private int ProductId;
@JsonProperty("Name")
private String Name;
@JsonProperty("Cost")
private int Cost;
public Product() {
}
```


```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


### HTTP trigger, get multiple rows

The following example shows an Azure Database for MySQL input binding in a Java function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query and returns the results in the HTTP response.

```
package com.function;
import com.function.Common.Product;
import com.microsoft.azure.functions.HttpMethod;
import com.microsoft.azure.functions.HttpRequestMessage;
import com.microsoft.azure.functions.HttpResponseMessage;
import com.microsoft.azure.functions.HttpStatus;
import com.microsoft.azure.functions.annotation.AuthorizationLevel;
import com.microsoft.azure.functions.annotation.FunctionName;
import com.microsoft.azure.functions.annotation.HttpTrigger;
import com.microsoft.azure.functions.mysql.annotation.CommandType;
import com.microsoft.azure.functions.mysql.annotation.MySqlInput;
import java.util.Optional;
public class GetProducts {
@FunctionName("GetProducts")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "getproducts}")
HttpRequestMessage<Optional<String>> request,
@MySqlInput(
name = "products",
commandText = "SELECT * FROM Products",
commandType = CommandType.Text,
connectionStringSetting = "MySqlConnectionString")
Product[] products) {
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(products).build();
}
}
```


### HTTP trigger, get a row by ID from a query string

The following example shows an Azure Database for MySQL input binding in a Java function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query filtered by a parameter from the query string and returns the row in the HTTP response.

```
public class GetProductById {
@FunctionName("GetProductById")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "getproducts/{productid}")
HttpRequestMessage<Optional<String>> request,
@MySqlInput(
name = "products",
commandText = "SELECT * FROM Products WHERE ProductId= @productId",
commandType = CommandType.Text,
parameters = "@productId={productid}",
connectionStringSetting = "MySqlConnectionString")
Product[] products) {
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(products).build();
}
}
```


### HTTP trigger, delete rows

The following example shows an Azure Database for MySQL input binding in a Java function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding executes a stored procedure with input from the HTTP request's query parameter.

The stored procedure `DeleteProductsCost`

must be created on the database. In this example, the stored procedure deletes a single record or all records, depending on the value of the parameter.

```
DROP PROCEDURE IF EXISTS DeleteProductsCost;
Create Procedure DeleteProductsCost(cost INT)
BEGIN
DELETE from Products where Products.cost = cost;
END
```


```
public class DeleteProductsStoredProcedure {
@FunctionName("DeleteProductsStoredProcedure")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "Deleteproducts-storedprocedure/{cost}")
HttpRequestMessage<Optional<String>> request,
@MySqlInput(
name = "products",
commandText = "DeleteProductsCost",
commandType = CommandType.StoredProcedure,
parameters = "@Cost={cost}",
connectionStringSetting = "MySqlConnectionString")
Product[] products) {
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(products).build();
}
}
```


More samples for the Azure Database for MySQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-js).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-javascript)[HTTP trigger, get a row by ID from a query string](#http-trigger-look-up-id-from-query-string-javascript)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-javascript)

The examples refer to a database table:

```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


### HTTP trigger, get multiple rows

The following example shows an Azure Database for MySQL input binding that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query and returns the results in the HTTP response.

```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const mysqlInput = input.generic({
commandText: 'select * from Products',
commandType: 'Text',
connectionStringSetting: 'MySqlConnectionString',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log('HTTP trigger and MySQL input binding function processed a request.');
const products = context.extraInputs.get(mysqlInput);
return {
jsonBody: products,
};
}
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraInputs: [mysqlInput],
handler: httpTrigger1,
});
```


```
const { app, input } = require('@azure/functions');
const mysqlInput = input.generic({
type: 'mysql',
commandText: 'select * from Products where Cost = @Cost',
parameters: '@Cost={Cost}',
commandType: 'Text',
connectionStringSetting: 'MySqlConnectionString'
})
app.http('GetProducts', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
route: 'getproducts/{cost}',
extraInputs: [mysqlInput],
handler: async (request, context) => {
const products = JSON.stringify(context.extraInputs.get(mysqlInput));
return {
status: 200,
body: products
};
}
});
```


### HTTP trigger, get a row by ID from a query string

The following example shows an Azure Database for MySQL input binding that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query filtered by a parameter from the query string and returns the row in the HTTP response.

```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const mysqlInput = input.generic({
commandText: 'select * from Products where ProductId= @productId',
commandType: 'Text',
parameters: '@productId={productid}',
connectionStringSetting: 'MySqlConnectionString',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log('HTTP trigger and MySQL input binding function processed a request.');
const products = context.extraInputs.get(mysqlInput);
return {
jsonBody: products,
};
}
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraInputs: [mysqlInput],
handler: httpTrigger1,
});
```


```
const { app, input } = require('@azure/functions');
const mysqlInput = input.generic({
type: 'mysql',
commandText: 'select * from Products where ProductId= @productId',
commandType: 'Text',
parameters: '@productId={productid}',
connectionStringSetting: 'MySqlConnectionString'
})
app.http('GetProducts', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
route: 'getproducts/{productid}',
extraInputs: [mysqlInput],
handler: async (request, context) => {
const products = JSON.stringify(context.extraInputs.get(mysqlInput));
return {
status: 200,
body: products
};
}
});
```


### HTTP trigger, delete rows

The following example shows an Azure Database for MySQL input binding that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding executes a stored procedure with input from the HTTP request's query parameter.

The stored procedure `DeleteProductsCost`

must be created on the database. In this example, the stored procedure deletes a single record or all records, depending on the value of the parameter.

```
DROP PROCEDURE IF EXISTS DeleteProductsCost;
Create Procedure DeleteProductsCost(cost INT)
BEGIN
DELETE from Products where Products.cost = cost;
END
```


```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const mysqlInput = input.generic({
commandText: 'DeleteProductsCost',
commandType: 'StoredProcedure',
parameters: '@Cost={cost}',
connectionStringSetting: 'MySqlConnectionString',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log('HTTP trigger and MySQL input binding function processed a request.');
const products = context.extraInputs.get(mysqlInput);
return {
jsonBody: products,
};
}
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraInputs: [mysqlInput],
handler: httpTrigger1,
});
```


```
const { app, input } = require('@azure/functions');
const mysqlInput = input.generic({
type: 'mysql',
commandText: 'DeleteProductsCost',
commandType: 'StoredProcedure',
parameters: '@Cost={cost}',
connectionStringSetting: 'MySqlConnectionString'
})
app.http('httpTrigger1', {
methods: ['POST'],
authLevel: 'anonymous',
route: 'DeleteProductsByCost',
extraInputs: [mysqlInput],
handler: async (request, context) => {
const products = JSON.stringify(context.extraInputs.get(mysqlInput));
return {
status: 200,
body: products
};
}
});
```


More samples for the Azure Database for MySQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-powershell).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-powershell)[HTTP trigger, get a row by ID from a query string](#http-trigger-look-up-id-from-query-string-powershell)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-powershell)

The examples refer to a database table:

```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


### HTTP trigger, get multiple rows

The following example shows an Azure Database for MySQL input binding in a function.json file and a PowerShell function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query and returns the results in the HTTP response.

The following example is binding data in the function.json file:

```
{
"bindings": [
{
"authLevel": "function",
"name": "Request",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get"
],
"route": "getproducts/{cost}"
},
{
"name": "response",
"type": "http",
"direction": "out"
},
{
"name": "products",
"type": "mysql",
"direction": "in",
"commandText": "select * from Products",
"commandType": "Text",
"connectionStringSetting": "MySqlConnectionString"
}
],
"disabled": false
}
```


The [Configuration](#configuration) section explains these properties.

The following example is sample PowerShell code for the function in the run.ps1 file:

```
using namespace System.Net
param($Request, $TriggerMetadata, $products)
Write-Host "PowerShell function with MySql Input Binding processed a request."
Push-OutputBinding -Name response -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = $products
})
```


### HTTP trigger, get a row by ID from a query string

The following example shows an Azure Database for MySQL input binding in a PowerShell function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query filtered by a parameter from the query string and returns the row in the HTTP response.

The following example is binding data in the function.json file:

```
{
"bindings": [
{
"authLevel": "function",
"name": "Request",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get"
],
"route": "getproducts/{productid}"
},
{
"name": "response",
"type": "http",
"direction": "out"
},
{
"name": "products",
"type": "mysql",
"direction": "in",
"commandText": "select * from Products where ProductId= @productId",
"commandType": "Text",
"parameters": "MySqlConnectionString",
"connectionStringSetting": "MySqlConnectionString"
}
],
"disabled": false
}
```


The [Configuration](#configuration) section explains these properties.

The following example is sample PowerShell code for the function in the run.ps1 file:

```
using namespace System.Net
param($Request, $TriggerMetadata, $products)
Write-Host "PowerShell function with MySql Input Binding processed a request."
Push-OutputBinding -Name response -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = $products
})
```


### HTTP trigger, delete rows

The following example shows an Azure Database for MySQL input binding in a function.json file and a PowerShell function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding executes a stored procedure with input from the HTTP request's query parameter.

The stored procedure `DeleteProductsCost`

must be created on the database. In this example, the stored procedure deletes a single record or all records, depending on the value of the parameter.

```
DROP PROCEDURE IF EXISTS DeleteProductsCost;
Create Procedure DeleteProductsCost(cost INT)
BEGIN
DELETE from Products where Products.cost = 'cost';
END
```


```
{
"bindings": [
{
"authLevel": "function",
"name": "Request",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get"
],
"route": "deleteproducts-storedprocedure/{cost}"
},
{
"name": "response",
"type": "http",
"direction": "out"
},
{
"name": "products",
"type": "mysql",
"direction": "in",
"commandText": "DeleteProductsCost",
"commandType": "StoredProcedure",
"parameters": "@Cost={cost}",
"connectionStringSetting": "MySqlConnectionString"
}
],
"disabled": false
}
```


The [Configuration](#configuration) section explains these properties.

The following example is sample PowerShell code for the function in the run.ps1 file:

```
using namespace System.Net
param($Request, $TriggerMetadata, $products)
Write-Host "PowerShell function with MySql Input Binding processed a request."
Push-OutputBinding -Name response -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = $products
}
```


More samples for the Azure Database for MySQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-python).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-python)[HTTP trigger, get a row by ID from a query string](#http-trigger-look-up-id-from-query-string-python)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-python)

The examples refer to a database table:

```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


Note

You must use Azure Functions version 1.22.0b4 for Python.

### HTTP trigger, get multiple rows

The following example shows an Azure Database for MySQL input binding in a function.json file and a Python function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query and returns the results in the HTTP response.

The following example is sample Python code for the function_app.py file:

```
import azure.functions as func
import datetime
import json
import logging
app = func.FunctionApp()
@app.generic_trigger(arg_name="req", type="httpTrigger", route="getproducts/{cost}")
@app.generic_output_binding(arg_name="$return", type="http")
@app.generic_input_binding(arg_name="products", type="mysql",
commandText= "select * from Products",
command_type="Text",
connection_string_setting="MySqlConnectionString")
def mysql_test(req: func.HttpRequest, products: func.MySqlRowList) -> func.HttpResponse:
rows = list(map(lambda r: json.loads(r.to_json()), products))
return func.HttpResponse(
json.dumps(rows),
status_code=200,
mimetype="application/json"
)
```


### HTTP trigger, get a row by ID from a query string

The following example shows an Azure Database for MySQL input binding in a Python function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query filtered by a parameter from the query string and returns the row in the HTTP response.

The following example is sample Python code for the function_app.py file:

```
import azure.functions as func
import datetime
import json
import logging
app = func.FunctionApp()
@app.generic_trigger(arg_name="req", type="httpTrigger", route="getproducts/{cost}")
@app.generic_output_binding(arg_name="$return", type="http")
@app.generic_input_binding(arg_name="products", type="mysql",
commandText= "select * from Products where ProductId= @productId",
command_type="Text",
parameters= "@productId={productid}",
connection_string_setting="MySqlConnectionString")
def mysql_test(req: func.HttpRequest, products: func.MySqlRowList) -> func.HttpResponse:
rows = list(map(lambda r: json.loads(r.to_json()), products))
return func.HttpResponse(
json.dumps(rows),
status_code=200,
mimetype="application/json"
)
```


### HTTP trigger, delete rows

The following example shows an Azure Database for MySQL input binding in a function.json file and a Python function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding executes a stored procedure with input from the HTTP request's query parameter.

The stored procedure `DeleteProductsCost`

must be created on the database. In this example, the stored procedure deletes a single record or all records, depending on the value of the parameter.

```
DROP PROCEDURE IF EXISTS DeleteProductsCost;
Create Procedure DeleteProductsCost(cost INT)
BEGIN
DELETE from Products where Products.cost = cost;
END
```


The following example is sample Python code for the function_app.py file:

```
import azure.functions as func
import datetime
import json
import logging
app = func.FunctionApp()
@app.generic_trigger(arg_name="req", type="httpTrigger", route="getproducts/{cost}")
@app.generic_output_binding(arg_name="$return", type="http")
@app.generic_input_binding(arg_name="products", type="mysql",
commandText= "DeleteProductsCost",
command_type="StoredProcedure",
parameters= "@Cost={cost}",
connection_string_setting="MySqlConnectionString")
def mysql_test(req: func.HttpRequest, products: func.MySqlRowList) -> func.HttpResponse:
rows = list(map(lambda r: json.loads(r.to_json()), products))
return func.HttpResponse(
json.dumps(rows),
status_code=200,
mimetype="application/json"
)
```


## Attributes

The [C# library](functions-dotnet-class-library) uses the `MySqlAttribute`

attribute to declare the MySQL bindings on the function. The attribute has the following properties:

| Attribute property | Description |
|---|---|
`CommandText` |
Required. The MySQL query command or name of the stored procedure that the binding executes. |
`ConnectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is executed. This value isn't the actual connection string and must instead resolve to an environment variable name. |
`CommandType` |
Required. A
`CommandType` |

[for a query and](/en-us/dotnet/api/system.data.commandtype#fields)

`Text`

[for a stored procedure.](/en-us/dotnet/api/system.data.commandtype#fields)

`StoredProcedure`

`Parameters`

`@param1=param1,@param2=param2`

. The parameter name and parameter value can't contain a comma (`,`

) or an equal sign (`=`

).## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@MySQLInput`

annotation on parameters whose values would come from Azure Database for MySQL. This annotation supports the following elements:

| Element | Description |
|---|---|
`commandText` |
Required. The MySQL query command or name of the stored procedure that the binding executes. |
`connectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is executed. This value isn't the actual connection string and must instead resolve to an environment variable name. |
`commandType` |
Required. A
`CommandType` |

[for a query and](/en-us/dotnet/api/system.data.commandtype#fields)

`Text`

[for a stored procedure.](/en-us/dotnet/api/system.data.commandtype#fields)

`StoredProcedure`

`name`

`parameters`

`@param1=param1,@param2=param2`

. The parameter name and parameter value can't contain a comma (`,`

) or an equal sign (`=`

).## Configuration

The following table explains the properties that you can set on the `options`

object passed to the `input.generic()`

method:

| Property | Description |
|---|---|
`commandText` |
Required. The MySQL query command or name of the stored procedure that the binding executes. |
`connectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is executed. This value isn't the actual connection string and must instead resolve to an environment variable name. Optional keywords in the connection string value are
|

`commandType`

[value, which is](/en-us/dotnet/api/system.data.commandtype)`CommandType`

[for a query and](/en-us/dotnet/api/system.data.commandtype#fields)`Text`

[for a stored procedure.](/en-us/dotnet/api/system.data.commandtype#fields)`StoredProcedure`

`parameters`

`@param1=param1,@param2=param2`

. The parameter name and parameter value can't contain a comma (`,`

) or an equal sign (`=`

).## Configuration

The following table explains the binding configuration properties that you set in the function.json file:

| Property | Description |
|---|---|
`type` |
Required. Must be set to `mysql` . |
`direction` |
Required. Must be set to `in` . |
`name` |
Required. The name of the variable that represents the query results in function code. |
`commandText` |
Required. The MySQL query command or name of the stored procedure that the binding executes. |
`connectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is executed. This value isn't the actual connection string and must instead resolve to an environment variable name. Optional keywords in the connection string value are
|

`commandType`

[value, which is](/en-us/dotnet/api/system.data.commandtype)`CommandType`

[for a query and](/en-us/dotnet/api/system.data.commandtype#fields)`Text`

[for a stored procedure.](/en-us/dotnet/api/system.data.commandtype#fields)`StoredProcedure`

`parameters`

`@param1=param1,@param2=param2`

. The parameter name and parameter value can't contain a comma (`,`

) or an equal sign (`=`

).When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

The attribute's constructor takes the MySQL command text, the command type, parameters, and the name of the connection string setting. The command can be a MySQL query with the command type `System.Data.CommandType.Text`

or a stored procedure name with the command type `System.Data.CommandType.StoredProcedure`

. The name of the connection string setting corresponds to the application setting (in local.settings.json for local development) that contains the [connection string](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html) to Azure Database for MySQL.

If an exception occurs when an Azure Database for MySQL input binding is executed, the function code stops running. The result might be an error code, such as an HTTP trigger that returns a 500 error code.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-reference-node -->

# Azure Functions Node.js developer guide

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This guide is an introduction to developing Azure Functions using JavaScript or TypeScript. The article assumes that you have already read the [Azure Functions developer guide](functions-reference).

Important

The content of this article changes based on your choice of the Node.js programming model in the selector at the top of this page. The version you choose should match the version of the [ @azure/functions](https://www.npmjs.com/package/@azure/functions) npm package you're using in your app. If you don't have that package listed in your

`package.json`

, the default is v3. Learn more about the differences between v3 and v4 in the [migration guide](functions-node-upgrade-v4).

As a Node.js developer, you might also be interested in one of the following articles:

| Getting started | Concepts | Guided learning |
|---|---|---|

## Considerations

- The Node.js programming model shouldn't be confused with the Azure Functions runtime:
**Programming model**: Defines how you author your code and is specific to JavaScript and TypeScript.**Runtime**: Defines underlying behavior of Azure Functions and is shared across all languages.

- The version of the programming model is strictly tied to the version of the
npm package. It's versioned independently of the`@azure/functions`

[runtime](functions-versions). Both the runtime and the programming model use the number 4 as their latest major version, but that's a coincidence. - You can't mix the v3 and v4 programming models in the same function app. As soon as you register one v4 function in your app, any v3 functions registered in
*function.json*files are ignored.

## Supported versions

The following table shows each version of the Node.js programming model along with its supported versions of the Azure Functions runtime and Node.js.

|
|---|

[Functions Runtime Version](functions-versions)

[Node.js Version](https://github.com/nodejs/release#release-schedule)

[Functions Versions](functions-versions)for more info.[Functions Versions](functions-versions)for more info.## Folder structure

The required folder structure for a JavaScript project looks like the following example:

```
<project_root>/
| - .vscode/
| - node_modules/
| - myFirstFunction/
| | - index.js
| | - function.json
| - mySecondFunction/
| | - index.js
| | - function.json
| - .funcignore
| - host.json
| - local.settings.json
| - package.json
```


The main project folder, *<project_root>*, can contain the following files:

**.vscode/**: (Optional) Contains the stored Visual Studio Code configuration. To learn more, see[Visual Studio Code settings](https://code.visualstudio.com/docs/getstarted/settings).**myFirstFunction/function.json**: Contains configuration for the function's trigger, inputs, and outputs. The name of the directory determines the name of your function.**myFirstFunction/index.js**: Stores your function code. To change this default file path, see[using scriptFile](#using-scriptfile).**.funcignore**: (Optional) Declares files that shouldn't get published to Azure. Usually, this file contains*.vscode/*to ignore your editor setting,*test/*to ignore test cases, and*local.settings.json*to prevent local app settings being published.**host.json**: Contains configuration options that affect all functions in a function app instance. This file does get published to Azure. Not all options are supported when running locally. To learn more, see[host.json](functions-host-json).**local.settings.json**: Used to store app settings and connection strings when it's running locally. This file doesn't get published to Azure. To learn more, see[local.settings.file](functions-develop-local#local-settings-file).**package.json**: Contains configuration options like a list of package dependencies, the main entrypoint, and scripts.

The recommended folder structure for a JavaScript project looks like the following example:

```
<project_root>/
| - .vscode/
| - node_modules/
| - src/
| | - functions/
| | | - myFirstFunction.js
| | | - mySecondFunction.js
| - test/
| | - functions/
| | | - myFirstFunction.test.js
| | | - mySecondFunction.test.js
| - .funcignore
| - host.json
| - local.settings.json
| - package.json
```


The main project folder, *<project_root>*, can contain the following files:

**.vscode/**: (Optional) Contains the stored Visual Studio Code configuration. To learn more, see[Visual Studio Code settings](https://code.visualstudio.com/docs/getstarted/settings).**src/functions/**: The default location for all functions and their related triggers and bindings.**test/**: (Optional) Contains the test cases of your function app.**.funcignore**: (Optional) Declares files that shouldn't get published to Azure. Usually, this file contains*.vscode/*to ignore your editor setting,*test/*to ignore test cases, and*local.settings.json*to prevent local app settings being published.**host.json**: Contains configuration options that affect all functions in a function app instance. This file does get published to Azure. Not all options are supported when running locally. To learn more, see[host.json](functions-host-json).**local.settings.json**: Used to store app settings and connection strings when it's running locally. This file doesn't get published to Azure. To learn more, see[local.settings.file](functions-develop-local#local-settings-file).**package.json**: Contains configuration options like a list of package dependencies, the main entrypoint, and scripts.

## Registering a function

The v3 model registers a function based on the existence of two files. First, you need a `function.json`

file located in a folder one level down from the root of your app. Second, you need a JavaScript file that [exports](https://nodejs.org/api/modules.html#modules_module_exports) your function. By default, the model looks for an `index.js`

file in the same folder as your `function.json`

. If you're using TypeScript, you must use the [ scriptFile](#using-scriptfile) property in

`function.json`

to point to the compiled JavaScript file. To customize the file location or export name of your function, see [configuring your function's entry point](functions-reference-node#configure-function-entry-point).

The function you export should always be declared as an [ async function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) in the v3 model. You can export a synchronous function, but then you must call

[to signal that your function is completed, which is deprecated and not recommended.](#contextdone)

`context.done()`

Your function is passed an [invocation context](#invocation-context) as the first argument and your

[inputs](#inputs)as the remaining arguments.

The following example is a simple function that logs that it was triggered and responds with `Hello, world!`

:

```
{
"bindings": [
{
"type": "httpTrigger",
"direction": "in",
"name": "req",
"authLevel": "anonymous",
"methods": ["get", "post"]
},
{
"type": "http",
"direction": "out",
"name": "res"
}
]
}
```


```
module.exports = async function (context, request) {
context.log("Http function was triggered.");
context.res = { body: "Hello, world!" };
};
```


The programming model loads your functions based on the `main`

field in your `package.json`

. You can set the `main`

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

In order to register a function, you must import the `app`

object from the `@azure/functions`

npm module and call the method specific to your trigger type. The first argument when registering a function is the function name. The second argument is an `options`

object specifying configuration for your trigger, your handler, and any other inputs or outputs. In some cases where trigger configuration isn't necessary, you can pass the handler directly as the second argument instead of an `options`

object.

Registering a function can be done from any file in your project, as long as that file is loaded (directly or indirectly) based on the `main`

field in your `package.json`

file. The function should be registered at a global scope because you can't register functions once executions start.

The following example is a simple function that logs that it was triggered and responds with `Hello, world!`

:

```
const { app } = require("@azure/functions");
app.http("helloWorld1", {
methods: ["POST", "GET"],
handler: async (request, context) => {
context.log("Http function was triggered.");
return { body: "Hello, world!" };
},
});
```


## Inputs and outputs

Your function is required to have exactly one primary input called the trigger. It might also have secondary inputs and/or outputs. Inputs and outputs are configured in your `function.json`

files and are also referred to as [bindings](functions-triggers-bindings).

### Inputs

Inputs are bindings with `direction`

set to `in`

. The main difference between a trigger and a secondary input is that the `type`

for a trigger ends in `Trigger`

, for example type [ blobTrigger](functions-bindings-storage-blob-trigger) vs type

[. Most functions only use a trigger, and not many secondary input types are supported.](functions-bindings-storage-blob-input)

`blob`

Inputs can be accessed in several ways:

Use the arguments in the same order that they're defined in*[Recommended]*As arguments passed to your function:`function.json`

. The`name`

property defined in`function.json`

doesn't need to match the name of your argument, although we recommend it for the sake of organization.`module.exports = async function (context, myTrigger, myInput, myOtherInput) { ... };`


**As properties of**Use the key matching the:`context.bindings`

`name`

property defined in`function.json`

.`module.exports = async function (context) { context.log("This is myTrigger: " + context.bindings.myTrigger); context.log("This is myInput: " + context.bindings.myInput); context.log("This is myOtherInput: " + context.bindings.myOtherInput); };`


### Outputs

Outputs are bindings with `direction`

set to `out`

and can be set in several ways:

If you're using an async function, you can return the value directly. You must change the*[Recommended for single output]*Return the value directly:`name`

property of the output binding to`$return`

in`function.json`

like in the following example:`{ "name": "$return", "type": "http", "direction": "out" }`

`module.exports = async function (context, request) { return { body: "Hello, world!", }; };`


If you're using an async function, you can return an object with a property matching the name of each binding in your*[Recommended for multiple outputs]*Return an object containing all outputs:`function.json`

. The following example uses output bindings named "httpResponse" and "queueOutput":`{ "name": "httpResponse", "type": "http", "direction": "out" }, { "name": "queueOutput", "type": "queue", "direction": "out", "queueName": "helloworldqueue", "connection": "storage_APPSETTING" }`

`module.exports = async function (context, request) { let message = "Hello, world!"; return { httpResponse: { body: message, }, queueOutput: message, }; };`


**Set values on**If you're not using an async function or you don't want to use the previous options, you can set values directly on`context.bindings`

:`context.bindings`

, where the key matches the name of the binding. The following example uses output bindings named "httpResponse" and "queueOutput":`{ "name": "httpResponse", "type": "http", "direction": "out" }, { "name": "queueOutput", "type": "queue", "direction": "out", "queueName": "helloworldqueue", "connection": "storage_APPSETTING" }`

`module.exports = async function (context, request) { let message = "Hello, world!"; context.bindings.httpResponse = { body: message, }; context.bindings.queueOutput = message; };`


### Bindings data type

You can use the `dataType`

property on an input binding to change the type of your input. However, the approach has some limitations:

- In Node.js, only
`string`

and`binary`

are supported (`stream`

isn't) - For HTTP inputs, the
`dataType`

property is ignored. Instead, use properties on the`request`

object to get the body in your desired format. For more information, see[HTTP request](#http-request).

In the following example of a [storage queue trigger](functions-bindings-storage-queue-trigger), the default type of `myQueueItem`

is a `string`

, but if you set `dataType`

to `binary`

, the type changes to a Node.js `Buffer`

.

```
{
"name": "myQueueItem",
"type": "queueTrigger",
"direction": "in",
"queueName": "helloworldqueue",
"connection": "storage_APPSETTING",
"dataType": "binary"
}
```


```
const { Buffer } = require("node:buffer");
module.exports = async function (context, myQueueItem) {
if (typeof myQueueItem === "string") {
context.log("myQueueItem is a string");
} else if (Buffer.isBuffer(myQueueItem)) {
context.log("myQueueItem is a buffer");
}
};
```


Your function is required to have exactly one primary input called the trigger. It might also have secondary inputs, a primary output called the return output, and/or secondary outputs. Inputs and outputs are also referred to as [bindings](functions-triggers-bindings) outside the context of the Node.js programming model. Before v4 of the model, these bindings were configured in `function.json`

files.

### Trigger input

The trigger is the only required input or output. For most trigger types, you register a function by using a method on the `app`

object named after the trigger type. You can specify configuration specific to the trigger directly on the `options`

argument. For example, an HTTP trigger allows you to specify a route. During execution, the value corresponding to this trigger is passed in as the first argument to your handler.

```
const { app } = require('@azure/functions');
app.http('helloWorld1', {
route: 'hello/world',
handler: async (request, context) => {
...
}
});
```


### Return output

The return output is optional, and in some cases configured by default. For example, an HTTP trigger registered with `app.http`

is configured to return an HTTP response output automatically. For most output types, you specify the return configuration on the `options`

argument with the help of the `output`

object exported from the `@azure/functions`

module. During execution, you set this output by returning it from your handler.

The following example uses a [timer trigger](functions-bindings-timer) and a [storage queue output](functions-bindings-storage-queue-output):

```
const { app, output } = require('@azure/functions');
app.timer('timerTrigger1', {
schedule: '0 */5 * * * *',
return: output.storageQueue({
connection: 'storage_APPSETTING',
...
}),
handler: (myTimer, context) => {
return { hello: 'world' }
}
});
```


### Extra inputs and outputs

In addition to the trigger and return, you might specify extra inputs or outputs on the `options`

argument when registering a function. The `input`

and `output`

objects exported from the `@azure/functions`

module provide type-specific methods to help construct the configuration. During execution, you get or set the values with `context.extraInputs.get`

or `context.extraOutputs.set`

, passing in the original configuration object as the first argument.

The following example is a function triggered by a [storage queue](functions-bindings-storage-queue-trigger), with an extra [storage blob input](functions-bindings-storage-blob-input) that is copied to an extra [storage blob output](functions-bindings-storage-blob-output). The queue message should be the name of a file and replaces `{queueTrigger}`

as the blob name to be copied, with the help of a [binding expression](functions-bindings-expressions-patterns).

```
const { app, input, output } = require("@azure/functions");
const blobInput = input.storageBlob({
connection: "storage_APPSETTING",
path: "helloworld/{queueTrigger}",
});
const blobOutput = output.storageBlob({
connection: "storage_APPSETTING",
path: "helloworld/{queueTrigger}-copy",
});
app.storageQueue("copyBlob1", {
queueName: "copyblobqueue",
connection: "storage_APPSETTING",
extraInputs: [blobInput],
extraOutputs: [blobOutput],
handler: (queueItem, context) => {
const blobInputValue = context.extraInputs.get(blobInput);
context.extraOutputs.set(blobOutput, blobInputValue);
},
});
```


### Generic inputs and outputs

The `app`

, `trigger`

, `input`

, and `output`

objects exported by the `@azure/functions`

module provide type-specific methods for most types. For all the types that aren't supported, a `generic`

method is provided to allow you to manually specify the configuration. The `generic`

method can also be used if you want to change the default settings provided by a type-specific method.

The following example is a simple HTTP triggered function using generic methods instead of type-specific methods.

```
const { app, output, trigger } = require("@azure/functions");
app.generic("helloWorld1", {
trigger: trigger.generic({
type: "httpTrigger",
methods: ["GET", "POST"],
}),
return: output.generic({
type: "http",
}),
handler: async (request, context) => {
context.log(`Http function processed request for url "${request.url}"`);
return { body: `Hello, world!` };
},
});
```


## SDK types

Several binding extensions now enable you to work directly with the Azure SDK types.

### Azure Blob storage

SDK bindings capability in Azure Functions enables you to work directly with the Azure Blob storage SDK types like `BlobClient`

and `ContainerClient`

instead of raw data. This provides full access to all SDK methods when working with blobs.

To configure your project to work with SDK types:

- Add the
`@azure/functions-extensions-blob`

extension preview packages to the`package.json`

file in the project, which should include at least these packages:

```
"dependencies": {
"@azure/functions": "4.7.2-preview",
"@azure/functions-extensions-blob": "0.2.0-preview"
},
```


- Add
`enableHttpStream: true`

in your`app.setup`

to support streaming types:

```
import { app } from '@azure/functions';
app.setup({
enableHttpStream: true,
});
```


This example shows how to get the BlobClient from both a Storage Blob trigger and from the input binding on an HTTP trigger:

```
import "@azure/functions-extensions-blob"; // This is the mandatory first import for SDK binding
import { StorageBlobClient } from "@azure/functions-extensions-blob";
import { app, InvocationContext } from "@azure/functions";
export async function storageBlobTrigger(
blobStorageClient: StorageBlobClient, // SDK binding provides this client
context: InvocationContext
): Promise<void> {
context.log(`Blob trigger processing: ${context.triggerMetadata.name}`);
// Access to full SDK capabilities
const blobProperties = await blobStorageClient.blobClient.getProperties();
context.log(`Blob size: ${blobProperties.contentLength}`);
// Download blob content
const downloadResponse = await blobStorageClient.blobClient.download();
context.log(`Content: ${downloadResponse}`);
}
// Register the function
app.storageBlob("storageBlobTrigger", {
path: "snippets/{name}",
connection: "AzureWebJobsStorage",
sdkBinding: true, // Enable SDK binding
handler: storageBlobTrigger,
});
```


This example shows how to get the `ContainerClient`

from both a Storage Blob input binding using an HTTP trigger:

```
import "@azure/functions-extensions-blob"; // This is the mandatory first import for SDK binding
import { StorageBlobClient } from "@azure/functions-extensions-blob";
import {
app,
HttpRequest,
HttpResponseInit,
input,
InvocationContext,
} from "@azure/functions";
const blobInput = input.storageBlob({
path: "snippets",
connection: "AzureWebJobsStorage",
sdkBinding: true,
});
export async function listBlobs(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
// Get input binding for a specific container
const storageBlobClient = context.extraInputs.get(
blobInput
) as StorageBlobClient;
// List all blobs in the container
const blobs = [];
for await (const blob of storageBlobClient.containerClient.listBlobsFlat()) {
blobs.push(blob.name);
}
return { jsonBody: { blobs } };
}
app.http("listBlobs", {
methods: ["GET"],
authLevel: "function",
extraInputs: [blobInput],
handler: listBlobs,
});
```


Keep these considerations in mind when working with SDK types:

- Always have
`import "@azure/functions-extensions-blob"`

first in your files to ensure side effects run. - Set
`sdkBinding: true`

in your binding configuration. - Use the appropriate client type for your operation:
`blobClient`

for operations on a single blob`containerClient`

for operations on a container

- Handle errors appropriately with
`try`

/`catch`

blocks - For large blob operations, consider using streaming methods to avoid memory issues.

For more information, see these [Blob Storage SDK Bindings for Node.js Samples](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-nodejs):
for more examples on how to incorporate SDK Bindings for Blob into your function app.

### Azure Service Bus

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

## Invocation context

Each invocation of your function is passed an invocation `context`

object, used to read inputs, set outputs, write to logs, and read various metadata. In the v3 model, the context object is always the first argument passed to your handler.

The `context`

object has the following properties:

| Property | Description |
|---|---|
`invocationId` |
The ID of the current function invocation. |
`executionContext` |
See
|

`bindings`

[bindings](#contextbindings).`bindingData`

[event hub trigger](functions-bindings-event-hubs-trigger)has an`enqueuedTimeUtc`

property.`traceContext`

[.](https://www.w3.org/TR/trace-context/)`Trace Context`

`bindingDefinitions`

`function.json`

.`req`

[HTTP request](#http-request).`res`

[HTTP response](#http-response).### context.executionContext

The `context.executionContext`

object has the following properties:

| Property | Description |
|---|---|
`invocationId` |
The ID of the current function invocation. |
`functionName` |
The name of the function that is being invoked. The name of the folder containing the `function.json` file determines the name of the function. |
`functionDirectory` |
The folder containing the `function.json` file. |
`retryContext` |
See
|

#### context.executionContext.retryContext

The `context.executionContext.retryContext`

object has the following properties:

| Property | Description |
|---|---|
`retryCount` |
A number representing the current retry attempt. |
`maxRetryCount` |
Maximum number of times an execution is retried. A value of `-1` means to retry indefinitely. |
`exception` |
Exception that caused the retry. |

### context.bindings

The `context.bindings`

object is used to read inputs or set outputs. The following example is a [storage queue trigger](functions-bindings-storage-queue-trigger), which uses `context.bindings`

to copy a [storage blob input](functions-bindings-storage-blob-input) to a [storage blob output](functions-bindings-storage-blob-output). The queue message's content replaces `{queueTrigger}`

as the file name to be copied, with the help of a [binding expression](functions-bindings-expressions-patterns).

```
{
"name": "myQueueItem",
"type": "queueTrigger",
"direction": "in",
"connection": "storage_APPSETTING",
"queueName": "helloworldqueue"
},
{
"name": "myInput",
"type": "blob",
"direction": "in",
"connection": "storage_APPSETTING",
"path": "helloworld/{queueTrigger}"
},
{
"name": "myOutput",
"type": "blob",
"direction": "out",
"connection": "storage_APPSETTING",
"path": "helloworld/{queueTrigger}-copy"
}
```


```
module.exports = async function (context, myQueueItem) {
const blobValue = context.bindings.myInput;
context.bindings.myOutput = blobValue;
};
```


### context.done

The `context.done`

method is deprecated. Before async functions were supported, you would signal your function is done by calling `context.done()`

:

```
module.exports = function (context, request) {
context.log("this pattern is now deprecated");
context.done();
};
```


We recommend that you remove the call to `context.done()`

and mark your function as async so that it returns a promise (even if you don't `await`

anything). As soon as your function finishes (in other words, the returned promise resolves), the v3 model knows your function is done.

```
module.exports = async function (context, request) {
context.log("you don't need context.done or an awaited call");
};
```


Each invocation of your function is passed an invocation `context`

object, with information about your invocation and methods used for logging. In the v4 model, the `context`

object is typically the second argument passed to your handler.

The `InvocationContext`

class has the following properties:

| Property | Description |
|---|---|
`invocationId` |
The ID of the current function invocation. |
`functionName` |
The name of the function. |
`extraInputs` |
Used to get the values of extra inputs. For more information, see
|

`extraOutputs`

[extra inputs and outputs](#extra-inputs-and-outputs).`retryContext`

[retry context](#retry-context).`traceContext`

[.](https://www.w3.org/TR/trace-context/)`Trace Context`

`triggerMetadata`

[event hub trigger](functions-bindings-event-hubs-trigger)has an`enqueuedTimeUtc`

property.`options`

### Retry context

The `retryContext`

object has the following properties:

| Property | Description |
|---|---|
`retryCount` |
A number representing the current retry attempt. |
`maxRetryCount` |
Maximum number of times an execution is retried. A value of `-1` means to retry indefinitely. |
`exception` |
Exception that caused the retry. |

For more information, see [ retry-policies](functions-bindings-errors#retry-policies).

## Logging

In Azure Functions, it's recommended to use `context.log()`

to write logs. Azure Functions integrates with Azure Application Insights to better capture your function app logs. Application Insights, part of Azure Monitor, provides facilities for collection, visual rendering, and analysis of both application logs and your trace outputs. To learn more, see [monitoring Azure Functions](functions-monitoring).

Note

If you use the alternative Node.js `console.log`

method, those logs are tracked at the app-level and will *not* be associated with any specific function. We *highly recommend* that your use `context`

for logging instead of `console`

so that all logs are associated with a specific function.

The following example writes a log at the default "information" level, including the invocation ID:

```
context.log(`Something has happened. Invocation ID: "${context.invocationId}"`);
```


### Log levels

In addition to the default `context.log`

method, the following methods are available that let you write logs at specific levels:

| Method | Description |
|---|---|
`context.log.error()` |
Writes an error-level event to the logs. |
`context.log.warn()` |
Writes a warning-level event to the logs. |
`context.log.info()` |
Writes an information-level event to the logs. |
`context.log.verbose()` |
Writes a trace-level event to the logs. |

| Method | Description |
|---|---|
`context.trace()` |
Writes a trace-level event to the logs. |
`context.debug()` |
Writes a debug-level event to the logs. |
`context.info()` |
Writes an information-level event to the logs. |
`context.warn()` |
Writes a warning-level event to the logs. |
`context.error()` |
Writes an error-level event to the logs. |

### Configure log level

Azure Functions lets you define the threshold level to be used when tracking and viewing logs. To set the threshold, use the `logging.logLevel`

property in the `host.json`

file. This property lets you define a default level applied to all functions, or a threshold for each individual function. To learn more, see [How to configure monitoring for Azure Functions](configure-monitoring).

## Track custom data

By default, Azure Functions writes output as traces to Application Insights. For more control, you can instead use the [Application Insights Node.js SDK](https://github.com/microsoft/applicationinsights-node.js) to send custom data to your Application Insights instance.

```
const appInsights = require("applicationinsights");
appInsights.setup();
const client = appInsights.defaultClient;
module.exports = async function (context, request) {
// Use this with 'tagOverrides' to correlate custom logs to the parent function invocation.
var operationIdOverride = {
"ai.operation.id": context.traceContext.traceparent,
};
client.trackEvent({
name: "my custom event",
tagOverrides: operationIdOverride,
properties: { customProperty2: "custom property value" },
});
client.trackException({
exception: new Error("handled exceptions can be logged with this method"),
tagOverrides: operationIdOverride,
});
client.trackMetric({
name: "custom metric",
value: 3,
tagOverrides: operationIdOverride,
});
client.trackTrace({
message: "trace message",
tagOverrides: operationIdOverride,
});
client.trackDependency({
target: "http://dbname",
name: "select customers proc",
data: "SELECT * FROM Customers",
duration: 231,
resultCode: 0,
success: true,
dependencyTypeName: "ZSQL",
tagOverrides: operationIdOverride,
});
client.trackRequest({
name: "GET /customers",
url: "http://myserver/customers",
duration: 309,
resultCode: 200,
success: true,
tagOverrides: operationIdOverride,
});
};
```


The `tagOverrides`

parameter sets the `operation_Id`

to the function's invocation ID. This setting enables you to correlate all of the automatically generated and custom logs for a given function invocation.

## HTTP triggers

HTTP and webhook triggers use request and response objects to represent HTTP messages.

HTTP and webhook triggers use `HttpRequest`

and `HttpResponse`

objects to represent HTTP messages. The classes represent a subset of the [fetch standard](https://developer.mozilla.org/docs/Web/API/fetch), using Node.js's [ undici](https://undici.nodejs.org/) package.

### HTTP Request

The request can be accessed in several ways:

**As the second argument to your function:**`module.exports = async function (context, request) { context.log(`Http function processed request for url "${request.url}"`);`


**From the**`context.req`

property:`module.exports = async function (context, request) { context.log(`Http function processed request for url "${context.req.url}"`);`


**From the named input bindings:**This option works the same as any non HTTP binding. The binding name in`function.json`

must match the key on`context.bindings`

, or "request1" in the following example:`{ "name": "request1", "type": "httpTrigger", "direction": "in", "authLevel": "anonymous", "methods": ["get", "post"] }`

`module.exports = async function (context, request) { context.log(`Http function processed request for url "${context.bindings.request1.url}"`);`


The `HttpRequest`

object has the following properties:

| Property | Type | Description |
|---|---|---|
`method` |
`string` |
HTTP request method used to invoke this function. |
`url` |
`string` |
Request URL. |
`headers` |
`Record<string, string>` |
HTTP request headers. This object is case sensitive. It's recommended to use `request.getHeader('header-name')` instead, which is case insensitive. |
`query` |
`Record<string, string>` |
Query string parameter keys and values from the URL. |
`params` |
`Record<string, string>` |
Route parameter keys and values. |
`user` |
`HttpRequestUser \| null` |
Object representing logged-in user, either through Functions authentication, SWA Authentication, or null when no such user is logged in. |
`body` |
`Buffer \| string \| any` |
If the media type is "application/octet-stream" or "multipart/*", `body` is a Buffer. If the value is a JSON parse-able string, `body` is the parsed object. Otherwise, `body` is a string. |
`rawBody` |
`string` |
The body as a string. Despite the name, this property doesn't return a Buffer. |
`bufferBody` |
`Buffer` |
The body as a buffer. |

The request can be accessed as the first argument to your handler for an HTTP triggered function.

```
async (request, context) => {
context.log(`Http function processed request for url "${request.url}"`);
```


The `HttpRequest`

object has the following properties:

| Property | Type | Description |
|---|---|---|
`method` |
`string` |
HTTP request method used to invoke this function. |
`url` |
`string` |
Request URL. |
`headers` |
`Headers` |

`query`

`URLSearchParams`

`params`

`Record<string, string>`

`user`

`HttpRequestUser \| null`

`body`

`ReadableStream \| null`

`bodyUsed`

`boolean`

In order to access a request or response's body, the following methods can be used:

| Method | Return Type |
|---|---|
`arrayBuffer()` |
`Promise<ArrayBuffer>` |

`blob()`

`Promise<Blob>`

`formData()`

`Promise<FormData>`

`json()`

`Promise<unknown>`

`text()`

`Promise<string>`

Note

The body functions can be run only once. Subsequent calls resolve with empty strings/ArrayBuffers.

### HTTP Response

The response can be set in several ways:

**Set the**`context.res`

property:`module.exports = async function (context, request) { context.res = { body: `Hello, world!` };`


**Return the response:**If your function is async and you set the binding name to`$return`

in your`function.json`

, you can return the response directly instead of setting it on`context`

.`{ "type": "http", "direction": "out", "name": "$return" }`

`module.exports = async function (context, request) { return { body: `Hello, world!` };`


**Set the named output binding:**This option works the same as any non HTTP binding. The binding name in`function.json`

must match the key on`context.bindings`

, or "response1" in the following example:`{ "type": "http", "direction": "out", "name": "response1" }`

`module.exports = async function (context, request) { context.bindings.response1 = { body: `Hello, world!` };`


**Call**This option is deprecated. It implicitly calls`context.res.send()`

:`context.done()`

and can't be used in an async function.`module.exports = function (context, request) { context.res.send(`Hello, world!`);`


If you create a new object when setting the response, that object must match the `HttpResponseSimple`

interface, which has the following properties:

| Property | Type | Description |
|---|---|---|
`headers` |
`Record<string, string>` (optional) |
HTTP response headers. |
`cookies` |
`Cookie[]` (optional) |
HTTP response cookies. |
`body` |
`any` (optional) |
HTTP response body. |
`statusCode` |
`number` (optional) |
HTTP response status code. If not set, defaults to `200` . |
`status` |
`number` (optional) |
The same as `statusCode` . This property is ignored if `statusCode` is set. |

You can also modify the `context.res`

object without overwriting it. The default `context.res`

object uses the `HttpResponseFull`

interface, which supports the following methods in addition to the `HttpResponseSimple`

properties:

| Method | Description |
|---|---|
`status()` |
Sets the status. |
`setHeader()` |
Sets a header field. NOTE: `res.set()` and `res.header()` are also supported and do the same thing. |
`getHeader()` |
Get a header field. NOTE: `res.get()` is also supported and does the same thing. |
`removeHeader()` |
Removes a header. |
`type()` |
Sets the "content-type" header. |
`send()` |
This method is deprecated. It sets the body and calls `context.done()` to indicate a sync function is finished. NOTE: `res.end()` is also supported and does the same thing. |
`sendStatus()` |
This method is deprecated. It sets the status code and calls `context.done()` to indicate a sync function is finished. |
`json()` |
This method is deprecated. It sets the "content-type" to "application/json", sets the body, and calls `context.done()` to indicate a sync function is finished. |

The response can be set in several ways:

**As a simple interface with type**This option is the most concise way of returning responses.`HttpResponseInit`

:`return { body: `Hello, world!` };`


The `HttpResponseInit`

interface has the following properties:

| Property | Type | Description |
|---|---|---|
`body` |
`BodyInit` (optional) |
HTTP response body as one of
`ArrayBuffer` |

[,](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array)

`AsyncIterable<Uint8Array>`

[,](https://developer.mozilla.org/docs/Web/API/Blob)

`Blob`

[,](https://developer.mozilla.org/docs/Web/API/FormData)

`FormData`

[,](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array)

`Iterable<Uint8Array>`

[,](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer)

`NodeJS.ArrayBufferView`

[,](https://developer.mozilla.org/docs/Web/API/URLSearchParams)

`URLSearchParams`

`null`

, or `string`

.`jsonBody`

`any`

(optional)`HttpResponseInit.body`

property is ignored in favor of this property.`status`

`number`

(optional)`200`

.`headers`

[(optional)](https://developer.mozilla.org/docs/Web/API/Headers)`HeadersInit`

`cookies`

`Cookie[]`

(optional)**As a class with type**This option provides helper methods for reading and modifying various parts of the response like the headers.`HttpResponse`

:`const response = new HttpResponse({ body: `Hello, world!` }); response.headers.set("content-type", "application/json"); return response;`


The `HttpResponse`

class accepts an optional `HttpResponseInit`

as an argument to its constructor and has the following properties:

| Property | Type | Description |
|---|---|---|
`status` |
`number` |
HTTP response status code. |
`headers` |
`Headers` |

`cookies`

`Cookie[]`

`body`

`ReadableStream | null`

`bodyUsed`

`boolean`

## HTTP streams

HTTP streams is a feature that makes it easier to process large data, stream OpenAI responses, deliver dynamic content, and support other core HTTP scenarios. It lets you stream requests to and responses from HTTP endpoints in your Node.js function app. Use HTTP streams in scenarios where your app requires real-time exchange and interaction between client and server over HTTP. You can also use HTTP streams to get the best performance and reliability for your apps when using HTTP.

Important

HTTP streams aren't supported in the v3 model. [Upgrade to the v4 model](functions-node-upgrade-v4) to use the HTTP streaming feature.
The existing `HttpRequest`

and `HttpResponse`

types in programming model v4 already support various ways of handling the message body, including as a stream.

### Prerequisites

- The
version 4.3.0 or later.`@azure/functions`

npm package [Azure Functions runtime](functions-versions)version 4.28 or later.[Azure Functions Core Tools](functions-run-local)version 4.0.5530 or a later version, which contains the correct runtime version.

### Enable streams

Use these steps to enable HTTP streams in your function app in Azure and in your local projects:

If you plan to stream large amounts of data, modify the

setting in Azure. The default maximum body size allowed is`FUNCTIONS_REQUEST_BODY_SIZE_LIMIT`

`104857600`

, which limits your requests to a size of ~100 MB.For local development, also add

`FUNCTIONS_REQUEST_BODY_SIZE_LIMIT`

to the[local.settings.json file](functions-develop-local#local-settings-file).Add the following code to your app in any file included by your

[main field](functions-reference-node#registering-a-function).`const { app } = require("@azure/functions"); app.setup({ enableHttpStream: true });`


### Stream examples

This example shows an HTTP triggered function that receives data via an HTTP POST request, and the function streams this data to a specified output file:

```
const { app } = require('@azure/functions');
const { createWriteStream } = require('fs');
const { Writable } = require('stream');
app.http('httpTriggerStreamRequest', {
methods: ['POST'],
authLevel: 'anonymous',
handler: async (request, context) => {
const writeStream = createWriteStream('<output file path>');
await request.body.pipeTo(Writable.toWeb(writeStream));
return { body: 'Done!' };
},
});
```


This example shows an HTTP triggered function that streams a file's content as the response to incoming HTTP GET requests:

```
const { app } = require('@azure/functions');
const { createReadStream } = require('fs');
app.http('httpTriggerStreamResponse', {
methods: ['GET'],
authLevel: 'anonymous',
handler: async (request, context) => {
const body = createReadStream('<input file path>');
return { body };
},
});
```


For a ready-to-run sample app using streams, check out this example on [GitHub](https://github.com/Azure-Samples/azure-functions-nodejs-stream).

### Stream considerations

- Use
`request.body`

to obtain the maximum benefit from using streams. You can still continue to use methods like`request.text()`

, which always return the body as a string.

## Hooks

Hooks aren't supported in the v3 model. [Upgrade to the v4 model](functions-node-upgrade-v4) to use hooks.

Use a hook to execute code at different points in the Azure Functions lifecycle. Hooks are executed in the order they're registered and can be registered from any file in your app. There are currently two scopes of hooks, "app" level and "invocation" level.

### Invocation hooks

Invocation hooks are executed once per invocation of your function, either before in a `preInvocation`

hook or after in a `postInvocation`

hook. By default your hook executes for all trigger types, but you can also filter by type. The following example shows how to register an invocation hook and filter by trigger type:

```
const { app } = require('@azure/functions');
app.hook.preInvocation((context) => {
if (context.invocationContext.options.trigger.type === 'httpTrigger') {
context.invocationContext.log(
`preInvocation hook executed for http function ${context.invocationContext.functionName}`
);
}
});
app.hook.postInvocation((context) => {
if (context.invocationContext.options.trigger.type === 'httpTrigger') {
context.invocationContext.log(
`postInvocation hook executed for http function ${context.invocationContext.functionName}`
);
}
});
```


The first argument to the hook handler is a context object specific to that hook type.

The `PreInvocationContext`

object has the following properties:

| Property | Description |
|---|---|
`inputs` |
The arguments passed to the invocation. |
`functionHandler` |
The function handler for the invocation. Changes to this value affect the function itself. |
`invocationContext` |
The
|

`hookData`

The `PostInvocationContext`

object has the following properties:

| Property | Description |
|---|---|
`inputs` |
The arguments passed to the invocation. |
`result` |
The result of the function. Changes to this value affect the overall result of the function. |
`error` |
The error thrown by the function, or null/undefined if there's no error. Changes to this value affect the overall result of the function. |
`invocationContext` |
The
|

`hookData`

### App hooks

App hooks are executed once per instance of your app, either during startup in an `appStart`

hook or during termination in an `appTerminate`

hook. App terminate hooks have a limited time to execute and don't execute in all scenarios.

The Azure Functions runtime currently [doesn't support](https://github.com/Azure/azure-functions-host/issues/8222) context logging outside of an invocation. Use the Application Insights [npm package](https://www.npmjs.com/package/applicationinsights) to log data during app level hooks.

The following example registers app hooks:

```
const { app } = require('@azure/functions');
app.hook.appStart((context) => {
// add your logic here
});
app.hook.appTerminate((context) => {
// add your logic here
});
```


The first argument to the hook handler is a context object specific to that hook type.

The `AppStartContext`

object has the following properties:

| Property | Description |
|---|---|
`hookData` |
The recommended place to store and share data between hooks in the same scope. You should use a unique property name so that it doesn't conflict with other hooks' data. |

The `AppTerminateContext`

object has the following properties:

| Property | Description |
|---|---|
`hookData` |
The recommended place to store and share data between hooks in the same scope. You should use a unique property name so that it doesn't conflict with other hooks' data. |

## Scaling and concurrency

By default, Azure Functions automatically monitors the load on your application and creates more host instances for Node.js as needed. Azure Functions uses built-in (not user configurable) thresholds for different trigger types to decide when to add instances, such as the age of messages and queue size for QueueTrigger. For more information, see [How the Consumption and Premium plans work](event-driven-scaling).

This scaling behavior is sufficient for many Node.js applications. For CPU-bound applications, you can improve performance further by using multiple language worker processes. You can increase the number of worker processes per host from the default of 1 up to a max of 10 by using the [FUNCTIONS_WORKER_PROCESS_COUNT](functions-app-settings#functions_worker_process_count) application setting. Azure Functions then tries to evenly distribute simultaneous function invocations across these workers. This behavior makes it less likely that a CPU-intensive function blocks other functions from running. The setting applies to each host that Azure Functions creates when scaling out your application to meet demand.

Warning

Use the `FUNCTIONS_WORKER_PROCESS_COUNT`

setting with caution. Multiple processes running in the same instance can lead to unpredictable behavior and increase function load times. If you use this setting, we *highly recommend* that you offset these downsides by [running from a package file](run-functions-from-deployment-package).

## Node version

You can see the current version that the runtime is using by logging `process.version`

from any function. See [ supported versions](#supported-versions) for a list of Node.js versions supported by each programming model.

### Setting the Node version

The way that you upgrade your Node.js version depends on the OS on which your function app runs.

When it runs on Windows, the Node.js version is set by the [ WEBSITE_NODE_DEFAULT_VERSION](functions-app-settings#website_node_default_version) application setting. This setting can be updated either by using the Azure CLI or in the Azure portal.

For more information about Node.js versions, see [Supported versions](#supported-versions).

Before upgrading your Node.js version, make sure your function app is running on the latest version of the Azure Functions runtime. If you need to upgrade your runtime version, see [Migrate apps from Azure Functions version 3.x to version 4.x](migrate-version-3-version-4?pivots=programming-language-javascript).

Run the Azure CLI [ az functionapp config appsettings set](/en-us/cli/azure/functionapp/config#az-functionapp-config-appsettings-set) command to update the Node.js version for your function app running on Windows:

```
az functionapp config appsettings set --settings WEBSITE_NODE_DEFAULT_VERSION=~22 \
--name <FUNCTION_APP_NAME> --resource-group <RESOURCE_GROUP_NAME>
```


This sets the [ WEBSITE_NODE_DEFAULT_VERSION application setting](functions-app-settings#website_node_default_version) the supported LTS version of

`~22`

.After changes are made, your function app restarts. To learn more about Functions support for Node.js, see [Language runtime support policy](language-support-policy).

## Environment variables

Environment variables can be useful for operational secrets (connection strings, keys, endpoints, etc.) or environmental settings such as profiling variables. You can add environment variables in both your local and cloud environments and access them through `process.env`

in your function code.

The following example logs the `WEBSITE_SITE_NAME`

environment variable:

```
module.exports = async function (context) {
context.log(`WEBSITE_SITE_NAME: ${process.env["WEBSITE_SITE_NAME"]}`);
};
```


```
async function timerTrigger1(myTimer, context) {
context.log(`WEBSITE_SITE_NAME: ${process.env["WEBSITE_SITE_NAME"]}`);
}
```


### In local development environment

When you run locally, your functions project includes a [ local.settings.json file](functions-run-local), where you store your environment variables in the

`Values`

object.```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "",
"FUNCTIONS_WORKER_RUNTIME": "node",
"CUSTOM_ENV_VAR_1": "hello",
"CUSTOM_ENV_VAR_2": "world"
}
}
```


### In Azure cloud environment

When you run in Azure, the function app lets you set and use [Application settings](functions-app-settings), such as service connection strings, and exposes these settings as environment variables during execution.

There are several ways that you can add, update, and delete function app settings:

Changes to function app settings require your function app to be restarted.

### Worker environment variables

There are several Functions environment variables specific to Node.js:

#### languageWorkers**node**arguments

This setting allows you to specify custom arguments when starting your Node.js process. It's most often used locally to start the worker in debug mode, but can also be used in Azure if you need custom arguments.

Warning

If possible, avoid using `languageWorkers__node__arguments`

in Azure because it can have a negative effect on cold start times. Rather than using prewarmed workers, the runtime has to start a new worker from scratch with your custom arguments.

#### logging**logLevel**Worker

This setting adjusts the default log level for Node.js-specific worker logs. By default, only warning or error logs are shown, but you can set it to `information`

or `debug`

to help diagnose issues with the Node.js worker. For more information, see [configuring log levels](configure-monitoring#configure-log-levels).

## ECMAScript modules (preview)

Note

As ECMAScript modules are currently a preview feature in Node.js 14 or higher in Azure Functions.

[ECMAScript modules](https://nodejs.org/docs/latest-v14.x/api/esm.html#esm_modules_ecmascript_modules) (ES modules) are the new official standard module system for Node.js. So far, the code samples in this article use the CommonJS syntax. When running Azure Functions in Node.js 14 or higher, you can choose to write your functions using ES modules syntax.

To use ES modules in a function, change its filename to use a `.mjs`

extension. The following *index.mjs* file example is an HTTP triggered function that uses ES modules syntax to import the `uuid`

library and return a value.

```
import { v4 as uuidv4 } from "uuid";
async function httpTrigger1(context, request) {
context.res.body = uuidv4();
}
export default httpTrigger;
```


```
import { v4 as uuidv4 } from "uuid";
async function httpTrigger1(request, context) {
return { body: uuidv4() };
}
app.http("httpTrigger1", {
methods: ["GET", "POST"],
handler: httpTrigger1,
});
```


## Configure function entry point

The `function.json`

properties `scriptFile`

and `entryPoint`

can be used to configure the location and name of your exported function. The `scriptFile`

property is required when you're using TypeScript and should point to the compiled JavaScript.

### Using `scriptFile`


By default, a JavaScript function is executed from `index.js`

, a file that shares the same parent directory as its corresponding `function.json`

.

`scriptFile`

can be used to get a folder structure that looks like the following example:

```
<project_root>/
| - node_modules/
| - myFirstFunction/
| | - function.json
| - lib/
| | - sayHello.js
| - host.json
| - package.json
```


The `function.json`

for `myFirstFunction`

should include a `scriptFile`

property pointing to the file with the exported function to run.

```
{
"scriptFile": "../lib/sayHello.js",
"bindings": [
...
]
}
```


### Using `entryPoint`


In the v3 model, a function must be exported using `module.exports`

in order to be found and run. By default, the function that executes when triggered is the only export from that file, the export named `run`

, or the export named `index`

. The following example sets `entryPoint`

in `function.json`

to a custom value, "logHello":

```
{
"entryPoint": "logHello",
"bindings": [
...
]
}
```


```
async function logHello(context) {
context.log("Hello, world!");
}
module.exports = { logHello };
```


## Local debugging

We recommend that you use VS Code for local debugging, which starts your Node.js process in debug mode automatically and attaches to the process for you. For more information, see [run the function locally](how-to-create-function-vs-code?pivot=programming-language-javascript#run-the-function-locally).

If you're using a different tool for debugging or want to start your Node.js process in debug mode manually, add `"languageWorkers__node__arguments": "--inspect"`

under `Values`

in your [local.settings.json](functions-develop-local#local-settings-file). The `--inspect`

argument tells Node.js to listen for a debug client, on port 9229 by default. For more information, see the [Node.js debugging guide](https://nodejs.org/en/learn/getting-started/debugging).

## Recommendations

This section describes several impactful patterns for Node.js apps that we recommend you follow.

### Choose single-vCPU App Service plans

When you create a function app that uses the App Service plan, we recommend that you select a single-vCPU plan rather than a plan with multiple vCPUs. Today, Functions runs Node.js functions more efficiently on single-vCPU VMs, and using larger VMs doesn't produce the expected performance improvements. When necessary, you can manually scale out by adding more single-vCPU VM instances, or you can enable autoscale. For more information, see [Scale instance count manually or automatically](/en-us/azure/azure-monitor/autoscale/autoscale-get-started?toc=/azure/app-service/toc.json).

### Run from a package file

When you develop Azure Functions in the serverless hosting model, cold starts are a reality. *Cold start* refers to the first time your function app starts after a period of inactivity, taking longer to start up. For Node.js apps with large dependency trees in particular, cold start can be significant. To speed up the cold start process, [run your functions as a package file](run-functions-from-deployment-package) when possible. Many deployment methods use this model by default, but if you're experiencing large cold starts you should check to make sure you're running this way.

### Use a single static client

When you use a service-specific client in an Azure Functions application, don't create a new client with every function invocation because you can hit connection limits. Instead, create a single, static client in the global scope. For more information, see [managing connections in Azure Functions](manage-connections).

### Use `async`

and `await`


When writing Azure Functions in Node.js, you should write code using the `async`

and `await`

keywords. Writing code using `async`

and `await`

instead of callbacks or `.then`

and `.catch`

with Promises helps avoid two common problems:

- Throwing uncaught exceptions that
[crash the Node.js process](https://nodejs.org/api/process.html#process_warning_using_uncaughtexception_correctly), potentially affecting the execution of other functions. - Unexpected behavior, such as missing logs from
`context.log`

, caused by asynchronous calls that aren't properly awaited.

In the following example, the asynchronous method `fs.readFile`

is invoked with an error-first callback function as its second parameter. This code causes both of the issues previously mentioned. An exception that isn't explicitly caught in the correct scope can crash the entire process (issue #1). Returning without ensuring the callback finishes means the http response sometimes has an empty body (issue #2).

```
// DO NOT USE THIS CODE
const { app } = require('@azure/functions');
const fs = require('fs');
app.http('httpTriggerBadAsync', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: async (request, context) => {
let fileData;
fs.readFile('./helloWorld.txt', (err, data) => {
if (err) {
context.error(err);
// BUG #1: This will result in an uncaught exception that crashes the entire process
throw err;
}
fileData = data;
});
// BUG #2: fileData is not guaranteed to be set before the invocation ends
return { body: fileData };
},
});
```


In the following example, the asynchronous method `fs.readFile`

is invoked with an error-first callback function as its second parameter. This code causes both of the issues previously mentioned. An exception that isn't explicitly caught in the correct scope can crash the entire process (issue #1). Calling the deprecated `context.done()`

method outside of the scope of the callback can signal the function is finished before the file is read (issue #2). In this example, calling `context.done()`

too early results in missing log entries starting with `Data from file:`

.

```
// NOT RECOMMENDED PATTERN
const fs = require("fs");
module.exports = function (context) {
fs.readFile("./hello.txt", (err, data) => {
if (err) {
context.log.error("ERROR", err);
// BUG #1: This will result in an uncaught exception that crashes the entire process
throw err;
}
context.log(`Data from file: ${data}`);
// context.done() should be called here
});
// BUG #2: Data is not guaranteed to be read before the Azure Function's invocation ends
context.done();
};
```


Use the `async`

and `await`

keywords to help avoid both of these issues. Most APIs in the Node.js ecosystem have been converted to support promises in some form. For example, starting in v14, Node.js provides an `fs/promises`

API to replace the `fs`

callback API.

In the following example, any unhandled exceptions thrown during the function execution only fail the individual invocation that raised the exception. The `await`

keyword means that steps following `readFile`

only execute after it's complete.

```
// Recommended pattern
const { app } = require('@azure/functions');
const fs = require('fs/promises');
app.http('httpTriggerGoodAsync', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: async (request, context) => {
try {
const fileData = await fs.readFile('./helloWorld.txt');
return { body: fileData };
} catch (err) {
context.error(err);
// This rethrown exception will only fail the individual invocation, instead of crashing the whole process
throw err;
}
},
});
```


With `async`

and `await`

, you also don't need to call the `context.done()`

callback.

```
// Recommended pattern
const fs = require("fs/promises");
module.exports = async function (context) {
let data;
try {
data = await fs.readFile("./hello.txt");
} catch (err) {
context.log.error("ERROR", err);
// This rethrown exception will be handled by the Functions Runtime and will only fail the individual invocation
throw err;
}
context.log(`Data from file: ${data}`);
};
```


## Troubleshoot

See the [Node.js Troubleshoot guide](functions-node-troubleshoot).

## Next steps

For more information, see the following resources:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-http-webhook-output -->

# Azure Functions HTTP output bindings

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the HTTP output binding to respond to the HTTP request sender (HTTP trigger). This binding requires an HTTP trigger and allows you to customize the response associated with the trigger's request.

The default return value for an HTTP-triggered function is:

`HTTP 204 No Content`

with an empty body in Functions 2.x and higher`HTTP 200 OK`

with an empty body in Functions 1.x

## Attribute

A return value attribute isn't required when using [HttpResponseData](/en-us/dotnet/api/microsoft.azure.functions.worker.http.httpresponsedata). However, when using a [ASP.NET Core integration](dotnet-isolated-process-guide#aspnet-core-integration) and [multi-binding output objects](dotnet-isolated-process-guide#multiple-output-bindings), the `[HttpResultAttribute]`

attribute should be applied to the object property. The attribute takes no parameters. To learn more, see [Usage](#usage).

## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the [HttpOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.httpoutput) annotation to define an output variable other than the default variable returned by the function. This annotation supports the following settings:

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

## Configuration

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| Property | Description |
|---|---|
type |
Must be set to `http` . |
direction |
Must be set to `out` . |
name |
The variable name used in function code for the response, or `$return` to use the return value. |

## Usage

To send an HTTP response, use the language-standard response patterns.

In .NET, the response type depends on the C# mode:

The HTTP triggered function returns an object of one of the following types:

[IActionResult](/en-us/dotnet/api/microsoft.aspnetcore.mvc.iactionresult)1(or`Task<IActionResult>`

)[HttpResponse](/en-us/dotnet/api/microsoft.aspnetcore.http.httpresponse)1(or`Task<HttpResponse>`

)[HttpResponseData](/en-us/dotnet/api/microsoft.azure.functions.worker.http.httpresponsedata)(or`Task<HttpResponseData>`

)- JSON serializable types representing the response body for a
`200 OK`

response.

1 This type is only available when using [ASP.NET Core integration](dotnet-isolated-process-guide#aspnet-core-integration).

When one of these types is used as part of [multi-binding output objects](dotnet-isolated-process-guide#multiple-output-bindings), the `[HttpResult]`

attribute should be applied to the object property. The attribute takes no parameters.

For Java, use an [HttpResponseMessage.Builder](/en-us/java/api/com.microsoft.azure.functions.httpresponsemessage.builder) to create a response to the HTTP trigger. To learn more, see [HttpRequestMessage and HttpResponseMessage](functions-reference-java#httprequestmessage-and-httpresponsemessage).

For example responses, see the [trigger examples](functions-bindings-http-webhook-trigger#example).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-rabbitmq -->

# RabbitMQ bindings for Azure Functions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions integrates with [RabbitMQ](https://www.rabbitmq.com/) via [triggers and bindings](functions-triggers-bindings).

Note

The RabbitMQ bindings are only fully supported on [Elastic Premium](functions-premium-plan) and [Dedicated (App Service)](dedicated-plan) plans. [Flex Consumption](flex-consumption-plan) and [Consumption](consumption-plan) plans aren't yet supported.

RabbitMQ bindings aren't supported by the Azure Functions v1.x runtime.

The Azure Functions RabbitMQ extension allows you to send and receive messages using the RabbitMQ API with Functions.

| Action | Type |
|---|---|
| Run a function when a RabbitMQ message comes through the queue |
|

[Output binding](functions-bindings-rabbitmq-output)## Prerequisites

Before working with the RabbitMQ extension, you must [set up your RabbitMQ endpoint](https://github.com/Azure/azure-functions-rabbitmq-extension/wiki/Setting-up-a-RabbitMQ-Endpoint). To learn more about RabbitMQ, see the [getting started page](https://www.rabbitmq.com/getstarted.html).

## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

Add the extension to your project by installing this [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Rabbitmq).

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

```
{
"version": "2.0",
"extensions": {
"rabbitMQ": {
"prefetchCount": 100,
"queueName": "queue",
"connectionString": "%<MyConnectionAppSetting>%",
"port": 10
}
}
}
```


| Property | Default | Description |
|---|---|---|
`prefetchCount` |
30 | Gets or sets the number of messages that the message receiver can simultaneously request and is cached. |
`queueName` |
n/a | Name of the queue to receive messages from. |
`connectionString` |
n/a | The app setting that contains the RabbitMQ message queue connection string. |
`port` |
0 | (ignored if using connectionString) Gets or sets the Port used. Defaults to 0, which points to rabbitmq client's default port setting: 5672. |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/python-build-options -->

# Build your Python Azure Functions apps

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions supports three build options for publishing your Python apps to Azure. Choose your build method based on your local environment, app dependencies, and runtime requirements.

## Quick comparison for build actions

| Deployment type | Where dependencies are installed | Typical use case |
|---|---|---|
|

[Local build](#local-build)[Custom dependencies](#custom-dependencies)## Deployment package considerations

When deploying your Python function app to Azure, keep these packaging requirements in mind:

**Package contents, not the folder**: Deploy the contents of your project folder, not the folder itself.**Root-level**: Ensure a single`host.json`

`host.json`

file is at the root of the deployment package, not nested in a subfolder.**Exclude development files**: You can exclude folders like`tests/`

,`.github/`

, and`.venv*/`

from the deployed package by including them in`.funcignore`

.**The build environment must match the production environment**: Your dependencies must be built on an ubuntu machine using the same python version as the production app.[Remote build](#remote-build)handles this scenario automatically.**Dependencies must be installed into**: Remote build installs all dependencies listed in`./.python_packages/lib/site-packages`

`requirements.txt`

into the correct directory.**Keep deployment package size in mind**: large dependency sets increase build time, cold start latency, and module import and initialization time. Applications with large scientific or ML libraries (including`pytorch`

) are especially impacted.**Remote build has a 60-second timeout**: If dependency installation exceeds the limit, the build fails. In that case, consider using a[local build](#local-build)and deploying with prebuilt dependencies.**Module import has a 2-minute time limit**: Python module loading and function indexing during startup has a 2-minute limit for Python 3.13 and above, or for older python versions with`PYTHON_ENABLE_INIT_INDEXING`

enabled. If your app exceeds this, reduce top-level imports or use lazy imports (import modules inside the function body instead of at the global scope).

## Remote build

Remote build is the recommended approach for a code-only deployment of your Python app to Functions.


With [remote build](functions-deployment-technologies#remote-build), the Functions platform handles package installation and ensures compatibility with the remote
runtime environment. Using remote build also results in a smaller deployment package.

You can use remote build when you publish your Python app using these tools:

: the**Azure Functions Core Tools**command requests a remote build by default when publishing Python apps.`func azure functionapp publish`

:**AZ CLI**uses remote build by default when deploying Python apps.`az functionapp deployment source config-zip`

: the**Visual Studio Code****Azure Functions: Deploy to Azure...**command always uses a remote build.: the**Continuous delivery by using GitHub Actions****Azure/functions-action@v1**action uses remote build when the`remote-build`

parameter is set to`true`

for the Flex Consumption plan or when`scm-do-build-during-deployment`

and`enable-oryx-build`

are set to`true`

for Dedicated plans.

To enable remote build for other scenarios, like [ Continuous delivery with Azure Pipelines](functions-how-to-azure-devops), see

[Enabling Remote Build](functions-deployment-technologies#remote-build).

Remote build also supports custom package indexes when by using the [ PIP_EXTRA_INDEX_URL](functions-app-settings#pip_extra_index_url) app setting. For more information, see

[Remote build](functions-deployment-technologies#remote-build).

Important

Remote build installs all dependencies listed in `requirements.txt`

. To ensure all required packages are installed, be sure to include those dependencies in your `requirements.txt`

file.

## Local build

If you don't request a remote build, then dependencies are instead installed on your machine. The entire local project and dependencies are then packaged locally and deployed to your function app. Using local build results in a larger package upload.

You also need to install dependencies into the correct directory. Use `pip install --target="./.python_packages/lib/site-packages"`

to install required dependencies into your local `.python_packages/lib/site-packages`

folder.
For example, if you have your dependencies listed in a `requirements.txt`

file, you can run this command:

```
pip install --target="./.python_packages/lib/site-packages" -r requirements.txt
```


Use local build when:

- You're developing locally on Linux or macOS.
- Remote build isn't available or is restricted.
- You want to define dependencies in a file other than
`requirements.txt`

, such as`pyproject.toml`

.

The following tools can be configured to use local build:

: use**Azure Functions Core Tools**with the`func azure functionapp publish`

`--no-build`

flag.:**AZ CLI**with the`az functionapp deployment source config-zip`

`--build-remote=false`

flag.: set the**Continuous delivery by using GitHub Actions**`remote-build`

parameter to`false`

for the Flex Consumption plan or set`scm-do-build-during-deployment`

and`enable-oryx-build`

to`false`

for Dedicated plans.

Important

When developing your Python apps on a Windows computer, don't use local build. Packages built on a Windows computer often have issues being deployed to and running on Linux in Azure Functions. Only use local build if you're confident the package runs on Linux based systems.

## Custom dependencies

Azure Functions supports custom and other non-PyPI dependencies by using the [ PIP_EXTRA_INDEX_URL](functions-app-settings#pip_extra_index_url) app setting or by creating a local build on a Linux or macOS computer.

### Remote build with an extra index URL

When your private packages are available online, you can request a remote build after setting the private package location by using the [ PIP_EXTRA_INDEX_URL](functions-app-settings#pip_extra_index_url) app setting.
When you set

[, remote builds use this package feed during deployment.](functions-app-settings#pip_extra_index_url)

`PIP_EXTRA_INDEX_URL`

[replaces the package index, so consider using](functions-app-settings#pip_index_url)

`PIP_INDEX_URL`

[instead to prevent unexpected behavior.](functions-app-settings#pip_extra_index_url)

`PIP_EXTRA_INDEX_URL`

### Local packages or wheels

Local packages and wheels are supported when building python Azure Function apps.

To install these packages or wheels using [remote build](#remote-build), you can include the dependencies in your `requirements.txt`

file and deploy with [remote build enabled](functions-deployment-technologies#remote-build).

For example, your `requirements.txt`

file might look like the following snippet:

```
# Installing a custom wheel
<my_package_wheel>.whl
# Installing a local package
path/to/my/package
```


To install these dependencies using [local build](#local-build), install the dependencies into your local `.python_packages/lib/site-packages`

folder and deploy with [remote build disabled](#local-build).
For example, if you have the packages defined in your `requirements.txt`

file, you can install and publish using the following commands and Core Tools:

```
pip install --target="./.python_packages/lib/site-packages" -r requirements.txt
func azure functionapp publish <APP_NAME> --no-build
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-best-practices -->

# Best practices for reliable Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions is an event-driven, compute-on-demand service that extends the existing Azure App Service application platform. It adds capabilities to implement code triggered by events occurring in Azure, in a partner service, and in on-premises systems. By using Functions, you can build solutions that connect to data sources or messaging solutions, which makes it easier to process and react to events. Functions runs in Azure data centers, which are complex with many integrated components. In a hosted cloud environment, it's expected that VMs can occasionally restart or move, and systems upgrades occur. Your functions apps also likely depend on external APIs, Azure Services, and other databases, which are also prone to periodic unreliability.

This article details some best practices for designing and deploying efficient function apps that remain healthy and perform well in a cloud-based environment.

## Choose the correct hosting plan

When you create a function app in Azure, you must choose a hosting plan for your app. The plan you choose affects performance, reliability, and cost. Azure Functions provides the following hosting plans:

When possible, use the [Flex Consumption plan](flex-consumption-plan) to host your dynamic scale apps.

In the context of the App Service platform, the *Premium* plan that dynamically hosts your functions is the Elastic Premium plan (EP). Other Dedicated (App Service) plans are called Premium. For more information, see [Azure Functions Premium plan](functions-premium-plan).

The hosting plan you choose determines the following behaviors:

- How your function app scales based on demand and how instance allocation is managed.
- The resources available to each function app instance.
- Support for advanced functionality, such as Azure Virtual Network connectivity.

For more information about choosing the correct hosting plan and a detailed comparison between the plans, see [Azure Functions hosting options](functions-scale).

Choose the correct plan when you create your function app. Functions provides a limited ability to switch your hosting plan, primarily between Consumption and Elastic Premium plans. For more information, see [Plan migration](functions-how-to-use-azure-function-app-settings?tabs=portal#plan-migration).

## Configure storage correctly

Functions requires a storage account be associated with your function app. The Functions host uses the storage account connection for operations such as managing triggers and logging function executions. It's also used when dynamically scaling function apps. For more information, see [Storage considerations for Azure Functions](storage-considerations).

A misconfigured file system or storage account in your function app can affect the performance and availability of your functions. For help with troubleshooting an incorrectly configured storage account, see the [storage troubleshooting](functions-recover-storage-account) article.

### Storage connection settings

Function apps that scale dynamically can run either from an Azure Files endpoint in your storage account or from the file servers associated with your scaled-out instances. This behavior is controlled by the following application settings:

The Premium plan and the Consumption plan on Windows support these settings. The Flex Consumption plan doesn't require these settings and uses a Blob storage container to host deployment packages instead of an Azure Files share.

When you create your function app in the Azure portal or by using Azure CLI or Azure PowerShell, you create these settings for your function app when needed. When you create your resources from an Azure Resource Manager template (ARM template), you need to also include `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

in the template.

On your first deployment using an ARM template, don't include `WEBSITE_CONTENTSHARE`

, which is generated for you.

You can use the following ARM template examples to help correctly configure these settings:

[Consumption plan](https://azure.microsoft.com/resources/templates/function-app-create-dynamic/)[Dedicated plan](https://azure.microsoft.com/resources/templates/function-app-create-dedicated/)[Premium plan with VNET integration](https://azure.microsoft.com/resources/templates/function-premium-vnet-integration/)[Consumption plan with a deployment slot](https://azure.microsoft.com/resources/templates/function-app-create-dynamic-slot/)

Important

The Azure Files service doesn't currently support identity-based connections. The Flex Consumption plan fully supports managed identities. For more information, see [Create an app without Azure Files](storage-considerations#create-an-app-without-azure-files).

### Storage account configuration

When creating a function app, you must create or link to a general-purpose Azure Storage account that supports Blob, Queue, and Table storage. Functions relies on Azure Storage for operations such as managing triggers and logging function executions. The storage account connection string for your function app is found in the `AzureWebJobsStorage`

and `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

application settings.

Keep in mind the following considerations when creating this storage account:

To reduce latency, create the storage account in the same region as the function app.

To improve performance in production, use a separate storage account for each function app. This aspect is especially true with Durable Functions and Event Hubs triggered functions.

For Event Hubs triggered functions, don't use an account with

[Data Lake Storage enabled](https://github.com/Azure/azure-functions-eventhubs-extension/issues/81).

### Handling large data sets

When running on Linux, you can add extra storage by mounting a file share. Mounting a share is a convenient way for a function to process a large existing data set. For more information, see [Mount file shares](storage-considerations#mount-file-shares).

## Organize your functions

As part of your solution, you likely develop and publish multiple functions. These functions are often combined into a single function app, but they can also run in separate function apps. In Premium and Dedicated (App Service) hosting plans, multiple function apps can also share the same resources by running in the same plan. How you group your functions and function apps can affect the performance, scaling, configuration, deployment, and security of your overall solution.

For Consumption and Premium plan, all functions in a function app are dynamically scaled together.

For more information on how to organize your functions, see [Function organization best practices](performance-reliability#function-organization-best-practices).

## Optimize deployments

When you deploy a function app, remember that the unit of deployment for functions in Azure is the function app. You deploy all functions in a function app at the same time, usually from the same deployment package.

Consider these options for a successful deployment:

Have your functions run from the deployment package. This

[run from package approach](run-functions-from-deployment-package)provides the following benefits:- Reduces the risk of file copy locking problems.
- Can be deployed directly to a production app and doesn't trigger a restart.
- All files in the package are available to your app.
- Improves the performance of ARM template deployments.
- Might reduce cold-start times, particularly for JavaScript functions with large npm package trees.

Consider using

[continuous deployment](functions-continuous-deployment)to connect deployments to your source control solution. Continuous deployments also let you run from the deployment package.For

[Premium plan hosting](functions-premium-plan), consider adding a warmup trigger to reduce latency when new instances are added. For more information, see[Azure Functions warm-up trigger](functions-bindings-warmup).To minimize deployment downtime, use deployment slots for Consumption, Premium, and Dedicated plans. Or, configure rolling updates for zero-downtime deployments in the Flex Consumption plan. For more information, see

[Azure Functions deployment slots](functions-deployment-slots)and[site update strategies in Flex Consumption](flex-consumption-site-updates).

## Write robust functions

Follow design principles that help with the general performance and availability of your functions. These principles include:

[Avoid long running functions](performance-reliability#avoid-long-running-functions)[Plan cross-function communication](performance-reliability#cross-function-communication)[Write functions to be stateless](performance-reliability#write-functions-to-be-stateless)[Write defensive functions](performance-reliability#write-defensive-functions)

Transient failures are common in cloud computing, so use a [retry pattern](/en-us/azure/architecture/patterns/retry) when accessing cloud-based resources. Many triggers and bindings already implement retry.

Prioritize integration testing by continuously testing your functions in the context of the full application and in your build automation pipelines.

## Design for security

Consider security during the planning phase, not after your functions are ready. For more information, see [Securing Azure Functions](security-concepts).

## Consider concurrency

As demand builds on your function app because of incoming events, Consumption and Premium plans scale out the function apps. It's important to understand how your function app responds to load and how the triggers can be configured to handle incoming events. For a general overview, see [Event-driven scaling in Azure Functions](event-driven-scaling).

Dedicated (App Service) plans require you to provide scaling for your function apps.

### Worker process count

In some cases, it's more efficient to handle the load by creating multiple processes, called language worker processes, in the instance before scale-out. The [FUNCTIONS_WORKER_PROCESS_COUNT](functions-app-settings#functions_worker_process_count) setting controls the maximum number of language worker processes allowed. The default for this setting is `1`

, which means that multiple processes aren't used. After the maximum number of processes are reached, the function app scales out to more instances to handle the load. This setting doesn't apply for [C# class library functions](functions-dotnet-class-library), which run in the host process.

When you use `FUNCTIONS_WORKER_PROCESS_COUNT`

on a Premium plan or Dedicated (App Service) plan, consider the number of cores provided by your plan. For example, the Premium plan `EP2`

provides two cores, so you should start with a value of `2`

and increase by two as needed, up to the maximum.

### Trigger configuration

When you plan for throughput and scaling, understand how the different types of triggers process events. Some triggers give you control over batching behaviors and concurrency. Adjusting these values can help each instance scale appropriately for the demands of the invoked functions. You apply these configuration options to all triggers in a function app, and maintain them in the host.json file for the app. For settings details, see the Configuration section of the specific trigger reference.

To learn more about how Functions processes message streams, see [Azure Functions reliable event processing](functions-reliable-event-processing).

### Plan for connections

Connection limits apply to function apps running in [Consumption plan](consumption-plan). These limits apply to each instance. Because of these limits and as a general best practice, optimize your outbound connections from your function code. For more information, see [Manage connections in Azure Functions](manage-connections).

### Language-specific considerations

For your language of choice, keep in mind the following considerations:

[Use cancellation tokens](functions-dotnet-class-library?#cancellation-tokens)(in-process only).

## Maximize availability

Cold start is a key consideration for serverless architectures. For more information, see [Cold starts](event-driven-scaling#cold-start). If cold start is a concern for your scenario, see [Understanding serverless cold start](https://azure.microsoft.com/blog/understanding-serverless-cold-start/).

Both Flex Consumption and Premium plans are recommended for reducing cold starts while maintaining dynamic scale. Use the following guidance to reduce cold starts and improve availability in all hosting plans.

| Plan | Guidance |
|---|---|
Flex Consumption plan |
•
•
|

**Premium plan**[Implement a Warmup trigger in your function app](functions-bindings-warmup)•

[Set the values for Always-Ready instances and Max Burst limit](functions-premium-plan#plan-and-sku-settings)•

[Use virtual network trigger support when using non-HTTP triggers on a virtual network](functions-networking-options#elastic-premium-plan-with-virtual-network-triggers)**Dedicated plans**[Run on at least two instances with Azure App Service Health Check enabled](../app-service/monitor-instances-health-check)•

[Implement autoscaling](/en-us/azure/architecture/best-practices/auto-scaling)**Consumption plan**•

[Review the](event-driven-scaling#limit-scale-out)`functionAppScaleLimit`

setting, which can limit scale-out• Check for a Daily Usage Quota (GB-Sec) limit set during development and testing. Consider removing this limit in production environments.

## Monitor effectively

Azure Functions offers built-in integration with Azure Application Insights to monitor your function execution and traces written from your code. For more information, see [Monitor executions in Azure Functions](functions-monitoring). Azure Monitor also provides facilities for monitoring the health of the function app itself. For more information, see [Monitor Azure Functions](monitor-functions).

Be aware of the following considerations when using Application Insights integration to monitor your functions:

Remove the

[AzureWebJobsDashboard](functions-app-settings#azurewebjobsdashboard)application setting. This setting was supported in older versions of Functions. Removing`AzureWebJobsDashboard`

improves the performance of your functions.Review the

[Application Insights logs](analyze-telemetry-data). If data you expect to find is missing, consider adjusting the sampling settings to better capture your monitoring scenario. Use the`excludedTypes`

setting to exclude certain types from sampling, such as`Request`

or`Exception`

. For more information, see[Configure sampling](configure-monitoring?tabs=v2#configure-sampling).

Azure Functions also allows you to [send system-generated and user-generated logs to Azure Monitor Logs](functions-monitor-log-analytics). Integration with Azure Monitor Logs is currently in preview.

## Build in redundancy

Your business needs might require that your functions always be available, even during a data center outage. To learn how to use a multiregional approach to keep your critical functions always running, see [Reliability in Azure Functions](/en-us/azure/reliability/reliability-functions).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-dotnet-dependency-injection -->

# Use dependency injection in .NET Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions supports the dependency injection (DI) software design pattern, which is a technique to achieve [Inversion of Control (IoC)](/en-us/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#dependency-inversion) between classes and their dependencies.

Dependency injection in Azure Functions is built on the .NET Core Dependency Injection features. Familiarity with

[.NET Core dependency injection](/en-us/aspnet/core/fundamentals/dependency-injection)is recommended. There are differences in how you override dependencies and how configuration values are read with Azure Functions on the Consumption plan.Support for dependency injection begins with Azure Functions 2.x.

Dependency injection patterns differ depending on whether your C# functions run

[in-process](functions-dotnet-class-library)or[out-of-process](dotnet-isolated-process-guide).

Important

The guidance in this article applies only to [C# class library functions](functions-dotnet-class-library), which run in-process with the runtime. This custom dependency injection model doesn't apply to [.NET isolated functions](dotnet-isolated-process-guide), which lets you run .NET functions out-of-process. The .NET isolated worker process model relies on regular ASP.NET Core dependency injection patterns. To learn more, see [Dependency injection](dotnet-isolated-process-guide#dependency-injection) in the .NET isolated worker process guide.

## Prerequisites

Before you can use dependency injection, you must install the following NuGet packages:

[Microsoft.NET.Sdk.Functions](https://www.nuget.org/packages/Microsoft.NET.Sdk.Functions/)package version 1.0.28 or later[Microsoft.Extensions.DependencyInjection](https://www.nuget.org/packages/Microsoft.Extensions.DependencyInjection/)(currently, only version 2.x or later supported)

## Register services

To register services, create a method to configure and add components to an `IFunctionsHostBuilder`

instance. The Azure Functions host creates an instance of `IFunctionsHostBuilder`

and passes it directly into your method.

Warning

For function apps running in the Consumption or Premium plans, modifications to configuration values used in triggers can cause scaling errors. Any changes to these properties by the `FunctionsStartup`

class results in a function app startup error.

Injection of `IConfiguration`

can lead to unexpected behavior. To learn more about adding configuration sources, see [Customizing configuration sources](#customizing-configuration-sources).

To register the method, add the `FunctionsStartup`

assembly attribute that specifies the type name used during startup.

```
using Microsoft.Azure.Functions.Extensions.DependencyInjection;
using Microsoft.Extensions.DependencyInjection;
[assembly: FunctionsStartup(typeof(MyNamespace.Startup))]
namespace MyNamespace;
public class Startup : FunctionsStartup
{
public override void Configure(IFunctionsHostBuilder builder)
{
builder.Services.AddHttpClient();
builder.Services.AddSingleton<IMyService>((s) => {
return new MyService();
});
builder.Services.AddSingleton<ILoggerProvider, MyLoggerProvider>();
}
}
```


This example uses the [Microsoft.Extensions.Http](https://www.nuget.org/packages/Microsoft.Extensions.Http/) package required to register an `HttpClient`

at startup.

### Caveats

A series of registration steps run before and after the runtime processes the startup class. Therefore, keep in mind the following items:

*The startup class is meant for only setup and registration.*Avoid using services registered at startup during the startup process. For instance, don't try to log a message in a logger that is being registered during startup. This point of the registration process is too early for your services to be available for use. After the`Configure`

method is run, the Functions runtime continues to register other dependencies, which can affect how your services operate.*The dependency injection container only holds explicitly registered types*. The only services available as injectable types are what are set up in the`Configure`

method. As a result, Functions-specific types like`BindingContext`

and`ExecutionContext`

aren't available during setup or as injectable types.*Configuring ASP.NET authentication isn't supported*. The Functions host configures ASP.NET authentication services to properly expose APIs for core lifecycle operations. Other configurations in a custom`Startup`

class can override this configuration, causing unintended consequences. For example, calling`builder.Services.AddAuthentication()`

can break authentication between the portal and the host, leading to messages such as[Azure Functions runtime is unreachable](functions-recover-storage-account#aspnet-authentication-overrides).

## Use injected dependencies

Constructor injection is used to make your dependencies available in a function. The use of constructor injection requires that you don't use static classes for injected services or for your function classes.

The following sample demonstrates how the `IMyService`

and `HttpClient`

dependencies are injected into an HTTP-triggered function.

```
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Extensions.Logging;
using System.Net.Http;
using System.Threading.Tasks;
namespace MyNamespace;
public class MyHttpTrigger
{
private readonly HttpClient _client;
private readonly IMyService _service;
public MyHttpTrigger(IHttpClientFactory httpClientFactory, IMyService service)
{
this._client = httpClientFactory.CreateClient();
this._service = service;
}
[FunctionName("MyHttpTrigger")]
public async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Function, "get", "post", Route = null)] HttpRequest req,
ILogger log)
{
var response = await _client.GetAsync("https://microsoft.com");
var message = _service.GetMessage();
return new OkObjectResult("Response from function with injected dependencies.");
}
}
```


This example uses the [Microsoft.Extensions.Http](https://www.nuget.org/packages/Microsoft.Extensions.Http/) package required to register an `HttpClient`

at startup.

## Service lifetimes

Azure Functions apps provide the same service lifetimes as [ASP.NET Dependency Injection](/en-us/aspnet/core/fundamentals/dependency-injection#service-lifetimes). For a Functions app, the different service lifetimes behave as follows:

**Transient**: Transient services are created upon each resolution of the service.**Scoped**: The scoped service lifetime matches a function execution lifetime. Scoped services are created once per function execution. Later requests for that service during the execution reuse the existing service instance.**Singleton**: The singleton service lifetime matches the host lifetime and is reused across function executions on that instance. Singleton lifetime services are recommended for connections and clients, for example`DocumentClient`

or`HttpClient`

instances.

View or download a [sample of different service lifetimes](https://github.com/Azure/azure-functions-dotnet-extensions/tree/main/src/samples/DependencyInjection/Scopes) on GitHub.

## Logging services

If you need your own logging provider, register a custom type as an instance of [ ILoggerProvider](/en-us/dotnet/api/microsoft.extensions.logging.iloggerfactory), which is available through the

[Microsoft.Extensions.Logging.Abstractions](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Abstractions/)NuGet package.

Application Insights is added by Azure Functions automatically.

Warning

- Don't add
`AddApplicationInsightsTelemetry()`

to the services collection, which registers services that conflict with services provided by the environment. - Don't register your own
`TelemetryConfiguration`

or`TelemetryClient`

if you're using the built-in Application Insights functionality. If you need to configure your own`TelemetryClient`

instance, create one via the injected`TelemetryConfiguration`

as shown in[Log custom telemetry in C# functions](functions-dotnet-class-library?tabs=v2,cmd#log-custom-telemetry-in-c-functions).

### ILogger<T> and ILoggerFactory

The host injects `ILogger<T>`

and `ILoggerFactory`

services into constructors. However, by default these new logging filters are filtered out of the function logs. You need to modify the `host.json`

file to opt in to extra filters and categories.

The following example demonstrates how to add an `ILogger<HttpTrigger>`

with logs that are exposed to the host.

```
namespace MyNamespace;
public class HttpTrigger
{
private readonly ILogger<HttpTrigger> _log;
public HttpTrigger(ILogger<HttpTrigger> log)
{
_log = log;
}
[FunctionName("HttpTrigger")]
public async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)] HttpRequest req)
{
_log.LogInformation("C# HTTP trigger function processed a request.");
// ...
}
```


The following example `host.json`

file adds the log filter.

```
{
"version": "2.0",
"logging": {
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"excludedTypes": "Request"
}
},
"logLevel": {
"MyNamespace.HttpTrigger": "Information"
}
}
}
```


For more information about log levels, see [Configure log levels](configure-monitoring#configure-log-levels).

## Function app provided services

The function host registers many services. The following services are safe to take as a dependency in your application:

| Service Type | Lifetime | Description |
|---|---|---|
`Microsoft.Extensions.Configuration.IConfiguration` |
Singleton | Runtime configuration |
`Microsoft.Azure.WebJobs.Host.Executors.IHostIdProvider` |
Singleton | Responsible for providing the ID of the host instance |

If there are other services you want to take a dependency on, [create an issue and propose them on GitHub](https://github.com/azure/azure-functions-host).

### Overriding host services

Overriding services provided by the host is currently not supported. If there are services you want to override, [create an issue and propose them on GitHub](https://github.com/azure/azure-functions-host).

## Working with options and settings

Values defined in [app settings](functions-how-to-use-azure-function-app-settings#settings) are available in an `IConfiguration`

instance, which allows you to read app settings values in the startup class.

You can extract values from the `IConfiguration`

instance into a custom type. Copying the app settings values to a custom type makes it easy test your services by making these values injectable. Settings read into the configuration instance must be simple key/value pairs. For functions running in an Elastic Premium plan, application setting names can only contain letters, numbers (`0-9`

), periods (`.`

), colons (`:`

) and underscores (`_`

). For more information, see [App setting considerations](functions-app-settings#app-setting-considerations).

Consider the following class that includes a property named consistent with an app setting:

```
public class MyOptions
{
public string MyCustomSetting { get; set; }
}
```


And a `local.settings.json`

file that might structure the custom setting as follows:

```
{
"IsEncrypted": false,
"Values": {
"MyOptions:MyCustomSetting": "Foobar"
}
}
```


From inside the `Startup.Configure`

method, you can extract values from the `IConfiguration`

instance into your custom type using the following code:

```
builder.Services.AddOptions<MyOptions>()
.Configure<IConfiguration>((settings, configuration) =>
{
configuration.GetSection("MyOptions").Bind(settings);
});
```


Calling `Bind`

copies values that have matching property names from the configuration into the custom instance. The options instance is now available in the IoC container to inject into a function.

The options object is injected into the function as an instance of the generic `IOptions`

interface. Use the `Value`

property to access the values found in your configuration.

```
using System;
using Microsoft.Extensions.Options;
public class HttpTrigger
{
private readonly MyOptions _settings;
public HttpTrigger(IOptions<MyOptions> options)
{
_settings = options.Value;
}
}
```


For more information, see [Options pattern in ASP.NET Core](/en-us/aspnet/core/fundamentals/configuration/options).

## Using ASP.NET Core user secrets

When you develop your app locally, ASP.NET Core provides a [Secret Manager tool](/en-us/aspnet/core/security/app-secrets#secret-manager) that allows you to store secret information outside the project root. It makes it less likely that secrets are accidentally committed to source control. Azure Functions Core Tools (version 3.0.3233 or later) automatically reads secrets created by the ASP.NET Core Secret Manager.

To configure a .NET Azure Functions project to use user secrets, run the following command in the project root.

```
dotnet user-secrets init
```


Then use the `dotnet user-secrets set`

command to create or update secrets.

```
dotnet user-secrets set MySecret "my secret value"
```


To access user secrets values in your function app code, use `IConfiguration`

or `IOptions`

.

## Customizing configuration sources

To specify other configuration sources, override the `ConfigureAppConfiguration`

method in your function app's `StartUp`

class.

The following sample adds configuration values from both base and optional environment-specific app settings files.

```
using System.IO;
using Microsoft.Azure.Functions.Extensions.DependencyInjection;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
[assembly: FunctionsStartup(typeof(MyNamespace.Startup))]
namespace MyNamespace;
public class Startup : FunctionsStartup
{
public override void ConfigureAppConfiguration(IFunctionsConfigurationBuilder builder)
{
FunctionsHostBuilderContext context = builder.GetContext();
builder.ConfigurationBuilder
.AddJsonFile(Path.Combine(context.ApplicationRootPath, "appsettings.json"), optional: true, reloadOnChange: false)
.AddJsonFile(Path.Combine(context.ApplicationRootPath, $"appsettings.{context.EnvironmentName}.json"), optional: true, reloadOnChange: false)
.AddEnvironmentVariables();
}
public override void Configure(IFunctionsHostBuilder builder)
{
}
}
```


Add configuration providers to the `ConfigurationBuilder`

property of `IFunctionsConfigurationBuilder`

. For more information on using configuration providers, see [Configuration in ASP.NET Core](/en-us/aspnet/core/fundamentals/configuration/#configuration-providers).

A `FunctionsHostBuilderContext`

is obtained from `IFunctionsConfigurationBuilder.GetContext()`

. Use this context to retrieve the current environment name and resolve the location of configuration files in your function app folder.

By default, configuration files such as `appsettings.json`

aren't automatically copied to the function app's output folder. Update your `.csproj`

file to match the following sample to ensure the files are copied.

```
<None Update="appsettings.json">
<CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
</None>
<None Update="appsettings.Development.json">
<CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
<CopyToPublishDirectory>Never</CopyToPublishDirectory>
</None>
```


## Next steps

For more information, see the following resources:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-target-based-scaling -->

# Target-based scaling

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Target-based scaling provides a fast and intuitive scaling model for customers and is currently supported for these binding extensions:

[Apache Kafka](#apache-kafka)[Azure Cosmos DB](#azure-cosmos-db)[Azure Event Hubs](#event-hubs)[Azure Queue Storage](#storage-queues)[Azure Service Bus (queue and topics)](#service-bus-queues-and-topics)

Target-based scaling replaces the previous Azure Functions incremental scaling model as the default for these extension types. Incremental scaling added or removed a maximum of one worker at [each new instance rate](event-driven-scaling#understanding-scaling-behaviors), with complex decisions for when to scale. In contrast, target-based scaling allows scale up of four instances at a time, and the scaling decision is based on a simple target-based equation:

In this equation, *event source length* refers to the number of events that must be processed. The default *target executions per instance* values come from the Software Development Kits (SDKs) used by the Azure Functions extensions. You don't need to make any changes for target-based scaling to work.

## Considerations

The following considerations apply when using target-based scaling:

- Target-based scaling is enabled by default for function apps on the
[Consumption plan](consumption-plan),[Flex Consumption plan](flex-consumption-plan), and[Elastic Premium plans](functions-premium-plan). Event-driven scaling isn't supported when running on[Dedicated (App Service) plans](dedicated-plan). - Target-based scaling is enabled by default starting with version 4.19.0 of the Functions runtime.
- When you use target-based scaling, scale limits are still honored. For more information, see
[Limit scale out](event-driven-scaling#limit-scale-out). - To achieve the most accurate scaling based on metrics, use only one target-based triggered function per function app. You should also consider running in a Flex Consumption plan, which offers
[per-function scaling](flex-consumption-plan#per-function-scaling). - When multiple functions in the same function app are all requesting to scale out at the same time, a sum across those functions is used to determine the change in desired instances. Functions requesting to scale out override functions requesting to scale in.
- When there are scale-in requests without any scale-out requests, the max scale in value is used.

## Opting out

Target-based scaling is enabled by default for function apps hosted on a Consumption plan or on a Premium plans. To disable target-based scaling and fall back to incremental scaling, add the following app setting to your function app:

| App Setting | Value |
|---|---|
`TARGET_BASED_SCALING_ENABLED` |
0 |

## Customizing target-based scaling

You can make the scaling behavior more or less aggressive based on your app's workload by adjusting *target executions per instance*. Each extension has different settings that you can use to set *target executions per instance*.

This table summarizes the `host.json`

values that are used for the *target executions per instance* values and the defaults:

| Extension | host.json values | Default Value |
|---|---|---|
| Event Hubs (Extension v5.x+) | extensions.eventHubs.maxEventBatchSize | 100* |
| Event Hubs (Extension v3.x+) | extensions.eventHubs.eventProcessorOptions.maxBatchSize | 10 |
| Event Hubs (if defined) | extensions.eventHubs.targetUnprocessedEventThreshold | n/a |
| Service Bus (Extension v5.x+, Single Dispatch) | extensions.serviceBus.maxConcurrentCalls | 16 |
| Service Bus (Extension v5.x+, Single Dispatch Sessions Based) | extensions.serviceBus.maxConcurrentSessions | 8 |
| Service Bus (Extension v5.x+, Batch Processing) | extensions.serviceBus.maxMessageBatchSize | 1000 |
| Service Bus (Functions v2.x+, Single Dispatch) | extensions.serviceBus.messageHandlerOptions.maxConcurrentCalls | 16 |
| Service Bus (Functions v2.x+, Single Dispatch Sessions Based) | extensions.serviceBus.sessionHandlerOptions.maxConcurrentSessions | 2000 |
| Service Bus (Functions v2.x+, Batch Processing) | extensions.serviceBus.batchOptions.maxMessageCount | 1000 |
| Storage Queue | extensions.queues.batchSize | 16 |

* The default `maxEventBatchSize`

changed in [v6.0.0](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.EventHubs/6.0.0) of the `Microsoft.Azure.WebJobs.Extensions.EventHubs`

package. In earlier versions, this value was 10.

For some binding extensions, the *target executions per instance* configuration is set using a function attribute:

| Extension | Function trigger setting | Default Value |
|---|---|---|
| Apache Kafka | `lagThreshold` |
1000 |
| Azure Cosmos DB | `maxItemsPerInvocation` |
100 |

To learn more, see the [example configurations for the supported extensions](#supported-extensions).

## Premium plan with runtime scale monitoring enabled

When [runtime scale monitoring](functions-networking-options#elastic-premium-plan-with-virtual-network-triggers) is enabled the extensions themselves handle dynamic scaling because the [scale controller](event-driven-scaling#runtime-scaling) doesn't have access to services secured by a virtual network. After you enable runtime scale monitoring, you'll need to upgrade your extension packages to these minimum versions to unlock the extra target-based scaling functionality:

| Extension Name | Minimum Version Needed |
|---|---|
| Apache Kafka | 3.9.0 |
| Azure Cosmos DB | 4.1.0 |
| Event Hubs | 5.2.0 |
| Service Bus | 5.9.0 |
| Storage Queue | 5.1.0 |

## Dynamic concurrency support

Target-based scaling introduces faster scaling, and uses defaults for *target executions per instance*. When using Service Bus, Storage queues, or Kafka, you can also enable [dynamic concurrency](functions-concurrency#dynamic-concurrency). In this configuration, the _target execution per instance value is determined automatically by the dynamic concurrency feature. It starts with limited concurrency and identifies the best setting over time.

## Supported extensions

The way in which you configure target-based scaling in your host.json file depends on the specific extension type. This section provides the configuration details for the extensions that currently support target-based scaling.

### Service Bus queues and topics

The Service Bus extension support three execution models, determined by the `IsBatched`

and `IsSessionsEnabled`

attributes of your Service Bus trigger. The default value for `IsBatched`

and `IsSessionsEnabled`

is `false`

.

| Execution Model | IsBatched | IsSessionsEnabled | Setting Used for target executions per instance |
|---|---|---|---|
| Single dispatch processing | false | false | maxConcurrentCalls |
| Single dispatch processing (session-based) | false | true | maxConcurrentSessions |
| Batch processing | true | false | maxMessageBatchSize or maxMessageCount |

Note

**Scale efficiency:** For the Service Bus extension, use *Manage* rights on resources for the most efficient scaling. With *Listen* rights, scaling reverts to incremental scale because the queue or topic length can't be used to inform scaling decisions. To learn more about setting rights in Service Bus access policies, see [Shared Access Authorization Policy](../service-bus-messaging/service-bus-sas#shared-access-authorization-policies).

#### Single dispatch processing

In this model, each invocation of your function processes a single message. The `maxConcurrentCalls`

setting governs *target executions per instance*. The specific setting depends on the version of the Service Bus extension.

Modify the `host.json`

setting `maxConcurrentCalls`

, as in the following example:

```
{
"version": "2.0",
"extensions": {
"serviceBus": {
"maxConcurrentCalls": 16
}
}
}
```


#### Single dispatch processing (session-based)

In this model, each invocation of your function processes a single message. However, depending on the number of active sessions for your Service Bus topic or queue, each instance leases one or more sessions. The specific setting depends on the version of the Service Bus extension.

Modify the `host.json`

setting `maxConcurrentSessions`

to set *target executions per instance*, as in the following example:

```
{
"version": "2.0",
"extensions": {
"serviceBus": {
"maxConcurrentSessions": 8
}
}
}
```


#### Batch processing

In this model, each invocation of your function processes a batch of messages. The specific setting depends on the version of the Service Bus extension.

Modify the `host.json`

setting `maxMessageBatchSize`

to set *target executions per instance*, as in the following example:

```
{
"version": "2.0",
"extensions": {
"serviceBus": {
"maxMessageBatchSize": 1000
}
}
}
```


### Event Hubs

For Azure Event Hubs, Azure Functions scales based on the number of unprocessed events distributed across all the partitions in the event hub within a list of valid instance counts. By default, the `host.json`

attributes used for *target executions per instance* are `maxEventBatchSize`

and `maxBatchSize`

. However, if you choose to fine-tune target-based scaling, you can define a separate parameter `targetUnprocessedEventThreshold`

that overrides to set *target executions per instance* without changing the batch settings. If `targetUnprocessedEventThreshold`

is set, the total unprocessed event count is divided by this value to determine the number of instances, which is then be rounded up to a worker instance count that creates a balanced partition distribution.

Warning

Setting `batchCheckpointFrequency`

above 1 for hosting plans supported by [target based scaling](#considerations) can cause incorrect scaling behavior. The platform calculates unprocessed events as "current position - checkpointed position", which may incorrectly indicate unprocessed messages when batches have been processed but not yet checkpointed, preventing proper scale-in when no messages remain.

#### Scaling Behavior and Stability

For Event Hubs, frequent scale-in and scale-out operations can trigger partition rebalancing, which leads to processing delays and increased latency. To mitigate this:

- The platform uses a predefined list of valid worker counts to guide scaling decisions.
- The platform ensures that scaling is stable and deliberate, avoiding disruptive changes to partition assignments.
- If the desired worker count isn't in the valid list—for example, 17, the system automatically selects the next largest valid count, which in this case is 32. Additionally, to prevent rapid repeated scaling, scale-in requests are throttled for 3 minutes after the last scale-up. This delay helps reduce unnecessary rebalancing and contributes to maintaining throughput efficiency.

#### Valid Instance Counts for Event Hubs

For each Event Hubs partition count, we calculate a corresponding list of valid instance counts to ensure optimal distribution and efficient scaling. These counts are chosen to align well with partitioning and concurrency requirements:

| Partition Count | Valid Instance Counts |
|---|---|
| 1 | [1] |
| 2 | [1, 2] |
| 4 | [1, 2, 4] |
| 8 | [1, 2, 3, 4, 8] |
| 10 | [1, 2, 3, 4, 5, 10] |
| 16 | [1, 2, 3, 4, 5, 6, 8, 16] |
| 32 | [1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 16, 32] |

These predefined counts help ensure that instances are distributed as evenly as possible across partitions, minimizing idle or overloaded workers.

Note

Note: For Premium and Dedicated event hub tiers the partition count can exceed 32, allowing for larger valid instance count sets. These tiers support higher throughput and scalability, and the valid worker count list is extended accordingly to evenly distribute event hub partitions across instances. Also, since Event Hubs is a partitioned workload, the number of partitions in your event hub is the limit for the maximum target instance count.

#### Event Hubs settings

The specific setting depends on the version of the Event Hubs extension.

Modify the `host.json`

setting `maxEventBatchSize`

to set *target executions per instance*, as in the following example:

```
{
"version": "2.0",
"extensions": {
"eventHubs": {
"maxEventBatchSize" : 100
}
}
}
```


When defined in `host.json`

, `targetUnprocessedEventThreshold`

is used as *target executions per instance* instead of `maxEventBatchSize`

, as in the following example:

```
{
"version": "2.0",
"extensions": {
"eventHubs": {
"targetUnprocessedEventThreshold": 153
}
}
}
```


### Storage Queues

For **v2.x+** of the Storage extension, modify the `host.json`

setting `batchSize`

to set *target executions per instance*:

```
{
"version": "2.0",
"extensions": {
"queues": {
"batchSize": 16
}
}
}
```


Note

**Scale efficiency:** For the storage queue extension, messages with [visibilityTimeout](/en-us/rest/api/storageservices/put-message#uri-parameters) are still counted in *event source length* by the Storage Queue APIs. This can cause overscaling of your function app. Consider using Service Bus queues que scheduled messages, [limiting scale out](event-driven-scaling#limit-scale-out), or not using visibilityTimeout for your solution.

### Azure Cosmos DB

Azure Cosmos DB uses a function-level attribute, `MaxItemsPerInvocation`

. The way you set this function-level attribute depends on your function language.

For a compiled C# function, set `MaxItemsPerInvocation`

in your trigger definition, as shown in the following examples for an in-process C# function:

```
namespace CosmosDBSamplesV2
{
public static class CosmosTrigger
{
[FunctionName("CosmosTrigger")]
public static void Run([CosmosDBTrigger(
databaseName: "ToDoItems",
collectionName: "Items",
MaxItemsPerInvocation: 100,
ConnectionStringSetting = "CosmosDBConnection",
LeaseCollectionName = "leases",
CreateLeaseCollectionIfNotExists = true)]IReadOnlyList<Document> documents,
ILogger log)
{
if (documents != null && documents.Count > 0)
{
log.LogInformation($"Documents modified: {documents.Count}");
log.LogInformation($"First document Id: {documents[0].Id}");
}
}
}
}
```


Note

Since Azure Cosmos DB is a partitioned workload, the number of physical partitions in your container is the limit for the target instance count. To learn more about Azure Cosmos DB scaling, see [physical partitions](/en-us/azure/cosmos-db/nosql/change-feed-processor#dynamic-scaling) and [lease ownership](/en-us/azure/cosmos-db/nosql/change-feed-processor#dynamic-scaling).

### Apache Kafka

The Apache Kafka extension uses a function-level attribute, `LagThreshold`

. For Kafka, the number of *desired instances* is calculated based on the total consumer lag divided by the `LagThreshold`

setting. For a given lag, reducing the lag threshold increases the number of desired instances.

The way you set this function-level attribute depends on your function language. This example sets the threshold to `100`

.

For a compiled C# function, set `LagThreshold`

in your trigger definition, as shown in the following examples for an in-process C# function for a Kafka Event Hubs trigger:

```
[FunctionName("KafkaTrigger")]
public static void Run(
[KafkaTrigger("BrokerList",
"topic",
Username = "$ConnectionString",
Password = "%EventHubConnectionString%",
Protocol = BrokerProtocol.SaslSsl,
AuthenticationMode = BrokerAuthenticationMode.Plain,
ConsumerGroup = "$Default",
LagThreshold = 100)] KafkaEventData<string> kevent, ILogger log)
{
log.LogInformation($"C# Kafka trigger function processed a message: {kevent.Value}");
}
```


## Next steps

To learn more, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-event-grid-blob-trigger -->

# Tutorial: Trigger Azure Functions on blob containers by using an event subscription

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Previous versions of the Azure Functions Blob Storage trigger poll your storage container for changes. More recent versions of the Blob Storage extension (5.x+) instead use an Event Grid event subscription on the container. This event subscription reduces latency by triggering your function instantly as changes occur in the subscribed container.

This article shows how to create a function that runs based on events raised when a blob is added to a container. You use Visual Studio Code for local development and to validate your code before deploying your project to Azure.

- Create an event-based Blob Storage triggered function in a new project.
- Validate locally within Visual Studio Code by using the Azurite emulator.
- Create a blob storage container in a new storage account in Azure.
- Create a function app in the Flex Consumption plan.
- Create an event subscription to the new blob container.
- Deploy and validate your function code in Azure.

This article supports version 4 of the Node.js programming model for Azure Functions.

This article supports version 2 of the Python programming model for Azure Functions.

This article creates a C# app that runs in isolated worker mode, which supports .NET 8.0.

Tip

This tutorial shows you how to create an app that runs on the [Flex Consumption plan](flex-consumption-plan). The Flex Consumption plan only supports the event-based version of the Blob Storage trigger.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).[C# extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)for Visual Studio Code.[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code.

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).[Node.js 14.x](https://nodejs.org/en/about/previous-releases)or above. Use the`node --version`

command to check your version.[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code. This extension installs[Azure Functions Core Tools](functions-run-local)for you the first time you locally run your functions.

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code.

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).Python versions that are

[supported by Azure Functions](supported-languages#languages-by-runtime-version). For more information, see[How to install Python](https://wiki.python.org/moin/BeginnersGuide/Download).[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)for Visual Studio Code.The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code.

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).The

[Java Development Kit](/en-us/azure/developer/java/fundamentals/java-support-on-azure), version 8, 11, 17 or 21(Linux).[Apache Maven](https://maven.apache.org), version 3.0 or above.[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code.

[Azure Storage extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurestorage)for Visual Studio Code.

Note

The Azure Storage extension for Visual Studio Code is in preview.

## Create a Blob triggered function

When you create a Blob Storage trigger function by using Visual Studio Code, you also create a new project. You need to edit the function to consume an event subscription as the source, rather than use the regular polled container.

In Visual Studio Code, press F1 to open the command palette, enter

`Azure Functions: Create Function...`

, and select**Create new project**.For your project workspace, select a directory location. Make sure that you either create a new folder or choose an empty folder for the project workspace.

Don't choose a project folder that's already part of a workspace.

At the prompts, provide the following information:

Prompt Action **Select a language**Select `C#`

.**Select a .NET runtime**Select `.NET 8.0 Isolated LTS`

.**Select a template for your project's first function**Select `Azure Blob Storage trigger (using Event Grid)`

.**Provide a function name**Enter `EventGridBlobTrigger`

.**Provide a namespace**Enter `My.Functions`

.**Select setting from "local.settings.json"**Select `Create new local app setting`

.**Select subscription**Select your subscription, if needed. **Select a storage account**Use Azurite emulator for local storage. **The path within your storage account that the trigger will monitor**Accept the default value `samples-workitems`

.**Select how you would like to open your project**Select `Open in current window`

.Prompt Action **Select a language**Select `Python`

.**Select a Python programming model**Select `Model V2`

**Select a Python interpreter to create a virtual environment**Select your preferred Python interpreter. If an option isn't shown, enter the full path to your Python binary. **Select a template for your project's first function**Select `Blob trigger`

. (The event-based template isn't yet available.)**Provide a function name**Enter `EventGridBlobTrigger`

.**The path within your storage account that the trigger will monitor**Accept the default value `samples-workitems`

.**Select setting from "local.settings.json"**Select `Create new local app setting`

.**Select subscription**Select your subscription, if needed. **Select a storage account**Use Azurite emulator for local storage. **Select how you would like to open your project**Select `Open in current window`

.Prompt Action **Select a language**Select `Java`

.**Select a version of Java**Select `Java 11`

or`Java 8`

, the Java version on which your functions run in Azure and that you've locally verified.**Provide a group ID**Select `com.function`

.**Provide an artifact ID**Select `EventGridBlobTrigger`

(or the default).**Provide a version**Select `1.0-SNAPSHOT`

.**Provide a package name**Select `com.function`

.**Provide an app name**Accept the generated name starting with `EventGridBlobTrigger`

.**Select the build tool for Java project**Select `Maven`

.**Select how you would like to open your project**Select `Open in current window`

.An HTTP triggered function (

`HttpExample`

) is created for you. You won't use this function and must instead create a new function.Prompt Action **Select a language for your function project**Select `TypeScript`

.**Select a TypeScript programming model**Select `Model V4`

.**Select a template for your project's first function**Select `Azure Blob Storage trigger (using Event Grid)`

.**Provide a function name**Enter `EventGridBlobTrigger`

.**Select setting from "local.settings.json"**Select `Create new local app setting`

.**Select subscription**Select your subscription, if needed. **Select a storage account**Use Azurite emulator for local storage. **The path within your storage account that the trigger will monitor**Accept the default value `samples-workitems`

.**Select how you would like to open your project**Select `Open in current window`

.Prompt Action **Select a language for your function project**Select `JavaScript`

.**Select a JavaScript programming model**Select `Model V4`

.**Select a template for your project's first function**Select `Azure Blob Storage trigger (using Event Grid)`

.**Provide a function name**Enter `eventGridBlobTrigger`

.**Select setting from "local.settings.json"**Select `Create new local app setting`

.**Select subscription**Select your subscription, if needed. **Select a storage account**Use Azurite emulator for local storage. **The path within your storage account that the trigger will monitor**Accept the default value `samples-workitems`

.**Select how you would like to open your project**Select `Open in current window`

.Prompt Action **Select a language for your function project**Select `PowerShell`

.**Select a template for your project's first function**Select `Azure Blob Storage trigger (using Event Grid)`

.**Provide a function name**Enter `EventGridBlobTrigger`

.**Select setting from "local.settings.json"**Select `Create new local app setting`

.**Select subscription**Select your subscription, if needed. **Select a storage account**Use Azurite emulator for local storage. **The path within your storage account that the trigger will monitor**Accept the default value `samples-workitems`

.**Select how you would like to open your project**Select `Open in current window`

.

In the command palette, enter

`Azure Functions: Create Function...`

and select`EventGridBlobTrigger`

. If you don't see this template, first select**Change template filter**>**All**.At the prompts, provide the following information:

Prompt Action **Provide a package name**Select `com.function`

.**Provide a function name**Enter `EventGridBlobTrigger`

.**Select setting from "local.settings.json"**Select `Create new local app setting`

.**Select subscription**Select your subscription. **Select a storage account**Use Azurite emulator for local storage. **The path within your storage account that the trigger will monitor**Accept the default value `samples-workitems`

.

You now have a function that can be triggered by events in a Blob Storage container.

## Update the trigger source

You need to switch the trigger source from the default Blob trigger source (container polling) to an event subscription source.

Open the function_app.py project file. You see a definition for the

`EventGridBlobTrigger`

function with the`blob_trigger`

decorator applied.Update the decorator by adding

`source = "EventGrid"`

. Your function should now look something like this:`@app.blob_trigger(arg_name="myblob", source="EventGrid", path="samples-workitems", connection="<STORAGE_ACCOUNT>") def EventGridBlobTrigger(myblob: func.InputStream): logging.info(f"Python blob trigger function processed blob" f"Name: {myblob.name}" f"Blob Size: {myblob.length} bytes")`

In this definition,

`source = "EventGrid"`

indicates that an event subscription to the`samples-workitems`

blob container is used as the source of the event that starts the trigger.

## (Optional) Review the code

Open the generated `EventGridBlobTrigger.cs`

file. You see a definition for an `EventGridBlobTrigger`

function that looks something like this:

```
[Function(nameof(EventGridBlobTriggerCSharp))]
public async Task Run([BlobTrigger("PathValue/{name}", Source = BlobTriggerSource.EventGrid, Connection = "ConnectionValue")] Stream stream, string name)
{
using var blobStreamReader = new StreamReader(stream);
var content = await blobStreamReader.ReadToEndAsync();
_logger.LogInformation("C# Blob Trigger (using Event Grid) processed blob\n Name: {name} \n Data: {content}", name, content);
}
```


In this definition, `Source = BlobTriggerSource.EventGrid`

indicates that an event subscription to the blob container (in the example `PathValue`

) is the source of the event that starts the trigger.

Open the generated `EventGridBlobTrigger.java`

file. You see a definition for an `EventGridBlobTrigger`

function that looks something like this:

```
@FunctionName("EventGridBlobTrigger")
@StorageAccount("<STORAGE_ACCOUNT>")
public void run(
@BlobTrigger(name = "content", source = "EventGrid", path = "samples-workitems/{name}", dataType = "binary") byte[] content,
@BindingName("name") String name,
final ExecutionContext context
) {
context.getLogger().info("Java Blob trigger function processed a blob. Name: " + name + "\n Size: " + content.length + " Bytes");
}
```


In this definition, `source = EventGrid`

indicates that an event subscription to the `samples-workitems`

blob container is the source of the event that starts the trigger.

In the `EventGridBlobTrigger`

folder, open the `function.json`

file and find a binding definition like this with a `type`

of `blobTrigger`

and a `source`

of `EventGrid`

:

```
{
"bindings": [
{
"name": "InputBlob",
"type": "blobTrigger",
"direction": "in",
"path": "samples-workitems/{name}",
"source": "EventGrid",
"connection":""
}
]
}
```


The `path`

indicates that the `samples-workitems`

blob container is the source of the event that starts the trigger.

Open the generated `EventGridBlobTrigger.js`

file. You see a definition for a function that looks something like this:

```
const { app } = require('@azure/functions');
app.storageBlob('storageBlobTrigger1', {
path: 'samples-workitems/{name}',
connection: 'MyStorageAccountAppSetting',
source: 'EventGrid',
handler: (blob, context) => {
context.log(
`Storage blob function processed blob "${context.triggerMetadata.name}" with size ${blob.length} bytes`
);
},
});
```


In this definition, a `source`

of `EventGrid`

indicates that an event subscription to the `samples-workitems`

blob container is the source of the event that starts the trigger.

Open the generated `EventGridBlobTrigger.ts`

file. You see a definition for a function that looks something like this:

```
import { app, InvocationContext } from '@azure/functions';
export async function storageBlobTrigger1(blob: Buffer, context: InvocationContext): Promise<void> {
context.log(
`Storage blob function processed blob "${context.triggerMetadata.name}" with size ${blob.length} bytes`
);
}
app.storageBlob('storageBlobTrigger1', {
path: 'samples-workitems/{name}',
connection: 'MyStorageAccountAppSetting',
source: 'EventGrid',
handler: storageBlobTrigger1,
});
```


In this definition, a `source`

of `EventGrid`

indicates that an event subscription to the `samples-workitems`

blob container is the source of the event that starts the trigger.

## Upgrade the Storage extension

To use the Event Grid-based Blob Storage trigger, you need version 5.x or later of the Azure Functions Storage extension.

To upgrade your project to the required extension version, run this [ dotnet add package](/en-us/dotnet/core/tools/dotnet-add-package) command in the Terminal window:

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs
```


Open the

`host.json`

project file, and review the`extensionBundle`

element.If

`extensionBundle.version`

isn't at least`3.3.0`

, replace the`extensionBundle`

element with this version:`"extensionBundle": { "id": "Microsoft.Azure.Functions.ExtensionBundle", "version": "[4.0.0, 5.0.0)" }`


## Prepare local storage emulation

Visual Studio Code uses Azurite to emulate Azure Storage services when running locally. Use Azurite to emulate the Azure Blob Storage service during local development and testing.

If you haven't already done so, install the

[Azurite v3 extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=Azurite.azurite).Verify that the

*local.settings.json*file has`"UseDevelopmentStorage=true"`

set for`AzureWebJobsStorage`

. This setting tells Core Tools to use Azurite instead of a real storage account connection when running locally.Press F1 to open the command palette, type

`Azurite: Start`

, and press Enter. This action starts the Azurite Blob Storage service emulator.Select the Azure icon in the Activity bar, expand

**Workspace**>**Attached Storage Accounts**>**Local Emulator**, right-click**Blob Containers**, select**Create Blob Container...**, enter the name`samples-workitems`

, and press Enter.Expand

**Blob Containers**>**samples-workitems**and select**Upload files...**.Choose a file to upload to the locally emulated container. Your function processes this file later to verify and debug your function code. A text file might work best with the Blob trigger template code.


## Run the function locally

With a file in emulated storage, you can run your function to simulate an event raised by an Event Grid subscription. The event info passed to your trigger depends on the file you added to the local container.

Set any breakpoints and press F5 to start your project for local debugging. Azure Functions Core Tools should be running in your Terminal window.

Back in the Azure area, expand

**Workspace**>**Local Project**>**Functions**, right-click the function, and select**Execute Function Now...**.In the request body dialog, type

`samples-workitems/<TEST_FILE_NAME>`

, replacing`<TEST_FILE_NAME>`

with the name of the file you uploaded in the local storage emulator.Press Enter to run the function. The value you provided is the path to your blob in the local emulator. This string gets passed to your trigger in the request payload, which simulates the payload when an event subscription calls your function to report a blob being added to the container.

Review the output of this function execution. You should see in the output the name of the file and its contents logged. If you set any breakpoints, you might need to continue the execution.


Now that you've successfully validated your function code locally, it's time to publish the project to a new function app in Azure.

## Prepare the Azure Storage account

Event subscriptions to Azure Storage require a general-purpose v2 storage account. You can use the Azure Storage extension for Visual Studio Code to create this storage account.

In Visual Studio Code, press F1 to open the command palette and enter

`Azure Storage: Create Storage Account...`

. Provide this information when prompted:Prompt Action **Enter the name of the new storage account**Provide a globally unique name. Storage account names must have 3 to 24 characters in length with only lowercase letters and numbers. For easier identification, use the same name for the resource group and the function app name. **Select a location for new resources**For better performance, choose a [region near you](https://azure.microsoft.com/regions/).The extension creates a general-purpose v2 storage account with the name you provide. The same name is also used for the resource group that contains the storage account. The Event Grid-based Blob Storage trigger requires a general-purpose v2 storage account.

Press F1 again and in the command palette enter

`Azure Storage: Create Blob Container...`

. Provide this information when prompted:Prompt Action **Select a resource**Select the general-purpose v2 storage account that you created. **Enter a name for the new blob container**Enter `samples-workitems`

, which is the container name referenced in your code project.

Your function app also needs a storage account to run. For simplicity, this tutorial uses the same storage account for your blob trigger and your function app. However, in production, you might want to use a separate storage account with your function app. For more information, see [Storage considerations for Azure Functions](storage-considerations).

## Create the function app

Use these steps to create a function app in the Flex Consumption plan. When you host your app in a Flex Consumption plan, Blob Storage triggers must use event subscriptions.

In the command palette, enter

**Azure Functions: Create function app in Azure...(Advanced)**.Follow the prompts and provide this information:

Prompt Selection **Enter a globally unique name for the new function app**Type a globally unique name that identifies your new function app and then select Enter. Valid characters for a function app name are `a-z`

,`0-9`

, and`-`

.**Select a hosting plan**Choose **Flex Consumption**, which is the recommended[hosting plan](functions-scale)for serverless hosting.**Select a location for new resources**Select a location in a [region](https://azure.microsoft.com/regions/)near you or near other services that your functions access.**Select a runtime stack**Select the language version you currently run locally. **Select an instance size**Select **512**. You can always[change the instance size](flex-consumption-how-to#configure-instance-memory)setting to a larger size later.**Enter the maximum instance count**Select the default value of **100**, which limits the total scale-out of your app. You can also choose a different value between 1 and 1,000.**Select a resource group**Select **Create new resource group**and accept the default or enter another name for the new group that's unique in your subscription.**Select resource authentication type**Select **Managed identity**so that your app connects to remote resources by using Microsoft Entra ID authentication instead of using shared secrets (connection strings and keys), which are less secure.**Select a user assigned identity**Select **Create new user-assigned identity**.**Select a location for new resources**Select the same region as the storage account you created. If for some reason this region isn't supported by the Flex Consumption play, it isn't displayed. In that case, choose a nearby [region](https://azure.microsoft.com/regions/)instead. For more information, see[View currently supported regions](flex-consumption-how-to#view-currently-supported-regions).**Select a storage account**Choose the name of the storage account you created. **Select an Application Insights resource for your app**Choose **Create new Application Insights resource**and at the prompt provide the name for the instance used to store runtime data from your functions.A notification appears after your function app is created. Select

**View Output**in this notification to view the creation results, including the Azure resources that you created.

## Deploy your function code

Important

Deploying to an existing function app always overwrites the contents of that app in Azure.

In the command palette, enter and then select

**Azure Functions: Deploy to Function App**.Select the function app you just created. When prompted about overwriting previous deployments, select

**Deploy**to deploy your function code to the new function app resource.When deployment is completed, select

**View Output**to view the creation and deployment results, including the Azure resources that you created. If you miss the notification, select the bell icon in the lower-right corner to see it again.

## Update application settings

Because the publishing process doesn't automatically upload required application settings from the `local.settings.json`

file, you must upload them to your function app so that your function runs correctly in Azure.

In the command palette, enter

`Azure Functions: Download Remote Settings...`

, and in the**Select a resource**prompt choose the name of your function app.When prompted that the

`AzureWebJobsStorage`

setting already exists, select**Yes**to overwrite the local emulator setting with the actual storage account connection string from Azure.In the

`local.settings.json`

file, replace the local emulator setting with same connection string used for`AzureWebJobsStorage`

.Remove the

`FUNCTIONS_WORKER_RUNTIME`

entry, which isn't supported in a Flex Consumption plan.In the command palette, enter

`Azure Functions: Upload Local Settings...`

, and in the**Select a resource**prompt choose the name of your function app.

Now both the Functions host and the trigger share the same storage account.

## Build the endpoint URL

To create an event subscription, you need to provide Event Grid with the URL of the specific endpoint to report Blob Storage events. This *blob extension* URL is composed of these parts:

| Part | Example |
|---|---|
| Base function app URL | `https://<FUNCTION_APP_NAME>.azurewebsites.net` |
| Blob-specific path | `/runtime/webhooks/blobs` |
| Function query string | `?functionName=Host.Functions.<FUNCTION_NAME>` |
| Blob extension access key | `&code=<BLOB_EXTENSION_KEY>` |

While your app connects to the storage account by using Microsoft Entra ID authentication, the blob extension access key helps protect your blob extension webhook from unauthorized access. To find your blob extension access key:

In Visual Studio Code, select the Azure icon in the Activity bar. In

**Resources**, expand your subscription, expand**Function App**, right-click the function app you created, and select**Open in portal**.Under

**Functions**in the left menu, select**App keys**.Under

**System keys**, select the key named**blobs_extension**, and copy the key**Value**.Include this value in the query string of the new endpoint URL.

Create a new endpoint URL for the Blob Storage trigger based on the following example:

`https://<FUNCTION_APP_NAME>.azurewebsites.net/runtime/webhooks/blobs?functionName=Host.Functions.EventGridBlobTrigger&code=<BLOB_EXTENSION_KEY>`

In this example, replace

`<FUNCTION_APP_NAME>`

with the name of your function app, and`<BLOB_EXTENSION_KEY>`

with the value you got from the portal. If you used a different name for your function, replace`EventGridBlobTrigger`

with that function name.

You can now use this endpoint URL to create an event subscription.

## Create the event subscription

An event subscription, powered by Azure Event Grid, raises events based on changes in the subscribed blob container. This event is then sent to the blob extension endpoint for your function. After you create an event subscription, you can't update the endpoint URL.

In Visual Studio Code, choose the Azure icon in the Activity bar. In

**Resources**, expand your subscription, expand**Storage accounts**, right-click the storage account you created earlier, and select**Open in portal**.Sign in to the

[Azure portal](https://portal.azure.com)and make a note of the**Resource group**for your storage account. Create your other resources in the same group to make it easier to clean up resources when you're done.Select the

**Events**option from the left menu.In the

**Events**window, select the**+ Event Subscription**button, and provide values from the following table into the**Basic**tab:Setting Suggested value Description **Name***myBlobEventSub*Name that identifies the event subscription. Use the name to quickly find the event subscription. **Event Schema****Event Grid Schema**Use the default schema for events. **System Topic Name***samples-workitems-blobs*Name for the topic, which represents the container. The topic is created with the first subscription, and you use it for future event subscriptions. **Filter to Event Types***Blob Created***Endpoint Type****Web Hook**The blob storage trigger uses a web hook endpoint. **Endpoint**Your Azure-based URL endpoint Use the URL endpoint that you built, which includes the key value. Select

**Confirm selection**to validate the endpoint URL.Select the

**Filters**tab and provide the following information to the prompts:Setting Suggested value Description **Enable subject filtering***Enabled*Enables filtering on which blobs can trigger the function. **Subject Begins With**`/blobServices/default/containers/<CONTAINER_NAME>/blobs/<BLOB_PREFIX>`

Replace `<CONTAINER_NAME`

and`<BLOB_PREFIX>`

with values you choose. This setting triggers the subscription only for blobs that start with`BLOB_PREFIX`

and are in the`CONTAINER_NAME`

container.**Subject Ends With***.txt*Ensures that the function is only triggered by blobs ending with `.txt`

.For more information on filtering to specific blobs, see

[Event Filtering for Azure Event Hubs](../event-grid/event-filtering).Select

**Create**to create the event subscription.

## Upload a file to the container

You can upload a file from your computer to your blob storage container by using Visual Studio Code.

In Visual Studio Code, press F1 to open the command palette and type

`Azure Storage: Upload Files...`

.In the

**Open**dialog box, choose a file, preferably a text file, and select**Upload**.Provide the following information at the prompts:

Setting Suggested value Description **Enter the destination directory of this upload**default Accept the default value of `/`

, which is the container root.**Select a resource**Storage account name Choose the name of the storage account you created in a previous step. **Select a resource type****Blob Containers**You're uploading to a blob container. **Select Blob Container****samples-workitems**This value is the name of the container you created in a previous step.

Browse your local file system to find a file to upload, then select the **Upload** button to upload the file.

## Verify the function in Azure

When you upload a file to the **samples-workitems** container, the function triggers. You can verify the function by checking the following items on the Azure portal:

In your storage account, go to the

**Events**page, select**Event Subscriptions**, and you should see that an event was delivered. There might be up to a five-minute delay for the event to show up on the chart.Back in your function app page in the portal, under

**Functions**find your function and select**Invocations and more**. You should see traces written from your successful function execution.

## Clean up resources

When you continue to the [next step](#next-steps) and add an Azure Storage queue binding to your function, you'll need to keep all your resources in place to build on what you've already done.

Otherwise, you can use the following steps to delete the function app and its related resources to avoid incurring any further costs.

In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azure: Open in portal`

.Choose your function app and press

`Enter`. The function app page opens in the Azure portal.In the

**Overview**tab, select the named link next to**Resource group**.On the

**Resource group**page, review the list of included resources, and verify that they're the ones you want to delete.Select

**Delete resource group**, and follow the instructions.Deletion may take a couple of minutes. When it's done, a notification appears for a few seconds. You can also select the bell icon at the top of the page to view the notification.


For more information about Functions costs, see [Estimating Consumption plan costs](functions-consumption-costs).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-mysql-output -->

# Azure Database for MySQL output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can use the Azure Database for MySQL output binding to write to a database.

For information on setup and configuration, see the [overview](functions-bindings-azure-mysql).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

## Examples

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

More samples for the Azure Database for MySQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples).

This section contains the following example:

The example refers to a `Product`

class and a corresponding database table:

```
namespace AzureMySqlSamples.Common
{
public class Product
{
public int? ProductId { get; set; }
public string Name { get; set; }
public int Cost { get; set; }
public override bool Equals(object obj)
}
}
```


```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


### HTTP trigger, write one record

The following example shows a [C# function](functions-dotnet-class-library) that adds a record to a database, by using data provided in an HTTP `POST`

request as a JSON body.

```
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.MySql;
using Microsoft.Azure.Functions.Worker.Http;
using AzureMySqlSamples.Common;
namespace AzureMySqlSamples.OutputBindingSamples
{
public static class AddProduct
{
[FunctionName(nameof(AddProduct))]
public static IActionResult Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "post", Route = "addproduct")]
[FromBody] Product prod,
[MySql("Products", "MySqlConnectionString")] out Product product)
{
product = prod;
return new CreatedResult($"/api/addproduct", product);
}
}
}
```


More samples for the Azure Database for MySQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-java).

This section contains the following example:

The example refers to a `Product`

class and a corresponding database table:

```
package com.function.Common;
import com.fasterxml.jackson.annotation.JsonProperty;
public class Product {
@JsonProperty("ProductId")
private int ProductId;
@JsonProperty("Name")
private String Name;
@JsonProperty("Cost")
private int Cost;
public Product() {
}
public Product(int productId, String name, int cost) {
ProductId = productId;
Name = name;
Cost = cost;
}
}
```


```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


### HTTP trigger, write a record to a table

The following example shows an Azure Database for MySQL output binding in a Java function that adds a record to a table, by using data provided in an HTTP `POST`

request as a JSON body. The function takes an additional dependency on the [com.google.code.gson](https://github.com/google/gson) library to parse the JSON body.

```
<dependency>
<groupId>com.google.code.gson</groupId>
<artifactId>gson</artifactId>
<version>2.10.1</version>
</dependency>
```


```
package com.function;
import com.microsoft.azure.functions.HttpMethod;
import com.microsoft.azure.functions.HttpRequestMessage;
import com.microsoft.azure.functions.HttpResponseMessage;
import com.microsoft.azure.functions.HttpStatus;
import com.microsoft.azure.functions.OutputBinding;
import com.microsoft.azure.functions.annotation.AuthorizationLevel;
import com.microsoft.azure.functions.annotation.FunctionName;
import com.microsoft.azure.functions.annotation.HttpTrigger;
import com.microsoft.azure.functions.mysql.annotation.MySqlOutput;
import com.fasterxml.jackson.core.JsonParseException;
import com.fasterxml.jackson.databind.JsonMappingException;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.function.Common.Product;
import java.io.IOException;
import java.util.Optional;
public class AddProduct {
@FunctionName("AddProduct")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "addproduct")
HttpRequestMessage<Optional<String>> request,
@MySqlOutput(
name = "product",
commandText = "Products",
connectionStringSetting = "MySqlConnectionString")
OutputBinding<Product> product) throws JsonParseException, JsonMappingException, IOException {
String json = request.getBody().get();
ObjectMapper mapper = new ObjectMapper();
Product p = mapper.readValue(json, Product.class);
product.setValue(p);
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(product).build();
}
}
```


More samples for the Azure Database for MySQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples).

This section contains the following example:

The example refers to a database table:

```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


### HTTP trigger, write records to a table

The following example shows an Azure Database for MySQL output binding that adds records to a table, by using data provided in an HTTP `POST`

request as a JSON body.

```
const { app, output } = require('@azure/functions');
const mysqlOutput = output.generic({
type: 'mysql',
commandText: 'Products',
connectionStringSetting: 'MySqlConnectionString'
})
// Upsert the product, which will insert it into the Products table if the primary key (ProductId) for that item doesn't exist.
// If it does, update it to have the new name and cost.
app.http('AddProduct', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [mysqlOutput],
handler: async (request, context) => {
// Note that this expects the body to be a JSON object or array of objects that have a property
// matching each of the columns in the table to upsert to.
const product = await request.json();
context.extraOutputs.set(mysqlOutput, product);
return {
status: 201,
body: JSON.stringify(product)
};
}
});
```


```
const { app, output } = require('@azure/functions');
const mysqlOutput = output.generic({
type: 'mysql',
commandText: 'Products',
connectionStringSetting: 'MySqlConnectionString'
})
// Upsert the product, which will insert it into the Products table if the primary key (ProductId) for that item doesn't exist.
// If it does, update it to have the new name and cost.
app.http('AddProduct', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [mysqlOutput],
handler: async (request, context) => {
// Note that this expects the body to be a JSON object or array of objects that have a property
// matching each of the columns in the table to upsert to.
const product = await request.json();
context.extraOutputs.set(mysqlOutput, product);
return {
status: 201,
body: JSON.stringify(product)
};
}
});
```


More samples for the Azure Database for MySQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-powershell).

This section contains the following example:

The example refers to a database table:

```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


### HTTP trigger, write records to a table

The following example shows an Azure Database for MySQL output binding in a function.json file and a PowerShell function that adds records to a table, by using data provided in an HTTP `POST`

request as a JSON body.

The following example is binding data in the function.json file:

```
{
"bindings": [
{
"authLevel": "function",
"name": "Request",
"direction": "in",
"type": "httpTrigger",
"methods": [
"post"
],
"route": "addproduct"
},
{
"name": "response",
"type": "http",
"direction": "out"
},
{
"name": "product",
"type": "mysql",
"direction": "out",
"commandText": "Products",
"connectionStringSetting": "MySqlConnectionString"
}
],
"disabled": false
}
```


The [Configuration](#configuration) section explains these properties.

The following example is sample PowerShell code for the function in the run.ps1 file:

```
using namespace System.Net
# Trigger binding data passed in via parameter block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell function with MySql Output Binding processed a request."
# Note that this expects the body to be a JSON object or array of objects
# that have a property matching each of the columns in the table to upsert to.
$req_body = $Request.Body
# Assign the value that you want to pass to the MySQL output binding.
# The -Name value corresponds to the name property in the function.json file for the binding.
Push-OutputBinding -Name product -Value $req_body
# Assign the value to return as the HTTP response.
# The -Name value matches the name property in the function.json file for the binding.
Push-OutputBinding -Name response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $req_body
})
```


More samples for the Azure Database for MySQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-python).

This section contains the following example:

The example refers to a database table:

```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


Note

You must use Azure Functions version 1.22.0b4 for Python.

### HTTP trigger, write records to a table

The following example shows an Azure Database for MySQL output binding in a function.json file and a Python function that adds records to a table, by using data provided in an HTTP `POST`

request as a JSON body.

The following example is sample Python code for the function_app.py file:

```
import json
import azure.functions as func
app = func.FunctionApp(http_auth_level=func.AuthLevel.ANONYMOUS)
@app.generic_trigger(arg_name="req", type="httpTrigger", route="addproduct")
@app.generic_output_binding(arg_name="$return", type="http")
@app.generic_output_binding(arg_name="r", type="mysql",
command_text="Products",
connection_string_setting="MySqlConnectionString")
def mysql_output(req: func.HttpRequest, r: func.Out[func.MySqlRow]) \
-> func.HttpResponse:
body = json.loads(req.get_body())
row = func.MySqlRow.from_dict(body)
r.set(row)
return func.HttpResponse(
body=req.get_body(),
status_code=201,
mimetype="application/json"
)
```


## Attributes

The [C# library](functions-dotnet-class-library) uses the `MySqlAttribute`

attribute to declare the MySQL bindings on the function, which has the following properties:

| Attribute property | Description |
|---|---|
`CommandText` |
Required. The name of the table that the binding writes to. |
`ConnectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database to which data is written. This value isn't the actual connection string and must instead resolve to an environment variable. |

## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@MySQLOutput`

annotation on parameters whose value would come from Azure Database for MySQL. This annotation supports the following elements:

| Element | Description |
|---|---|
`commandText` |
Required. The name of the table that the binding writes to. |
`connectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database to which data is written. This value isn't the actual connection string and must instead resolve to an environment variable. |
`name` |
Required. The unique name of the function binding. |

## Configuration

The following table explains the properties that you can set on the `options`

object passed to the `output.generic()`

method:

| Property | Description |
|---|---|
`commandText` |
Required. The name of the table that the binding writes to. |
`connectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database to which data is written. This value isn't the actual connection string and must instead resolve to an environment variable. |

## Configuration

The following table explains the binding configuration properties that you set in the function.json file:

| Property | Description |
|---|---|
`type` |
Required. Must be set to `Mysql` . |
`direction` |
Required. Must be set to `out` . |
`name` |
Required. The name of the variable that represents the entity in function code. |
`commandText` |
Required. The name of the table that the binding writes to. |
`connectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database to which data is written. This value isn't the actual connection string and must instead resolve to an environment variable. |

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

Note

The output binding supports all special characters, including dollar sign ($), backtick (`), hyphen (-), and underscore (_). For more information, see the [MySQL community documentation](https://dev.mysql.com/doc/refman/8.0/en/identifiers.html).

A programming language might define member attributes that contain special characters that it supports. For example, C# has a few limitations for defining [variables](/en-us/dotnet/csharp/fundamentals/coding-style/identifier-names).

Otherwise, you can use `JObject`

for the output binding that covers all special characters. You can follow a [detailed example on GitHub](https://github.com/Azure/azure-functions-mysql-extension/blob/main/samples/samples-csharp/OutputBindingSamples/AddProductJObject.cs).

## Usage

The `CommandText`

property is the name of the table where the data is stored. The name of the connection string setting corresponds to the application setting that contains the connection string to Azure Database for MySQL.

If an exception occurs when a MySQL input binding is executed, the function code won't run. The result might be an error code, such as an HTTP trigger that returns a 500 error code.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr-output-publish -->

# Dapr Publish output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Dapr publish output binding allows you to publish a message to a Dapr topic during a function execution.

For information on setup and configuration details of the Dapr extension, see the [Dapr extension overview](functions-bindings-dapr).

## Example

A C# function can be created using one of the following C# modes:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).The following example demonstrates using a Dapr publish output binding to perform a Dapr publish operation to a pub/sub component and topic.

```
[FunctionName("PublishOutputBinding")]
public static void Run(
[HttpTrigger(AuthorizationLevel.Function, "post", Route = "topic/{topicName}")] HttpRequest req,
[DaprPublish(PubSubName = "%PubSubName%", Topic = "{topicName}")] out DaprPubSubEvent pubSubEvent,
ILogger log)
{
string requestBody = new StreamReader(req.Body).ReadToEnd();
pubSubEvent = new DaprPubSubEvent(requestBody);
}
```


The following example creates a `"TransferEventBetweenTopics"`

function using the `DaprPublishOutput`

binding with an [ DaprTopicTrigger](functions-bindings-dapr-trigger-topic):

```
@FunctionName("TransferEventBetweenTopics")
public String run(
@DaprTopicTrigger(
pubSubName = "%PubSubName%",
topic = "A")
String request,
@DaprPublishOutput(
pubSubName = "%PubSubName%",
topic = "B")
OutputBinding<String> payload,
final ExecutionContext context) throws JsonProcessingException {
context.getLogger().info("Java function processed a TransferEventBetweenTopics request from the Dapr Runtime.");
}
```


In the following example, the Dapr publish output binding is paired with an HTTP trigger, which is registered by the `app`

object:

```
const { app, trigger } = require('@azure/functions');
app.generic('PublishOutputBinding', {
trigger: trigger.generic({
type: 'httpTrigger',
authLevel: 'anonymous',
methods: ['POST'],
route: "topic/{topicName}",
name: "req"
}),
return: daprPublishOutput,
handler: async (request, context) => {
context.log("Node HTTP trigger function processed a request.");
const payload = await request.text();
context.log(JSON.stringify(payload));
return { payload: payload };
}
});
```


The following examples show Dapr triggers in a *function.json* file and PowerShell code that uses those bindings.

Here's the *function.json* file for `daprPublish`

:

```
{
"bindings":
{
"type": "daprPublish",
"direction": "out",
"name": "pubEvent",
"pubsubname": "%PubSubName%",
"topic": "B"
}
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

In code:

```
using namespace System
using namespace Microsoft.Azure.WebJobs
using namespace Microsoft.Extensions.Logging
using namespace Microsoft.Azure.WebJobs.Extensions.Dapr
using namespace Newtonsoft.Json.Linq
# Example to use Dapr Service Invocation Trigger and Dapr State Output binding to persist a new state into statestore
param (
$subEvent
)
Write-Host "PowerShell function processed a TransferEventBetweenTopics request from the Dapr Runtime."
# Convert the object to a JSON-formatted string with ConvertTo-Json
$jsonString = $subEvent["data"]
$messageFromTopicA = "Transfer from Topic A: $jsonString".Trim()
$publish_output_binding_req_body = @{
"payload" = $messageFromTopicA
}
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name pubEvent -Value $publish_output_binding_req_body
```


The following example shows a Dapr Publish output binding, which uses the [v2 Python programming model](functions-reference-python). To use `daprPublish`

in your Python function app code:

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="TransferEventBetweenTopics")
@app.dapr_topic_trigger(arg_name="subEvent", pub_sub_name="%PubSubName%", topic="A", route="A")
@app.dapr_publish_output(arg_name="pubEvent", pub_sub_name="%PubSubName%", topic="B")
def main(subEvent, pubEvent: func.Out[bytes]) -> None:
logging.info('Python function processed a TransferEventBetweenTopics request from the Dapr Runtime.')
subEvent_json = json.loads(subEvent)
payload = "Transfer from Topic A: " + str(subEvent_json["data"])
pubEvent.set(json.dumps({"payload": payload}).encode('utf-8'))
```


## Attributes

In the [in-process model](functions-dotnet-class-library), use the `DaprPublish`

to define a Dapr publish output binding, which supports these parameters:

| function.json property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
PubSubName |
The name of the Dapr pub/sub to send the message. | ✔️ | ✔️ |
Topic |
The name of the Dapr topic to send the message. | ✔️ | ✔️ |
Payload |
Required. The message being published. |
❌ | ✔️ |

## Annotations

The `DaprPublishOutput`

annotation allows you to have a function access a published message.

| Element | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
pubSubName |
The name of the Dapr pub/sub to send the message. | ✔️ | ✔️ |
topic |
The name of the Dapr topic to send the message. | ✔️ | ✔️ |
payload |
Required. The message being published. |
❌ | ✔️ |

## Configuration

The following table explains the binding configuration properties that you set in the code.

| Property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
pubsubname |
The name of the publisher component service. | ✔️ | ✔️ |
topic |
The name/identifier of the publisher topic. | ✔️ | ✔️ |
payload |
Required. The message being published. |
❌ | ✔️ |

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
pubsubname |
The name of the publisher component service. | ✔️ | ✔️ |
topic |
The name/identifier of the publisher topic. | ✔️ | ✔️ |
payload |
Required. The message being published. |
❌ | ✔️ |

The following table explains the binding configuration properties for `@dapp.dapr_publish_output`

that you set in your Python code.

| Property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
pub_sub_name |
The name of the publisher event. | ✔️ | ✔️ |
topic |
The publisher topic name/identifier. | ✔️ | ✔️ |
payload |
Required. The message being published. |
❌ | ✔️ |

If properties are defined in both Attributes and `RequestBody`

, priority is given to data provided in `RequestBody`

.

See the [Example section](#example) for complete examples.

## Usage

To use the Dapr publish output binding, start by setting up a Dapr pub/sub component. You can learn more about which component to use and how to set it up in the official Dapr documentation.

To use the `daprPublish`

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-register -->

# Register Azure Functions binding extensions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Functions runtime natively runs HTTP and timer triggers. The behaviors of the other supported [triggers and bindings](functions-triggers-bindings) are implemented in separate extension packages.

Projects that use a .NET class library use binding extensions that are installed in the project as NuGet packages.

Extension bundles allow non-.NET apps to use binding extensions without having to interact with .NET infrastructure.

## Extension bundles

Extension bundles add a predefined set of compatible binding extensions to your function app. Extension bundles are versioned. Each version contains a specific set of binding extensions that are verified to work together. Select a bundle version based on the extensions that you need in your app.

When you create an Azure Functions project from a non-.NET template, extension bundles are already enabled in the app's `host.json`

file.

When possible, use the latest version range to obtain optimal app performance and access to the latest features. To learn more about extension bundles, see [Azure Functions extension bundles](extension-bundles).

In the unlikely event that you can't use an extension bundle, you must instead explicitly install extensions.

## Explicitly install extensions

For projects that use a compiled C# class library, you install the NuGet packages for the extensions that you need as you normally would in your apps. For more information, see the [Visual Studio Code developer guide](functions-develop-vs-code?tabs=csharp#install-binding-extensions) or the [Visual Studio developer guide](functions-develop-vs#add-bindings).

Make sure to obtain the correct package, because the namespace differs depending on the execution model:

| Execution model | Namespace |
|---|---|
|

`Microsoft.Azure.Functions.Worker.Extensions.*`

[In-process](functions-dotnet-class-library)`Microsoft.Azure.WebJobs.Extensions.*`

Azure Functions provides extension bundles for non-.NET projects. These bundles contain a full set of binding extensions that are verified to be compatible. If you're having compatibility problems between two or more binding extensions, review compatible combinations of extension versions. For supported combinations of binding extensions, see the [release page for extension bundles](https://github.com/Azure/azure-functions-extension-bundles/releases).

There are cases when you can't use extension bundles, such as when you need to use a specific prerelease version of a specific extension. In these rare cases, you must manually install any required binding extensions in a C# project file that references the specific extensions that your app requires.

To manually install binding extensions:

Remove the extension bundle reference from your

`host.json`

file.Use the

command in Azure Functions Core Tools to generate the required`func extensions install`

`extensions.csproj`

file in the root of your local project.For portal-only development, you need to manually create an

`extensions.csproj`

file in the root of your function app in Azure. To learn more, see[Manually install extensions](functions-how-to-use-azure-function-app-settings#manually-install-extensions).Edit the

`extensions.csproj`

file by explicitly adding a`PackageReference`

element for every specific binding extension and version that your app requires.Validate your app functionality locally and then redeploy your project, including

`extensions.csproj`

, to your function app in Azure.

As soon as possible, you should [switch your app back to using the latest supported extension bundle](extension-bundles#define-an-extension-bundle-reference).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/errors-diagnostics/diagnostic-events/azfd0013 -->

# AZFD0013: The configured runtime does not match the worker runtime metadata found in the deployed function app artifacts

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This event occurs when a function app has a `FUNCTIONS_WORKER_RUNTIME`

setting specifying a language stack, but a payload for a different stack is deployed to it.

| Value | |
|---|---|
Event ID |
AZFD0013 |
Severity |
Warning or Error |

## Event description

The `FUNCTIONS_WORKER_RUNTIME`

application setting indicates the language or language stack on which the function app runs, such as `python`

. For more information on valid values, see the [ FUNCTIONS_WORKER_RUNTIME](../../functions-app-settings#functions_worker_runtime) reference. The deployed application must correspond with the provided value. If there is a mismatch, it means that either the value of

`FUNCTIONS_WORKER_RUNTIME`

is incorrect, or that an unexpected payload was deployed to the application.This event may appear for apps that were previously using inconsistent and undefined behavior to continue running while in a mismatch state. Follow the instructions in this article to resolve the event for these applications. Doing so allows these apps to take advantage of performance enhancements and ensure that they can continue to operate as expected.

.NET apps undergoing a [migration from the in-process model to the isolated worker](../../migrate-dotnet-to-isolated-model) may encounter this event temporarily during that process. When `FUNCTIONS_WORKER_RUNTIME`

is updated to `dotnet-isolated`

, but the application is still using an in-process model payload, this event may appear until the migration is completed. See the migration guidance for instructions on using deployment slots to prevent this event from appearing in your production environment.

## How to resolve the event

The event message indicates the current value of `FUNCTIONS_WORKER_RUNTIME`

and the detected runtime metadata from the app payload. These values must be aligned, either by deploying an application payload of the appropriate type or by updating the setting to an expected value

For most applications, the correct resolution is to update the value of [ FUNCTIONS_WORKER_RUNTIME](../../functions-app-settings#functions_worker_runtime). To do so, on your function app in Azure, set the

`FUNCTIONS_WORKER_RUNTIME`

[application setting](../../functions-how-to-use-azure-function-app-settings#settings)to the expected value for your application payload. The expected value is not necessarily the same as the detected runtime metadata, though in many cases it will be. Use the following table to determine the correct value to use:

| Detected payload | Expected `FUNCTIONS_WORKER_RUNTIME` value |
|---|---|
`CSharp` |
`dotnet` |
`custom` |
`custom` |
`dotnet` |
`dotnet` |
`dotnet-isolated` |
`dotnet-isolated` |
`java` |
`java` |
`node` |
`node` |
`powershell` |
`powershell` |
`python` |
`python` |
Any multi-stack payload1 |
`dotnet` |

1 A multi-stack payload is a comma-separated list of stack values. Multi-stack payloads are only supported for [Logic Apps Standard](../../../logic-apps/single-tenant-overview-compare).

When running locally in the Azure Functions Core Tools, you should also add `FUNCTIONS_WORKER_RUNTIME`

to the [local.settings.json file](../../functions-develop-local#local-settings-file).

For apps following a migration guide, see that guide for relevant instructions. [Migrating .NET applications to the isolated worker model](../../migrate-dotnet-to-isolated-model) involves first setting `FUNCTIONS_WORKER_RUNTIME`

to `dotnet-isolated`

before deploying the updated application payload, and this event may appear temporarily between those steps.

## When to suppress the event

This event shouldn't be suppressed.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-sql-input -->

# Azure SQL input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When a function runs, the Azure SQL input binding retrieves data from a database and passes it to the input parameter of the function.

For information on setup and configuration details, see the [overview](functions-bindings-azure-sql).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

## Examples

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

More samples for the Azure SQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-outofproc).

This section contains the following examples:

[HTTP trigger, get row by ID from query string](#http-trigger-look-up-id-from-query-string-c-oop)[HTTP trigger, get multiple rows from route data](#http-trigger-get-multiple-items-from-route-data-c-oop)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-c-oop)

The examples refer to a `ToDoItem`

class and a corresponding database table:

```
namespace AzureSQL.ToDo
{
public class ToDoItem
{
public Guid Id { get; set; }
public int? order { get; set; }
public string title { get; set; }
public string url { get; set; }
public bool? completed { get; set; }
}
}
```


```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


### HTTP trigger, get row by ID from query string

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a single record. The function is [triggered by an HTTP request](functions-bindings-http-webhook-trigger) that uses a query string to specify the ID. That ID is used to retrieve a `ToDoItem`

record with the specified query.

Note

The HTTP query string parameter is case-sensitive.

```
using System.Collections.Generic;
using System.Linq;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.Sql;
using Microsoft.Azure.Functions.Worker.Http;
namespace AzureSQLSamples
{
public static class GetToDoItem
{
[FunctionName("GetToDoItem")]
public static IActionResult Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "gettodoitem")]
HttpRequest req,
[SqlInput(commandText: "select [Id], [order], [title], [url], [completed] from dbo.ToDo where Id = @Id",
commandType: System.Data.CommandType.Text,
parameters: "@Id={Query.id}",
connectionStringSetting: "SqlConnectionString")]
IEnumerable<ToDoItem> toDoItem)
{
return new OkObjectResult(toDoItem.FirstOrDefault());
}
}
}
```


### HTTP trigger, get multiple rows from route parameter

The following example shows a [C# function](functions-dotnet-class-library) that retrieves documents returned by the query. The function is [triggered by an HTTP request](functions-bindings-http-webhook-trigger) that uses route data to specify the value of a query parameter. That parameter is used to filter the `ToDoItem`

records in the specified query.

```
using System.Collections.Generic;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.Sql;
using Microsoft.Azure.Functions.Worker.Http;
namespace AzureSQLSamples
{
public static class GetToDoItems
{
[FunctionName("GetToDoItems")]
public static IActionResult Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "gettodoitems/{priority}")]
HttpRequest req,
[SqlInput(commandText: "select [Id], [order], [title], [url], [completed] from dbo.ToDo where [Priority] > @Priority",
commandType: System.Data.CommandType.Text,
parameters: "@Priority={priority}",
connectionStringSetting: "SqlConnectionString")]
IEnumerable<ToDoItem> toDoItems)
{
return new OkObjectResult(toDoItems);
}
}
}
```


### HTTP trigger, delete rows

The following example shows a [C# function](functions-dotnet-class-library) that executes a stored procedure with input from the HTTP request query parameter.

The stored procedure `dbo.DeleteToDo`

must be created on the SQL database. In this example, the stored procedure deletes a single record or all records depending on the value of the parameter.

```
CREATE PROCEDURE [dbo].[DeleteToDo]
@Id NVARCHAR(100)
AS
DECLARE @UID UNIQUEIDENTIFIER = TRY_CAST(@ID AS UNIQUEIDENTIFIER)
IF @UId IS NOT NULL AND @Id != ''
BEGIN
DELETE FROM dbo.ToDo WHERE Id = @UID
END
ELSE
BEGIN
DELETE FROM dbo.ToDo WHERE @ID = ''
END
SELECT [Id], [order], [title], [url], [completed] FROM dbo.ToDo
GO
```


```
namespace AzureSQL.ToDo
{
public static class DeleteToDo
{
// delete all items or a specific item from querystring
// returns remaining items
// uses input binding with a stored procedure DeleteToDo to delete items and return remaining items
[FunctionName("DeleteToDo")]
public static IActionResult Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "delete", Route = "DeleteFunction")] HttpRequest req,
ILogger log,
[SqlInput(commandText: "DeleteToDo", commandType: System.Data.CommandType.StoredProcedure,
parameters: "@Id={Query.id}", connectionStringSetting: "SqlConnectionString")]
IEnumerable<ToDoItem> toDoItems)
{
return new OkObjectResult(toDoItems);
}
}
}
```


More samples for the Azure SQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-java).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-java)[HTTP trigger, get row by ID from query string](#http-trigger-look-up-id-from-query-string-java)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-java)

The examples refer to a `ToDoItem`

class (in a separate file `ToDoItem.java`

) and a corresponding database table:

```
package com.function;
import java.util.UUID;
public class ToDoItem {
public UUID Id;
public int order;
public String title;
public String url;
public boolean completed;
public ToDoItem() {
}
public ToDoItem(UUID Id, int order, String title, String url, boolean completed) {
this.Id = Id;
this.order = order;
this.title = title;
this.url = url;
this.completed = completed;
}
}
```


```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


### HTTP trigger, get multiple rows

The following example shows a SQL input binding in a Java function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query and returns the results in the HTTP response.

```
package com.function;
import com.microsoft.azure.functions.HttpMethod;
import com.microsoft.azure.functions.HttpRequestMessage;
import com.microsoft.azure.functions.HttpResponseMessage;
import com.microsoft.azure.functions.HttpStatus;
import com.microsoft.azure.functions.annotation.AuthorizationLevel;
import com.microsoft.azure.functions.annotation.FunctionName;
import com.microsoft.azure.functions.annotation.HttpTrigger;
import com.microsoft.azure.functions.sql.annotation.SQLInput;
import java.util.Optional;
public class GetToDoItems {
@FunctionName("GetToDoItems")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@SQLInput(
name = "toDoItems",
commandText = "SELECT * FROM dbo.ToDo",
commandType = "Text",
connectionStringSetting = "SqlConnectionString")
ToDoItem[] toDoItems) {
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(toDoItems).build();
}
}
```


### HTTP trigger, get row by ID from query string

The following example shows a SQL input binding in a Java function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query, which is filtered by a parameter from the query string, and it returns the row in the HTTP response.

```
public class GetToDoItem {
@FunctionName("GetToDoItem")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@SQLInput(
name = "toDoItems",
commandText = "SELECT * FROM dbo.ToDo",
commandType = "Text",
parameters = "@Id={Query.id}",
connectionStringSetting = "SqlConnectionString")
ToDoItem[] toDoItems) {
ToDoItem toDoItem = toDoItems[0];
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(toDoItem).build();
}
}
```


### HTTP trigger, delete rows

The following example shows a SQL input binding in a Java function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It executes a stored procedure with input from the HTTP request query parameter.

The stored procedure `dbo.DeleteToDo`

must be created on the database. In this example, the stored procedure deletes a single record or all records depending on the value of the parameter.

```
CREATE PROCEDURE [dbo].[DeleteToDo]
@Id NVARCHAR(100)
AS
DECLARE @UID UNIQUEIDENTIFIER = TRY_CAST(@ID AS UNIQUEIDENTIFIER)
IF @UId IS NOT NULL AND @Id != ''
BEGIN
DELETE FROM dbo.ToDo WHERE Id = @UID
END
ELSE
BEGIN
DELETE FROM dbo.ToDo WHERE @ID = ''
END
SELECT [Id], [order], [title], [url], [completed] FROM dbo.ToDo
GO
```


```
public class DeleteToDo {
@FunctionName("DeleteToDo")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@SQLInput(
name = "toDoItems",
commandText = "dbo.DeleteToDo",
commandType = "StoredProcedure",
parameters = "@Id={Query.id}",
connectionStringSetting = "SqlConnectionString")
ToDoItem[] toDoItems) {
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(toDoItems).build();
}
}
```


More samples for the Azure SQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-js).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-javascript)[HTTP trigger, get row by ID from query string](#http-trigger-look-up-id-from-query-string-javascript)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-javascript)

The examples refer to a database table:

```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


### HTTP trigger, get multiple rows

The following example shows a SQL input binding that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query and returns the results in the HTTP response.

```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const sqlInput = input.sql({
commandText: 'select [Id], [order], [title], [url], [completed] from dbo.ToDo',
commandType: 'Text',
connectionStringSetting: 'SqlConnectionString',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log('HTTP trigger and SQL input binding function processed a request.');
const toDoItems = context.extraInputs.get(sqlInput);
return {
jsonBody: toDoItems,
};
}
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
extraInputs: [sqlInput],
handler: httpTrigger1,
});
```


```
const { app, input } = require('@azure/functions');
const sqlInput = input.sql({
commandText: 'select [Id], [order], [title], [url], [completed] from dbo.ToDo',
commandType: 'Text',
connectionStringSetting: 'SqlConnectionString',
});
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
extraInputs: [sqlInput],
handler: (request, context) => {
context.log('HTTP trigger and SQL input binding function processed a request.');
const toDoItems = context.extraInputs.get(sqlInput);
return {
jsonBody: toDoItems,
};
},
});
```


### HTTP trigger, get row by ID from query string

The following example shows a SQL input binding that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query, which is filtered by a parameter from the query string, and it returns the row in the HTTP response.

```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const sqlInput = input.sql({
commandText: 'select [Id], [order], [title], [url], [completed] from dbo.ToDo where Id = @Id',
commandType: 'Text',
parameters: '@Id={Query.id}',
connectionStringSetting: 'SqlConnectionString',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log('HTTP trigger and SQL input binding function processed a request.');
const toDoItem = context.extraInputs.get(sqlInput);
return {
jsonBody: toDoItem,
};
}
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
extraInputs: [sqlInput],
handler: httpTrigger1,
});
```


```
const { app, input } = require('@azure/functions');
const sqlInput = input.sql({
commandText: 'select [Id], [order], [title], [url], [completed] from dbo.ToDo where Id = @Id',
commandType: 'Text',
parameters: '@Id={Query.id}',
connectionStringSetting: 'SqlConnectionString',
});
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
extraInputs: [sqlInput],
handler: (request, context) => {
context.log('HTTP trigger and SQL input binding function processed a request.');
const toDoItem = context.extraInputs.get(sqlInput);
return {
jsonBody: toDoItem,
};
},
});
```


### HTTP trigger, delete rows

The following example shows a SQL input binding that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It executes a stored procedure with input from the HTTP request query parameter.

The stored procedure `dbo.DeleteToDo`

must be created on the database. In this example, the stored procedure deletes a single record or all records depending on the value of the parameter.

```
CREATE PROCEDURE [dbo].[DeleteToDo]
@Id NVARCHAR(100)
AS
DECLARE @UID UNIQUEIDENTIFIER = TRY_CAST(@ID AS UNIQUEIDENTIFIER)
IF @UId IS NOT NULL AND @Id != ''
BEGIN
DELETE FROM dbo.ToDo WHERE Id = @UID
END
ELSE
BEGIN
DELETE FROM dbo.ToDo WHERE @ID = ''
END
SELECT [Id], [order], [title], [url], [completed] FROM dbo.ToDo
GO
```


```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const sqlInput = input.sql({
commandText: 'DeleteToDo',
commandType: 'StoredProcedure',
parameters: '@Id={Query.id}',
connectionStringSetting: 'SqlConnectionString',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log('HTTP trigger and SQL input binding function processed a request.');
const toDoItems = context.extraInputs.get(sqlInput);
return {
jsonBody: toDoItems,
};
}
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
extraInputs: [sqlInput],
handler: httpTrigger1,
});
```


```
const { app, input } = require('@azure/functions');
const sqlInput = input.sql({
commandText: 'DeleteToDo',
commandType: 'StoredProcedure',
parameters: '@Id={Query.id}',
connectionStringSetting: 'SqlConnectionString',
});
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
extraInputs: [sqlInput],
handler: (request, context) => {
context.log('HTTP trigger and SQL input binding function processed a request.');
const toDoItems = context.extraInputs.get(sqlInput);
return {
jsonBody: toDoItems,
};
},
});
```


More samples for the Azure SQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-powershell).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-powershell)[HTTP trigger, get row by ID from query string](#http-trigger-look-up-id-from-query-string-powershell)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-powershell)

The examples refer to a database table:

```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


### HTTP trigger, get multiple rows

The following example shows a SQL input binding in a function.json file and a PowerShell function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query and returns the results in the HTTP response.

The following is binding data in the function.json file:

```
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"get"
]
},
{
"type": "http",
"direction": "out",
"name": "res"
},
{
"name": "todoItems",
"type": "sql",
"direction": "in",
"commandText": "select [Id], [order], [title], [url], [completed] from dbo.ToDo",
"commandType": "Text",
"connectionStringSetting": "SqlConnectionString"
}
```


The [configuration](#configuration) section explains these properties.

The following is sample PowerShell code for the function in the `run.ps1`

file:

```
using namespace System.Net
param($Request, $todoItems)
Write-Host "PowerShell function with SQL Input Binding processed a request."
Push-OutputBinding -Name res -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = $todoItems
})
```


### HTTP trigger, get row by ID from query string

The following example shows a SQL input binding in a PowerShell function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query, which is filtered by a parameter from the query string, and it returns the row in the HTTP response.

The following is binding data in the function.json file:

```
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"get"
]
},
{
"type": "http",
"direction": "out",
"name": "res"
},
{
"name": "todoItem",
"type": "sql",
"direction": "in",
"commandText": "select [Id], [order], [title], [url], [completed] from dbo.ToDo where Id = @Id",
"commandType": "Text",
"parameters": "@Id = {Query.id}",
"connectionStringSetting": "SqlConnectionString"
}
```


The [configuration](#configuration) section explains these properties.

The following is sample PowerShell code for the function in the `run.ps1`

file:

```
using namespace System.Net
param($Request, $todoItem)
Write-Host "PowerShell function with SQL Input Binding processed a request."
Push-OutputBinding -Name res -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = $todoItem
})
```


### HTTP trigger, delete rows

The following example shows a SQL input binding in a function.json file and a PowerShell function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It executes a stored procedure with input from the HTTP request query parameter.

The stored procedure `dbo.DeleteToDo`

must be created on the database. In this example, the stored procedure deletes a single record or all records depending on the value of the parameter.

```
CREATE PROCEDURE [dbo].[DeleteToDo]
@Id NVARCHAR(100)
AS
DECLARE @UID UNIQUEIDENTIFIER = TRY_CAST(@ID AS UNIQUEIDENTIFIER)
IF @UId IS NOT NULL AND @Id != ''
BEGIN
DELETE FROM dbo.ToDo WHERE Id = @UID
END
ELSE
BEGIN
DELETE FROM dbo.ToDo WHERE @ID = ''
END
SELECT [Id], [order], [title], [url], [completed] FROM dbo.ToDo
GO
```


```
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"get"
]
},
{
"type": "http",
"direction": "out",
"name": "res"
},
{
"name": "todoItems",
"type": "sql",
"direction": "in",
"commandText": "DeleteToDo",
"commandType": "StoredProcedure",
"parameters": "@Id = {Query.id}",
"connectionStringSetting": "SqlConnectionString"
}
```


The [configuration](#configuration) section explains these properties.

The following is sample PowerShell code for the function in the `run.ps1`

file:

```
using namespace System.Net
param($Request, $todoItems)
Write-Host "PowerShell function with SQL Input Binding processed a request."
Push-OutputBinding -Name res -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = $todoItems
})
```


More samples for the Azure SQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-python).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-python)[HTTP trigger, get row by ID from query string](#http-trigger-look-up-id-from-query-string-python)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-python)

The examples refer to a database table:

```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


### HTTP trigger, get multiple rows

The following example shows a SQL input binding in a function.json file and a Python function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query and returns the results in the HTTP response.

The following python code is a sample function_app.py file:

```
import json
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="GetToDo")
@app.route(route="gettodo")
@app.sql_input(arg_name="todo",
command_text="select [Id], [order], [title], [url], [completed] from dbo.ToDo",
command_type="Text",
connection_string_setting="SqlConnectionString")
def get_todo(req: func.HttpRequest, todo: func.SqlRowList) -> func.HttpResponse:
rows = list(map(lambda r: json.loads(r.to_json()), todo))
return func.HttpResponse(
json.dumps(rows),
status_code=200,
mimetype="application/json"
)
```


### HTTP trigger, get row by ID from query string

The following example shows a SQL input binding in a Python function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query, which is filtered by a parameter from the query string, and it returns the row in the HTTP response.

The following python code is a sample function_app.py file:

```
import json
import logging
import azure.functions as func
from azure.functions.decorators.core import DataType
app = func.FunctionApp()
@app.function_name(name="GetToDo")
@app.route(route="gettodo/{id}")
@app.sql_input(arg_name="todo",
command_text="select [Id], [order], [title], [url], [completed] from dbo.ToDo where Id = @Id",
command_type="Text",
parameters="@Id={id}",
connection_string_setting="SqlConnectionString")
def get_todo(req: func.HttpRequest, todo: func.SqlRowList) -> func.HttpResponse:
rows = list(map(lambda r: json.loads(r.to_json()), todo))
return func.HttpResponse(
json.dumps(rows),
status_code=200,
mimetype="application/json"
)
```


### HTTP trigger, delete rows

The following example shows a SQL input binding in a function.json file and a Python function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It executes a stored procedure with input from the HTTP request query parameter.

The stored procedure `dbo.DeleteToDo`

must be created on the database. In this example, the stored procedure deletes a single record or all records depending on the value of the parameter.

```
CREATE PROCEDURE [dbo].[DeleteToDo]
@Id NVARCHAR(100)
AS
DECLARE @UID UNIQUEIDENTIFIER = TRY_CAST(@ID AS UNIQUEIDENTIFIER)
IF @UId IS NOT NULL AND @Id != ''
BEGIN
DELETE FROM dbo.ToDo WHERE Id = @UID
END
ELSE
BEGIN
DELETE FROM dbo.ToDo WHERE @ID = ''
END
SELECT [Id], [order], [title], [url], [completed] FROM dbo.ToDo
GO
```


The following python code is a sample function_app.py file:

```
import json
import logging
import azure.functions as func
from azure.functions.decorators.core import DataType
app = func.FunctionApp()
@app.function_name(name="DeleteToDo")
@app.route(route="deletetodo/{id}")
@app.sql_input(arg_name="todo",
command_text="DeleteToDo",
command_type="StoredProcedure",
parameters="@Id={id}",
connection_string_setting="SqlConnectionString")
def get_todo(req: func.HttpRequest, todo: func.SqlRowList) -> func.HttpResponse:
rows = list(map(lambda r: json.loads(r.to_json()), todo))
return func.HttpResponse(
json.dumps(rows),
status_code=200,
mimetype="application/json"
)
```


## Attributes

The [C# library](functions-dotnet-class-library) uses the [SqlAttribute](https://github.com/Azure/azure-functions-sql-extension/blob/main/src/SqlAttribute.cs) attribute to declare the SQL bindings on the function, which has the following properties:

| Attribute property | Description |
|---|---|
CommandText |
Required. The Transact-SQL query command or name of the stored procedure executed by the binding. |
ConnectionStringSetting |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is being executed. This value isn't the actual connection string and must instead resolve to an environment variable name. |
CommandType |
Required. A
|

**Parameters**`@param1=param1,@param2=param2`

. The parameter name and the parameter value can't contain a comma (`,`

) or an equals sign (`=`

).## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@SQLInput`

annotation (`com.microsoft.azure.functions.sql.annotation.SQLInput`

) on parameters whose value would come from Azure SQL. This annotation supports the following elements:

| Element | Description |
|---|---|
commandText |
Required. The Transact-SQL query command or name of the stored procedure executed by the binding. |
connectionStringSetting |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is being executed. This value isn't the actual connection string and must instead resolve to an environment variable name. |
commandType |
Required. A
|

**name****parameters**`@param1=param1,@param2=param2`

. The parameter name and the parameter value can't contain a comma (`,`

) or an equals sign (`=`

).## Configuration

The following table explains the properties that you can set on the `options`

object passed to the `input.sql()`

method.

| Property | Description |
|---|---|
commandText |
Required. The Transact-SQL query command or name of the stored procedure executed by the binding. |
connectionStringSetting |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is being executed. This value isn't the actual connection string and must instead resolve to an environment variable name. Optional keywords in the connection string value are
|

**commandType**[CommandType](/en-us/dotnet/api/system.data.commandtype)value, which is[Text](/en-us/dotnet/api/system.data.commandtype#fields)for a query and[StoredProcedure](/en-us/dotnet/api/system.data.commandtype#fields)for a stored procedure.**parameters**`@param1=param1,@param2=param2`

. The parameter name and the parameter value can't contain a comma (`,`

) or an equals sign (`=`

).## Configuration

The following table explains the binding configuration properties that you set in the function.json file.

| function.json property | Description |
|---|---|
type |
Required. Must be set to `sql` . |
direction |
Required. Must be set to `in` . |
name |
Required. The name of the variable that represents the query results in function code. |
commandText |
Required. The Transact-SQL query command or name of the stored procedure executed by the binding. |
connectionStringSetting |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is being executed. This value isn't the actual connection string and must instead resolve to an environment variable name. Optional keywords in the connection string value are
|

**commandType**[CommandType](/en-us/dotnet/api/system.data.commandtype)value, which is[Text](/en-us/dotnet/api/system.data.commandtype#fields)for a query and[StoredProcedure](/en-us/dotnet/api/system.data.commandtype#fields)for a stored procedure.**parameters**`@param1=param1,@param2=param2`

. The parameter name and the parameter value can't contain a comma (`,`

) or an equals sign (`=`

).When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

The binding definition includes the SQL command text, the command type, parameters, and the connection string setting name. The command can be a Transact-SQL (T-SQL) query with the command type `System.Data.CommandType.Text`

or stored procedure name with the command type `System.Data.CommandType.StoredProcedure`

. The connection string setting name corresponds to the application setting (in `local.settings.json`

for local development) that contains the [connection string](/en-us/dotnet/api/microsoft.data.sqlclient.sqlconnection.connectionstring?view=sqlclient-dotnet-core-5.0&preserve-view=true#Microsoft_Data_SqlClient_SqlConnection_ConnectionString) to the Azure SQL or SQL Server instance.

Important

For optimal security, you should use Microsoft Entra ID with managed identities for connections between Functions and Azure SQL Database. Managed identities make your app more secure by eliminating secrets from your application deployments, such as credentials in the connection strings, server names, and ports being used. You can learn how to use managed identities in this tutorial, [Connect a function app to Azure SQL with managed identity and SQL bindings](functions-identity-access-azure-sql-with-managed-identity).

Queries executed by the input binding are [parameterized](/en-us/dotnet/api/microsoft.data.sqlclient.sqlparameter) in Microsoft.Data.SqlClient to reduce the risk of [SQL injection](/en-us/sql/relational-databases/security/sql-injection) from the parameter values passed into the binding.

If an exception occurs when a SQL input binding is executed, then the function code doesn't execute. This behavior may result in an error code being returned, such as an HTTP trigger returning a 500 error code.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/openapi-apim-integrate-visual-studio -->

# Create serverless APIs in Visual Studio using Azure Functions and API Management integration

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

REST APIs are often described using an OpenAPI definition (formerly known as Swagger) file. This file contains information about operations in an API and how the request and response data for the API should be structured.

In this tutorial, you learn how to:

- Create the code project in Visual Studio
- Install the OpenAPI extension
- Add an HTTP trigger endpoint, which includes OpenAPI definitions
- Test function APIs locally using built-in OpenAPI functionality
- Publish project to a function app in Azure
- Enable API Management integration
- Download the OpenAPI definition file

The serverless function you create provides an API that lets you determine whether an emergency repair on a wind turbine is cost-effective. Since you create both the function app and API Management instance in a consumption tier, your cost for completing this tutorial is minimal.

## Prerequisites

[Visual Studio 2022](https://azure.microsoft.com/downloads/). Make sure you select the**Azure development**workload during installation.An active

[Azure subscription](../guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing), create a[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

## Create the code project

The Azure Functions project template in Visual Studio creates a project that you can publish to a function app in Azure. You'll also create an HTTP triggered function from a template that supports OpenAPI definition file (formerly Swagger file) generation.

From the Visual Studio menu, select

**File**>**New**>**Project**.In

**Create a new project**, enter*functions*in the search box, choose the**Azure Functions**template, and then select**Next**.In

**Configure your new project**, enter a**Project name**for your project like`TurbineRepair`

, and then select**Create**.For the

**Create a new Azure Functions application**settings, select one of these options for**Functions worker**, where the option you choose depends on your chosen process model:**.NET 8.0 Isolated (Long Term Support)**: Your C# functions run in the isolated worker model, which is recommended. For more information, see the[isolated worker model guide](dotnet-isolated-process-guide).For the rest of the options, use the values in the following table:

Setting Value Description **Function template****Empty**This creates a project without a trigger, which gives you more control over the name of the HTTP triggered function when you add it later. **Use Azurite for runtime storage account (AzureWebJobsStorage)****Selected**You can use the emulator for local development of HTTP trigger functions. Because a function app in Azure requires a storage account, one is assigned or created when you publish your project to Azure. **Authorization level****Function**When running in Azure, clients must provide a key when accessing the endpoint. For more information, see [Authorization level](functions-bindings-http-webhook-trigger#http-auth).Select

**Create**to create the function project.

Next, you update the project by installing the OpenAPI extension for Azure Functions, which enables the discoverability of API endpoints in your app.

## Install the OpenAPI extension

To install the OpenAPI extension:

From the

**Tools**menu, select**NuGet Package Manager**>**Package Manager Console**.In the console, run the following

[Install-Package](/en-us/nuget/tools/ps-ref-install-package)command to install the OpenAPI extension:`NuGet\Install-Package Microsoft.Azure.Functions.Worker.Extensions.OpenApi -Version 1.5.1`

You might need to update the

[specific version](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.OpenApi), based on your version of .NET.

Now, you can add your HTTP endpoint function.

## Add an HTTP endpoint function

In a C# class library, the bindings used by the function are defined by applying attributes in the code. To create a function with an HTTP trigger:

In

**Solution Explorer**, right-click your project node and select**Add**>**New Azure Function**.Enter

**Turbine.cs**for the class, and then select**Add**.Choose the

**Http trigger**template, set**Authorization level**to**Function**, and then select**Add**. A Turbine.cs code file is added to your project that defines a new function endpoint with an HTTP trigger.

Now you can replace the HTTP trigger template code with code that implements the Turbine function endpoint, along with attributes that use OpenAPI to define endpoint.

## Update the function code

The function uses an HTTP trigger that takes two parameters:

| Parameter name | Description |
|---|---|
hours |
The estimated time to make a turbine repair, up to the nearest whole hour. |
capacity |
The capacity of the turbine, in kilowatts. |

The function then calculates how much a repair costs, and how much revenue the turbine could make in a 24-hour period. Parameters are supplied either in the query string or in the payload of a POST request.

In the Turbine.cs project file, replace the contents of the class generated from the HTTP trigger template with the following code, which depends on your process model:

```
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.WebJobs.Extensions.OpenApi.Core.Attributes;
using Microsoft.Azure.WebJobs.Extensions.OpenApi.Core.Enums;
using Microsoft.Extensions.Logging;
using Microsoft.OpenApi.Models;
using Newtonsoft.Json;
using System.Net;
namespace TurbineRepair
{
public class Turbine
{
const double revenuePerkW = 0.12;
const double technicianCost = 250;
const double turbineCost = 100;
private readonly ILogger<Turbine> _logger;
public Turbine(ILogger<Turbine> logger)
{
_logger = logger;
}
[Function("TurbineRepair")]
[OpenApiOperation(operationId: "Run")]
[OpenApiSecurity("function_key", SecuritySchemeType.ApiKey, Name = "code", In = OpenApiSecurityLocationType.Query)]
[OpenApiRequestBody("application/json", typeof(RequestBodyModel),
Description = "JSON request body containing { hours, capacity}")]
[OpenApiResponseWithBody(statusCode: HttpStatusCode.OK, contentType: "application/json", bodyType: typeof(string),
Description = "The OK response message containing a JSON result.")]
public static async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Function, "post", Route = null)] HttpRequest req,
ILogger log)
{
// Get request body data.
string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
dynamic? data = JsonConvert.DeserializeObject(requestBody);
int? capacity = data?.capacity;
int? hours = data?.hours;
// Return bad request if capacity or hours are not passed in
if (capacity == null || hours == null)
{
return new BadRequestObjectResult("Please pass capacity and hours in the request body");
}
// Formulas to calculate revenue and cost
double? revenueOpportunity = capacity * revenuePerkW * 24;
double? costToFix = hours * technicianCost + turbineCost;
string repairTurbine;
if (revenueOpportunity > costToFix)
{
repairTurbine = "Yes";
}
else
{
repairTurbine = "No";
};
return new OkObjectResult(new
{
message = repairTurbine,
revenueOpportunity = "$" + revenueOpportunity,
costToFix = "$" + costToFix
});
}
public class RequestBodyModel
{
public int Hours { get; set; }
public int Capacity { get; set; }
}
}
}
```


This function code returns a message of `Yes`

or `No`

to indicate whether an emergency repair is cost-effective. It also returns the revenue opportunity that the turbine represents and the cost to fix the turbine.

## Run and verify the API locally

When you run the function, the OpenAPI endpoints make it easy to try out the function locally using a generated page. You don't need to provide function access keys when running locally.

Press F5 to start the project. When Functions runtime starts locally, a set of OpenAPI and Swagger endpoints are shown in the output, along with the function endpoint.

In your browser, open the RenderSwaggerUI endpoint, which should look like

`http://localhost:7071/api/swagger/ui`

. A page is rendered, based on your OpenAPI definitions.Select

**POST**>**Try it out**, enter values for`hours`

and`capacity`

either as query parameters or in the JSON request body, and select**Execute**.When you enter integer values like 6 for

`hours`

and 2500 for`capacity`

, you get a JSON response that looks like the following example:

Now you have a function that determines the cost-effectiveness of emergency repairs. Next, you publish your project and API definitions to Azure.

## Publish the project to Azure

Before you can publish your project, you must have a function app in your Azure subscription. Visual Studio publishing creates a function app the first time you publish your project. It can also create an API Management instance that integrates with your function app to expose the TurbineRepair API.

In

**Solution Explorer**, right-click the project and select**Publish**and in**Target**, select**Azure**then**Next**.For the

**Specific target**, choose**Azure Function App (Windows)**to create a function app that runs on Windows, then select**Next**.In

**Function Instance**, choose**+ Create a new Azure Function...**.Create a new instance using the values specified in the following table:

Setting Value Description **Name**Globally unique name Name that uniquely identifies your new function app. Accept this name or enter a new name. Valid characters are: `a-z`

,`0-9`

, and`-`

.**Subscription**Your subscription The Azure subscription to use. Accept this subscription or select a new one from the drop-down list. [Resource group](../azure-resource-manager/management/overview)Name of your resource group The resource group in which to create your function app. Select an existing resource group from the drop-down list or choose **New**to create a new resource group.[Plan Type](functions-scale)Consumption When you publish your project to a function app that runs in a [Consumption plan](consumption-plan), you pay only for executions of your functions app. Other hosting plans incur higher costs.**Location**Location of the service Choose a **Location**in a[region](https://azure.microsoft.com/regions/)near you or other services your functions access.[Azure Storage](storage-considerations)General-purpose storage account An Azure Storage account is required by the Functions runtime. Select **New**to configure a general-purpose storage account. You can also choose an existing account that meets the[storage account requirements](storage-considerations#storage-account-requirements).Select

**Create**to create a function app and its related resources in Azure. Status of resource creation is shown in the lower left of the window.Back in

**Functions instance**, make sure that**Run from package file**is checked. Your function app is deployed using[Zip Deploy](functions-deployment-technologies#zip-deploy)with[Run-From-Package](run-functions-from-deployment-package)mode enabled. This deployment method is recommended for your functions project, since it results in better performance.Select

**Next**, and in**API Management**page, also choose**+ Create an API Management API**.Create an

**API in API Management**by using values in the following table:Setting Value Description **API name**TurbineRepair Name for the API. **Subscription name**Your subscription The Azure subscription to use. Accept this subscription or select a new one from the drop-down list. **Resource group**Name of your resource group Select the same resource group as your function app from the drop-down list. **API Management service**New instance Select **New**to create a new API Management instance in the same location in the serverless tier. Select**OK**to create the instance.Select

**Create**to create the API Management instance with the TurbineRepair API from the function integration.Select

**Finish**and after the publish profile creation process completes, select**Close**.Verify the Publish page now says

**Ready to publish**, and then select**Publish**to deploy the package containing your project files to your new function app in Azure.After the deployment completes, the root URL of the function app in Azure is shown in the

**Publish**tab.

## Get the function access key

In the

**Publish**tab, select the ellipses (**...**) next to**Hosting**and select**Open in Azure portal**. The function app you created is opened in the Azure portal in your default browser.Under

**Functions**on the**Overview page**, select >**Turbine**then select**Function keys**.Under

**Function keys**, select the*copy to clipboard*icon next to the**default**key. You can now set this key you copied in API Management so that it can access the function endpoint.

## Configure API Management

In the function app page, expand

**API**and select**API Management**.If the function app isn't already connected to the new API Management instance, select it under

**API Management**, select**API**>**OpenAPI Document on Azure Functions**, make sure**Import functions**is checked, and select**Link API**. Make sure that only**TurbineRepair**is selected for import and then**Select**.Select

**Go to API Management**at the top of the page, and in the API Management instance, expand**APIs**.Under

**APIs**>**All APIs**, select**OpenAPI Document on Azure Functions**>**POST Run**, then under**Inbound processing**select**Add policy**>**Set query parameters**.Below

**Inbound processing**, in**Set query parameters**, type`code`

for**Name**, select**+Value**, paste in the copied function key, and select**Save**. API Management includes the function key when it passes calls through to the function endpoint.

Now that the function key is set, you can call the `turbine`

API endpoint to verify that it works when hosted in Azure.

## Verify the API in Azure

In the API, select the

**Test**tab and then**POST Run**, enter the following code in the**Request body**>**Raw**, and select**Send**:`{ "hours": "6", "capacity": "2500" }`

As before, you can also provide the same values as query parameters.

Select

**Send**, and then view the**HTTP response**to verify the same results are returned from the API.

## Download the OpenAPI definition

If your API works as expected, you can download the OpenAPI definition for the new hosted APIs from API Management.

-
- Under
**APIs**, select**OpenAPI Document on Azure Functions**, select the ellipses (**...**), and select**Export**.

- Under
Choose the means of API export, including OpenAPI files in various formats. You can also

[export APIs from Azure API Management to the Power Platform](../api-management/export-api-power-platform).

## Clean up resources

In the preceding steps, you created Azure resources in a resource group. If you don't expect to need these resources in the future, you can delete them by deleting the resource group.

From the Azure portal menu or **Home** page, select **Resource groups**. Then, on the **Resource groups** page, select the group you created.

On the **myResourceGroup** page, make sure that the listed resources are the ones you want to delete.

Select **Delete resource group**, type the name of your group in the text box to confirm, and then select **Delete**.

## Next steps

You've used Visual Studio 2022 to create a function that's self-documenting because of the [OpenAPI Extension](https://github.com/Azure/azure-functions-openapi-extension) and integrated with API Management. You can now refine the definition in API Management in the portal. You can also [learn more about API Management](../api-management/api-management-key-concepts).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-how-to-use-azure-function-app-settings -->

# Manage your function app

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure Functions, a function app provides the execution context for your individual functions. Function app behaviors apply to all functions hosted by a given function app. All functions in a function app must be of the same [language](supported-languages).

Individual functions in a function app are deployed together and are scaled together. All functions in the same function app share resources, per instance, as the function app scales.

Connection strings, environment variables, and other application settings are defined separately for each function app. Any data that must be shared between function apps should be stored externally in a persisted store.

## Get started in the Azure portal

Note

Because of limitations on editing function code in the [Azure portal](https://portal.azure.com), you should develop your functions locally and publish your code project to a function app in Azure. For more information, see [Development limitations in the Azure portal](functions-how-to-use-azure-function-app-settings#development-limitations-in-the-azure-portal)

To view the app settings in your function app, follow these steps:

Sign in to the

[Azure portal](https://portal.azure.com)using your Azure account. Search for your function app and select it.In the left pane of your function app, expand

**Settings**, select**Environment variables**, and then select the**App settings**tab.

## Work with application settings

In addition to the predefined app settings used by Azure Functions, you can create any number of app settings, as required by your function code. For more information, see [App settings reference for Azure Functions](functions-app-settings).

These settings are stored encrypted. For more information, see [App settings security](security-concepts#application-settings).

You can manage app settings from the [Azure portal](functions-how-to-use-azure-function-app-settings?tabs=portal#settings), and by using the [Azure CLI](functions-how-to-use-azure-function-app-settings?tabs=azurecli#settings) and [Azure PowerShell](functions-how-to-use-azure-function-app-settings?tabs=powershell#settings). You can also manage app settings from [Visual Studio Code](functions-develop-vs-code#application-settings-in-azure) and from [Visual Studio](functions-develop-vs#function-app-settings).

Note

Changing application settings causes your function app to restart by default across all hosting plans. For zero-downtime deployments when changing settings, use the [Flex Consumption plan](flex-consumption-plan) with [rolling updates as the site update strategy](flex-consumption-site-updates). For other hosting plans, see [optimize deployments](functions-best-practices#optimize-deployments) for guidance on minimizing downtime.

To view your app settings, see [Get started in the Azure portal](#get-started-in-the-azure-portal).

The **App settings** tab maintains settings that are used by your function app:

### Use application settings

The function app settings values can also be read in your code as environment variables. For more information, see the Environment variables section of these language-specific reference articles:

When you develop a function app locally, you must maintain local copies of these values in the *local.settings.json* project file. For more information, see [Local settings file](functions-develop-local#local-settings-file).

## FTPS deployment settings

Azure Functions supports deploying project code to your function app by using FTPS. Because this deployment method requires you to [sync triggers](functions-deployment-technologies#trigger-syncing), it isn't recommended. To securely transfer project files, always use FTPS and not FTP.

To get the credentials required for FTPS deployment, use one of these methods:

You can get the FTPS publishing credentials in the Azure portal by downloading the publishing profile for your function app.

Important

The publishing profile contains important security credentials. Always secure the downloaded file on your local computer.

To download the publishing profile of your function app:

In the

[Azure portal](https://portal.azure.com), locate the page for your function app, expand**Settings**>**Configuration**in the left column.In the

**Configuration**page, select the**General settings**tab and make sure that**SCM Basic Auth Publishing Credentials**is turned**On**. When this setting is**Off**, you can't use publish profiles, so select**On**and then**Save**.Go back to the function app's

**Overview**page, and then select**Get publish profile**.Save and copy the contents of the file.


- In the file, locate the
`publishProfile`

element with the attribute`publishMethod="FTP"`

. In this element, the`publishUrl`

,`userName`

, and`userPWD`

attributes contain the target URL and credentials for FTPS publishing.

## Hosting plan type

When you create a function app, you also create a hosting plan in which the app runs. A plan can have one or more function apps. The functionality, scaling, and pricing of your functions depend on the type of plan. For more information, see [Azure Functions hosting options](functions-scale).

You can determine the type of plan being used by your function app from the Azure portal, or by using the Azure CLI or Azure PowerShell APIs.

The following values indicate the plan type:

| Plan type | Azure portal | Azure CLI/PowerShell |
|---|---|---|
|

**Consumption**`Dynamic`

[Premium](functions-premium-plan)**ElasticPremium**`ElasticPremium`

[Dedicated (App Service)](dedicated-plan)To determine the type of plan used by your function app, see the

**App Service Plan**in the**Overview**page of the function app in the[Azure portal](https://portal.azure.com).To see the pricing tier, select the name of the

**App Service Plan**, and then select**Settings > Properties**from the left pane.

## Plan migration

You can migrate a function app between a Consumption plan and a Premium plan on Windows.

Tip

We recommend you migrate your Consumption plan app to run in a Flex Consumption plan instead of a Premium plan. Migration to the Flex Consumption plan is the only migration option for a Linux Consumption plan app. For more information, see [Migrate Consumption plan apps to the Flex Consumption plan](migration/migrate-plan-consumption-to-flex).

When migrating between plans, keep in mind the following considerations:

- Direct migration to a Dedicated (App Service) plan isn't supported.
- Migration isn't supported on Linux.
- The source plan and the target plan must be in the same resource group and geographical region. For more information, see
[Move an app to another App Service plan](../app-service/app-service-plan-manage#move-an-app-to-another-app-service-plan). - The specific CLI commands depend on the direction of the migration.
- Downtime in your function executions occurs as the function app is migrated between plans.
- State and other app-specific content is maintained, because the same Azure Files share is used by the app both before and after migration.

You can migrate your plan using these tools:

You can use the [Azure portal](https://portal.azure.com) to switch to a different plan.

Choose the direction of the migration for your app on Windows.

## Development limitations in the Azure portal

The following table shows the operating systems and languages that support in-portal editing:

| Language | Flex Consumption | Premium | Dedicated | Consumption |
|---|---|---|---|---|
| C# | ||||
| Java | ||||
| JavaScript (Node.js) | ✔ | ✔ | Windows-only | |
| Python | Linux-only | Linux-only | Linux-only | |
| PowerShell | Windows-only | Windows-only | Windows-only | |
| TypeScript (Node.js) |

Consider these limitations when you develop your functions in the [Azure portal](https://portal.azure.com):

- In-portal editing is supported only for functions that were created or last modified in the Azure portal.
- In-portal editing is supported only for
[JavaScript](functions-reference-node),[PowerShell](functions-reference-powershell),[Python](functions-reference-python), and[C# script](functions-reference-csharp)(in-process) functions. - In-portal editing isn't currently supported by the
[Flex Consumption plan](flex-consumption-plan#considerations). - The ability to run your apps on Linux in a Consumption plan is planned for retirement. For more information, see
[Azure Functions Consumption plan hosting](consumption-plan). - When you deploy code to a function app from outside the Azure portal, you can no longer edit any of the code for that function app in the portal. In this case, just continue using
[local development](functions-develop-local). - For Python, development with custom modules isn't currently supported in the portal. To add custom modules to your function app, you must
[develop your app locally](functions-develop-local). - For compiled C# functions and Java functions, you can create the function app and related resources in the portal. However, you must create the functions code project locally and then publish it to Azure.

When possible, develop your functions locally and publish your code project to a function app in Azure. For more information, see [Code and test Azure Functions locally](functions-develop-local).

## Manually install extensions

C# class library functions can include the NuGet packages for [binding extensions](functions-bindings-register) directly in the class library project. For other non-.NET languages and C# script, you should [use extension bundles](extension-bundles). If you must manually install extensions, you can do so by [using Azure Functions Core Tools](functions-core-tools-reference#func-extensions-install) locally. If you can't use extension bundles and are only able to work in the portal, you need to use [Advanced Tools (Kudu)](#kudu) to manually create the extensions.csproj file directly in the site. Make sure to first remove the `extensionBundle`

element from the *host.json* file.

This same process works for any other file you need to add to your app.

Important

When possible, don't edit files directly in your function app in Azure. We recommend [downloading your app files locally](deployment-zip-push#download-your-function-app-files), using [Core Tools to install extensions](functions-core-tools-reference#func-extensions-install) and other packages, validating your changes, and then [republishing your app using Core Tools](functions-run-local#publish) or one of the other [supported deployment methods](functions-deployment-technologies#deployment-methods).

The Functions editor built into the Azure portal lets you update your function code and configuration files directly in the portal:

Select your function app, then under

**Functions**, select**Functions**.Choose your function and select

**Code + test**under**Developer**.Choose your file to edit and select

**Save**when you finish.

Files in the root of the app, such as function.proj or extensions.csproj need to be created and edited by using the [Advanced Tools (Kudu)](#kudu):

Select your function app, expand

**Development tools**, and then select**Advanced tools**>**Go**.If prompted, sign in to the Source Control Manager (SCM) site with your Azure credentials.

From the

**Debug console**menu, choose**CMD**.Navigate to

`.\site\wwwroot`

, select the plus (**+**) button at the top, and select**New file**.Give the file a name, such as

`extensions.csproj`

, and then press Enter.Select the edit button next to the new file, add or update code in the file, and then select

**Save**.For a project file like

*extensions.csproj*, run the following command to rebuild the extensions project:`dotnet build extensions.csproj`


## Platform features

Function apps run in the Azure App Service platform, which maintains them. As such, your function apps have access to most of the features of Azure's core web hosting platform. When you use the [Azure portal](https://portal.azure.com), the left pane is where you access the many features of the App Service platform that you can use in your function apps.

The following matrix indicates Azure portal feature support by hosting plan and operating system:

| Feature | Consumption plan | Flex Consumption plan | Premium plan | Dedicated plan |
|---|---|---|---|---|
|

Linux:

**X****X**[App Service editor](#editor)Linux:

**X****X**Linux:

**X**Linux:

**X**[Backups](../app-service/manage-backup)**X****X****X**[Console](#console)Linux:

**X****X**Linux: SSH

Linux: SSH

The rest of this article focuses on the following features in the portal that are useful for your function apps:

For more information about how to work with App Service settings, see [Configure Azure App Service Settings](../app-service/configure-common).

### App Service editor

The App Service editor is an advanced in-portal editor that you can use to modify JSON configuration files and code files alike. Choosing this option launches a separate browser tab with a basic editor. This editor enables you to integrate with the Git repository, run and debug code, and modify function app settings. This editor provides an enhanced development environment for your functions compared with the built-in function editor.

We recommend that you consider developing your functions on your local computer. When you develop locally and publish to Azure, your project files are read-only in the Azure portal. For more information, see [Code and test Azure Functions locally](functions-develop-local).

### Console

The in-portal console is an ideal developer tool when you prefer to interact with your function app from the command line. Common commands include directory and file creation and navigation, as well as executing batch files and scripts.

When developing locally, we recommend using the [Azure Functions Core Tools](functions-run-local) and the [Azure CLI](/en-us/cli/azure/).

### Advanced tools (Kudu)

The advanced tools for App Service (also known as Kudu) provide access to advanced administrative features of your function app. From Kudu, you manage system information, app settings, environment variables, site extensions, HTTP headers, and server variables. You can also launch **Kudu** by browsing to the SCM endpoint for your function app, for example: `https://<myfunctionapp>.scm.azurewebsites.net/`

.

### Deployment Center

When you use a source control solution to develop and maintain your functions code, Deployment Center lets you build and deploy from source control. Your project is built and deployed to Azure when you make updates. For more information, see [Deployment technologies in Azure Functions](functions-deployment-technologies).

### Cross-origin resource sharing

To prevent malicious code execution on the client, modern browsers block requests from web applications to resources running in a separate domain. [Cross-origin resource sharing (CORS)](https://developer.mozilla.org/docs/Web/HTTP/CORS) lets an `Access-Control-Allow-Origin`

header declare which origins are allowed to call endpoints on your function app.

When you configure the **Allowed origins** list for your function app, the `Access-Control-Allow-Origin`

header is automatically added to all responses from HTTP endpoints in your function app.

If there's another domain entry, the wildcard (*) is ignored.

### Authentication

When functions use an HTTP trigger, you can require calls to first be authenticated. App Service supports Microsoft Entra authentication and sign-in with social providers, such as Facebook, Microsoft, and X. For information about configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/overview-authentication-authorization).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-reference-powershell -->

# Azure Functions PowerShell developer guide

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides details about how you write Azure Functions using PowerShell.

A PowerShell Azure function (function) is represented as a PowerShell script that executes when triggered. Each function script has a related `function.json`

file that defines how the function behaves, such as how it's triggered and its input and output parameters. To learn more, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings).

Like other kinds of functions, PowerShell script functions take in parameters that match the names of all the input bindings defined in the `function.json`

file. A `TriggerMetadata`

parameter is also passed that contains additional information on the trigger that started the function.

This article assumes that you have already read the [Azure Functions developer guide](functions-reference). It also assumes that you completed the [Functions quickstart for PowerShell](how-to-create-function-vs-code?pivot=programming-language-powershell) to create your first PowerShell function.

## Folder structure

The required folder structure for a PowerShell project looks like the following. This default can be changed. For more information, see the [scriptFile](#configure-function-scriptfile) section.

```
PSFunctionApp
| - MyFirstFunction
| | - run.ps1
| | - function.json
| - MySecondFunction
| | - run.ps1
| | - function.json
| - Modules
| | - myFirstHelperModule
| | | - myFirstHelperModule.psd1
| | | - myFirstHelperModule.psm1
| | - mySecondHelperModule
| | | - mySecondHelperModule.psd1
| | | - mySecondHelperModule.psm1
| - local.settings.json
| - host.json
| - requirements.psd1
| - profile.ps1
| - extensions.csproj
| - bin
```


At the root of the project, there's a shared [ host.json](functions-host-json) file that can be used to configure the function app. Each function has a folder with its own code file (.ps1) and binding configuration file (

`function.json`

). The name of the function.json file's parent directory is always the name of your function.Certain bindings require the presence of an `extensions.csproj`

file. Binding extensions, required in [version 2.x and later versions](functions-versions) of the Functions runtime, are defined in the `extensions.csproj`

file, with the actual library files in the `bin`

folder. When developing locally, you must [register binding extensions](extension-bundles). When you develop functions in the Azure portal, this registration is done for you.

In PowerShell Function Apps, you might optionally have a `profile.ps1`

which runs when a function app starts to run (otherwise know as a * cold start*). For more information, see

[PowerShell profile](#powershell-profile).

## Defining a PowerShell script as a function

By default, the Functions runtime looks for your function in `run.ps1`

, where `run.ps1`

shares the same parent directory as its corresponding `function.json`

.

Your script is passed several arguments on execution. To handle these parameters, add a `param`

block to the top of your script as in the following example:

```
# $TriggerMetadata is optional here. If you don't need it, you can safely remove it from the param block
param($MyFirstInputBinding, $MySecondInputBinding, $TriggerMetadata)
```


### TriggerMetadata parameter

The `TriggerMetadata`

parameter is used to supply additional information about the trigger. This metadata varies from binding to binding but they all contain a `sys`

property that contains the following data:

```
$TriggerMetadata.sys
```


| Property | Description | Type |
|---|---|---|
| UtcNow | When, in UTC, the function was triggered | DateTime |
| MethodName | The name of the Function that was triggered | string |
| RandGuid | a unique guid to this execution of the function | string |

Every trigger type has a different set of metadata. For example, the `$TriggerMetadata`

for `QueueTrigger`

contains the `InsertionTime`

, `Id`

, `DequeueCount`

, among other things. For more information on the queue trigger's metadata, go to the [official documentation for queue triggers](functions-bindings-storage-queue-trigger#message-metadata). Check the documentation on the [triggers](functions-triggers-bindings) you're working with to see what comes inside the trigger metadata.

## Bindings

In PowerShell, [bindings](functions-triggers-bindings) are configured and defined in a function's function.json. Functions interact with bindings in many ways.

### Reading trigger and input data

Trigger and input bindings are read as parameters passed to your function. Input bindings have a `direction`

set to `in`

in function.json. The `name`

property defined in `function.json`

is the name of the parameter, in the `param`

block. Since PowerShell uses named parameters for binding, the order of the parameters doesn't matter. However, it's a best practice to follow the order of the bindings defined in the `function.json`

.

```
param($MyFirstInputBinding, $MySecondInputBinding)
```


### Writing output data

In Functions, an output binding has a `direction`

set to `out`

in the function.json. You can write to an output binding by using the `Push-OutputBinding`

cmdlet, which is available to the Functions runtime. In all cases, the `name`

property of the binding as defined in `function.json`

corresponds to the `Name`

parameter of the `Push-OutputBinding`

cmdlet.

The following example shows how to call `Push-OutputBinding`

in your function script:

```
param($MyFirstInputBinding, $MySecondInputBinding)
Push-OutputBinding -Name myQueue -Value $myValue
```


You can also pass in a value for a specific binding through the pipeline.

```
param($MyFirstInputBinding, $MySecondInputBinding)
Produce-MyOutputValue | Push-OutputBinding -Name myQueue
```


`Push-OutputBinding`

behaves differently based on the value specified for `-Name`

:

When the specified name can't be resolved to a valid output binding, then an error is thrown.

When the output binding accepts a collection of values, you can call

`Push-OutputBinding`

repeatedly to push multiple values.When the output binding only accepts a singleton value, calling

`Push-OutputBinding`

a second time raises an error.

#### Push-OutputBinding syntax

The following are valid parameters for calling `Push-OutputBinding`

:

| Name | Type | Position | Description |
|---|---|---|---|
`-Name` |
String | 1 | The name of the output binding you want to set. |
`-Value` |
Object | 2 | The value of the output binding you want to set, which is accepted from the pipeline ByValue. |
`-Clobber` |
SwitchParameter | Named | (Optional) When specified, forces the value to be set for a specified output binding. |

The following common parameters are also supported:

`Verbose`

`Debug`

`ErrorAction`

`ErrorVariable`

`WarningAction`

`WarningVariable`

`OutBuffer`

`PipelineVariable`

`OutVariable`


For more information, see [About CommonParameters](/en-us/powershell/module/microsoft.powershell.core/about/about_commonparameters).

#### Push-OutputBinding example: HTTP responses

An HTTP trigger returns a response using an output binding named `response`

. In the following example, the output binding of `response`

has the value of "output #1":

```
Push-OutputBinding -Name response -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = "output #1"
})
```


Because the output is to HTTP, which accepts a singleton value only, an error is thrown when `Push-OutputBinding`

is called a second time.

```
Push-OutputBinding -Name response -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = "output #2"
})
```


For outputs that only accept singleton values, you can use the `-Clobber`

parameter to override the old value instead of trying to add to a collection. The following example assumes that you have already added a value. By using `-Clobber`

, the response from the following example overrides the existing value to return a value of "output #3":

```
Push-OutputBinding -Name response -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = "output #3"
}) -Clobber
```


#### Push-OutputBinding example: Queue output binding

`Push-OutputBinding`

is used to send data to output bindings, such as an [Azure Queue storage output binding](functions-bindings-storage-queue-output). In the following example, the message written to the queue has a value of "output #1":

```
Push-OutputBinding -Name outQueue -Value "output #1"
```


The output binding for a Storage queue accepts multiple output values. In this case, calling the following example after the first writes to the queue a list with two items: "output #1" and "output #2".

```
Push-OutputBinding -Name outQueue -Value "output #2"
```


The following example, when called after the previous two, adds two more values to the output collection:

```
Push-OutputBinding -Name outQueue -Value @("output #3", "output #4")
```


When written to the queue, the message contains these four values: "output #1", "output #2", "output #3", and "output #4".

#### Get-OutputBinding cmdlet

You can use the `Get-OutputBinding`

cmdlet to retrieve the values currently set for your output bindings. This cmdlet retrieves a hashtable that contains the names of the output bindings with their respective values.

The following example uses `Get-OutputBinding`

to return current binding values:

```
Get-OutputBinding
```


```
Name Value
---- -----
MyQueue myData
MyOtherQueue myData
```


`Get-OutputBinding`

also contains a parameter called `-Name`

, which can be used to filter the returned binding, as in the following example:

```
Get-OutputBinding -Name MyQ*
```


```
Name Value
---- -----
MyQueue myData
```


Wildcards (*) are supported in `Get-OutputBinding`

.

## Logging

Logging in PowerShell functions works like regular PowerShell logging. You can use the logging cmdlets to write to each output stream. Each cmdlet maps to a log level used by Functions.

| Functions logging level | Logging cmdlet |
|---|---|
| Error | `Write-Error` |
| Warning | `Write-Warning` |
| Information | `Write-Information` `Write-Host` `Write-Output` Writes to the `Information` log level. |
| Debug | `Write-Debug` |
| Trace | `Write-Progress` `Write-Verbose` |

In addition to these cmdlets, anything written to the pipeline is redirected to the `Information`

log level and displayed with the default PowerShell formatting.

Important

Using the `Write-Verbose`

or `Write-Debug`

cmdlets isn't enough to see verbose and debug level logging. You must also configure the log level threshold, which declares what level of logs you actually care about. To learn more, see [Configure the function app log level](#configure-the-function-app-log-level).

### Configure the function app log level

Azure Functions lets you define the threshold level to make it easy to control the way Functions writes to the logs. To set the threshold for all traces written to the console, use the `logging.logLevel.default`

property in the [ host.json file](functions-host-json). This setting applies to all functions in your function app.

The following example sets the threshold to enable verbose logging for all functions, but sets the threshold to enable debug logging for a function named `MyFunction`

:

```
{
"logging": {
"logLevel": {
"Function.MyFunction": "Debug",
"default": "Trace"
}
}
}
```


For more information, see [host.json reference](functions-host-json).

### Viewing the logs

If your Function App is running in Azure, you can use Application Insights to monitor it. Read [monitoring Azure Functions](functions-monitoring) to learn more about viewing and querying function logs.

If you're running your Function App locally for development, logs default to the file system. To see the logs in the console, set the `AZURE_FUNCTIONS_ENVIRONMENT`

environment variable to `Development`

before starting the Function App.

## Triggers and bindings types

There are many triggers and bindings available to you to use with your function app. For the full list of triggers and bindings, see [Supported bindings](functions-triggers-bindings#supported-bindings).

All triggers and bindings are represented in code as a few real data types:

- Hashtable
- string
- byte[]
- int
- double
- HttpRequestContext
- HttpResponseContext

The first five types in this list are standard .NET types. The last two are used only by the [HttpTrigger trigger](#http-triggers-and-bindings).

Each binding parameter in your functions must be one of these types.

### HTTP triggers and bindings

HTTP and webhook triggers and HTTP output bindings use request and response objects to represent the HTTP messaging.

#### Request object

The request object that is passed into the script is of the type `HttpRequestContext`

, which has the following properties:

| Property | Description | Type |
|---|---|---|
`Body` |
An object that contains the body of the request. `Body` is serialized into the best type based on the data. For example, if the data is JSON, it's passed in as a hashtable. If the data is a string, it's passed in as a string. |
object |
`Headers` |
A dictionary that contains the request headers. | Dictionary<string,string>* |
`Method` |
The HTTP method of the request. | string |
`Params` |
An object that contains the routing parameters of the request. | Dictionary<string,string>* |
`Query` |
An object that contains the query parameters. | Dictionary<string,string>* |
`Url` |
The URL of the request. | string |

* All `Dictionary<string,string>`

keys are case-insensitive.

#### Response object

The response object that you should send back is of the type `HttpResponseContext`

, which has the following properties:

| Property | Description | Type |
|---|---|---|
`Body` |
An object that contains the body of the response. | object |
`ContentType` |
A short hand for setting the content type for the response. | string |
`Headers` |
An object that contains the response headers. | Dictionary or Hashtable |
`StatusCode` |
The HTTP status code of the response. | string or int |

#### Accessing the request and response

When you work with HTTP triggers, you can access the HTTP request the same way you would with any other input binding. It's in the `param`

block.

Use an `HttpResponseContext`

object to return a response, as shown in the following example:

`function.json`


```
{
"bindings": [
{
"type": "httpTrigger",
"direction": "in",
"authLevel": "anonymous"
},
{
"type": "http",
"direction": "out",
"name": "Response"
}
]
}
```


`run.ps1`


```
param($req, $TriggerMetadata)
$name = $req.Query.Name
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = "Hello $name!"
})
```


The result of invoking this function would be:

```
irm http://localhost:5001?Name=Functions
Hello Functions!
```


### Type-casting for triggers and bindings

For certain bindings like the blob binding, you're able to specify the type of the parameter.

For example, to have data from Blob storage supplied as a string, add the following type cast to my `param`

block:

```
param([string] $myBlob)
```


## PowerShell profile

In PowerShell, there's the concept of a PowerShell profile. If you're not familiar with PowerShell profiles, see [About profiles](/en-us/powershell/module/microsoft.powershell.core/about/about_profiles).

In PowerShell Functions, the profile script is executed once per PowerShell worker instance in the app when first deployed and after being idled ([cold start](#cold-start). When concurrency is enabled by setting the [PSWorkerInProcConcurrencyUpperBound](#concurrency) value, the profile script is run for each runspace created.

When you create a function app using tools, such as Visual Studio Code and Azure Functions Core Tools, a default `profile.ps1`

is created for you. The default profile is maintained
[on the Core Tools GitHub repository](https://github.com/Azure/azure-functions-core-tools/blob/main/src/Cli/func/StaticResources/profile.ps1)
and contains:

- Automatic MSI authentication to Azure.
- The ability to turn on the Azure PowerShell
`AzureRM`

PowerShell aliases if you would like.

## PowerShell versions

The following table shows the PowerShell versions available to each major version of the Functions runtime, and the .NET version required:

| Functions version | PowerShell version | .NET version |
|---|---|---|
| 4.x | PowerShell 7.4 | .NET 8 |
| 4.x | PowerShell 7.2 (support ending) | .NET 6 |

You can see the current version by printing `$PSVersionTable`

from any function.

To learn more about Azure Functions runtime support policy, refer to this [article](language-support-policy)

Note

Support for PowerShell 7.2 in Azure Functions ends on November 8, 2024. You might have to resolve some breaking changes when upgrading your PowerShell 7.2 functions to run on PowerShell 7.4. Follow this [migration guide](https://github.com/Azure/azure-functions-powershell-worker/wiki/Upgrading-your-Azure-Function-Apps-to-run-on-PowerShell-7.4) to upgrade to PowerShell 7.4.

### Running local on a specific version

When you run PowerShell functions locally, you need to add the setting `"FUNCTIONS_WORKER_RUNTIME_VERSION" : "7.4"`

to the `Values`

array in the local.setting.json file in the project root. When running locally on PowerShell 7.4, your local.settings.json file looks like the following example:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "",
"FUNCTIONS_WORKER_RUNTIME": "powershell",
"FUNCTIONS_WORKER_RUNTIME_VERSION" : "7.4"
}
}
```


Note

In PowerShell Functions, the value "~7" for FUNCTIONS_WORKER_RUNTIME_VERSION refers to "7.0.x". We don't automatically upgrade PowerShell Function apps that have "~7" to "7.4". Going forward, for PowerShell Function Apps, we require that apps specify both the major and minor version they want to target. It's necessary to mention "7.4" if you want to target "7.4.x"

### Changing the PowerShell version

Take these considerations into account before you migrate your PowerShell function app to PowerShell 7.4:

Because the migration might introduce breaking changes in your app, review this

[migration guide](https://github.com/Azure/azure-functions-powershell-worker/wiki/Upgrading-your-Azure-Function-Apps-to-run-on-PowerShell-7.4)before upgrading your app to PowerShell 7.4.Make sure that your function app is running on the latest version of the Functions runtime in Azure, which is version 4.x. For more information, see

[View the current runtime version](set-runtime-version#view-the-current-runtime-version).

Use the following steps to change the PowerShell version used by your function app. You can perform this operation either in the Azure portal or by using PowerShell.

In the

[Azure portal](https://portal.azure.com), browse to your function app.Under

**Settings**, choose**Configuration**. In the**General settings**tab, locate the**PowerShell version**.Choose your desired

**PowerShell Core version**and select**Save**. When warned about the pending restart choose**Continue**. The function app restarts on the chosen PowerShell version.

Note

Azure Functions support for PowerShell 7.4 is generally available (GA). You might see PowerShell 7.4 still indicated as preview in the Azure portal, but this value will be updated soon to reflect the GA status.

The function app restarts after the change is made to the configuration.

## Dependency management

Managing modules in Azure Functions written in PowerShell can be approached in two ways: using the Managed Dependencies feature or including the modules directly in your app content. Each method has its own advantages, and choosing the right one depends on your specific needs.

### Choosing the right module management approach

**Why use the Managed Dependencies feature?**

**Simplified initial installation**: Automatically handles module installation based on your`requirements.psd1`

file.**Auto-upgrades**: Modules are updated automatically, including security fixes, without requiring manual intervention.

**Why include modules in app content?**

**No dependency on the PowerShell Gallery**: Modules are bundled with your app, eliminating external dependencies.**More control**: Avoids the risk of regressions caused by automatic upgrades, giving you full control over which module versions are used.**Compatibility**: Works on Flex Consumption and is recommended for other Linux SKUs.

### Managed Dependencies feature

The Managed Dependencies feature allows Azure Functions to automatically download and manage PowerShell modules specified in the `requirements.psd1`

file. This feature is enabled by default in new PowerShell function apps.

#### Configuring requirements.psd1

To use Managed Dependencies in Azure Functions with PowerShell, you need to configure a `requirements.psd1`

file. This file specifies the modules your function requires, and Azure Functions automatically downloads and updates these modules to ensure that your environment stays up-to-date.

Here's how to set up and configure the `requirements.psd1`

file:

- Create a
`requirements.psd1`

file in the root directory of your Azure Function if one doesn't already exist. - Define the modules and their versions in a PowerShell data structure.

Example `requirements.psd1`

file:

```
@{
'Az' = '9.*' # Specifies the Az module and will use the latest version with major version 9
}
```


### Including modules in app content

For more control over your module versions and to avoid dependencies on external resources, you can include modules directly in your function app’s content.

To include custom modules:

**Create a**at the root of your function app.`Modules`

folder`mkdir ./Modules`

**Copy modules to the**using one of the following methods:`Modules`

folder**If modules are already available locally**:`Copy-Item -Path /mymodules/mycustommodule -Destination ./Modules -Recurse`

**Using**:`Save-Module`

to retrieve from the PowerShell Gallery`Save-Module -Name MyCustomModule -Path ./Modules`

**Using**:`Save-PSResource`

from the`PSResourceGet`

module`Save-PSResource -Name MyCustomModule -Path ./Modules`


Your function app should have the following structure:

```
PSFunctionApp
| - MyFunction
| | - run.ps1
| | - function.json
| - Modules
| | - MyCustomModule
| | - MyOtherCustomModule
| | - MySpecialModule.psm1
| - local.settings.json
| - host.json
| - requirements.psd1
```


When you start your function app, the PowerShell language worker adds this `Modules`

folder to the `$env:PSModulePath`

so that you can rely on module autoloading just as you would in a regular PowerShell script.

Note

If your function app is under source control, you should confirm that all the content in the Modules folder that you add isn't excluded by .gitignore. For example, if one of your modules has a bin folder that is getting excluded, you would want to modify the .gitignore by replacing `bin`

with

```
**/bin/**
!Modules/**
```


### Troubleshooting Managed Dependencies

#### Enabling Managed Dependencies

In order for Managed Dependencies to function, the feature must be enabled in host.json:

```
{
"managedDependency": {
"enabled": true
}
}
```


#### Target specific versions

When targeting specific module versions, it’s important to follow both of the following steps to ensure the correct module version is loaded:

**Specify the module version in**`requirements.psd1`

:`@{ 'Az.Accounts' = '1.9.5' }`

**Add an import statement to**`profile.ps1`

:`Import-Module Az.Accounts -RequiredVersion '1.9.5'`


Following these steps ensures the specified version is loaded when your function starts.

#### Configure specific Managed Dependency interval settings

You can configure how Managed Dependencies are downloaded and installed using the following app settings:

| Setting | Default Value | Description |
|---|---|---|
MDMaxBackgroundUpgradePeriod |
`7.00:00:00` (seven days) |
Controls the background update period for PowerShell function apps. |
MDNewSnapshotCheckPeriod |
`01:00:00` (one hour) |
Specifies how often the PowerShell worker checks for updates. |
MDMinBackgroundUpgradePeriod |
`1.00:00:00` (one day) |
Minimum time between upgrade checks. |

#### Dependency management considerations

**Internet Access**: Managed Dependencies require access to`https://www.powershellgallery.com`

to download modules. Ensure that your environment allows this access, including modifying firewall/VNet rules as needed. The required endpoints are described in[Troubleshooting Cmdlets](/en-us/powershell/gallery/how-to/getting-support/troubleshooting-cmdlets#required-network-endpoints). These endpoints can be added to the allow list, as required.**License Acceptance**: Managed Dependencies doesn't support modules that require license acceptance.**Flex Consumption Plan**: The Managed Dependencies feature isn't supported in the Flex Consumption plan. Use custom modules instead.**Module Locations**: On your local computer, modules are typically installed in one of the globally available folders in your`$env:PSModulePath`

. When running in Azure, the`$env:PSModulePath`

for a PowerShell function app differs from`$env:PSModulePath`

in a regular PowerShell script and contains both the`Modules`

folder uploaded with your app contents and a separate location managed by Managed Dependencies.

## Environment variables

In Functions, [app settings](functions-app-settings), such as service connection strings, are exposed as environment variables during execution. You can access these settings using `$env:NAME_OF_ENV_VAR`

, as shown in the following example:

```
param($myTimer)
Write-Host "PowerShell timer trigger function ran! $(Get-Date)"
Write-Host $env:AzureWebJobsStorage
Write-Host $env:WEBSITE_SITE_NAME
```


There are several ways that you can add, update, and delete function app settings:

Changes to function app settings require your function app to be restarted.

When running locally, app settings are read from the [local.settings.json](functions-develop-local#local-settings-file) project file.

## Concurrency

By default, the Functions PowerShell runtime can only process one invocation of a function at a time. However, this concurrency level might not be sufficient in the following situations:

- When you're trying to handle a large number of invocations at the same time.
- When you have functions that invoke other functions inside the same function app.

There are a few concurrency models that you could explore depending on the type of workload:

Increase

`FUNCTIONS_WORKER_PROCESS_COUNT`

. Increasing this setting allows handling function invocations in multiple processes within the same instance, which introduces certain CPU and memory overhead. In general, I/O-bound functions don't suffer from this overhead. For CPU-bound functions, the impact might be significant.Increase the

`PSWorkerInProcConcurrencyUpperBound`

app setting value. Increasing this setting allows creating multiple runspaces within the same process, which significantly reduces CPU and memory overhead.

You set these environment variables in the [app settings](functions-app-settings) of your function app.

Depending on your use case, Durable Functions might significantly improve scalability. To learn more, see [Durable Functions application patterns](durable/durable-functions-overview?tabs=powershell#application-patterns).

Note

You might get "requests are being queued due to no available runspaces" warnings. This message isn't an error. The message is telling you that requests are being queued. They're handled when the previous requests are completed.

### Considerations for using concurrency

PowerShell is a *single_threaded* scripting language by default. However, concurrency can be added by using multiple PowerShell runspaces in the same process. The number of runspaces created, and therefore the number of concurrent threads per worker, is limited by the `PSWorkerInProcConcurrencyUpperBound`

application setting. By default, the number of runspaces is set to 1,000 in version 4.x of the Functions runtime. In versions 3.x and below, the maximum number of runspaces is set to 1. The throughput of your function app is affected by the amount of CPU and memory available in the selected plan.

Azure PowerShell uses some *process-level* contexts and state to help save you from excess typing. However, if you turn on concurrency in your function app and invoke actions that change state, you could end up with race conditions. These race conditions are difficult to debug because one invocation relies on a certain state and the other invocation changed the state.

There's immense value in concurrency with Azure PowerShell, since some operations can take a considerable amount of time. However, you must proceed with caution. If you suspect that you're experiencing a race condition, set the PSWorkerInProcConcurrencyUpperBound app setting to `1`

and instead use [language worker process level isolation](functions-app-settings#functions_worker_process_count) for concurrency.

## Configure function scriptFile

By default, a PowerShell function is executed from `run.ps1`

, a file that shares the same parent directory as its corresponding `function.json`

.

The `scriptFile`

property in the `function.json`

can be used to get a folder structure that looks like the following example:

```
FunctionApp
| - host.json
| - myFunction
| | - function.json
| - lib
| | - PSFunction.ps1
```


In this case, the `function.json`

for `myFunction`

includes a `scriptFile`

property referencing the file with the exported function to run.

```
{
"scriptFile": "../lib/PSFunction.ps1",
"bindings": [
// ...
]
}
```


## Use PowerShell modules by configuring an entryPoint

PowerShell functions in this article are shown with the default `run.ps1`

script file generated by the templates.
However, you can also include your functions in PowerShell modules. You can reference your specific function code in the module by using the `scriptFile`

and `entryPoint`

fields in the function.json` configuration file.

In this case, `entryPoint`

is the name of a function or cmdlet in the PowerShell module referenced in `scriptFile`

.

Consider the following folder structure:

```
FunctionApp
| - host.json
| - myFunction
| | - function.json
| - lib
| | - PSFunction.psm1
```


Where `PSFunction.psm1`

contains:

```
function Invoke-PSTestFunc {
param($InputBinding, $TriggerMetadata)
Push-OutputBinding -Name OutputBinding -Value "output"
}
Export-ModuleMember -Function "Invoke-PSTestFunc"
```


In this example, the configuration for `myFunction`

includes a `scriptFile`

property that references `PSFunction.psm1`

, which is a PowerShell module in another folder. The `entryPoint`

property references the `Invoke-PSTestFunc`

function, which is the entry point in the module.

```
{
"scriptFile": "../lib/PSFunction.psm1",
"entryPoint": "Invoke-PSTestFunc",
"bindings": [
// ...
]
}
```


With this configuration, the `Invoke-PSTestFunc`

gets executed exactly as a `run.ps1`

would.

## Considerations for PowerShell functions

When you work with PowerShell functions, be aware of the considerations in the following sections.

### Cold Start

When developing Azure Functions in the [serverless hosting model](consumption-plan), cold starts are a reality. *Cold start* refers to period of time it takes for your function app to start running to process a request. Cold start happens more frequently in the Consumption plan because your function app gets shut down during periods of inactivity.

#### Avoid using Install-Module

Running `Install-Module`

in your function script on each invocation can cause performance issues. Instead, use `Save-Module`

or `Save-PSResource`

before publishing your function app to bundle the necessary modules.

For more information, see [Dependency management](#dependency-management).

## Next steps

For more information, see the following resources:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai-embeddingsstore-output -->

# Azure OpenAI embeddings store output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Azure OpenAI extension for Azure Functions is currently in preview.

The Azure OpenAI embeddings store output binding allows you to write files to a semantic document store that can be referenced later in a semantic search.

For information on setup and configuration details of the Azure OpenAI extension, see [Azure OpenAI extensions for Azure Functions](functions-bindings-openai). To learn more about semantic ranking in Azure AI Search, see [Semantic ranking in Azure AI Search](/en-us/azure/search/semantic-search-overview).

Note

References and examples are only provided for the [Node.js v4 model](functions-reference-node?pivots=nodejs-model-v4).

Note

References and examples are only provided for the [Python v2 model](functions-reference-python?pivots=python-mode-decorators#programming-model).

Note

While both C# process models are supported, only [isolated worker model](dotnet-isolated-process-guide) examples are provided.

## Example

This example writes an HTTP input stream to a semantic document store at the provided URL.

```
public class EmbeddingsRequest
{
[JsonPropertyName("url")]
public string? Url { get; set; }
}
[Function("IngestFile")]
public static async Task<EmbeddingsStoreOutputResponse> IngestFile(
[HttpTrigger(AuthorizationLevel.Function, "post")] HttpRequestData req)
{
using StreamReader reader = new(req.Body);
string request = await reader.ReadToEndAsync();
EmbeddingsStoreOutputResponse badRequestResponse = new()
{
HttpResponse = new BadRequestResult(),
SearchableDocument = new SearchableDocument(string.Empty)
};
if (string.IsNullOrWhiteSpace(request))
{
return badRequestResponse;
}
EmbeddingsRequest? requestBody = JsonSerializer.Deserialize<EmbeddingsRequest>(request);
if (string.IsNullOrWhiteSpace(requestBody?.Url))
{
throw new ArgumentException("Invalid request body. Make sure that you pass in {\"url\": value } as the request body.");
}
if (!Uri.TryCreate(requestBody.Url, UriKind.Absolute, out Uri? uri))
{
return badRequestResponse;
}
string filename = Path.GetFileName(uri.AbsolutePath);
return new EmbeddingsStoreOutputResponse
{
HttpResponse = new OkObjectResult(new { status = HttpStatusCode.OK }),
SearchableDocument = new SearchableDocument(filename)
};
}
```


This example writes an HTTP input stream to a semantic document store at the provided URL.

```
@FunctionName("IngestFile")
public HttpResponseMessage ingestFile(
@HttpTrigger(
name = "req",
methods = {HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<EmbeddingsRequest> request,
@EmbeddingsStoreOutput(name="EmbeddingsStoreOutput", input = "{url}", inputType = InputType.Url,
storeConnectionName = "AISearchEndpoint", collection = "openai-index",
embeddingsModel = "%EMBEDDING_MODEL_DEPLOYMENT_NAME%") OutputBinding<EmbeddingsStoreOutputResponse> output,
final ExecutionContext context) throws URISyntaxException {
if (request.getBody() == null || request.getBody().getUrl() == null)
{
throw new IllegalArgumentException("Invalid request body. Make sure that you pass in {\"url\": value } as the request body.");
}
URI uri = new URI(request.getBody().getUrl());
String filename = Paths.get(uri.getPath()).getFileName().toString();
EmbeddingsStoreOutputResponse embeddingsStoreOutputResponse = new EmbeddingsStoreOutputResponse(new SearchableDocument(filename));
output.setValue(embeddingsStoreOutputResponse);
JSONObject response = new JSONObject();
response.put("status", "success");
response.put("title", filename);
return request.createResponseBuilder(HttpStatus.CREATED)
.header("Content-Type", "application/json")
.body(response)
.build();
}
public class EmbeddingsStoreOutputResponse {
private SearchableDocument searchableDocument;
public EmbeddingsStoreOutputResponse(SearchableDocument searchableDocument) {
this.searchableDocument = searchableDocument;
}
public SearchableDocument getSearchableDocument() {
return searchableDocument;
}
}
```


This example writes an HTTP input stream to a semantic document store at the provided URL.

```
const embeddingsStoreOutput = output.generic({
type: "embeddingsStore",
input: "{url}",
inputType: "url",
connectionName: "AISearchEndpoint",
collection: "openai-index",
embeddingsModel: "%EMBEDDING_MODEL_DEPLOYMENT_NAME%"
});
app.http('IngestFile', {
methods: ['POST'],
authLevel: 'function',
extraOutputs: [embeddingsStoreOutput],
handler: async (request, context) => {
let requestBody = await request.json();
if (!requestBody || !requestBody.url) {
throw new Error("Invalid request body. Make sure that you pass in {\"url\": value } as the request body.");
}
let uri = requestBody.url;
let url = new URL(uri);
let fileName = path.basename(url.pathname);
context.extraOutputs.set(embeddingsStoreOutput, { title: fileName });
let response = {
status: "success",
title: fileName
};
return { status: 202, jsonBody: response }
}
});
```


```
interface EmbeddingsRequest {
url?: string;
}
const embeddingsStoreOutput = output.generic({
type: "embeddingsStore",
input: "{url}",
inputType: "url",
connectionName: "AISearchEndpoint",
collection: "openai-index",
embeddingsModel: "%EMBEDDING_MODEL_DEPLOYMENT_NAME%"
});
app.http('IngestFile', {
methods: ['POST'],
authLevel: 'function',
extraOutputs: [embeddingsStoreOutput],
handler: async (request, context) => {
let requestBody: EmbeddingsRequest | null = await request.json();
if (!requestBody || !requestBody.url) {
throw new Error("Invalid request body. Make sure that you pass in {\"url\": value } as the request body.");
}
let uri = requestBody.url;
let url = new URL(uri);
let fileName = path.basename(url.pathname);
context.extraOutputs.set(embeddingsStoreOutput, { title: fileName });
let response = {
status: "success",
title: fileName
};
return { status: 202, jsonBody: response }
}
});
```


This example writes an HTTP input stream to a semantic document store at the provided URL.

Here's the *function.json* file for ingesting files:

```
{
"bindings": [
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "Request",
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
"name": "EmbeddingsStoreOutput",
"type": "embeddingsStore",
"direction": "out",
"input": "{url}",
"inputType": "Url",
"storeConnectionName": "AISearchEndpoint",
"collection": "openai-index",
"embeddingsModel": "%EMBEDDING_MODEL_DEPLOYMENT_NAME%"
}
]
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

```
using namespace System.Net
param($Request, $TriggerMetadata)
$ErrorActionPreference = 'Stop'
$inputJson = $Request.Body
if (-not $inputJson -or -not $inputJson.Url) {
throw 'Invalid request body. Make sure that you pass in {\"url\": value } as the request body.'
}
$uri = [URI]$inputJson.Url
$filename = [System.IO.Path]::GetFileName($uri.AbsolutePath)
Push-OutputBinding -Name EmbeddingsStoreOutput -Value @{
"title" = $filename
}
$response = @{
"status" = "success"
"title" = $filename
}
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $response
Headers = @{
"Content-Type" = "application/json"
}
})
```


This example writes an HTTP input stream to a semantic document store at the provided URL.

```
@app.function_name("IngestFile")
@app.route(methods=["POST"])
@app.embeddings_store_output(
arg_name="requests",
input="{url}",
input_type="url",
store_connection_name="AISearchEndpoint",
collection="openai-index",
embeddings_model="%EMBEDDING_MODEL_DEPLOYMENT_NAME%",
)
def ingest_file(
req: func.HttpRequest, requests: func.Out[str]
) -> func.HttpResponse:
user_message = req.get_json()
if not user_message:
return func.HttpResponse(
json.dumps({"message": "No message provided"}),
status_code=400,
mimetype="application/json",
)
file_name_with_extension = os.path.basename(user_message["url"])
title = os.path.splitext(file_name_with_extension)[0]
create_request = {"title": title}
requests.set(json.dumps(create_request))
response_json = {"status": "success", "title": title}
return func.HttpResponse(
json.dumps(response_json), status_code=200, mimetype="application/json"
)
```


## Attributes

Apply the `EmbeddingsStoreOutput`

attribute to define an embeddings store output binding, which supports these parameters:

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
StoreConnectionName |
The name of an app setting or environment variable that contains the connection string value. This property supports binding expressions. |
Collection |
The name of the collection or table or index to search. This property supports binding expressions. |

## Annotations

The `EmbeddingsStoreOutput`

annotation enables you to define an embeddings store output binding, which supports these parameters:

| Element | Description |
|---|---|
name |
Gets or sets the name of the output binding. |
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
storeConnectionName |
The name of an app setting or environment variable that contains the connection string value. This property supports binding expressions. |
collection |
The name of the collection or table or index to search. This property supports binding expressions. |

## Decorators

During the preview, define the output binding as a `generic_output_binding`

binding of type `semanticSearch`

, which supports these parameters:

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
store_connection_name |
The name of an app setting or environment variable that contains the connection string value. This property supports binding expressions. |
collection |
The name of the collection or table or index to search. This property supports binding expressions. |

## Configuration

The binding supports these configuration properties that you set in the function.json file.

| Property | Description |
|---|---|
type |
Must be `embeddingsStore` . |
direction |
Must be `out` . |
name |
The name of the output binding. |
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
storeConnectionName |
The name of an app setting or environment variable that contains the connection string value. This property supports binding expressions. |
collection |
The name of the collection or table or index to search. This property supports binding expressions. |

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
storeConnectionName |
The name of an app setting or environment variable that contains the connection string value. This property supports binding expressions. |
collection |
The name of the collection or table or index to search. This property supports binding expressions. |

## Usage

See the [Example section](#example) for complete examples.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai-semanticsearch-input -->

# Azure OpenAI Semantic Search Input Binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Azure OpenAI extension for Azure Functions is currently in preview.

The Azure OpenAI semantic search input binding allows you to use semantic search on your embeddings.

For information on setup and configuration details of the Azure OpenAI extension, see [Azure OpenAI extensions for Azure Functions](functions-bindings-openai). To learn more about semantic ranking in Azure AI Search, see [Semantic ranking in Azure AI Search](/en-us/azure/search/semantic-search-overview).

Note

References and examples are only provided for the [Node.js v4 model](functions-reference-node?pivots=nodejs-model-v4).

Note

References and examples are only provided for the [Python v2 model](functions-reference-python?pivots=python-mode-decorators#programming-model).

Note

While both C# process models are supported, only [isolated worker model](dotnet-isolated-process-guide) examples are provided.

## Example

This example shows how to perform a semantic search on a file.

```
[Function("PromptFile")]
public static IActionResult PromptFile(
[HttpTrigger(AuthorizationLevel.Function, "post")] SemanticSearchRequest unused,
[SemanticSearchInput("AISearchEndpoint", "openai-index", Query = "{prompt}", ChatModel = "%CHAT_MODEL_DEPLOYMENT_NAME%", EmbeddingsModel = "%EMBEDDING_MODEL_DEPLOYMENT_NAME%")] SemanticSearchContext result)
{
return new ContentResult { Content = result.Response, ContentType = "text/plain" };
}
```


This example shows how to perform a semantic search on a file.

```
@FunctionName("PromptFile")
public HttpResponseMessage promptFile(
@HttpTrigger(
name = "req",
methods = {HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<SemanticSearchRequest> request,
@SemanticSearch(name = "search", searchConnectionName = "AISearchEndpoint", collection = "openai-index", query = "{prompt}", chatModel = "%CHAT_MODEL_DEPLOYMENT_NAME%", embeddingsModel = "%EMBEDDING_MODEL_DEPLOYMENT_NAME%", isReasoningModel = false ) String semanticSearchContext,
final ExecutionContext context) {
String response = new JSONObject(semanticSearchContext).getString("Response");
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(response)
.build();
}
public class SemanticSearchRequest {
public String prompt;
public String getPrompt() {
return prompt;
}
public void setPrompt(String prompt) {
this.prompt = prompt;
}
}
```


This example shows how to perform a semantic search on a file.

```
const semanticSearchInput = input.generic({
type: "semanticSearch",
connectionName: "AISearchEndpoint",
collection: "openai-index",
query: "{prompt}",
chatModel: "%CHAT_MODEL_DEPLOYMENT_NAME%",
embeddingsModel: "%EMBEDDING_MODEL_DEPLOYMENT_NAME%"
});
app.http('PromptFile', {
methods: ['POST'],
authLevel: 'function',
extraInputs: [semanticSearchInput],
handler: async (_request, context) => {
var responseBody = context.extraInputs.get(semanticSearchInput)
return { status: 200, body: responseBody.Response.trim() }
}
});
```


```
const semanticSearchInput = input.generic({
type: "semanticSearch",
connectionName: "AISearchEndpoint",
collection: "openai-index",
query: "{prompt}",
chatModel: "%CHAT_MODEL_DEPLOYMENT_NAME%",
embeddingsModel: "%EMBEDDING_MODEL_DEPLOYMENT_NAME%"
});
app.http('PromptFile', {
methods: ['POST'],
authLevel: 'function',
extraInputs: [semanticSearchInput],
handler: async (_request, context) => {
var responseBody: any = context.extraInputs.get(semanticSearchInput)
return { status: 200, body: responseBody.Response.trim() }
}
});
```


This example shows how to perform a semantic search on a file.

Here's the *function.json* file for prompting a file:

```
{
"bindings": [
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "Request",
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
"name": "SemanticSearchInput",
"type": "semanticSearch",
"direction": "in",
"searchConnectionName": "AISearchEndpoint",
"collection": "openai-index",
"query": "{prompt}",
"chatModel": "%CHAT_MODEL_DEPLOYMENT_NAME%",
"embeddingsModel": "%EMBEDDING_MODEL_DEPLOYMENT_NAME%"
}
]
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

```
using namespace System.Net
param($Request, $TriggerMetadata, $SemanticSearchInput)
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $SemanticSearchInput.Response
})
```


This example shows how to perform a semantic search on a file.

```
@app.function_name("PromptFile")
@app.route(methods=["POST"])
@app.semantic_search_input(
arg_name="result",
search_connection_name="AISearchEndpoint",
collection="openai-index",
query="{prompt}",
embeddings_model="%EMBEDDING_MODEL_DEPLOYMENT_NAME%",
chat_model="%CHAT_MODEL_DEPLOYMENT_NAME%",
)
def prompt_file(req: func.HttpRequest, result: str) -> func.HttpResponse:
result_json = json.loads(result)
response_json = {
"content": result_json.get("Response"),
"content_type": "text/plain",
}
return func.HttpResponse(
json.dumps(response_json), status_code=200, mimetype="application/json"
)
```


## Attributes

Apply the `SemanticSearchInput`

attribute to define a semantic search input binding, which supports these parameters:

| Parameter | Description |
|---|---|
SearchConnectionName |
The name of an app setting or environment variable that contains the connection string value. This property supports binding expressions. |
Collection |
The name of the collection or table or index to search. This property supports binding expressions. |
Query |
The semantic query text to use for searching. This property supports binding expressions. |
EmbeddingsModel |
Optional. The ID of the model to use for embeddings. The default value is `text-embedding-3-small` . This property supports binding expressions. |
ChatModel |
Optional. Gets or sets the name of the Large Language Model to invoke for chat responses. The default value is `gpt-3.5-turbo` . This property supports binding expressions. |
AIConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
SystemPrompt |
Optional. Gets or sets the system prompt to use for prompting the large language model. The system prompt is appended with knowledge that is fetched as a result of the `Query` . The combined prompt is sent to the OpenAI Chat API. This property supports binding expressions. |
MaxKnowledgeCount |
Optional. Gets or sets the number of knowledge items to inject into the `SystemPrompt` . |
IsReasoningModel |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Annotations

The `SemanticSearchInput`

annotation enables you to define a semantic search input binding, which supports these parameters:

| Element | Description |
|---|---|
name |
Gets or sets the name of the input binding. |
searchConnectionName |
The name of an app setting or environment variable that contains the connection string value. This property supports binding expressions. |
collection |
The name of the collection or table or index to search. This property supports binding expressions. |
query |
The semantic query text to use for searching. This property supports binding expressions. |
embeddingsModel |
Optional. The ID of the model to use for embeddings. The default value is `text-embedding-3-small` . This property supports binding expressions. |
chatModel |
Optional. Gets or sets the name of the Large Language Model to invoke for chat responses. The default value is `gpt-3.5-turbo` . This property supports binding expressions. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
systemPrompt |
Optional. Gets or sets the system prompt to use for prompting the large language model. The system prompt is appended with knowledge that is fetched as a result of the `Query` . The combined prompt is sent to the OpenAI Chat API. This property supports binding expressions. |
maxKnowledgeCount |
Optional. Gets or sets the number of knowledge items to inject into the `SystemPrompt` . |
isReasoningModel |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Decorators

During the preview, define the input binding as a `generic_input_binding`

binding of type `semanticSearch`

, which supports these parameters:

| Parameter | Description |
|---|---|
arg_name |
The name of the variable that represents the binding parameter. |
search_connection_name |
The name of an app setting or environment variable that contains the connection string value. This property supports binding expressions. |
collection |
The name of the collection or table or index to search. This property supports binding expressions. |
query |
The semantic query text to use for searching. This property supports binding expressions. |
embeddings_model |
Optional. The ID of the model to use for embeddings. The default value is `text-embedding-3-small` . This property supports binding expressions. |
chat_model |
Optional. Gets or sets the name of the Large Language Model to invoke for chat responses. The default value is `gpt-3.5-turbo` . This property supports binding expressions. |
ai_connection_name |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
system_prompt |
Optional. Gets or sets the system prompt to use for prompting the large language model. The system prompt is appended with knowledge that is fetched as a result of the `Query` . The combined prompt is sent to the OpenAI Chat API. This property supports binding expressions. |
max_knowledge_count |
Optional. Gets or sets the number of knowledge items to inject into the `SystemPrompt` . |
is_reasoning _model |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Configuration

The binding supports these configuration properties that you set in the function.json file.

| Property | Description |
|---|---|
type |
Must be `semanticSearch` . |
direction |
Must be `in` . |
name |
The name of the input binding. |
searchConnectionName |
Gets or sets the name of an app setting or environment variable that contains a connection string value. This property supports binding expressions. |
collection |
The name of the collection or table or index to search. This property supports binding expressions. |
query |
The semantic query text to use for searching. This property supports binding expressions. |
embeddingsModel |
Optional. The ID of the model to use for embeddings. The default value is `text-embedding-3-small` . This property supports binding expressions. |
chatModel |
Optional. Gets or sets the name of the Large Language Model to invoke for chat responses. The default value is `gpt-3.5-turbo` . This property supports binding expressions. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
systemPrompt |
Optional. Gets or sets the system prompt to use for prompting the large language model. The system prompt is appended with knowledge that is fetched as a result of the `Query` . The combined prompt is sent to the OpenAI Chat API. This property supports binding expressions. |
maxKnowledgeCount |
Optional. Gets or sets the number of knowledge items to inject into the `SystemPrompt` . |
isReasoningModel |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Configuration

The binding supports these properties, which are defined in your code:

| Property | Description |
|---|---|
searchConnectionName |
The name of an app setting or environment variable that contains the connection string value. This property supports binding expressions. |
collection |
The name of the collection or table or index to search. This property supports binding expressions. |
query |
The semantic query text to use for searching. This property supports binding expressions. |
embeddingsModel |
Optional. The ID of the model to use for embeddings. The default value is `text-embedding-3-small` . This property supports binding expressions. |
chatModel |
Optional. Gets or sets the name of the Large Language Model to invoke for chat responses. The default value is `gpt-3.5-turbo` . This property supports binding expressions. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
systemPrompt |
Optional. Gets or sets the system prompt to use for prompting the large language model. The system prompt is appended with knowledge that is fetched as a result of the `Query` . The combined prompt is sent to the OpenAI Chat API. This property supports binding expressions. |
maxKnowledgeCount |
Optional. Gets or sets the number of knowledge items to inject into the `SystemPrompt` . |
isReasoningModel |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Usage

See the [Example section](#example) for complete examples.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-consumption-costs -->

# Estimating consumption-based costs

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to estimate plan costs for both the [Flex Consumption plan](flex-consumption-plan) and the legacy [Consumption plan](consumption-plan).

Choose the hosting option that best supports the feature, performance, and cost requirements for your function executions. For more information, see [Azure Functions scale and hosting](functions-scale).

This article focuses on the two consumption plans because billing in these plans depends on active periods of executions inside each instance.

Provides fast horizontal scaling, with flexible compute options, virtual network integration, and full support for connections using Microsoft Entra ID authentication. In this plan, instances dynamically scale out based on configured per-instance concurrency, incoming events, and per-function workloads for optimal efficiency. Flex Consumption is the recommended plan for serverless hosting. For more information, see [Azure Functions Flex Consumption plan hosting](flex-consumption-plan).

Durable Functions can also run in both of these plans. For more information about the cost considerations when using Durable Functions, see [Durable Functions billing](durable/durable-functions-billing).

## Consumption-based costs

The way that consumption-based costs are calculated, including free grants, depends on the specific plan. For the most current cost and grant information, see the [Azure Functions pricing page](https://azure.microsoft.com/pricing/details/functions/).

There are two modes by which your costs are determined when running your apps in the Flex Consumption plan. Each mode is determined on a per-instance basis.

| Billing mode | Description |
|---|---|
On Demand |
When running in on demand mode, you are billed only for the amount of time your function code is executing on your available instances. In on demand mode, no minimum instance count is required. You're billed for:• The total amount of memory provisioned while each on demand instance is actively executing functions (in GB-seconds), minus a free grant of GB-s per month.• The total number of executions, minus a free grant (number) of executions per month. |
Always ready |
You can configure one or more instances, assigned to specific trigger types (HTTP/Durable/Blob) and individual functions, that are always available to handle requests. When you have any always ready instances enabled, you're billed for: • The total amount of memory provisioned across all of your always ready instances, known as the baseline (in GB-seconds).• The total amount of memory provisioned during the time each always ready instance is actively executing functions (in GB-seconds).• The total number of executions. In always ready billing, there are no free grants. |

For the most up-to-date information on execution pricing, always ready baseline costs, and free grants for on demand executions, see the [Azure Functions pricing page](https://azure.microsoft.com/pricing/details/functions/#pricing).

This diagram shows how on-demand costs are determined in this plan:


In addition to execution time, when you use one or more always ready instances, you pay a lower, baseline rate for the number of always ready instances you maintain. Execution time for always ready instances might be cheaper than execution time on instances with on demand execution.

Important

This article uses on-demand pricing to help you understand example calculations. Always check the current costs on the [Azure Functions pricing page](https://azure.microsoft.com/pricing/details/functions/) when estimating costs you might incur while running your functions in the Flex Consumption plan.

Consider a function app that has only HTTP triggers with these basic facts:

- HTTP triggers handle 40 constant requests per second.
- HTTP triggers handle 10 concurrent requests.
- The instance memory size is 2,048 MB.
- You configure
*no always ready instances*, which means the app can scale to zero.

In a situation like this, pricing depends more on the kind of work done during code execution. Let's look at two workload scenarios:

**CPU-bound workload:**In a CPU-bound workload, there's no advantage to processing multiple requests in parallel in the same instance. This limitation means that you're better off distributing each request to its own instance so requests complete as quickly as possible without contention. In this scenario, set a low[HTTP trigger concurrency](functions-concurrency#http-trigger-concurrency)of`1`

. With 10 concurrent requests, the app scales to a steady state of roughly 10 instances, and each instance is continuously active processing one request at a time.Because the size of each instance is ~2 GB, the consumption for a single continuously active instance is

`2 GB * 3600 s = 7200 GB-s`

. Assuming an on-demand execution rate of $0.000026 GB-s (without any free grants applied), the cost becomes`$0.1872 USD`

per hour per instance. Because the CPU-bound app scales to 10 instances, the total hourly rate for execution time is`$1.872 USD`

.Similarly, the on-demand per-execution charge (without any free grants) of 40 requests per second is equal to

`40 * 3600 = 144,000`

or`0.144 million`

executions per hour. Assuming an on-demand rate of`$0.40`

per million executions, the total (grant-free) hourly cost of executions is`0.144 * $0.40`

, which is`$0.0576`

per hour.In this scenario, the total hourly cost of running on-demand on 10 instances is

`$1.872 + $0.0576s = $1.9296 USD`

.**IO bound workload:**In an IO-bound workload, most of the application time is spent waiting on incoming request, which might be limited by network throughput or other upstream factors. Because of the limited inputs, the code can process multiple operations concurrently without negative impacts. In this scenario, assume you can process all 10 concurrent requests on the same instance.Because consumption charges are based only on the memory of each active instance, the consumption charge calculation is simply

`2 GB * 3600 s = 7200 GB-s`

, which at the assumed on-demand execution rate (without any free grants applied) is`$0.1872 USD`

per hour for the single instance.As in the CPU-bound scenario, the on-demand per-execution charge (without any free grants) of 40 requests per second is equal to

`40 * 3600 = 144,000`

or 0.144 million executions per hour. In this case, the total (grant-free) hourly cost of executions`0.144 * $0.40`

, which is`$0.0576`

per hour.In this scenario, the total hourly cost of running on-demand a single instance is

`$0.1872 + $0.0576 = $0.245 USD`

.

## Behaviors affecting execution time

The following behaviors of your functions can affect the execution time:

**Triggers and bindings**: The time taken to read input from and write output to your[function bindings](functions-triggers-bindings)counts as execution time. For example, when your function uses an output binding to write a message to an Azure storage queue, your execution time includes the time taken to write the message to the queue, which is included in the calculation of the function cost.**Asynchronous execution**: The time that your function waits for the results of an async request (`await`

in C#) counts as execution time. The GB-second calculation is based on the start and end time of the function and the memory usage over that period. What happens over that time in terms of CPU activity isn't factored into the calculation. You might be able to reduce costs during asynchronous operations by using[Durable Functions](durable/durable-functions-overview). You're not billed for time spent at awaits in orchestrator functions.

## Viewing and estimating costs from metrics

In [your invoice](../cost-management-billing/understand/download-azure-invoice), you can view the cost-related data along with the actual billed costs. However, this invoice data is a monthly aggregate for a past invoice period.

This section shows you how to use metrics, both app-level and function executions, to estimate costs for running your function apps.

### Function app-level metrics

The app-level metrics available to your app depend on the type of consumption plan you use.

These Azure Monitor metrics are related to Flex Consumption plan billing:

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

For more information, see [Azure Functions monitoring data reference](monitor-functions-reference).

To better understand the costs of your functions, use Azure Monitor to view cost-related metrics that your function apps generate. You can view Monitor metrics by using one of these tools:

Use [Azure Monitor metrics explorer](/en-us/azure/azure-monitor/essentials/metrics-getting-started) to view cost-related data for your Flex Consumption plan function apps in a graphical format.

In the

[Azure portal](https://portal.azure.com), go to your function app.In the left panel, scroll down to

**Monitoring**and select**Metrics**.From

**Metric**, select**On Demand Function Execution Count**and**Sum**for**Aggregation**. This selection adds the sum of the execution counts during the chosen period to the chart.Select

**Add metric**and add**On Demand Function Execution Units**,**Always Ready Function Execution Count**,**Always Ready Function Execution Units**, and**Always Ready Units**to the chart.

The resulting chart contains the totals for all the Flex Consumption execution metrics in the chosen time range, which in this example is a custom time range.

Because the number of On Demand Function Execution Units is greater than On Demand Function Execution Count, and there were no [always ready instances](flex-consumption-plan#always-ready-instances) on the app, the chart just shows On Demand Function Execution Units.

This chart shows a total of 3.54 billion `On Demand Function Execution Units`

consumed in a 16-minute period, measured in MB-milliseconds. To convert to GB-seconds, divide by 1,024,000. In this example, the function app consumed `3,540,000,000 / 1,024,000 = 3,457.03`

GB-seconds. You can take this value and multiply it by the current price of On Demand Execution Time on the [Functions pricing page](https://azure.microsoft.com/pricing/details/functions/), which gives you the cost of these 16 minutes, assuming you already used any free grants of execution time. You can use this same calculation with the The Always Ready Function Execution Units metric and the Always Ready Execution Time billing meter cost, as well as with the Always Ready Units metric and the Always Ready Baseline billing meter cost, to find out the GB-seconds costs for always ready instances.

To calculate the On Demand Total Executions cost, take the On Demand Function Execution Count sum for the same time period, convert to millions, and then multiply by the On Demand Total Executions price on the [Functions pricing page](https://azure.microsoft.com/pricing/details/functions/). For example, 2,100 executions in the example above converts to `0.0021`

million executions. You can use this same calculation with the Always Ready Function Execution Count metric and the Always Ready Total Executions billing meter to find out the cost for executions handled by always ready instance.

### Function-level metrics

Memory usage is important when estimating costs of your function executions. However, the way memory usage impacts your costs depends on the specific plan type:

In the Flex Consumption plan, you pay for the time the instance runs based on your chosen [instance size](flex-consumption-plan#instance-sizes), which has a set memory limit. For more information, see [Billing](flex-consumption-plan#billing).

If you haven't already done so, [enable Application Insights in your function app](configure-monitoring#enable-application-insights-integration). With this integration enabled, you can [query this telemetry data in the portal](analyze-telemetry-data#query-telemetry-data).

You can use either [Azure Monitor metrics explorer](/en-us/azure/azure-monitor/essentials/metrics-getting-started) in the [Azure portal](https://portal.azure.com) or REST APIs to get Monitor Metrics data.

#### Determine memory usage

Under **Monitoring**, select **Logs (Analytics)**, then copy the following telemetry query and paste it into the query window and select **Run**. This query returns the total memory usage at each sampled time.

```
performanceCounters
| where name == "Private Bytes"
| project timestamp, name, value
```


The results look like the following example:

| timestamp [UTC] | name | value |
|---|---|---|
| 9/12/2019, 1:05:14.947 AM | Private Bytes | 209,932,288 |
| 9/12/2019, 1:06:14.994 AM | Private Bytes | 212,189,184 |
| 9/12/2019, 1:06:30.010 AM | Private Bytes | 231,714,816 |
| 9/12/2019, 1:07:15.040 AM | Private Bytes | 210,591,744 |
| 9/12/2019, 1:12:16.285 AM | Private Bytes | 216,285,184 |
| 9/12/2019, 1:12:31.376 AM | Private Bytes | 235,806,720 |

#### Determine duration

Azure Monitor tracks metrics at the resource level, which for Functions is the function app. Application Insights integration emits metrics on a per-function basis. Here's an example analytics query to get the average duration of a function:

```
customMetrics
| where name contains "Duration"
| extend averageDuration = valueSum / valueCount
| summarize averageDurationMilliseconds=avg(averageDuration) by name
```


| name | averageDurationMilliseconds |
|---|---|
| QueueTrigger AvgDurationMs | 16.087 |
| QueueTrigger MaxDurationMs | 90.249 |
| QueueTrigger MinDurationMs | 8.522 |

## Other related costs

When estimating the overall cost of running your functions in any plan, remember that the Functions runtime uses several other Azure services, which are each billed separately. When you estimate pricing for function apps, any triggers and bindings you have that integrate with other Azure services require you to create and pay for those other services.

For functions running in a Consumption plan, the total cost is the execution cost of your functions, plus the cost of bandwidth and other services.

When estimating the overall costs of your function app and related services, use the [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?service=functions).

| Related cost | Description |
|---|---|
Storage account |
Each function app requires that you have an associated General Purpose
|

**Application Insights**[Application Insights](/en-us/azure/azure-monitor/app/app-insights-overview)to provide a high-performance monitoring experience for your function apps. While not required, you should[enable Application Insights integration](configure-monitoring#enable-application-insights-integration). A free grant of telemetry data is included every month. To learn more, see[the Azure Monitor pricing page](https://azure.microsoft.com/pricing/details/monitor/).**Network bandwidth**

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-storage-queue-triggered-function -->

# Create a function triggered by Azure Queue storage

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Learn how to create a function that is triggered when messages are submitted to an Azure Storage queue.

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

Next, you create a function in the new function app.

## Create a Queue triggered function

In your function app, select

**Overview**, and then select**+ Create**under**Functions**.Under

**Select a template**, scroll down and choose the**Azure Queue Storage trigger**template.In

**Template details**, configure the new trigger with the settings as specified in this table, then select**Create**:Setting Suggested value Description **Job type**Append to app You only see this setting for a Python v2 app. **Name**Unique in your function app Name of this queue triggered function. **Queue name**myqueue-items Name of the queue to connect to in your Storage account. **Storage account connection**AzureWebJobsStorage You can use the storage account connection already being used by your function app, or create a new one. Azure creates the Queue Storage triggered function based on the provided values. Next, you connect to your Azure storage account and create the

**myqueue-items**storage queue.

## Create the queue

Return to the

**Overview**page for your function app, select your**Resource group**, then find and select the storage account in your resource group.In the storage account page, select

**Data storage**>**Queues**>**+ Queue**.In the

**Name**field, type`myqueue-items`

, and then select**Create**.Select the new

**myqueue-items**queue, which you use to test the function by adding a message to the queue.

## Test the function

In a new browser window, return to your function app page and select

**Log stream**, which displays real-time logging for your app.In the

**myqueue-items**queue, select**Add message**, type "Hello World!" in**Message text**, and select**OK**.Go back to your function app logs and verify that the function ran to process the message from the queue.

Back in your storage queue, select

**Refresh**and verify that the message has been processed and is no longer in the queue.

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

You have created a function that runs when a message is added to a storage queue. For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue).

Now that you have a created your first function, let's add an output binding to the function that writes a message back to another queue.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/event-grid-how-tos -->

# How to work with Event Grid triggers and bindings in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions provides built-in integration with Azure Event Grid by using [triggers and bindings](functions-triggers-bindings). This article shows you how to configure and locally evaluate your Event Grid trigger and bindings. For more information about Event Grid trigger and output binding definitions and examples, see one of the following reference articles:

[Azure Event Grid bindings Overview](functions-bindings-event-grid)[Azure Event Grid trigger for Azure Functions](functions-bindings-event-grid-trigger)[Azure Event Grid output binding for Azure Functions](functions-bindings-event-grid-output)

## Create an event subscription

To start receiving Event Grid HTTP requests, you need a subscription to events raised by Event Grid. Event subscriptions specify the endpoint URL that invokes the function. When you create an event subscription from your function's **Integration** tab in the [Azure portal](https://portal.azure.com), the URL is supplied for you. When you programmatically create an event subscription or when you create the event subscription from Event Grid, you'll need to provide the endpoint. The endpoint URL contains a system key, which you must obtain from Functions administrator REST APIs.

## Get the webhook endpoint URL

The URL endpoint for your Event Grid triggered function depends on the version of the Functions runtime. The following example shows the version-specific URL pattern:

```
https://{functionappname}.azurewebsites.net/runtime/webhooks/eventgrid?functionName={functionname}&code={systemkey}
```


Note

There is a version of the Blob storage trigger that also uses event subscriptions. The endpoint URL for this kind of Blob storage trigger has a path of `/runtime/webhooks/blobs`

, whereas the path for an Event Grid trigger would be `/runtime/webhooks/EventGrid`

. For a comparison of options for processing blobs, see [Trigger on a blob container](storage-considerations#trigger-on-a-blob-container).

## Obtain the system key

The URL endpoint you construct includes a system key value. The system key is an authorization key, specific to the Event Grid webhook, that must be included in a request to the endpoint URL for an Event Grid trigger. The following section explains how to get the system key.

You can also get the master key for your function app from **Functions** > **App keys** in the portal.

Caution

The master key provides administrator access to your function app. Don't share this key with third parties or distribute it in native client applications.

For more information, see [Work with access keys in Azure Functions](function-keys-how-to).

You can get the system key from your function app by using the following administrator APIs (HTTP GET):

```
http://{functionappname}.azurewebsites.net/admin/host/systemkeys/eventgrid_extension?code={masterkey}
```


This REST API is an administrator API, so it requires your function app [master key](function-keys-how-to). Don't confuse the system key (for invoking an Event Grid trigger function) with the master key (for performing administrative tasks on the function app). When you subscribe to an Event Grid topic, be sure to use the system key.

Here's an example of the response that provides the system key:

```
{
"name": "eventgridextensionconfig_extension",
"value": "{the system key for the function}",
"links": [
{
"rel": "self",
"href": "{the URL for the function, without the system key}"
}
]
}
```


## Create the subscription

You can create an event subscription either from the [Azure portal](https://portal.azure.com) or by using the Azure CLI.

For functions that you develop in the Azure portal with the Event Grid trigger, select **Integration** then choose the **Event Grid Trigger** and select **Create Event Grid subscription**.


When you select this link, the portal opens the **Create Event Subscription** page with the current trigger endpoint already defined.


For more information about how to create subscriptions by using the Azure portal, see [Create custom event - Azure portal](../event-grid/custom-event-quickstart-portal) in the Event Grid documentation.

For more information about how to create a subscription, see [the blob storage quickstart](../storage/blobs/storage-blob-event-quickstart#subscribe-to-your-storage-account) or the other Event Grid quickstarts.

## Local testing with viewer web app

To test an Event Grid trigger locally, you have to get Event Grid HTTP requests delivered from their origin in the cloud to your local machine. One way to do that is by capturing requests online and manually resending them on your local machine:

[Create a viewer web app](#create-a-viewer-web-app)that captures event messages.[Create an Event Grid subscription](#create-an-event-grid-subscription)that sends events to the viewer app.[Generate a request](#generate-a-request)and copy the request body from the viewer app.[Manually post the request](#manually-post-the-request)to the localhost URL of your Event Grid trigger function.

To send an HTTP post request, you need an HTTP test tool. Make sure to choose a tool that keeps your data secure. For more information, see [HTTP test tools](functions-develop-local#http-test-tools).

When you're done testing, you can use the same subscription for production by updating the endpoint. Use the [ az eventgrid event-subscription update](/en-us/cli/azure/eventgrid/event-subscription#az-eventgrid-event-subscription-update) Azure CLI command.

## Create a viewer web app

To simplify capturing event messages, you can deploy a [pre-built web app](https://github.com/Azure-Samples/azure-event-grid-viewer) that displays the event messages. The deployed solution includes an App Service plan, an App Service web app, and source code from GitHub.

Select **Deploy to Azure** to deploy the solution to your subscription. In the Azure portal, provide values for the parameters.

The deployment may take a few minutes to complete. After the deployment has succeeded, view your web app to make sure it's running. In a web browser, navigate to:
`https://<your-site-name>.azurewebsites.net`


You see the site but no events have been posted to it yet.

## Create an Event Grid subscription

Create an Event Grid subscription of the type you want to test, and give it the URL from your web app as the endpoint for event notification. The endpoint for your web app must include the suffix `/api/updates/`

. So, the full URL is `https://<your-site-name>.azurewebsites.net/api/updates`


For information about how to create subscriptions by using the Azure portal, see [Create custom event - Azure portal](../event-grid/custom-event-quickstart-portal) in the Event Grid documentation.

## Generate a request

Trigger an event that will generate HTTP traffic to your web app endpoint. For example, if you created a blob storage subscription, upload or delete a blob. When a request shows up in your web app, copy the request body.

The subscription validation request will be received first; ignore any validation requests, and copy the event request.

## Manually post the request

Run your Event Grid function locally. The `Content-Type`

and `aeg-event-type`

headers are required to be manually set, while and all other values can be left as default.

Use your HTTP test tool to create an HTTP POST request:

Set a

`Content-Type: application/json`

header.Set an

`aeg-event-type: Notification`

header.Paste the RequestBin data into the request body.

Send an HTTP POST request to the endpoint that manually starts the Event Grid trigger.


The `functionName`

parameter must be the name specified in the `FunctionName`

attribute.

The Event Grid trigger function executes and shows logs similar to the following example:

## Next steps

To learn more about Event Grid with Functions, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/configure-monitoring -->

# How to configure monitoring for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions integrates with Application Insights to better enable you to monitor your function apps. Application Insights, a feature of Azure Monitor, is an extensible Application Performance Management (APM) service that collects data generated by your function app, including information your app writes to logs. Application Insights integration is typically enabled when your function app is created. If your app doesn't have the instrumentation key set, you must first [enable Application Insights integration](#enable-application-insights-integration).

You can use Application Insights without any custom configuration. However, the default configuration can result in high volumes of data. If you're using a Visual Studio Azure subscription, you might hit your data cap for Application Insights. For information about Application Insights costs, see [Application Insights billing](/en-us/azure/azure-monitor/logs/cost-logs#application-insights-billing). For more information, see [Solutions with high-volume of telemetry](#solutions-with-high-volume-of-telemetry).

In this article, you learn how to configure and customize the data that your functions send to Application Insights. You can set common logging configurations in the * host.json* file. By default, these settings also govern custom logs emitted by your code. However, in some cases this behavior can be disabled in favor of options that give you more control over logging. For more information, see

[Custom application logs](#custom-application-logs).

Note

You can use specially configured application settings to represent specific settings in a *host.json* file for a particular environment. Doing so lets you effectively change *host.json* settings without needing to republish the *host.json* file in your project. For more information, see [Override host.json values](functions-host-json#override-hostjson-values).

## Custom application logs

By default, custom application logs you write are sent to the Functions host, which then sends them to Application Insights under the [Worker category](#configure-categories). Some language stacks allow you to instead send the logs directly to Application Insights, which gives you full control over how logs you write are emitted. In this case, the logging pipeline changes from `worker -> Functions host -> Application Insights`

to `worker -> Application Insights`

.

The following table summarizes the configuration options available for each stack:

| Language stack | Where to configure custom logs |
|---|---|
| .NET (in-process model) | `host.json` |
| .NET (isolated model) | Default (send custom logs to the Functions host): `host.json` To send logs directly to Application Insights, see:
|
| Node.js | `host.json` |
| Python | `host.json` |
| Java | Default (send custom logs to the Functions host): `host.json` To send logs directly to Application Insights, see:
|
| PowerShell | `host.json` |

When you configure custom application logs to be sent directly, the host no longer emits them, and `host.json`

no longer controls their behavior. Similarly, the options exposed by each stack apply only to custom logs, and they don't change the behavior of the other runtime logs described in this article. In this case, to control the behavior of all logs, you might need to make changes in both configurations.

## Configure categories

The Azure Functions logger includes a *category* for every log. The category indicates which part of the runtime code or your function code wrote the log. Categories differ between version 1.x and later versions.

Category names are assigned differently in Functions compared to other .NET frameworks. For example, when you use `ILogger<T>`

in ASP.NET, the category is the name of the generic type. C# functions also use `ILogger<T>`

, but instead of setting the generic type name as a category, the runtime assigns categories based on the source. For example:

- Entries related to running a function are assigned a category of
`Function.<FUNCTION_NAME>`

. - Entries created by user code inside the function, such as when calling
`logger.LogInformation()`

, are assigned a category of`Function.<FUNCTION_NAME>.User`

.

The following table describes the main categories of logs that the runtime creates:

| Category | Table | Description |
|---|---|---|
`Function` |
traces |
Includes function started and completed logs for all function runs. For successful runs, these logs are at the `Information` level. Exceptions are logged at the `Error` level. The runtime also creates `Warning` level logs, such as when queue messages are sent to the
|
`Function.<YOUR_FUNCTION_NAME>` |
dependencies |
Dependency data is automatically collected for some services. For successful runs, these logs are at the `Information` level. For more information, see
`Error` level. The runtime also creates `Warning` level logs, such as when queue messages are sent to the
|
`Function.<YOUR_FUNCTION_NAME>` |
customMetricscustomEvents |
C# and JavaScript SDKs lets you collect custom metrics and log custom events. For more information, see
|

`Function.<YOUR_FUNCTION_NAME>`

**traces**`Information`

level. Exceptions are logged at the `Error`

level. The runtime also creates `Warning`

level logs, such as when queue messages are sent to the [poison queue](functions-bindings-storage-queue-trigger#poison-messages).`Function.<YOUR_FUNCTION_NAME>.User`

**traces**[Writing to logs](functions-monitoring#writing-to-logs).`Host.Aggregator`

**customMetrics**[configurable](#configure-the-aggregator)period of time. The default period is 30 seconds or 1,000 results, whichever comes first. Examples are the number of runs, success rate, and duration. All of these logs are written at the`Information`

level. If you filter at `Warning`

or higher, you don't see any of this data.`Host.Results`

**requests**`Information`

level. If you filter at `Warning`

or higher, you don't see any of this data.`Microsoft`

**traces**`Worker`

**traces**`Microsoft.*`

category, such as `Microsoft.Azure.WebJobs.Script.Workers.Rpc.RpcFunctionInvocationDispatcher`

. These logs are written at the `Information`

level.Note

For .NET class library functions, these categories assume you're using `ILogger`

and not `ILogger<T>`

. For more information, see the [Functions ILogger documentation](functions-dotnet-class-library#ilogger).

The **Table** column indicates to which table in Application Insights the log is written.

## Configure log levels

A *log level* is assigned to every log. The value is an integer that indicates relative importance:

| LogLevel | Code | Description |
|---|---|---|
| Trace | 0 | Logs that contain the most detailed messages. These messages might contain sensitive application data. These messages are disabled by default and should never be enabled in a production environment. |
| Debug | 1 | Logs that are used for interactive investigation during development. These logs should primarily contain information useful for debugging and have no long-term value. |
| Information | 2 | Logs that track the general flow of the application. These logs should have long-term value. |
| Warning | 3 | Logs that highlight an abnormal or unexpected event in the application flow, but don't otherwise cause the application execution to stop. |
| Error | 4 | Logs that highlight when the current flow of execution is stopped because of a failure. These errors should indicate a failure in the current activity, not an application-wide failure. |
| Critical | 5 | Logs that describe an unrecoverable application or system crash, or a catastrophic failure that requires immediate attention. |
| None | 6 | Disables logging for the specified category. |

The [ host.json file](functions-host-json) configuration determines how much logging a functions app sends to Application Insights.

For each category, you indicate the minimum log level to send. The *host.json* settings vary depending on the [Functions runtime version](functions-versions).

The following examples define logging based on the following rules:

- The default logging level is set to
`Warning`

to prevent[excessive logging](#solutions-with-high-volume-of-telemetry)for unanticipated categories. `Host.Aggregator`

and`Host.Results`

are set to lower levels. Setting logging levels too high (especially higher than`Information`

) can result in loss of metrics and performance data.- Logging for function runs is set to
`Information`

. If necessary, you can[override](functions-host-json#override-hostjson-values)this setting in local development to`Debug`

or`Trace`

.

```
{
"logging": {
"fileLoggingMode": "debugOnly",
"logLevel": {
"default": "Warning",
"Host.Aggregator": "Trace",
"Host.Results": "Information",
"Function": "Information"
}
}
}
```


If * host.json* includes multiple logs that start with the same string, the more defined logs ones are matched first. Consider the following example that logs everything in the runtime, except

`Host.Aggregator`

, at the `Error`

level:```
{
"logging": {
"fileLoggingMode": "debugOnly",
"logLevel": {
"default": "Information",
"Host": "Error",
"Function": "Error",
"Host.Aggregator": "Information"
}
}
}
```


You can use a log level setting of `None`

to prevent any logs from being written for a category.

Caution

Azure Functions integrates with Application Insights by storing telemetry events in Application Insights tables. If you set a category log level to any value different from `Information`

, it prevents the telemetry from flowing to those tables, and you won't be able to see related data in the **Application Insights** and **Function Monitor** tabs.

For example, for the previous samples:

- If you set the
`Host.Results`

category to the`Error`

log level, Azure gathers only host execution telemetry events in the`requests`

table for failed function executions, preventing the display of host execution details of successful executions in both the**Application Insights**and**Function Monitor**tabs. - If you set the
`Function`

category to the`Error`

log level, it stops gathering function telemetry data related to`dependencies`

,`customMetrics`

, and`customEvents`

for all the functions, preventing you from viewing any of this data in Application Insights. Azure gathers only`traces`

logged at the`Error`

level.

In both cases, Azure continues to collect errors and exceptions data in the **Application Insights** and **Function Monitor** tabs. For more information, see [Solutions with high-volume of telemetry](#solutions-with-high-volume-of-telemetry).

## Configure the aggregator

As noted in the previous section, the runtime aggregates data about function executions over a period of time. The default period is 30 seconds or 1,000 runs, whichever comes first. You can configure this setting in the * host.json* file. For example:

```
{
"aggregator": {
"batchSize": 1000,
"flushTimeout": "00:00:30"
}
}
```


## Configure sampling

Application Insights has a [sampling](/en-us/azure/azure-monitor/app/sampling) feature that can protect you from producing too much telemetry data on completed executions at times of peak load. When the rate of incoming executions exceeds a specified threshold, Application Insights starts to randomly ignore some of the incoming executions. The default setting for maximum number of executions per second is 20 (five in version 1.x). You can configure sampling in [ host.json](functions-host-json#applicationinsights). Here's an example:

```
{
"logging": {
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"maxTelemetryItemsPerSecond" : 20,
"excludedTypes": "Request;Exception"
}
}
}
}
```


You can exclude certain types of telemetry from sampling. In this example, data of type `Request`

and `Exception`

is excluded from sampling. It ensures that *all* function executions (requests) and exceptions are logged while other types of telemetry remain subject to sampling.

If your project uses a dependency on the Application Insights SDK to do manual telemetry tracking, you might experience unusual behavior if your sampling configuration differs from the sampling configuration in your function app. In such cases, use the same sampling configuration as the function app. For more information, see [Sampling in Application Insights](/en-us/azure/azure-monitor/app/sampling).

## Enable SQL query collection

Application Insights automatically collects data on dependencies for HTTP requests, database calls, and for several bindings. For more information, see [Dependencies](functions-monitoring#dependencies). For SQL calls, the name of the server and database is always collected and stored, but SQL query text isn't collected by default. You can use `dependencyTrackingOptions.enableSqlCommandTextInstrumentation`

to enable SQL query text logging by using the following settings (at a minimum) in your [host.json file](functions-host-json#applicationinsightsdependencytrackingoptions):

```
"logging": {
"applicationInsights": {
"enableDependencyTracking": true,
"dependencyTrackingOptions": {
"enableSqlCommandTextInstrumentation": true
}
}
}
```


For more information, see [Advanced SQL tracking to get full SQL query](/en-us/azure/azure-monitor/app/asp-net-dependencies#advanced-sql-tracking-to-get-full-sql-query).

## Configure scale controller logs

*This feature is in preview.*

You can have the [Azure Functions scale controller](event-driven-scaling#runtime-scaling) emit logs to either Application Insights or to Blob storage to better understand the decisions the scale controller is making for your function app.

To enable this feature, add an application setting named `SCALE_CONTROLLER_LOGGING_ENABLED`

to your function app settings. The following value of the setting must be in the format `<DESTINATION>:<VERBOSITY>`

. For more information, see the following table:

| Property | Description |
|---|---|
`<DESTINATION>` |
The destination to which logs are sent. Valid values are `AppInsights` and `Blob` .When you use `AppInsights` , ensure that the
When you set the destination to `Blob` , logs are created in a blob container named `azure-functions-scale-controller` in the default storage account set in the `AzureWebJobsStorage` application setting. |
`<VERBOSITY>` |
Specifies the level of logging. Supported values are `None` , `Warning` , and `Verbose` .When set to `Verbose` , the scale controller logs a reason for every change in the worker count, and information about the triggers that factor into those decisions. Verbose logs include trigger warnings and the hashes used by the triggers before and after the scale controller runs. |

Tip

Keep in mind that while you leave scale controller logging enabled, it impacts the [potential costs of monitoring your function app](functions-monitoring#application-insights-pricing-and-limits). Consider enabling logging until you collect enough data to understand how the scale controller is behaving, and then disabling it.

For example, the following Azure CLI command turns on verbose logging from the scale controller to Application Insights:

```
az functionapp config appsettings set --name <FUNCTION_APP_NAME> \
--resource-group <RESOURCE_GROUP_NAME> \
--settings SCALE_CONTROLLER_LOGGING_ENABLED=AppInsights:Verbose
```


In this example, replace `<FUNCTION_APP_NAME>`

and `<RESOURCE_GROUP_NAME>`

with the name of your function app and the resource group name, respectively.

The following Azure CLI command disables logging by setting the verbosity to `None`

:

```
az functionapp config appsettings set --name <FUNCTION_APP_NAME> \
--resource-group <RESOURCE_GROUP_NAME> \
--settings SCALE_CONTROLLER_LOGGING_ENABLED=AppInsights:None
```


You can also disable logging by removing the `SCALE_CONTROLLER_LOGGING_ENABLED`

setting using the following Azure CLI command:

```
az functionapp config appsettings delete --name <FUNCTION_APP_NAME> \
--resource-group <RESOURCE_GROUP_NAME> \
--setting-names SCALE_CONTROLLER_LOGGING_ENABLED
```


With scale controller logging enabled, you're now able to [query your scale controller logs](analyze-telemetry-data#query-scale-controller-logs).

## Enable Application Insights integration

For a function app to send data to Application Insights, it needs to connect to the Application Insights resource using **only one** of these application settings:

| Setting name | Description |
|---|---|
`APPLICATIONINSIGHTS_CONNECTION_STRING` |
This setting is recommended and is required when your Application Insights instance runs in a sovereign cloud. The connection string supports other
|

`APPINSIGHTS_INSTRUMENTATIONKEY`

When you create your function app in the [Azure portal](functions-get-started) from the command line by using [Azure Functions Core Tools](how-to-create-function-azure-cli?pivots=programming-language-csharp) or [Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-csharp), Application Insights integration is enabled by default. The Application Insights resource has the same name as your function app, and is created either in the same region or in the nearest region.

### Require Microsoft Entra authentication

You can use the [ APPLICATIONINSIGHTS_AUTHENTICATION_STRING](functions-app-settings#applicationinsights_authentication_string) setting to enable connections to Application Insights using Microsoft Entra authentication. This creates a consistent authentication experience across all Application Insights pipelines, including Profiler and Snapshot Debugger, as well as from the Functions host and language-specific agents.

Note

There's currently no Microsoft Entra ID authentication support for local development.

When Ingesting data in a sovereign cloud, Microsoft Entra ID authentication isn't available when using the Application Insights SDK. OpenTelemetry-based data collection supports Microsoft Entra ID authentication across all cloud environments, including sovereign clouds.

The value contains either `Authorization=AAD`

for a system-assigned managed identity or `ClientId=<YOUR_CLIENT_ID>;Authorization=AAD`

for a user-assigned managed identity. The managed identity must already be available to the function app, with an assigned role equivalent to [Monitoring Metrics Publisher](/en-us/azure/role-based-access-control/built-in-roles/monitor#monitoring-metrics-publisher). For more information, see [Microsoft Entra authentication for Application Insights](/en-us/azure/azure-monitor/app/azure-ad-authentication).

The [ APPLICATIONINSIGHTS_CONNECTION_STRING](functions-app-settings#applicationinsights_connection_string) setting is still required.

Note

When using `APPLICATIONINSIGHTS_AUTHENTICATION_STRING`

to connect to Application Insights using Microsoft Entra authentication, you should also [Disable local authentication for Application Insights](/en-us/azure/azure-monitor/app/azure-ad-authentication#disable-local-authentication). This configuration requires Microsoft Entra authentication in order for telemetry to be ingested into your workspace.

### New function app in the portal

To review the Application Insights resource being created, select it to expand the **Application Insights** window. You can change the **New resource name** or select a different **Location** in an [Azure geography](https://azure.microsoft.com/global-infrastructure/geographies/) where you want to store your data.


When you select **Create**, an Application Insights resource is created with your function app, which has the `APPLICATIONINSIGHTS_CONNECTION_STRING`

set in application settings. Everything is ready to go.

### Add to an existing function app

If an Application Insights resource wasn't created with your function app, use the following steps to create the resource. You can then add the connection string from that resource as an [application setting](functions-how-to-use-azure-function-app-settings#settings) in your function app.

In the

[Azure portal](https://portal.azure.com), search for and select**function app**, and then select your function app.Select the

**Application Insights is not configured**banner at the top of the window. If you don't see this banner, then your app might already have Application Insights enabled.Expand

**Change your resource**and create an Application Insights resource by using the settings specified in the following table:Setting Suggested value Description **New resource name**Unique app name It's easiest to use the same name as your function app, which must be unique in your subscription. **Location**West Europe If possible, use the same [region](https://azure.microsoft.com/regions/)as your function app, or the one that's close to that region.Select

**Apply**.The Application Insights resource is created in the same resource group and subscription as your function app. After the resource is created, close the

**Application Insights**window.In your function app, expand

**Settings**, and then select**Environment variables**. In the**App settings**tab, if you see an app setting named`APPLICATIONINSIGHTS_CONNECTION_STRING`

, Application Insights integration is enabled for your function app running in Azure. If this setting doesn't exist, add it by using your Application Insights connection string as the value.

Note

Older function apps might use `APPINSIGHTS_INSTRUMENTATIONKEY`

instead of `APPLICATIONINSIGHTS_CONNECTION_STRING`

. When possible, update your app to use the connection string instead of the instrumentation key.

## Disable built-in logging

Early versions of Functions used built-in monitoring, which is no longer recommended. When you enable Application Insights, disable the built-in logging that uses Azure Storage. The built-in logging is useful for testing with light workloads, but isn't intended for high-load production use. For production monitoring, we recommend Application Insights. If you use built-in logging in production, the logging record might be incomplete because of throttling on Azure Storage.

To disable built-in logging, delete the `AzureWebJobsDashboard`

app setting. For more information about how to delete app settings in the Azure portal, see the **Application settings** section of [How to manage a function app](functions-how-to-use-azure-function-app-settings#settings). Before you delete the app setting, ensure that no existing functions in the same function app use the setting for Azure Storage triggers or bindings.

## Solutions with high volume of telemetry

Function apps are an essential part of solutions that can cause high volumes of telemetry, such as IoT solutions, rapid event driven solutions, high load financial systems, and integration systems. In this case, you should consider extra configuration to reduce costs while maintaining observability.

The generated telemetry can be consumed in real-time dashboards, alerting, detailed diagnostics, and so on. Depending on how the generated telemetry is consumed, you need to define a strategy to reduce the volume of data generated. This strategy allows you to properly monitor, operate, and diagnose your function apps in production. Consider the following options:

**Use the correct table plan**:[Table plans](/en-us/azure/azure-monitor/logs/data-platform-logs#table-plans)help you manage data costs by controlling how often you use the data in a table and the kind of analysis you need to perform. To reduce costs, you can choose the`Basic`

plan, which does lack some features available in the`Analytics`

plan.**Use sampling**: As mentioned[previously](#configure-sampling), sampling helps to dramatically reduce the volume of telemetry events ingested while maintaining a statistically correct analysis. It could happen that even using sampling you still get a high volume of telemetry. Inspect the options that[adaptive sampling](/en-us/azure/azure-monitor/app/sampling#configuring-adaptive-sampling-for-aspnet-applications)provides to you. For example, set the`maxTelemetryItemsPerSecond`

to a value that balances the volume generated with your monitoring needs. Keep in mind that the telemetry sampling is applied per host executing your function app.**Default log level**: Use`Warning`

or`Error`

as the default value for all telemetry categories. Later, you can decide which[categories](#configure-categories)you want to set at the`Information`

level, so that you can monitor and diagnose your functions properly.**Tune your functions telemetry**: With the default log level set to`Error`

or`Warning`

, no detailed information from each function is gathered (dependencies, custom metrics, custom events, and traces). For those functions that are key for production monitoring, define an explicit entry for the`Function.<YOUR_FUNCTION_NAME>`

category and set it to`Information`

, so that you can gather detailed information. To avoid gathering[user-generated logs](functions-monitoring#writing-to-logs)at the`Information`

level, set the`Function.<YOUR_FUNCTION_NAME>.User`

category to the`Error`

or`Warning`

log level.**Host.Aggregator category**: As described in[configure categories](#configure-categories), this category provides aggregated information of function invocations. The information from this category is gathered in the Application Insights`customMetrics`

table, and is shown in the function**Overview**tab in the Azure portal. Depending on how you configure the aggregator, consider that there can be a delay, determined by the`flushTimeout`

setting, in the telemetry gathered. If you set this category to a value different from`Information`

, you stop gathering the data in the`customMetrics`

table and don't display metrics in the function**Overview**tab.The following screenshot shows

`Host.Aggregator`

telemetry data displayed in the function**Overview**tab:The following screenshot shows

`Host.Aggregator`

telemetry data in Application Insights`customMetrics`

table:**Host.Results category**: As described in[configure categories](#configure-categories), this category provides the runtime-generated logs indicating the success or failure of a function invocation. The information from this category is gathered in the Application Insights`requests`

table, and is shown in the function**Monitor**tab and in different Application Insights dashboards (Performance, Failures, and so on). If you set this category to a value different than`Information`

, you gather only telemetry generated at the log level defined (or higher). For example, setting it to`error`

results in tracking requests data only for failed executions.The following screenshot shows the

`Host.Results`

telemetry data displayed in the function**Monitor**tab:The following screenshot shows

`Host.Results`

telemetry data displayed in Application Insights Performance dashboard:**Host.Aggregator vs Host.Results**: Both categories provide good insights about function executions. If needed, you can remove the detailed information from one of these categories, so that you can use the other for monitoring and alerting. Here's a sample:

```
{
"version": "2.0",
"logging": {
"logLevel": {
"default": "Warning",
"Function": "Error",
"Host.Aggregator": "Error",
"Host.Results": "Information",
"Function.Function1": "Information",
"Function.Function1.User": "Error"
},
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"maxTelemetryItemsPerSecond": 1,
"excludedTypes": "Exception"
}
}
}
}
```


With this configuration:

The default value for all functions and telemetry categories is set to

`Warning`

(including Microsoft and Worker categories). So, by default, all errors and warnings generated by runtime and custom logging are gathered.The

`Function`

category log level is set to`Error`

, so for all functions, by default, only exceptions and error logs are gathered. Dependencies, user-generated metrics, and user-generated events are skipped.For the

`Host.Aggregator`

category, as it's set to the`Error`

log level, aggregated information from function invocations isn't gathered in the`customMetrics`

Application Insights table, and information about executions counts (total, successful, and failed) aren't shown in the function overview dashboard.For the

`Host.Results`

category, all the host execution information is gathered in the`requests`

Application Insights table. All the invocations results are shown in the function Monitor dashboard and in Application Insights dashboards.For the function called

`Function1`

, we set the log level to`Information`

. So, for this concrete function, all the telemetry is gathered (dependency, custom metrics, and custom events). For the same function, we set the`Function1.User`

category (user-generated traces) to`Error`

, so only custom error logging is gathered.Note

Configuration per function isn't supported in v1.x of the Functions runtime.

Sampling is configured to send one telemetry item per second per type, excluding the exceptions. This sampling happens for each server host running our function app. So, if we have four instances, this configuration emits four telemetry items per second per type and all the exceptions that might occur.

Note

Metric counts such as request rate and exception rate are adjusted to compensate for the sampling rate, so that they show approximately correct values in Metric Explorer.


Tip

Experiment with different configurations to ensure that you cover your requirements for logging, monitoring, and alerting. Also, ensure that you have detailed diagnostics in case of unexpected errors or malfunctioning.

## Overriding monitoring configuration at runtime

Finally, there could be situations where you need to quickly change the logging behavior of a certain category in production, and you don't want to make a whole deployment just for a change in the *host.json* file. For such cases, you can override the [host.json values](functions-host-json#override-hostjson-values).

To configure these values at App settings level (and avoid redeployment on just *host.json* changes), you should override specific `host.json`

values by creating an equivalent value as an application setting. When the runtime finds an application setting in the format `AzureFunctionsJobHost__path__to__setting`

, it overrides the equivalent `host.json`

setting located at `path.to.setting`

in the JSON. When expressed as an application setting, a double underscore (`__`

) replaces the dot (`.`

) used to indicate JSON hierarchy. For example, you can use the following app settings to configure individual function log levels in `host.json`

.

| Host.json path | App setting |
|---|---|
| logging.logLevel.default | AzureFunctionsJobHost__logging__logLevel__default |
| logging.logLevel.Host.Aggregator | AzureFunctionsJobHost__logging__logLevel__Host.Aggregator |
| logging.logLevel.Function | AzureFunctionsJobHost__logging__logLevel__Function |
| logging.logLevel.Function.Function1 | AzureFunctionsJobHost__logging__logLevel__Function.Function1 |
| logging.logLevel.Function.Function1.User | AzureFunctionsJobHost__logging__logLevel__Function.Function1.User |

You can override the settings directly at the Azure portal Function App Configuration pane or by using an Azure CLI or PowerShell script.

```
az functionapp config appsettings set --name MyFunctionApp --resource-group MyResourceGroup --settings "AzureFunctionsJobHost__logging__logLevel__Host.Aggregator=Information"
```


Note

Overriding the `host.json`

through changing app settings will restart your function app.
App settings that contain a period aren't supported when running on Linux in an Elastic Premium plan or a Dedicated (App Service) plan. In these hosting environments, you should continue to use the *host.json* file.

## Monitor function apps using Health check

You can use the Health Check feature to monitor function apps on the Premium (Elastic Premium) and Dedicated (App Service) plans. Health check isn't an option for the Flex Consumption and Consumption plans. To learn how to configure it, see [Monitor App Service instances using Health check](../app-service/monitor-instances-health-check). Your function app should have an HTTP trigger function that responds with an HTTP status code of 200 on the same endpoint as configured on the `Path`

parameter of the health check. You can also have that function perform extra checks to ensure that dependent services are reachable and working.

## Related content

For more information about monitoring, see:
