---
merged_at: 2026-01-29T15:49:53.278576
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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

`Azurite: Start Blob Service`

, and press enter. This action starts the Azurite Blob Storage service emulator.Select the Azure icon in the Activity bar, expand

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

.**Select a hosting plan**Choose **Flex Consumption**, which is the recommended[hosting plan](functions-scale)for serverless hosting.**Select a location for new resources**Select a location in a [region](https://azure.microsoft.com/regions/)near you or near other services that your functions access.**Select a runtime stack**Select the language version you currently run locally. **Select an instance size**Select **512**. You can always[change the instance size](flex-consumption-how-to#configure-instance-memory)setting to a larger size later.**Enter the maximum instance count**Select the default value of **100**, which limits the total scale-out of your app. You can also choose a different value between 40 and 1,000.**Select a resource group**Select **Create new resource group**and accept the default or enter another name for the new group that's unique in your subscription.**Select resource authentication type**Select **Managed identity**so that your app connects to remote resources by using Microsoft Entra ID authentication instead of using shared secrets (connection strings and keys), which are less secure.**Select a user assigned identity**Select **Create new user-assigned identity**.**Select a location for new resources**Select the same region as the storage account you created. If for some reason this region isn't supported by the Flex Consumption play, it isn't displayed. In that case, choose a nearby [region](https://azure.microsoft.com/regions/)instead. For more information, see[View currently supported regions](flex-consumption-how-to#view-currently-supported-regions).**Select a storage account**Choose the name of the storage account you created. **Select an Application Insights resource for your app**Choose **Create new Application Insights resource**and at the prompt provide the name for the instance used to store runtime data from your functions.A notification appears after your function app is created. Select

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
<!-- Source: N/A -->

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
