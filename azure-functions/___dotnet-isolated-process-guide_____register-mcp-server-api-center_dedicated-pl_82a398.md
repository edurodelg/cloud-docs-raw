---
merged_at: 2026-01-31T00:09:26.094237
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-mcp-trigger -->

# MCP tool trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the MCP tool trigger to define tool endpoints in a [Model Content Protocol (MCP)](https://github.com/modelcontextprotocol) server. Client language models and agents can use tools to perform specific tasks, such as storing or accessing code snippets.

For information on setup and configuration details, see the [overview](functions-bindings-mcp).

## Example

Note

For C#, the Azure Functions MCP extension supports only the [isolated worker model](dotnet-isolated-process-guide).

This code creates an endpoint to expose a tool named `SaveSnippet`

that tries to persist a named code snippet to blob storage.

```
private const string BlobPath = "snippets/{mcptoolargs.snippetname}.json";
[Function(nameof(SaveSnippet))]
[BlobOutput(BlobPath)]
public string SaveSnippet(
[McpToolTrigger("save_snippet", "Saves a code snippet into your snippet collection.")]
ToolInvocationContext context,
[McpToolProperty("snippetname", "The name of the snippet.", isRequired: true)]
string name,
[McpToolProperty("snippet", "The code snippet.", isRequired: true)]
string snippet
)
{
return snippet;
}
```


This code creates an endpoint to expose a tool named `GetSnippet`

that tries to retrieve a code snippet by name from blob storage.

```
private const string BlobPath = "snippets/{mcptoolargs.snippetname}.json";
[Function(nameof(GetSnippet))]
public object GetSnippet(
[McpToolTrigger("get_snippets", "Gets code snippets from your snippet collection.")]
ToolInvocationContext context,
[BlobInput(BlobPath)] string snippetContent
)
{
return snippetContent;
}
```


The tool properties for the `GetSnippet`

function are configured in `Program.cs`

:

```
var builder = FunctionsApplication.CreateBuilder(args);
builder.ConfigureFunctionsWebApplication();
builder.Services
.AddApplicationInsightsTelemetryWorkerService()
.ConfigureFunctionsApplicationInsights();
builder
.ConfigureMcpTool("get_snippets")
.WithProperty("snippetname", "string", "The name of the snippet.", required: true);
builder.Build().Run();
```


Tip

The example above used literal strings for things like the name of the "get_snippets" tool in both `Program.cs`

and the function. Consider instead using shared constant strings to keep things in sync across your project.

For the complete code example, see [SnippetTool.cs](https://github.com/Azure-Samples/remote-mcp-functions-dotnet/blob/main/src/SnippetsTool.cs).

This code creates an endpoint to expose a tool named `SaveSnippets`

that tries to persist a named code snippet to blob storage.

```
@FunctionName("SaveSnippets")
@StorageAccount("AzureWebJobsStorage")
public String saveSnippet(
@McpToolTrigger(
name = "saveSnippets",
description = "Saves a text snippet to your snippets collection."
)
String mcpToolInvocationContext,
@McpToolProperty(
name = "snippetName",
propertyType = "string",
description = "The name of the snippet.",
required = true
)
String snippetName,
@McpToolProperty(
name = "snippet",
propertyType = "string",
description = "The content of the snippet.",
required = true
)
String snippet,
@BlobOutput(name = "outputBlob", path = "snippets/{mcptoolargs.snippetName}.json")
OutputBinding<String> outputBlob,
final ExecutionContext context
) {
// Log the entire incoming JSON for debugging
context.getLogger().info(mcpToolInvocationContext);
// Log the snippet name and content
context.getLogger().info("Saving snippet with name: " + snippetName);
context.getLogger().info("Snippet content:\n" + snippet);
// Write the snippet content to the output blob
outputBlob.setValue(snippet);
return "Successfully saved snippet '" + snippetName + "' with " + snippet.length() + " characters.";
}
```


This code creates an endpoint to expose a tool named `GetSnippets`

that tries to retrieve a code snippet by name from blob storage.

```
@FunctionName("GetSnippets")
@StorageAccount("AzureWebJobsStorage")
public String getSnippet(
@McpToolTrigger(
name = "getSnippets",
description = "Gets a text snippet from your snippets collection."
)
String mcpToolInvocationContext,
@McpToolProperty(
name = "snippetName",
propertyType = "string",
description = "The name of the snippet.",
required = true
)
String snippetName,
@BlobInput(name = "inputBlob", path = "snippets/{mcptoolargs.snippetName}.json")
String inputBlob,
final ExecutionContext context
) {
// Log the entire incoming JSON for debugging
context.getLogger().info(mcpToolInvocationContext);
// Log the snippet name and the fetched snippet content from the blob
context.getLogger().info("Retrieving snippet with name: " + snippetName);
context.getLogger().info("Snippet content:");
context.getLogger().info(inputBlob);
// Return the snippet content or a not found message
if (inputBlob != null && !inputBlob.trim().isEmpty()) {
return inputBlob;
} else {
return "Snippet '" + snippetName + "' not found.";
}
}
```


For the complete code example, see [Snippets.java](https://github.com/Azure-Samples/remote-mcp-functions-java/blob/main/src/main/java/com/function/Snippets.java).

Example code for JavaScript isn't currently available. See the TypeScript examples for general guidance using Node.js.

This code creates an endpoint to expose a tool named `savesnippet`

that tries to persist a named code snippet to blob storage.

```
import { app, InvocationContext, input, output, arg } from "@azure/functions";
app.mcpTool("saveSnippet", {
toolName: SAVE_SNIPPET_TOOL_NAME,
description: SAVE_SNIPPET_TOOL_DESCRIPTION,
toolProperties: {
[SNIPPET_NAME_PROPERTY_NAME]: arg.string().describe(SNIPPET_NAME_PROPERTY_DESCRIPTION),
[SNIPPET_PROPERTY_NAME]: arg.string().describe(SNIPPET_PROPERTY_DESCRIPTION)
},
extraOutputs: [blobOutputBinding],
handler: saveSnippet,
});
```


This code handles the `savesnippet`

trigger:

```
export async function saveSnippet(
_toolArguments: unknown,
context: InvocationContext
): Promise<string> {
console.info("Saving snippet");
// Get snippet name and content from the tool arguments
const mcptoolargs = context.triggerMetadata.mcptoolargs as {
snippetname?: string;
snippet?: string;
};
const snippetName = mcptoolargs?.snippetname;
const snippet = mcptoolargs?.snippet;
if (!snippetName) {
return "No snippet name provided";
}
if (!snippet) {
return "No snippet content provided";
}
// Save the snippet to blob storage using the output binding
context.extraOutputs.set(blobOutputBinding, snippet);
console.info(`Saved snippet: ${snippetName}`);
return snippet;
}
```


This code creates an endpoint to expose a tool named `getsnippet`

that tries to retrieve a code snippet by name from blob storage.

```
import { app, InvocationContext, input, output, arg } from "@azure/functions";
app.mcpTool("getSnippet", {
toolName: GET_SNIPPET_TOOL_NAME,
description: GET_SNIPPET_TOOL_DESCRIPTION,
toolProperties: {
[SNIPPET_NAME_PROPERTY_NAME]: arg.string().describe(SNIPPET_NAME_PROPERTY_DESCRIPTION)
},
extraInputs: [blobInputBinding],
handler: getSnippet,
});
```


This code handles the `getsnippet`

trigger:

```
export async function getSnippet(
_toolArguments: unknown,
context: InvocationContext
): Promise<string> {
console.info("Getting snippet");
// Get snippet name from the tool arguments
const mcptoolargs = context.triggerMetadata.mcptoolargs as {
snippetname?: string;
};
const snippetName = mcptoolargs?.snippetname;
console.info(`Snippet name: ${snippetName}`);
if (!snippetName) {
return "No snippet name provided";
}
// Get the content from blob binding - properly retrieving from extraInputs
const snippetContent = context.extraInputs.get(blobInputBinding);
if (!snippetContent) {
return `Snippet '${snippetName}' not found`;
}
console.info(`Retrieved snippet: ${snippetName}`);
return snippetContent as string;
}
```


For the complete code example, see [snippetsMcpTool.ts](https://github.com/Azure-Samples/remote-mcp-functions-typescript/blob/main/src/functions/snippetsMcpTool.ts).

This code uses the `mcp_tool_trigger`

decorator to create an endpoint to expose a tool named `save_snippet`

that tries to persist a named code snippet to blob storage.

```
@app.mcp_tool_trigger(
arg_name="context",
tool_name="save_snippet",
description="Save a snippet with a name.",
tool_properties=tool_properties_save_snippets_json,
)
@app.blob_output(arg_name="file", connection="AzureWebJobsStorage", path=_BLOB_PATH)
def save_snippet(file: func.Out[str], context) -> str:
content = json.loads(context)
snippet_name_from_args = content["arguments"][_SNIPPET_NAME_PROPERTY_NAME]
snippet_content_from_args = content["arguments"][_SNIPPET_PROPERTY_NAME]
if not snippet_name_from_args:
return "No snippet name provided"
if not snippet_content_from_args:
return "No snippet content provided"
file.set(snippet_content_from_args)
logging.info(f"Saved snippet: {snippet_content_from_args}")
return f"Snippet '{snippet_content_from_args}' saved successfully"
```


This code uses the `mcp_tool_trigger`

decorator to create an endpoint to expose a tool named `get_snippet`

that tries to retrieve a code snippet by name from blob storage.

```
@app.mcp_tool_trigger(
arg_name="context",
tool_name="get_snippet",
description="Retrieve a snippet by name.",
tool_properties=tool_properties_get_snippets_json,
)
@app.blob_input(arg_name="file", connection="AzureWebJobsStorage", path=_BLOB_PATH)
def get_snippet(file: func.InputStream, context) -> str:
"""
Retrieves a snippet by name from Azure Blob Storage.
Args:
file (func.InputStream): The input binding to read the snippet from Azure Blob Storage.
context: The trigger context containing the input arguments.
Returns:
str: The content of the snippet or an error message.
"""
snippet_content = file.read().decode("utf-8")
logging.info(f"Retrieved snippet: {snippet_content}")
return snippet_content
```


For the complete code example, see [function_app.py](https://github.com/Azure-Samples/remote-mcp-functions-python/blob/main/src/function_app.py).

Important

The MCP extension doesn't currently support PowerShell apps.

## Attributes

C# libraries use `McpToolTriggerAttribute`

to define the function trigger.

The attribute's constructor takes the following parameters:

| Parameter | Description |
|---|---|
ToolName |
(Required) name of the tool that's being exposed by the MCP trigger endpoint. |
Description |
(Optional) friendly description of the tool endpoint for clients. |

See [Usage](#usage) to learn how to define properties of the endpoint as input parameters.

## Annotations

The `@McpToolTrigger`

annotation creates a function that exposes a tool endpoint in your remote MCP server.

The annotation supports the following configuration options:

| Parameter | Description |
|---|---|
name |
(Required) name of the tool that's being exposed by the MCP trigger endpoint. |
description |
(Optional) friendly description of the tool endpoint for clients. |

The `@McpToolProperty`

annotation defines individual properties for your tools. Each property parameter in your function should be annotated with this annotation.

The `@McpToolProperty`

annotation supports the following configuration options:

| Parameter | Description |
|---|---|
name |
(Required) name of the tool property that gets exposed to clients. |
propertyType |
(Required) type of the tool property. Valid types are: `string` , `number` , `integer` , `boolean` , `object` . |
description |
(Optional) description of what the tool property does. |
required |
(Optional) if set to `true` , the tool property is required as an argument for tool calls. Defaults to `false` . |

## Decorators

*Applies only to the Python v2 programming model.*

The `mcp_tool_trigger`

decorator requires version 1.24.0 or later of the [ azure-functions package](https://pypi.org/project/azure-functions/). The following MCP trigger properties are supported on

`mcp_tool_trigger`

:| Property | Description |
|---|---|
arg_name |
The variable name (usually `context` ) used in function code to access the execution context. |
tool_name |
(Required) The name of the MCP server tool exposed by the function endpoint. |
description |
A description of the MCP server tool exposed by the function endpoint. |
tool_properties |
The JSON string representation of one or more property objects that expose properties of the tool to clients. |

## Configuration

The trigger supports these binding options, which are defined in your code:

| Options | Description |
|---|---|
type |
Must be set to `mcpToolTrigger` . Only used with generic definitions. |
toolName |
(Required) The name of the MCP server tool exposed by the function endpoint. |
description |
A description of the MCP server tool exposed by the function endpoint. |
toolProperties |
An array of `toolProperty` objects that expose properties of the tool to clients. |
extraOutputs |
When defined, sends function output to another binding. |
handler |
The method that contains the actual function code. |

See the [Example section](#example) for complete examples.

## Usage

The MCP tool trigger can bind to the following types:

| Type | Description |
|---|---|
|

[define tool properties](#tool-properties).When binding to a JSON serializable type, you can optionally also include a parameter of type

[ToolInvocationContext](https://github.com/Azure/azure-functions-mcp-extension/blob/main/src/Microsoft.Azure.Functions.Worker.Extensions.Mcp/Abstractions/ToolInvocationContext.cs)to access the tool call information.### Tool properties

MCP clients invoke tools with arguments to provide data and context for the tool's operation. The clients know how to collect and pass these arguments based on properties that the tool advertises as part of the protocol. You therefore need to define properties of the tool in your function code.

When you define a tool property, it's optional by default, and the client can omit it when invoking the tool. You need to explicitly mark properties as required if the tool can't operate without them.

Note

Earlier versions of the MCP extension preview made all tool properties required by default. This behavior changed as of version `1.0.0-preview.7`

, and now you must explicitly mark properties as required.

In C#, you can define properties for your tools in several ways. Which approach you use is a matter of code style preference. The options are:

- Your function takes input parameters using the
`McpToolProperty`

attribute. - You define a custom type with the properties, and the function binds to that type.
- You use the
`FunctionsApplicationBuilder`

to define properties in your`Program.cs`

file.

You can define one or more tool properties by applying the `McpToolProperty`

attribute to input binding-style parameters in your function.

The `McpToolPropertyAttribute`

type supports these properties:

| Property | Description |
|---|---|
PropertyName |
Name of the tool property that gets exposed to clients. |
Description |
Description of what the tool property does. |
IsRequired |
(Optional) If set to `true` , the tool property is required as an argument for tool calls. Defaults to `false` . |

The property type is inferred from the type of the parameter to which you apply the attribute. For example `[McpToolProperty("snippetname", "The name of the snippet.", true)] string name`

defines a required tool property named `snippetname`

of type `string`

in MCP messages.

You can see these attributes used in the `SaveSnippet`

tool in the [Examples](#example).

In Java, you define tool properties by using the `@McpToolProperty`

annotation on individual function parameters. Each parameter that represents a tool property should be annotated with this annotation, specifying the property name, type, description, and whether it's required.

You can see these annotations used in the [Examples](#example).

You can configure tool properties in the trigger definition's `toolProperties`

field, which is a string representation of an array of `ToolProperty`

objects.

A `ToolProperty`

object has this structure:

```
{
"propertyName": "Name of the property",
"propertyType": "Type of the property",
"description": "Optional property description",
"isRequired": true|false,
"isArray": true|false
}
```


The fields of a `ToolProperty`

object are:

| Property | Description |
|---|---|
propertyName |
Name of the tool property that gets exposed to clients. |
propertyType |
Type of the tool property. Valid types are: `string` , `number` , `integer` , `boolean` , `object` . See `isArray` for array types. |
description |
Description of what the tool property does. |
isRequired |
(Optional) If set to `true` , the tool property is required as an argument for tool calls. Defaults to `false` . |
isArray |
(Optional) If set to `true` , the tool property is an array of the specified property type. Defaults to `false` . |

You can provide the `toolProperties`

field as an array of `ToolProperty`

objects, or you can use the `arg`

helpers from `@azure/functions`

to define properties in a more type-safe way:

```
toolProperties: {
[SNIPPET_NAME_PROPERTY_NAME]: arg.string().describe(SNIPPET_NAME_PROPERTY_DESCRIPTION)
}
```


For more information, see [Examples](#example).

## host.json settings

The host.json file contains settings that control MCP trigger behaviors. See the [host.json settings](functions-bindings-mcp#hostjson-settings) section for details regarding available settings.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-twilio -->

# Twilio binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to send text messages by using [Twilio](https://www.twilio.com/) bindings in Azure Functions. Azure Functions supports output bindings for Twilio.

This is reference information for Azure Functions developers. If you're new to Azure Functions, start with the following resources:

C# developer references:


## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

There is currently no support for Twilio for an isolated worker process app.

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

## Example

Unless otherwise noted, these examples are specific to version 2.x and later version of the Functions runtime.

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The Twilio binding isn't currently supported for a function app running in an isolated worker process.

The following example shows a Twilio output binding in a *function.json* file and a [JavaScript function](functions-reference-node) that uses the binding.

Here's binding data in the *function.json* file:

Example function.json:

```
{
"type": "twilioSms",
"name": "message",
"accountSidSetting": "TwilioAccountSid",
"authTokenSetting": "TwilioAuthToken",
"from": "+1425XXXXXXX",
"direction": "out",
"body": "Azure Functions Testing"
}
```


Here's the JavaScript code:

```
module.exports = async function (context, myQueueItem) {
context.log('Node.js queue trigger function processed work item', myQueueItem);
// In this example the queue item is a JSON string representing an order that contains the name of a
// customer and a mobile number to send text updates to.
var msg = "Hello " + myQueueItem.name + ", thank you for your order.";
// Even if you want to use a hard coded message in the binding, you must at least
// initialize the message binding.
context.bindings.message = {};
// A dynamic message can be set instead of the body in the output binding. The "To" number
// must be specified in code.
context.bindings.message = {
body : msg,
to : myQueueItem.mobileNumber
};
};
```


Complete PowerShell examples aren't currently available for SendGrid bindings.

The following example shows how to send an SMS message using the output binding as defined in the following *function.json*.

```
{
"type": "twilioSms",
"name": "twilioMessage",
"accountSidSetting": "TwilioAccountSID",
"authTokenSetting": "TwilioAuthToken",
"from": "+1XXXXXXXXXX",
"direction": "out",
"body": "Azure Functions Testing"
}
```


You can pass a serialized JSON object to the `func.Out`

parameter to send the SMS message.

```
import logging
import json
import azure.functions as func
def main(req: func.HttpRequest, twilioMessage: func.Out[str]) -> func.HttpResponse:
message = req.params.get('message')
to = req.params.get('to')
value = {
"body": message,
"to": to
}
twilioMessage.set(json.dumps(value))
return func.HttpResponse(f"Message sent")
```


The following example shows how to use the [TwilioSmsOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.twiliosmsoutput) annotation to send an SMS message. Values for `to`

, `from`

, and `body`

are required in the attribute definition even if you override them programmatically.

```
package com.function;
import java.util.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.*;
public class TwilioOutput {
@FunctionName("TwilioOutput")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = { HttpMethod.GET, HttpMethod.POST },
authLevel = AuthorizationLevel.FUNCTION) HttpRequestMessage<Optional<String>> request,
@TwilioSmsOutput(
name = "twilioMessage",
accountSid = "AzureWebJobsTwilioAccountSID",
authToken = "AzureWebJobsTwilioAuthToken",
to = "+1XXXXXXXXXX",
body = "From Azure Functions",
from = "+1XXXXXXXXXX") OutputBinding<String> twilioMessage,
final ExecutionContext context) {
String message = request.getQueryParameters().get("message");
String to = request.getQueryParameters().get("to");
StringBuilder builder = new StringBuilder()
.append("{")
.append("\"body\": \"%s\",")
.append("\"to\": \"%s\"")
.append("}");
final String body = String.format(builder.toString(), message, to);
twilioMessage.setValue(body);
return request.createResponseBuilder(HttpStatus.OK).body("Message sent").build();
}
}
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the output binding. C# script instead uses a [function.json configuration file](#configuration).

The Twilio binding isn't currently supported for a function app running in an isolated worker process.

## Annotations

The [TwilioSmsOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.twiliosmsoutput) annotation allows you to declaratively configure the Twilio output binding by providing the following configuration values:

+

Place the [TwilioSmsOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.twiliosmsoutput) annotation on an [ OutputBinding<T>](/en-us/java/api/com.microsoft.azure.functions.outputbinding) parameter, where

`T`

may be any native Java type such as `int`

, `String`

, `byte[]`

, or a POJO type.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file, which differs by runtime version:

| function.json property | Description |
|---|---|
type |
must be set to `twilioSms` . |
direction |
must be set to `out` . |
name |
Variable name used in function code for the Twilio SMS text message. |
accountSidSetting |
This value must be set to the name of an app setting that holds your Twilio Account Sid (`TwilioAccountSid` ). When not set, the default app setting name is `AzureWebJobsTwilioAccountSid` . |
authTokenSetting |
This value must be set to the name of an app setting that holds your Twilio authentication token (`TwilioAccountAuthToken` ). When not set, the default app setting name is `AzureWebJobsTwilioAuthToken` . |
from |
This value is set to the phone number that the SMS text is sent from. |
body |
This value can be used to hard code the SMS text message if you don't need to set it dynamically in the code for your function. |

In version 2.x, you set the `to`

value in your code.

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

---
<!-- Source: N/A -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-data-explorer -->

# Azure Data Explorer bindings for Azure Functions overview (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This set of articles explains how to work with [Azure Data Explorer](/en-us/azure/data-explorer/index) bindings in Azure Functions. Azure Functions supports input bindings and output bindings for Azure Data Explorer clusters.

| Action | Type |
|---|---|
| Read data from a database |
|

[Output binding](functions-bindings-azure-data-explorer-output)## Install the extension

The extension NuGet package you install depends on the C# mode you're using in your function app.

Functions run in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

Add the extension to your project by installing [this NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Kusto/).

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Kusto --prerelease
```


## Install the bundle

Azure Data Explorer bindings extension is part of a preview [extension bundle](extension-bundles), which is specified in your *host.json* project file.

You can add the preview extension bundle by adding or replacing the following code in your *host.json* file:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle.Preview",
"version": "[4.*, 5.0.0)"
}
}
```


## Functions runtime

Note

Python language support for the Azure Data Explorer bindings extension is available starting with v4.6.0 or later of the [Functions runtime](set-runtime-version#manual-version-updates-on-linux). You might need to update your installation of Azure Functions [Core Tools](functions-run-local) for local development.

## Install the bundle

The Azure Data Explorer bindings extension is part of a preview [extension bundle](extension-bundles), which is specified in your *host.json* project file.

You can add the preview extension bundle by adding or replacing the following code in your *host.json* file:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle.Preview",
"version": "[4.*, 5.0.0)"
}
}
```


## Install the bundle

Azure Data Explorer bindings extension is part of a preview [extension bundle](extension-bundles), which is specified in your *host.json* project file.

You can add the preview extension bundle by adding or replacing the following code in your *host.json* file:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle.Preview",
"version": "[4.*, 5.0.0)"
}
}
```


## Update packages

Add the Java library for Azure Data Explorer bindings to your Functions project with an update to the `pom.xml`

file in your Python Azure Functions project, as follows:

```
<dependency>
<groupId>com.microsoft.azure.functions</groupId>
<artifactId>azure-functions-java-library-kusto</artifactId>
<version>1.0.4-Preview</version>
</dependency>
```


## Kusto connection string

Azure Data Explorer bindings for Azure Functions have a required property for the connection string on all bindings. The connection string is documented at [Kusto connection strings](/en-us/azure/data-explorer/kusto/api/connection-strings/kusto).

## Considerations

- Azure Data Explorer binding supports version 4.x and later of the Functions runtime.
- Source code for the Azure Data Explorer bindings is in
[this GitHub repository](https://github.com/Azure/Webjobs.Extensions.Kusto). - For enhanced security, your function app should use managed identities when connecting to Azure Data Explorer instead of using connection strings that contain keys. For more information, see
[Kusto connection strings](/en-us/azure/data-explorer/kusto/api/connection-strings/kusto). For managed identity-based connections, you must set the`managedServiceIdentity`

property in the binding definition. - This binding requires connectivity to Azure Data Explorer. For input bindings, users require
**Viewer**permissions. For output bindings, users require**Ingestor**permissions. For more information about permissions, see[Role-based access control](/en-us/azure/data-explorer/kusto/management/access-control/role-based-access-control).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-kafka-trigger -->

# Apache Kafka trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the Apache Kafka trigger in Azure Functions to run your function code in response to messages in Kafka topics. You can also use a [Kafka output binding](functions-bindings-kafka-output) to write from your function to a topic. For information on setup and configuration details, see [Apache Kafka bindings for Azure Functions overview](functions-bindings-kafka).

Important

Kafka bindings are available for Functions on the [Flex Consumption plan](flex-consumption-plan), [Elastic Premium Plan](functions-premium-plan), and [Dedicated (App Service) plan](dedicated-plan). They are only supported on version 4.x of the Functions runtime.

## Example

The usage of the trigger depends on the C# modality used in your function app, which can be one of the following modes:

A compiled C# function that uses an [isolated worker process class library](dotnet-isolated-process-guide) that runs in a process that's separate from the runtime.

The attributes you use depend on the specific event provider.

The following example shows a C# function that reads and logs the Kafka message as a Kafka event:

```
[Function("KafkaTrigger")]
public static void Run(
[KafkaTrigger("BrokerList",
"topic",
Username = "ConfluentCloudUserName",
Password = "ConfluentCloudPassword",
Protocol = BrokerProtocol.SaslSsl,
AuthenticationMode = BrokerAuthenticationMode.Plain,
ConsumerGroup = "$Default")] string eventData, FunctionContext context)
{
var logger = context.GetLogger("KafkaFunction");
logger.LogInformation($"C# Kafka trigger function processed a message: {JObject.Parse(eventData)["Value"]}");
}
```


To receive events in a batch, use a string array as input, as shown in the following example:

```
[Function("KafkaTriggerMany")]
public static void Run(
[KafkaTrigger("BrokerList",
"topic",
Username = "ConfluentCloudUserName",
Password = "ConfluentCloudPassword",
Protocol = BrokerProtocol.SaslSsl,
AuthenticationMode = BrokerAuthenticationMode.Plain,
ConsumerGroup = "$Default",
IsBatched = true)] string[] events, FunctionContext context)
{
foreach (var kevent in events)
{
var logger = context.GetLogger("KafkaFunction");
logger.LogInformation($"C# Kafka trigger function processed a message: {JObject.Parse(kevent)["Value"]}");
}
```


The following function logs the message and headers for the Kafka Event:

```
[Function("KafkaTriggerWithHeaders")]
public static void Run(
[KafkaTrigger("BrokerList",
"topic",
Username = "ConfluentCloudUserName",
Password = "ConfluentCloudPassword",
Protocol = BrokerProtocol.SaslSsl,
AuthenticationMode = BrokerAuthenticationMode.Plain,
ConsumerGroup = "$Default")] string eventData, FunctionContext context)
{
var eventJsonObject = JObject.Parse(eventData);
var logger = context.GetLogger("KafkaFunction");
logger.LogInformation($"C# Kafka trigger function processed a message: {eventJsonObject["Value"]}");
var headersJArr = eventJsonObject["Headers"] as JArray;
logger.LogInformation("Headers for this event: ");
foreach (JObject header in headersJArr)
{
logger.LogInformation($"{header["Key"]} {System.Text.Encoding.UTF8.GetString((byte[])header["Value"])}");
}
}
```


For a complete set of working .NET examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/dotnet-isolated/).

The usage of the trigger depends on your version of the Node.js programming model.

In the Node.js v4 model, you define your trigger directly in your function code. For more information, see the [Azure Functions Node.js developer guide](functions-reference-node?pivots=nodejs-model-v4).

In these examples, the event providers are either Confluent or Azure Event Hubs. These examples show how to define a Kafka trigger for a function that reads a Kafka message.

```
const { app } = require("@azure/functions");
async function kafkaTrigger(event, context) {
context.log("Event Offset: " + event.Offset);
context.log("Event Partition: " + event.Partition);
context.log("Event Topic: " + event.Topic);
context.log("Event Timestamp: " + event.Timestamp);
context.log("Event Key: " + event.Key);
context.log("Event Value (as string): " + event.Value);
let event_obj = JSON.parse(event.Value);
context.log("Event Value Object: ");
context.log(" Value.registertime: ", event_obj.registertime.toString());
context.log(" Value.userid: ", event_obj.userid);
context.log(" Value.regionid: ", event_obj.regionid);
context.log(" Value.gender: ", event_obj.gender);
}
app.generic("Kafkatrigger", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
topic: "topic",
brokerList: "%BrokerList%",
username: "%ConfluentCloudUserName%",
password: "%ConfluentCloudPassword%",
consumerGroup: "$Default",
protocol: "saslSsl",
authenticationMode: "plain",
dataType: "string"
},
handler: kafkaTrigger,
});
```


To receive events in a batch, set the `cardinality`

value to `many`

, as shown in these examples:

```
const { app } = require("@azure/functions");
async function kafkaTriggerMany(events, context) {
for (const event of events) {
context.log("Event Offset: " + event.Offset);
context.log("Event Partition: " + event.Partition);
context.log("Event Topic: " + event.Topic);
context.log("Event Key: " + event.Key);
context.log("Event Timestamp: " + event.Timestamp);
context.log("Event Value (as string): " + event.Value);
let event_obj = JSON.parse(event.Value);
context.log("Event Value Object: ");
context.log(" Value.registertime: ", event_obj.registertime.toString());
context.log(" Value.userid: ", event_obj.userid);
context.log(" Value.regionid: ", event_obj.regionid);
context.log(" Value.gender: ", event_obj.gender);
}
}
app.generic("kafkaTriggerMany", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
topic: "topic",
brokerList: "%BrokerList%",
username: "%ConfluentCloudUserName%",
password: "%ConfluentCloudPassword%",
consumerGroup: "$Default",
protocol: "saslSsl",
authenticationMode: "plain",
dataType: "string",
cardinality: "MANY"
},
handler: kafkaTriggerMany,
});
```


You can define a generic [Avro schema](http://avro.apache.org/docs/current/) for the event passed to the trigger. This example defines the trigger for the specific provider with a generic Avro schema:

```
const { app } = require("@azure/functions");
async function kafkaAvroGenericTrigger(event, context) {
context.log("Processed kafka event: ", event);
if (context.triggerMetadata?.key !== undefined) {
context.log("message key: ", context.triggerMetadata?.key);
}
}
app.generic("kafkaAvroGenericTrigger", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
protocol: "SASLSSL",
password: "EventHubConnectionString",
dataType: "string",
topic: "topic",
authenticationMode: "PLAIN",
avroSchema:
'{"type":"record","name":"Payment","namespace":"io.confluent.examples.clients.basicavro","fields":[{"name":"id","type":"string"},{"name":"amount","type":"double"},{"name":"type","type":"string"}]}',
consumerGroup: "$Default",
username: "$ConnectionString",
brokerList: "%BrokerList%",
},
handler: kafkaAvroGenericTrigger,
});
```


For a complete set of working JavaScript examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/javascript-v4/src/functions).

```
import { app, InvocationContext } from "@azure/functions";
// This is a sample interface that describes the actual data in your event.
interface EventData {
registertime: number;
userid: string;
regionid: string;
gender: string;
}
export async function kafkaTrigger(
event: any,
context: InvocationContext
): Promise<void> {
context.log("Event Offset: " + event.Offset);
context.log("Event Partition: " + event.Partition);
context.log("Event Topic: " + event.Topic);
context.log("Event Timestamp: " + event.Timestamp);
context.log("Event Value (as string): " + event.Value);
let event_obj: EventData = JSON.parse(event.Value);
context.log("Event Value Object: ");
context.log(" Value.registertime: ", event_obj.registertime.toString());
context.log(" Value.userid: ", event_obj.userid);
context.log(" Value.regionid: ", event_obj.regionid);
context.log(" Value.gender: ", event_obj.gender);
}
app.generic("Kafkatrigger", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
topic: "topic",
brokerList: "%BrokerList%",
username: "%ConfluentCloudUserName%",
password: "%ConfluentCloudPassword%",
consumerGroup: "$Default",
protocol: "saslSsl",
authenticationMode: "plain",
dataType: "string"
},
handler: kafkaTrigger,
});
```


To receive events in a batch, set the `cardinality`

value to `many`

, as shown in these examples:

```
import { app, InvocationContext } from "@azure/functions";
// This is a sample interface that describes the actual data in your event.
interface EventData {
registertime: number;
userid: string;
regionid: string;
gender: string;
}
interface KafkaEvent {
Offset: number;
Partition: number;
Topic: string;
Timestamp: number;
Value: string;
}
export async function kafkaTriggerMany(
events: any,
context: InvocationContext
): Promise<void> {
for (const event of events) {
context.log("Event Offset: " + event.Offset);
context.log("Event Partition: " + event.Partition);
context.log("Event Topic: " + event.Topic);
context.log("Event Timestamp: " + event.Timestamp);
context.log("Event Value (as string): " + event.Value);
let event_obj: EventData = JSON.parse(event.Value);
context.log("Event Value Object: ");
context.log(" Value.registertime: ", event_obj.registertime.toString());
context.log(" Value.userid: ", event_obj.userid);
context.log(" Value.regionid: ", event_obj.regionid);
context.log(" Value.gender: ", event_obj.gender);
}
}
app.generic("kafkaTriggerMany", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
topic: "topic",
brokerList: "%BrokerList%",
username: "%ConfluentCloudUserName%",
password: "%ConfluentCloudPassword%",
consumerGroup: "$Default",
protocol: "saslSsl",
authenticationMode: "plain",
dataType: "string",
cardinality: "MANY"
},
handler: kafkaTriggerMany,
});
```


You can define a generic [Avro schema](http://avro.apache.org/docs/current/) for the event passed to the trigger. This example defines the trigger for the specific provider with a generic Avro schema:

```
import { app, InvocationContext } from "@azure/functions";
export async function kafkaAvroGenericTrigger(
event: any,
context: InvocationContext
): Promise<void> {
context.log("Processed kafka event: ", event);
context.log(
`Message ID: ${event.id}, amount: ${event.amount}, type: ${event.type}`
);
if (context.triggerMetadata?.key !== undefined) {
context.log(`Message Key : ${context.triggerMetadata?.key}`);
}
}
app.generic("kafkaAvroGenericTrigger", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
protocol: "SASLSSL",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
dataType: "string",
topic: "topic",
authenticationMode: "PLAIN",
avroSchema:
'{"type":"record","name":"Payment","namespace":"io.confluent.examples.clients.basicavro","fields":[{"name":"id","type":"string"},{"name":"amount","type":"double"},{"name":"type","type":"string"}]}',
consumerGroup: "$Default",
brokerList: "%BrokerList%",
},
handler: kafkaAvroGenericTrigger,
});
```


For a complete set of working TypeScript examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/typescript-v4/src/functions).

The specific properties of the `function.json`

file depend on your event provider. In these examples, the event providers are either Confluent or Azure Event Hubs. The following examples show a Kafka trigger for a function that reads and logs a Kafka message.

The following `function.json`

file defines the trigger for the specific provider:

```
{
"bindings": [
{
"type": "kafkaTrigger",
"name": "kafkaEvent",
"direction": "in",
"protocol" : "SASLSSL",
"password" : "%ConfluentCloudPassword%",
"dataType" : "string",
"topic" : "topic",
"authenticationMode" : "PLAIN",
"consumerGroup" : "$Default",
"username" : "%ConfluentCloudUserName%",
"brokerList" : "%BrokerList%",
"sslCaLocation": "confluent_cloud_cacert.pem"
}
]
}
```


The following code runs when the function is triggered:

```
using namespace System.Net
param($kafkaEvent, $TriggerMetadata)
Write-Output "Powershell Kafka trigger function called for message $kafkaEvent.Value"
```


To receive events in a batch, set the `cardinality`

value to `many`

in the function.json file, as shown in the following examples:

```
{
"bindings": [
{
"type": "kafkaTrigger",
"name": "kafkaEvent",
"direction": "in",
"protocol" : "SASLSSL",
"password" : "%ConfluentCloudPassword%",
"dataType" : "string",
"topic" : "topic",
"authenticationMode" : "PLAIN",
"cardinality" : "MANY",
"consumerGroup" : "$Default",
"username" : "%ConfluentCloudUserName%",
"brokerList" : "%BrokerList%",
"sslCaLocation": "confluent_cloud_cacert.pem"
}
]
}
```


The following code parses the array of events and logs the event data:

```
using namespace System.Net
param($kafkaEvents, $TriggerMetadata)
$kafkaEvents
foreach ($kafkaEvent in $kafkaEvents) {
$event = $kafkaEvent | ConvertFrom-Json -AsHashtable
Write-Output "Powershell Kafka trigger function called for message $event.Value"
}
```


The following code logs the header data:

```
using namespace System.Net
param($kafkaEvents, $TriggerMetadata)
foreach ($kafkaEvent in $kafkaEvents) {
$kevent = $kafkaEvent | ConvertFrom-Json -AsHashtable
Write-Output "Powershell Kafka trigger function called for message $kevent.Value"
Write-Output "Headers for this message:"
foreach ($header in $kevent.Headers) {
$DecodedValue = [System.Text.Encoding]::Unicode.GetString([System.Convert]::FromBase64String($header.Value))
$Key = $header.Key
Write-Output "Key: $Key Value: $DecodedValue"
}
}
```


You can define a generic [Avro schema](http://avro.apache.org/docs/current/) for the event passed to the trigger. The following function.json defines the trigger for the specific provider with a generic Avro schema:

```
{
"bindings" : [ {
"type" : "kafkaTrigger",
"direction" : "in",
"name" : "kafkaEvent",
"protocol" : "SASLSSL",
"password" : "ConfluentCloudPassword",
"topic" : "topic",
"authenticationMode" : "PLAIN",
"avroSchema" : "{\"type\":\"record\",\"name\":\"Payment\",\"namespace\":\"io.confluent.examples.clients.basicavro\",\"fields\":[{\"name\":\"id\",\"type\":\"string\"},{\"name\":\"amount\",\"type\":\"double\"},{\"name\":\"type\",\"type\":\"string\"}]}",
"consumerGroup" : "$Default",
"username" : "ConfluentCloudUsername",
"brokerList" : "%BrokerList%"
} ]
}
```


The following code runs when the function is triggered:

```
using namespace System.Net
param($kafkaEvent, $TriggerMetadata)
Write-Output "Powershell Kafka trigger function called for message $kafkaEvent.Value"
```


For a complete set of working PowerShell examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/powershell/).

The usage of the trigger depends on your version of the Python programming model.

In the Python v2 model, you define your trigger directly in your function code using decorators. For more information, see the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

These examples show how to define a Kafka trigger for a function that reads a Kafka message.

```
@KafkaTrigger.function_name(name="KafkaTrigger")
@KafkaTrigger.kafka_trigger(
arg_name="kevent",
topic="KafkaTopic",
broker_list="KafkaBrokerList",
username="KafkaUsername",
password="KafkaPassword",
protocol="SaslSsl",
authentication_mode="Plain",
consumer_group="$Default1")
def kafka_trigger(kevent : func.KafkaEvent):
logging.info(kevent.get_body().decode('utf-8'))
logging.info(kevent.metadata)
```


This example receives events in a batch by setting the `cardinality`

value to `many`

.

```
@KafkaTrigger.function_name(name="KafkaTriggerMany")
@KafkaTrigger.kafka_trigger(
arg_name="kevents",
topic="KafkaTopic",
broker_list="KafkaBrokerList",
username="KafkaUsername",
password="KafkaPassword",
protocol="SaslSsl",
authentication_mode="Plain",
cardinality="MANY",
data_type="string",
consumer_group="$Default2")
def kafka_trigger_many(kevents : typing.List[func.KafkaEvent]):
for event in kevents:
logging.info(event.get_body())
```


You can define a generic [Avro schema](http://avro.apache.org/docs/current/) for the event passed to the trigger.

```
@KafkaTriggerAvro.function_name(name="KafkaTriggerAvroOne")
@KafkaTriggerAvro.kafka_trigger(
arg_name="kafkaTriggerAvroGeneric",
topic="KafkaTopic",
broker_list="KafkaBrokerList",
username="KafkaUsername",
password="KafkaPassword",
protocol="SaslSsl",
authentication_mode="Plain",
consumer_group="$Default",
avro_schema= "{\"type\":\"record\",\"name\":\"Payment\",\"namespace\":\"io.confluent.examples.clients.basicavro\",\"fields\":[{\"name\":\"id\",\"type\":\"string\"},{\"name\":\"amount\",\"type\":\"double\"},{\"name\":\"type\",\"type\":\"string\"}]}")
def kafka_trigger_avro_one(kafkaTriggerAvroGeneric : func.KafkaEvent):
logging.info(kafkaTriggerAvroGeneric.get_body().decode('utf-8'))
logging.info(kafkaTriggerAvroGeneric.metadata)
```


For a complete set of working Python examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/python-v2/).

The annotations you use to configure your trigger depend on the specific event provider.

The following example shows a Java function that reads and logs the content of the Kafka event:

```
@FunctionName("KafkaTrigger")
public void runSingle(
@KafkaTrigger(
name = "KafkaTrigger",
topic = "topic",
brokerList="%BrokerList%",
consumerGroup="$Default",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
protocol = BrokerProtocol.SASLSSL,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
dataType = "string"
) String kafkaEventData,
final ExecutionContext context) {
context.getLogger().info(kafkaEventData);
}
```


To receive events in a batch, use an input string as an array, as shown in the following example:

```
@FunctionName("KafkaTriggerMany")
public void runMany(
@KafkaTrigger(
name = "kafkaTriggerMany",
topic = "topic",
brokerList="%BrokerList%",
consumerGroup="$Default",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
protocol = BrokerProtocol.SASLSSL,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
cardinality = Cardinality.MANY,
dataType = "string"
) String[] kafkaEvents,
final ExecutionContext context) {
for (String kevent: kafkaEvents) {
context.getLogger().info(kevent);
}
}
```


The following function logs the message and headers for the Kafka Event:

```
@FunctionName("KafkaTriggerManyWithHeaders")
public void runSingle(
@KafkaTrigger(
name = "KafkaTrigger",
topic = "topic",
brokerList="%BrokerList%",
consumerGroup="$Default",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
protocol = BrokerProtocol.SASLSSL,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
dataType = "string",
cardinality = Cardinality.MANY
) List<String> kafkaEvents,
final ExecutionContext context) {
Gson gson = new Gson();
for (String keventstr: kafkaEvents) {
KafkaEntity kevent = gson.fromJson(keventstr, KafkaEntity.class);
context.getLogger().info("Java Kafka trigger function called for message: " + kevent.Value);
context.getLogger().info("Headers for the message:");
for (KafkaHeaders header : kevent.Headers) {
String decodedValue = new String(Base64.getDecoder().decode(header.Value));
context.getLogger().info("Key:" + header.Key + " Value:" + decodedValue);
}
}
}
```


You can define a generic [Avro schema](http://avro.apache.org/docs/current/) for the event passed to the trigger. The following function defines a trigger for the specific provider with a generic Avro schema:

```
private static final String schema = "{\"type\":\"record\",\"name\":\"Payment\",\"namespace\":\"io.confluent.examples.clients.basicavro\",\"fields\":[{\"name\":\"id\",\"type\":\"string\"},{\"name\":\"amount\",\"type\":\"double\"},{\"name\":\"type\",\"type\":\"string\"}]}";
@FunctionName("KafkaAvroGenericTrigger")
public void runOne(
@KafkaTrigger(
name = "kafkaAvroGenericSingle",
topic = "topic",
brokerList="%BrokerList%",
consumerGroup="$Default",
username = "ConfluentCloudUsername",
password = "ConfluentCloudPassword",
avroSchema = schema,
authenticationMode = BrokerAuthenticationMode.PLAIN,
protocol = BrokerProtocol.SASLSSL) Payment payment,
final ExecutionContext context) {
context.getLogger().info(payment.toString());
}
```


For a complete set of working Java examples for Confluent, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/java/confluent/src/main/java/com/contoso/kafka).

## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the `KafkaTriggerAttribute`

to define the function trigger.

The following table explains the properties you can set by using this trigger attribute:

| Parameter | Description |
|---|---|
BrokerList |
(Required) The list of Kafka brokers monitored by the trigger. See
|

**Topic****ConsumerGroup****AvroSchema****KeyAvroSchema****KeyDataType**`KeyAvroSchema`

is set, this value is generic record. Accepted values are `Int`

, `Long`

, `String`

, and `Binary`

.**AuthenticationMode**`NotSet`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

, and `OAuthBearer`

.**Username**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**Password**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**Protocol**`NotSet`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**SslCaLocation****SslCertificateLocation****SslKeyLocation****SslKeyPassword****SslCertificatePEM**[Connections](#connections)for more information.**SslKeyPEM**[Connections](#connections)for more information.**SslCaPEM**[Connections](#connections)for more information.**SslCertificateandKeyPEM**[Connections](#connections)for more information.**SchemaRegistryUrl**[Connections](#connections)for more information.**SchemaRegistryUsername**[Connections](#connections)for more information.**SchemaRegistryPassword**[Connections](#connections)for more information.**OAuthBearerMethod**`oidc`

and `default`

.**OAuthBearerClientId**`OAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client ID. See [Connections](#connections)for more information.**OAuthBearerClientSecret**`OAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client secret. See [Connections](#connections)for more information.**OAuthBearerScope****OAuthBearerTokenEndpointUrl**`oidc`

method is used. See [Connections](#connections)for more information.**OAuthBearerExtensions**`oidc`

method is used. For example: `supportFeatureX=true,organizationId=sales-emea`

.## Annotations

The `KafkaTrigger`

annotation enables you to create a function that runs when it receives a topic. Supported options include the following elements:

| Element | Description |
|---|---|
name |
(Required) The name of the variable that represents the queue or topic message in function code. |
brokerList |
(Required) The list of Kafka brokers monitored by the trigger. See
|

**topic****cardinality**`ONE`

(default) and `MANY`

. Use `ONE`

when the input is a single message and `MANY`

when the input is an array of messages. When you use `MANY`

, you must also set a `dataType`

.**dataType**`string`

, the input is treated as just a string. When `binary`

, the message is received as binary data, and Functions tries to deserialize it to an actual parameter type byte[].**consumerGroup****avroSchema****authenticationMode**`NotSet`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

.**username**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**password**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**protocol**`NotSet`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****lagThreshold****schemaRegistryUrl**[Connections](#connections)for more information.**schemaRegistryUsername**[Connections](#connections)for more information.**schemaRegistryPassword**[Connections](#connections)for more information.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

function.json property |
Description |
|---|---|
type |
(Required) Set to `kafkaTrigger` . |
direction |
(Required) Set to `in` . |
name |
(Required) The name of the variable that represents the brokered data in function code. |
brokerList |
(Required) The list of Kafka brokers monitored by the trigger. See
|

**topic****cardinality**`ONE`

(default) and `MANY`

. Use `ONE`

when the input is a single message and `MANY`

when the input is an array of messages. When you use `MANY`

, you must also set a `dataType`

.**dataType**`string`

, the input is treated as just a string. When `binary`

, the message is received as binary data, and Functions tries to deserialize it to an actual byte array parameter type.**consumerGroup****avroSchema****keyAvroSchema****keyDataType**`keyAvroSchema`

is set, this value is generic record. Accepted values are `Int`

, `Long`

, `String`

, and `Binary`

.**authenticationMode**`NotSet`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

.**username**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**password**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**protocol**`NotSet`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****sslCertificatePEM**[Connections](#connections)for more information.**sslKeyPEM**[Connections](#connections)for more information.**sslCaPEM**[Connections](#connections)for more information.**sslCertificateandKeyPEM**[Connections](#connections)for more information.**lagThreshold****schemaRegistryUrl**[Connections](#connections)for more information.**schemaRegistryUsername**[Connections](#connections)for more information.**schemaRegistryPassword**[Connections](#connections)for more information.**oAuthBearerMethod**`oidc`

and `default`

.**oAuthBearerClientId**`oAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client ID. See [Connections](#connections)for more information.**oAuthBearerClientSecret**`oAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client secret. See [Connections](#connections)for more information.**oAuthBearerScope****oAuthBearerTokenEndpointUrl**`oidc`

method is used. See [Connections](#connections)for more information.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file. Python uses snake_case naming conventions for configuration properties.

function.json property |
Description |
|---|---|
type |
(Required) Set to `kafkaTrigger` . |
direction |
(Required) Set to `in` . |
name |
(Required) The name of the variable that represents the brokered data in function code. |
broker_list |
(Required) The list of Kafka brokers monitored by the trigger. See
|

**topic****cardinality**`ONE`

(default) and `MANY`

. Use `ONE`

when the input is a single message and `MANY`

when the input is an array of messages. When you use `MANY`

, you must also set a `data_type`

.**data_type**`string`

, the input is treated as just a string. When `binary`

, the message is received as binary data, and Functions tries to deserialize it to an actual parameter type byte[].**consumerGroup****avroSchema****authentication_mode**`NOTSET`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

.**username**`authentication_mode`

is `Gssapi`

. See [Connections](#connections)for more information.**password**`authentication_mode`

is `Gssapi`

. See [Connections](#connections)for more information.**protocol**`NOTSET`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****lag_threshold****schema_registry_url**[Connections](#connections)for more information.**schema_registry_username**[Connections](#connections)for more information.**schema_registry_password**[Connections](#connections)for more information.**o_auth_bearer_method**`oidc`

and `default`

.**o_auth_bearer_client_id**`o_auth_bearer_method`

is set to `oidc`

, this specifies the OAuth bearer client ID. See [Connections](#connections)for more information.**o_auth_bearer_client_secret**`o_auth_bearer_method`

is set to `oidc`

, this specifies the OAuth bearer client secret. See [Connections](#connections)for more information.**o_auth_bearer_scope****o_auth_bearer_token_endpoint_url**`oidc`

method is used. See [Connections](#connections)for more information.Note

Certificate PEM-related properties and Avro key-related properties aren't yet available in the Python library.

## Usage

The Kafka trigger currently supports Kafka events as strings and string arrays that are JSON payloads.

The Kafka trigger passes Kafka messages to the function as strings. The trigger also supports string arrays that are JSON payloads.

In a Premium plan, you must enable runtime scale monitoring for the Kafka output to scale out to multiple instances. To learn more, see [Enable runtime scaling](functions-bindings-kafka#enable-runtime-scaling).

You can't use the **Test/Run** feature of the **Code + Test** page in the Azure portal to work with Kafka triggers. You must instead send test events directly to the topic being monitored by the trigger.

For a complete set of supported host.json settings for the Kafka trigger, see [host.json settings](functions-bindings-kafka#hostjson-settings).

## Connections

Store all connection information required by your triggers and bindings in application settings, not in the binding definitions in your code. This guidance applies to credentials, which you should never store in your code.

Important

Credential settings must reference an [application setting](functions-how-to-use-azure-function-app-settings#settings). Don't hard-code credentials in your code or configuration files. When running locally, use the [local.settings.json file](functions-develop-local#local-settings-file) for your credentials, and don't publish the local.settings.json file.

When connecting to a managed Kafka cluster provided by [Confluent in Azure](https://www.confluent.io/azure/), you can use one of the following authentication methods.

Note

When using the Flex Consumption plan, file location-based certificate authentication properties (`SslCaLocation`

, `SslCertificateLocation`

, `SslKeyLocation`

) aren't supported. Instead, use the PEM-based certificate properties (`SslCaPEM`

, `SslCertificatePEM`

, `SslKeyPEM`

, `SslCertificateandKeyPEM`

) or store certificates in Azure Key Vault.

#### Schema Registry

To make use of schema registry provided by Confluent in Kafka Extension, set the following credentials:

| Setting | Recommended Value | Description |
|---|---|---|
SchemaRegistryUrl |
`SchemaRegistryUrl` |
URL of the schema registry service used for schema management. Usually of the format `https://psrc-xyz.us-east-2.aws.confluent.cloud` |
SchemaRegistryUsername |
`CONFLUENT_API_KEY` |
Username for basic auth on schema registry (if required). |
SchemaRegistryPassword |
`CONFLUENT_API_SECRET` |
Password for basic auth on schema registry (if required). |

#### Username/Password authentication

While using this form of authentication, make sure that `Protocol`

is set to either `SaslPlaintext`

or `SaslSsl`

, `AuthenticationMode`

is set to `Plain`

, `ScramSha256`

or `ScramSha512`

and, if the CA cert being used is different from the default ISRG Root X1 cert, make sure to update `SslCaLocation`

or `SslCaPEM`

.

| Setting | Recommended value | Description |
|---|---|---|
BrokerList |
`BootstrapServer` |
App setting named `BootstrapServer` contains the value of bootstrap server found in Confluent Cloud settings page. The value resembles `xyz-xyzxzy.westeurope.azure.confluent.cloud:9092` . |
Username |
`ConfluentCloudUsername` |
App setting named `ConfluentCloudUsername` contains the API access key from the Confluent Cloud web site. |
Password |
`ConfluentCloudPassword` |
App setting named `ConfluentCloudPassword` contains the API secret obtained from the Confluent Cloud web site. |
SslCaPEM |
`SSLCaPemCertificate` |
App setting named `SSLCaPemCertificate` that contains the CA certificate as a string in PEM format. The value should follow the standard format, for example: `-----BEGIN CERTIFICATE-----\nMII....JQ==\n-----END CERTIFICATE-----` . |

#### SSL authentication

Ensure that `Protocol`

is set to `SSL`

.

| Setting | Recommended Value | Description |
|---|---|---|
BrokerList |
`BootstrapServer` |
App setting named `BootstrapServer` contains the value of bootstrap server found in Confluent Cloud settings page. The value resembles `xyz-xyzxzy.westeurope.azure.confluent.cloud:9092` . |
SslCaPEM |
`SslCaCertificatePem` |
App setting named `SslCaCertificatePem` that contains PEM value of the CA certificate as a string. The value should follow the standard format: `-----BEGIN CERTIFICATE-----\nMII...JQ==\n-----END CERTIFICATE-----` |
SslCertificatePEM |
`SslClientCertificatePem` |
App setting named `SslClientCertificatePem` that contains PEM value of the client certificate as a string. The value should follow the standard format: `-----BEGIN CERTIFICATE-----\nMII...JQ==\n-----END CERTIFICATE-----` |
SslKeyPEM |
`SslClientKeyPem` |
App setting named `SslClientKeyPem` that contains PEM value of the client private key as a string. The value should follow the standard format: `-----BEGIN PRIVATE KEY-----\nMII...JQ==\n-----END PRIVATE KEY-----` |
SslCertificateandKeyPEM |
`SslClientCertificateAndKeyPem` |
App setting named `SslClientCertificateAndKeyPem` that contains PEM value of the client certificate and client private key concatenated as a string. The value should follow the standard format: `-----BEGIN CERTIFICATE-----\nMII....JQ==\n-----END CERTIFICATE-----\n-----BEGIN PRIVATE KEY-----\nMIIE....BM=\n-----END PRIVATE KEY-----` |
SslKeyPassword |
`SslClientKeyPassword` |
App setting named `SslClientKeyPassword` that contains the password for the private key (if any). |

#### OAuth authentication

When using OAuth authentication, configure the OAuth-related properties in your binding definitions.

The string values you use for these settings must be present as [application settings in Azure](functions-how-to-use-azure-function-app-settings#settings) or in the `Values`

collection in the [local.settings.json file](functions-develop-local#local-settings-file) during local development.

You should also set the `Protocol`

and `AuthenticationMode`

in your binding definitions.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-mcp-trigger -->

# MCP tool trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the MCP tool trigger to define tool endpoints in a [Model Content Protocol (MCP)](https://github.com/modelcontextprotocol) server. Client language models and agents can use tools to perform specific tasks, such as storing or accessing code snippets.

For information on setup and configuration details, see the [overview](functions-bindings-mcp).

## Example

Note

For C#, the Azure Functions MCP extension supports only the [isolated worker model](dotnet-isolated-process-guide).

This code creates an endpoint to expose a tool named `SaveSnippet`

that tries to persist a named code snippet to blob storage.

```
private const string BlobPath = "snippets/{mcptoolargs.snippetname}.json";
[Function(nameof(SaveSnippet))]
[BlobOutput(BlobPath)]
public string SaveSnippet(
[McpToolTrigger("save_snippet", "Saves a code snippet into your snippet collection.")]
ToolInvocationContext context,
[McpToolProperty("snippetname", "The name of the snippet.", isRequired: true)]
string name,
[McpToolProperty("snippet", "The code snippet.", isRequired: true)]
string snippet
)
{
return snippet;
}
```


This code creates an endpoint to expose a tool named `GetSnippet`

that tries to retrieve a code snippet by name from blob storage.

```
private const string BlobPath = "snippets/{mcptoolargs.snippetname}.json";
[Function(nameof(GetSnippet))]
public object GetSnippet(
[McpToolTrigger("get_snippets", "Gets code snippets from your snippet collection.")]
ToolInvocationContext context,
[BlobInput(BlobPath)] string snippetContent
)
{
return snippetContent;
}
```


The tool properties for the `GetSnippet`

function are configured in `Program.cs`

:

```
var builder = FunctionsApplication.CreateBuilder(args);
builder.ConfigureFunctionsWebApplication();
builder.Services
.AddApplicationInsightsTelemetryWorkerService()
.ConfigureFunctionsApplicationInsights();
builder
.ConfigureMcpTool("get_snippets")
.WithProperty("snippetname", "string", "The name of the snippet.", required: true);
builder.Build().Run();
```


Tip

The example above used literal strings for things like the name of the "get_snippets" tool in both `Program.cs`

and the function. Consider instead using shared constant strings to keep things in sync across your project.

For the complete code example, see [SnippetTool.cs](https://github.com/Azure-Samples/remote-mcp-functions-dotnet/blob/main/src/SnippetsTool.cs).

This code creates an endpoint to expose a tool named `SaveSnippets`

that tries to persist a named code snippet to blob storage.

```
@FunctionName("SaveSnippets")
@StorageAccount("AzureWebJobsStorage")
public String saveSnippet(
@McpToolTrigger(
name = "saveSnippets",
description = "Saves a text snippet to your snippets collection."
)
String mcpToolInvocationContext,
@McpToolProperty(
name = "snippetName",
propertyType = "string",
description = "The name of the snippet.",
required = true
)
String snippetName,
@McpToolProperty(
name = "snippet",
propertyType = "string",
description = "The content of the snippet.",
required = true
)
String snippet,
@BlobOutput(name = "outputBlob", path = "snippets/{mcptoolargs.snippetName}.json")
OutputBinding<String> outputBlob,
final ExecutionContext context
) {
// Log the entire incoming JSON for debugging
context.getLogger().info(mcpToolInvocationContext);
// Log the snippet name and content
context.getLogger().info("Saving snippet with name: " + snippetName);
context.getLogger().info("Snippet content:\n" + snippet);
// Write the snippet content to the output blob
outputBlob.setValue(snippet);
return "Successfully saved snippet '" + snippetName + "' with " + snippet.length() + " characters.";
}
```


This code creates an endpoint to expose a tool named `GetSnippets`

that tries to retrieve a code snippet by name from blob storage.

```
@FunctionName("GetSnippets")
@StorageAccount("AzureWebJobsStorage")
public String getSnippet(
@McpToolTrigger(
name = "getSnippets",
description = "Gets a text snippet from your snippets collection."
)
String mcpToolInvocationContext,
@McpToolProperty(
name = "snippetName",
propertyType = "string",
description = "The name of the snippet.",
required = true
)
String snippetName,
@BlobInput(name = "inputBlob", path = "snippets/{mcptoolargs.snippetName}.json")
String inputBlob,
final ExecutionContext context
) {
// Log the entire incoming JSON for debugging
context.getLogger().info(mcpToolInvocationContext);
// Log the snippet name and the fetched snippet content from the blob
context.getLogger().info("Retrieving snippet with name: " + snippetName);
context.getLogger().info("Snippet content:");
context.getLogger().info(inputBlob);
// Return the snippet content or a not found message
if (inputBlob != null && !inputBlob.trim().isEmpty()) {
return inputBlob;
} else {
return "Snippet '" + snippetName + "' not found.";
}
}
```


For the complete code example, see [Snippets.java](https://github.com/Azure-Samples/remote-mcp-functions-java/blob/main/src/main/java/com/function/Snippets.java).

Example code for JavaScript isn't currently available. See the TypeScript examples for general guidance using Node.js.

This code creates an endpoint to expose a tool named `savesnippet`

that tries to persist a named code snippet to blob storage.

```
import { app, InvocationContext, input, output, arg } from "@azure/functions";
app.mcpTool("saveSnippet", {
toolName: SAVE_SNIPPET_TOOL_NAME,
description: SAVE_SNIPPET_TOOL_DESCRIPTION,
toolProperties: {
[SNIPPET_NAME_PROPERTY_NAME]: arg.string().describe(SNIPPET_NAME_PROPERTY_DESCRIPTION),
[SNIPPET_PROPERTY_NAME]: arg.string().describe(SNIPPET_PROPERTY_DESCRIPTION)
},
extraOutputs: [blobOutputBinding],
handler: saveSnippet,
});
```


This code handles the `savesnippet`

trigger:

```
export async function saveSnippet(
_toolArguments: unknown,
context: InvocationContext
): Promise<string> {
console.info("Saving snippet");
// Get snippet name and content from the tool arguments
const mcptoolargs = context.triggerMetadata.mcptoolargs as {
snippetname?: string;
snippet?: string;
};
const snippetName = mcptoolargs?.snippetname;
const snippet = mcptoolargs?.snippet;
if (!snippetName) {
return "No snippet name provided";
}
if (!snippet) {
return "No snippet content provided";
}
// Save the snippet to blob storage using the output binding
context.extraOutputs.set(blobOutputBinding, snippet);
console.info(`Saved snippet: ${snippetName}`);
return snippet;
}
```


This code creates an endpoint to expose a tool named `getsnippet`

that tries to retrieve a code snippet by name from blob storage.

```
import { app, InvocationContext, input, output, arg } from "@azure/functions";
app.mcpTool("getSnippet", {
toolName: GET_SNIPPET_TOOL_NAME,
description: GET_SNIPPET_TOOL_DESCRIPTION,
toolProperties: {
[SNIPPET_NAME_PROPERTY_NAME]: arg.string().describe(SNIPPET_NAME_PROPERTY_DESCRIPTION)
},
extraInputs: [blobInputBinding],
handler: getSnippet,
});
```


This code handles the `getsnippet`

trigger:

```
export async function getSnippet(
_toolArguments: unknown,
context: InvocationContext
): Promise<string> {
console.info("Getting snippet");
// Get snippet name from the tool arguments
const mcptoolargs = context.triggerMetadata.mcptoolargs as {
snippetname?: string;
};
const snippetName = mcptoolargs?.snippetname;
console.info(`Snippet name: ${snippetName}`);
if (!snippetName) {
return "No snippet name provided";
}
// Get the content from blob binding - properly retrieving from extraInputs
const snippetContent = context.extraInputs.get(blobInputBinding);
if (!snippetContent) {
return `Snippet '${snippetName}' not found`;
}
console.info(`Retrieved snippet: ${snippetName}`);
return snippetContent as string;
}
```


For the complete code example, see [snippetsMcpTool.ts](https://github.com/Azure-Samples/remote-mcp-functions-typescript/blob/main/src/functions/snippetsMcpTool.ts).

This code uses the `mcp_tool_trigger`

decorator to create an endpoint to expose a tool named `save_snippet`

that tries to persist a named code snippet to blob storage.

```
@app.mcp_tool_trigger(
arg_name="context",
tool_name="save_snippet",
description="Save a snippet with a name.",
tool_properties=tool_properties_save_snippets_json,
)
@app.blob_output(arg_name="file", connection="AzureWebJobsStorage", path=_BLOB_PATH)
def save_snippet(file: func.Out[str], context) -> str:
content = json.loads(context)
snippet_name_from_args = content["arguments"][_SNIPPET_NAME_PROPERTY_NAME]
snippet_content_from_args = content["arguments"][_SNIPPET_PROPERTY_NAME]
if not snippet_name_from_args:
return "No snippet name provided"
if not snippet_content_from_args:
return "No snippet content provided"
file.set(snippet_content_from_args)
logging.info(f"Saved snippet: {snippet_content_from_args}")
return f"Snippet '{snippet_content_from_args}' saved successfully"
```


This code uses the `mcp_tool_trigger`

decorator to create an endpoint to expose a tool named `get_snippet`

that tries to retrieve a code snippet by name from blob storage.

```
@app.mcp_tool_trigger(
arg_name="context",
tool_name="get_snippet",
description="Retrieve a snippet by name.",
tool_properties=tool_properties_get_snippets_json,
)
@app.blob_input(arg_name="file", connection="AzureWebJobsStorage", path=_BLOB_PATH)
def get_snippet(file: func.InputStream, context) -> str:
"""
Retrieves a snippet by name from Azure Blob Storage.
Args:
file (func.InputStream): The input binding to read the snippet from Azure Blob Storage.
context: The trigger context containing the input arguments.
Returns:
str: The content of the snippet or an error message.
"""
snippet_content = file.read().decode("utf-8")
logging.info(f"Retrieved snippet: {snippet_content}")
return snippet_content
```


For the complete code example, see [function_app.py](https://github.com/Azure-Samples/remote-mcp-functions-python/blob/main/src/function_app.py).

Important

The MCP extension doesn't currently support PowerShell apps.

## Attributes

C# libraries use `McpToolTriggerAttribute`

to define the function trigger.

The attribute's constructor takes the following parameters:

| Parameter | Description |
|---|---|
ToolName |
(Required) name of the tool that's being exposed by the MCP trigger endpoint. |
Description |
(Optional) friendly description of the tool endpoint for clients. |

See [Usage](#usage) to learn how to define properties of the endpoint as input parameters.

## Annotations

The `@McpToolTrigger`

annotation creates a function that exposes a tool endpoint in your remote MCP server.

The annotation supports the following configuration options:

| Parameter | Description |
|---|---|
name |
(Required) name of the tool that's being exposed by the MCP trigger endpoint. |
description |
(Optional) friendly description of the tool endpoint for clients. |

The `@McpToolProperty`

annotation defines individual properties for your tools. Each property parameter in your function should be annotated with this annotation.

The `@McpToolProperty`

annotation supports the following configuration options:

| Parameter | Description |
|---|---|
name |
(Required) name of the tool property that gets exposed to clients. |
propertyType |
(Required) type of the tool property. Valid types are: `string` , `number` , `integer` , `boolean` , `object` . |
description |
(Optional) description of what the tool property does. |
required |
(Optional) if set to `true` , the tool property is required as an argument for tool calls. Defaults to `false` . |

## Decorators

*Applies only to the Python v2 programming model.*

The `mcp_tool_trigger`

decorator requires version 1.24.0 or later of the [ azure-functions package](https://pypi.org/project/azure-functions/). The following MCP trigger properties are supported on

`mcp_tool_trigger`

:| Property | Description |
|---|---|
arg_name |
The variable name (usually `context` ) used in function code to access the execution context. |
tool_name |
(Required) The name of the MCP server tool exposed by the function endpoint. |
description |
A description of the MCP server tool exposed by the function endpoint. |
tool_properties |
The JSON string representation of one or more property objects that expose properties of the tool to clients. |

## Configuration

The trigger supports these binding options, which are defined in your code:

| Options | Description |
|---|---|
type |
Must be set to `mcpToolTrigger` . Only used with generic definitions. |
toolName |
(Required) The name of the MCP server tool exposed by the function endpoint. |
description |
A description of the MCP server tool exposed by the function endpoint. |
toolProperties |
An array of `toolProperty` objects that expose properties of the tool to clients. |
extraOutputs |
When defined, sends function output to another binding. |
handler |
The method that contains the actual function code. |

See the [Example section](#example) for complete examples.

## Usage

The MCP tool trigger can bind to the following types:

| Type | Description |
|---|---|
|

[define tool properties](#tool-properties).When binding to a JSON serializable type, you can optionally also include a parameter of type

[ToolInvocationContext](https://github.com/Azure/azure-functions-mcp-extension/blob/main/src/Microsoft.Azure.Functions.Worker.Extensions.Mcp/Abstractions/ToolInvocationContext.cs)to access the tool call information.### Tool properties

MCP clients invoke tools with arguments to provide data and context for the tool's operation. The clients know how to collect and pass these arguments based on properties that the tool advertises as part of the protocol. You therefore need to define properties of the tool in your function code.

When you define a tool property, it's optional by default, and the client can omit it when invoking the tool. You need to explicitly mark properties as required if the tool can't operate without them.

Note

Earlier versions of the MCP extension preview made all tool properties required by default. This behavior changed as of version `1.0.0-preview.7`

, and now you must explicitly mark properties as required.

In C#, you can define properties for your tools in several ways. Which approach you use is a matter of code style preference. The options are:

- Your function takes input parameters using the
`McpToolProperty`

attribute. - You define a custom type with the properties, and the function binds to that type.
- You use the
`FunctionsApplicationBuilder`

to define properties in your`Program.cs`

file.

You can define one or more tool properties by applying the `McpToolProperty`

attribute to input binding-style parameters in your function.

The `McpToolPropertyAttribute`

type supports these properties:

| Property | Description |
|---|---|
PropertyName |
Name of the tool property that gets exposed to clients. |
Description |
Description of what the tool property does. |
IsRequired |
(Optional) If set to `true` , the tool property is required as an argument for tool calls. Defaults to `false` . |

The property type is inferred from the type of the parameter to which you apply the attribute. For example `[McpToolProperty("snippetname", "The name of the snippet.", true)] string name`

defines a required tool property named `snippetname`

of type `string`

in MCP messages.

You can see these attributes used in the `SaveSnippet`

tool in the [Examples](#example).

In Java, you define tool properties by using the `@McpToolProperty`

annotation on individual function parameters. Each parameter that represents a tool property should be annotated with this annotation, specifying the property name, type, description, and whether it's required.

You can see these annotations used in the [Examples](#example).

You can configure tool properties in the trigger definition's `toolProperties`

field, which is a string representation of an array of `ToolProperty`

objects.

A `ToolProperty`

object has this structure:

```
{
"propertyName": "Name of the property",
"propertyType": "Type of the property",
"description": "Optional property description",
"isRequired": true|false,
"isArray": true|false
}
```


The fields of a `ToolProperty`

object are:

| Property | Description |
|---|---|
propertyName |
Name of the tool property that gets exposed to clients. |
propertyType |
Type of the tool property. Valid types are: `string` , `number` , `integer` , `boolean` , `object` . See `isArray` for array types. |
description |
Description of what the tool property does. |
isRequired |
(Optional) If set to `true` , the tool property is required as an argument for tool calls. Defaults to `false` . |
isArray |
(Optional) If set to `true` , the tool property is an array of the specified property type. Defaults to `false` . |

You can provide the `toolProperties`

field as an array of `ToolProperty`

objects, or you can use the `arg`

helpers from `@azure/functions`

to define properties in a more type-safe way:

```
toolProperties: {
[SNIPPET_NAME_PROPERTY_NAME]: arg.string().describe(SNIPPET_NAME_PROPERTY_DESCRIPTION)
}
```


For more information, see [Examples](#example).

## host.json settings

The host.json file contains settings that control MCP trigger behaviors. See the [host.json settings](functions-bindings-mcp#hostjson-settings) section for details regarding available settings.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-twilio -->

# Twilio binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to send text messages by using [Twilio](https://www.twilio.com/) bindings in Azure Functions. Azure Functions supports output bindings for Twilio.

This is reference information for Azure Functions developers. If you're new to Azure Functions, start with the following resources:

C# developer references:


## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

There is currently no support for Twilio for an isolated worker process app.

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

## Example

Unless otherwise noted, these examples are specific to version 2.x and later version of the Functions runtime.

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The Twilio binding isn't currently supported for a function app running in an isolated worker process.

The following example shows a Twilio output binding in a *function.json* file and a [JavaScript function](functions-reference-node) that uses the binding.

Here's binding data in the *function.json* file:

Example function.json:

```
{
"type": "twilioSms",
"name": "message",
"accountSidSetting": "TwilioAccountSid",
"authTokenSetting": "TwilioAuthToken",
"from": "+1425XXXXXXX",
"direction": "out",
"body": "Azure Functions Testing"
}
```


Here's the JavaScript code:

```
module.exports = async function (context, myQueueItem) {
context.log('Node.js queue trigger function processed work item', myQueueItem);
// In this example the queue item is a JSON string representing an order that contains the name of a
// customer and a mobile number to send text updates to.
var msg = "Hello " + myQueueItem.name + ", thank you for your order.";
// Even if you want to use a hard coded message in the binding, you must at least
// initialize the message binding.
context.bindings.message = {};
// A dynamic message can be set instead of the body in the output binding. The "To" number
// must be specified in code.
context.bindings.message = {
body : msg,
to : myQueueItem.mobileNumber
};
};
```


Complete PowerShell examples aren't currently available for SendGrid bindings.

The following example shows how to send an SMS message using the output binding as defined in the following *function.json*.

```
{
"type": "twilioSms",
"name": "twilioMessage",
"accountSidSetting": "TwilioAccountSID",
"authTokenSetting": "TwilioAuthToken",
"from": "+1XXXXXXXXXX",
"direction": "out",
"body": "Azure Functions Testing"
}
```


You can pass a serialized JSON object to the `func.Out`

parameter to send the SMS message.

```
import logging
import json
import azure.functions as func
def main(req: func.HttpRequest, twilioMessage: func.Out[str]) -> func.HttpResponse:
message = req.params.get('message')
to = req.params.get('to')
value = {
"body": message,
"to": to
}
twilioMessage.set(json.dumps(value))
return func.HttpResponse(f"Message sent")
```


The following example shows how to use the [TwilioSmsOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.twiliosmsoutput) annotation to send an SMS message. Values for `to`

, `from`

, and `body`

are required in the attribute definition even if you override them programmatically.

```
package com.function;
import java.util.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.*;
public class TwilioOutput {
@FunctionName("TwilioOutput")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = { HttpMethod.GET, HttpMethod.POST },
authLevel = AuthorizationLevel.FUNCTION) HttpRequestMessage<Optional<String>> request,
@TwilioSmsOutput(
name = "twilioMessage",
accountSid = "AzureWebJobsTwilioAccountSID",
authToken = "AzureWebJobsTwilioAuthToken",
to = "+1XXXXXXXXXX",
body = "From Azure Functions",
from = "+1XXXXXXXXXX") OutputBinding<String> twilioMessage,
final ExecutionContext context) {
String message = request.getQueryParameters().get("message");
String to = request.getQueryParameters().get("to");
StringBuilder builder = new StringBuilder()
.append("{")
.append("\"body\": \"%s\",")
.append("\"to\": \"%s\"")
.append("}");
final String body = String.format(builder.toString(), message, to);
twilioMessage.setValue(body);
return request.createResponseBuilder(HttpStatus.OK).body("Message sent").build();
}
}
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the output binding. C# script instead uses a [function.json configuration file](#configuration).

The Twilio binding isn't currently supported for a function app running in an isolated worker process.

## Annotations

The [TwilioSmsOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.twiliosmsoutput) annotation allows you to declaratively configure the Twilio output binding by providing the following configuration values:

+

Place the [TwilioSmsOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.twiliosmsoutput) annotation on an [ OutputBinding<T>](/en-us/java/api/com.microsoft.azure.functions.outputbinding) parameter, where

`T`

may be any native Java type such as `int`

, `String`

, `byte[]`

, or a POJO type.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file, which differs by runtime version:

| function.json property | Description |
|---|---|
type |
must be set to `twilioSms` . |
direction |
must be set to `out` . |
name |
Variable name used in function code for the Twilio SMS text message. |
accountSidSetting |
This value must be set to the name of an app setting that holds your Twilio Account Sid (`TwilioAccountSid` ). When not set, the default app setting name is `AzureWebJobsTwilioAccountSid` . |
authTokenSetting |
This value must be set to the name of an app setting that holds your Twilio authentication token (`TwilioAccountAuthToken` ). When not set, the default app setting name is `AzureWebJobsTwilioAuthToken` . |
from |
This value is set to the phone number that the SMS text is sent from. |
body |
This value can be used to hard code the SMS text message if you don't need to set it dynamically in the code for your function. |

In version 2.x, you set the `to`

value in your code.

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-rabbitmq-output -->

# RabbitMQ output binding for Azure Functions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the RabbitMQ output binding to send messages to a RabbitMQ queue.

Note

The RabbitMQ bindings are only fully supported on [Elastic Premium](functions-premium-plan) and [Dedicated (App Service)](dedicated-plan) plans. [Flex Consumption](flex-consumption-plan) and [Consumption](consumption-plan) plans aren't yet supported.

RabbitMQ bindings aren't supported by the Azure Functions v1.x runtime.

For information on setup and configuration details, see the [overview](functions-bindings-rabbitmq-output).

## Example

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

```
[Function(nameof(RabbitMQFunction))]
[RabbitMQOutput(QueueName = "destinationQueue", ConnectionStringSetting = "RabbitMQConnection")]
public static string Run([RabbitMQTrigger("queue", ConnectionStringSetting = "RabbitMQConnection")] string item,
FunctionContext context)
{
var logger = context.GetLogger(nameof(RabbitMQFunction));
logger.LogInformation(item);
var message = $"Output message created at {DateTime.Now}";
return message;
}
```


The following Java function uses the `@RabbitMQOutput`

annotation from the [Java RabbitMQ types](https://mvnrepository.com/artifact/com.microsoft.azure.functions/azure-functions-java-library-rabbitmq) to describe the configuration for a RabbitMQ queue output binding. The function sends a message to the RabbitMQ queue when triggered by a TimerTrigger every 5 minutes.

```
@FunctionName("RabbitMQOutputExample")
public void run(
@TimerTrigger(name = "keepAliveTrigger", schedule = "0 */5 * * * *") String timerInfo,
@RabbitMQOutput(connectionStringSetting = "rabbitMQConnectionAppSetting", queueName = "hello") OutputBinding<String> output,
final ExecutionContext context) {
output.setValue("Some string");
}
```


The following example shows a RabbitMQ output binding in a *function.json* file and a [JavaScript function](functions-reference-node) that uses the binding. The function reads in the message from an HTTP trigger and outputs it to the RabbitMQ queue.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"type": "httpTrigger",
"direction": "in",
"authLevel": "function",
"name": "input",
"methods": [
"get",
"post"
]
},
{
"type": "rabbitMQ",
"name": "outputMessage",
"queueName": "outputQueue",
"connectionStringSetting": "rabbitMQConnectionAppSetting",
"direction": "out"
}
]
}
```


Here's JavaScript code:

```
module.exports = async function (context, input) {
context.bindings.outputMessage = input.body;
};
```


The following example shows a RabbitMQ output binding in a *function.json* file and a Python function that uses the binding. The function reads in the message from an HTTP trigger and outputs it to the RabbitMQ queue.

Here's the binding data in the *function.json* file:

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"get",
"post"
]
},
{
"type": "http",
"direction": "out",
"name": "$return"
},
{
"type": "rabbitMQ",
"name": "outputMessage",
"queueName": "outputQueue",
"connectionStringSetting": "rabbitMQConnectionAppSetting",
"direction": "out"
}
]
}
```


In * _init_.py*:

```
import azure.functions as func
def main(req: func.HttpRequest, outputMessage: func.Out[str]) -> func.HttpResponse:
input_msg = req.params.get('message')
outputMessage.set(input_msg)
return 'OK'
```


## Attributes

Both [isolated worker process](dotnet-isolated-process-guide) and [in-process](functions-dotnet-class-library) C# libraries use an attribute to define an output binding that writes to a RabbitMQ queue.

The `RabbitMQOutputAttribute`

constructor accepts these parameters:

| Parameter | Description |
|---|---|
QueueName |
Name of the queue from which to receive messages. |
HostName |
This parameter is no longer supported and is ignored. It will be removed in a future version. |
ConnectionStringSetting |
The name of the app setting that contains the connection string for your RabbitMQ server. This setting only takes an app setting key name, you can't directly set a connection string value. For more information, see
|

**UserNameSetting****PasswordSetting****Port**`5672`

.**DisableCertificateValidation**## Annotations

The `RabbitMQOutput`

annotation allows you to create a function that runs when a RabbitMQ message is created.

The annotation supports the following configuration settings:

| Setting | Description |
|---|---|
queueName |
Name of the queue from which to receive messages. |
connectionStringSetting |
The name of the app setting that contains the connection string for your RabbitMQ server. This setting only takes an app setting key name, you can't directly set a connection string value. For more information, see
|

**disableCertificateValidation**## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `RabbitMQ` . |
direction |
Must be set to `out` . |
name |
The name of the variable that represents the queue in function code. |
queueName |
Name of the queue to send messages to. |
connectionStringSetting |
The name of the app setting that contains the connection string for your RabbitMQ server. This setting only takes an app setting key name, you can't directly set a connection string value. For more information, see
|

**disableCertificateValidation**When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

See the [Example section](#example) for complete examples.

## Usage

The parameter type supported by the RabbitMQ trigger depends on the Functions runtime version, the extension package version, and the C# modality used.

The RabbitMQ bindings currently support only string and serializable object types when running in an isolated worker process.

Use the following parameter types for the output binding:

`byte[]`

- If the parameter value is null when the function exits, Functions doesn't create a message.`string`

- If the parameter value is null when the function exits, Functions doesn't create a message.`POJO`

- If the parameter value isn't formatted as a Java object, an error will be received.

The queue message is available via `context.bindings.<NAME>`

where `<NAME>`

matches the name defined in function.json. If the payload is JSON, the value is deserialized into an object.

### Connections

Important

The RabbitMQ binding doesn't support Microsoft Entra authentication and managed identities. You can use Azure Key Vault to centrally managed your RabbitMQ connection strings. To learn more, see [Manage Connections](manage-connections).

Starting with version 2.x of the extension, `hostName`

, `userNameSetting`

, and `passwordSetting`

are no longer supported to define a connection to the RabbitMQ server. You must instead use `connectionStringSetting`

.

The `connectionStringSetting`

property can only accept the name of a key-value pair in app settings. You can't directly set a connection string value in the binding.

For example, when you have set `connectionStringSetting`

to `rabbitMQConnection`

in your binding definition, your function app must have an app setting named `rabbitMQConnection`

that returns either a connection value like `amqp://myuser:***@contoso.rabbitmq.example.com:5672`

or an [Azure Key Vault reference](../app-service/app-service-key-vault-references).

When running locally, you must also have the key value for `connectionStringSetting`

defined in your *local.settings.json* file. Otherwise, your app can't connect to the service from your local computer and an error occurs.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-kafka-trigger -->

# Apache Kafka trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the Apache Kafka trigger in Azure Functions to run your function code in response to messages in Kafka topics. You can also use a [Kafka output binding](functions-bindings-kafka-output) to write from your function to a topic. For information on setup and configuration details, see [Apache Kafka bindings for Azure Functions overview](functions-bindings-kafka).

Important

Kafka bindings are available for Functions on the [Flex Consumption plan](flex-consumption-plan), [Elastic Premium Plan](functions-premium-plan), and [Dedicated (App Service) plan](dedicated-plan). They are only supported on version 4.x of the Functions runtime.

## Example

The usage of the trigger depends on the C# modality used in your function app, which can be one of the following modes:

A compiled C# function that uses an [isolated worker process class library](dotnet-isolated-process-guide) that runs in a process that's separate from the runtime.

The attributes you use depend on the specific event provider.

The following example shows a C# function that reads and logs the Kafka message as a Kafka event:

```
[Function("KafkaTrigger")]
public static void Run(
[KafkaTrigger("BrokerList",
"topic",
Username = "ConfluentCloudUserName",
Password = "ConfluentCloudPassword",
Protocol = BrokerProtocol.SaslSsl,
AuthenticationMode = BrokerAuthenticationMode.Plain,
ConsumerGroup = "$Default")] string eventData, FunctionContext context)
{
var logger = context.GetLogger("KafkaFunction");
logger.LogInformation($"C# Kafka trigger function processed a message: {JObject.Parse(eventData)["Value"]}");
}
```


To receive events in a batch, use a string array as input, as shown in the following example:

```
[Function("KafkaTriggerMany")]
public static void Run(
[KafkaTrigger("BrokerList",
"topic",
Username = "ConfluentCloudUserName",
Password = "ConfluentCloudPassword",
Protocol = BrokerProtocol.SaslSsl,
AuthenticationMode = BrokerAuthenticationMode.Plain,
ConsumerGroup = "$Default",
IsBatched = true)] string[] events, FunctionContext context)
{
foreach (var kevent in events)
{
var logger = context.GetLogger("KafkaFunction");
logger.LogInformation($"C# Kafka trigger function processed a message: {JObject.Parse(kevent)["Value"]}");
}
```


The following function logs the message and headers for the Kafka Event:

```
[Function("KafkaTriggerWithHeaders")]
public static void Run(
[KafkaTrigger("BrokerList",
"topic",
Username = "ConfluentCloudUserName",
Password = "ConfluentCloudPassword",
Protocol = BrokerProtocol.SaslSsl,
AuthenticationMode = BrokerAuthenticationMode.Plain,
ConsumerGroup = "$Default")] string eventData, FunctionContext context)
{
var eventJsonObject = JObject.Parse(eventData);
var logger = context.GetLogger("KafkaFunction");
logger.LogInformation($"C# Kafka trigger function processed a message: {eventJsonObject["Value"]}");
var headersJArr = eventJsonObject["Headers"] as JArray;
logger.LogInformation("Headers for this event: ");
foreach (JObject header in headersJArr)
{
logger.LogInformation($"{header["Key"]} {System.Text.Encoding.UTF8.GetString((byte[])header["Value"])}");
}
}
```


For a complete set of working .NET examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/dotnet-isolated/).

The usage of the trigger depends on your version of the Node.js programming model.

In the Node.js v4 model, you define your trigger directly in your function code. For more information, see the [Azure Functions Node.js developer guide](functions-reference-node?pivots=nodejs-model-v4).

In these examples, the event providers are either Confluent or Azure Event Hubs. These examples show how to define a Kafka trigger for a function that reads a Kafka message.

```
const { app } = require("@azure/functions");
async function kafkaTrigger(event, context) {
context.log("Event Offset: " + event.Offset);
context.log("Event Partition: " + event.Partition);
context.log("Event Topic: " + event.Topic);
context.log("Event Timestamp: " + event.Timestamp);
context.log("Event Key: " + event.Key);
context.log("Event Value (as string): " + event.Value);
let event_obj = JSON.parse(event.Value);
context.log("Event Value Object: ");
context.log(" Value.registertime: ", event_obj.registertime.toString());
context.log(" Value.userid: ", event_obj.userid);
context.log(" Value.regionid: ", event_obj.regionid);
context.log(" Value.gender: ", event_obj.gender);
}
app.generic("Kafkatrigger", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
topic: "topic",
brokerList: "%BrokerList%",
username: "%ConfluentCloudUserName%",
password: "%ConfluentCloudPassword%",
consumerGroup: "$Default",
protocol: "saslSsl",
authenticationMode: "plain",
dataType: "string"
},
handler: kafkaTrigger,
});
```


To receive events in a batch, set the `cardinality`

value to `many`

, as shown in these examples:

```
const { app } = require("@azure/functions");
async function kafkaTriggerMany(events, context) {
for (const event of events) {
context.log("Event Offset: " + event.Offset);
context.log("Event Partition: " + event.Partition);
context.log("Event Topic: " + event.Topic);
context.log("Event Key: " + event.Key);
context.log("Event Timestamp: " + event.Timestamp);
context.log("Event Value (as string): " + event.Value);
let event_obj = JSON.parse(event.Value);
context.log("Event Value Object: ");
context.log(" Value.registertime: ", event_obj.registertime.toString());
context.log(" Value.userid: ", event_obj.userid);
context.log(" Value.regionid: ", event_obj.regionid);
context.log(" Value.gender: ", event_obj.gender);
}
}
app.generic("kafkaTriggerMany", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
topic: "topic",
brokerList: "%BrokerList%",
username: "%ConfluentCloudUserName%",
password: "%ConfluentCloudPassword%",
consumerGroup: "$Default",
protocol: "saslSsl",
authenticationMode: "plain",
dataType: "string",
cardinality: "MANY"
},
handler: kafkaTriggerMany,
});
```


You can define a generic [Avro schema](http://avro.apache.org/docs/current/) for the event passed to the trigger. This example defines the trigger for the specific provider with a generic Avro schema:

```
const { app } = require("@azure/functions");
async function kafkaAvroGenericTrigger(event, context) {
context.log("Processed kafka event: ", event);
if (context.triggerMetadata?.key !== undefined) {
context.log("message key: ", context.triggerMetadata?.key);
}
}
app.generic("kafkaAvroGenericTrigger", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
protocol: "SASLSSL",
password: "EventHubConnectionString",
dataType: "string",
topic: "topic",
authenticationMode: "PLAIN",
avroSchema:
'{"type":"record","name":"Payment","namespace":"io.confluent.examples.clients.basicavro","fields":[{"name":"id","type":"string"},{"name":"amount","type":"double"},{"name":"type","type":"string"}]}',
consumerGroup: "$Default",
username: "$ConnectionString",
brokerList: "%BrokerList%",
},
handler: kafkaAvroGenericTrigger,
});
```


For a complete set of working JavaScript examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/javascript-v4/src/functions).

```
import { app, InvocationContext } from "@azure/functions";
// This is a sample interface that describes the actual data in your event.
interface EventData {
registertime: number;
userid: string;
regionid: string;
gender: string;
}
export async function kafkaTrigger(
event: any,
context: InvocationContext
): Promise<void> {
context.log("Event Offset: " + event.Offset);
context.log("Event Partition: " + event.Partition);
context.log("Event Topic: " + event.Topic);
context.log("Event Timestamp: " + event.Timestamp);
context.log("Event Value (as string): " + event.Value);
let event_obj: EventData = JSON.parse(event.Value);
context.log("Event Value Object: ");
context.log(" Value.registertime: ", event_obj.registertime.toString());
context.log(" Value.userid: ", event_obj.userid);
context.log(" Value.regionid: ", event_obj.regionid);
context.log(" Value.gender: ", event_obj.gender);
}
app.generic("Kafkatrigger", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
topic: "topic",
brokerList: "%BrokerList%",
username: "%ConfluentCloudUserName%",
password: "%ConfluentCloudPassword%",
consumerGroup: "$Default",
protocol: "saslSsl",
authenticationMode: "plain",
dataType: "string"
},
handler: kafkaTrigger,
});
```


To receive events in a batch, set the `cardinality`

value to `many`

, as shown in these examples:

```
import { app, InvocationContext } from "@azure/functions";
// This is a sample interface that describes the actual data in your event.
interface EventData {
registertime: number;
userid: string;
regionid: string;
gender: string;
}
interface KafkaEvent {
Offset: number;
Partition: number;
Topic: string;
Timestamp: number;
Value: string;
}
export async function kafkaTriggerMany(
events: any,
context: InvocationContext
): Promise<void> {
for (const event of events) {
context.log("Event Offset: " + event.Offset);
context.log("Event Partition: " + event.Partition);
context.log("Event Topic: " + event.Topic);
context.log("Event Timestamp: " + event.Timestamp);
context.log("Event Value (as string): " + event.Value);
let event_obj: EventData = JSON.parse(event.Value);
context.log("Event Value Object: ");
context.log(" Value.registertime: ", event_obj.registertime.toString());
context.log(" Value.userid: ", event_obj.userid);
context.log(" Value.regionid: ", event_obj.regionid);
context.log(" Value.gender: ", event_obj.gender);
}
}
app.generic("kafkaTriggerMany", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
topic: "topic",
brokerList: "%BrokerList%",
username: "%ConfluentCloudUserName%",
password: "%ConfluentCloudPassword%",
consumerGroup: "$Default",
protocol: "saslSsl",
authenticationMode: "plain",
dataType: "string",
cardinality: "MANY"
},
handler: kafkaTriggerMany,
});
```


You can define a generic [Avro schema](http://avro.apache.org/docs/current/) for the event passed to the trigger. This example defines the trigger for the specific provider with a generic Avro schema:

```
import { app, InvocationContext } from "@azure/functions";
export async function kafkaAvroGenericTrigger(
event: any,
context: InvocationContext
): Promise<void> {
context.log("Processed kafka event: ", event);
context.log(
`Message ID: ${event.id}, amount: ${event.amount}, type: ${event.type}`
);
if (context.triggerMetadata?.key !== undefined) {
context.log(`Message Key : ${context.triggerMetadata?.key}`);
}
}
app.generic("kafkaAvroGenericTrigger", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
protocol: "SASLSSL",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
dataType: "string",
topic: "topic",
authenticationMode: "PLAIN",
avroSchema:
'{"type":"record","name":"Payment","namespace":"io.confluent.examples.clients.basicavro","fields":[{"name":"id","type":"string"},{"name":"amount","type":"double"},{"name":"type","type":"string"}]}',
consumerGroup: "$Default",
brokerList: "%BrokerList%",
},
handler: kafkaAvroGenericTrigger,
});
```


For a complete set of working TypeScript examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/typescript-v4/src/functions).

The specific properties of the `function.json`

file depend on your event provider. In these examples, the event providers are either Confluent or Azure Event Hubs. The following examples show a Kafka trigger for a function that reads and logs a Kafka message.

The following `function.json`

file defines the trigger for the specific provider:

```
{
"bindings": [
{
"type": "kafkaTrigger",
"name": "kafkaEvent",
"direction": "in",
"protocol" : "SASLSSL",
"password" : "%ConfluentCloudPassword%",
"dataType" : "string",
"topic" : "topic",
"authenticationMode" : "PLAIN",
"consumerGroup" : "$Default",
"username" : "%ConfluentCloudUserName%",
"brokerList" : "%BrokerList%",
"sslCaLocation": "confluent_cloud_cacert.pem"
}
]
}
```


The following code runs when the function is triggered:

```
using namespace System.Net
param($kafkaEvent, $TriggerMetadata)
Write-Output "Powershell Kafka trigger function called for message $kafkaEvent.Value"
```


To receive events in a batch, set the `cardinality`

value to `many`

in the function.json file, as shown in the following examples:

```
{
"bindings": [
{
"type": "kafkaTrigger",
"name": "kafkaEvent",
"direction": "in",
"protocol" : "SASLSSL",
"password" : "%ConfluentCloudPassword%",
"dataType" : "string",
"topic" : "topic",
"authenticationMode" : "PLAIN",
"cardinality" : "MANY",
"consumerGroup" : "$Default",
"username" : "%ConfluentCloudUserName%",
"brokerList" : "%BrokerList%",
"sslCaLocation": "confluent_cloud_cacert.pem"
}
]
}
```


The following code parses the array of events and logs the event data:

```
using namespace System.Net
param($kafkaEvents, $TriggerMetadata)
$kafkaEvents
foreach ($kafkaEvent in $kafkaEvents) {
$event = $kafkaEvent | ConvertFrom-Json -AsHashtable
Write-Output "Powershell Kafka trigger function called for message $event.Value"
}
```


The following code logs the header data:

```
using namespace System.Net
param($kafkaEvents, $TriggerMetadata)
foreach ($kafkaEvent in $kafkaEvents) {
$kevent = $kafkaEvent | ConvertFrom-Json -AsHashtable
Write-Output "Powershell Kafka trigger function called for message $kevent.Value"
Write-Output "Headers for this message:"
foreach ($header in $kevent.Headers) {
$DecodedValue = [System.Text.Encoding]::Unicode.GetString([System.Convert]::FromBase64String($header.Value))
$Key = $header.Key
Write-Output "Key: $Key Value: $DecodedValue"
}
}
```


You can define a generic [Avro schema](http://avro.apache.org/docs/current/) for the event passed to the trigger. The following function.json defines the trigger for the specific provider with a generic Avro schema:

```
{
"bindings" : [ {
"type" : "kafkaTrigger",
"direction" : "in",
"name" : "kafkaEvent",
"protocol" : "SASLSSL",
"password" : "ConfluentCloudPassword",
"topic" : "topic",
"authenticationMode" : "PLAIN",
"avroSchema" : "{\"type\":\"record\",\"name\":\"Payment\",\"namespace\":\"io.confluent.examples.clients.basicavro\",\"fields\":[{\"name\":\"id\",\"type\":\"string\"},{\"name\":\"amount\",\"type\":\"double\"},{\"name\":\"type\",\"type\":\"string\"}]}",
"consumerGroup" : "$Default",
"username" : "ConfluentCloudUsername",
"brokerList" : "%BrokerList%"
} ]
}
```


The following code runs when the function is triggered:

```
using namespace System.Net
param($kafkaEvent, $TriggerMetadata)
Write-Output "Powershell Kafka trigger function called for message $kafkaEvent.Value"
```


For a complete set of working PowerShell examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/powershell/).

The usage of the trigger depends on your version of the Python programming model.

In the Python v2 model, you define your trigger directly in your function code using decorators. For more information, see the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

These examples show how to define a Kafka trigger for a function that reads a Kafka message.

```
@KafkaTrigger.function_name(name="KafkaTrigger")
@KafkaTrigger.kafka_trigger(
arg_name="kevent",
topic="KafkaTopic",
broker_list="KafkaBrokerList",
username="KafkaUsername",
password="KafkaPassword",
protocol="SaslSsl",
authentication_mode="Plain",
consumer_group="$Default1")
def kafka_trigger(kevent : func.KafkaEvent):
logging.info(kevent.get_body().decode('utf-8'))
logging.info(kevent.metadata)
```


This example receives events in a batch by setting the `cardinality`

value to `many`

.

```
@KafkaTrigger.function_name(name="KafkaTriggerMany")
@KafkaTrigger.kafka_trigger(
arg_name="kevents",
topic="KafkaTopic",
broker_list="KafkaBrokerList",
username="KafkaUsername",
password="KafkaPassword",
protocol="SaslSsl",
authentication_mode="Plain",
cardinality="MANY",
data_type="string",
consumer_group="$Default2")
def kafka_trigger_many(kevents : typing.List[func.KafkaEvent]):
for event in kevents:
logging.info(event.get_body())
```


You can define a generic [Avro schema](http://avro.apache.org/docs/current/) for the event passed to the trigger.

```
@KafkaTriggerAvro.function_name(name="KafkaTriggerAvroOne")
@KafkaTriggerAvro.kafka_trigger(
arg_name="kafkaTriggerAvroGeneric",
topic="KafkaTopic",
broker_list="KafkaBrokerList",
username="KafkaUsername",
password="KafkaPassword",
protocol="SaslSsl",
authentication_mode="Plain",
consumer_group="$Default",
avro_schema= "{\"type\":\"record\",\"name\":\"Payment\",\"namespace\":\"io.confluent.examples.clients.basicavro\",\"fields\":[{\"name\":\"id\",\"type\":\"string\"},{\"name\":\"amount\",\"type\":\"double\"},{\"name\":\"type\",\"type\":\"string\"}]}")
def kafka_trigger_avro_one(kafkaTriggerAvroGeneric : func.KafkaEvent):
logging.info(kafkaTriggerAvroGeneric.get_body().decode('utf-8'))
logging.info(kafkaTriggerAvroGeneric.metadata)
```


For a complete set of working Python examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/python-v2/).

The annotations you use to configure your trigger depend on the specific event provider.

The following example shows a Java function that reads and logs the content of the Kafka event:

```
@FunctionName("KafkaTrigger")
public void runSingle(
@KafkaTrigger(
name = "KafkaTrigger",
topic = "topic",
brokerList="%BrokerList%",
consumerGroup="$Default",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
protocol = BrokerProtocol.SASLSSL,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
dataType = "string"
) String kafkaEventData,
final ExecutionContext context) {
context.getLogger().info(kafkaEventData);
}
```


To receive events in a batch, use an input string as an array, as shown in the following example:

```
@FunctionName("KafkaTriggerMany")
public void runMany(
@KafkaTrigger(
name = "kafkaTriggerMany",
topic = "topic",
brokerList="%BrokerList%",
consumerGroup="$Default",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
protocol = BrokerProtocol.SASLSSL,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
cardinality = Cardinality.MANY,
dataType = "string"
) String[] kafkaEvents,
final ExecutionContext context) {
for (String kevent: kafkaEvents) {
context.getLogger().info(kevent);
}
}
```


The following function logs the message and headers for the Kafka Event:

```
@FunctionName("KafkaTriggerManyWithHeaders")
public void runSingle(
@KafkaTrigger(
name = "KafkaTrigger",
topic = "topic",
brokerList="%BrokerList%",
consumerGroup="$Default",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
protocol = BrokerProtocol.SASLSSL,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
dataType = "string",
cardinality = Cardinality.MANY
) List<String> kafkaEvents,
final ExecutionContext context) {
Gson gson = new Gson();
for (String keventstr: kafkaEvents) {
KafkaEntity kevent = gson.fromJson(keventstr, KafkaEntity.class);
context.getLogger().info("Java Kafka trigger function called for message: " + kevent.Value);
context.getLogger().info("Headers for the message:");
for (KafkaHeaders header : kevent.Headers) {
String decodedValue = new String(Base64.getDecoder().decode(header.Value));
context.getLogger().info("Key:" + header.Key + " Value:" + decodedValue);
}
}
}
```


You can define a generic [Avro schema](http://avro.apache.org/docs/current/) for the event passed to the trigger. The following function defines a trigger for the specific provider with a generic Avro schema:

```
private static final String schema = "{\"type\":\"record\",\"name\":\"Payment\",\"namespace\":\"io.confluent.examples.clients.basicavro\",\"fields\":[{\"name\":\"id\",\"type\":\"string\"},{\"name\":\"amount\",\"type\":\"double\"},{\"name\":\"type\",\"type\":\"string\"}]}";
@FunctionName("KafkaAvroGenericTrigger")
public void runOne(
@KafkaTrigger(
name = "kafkaAvroGenericSingle",
topic = "topic",
brokerList="%BrokerList%",
consumerGroup="$Default",
username = "ConfluentCloudUsername",
password = "ConfluentCloudPassword",
avroSchema = schema,
authenticationMode = BrokerAuthenticationMode.PLAIN,
protocol = BrokerProtocol.SASLSSL) Payment payment,
final ExecutionContext context) {
context.getLogger().info(payment.toString());
}
```


For a complete set of working Java examples for Confluent, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/java/confluent/src/main/java/com/contoso/kafka).

## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the `KafkaTriggerAttribute`

to define the function trigger.

The following table explains the properties you can set by using this trigger attribute:

| Parameter | Description |
|---|---|
BrokerList |
(Required) The list of Kafka brokers monitored by the trigger. See
|

**Topic****ConsumerGroup****AvroSchema****KeyAvroSchema****KeyDataType**`KeyAvroSchema`

is set, this value is generic record. Accepted values are `Int`

, `Long`

, `String`

, and `Binary`

.**AuthenticationMode**`NotSet`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

, and `OAuthBearer`

.**Username**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**Password**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**Protocol**`NotSet`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**SslCaLocation****SslCertificateLocation****SslKeyLocation****SslKeyPassword****SslCertificatePEM**[Connections](#connections)for more information.**SslKeyPEM**[Connections](#connections)for more information.**SslCaPEM**[Connections](#connections)for more information.**SslCertificateandKeyPEM**[Connections](#connections)for more information.**SchemaRegistryUrl**[Connections](#connections)for more information.**SchemaRegistryUsername**[Connections](#connections)for more information.**SchemaRegistryPassword**[Connections](#connections)for more information.**OAuthBearerMethod**`oidc`

and `default`

.**OAuthBearerClientId**`OAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client ID. See [Connections](#connections)for more information.**OAuthBearerClientSecret**`OAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client secret. See [Connections](#connections)for more information.**OAuthBearerScope****OAuthBearerTokenEndpointUrl**`oidc`

method is used. See [Connections](#connections)for more information.**OAuthBearerExtensions**`oidc`

method is used. For example: `supportFeatureX=true,organizationId=sales-emea`

.## Annotations

The `KafkaTrigger`

annotation enables you to create a function that runs when it receives a topic. Supported options include the following elements:

| Element | Description |
|---|---|
name |
(Required) The name of the variable that represents the queue or topic message in function code. |
brokerList |
(Required) The list of Kafka brokers monitored by the trigger. See
|

**topic****cardinality**`ONE`

(default) and `MANY`

. Use `ONE`

when the input is a single message and `MANY`

when the input is an array of messages. When you use `MANY`

, you must also set a `dataType`

.**dataType**`string`

, the input is treated as just a string. When `binary`

, the message is received as binary data, and Functions tries to deserialize it to an actual parameter type byte[].**consumerGroup****avroSchema****authenticationMode**`NotSet`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

.**username**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**password**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**protocol**`NotSet`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****lagThreshold****schemaRegistryUrl**[Connections](#connections)for more information.**schemaRegistryUsername**[Connections](#connections)for more information.**schemaRegistryPassword**[Connections](#connections)for more information.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

function.json property |
Description |
|---|---|
type |
(Required) Set to `kafkaTrigger` . |
direction |
(Required) Set to `in` . |
name |
(Required) The name of the variable that represents the brokered data in function code. |
brokerList |
(Required) The list of Kafka brokers monitored by the trigger. See
|

**topic****cardinality**`ONE`

(default) and `MANY`

. Use `ONE`

when the input is a single message and `MANY`

when the input is an array of messages. When you use `MANY`

, you must also set a `dataType`

.**dataType**`string`

, the input is treated as just a string. When `binary`

, the message is received as binary data, and Functions tries to deserialize it to an actual byte array parameter type.**consumerGroup****avroSchema****keyAvroSchema****keyDataType**`keyAvroSchema`

is set, this value is generic record. Accepted values are `Int`

, `Long`

, `String`

, and `Binary`

.**authenticationMode**`NotSet`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

.**username**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**password**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**protocol**`NotSet`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****sslCertificatePEM**[Connections](#connections)for more information.**sslKeyPEM**[Connections](#connections)for more information.**sslCaPEM**[Connections](#connections)for more information.**sslCertificateandKeyPEM**[Connections](#connections)for more information.**lagThreshold****schemaRegistryUrl**[Connections](#connections)for more information.**schemaRegistryUsername**[Connections](#connections)for more information.**schemaRegistryPassword**[Connections](#connections)for more information.**oAuthBearerMethod**`oidc`

and `default`

.**oAuthBearerClientId**`oAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client ID. See [Connections](#connections)for more information.**oAuthBearerClientSecret**`oAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client secret. See [Connections](#connections)for more information.**oAuthBearerScope****oAuthBearerTokenEndpointUrl**`oidc`

method is used. See [Connections](#connections)for more information.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file. Python uses snake_case naming conventions for configuration properties.

function.json property |
Description |
|---|---|
type |
(Required) Set to `kafkaTrigger` . |
direction |
(Required) Set to `in` . |
name |
(Required) The name of the variable that represents the brokered data in function code. |
broker_list |
(Required) The list of Kafka brokers monitored by the trigger. See
|

**topic****cardinality**`ONE`

(default) and `MANY`

. Use `ONE`

when the input is a single message and `MANY`

when the input is an array of messages. When you use `MANY`

, you must also set a `data_type`

.**data_type**`string`

, the input is treated as just a string. When `binary`

, the message is received as binary data, and Functions tries to deserialize it to an actual parameter type byte[].**consumerGroup****avroSchema****authentication_mode**`NOTSET`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

.**username**`authentication_mode`

is `Gssapi`

. See [Connections](#connections)for more information.**password**`authentication_mode`

is `Gssapi`

. See [Connections](#connections)for more information.**protocol**`NOTSET`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****lag_threshold****schema_registry_url**[Connections](#connections)for more information.**schema_registry_username**[Connections](#connections)for more information.**schema_registry_password**[Connections](#connections)for more information.**o_auth_bearer_method**`oidc`

and `default`

.**o_auth_bearer_client_id**`o_auth_bearer_method`

is set to `oidc`

, this specifies the OAuth bearer client ID. See [Connections](#connections)for more information.**o_auth_bearer_client_secret**`o_auth_bearer_method`

is set to `oidc`

, this specifies the OAuth bearer client secret. See [Connections](#connections)for more information.**o_auth_bearer_scope****o_auth_bearer_token_endpoint_url**`oidc`

method is used. See [Connections](#connections)for more information.Note

Certificate PEM-related properties and Avro key-related properties aren't yet available in the Python library.

## Usage

The Kafka trigger currently supports Kafka events as strings and string arrays that are JSON payloads.

The Kafka trigger passes Kafka messages to the function as strings. The trigger also supports string arrays that are JSON payloads.

In a Premium plan, you must enable runtime scale monitoring for the Kafka output to scale out to multiple instances. To learn more, see [Enable runtime scaling](functions-bindings-kafka#enable-runtime-scaling).

You can't use the **Test/Run** feature of the **Code + Test** page in the Azure portal to work with Kafka triggers. You must instead send test events directly to the topic being monitored by the trigger.

For a complete set of supported host.json settings for the Kafka trigger, see [host.json settings](functions-bindings-kafka#hostjson-settings).

## Connections

Store all connection information required by your triggers and bindings in application settings, not in the binding definitions in your code. This guidance applies to credentials, which you should never store in your code.

Important

Credential settings must reference an [application setting](functions-how-to-use-azure-function-app-settings#settings). Don't hard-code credentials in your code or configuration files. When running locally, use the [local.settings.json file](functions-develop-local#local-settings-file) for your credentials, and don't publish the local.settings.json file.

When connecting to a managed Kafka cluster provided by [Confluent in Azure](https://www.confluent.io/azure/), you can use one of the following authentication methods.

Note

When using the Flex Consumption plan, file location-based certificate authentication properties (`SslCaLocation`

, `SslCertificateLocation`

, `SslKeyLocation`

) aren't supported. Instead, use the PEM-based certificate properties (`SslCaPEM`

, `SslCertificatePEM`

, `SslKeyPEM`

, `SslCertificateandKeyPEM`

) or store certificates in Azure Key Vault.

#### Schema Registry

To make use of schema registry provided by Confluent in Kafka Extension, set the following credentials:

| Setting | Recommended Value | Description |
|---|---|---|
SchemaRegistryUrl |
`SchemaRegistryUrl` |
URL of the schema registry service used for schema management. Usually of the format `https://psrc-xyz.us-east-2.aws.confluent.cloud` |
SchemaRegistryUsername |
`CONFLUENT_API_KEY` |
Username for basic auth on schema registry (if required). |
SchemaRegistryPassword |
`CONFLUENT_API_SECRET` |
Password for basic auth on schema registry (if required). |

#### Username/Password authentication

While using this form of authentication, make sure that `Protocol`

is set to either `SaslPlaintext`

or `SaslSsl`

, `AuthenticationMode`

is set to `Plain`

, `ScramSha256`

or `ScramSha512`

and, if the CA cert being used is different from the default ISRG Root X1 cert, make sure to update `SslCaLocation`

or `SslCaPEM`

.

| Setting | Recommended value | Description |
|---|---|---|
BrokerList |
`BootstrapServer` |
App setting named `BootstrapServer` contains the value of bootstrap server found in Confluent Cloud settings page. The value resembles `xyz-xyzxzy.westeurope.azure.confluent.cloud:9092` . |
Username |
`ConfluentCloudUsername` |
App setting named `ConfluentCloudUsername` contains the API access key from the Confluent Cloud web site. |
Password |
`ConfluentCloudPassword` |
App setting named `ConfluentCloudPassword` contains the API secret obtained from the Confluent Cloud web site. |
SslCaPEM |
`SSLCaPemCertificate` |
App setting named `SSLCaPemCertificate` that contains the CA certificate as a string in PEM format. The value should follow the standard format, for example: `-----BEGIN CERTIFICATE-----\nMII....JQ==\n-----END CERTIFICATE-----` . |

#### SSL authentication

Ensure that `Protocol`

is set to `SSL`

.

| Setting | Recommended Value | Description |
|---|---|---|
BrokerList |
`BootstrapServer` |
App setting named `BootstrapServer` contains the value of bootstrap server found in Confluent Cloud settings page. The value resembles `xyz-xyzxzy.westeurope.azure.confluent.cloud:9092` . |
SslCaPEM |
`SslCaCertificatePem` |
App setting named `SslCaCertificatePem` that contains PEM value of the CA certificate as a string. The value should follow the standard format: `-----BEGIN CERTIFICATE-----\nMII...JQ==\n-----END CERTIFICATE-----` |
SslCertificatePEM |
`SslClientCertificatePem` |
App setting named `SslClientCertificatePem` that contains PEM value of the client certificate as a string. The value should follow the standard format: `-----BEGIN CERTIFICATE-----\nMII...JQ==\n-----END CERTIFICATE-----` |
SslKeyPEM |
`SslClientKeyPem` |
App setting named `SslClientKeyPem` that contains PEM value of the client private key as a string. The value should follow the standard format: `-----BEGIN PRIVATE KEY-----\nMII...JQ==\n-----END PRIVATE KEY-----` |
SslCertificateandKeyPEM |
`SslClientCertificateAndKeyPem` |
App setting named `SslClientCertificateAndKeyPem` that contains PEM value of the client certificate and client private key concatenated as a string. The value should follow the standard format: `-----BEGIN CERTIFICATE-----\nMII....JQ==\n-----END CERTIFICATE-----\n-----BEGIN PRIVATE KEY-----\nMIIE....BM=\n-----END PRIVATE KEY-----` |
SslKeyPassword |
`SslClientKeyPassword` |
App setting named `SslClientKeyPassword` that contains the password for the private key (if any). |

#### OAuth authentication

When using OAuth authentication, configure the OAuth-related properties in your binding definitions.

The string values you use for these settings must be present as [application settings in Azure](functions-how-to-use-azure-function-app-settings#settings) or in the `Values`

collection in the [local.settings.json file](functions-develop-local#local-settings-file) during local development.

You should also set the `Protocol`

and `AuthenticationMode`

in your binding definitions.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-app-settings -->

# App settings reference for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Application settings in a function app contain configuration options that affect all functions for that function app. These settings are accessed as environment variables. This article lists the app settings that are available in function apps.

There are several ways that you can add, update, and delete function app settings:

Changes to function app settings require your function app to be restarted.

In this article, example connection string values are truncated for readability.

Azure Functions uses the Azure App Service platform for hosting. You might find some settings relevant to hosting your function app in [Environment variables and app settings in Azure App Service](../app-service/reference-app-settings).

## App setting considerations

When you use app settings, you should be aware of the following considerations:

Changing application settings causes your function app to restart by default across all hosting plans. For zero-downtime deployments when changing settings, use the

[Flex Consumption plan](flex-consumption-plan)with[rolling updates as the site update strategy](flex-consumption-site-updates). For other hosting plans, see[optimize deployments](functions-best-practices#optimize-deployments)for guidance on minimizing downtime.In setting names, double-underscore (

`__`

) and colon (`:`

) are considered reserved values. Double-underscores are interpreted as hierarchical delimiters on both Windows and Linux. Colons are interpreted in the same way only on Windows. For example, the setting`AzureFunctionsWebHost__hostid=somehost_123456`

would be interpreted as the following JSON object:`"AzureFunctionsWebHost": { "hostid": "somehost_123456" }`

In this article, only double-underscores are used, since they're supported on both operating systems. Most of the settings that support managed identity connections use double-underscores.

When functions runs locally, app settings are specified in the

`Values`

collection in the[local.settings.json](functions-develop-local#local-settings-file).There are other function app configuration options in the

[host.json](functions-host-json)file and in the[local.settings.json](functions-develop-local#local-settings-file)file.You can use application settings to override host.json setting values without having to change the host.json file itself. This approach is helpful for scenarios where you need to configure or modify specific host.json settings for a specific environment. This approach also lets you change host.json settings without having to republish your project. To learn more, see the

[host.json reference article](functions-host-json#override-hostjson-values).This article documents the settings that are most relevant to your function apps. Because Azure Functions runs on App Service, other application settings are also supported. For more information, see

[Environment variables and app settings in Azure App Service](../app-service/reference-app-settings).Some scenarios also require you to work with settings documented in

[App Service site settings](#app-service-site-settings).Changing any

*read-only*[App Service application settings](../app-service/reference-app-settings#app-environment)can put your function app into an unresponsive state.Take care when updating application settings by using REST APIs, including ARM templates. Because these APIs replace the existing application settings, you must include all existing settings when adding or modifying settings using REST APIs or ARM templates. When possible, use Azure CLI or Azure PowerShell to programmatically work with application settings. For more information, see

[Work with application settings](functions-how-to-use-azure-function-app-settings#settings).

## APPINSIGHTS_INSTRUMENTATIONKEY

The instrumentation key for Application Insights. Don't use both `APPINSIGHTS_INSTRUMENTATIONKEY`

and `APPLICATIONINSIGHTS_CONNECTION_STRING`

. When possible, use `APPLICATIONINSIGHTS_CONNECTION_STRING`

. When Application Insights runs in a sovereign cloud, you must use `APPLICATIONINSIGHTS_CONNECTION_STRING`

. For more information, see [How to configure monitoring for Azure Functions](configure-monitoring).

| Key | Sample value |
|---|---|
| APPINSIGHTS_INSTRUMENTATIONKEY | `55555555-af77-484b-9032-64f83bb83bb` |

Don't use both `APPINSIGHTS_INSTRUMENTATIONKEY`

and `APPLICATIONINSIGHTS_CONNECTION_STRING`

. We recommend that you use `APPLICATIONINSIGHTS_CONNECTION_STRING`

.

## APPLICATIONINSIGHTS_AUTHENTICATION_STRING

Enables access to Application Insights by using Microsoft Entra authentication. Use this setting when you must connect to your Application Insights workspace by using Microsoft Entra authentication. For more information, see [Microsoft Entra authentication for Application Insights](/en-us/azure/azure-monitor/app/azure-ad-authentication).

When you use `APPLICATIONINSIGHTS_AUTHENTICATION_STRING`

, the specific value that you set depends on the type of managed identity:

| Managed identity | Setting value |
|---|---|
| System-assigned | `Authorization=AAD` |
| User-assigned | `Authorization=AAD;ClientId=<USER_ASSIGNED_CLIENT_ID>` |

This authentication requirement is applied to connections from the Functions host, snapshot debugger, profiler, and any language-specific agents. To use this setting, the managed identity must already be available to the function app, with an assigned role equivalent to [Monitoring Metrics Publisher](/en-us/azure/role-based-access-control/built-in-roles/monitor#monitoring-metrics-publisher).

Note

When using `APPLICATIONINSIGHTS_AUTHENTICATION_STRING`

to connect to Application Insights using Microsoft Entra authentication, you should also [Disable local authentication for Application Insights](/en-us/azure/azure-monitor/app/azure-ad-authentication#disable-local-authentication). This configuration requires Microsoft Entra authentication in order for telemetry to be ingested into your workspace.

## APPLICATIONINSIGHTS_CONNECTION_STRING

The connection string for Application Insights. Don't use both `APPINSIGHTS_INSTRUMENTATIONKEY`

and `APPLICATIONINSIGHTS_CONNECTION_STRING`

. We recommend the use of `APPLICATIONINSIGHTS_CONNECTION_STRING`

in all cases. It's a requirement in the following cases:

- When your function app requires the added customizations supported by using the connection string
- When your Application Insights instance runs in a sovereign cloud, which requires a custom endpoint

For more information, see [Connection strings](/en-us/azure/azure-monitor/app/sdk-connection-string).

| Key | Sample value |
|---|---|
| APPLICATIONINSIGHTS_CONNECTION_STRING | `InstrumentationKey=...` |

To connect to Application Insights with Microsoft Entra authentication, you should use [ APPLICATIONINSIGHTS_AUTHENTICATION_STRING](#applicationinsights_authentication_string).

## AZURE_FUNCTION_PROXY_DISABLE_LOCAL_CALL

Important

Azure Functions proxies was a feature of [versions 1.x through 3.x](functions-versions) of the Azure Functions runtime. For more information, see [Functions proxies](functions-proxies).

## AZURE_FUNCTION_PROXY_BACKEND_URL_DECODE_SLASHES

Important

Azure Functions proxies was a feature of [versions 1.x through 3.x](functions-versions) of the Azure Functions runtime. For more information, see [Functions proxies](functions-proxies).

## AZURE_FUNCTIONS_ENVIRONMENT

Configures the runtime [hosting environment](/en-us/dotnet/api/microsoft.extensions.hosting.environments) of the function app when running in Azure. This value is read during initialization. The runtime accepts only these values:

| Value | Description |
|---|---|
`Production` |
Represents a production environment, with reduced logging and full performance optimizations. This value is the default when `AZURE_FUNCTIONS_ENVIRONMENT` either isn't set or is set to an unsupported value. |
`Staging` |
Represents a staging environment, such as when running in a
|

`Development`

`AZURE_FUNCTIONS_ENVIRONMENT`

to `Development`

when running on your local computer. This setting can't be overridden in the local.settings.json file.Use this setting instead of `ASPNETCORE_ENVIRONMENT`

when you need to change the runtime environment in Azure to something other than `Production`

. For more information, see [Environment-based Startup class and methods](/en-us/aspnet/core/fundamentals/environments#environments).

This setting isn't available in version 1.x of the Functions runtime.

## AzureFunctionsJobHost__*

In version 2.x and later versions of the Functions runtime, application settings can override [host.json](functions-host-json) settings in the current environment. These overrides are expressed as application settings named `AzureFunctionsJobHost__path__to__setting`

. For more information, see [Override host.json values](functions-host-json#override-hostjson-values).

## AzureFunctionsWebHost__hostid

Sets the host ID for a given function app, which should be a unique ID. This setting overrides the automatically generated host ID value for your app. Use this setting only when you need to prevent host ID collisions between function apps that share the same storage account.

A host ID must meet the following requirements:

- Be between 1 and 32 characters
- Contain only lowercase letters, numbers, and dashes
- Not start or end with a dash
- Not contain consecutive dashes

An easy way to generate an ID is to take a GUID, remove the dashes, and make it lower case, such as by converting the GUID `1835D7B5-5C98-4790-815D-072CC94C6F71`

to the value `1835d7b55c984790815d072cc94c6f71`

.

| Key | Sample value |
|---|---|
| AzureFunctionsWebHost__hostid | `myuniquefunctionappname123456789` |

For more information, see [Host ID considerations](storage-considerations#host-id-considerations).

## AzureWebJobsDashboard

*This setting is deprecated and is only supported when running on version 1.x of the Azure Functions runtime.*

Optional storage account connection string for storing logs and displaying them in the **Monitor** tab in the Azure portal. The storage account must be a general-purpose one that supports blobs, queues, and tables. To learn more, see [Storage account requirements](storage-considerations#storage-account-requirements).

| Key | Sample value |
|---|---|
| AzureWebJobsDashboard | `DefaultEndpointsProtocol=https;AccountName=...` |

## AzureWebJobsDisableHomepage

A value of `true`

disables the default landing page that is shown for the root URL of a function app. The default value is `false`

.

| Key | Sample value |
|---|---|
| AzureWebJobsDisableHomepage | `true` |

When this app setting is omitted or set to `false`

, a page similar to the following example is displayed in response to the URL `<functionappname>.azurewebsites.net`

.


## AzureWebJobsDotNetReleaseCompilation

`true`

means use `Release`

mode when compiling .NET code. `false`

means use Debug mode. Default is `true`

.

| Key | Sample value |
|---|---|
| AzureWebJobsDotNetReleaseCompilation | `true` |

## AzureWebJobsFeatureFlags

A comma-delimited list of beta features to enable. Beta features enabled by these flags aren't production ready, but can be enabled for experimental use before they go live.

| Key | Sample value |
|---|---|
| AzureWebJobsFeatureFlags | `feature1,feature2,EnableProxies` |

If your app currently has this setting, add new flags to the end of the comma-delineated list.

Currently supported feature flags:

| Flag value | Description |
|---|---|
`EnableProxies` |
Re-enables proxies on version 4.x of the Functions runtime while you plan your migration to Azure API Management. For more information, see
|

`EnableAzureMonitorTimeIsoFormat`

`ISO 8601`

time format in Azure Monitor logs for Linux apps running on a Dedicated (App Service) plan.## AzureWebJobsKubernetesSecretName

Indicates the Kubernetes Secrets resource used for storing keys. Supported only when running in Kubernetes.

| Key | Sample value |
|---|---|
| AzureWebJobsKubernetesSecretName | `<SECRETS_RESOURCE>` |

Considerations when you use a Kubernetes Secrets resource:

- You must also set
`AzureWebJobsSecretStorageType`

to`kubernetes`

. When`AzureWebJobsKubernetesSecretName`

isn't set, the repository is considered read only. In this case, the values must be generated before deployment. - The
[Azure Functions Core Tools](functions-run-local)generates the values automatically when deploying to Kubernetes. [Immutable secrets](https://kubernetes.io/docs/concepts/configuration/secret/#secret-immutable)aren't supported and using them results in runtime errors.

To learn more, see [Manage key storage](function-keys-how-to#manage-key-storage).

## AzureWebJobsSecretStorageKeyVaultClientId

The client ID of the user-assigned managed identity or the app registration used to access the vault where keys are stored. This setting requires you to set `AzureWebJobsSecretStorageType`

to `keyvault`

. Supported in version 4.x and later versions of the Functions runtime.

| Key | Sample value |
|---|---|
| AzureWebJobsSecretStorageKeyVaultClientId | `<CLIENT_ID>` |

To learn more, see [Manage key storage](function-keys-how-to#manage-key-storage).

## AzureWebJobsSecretStorageKeyVaultClientSecret

The secret for client ID of the user-assigned managed identity or the app registration used to access the vault where keys are stored. This setting requires you to set `AzureWebJobsSecretStorageType`

to `keyvault`

. Supported in version 4.x and later versions of the Functions runtime.

| Key | Sample value |
|---|---|
| AzureWebJobsSecretStorageKeyVaultClientSecret | `<CLIENT_SECRET>` |

To learn more, see [Manage key storage](function-keys-how-to#manage-key-storage).

## AzureWebJobsSecretStorageKeyVaultName

*This setting is deprecated and was only used when running on version 3.x of the Azure Functions runtime.*

The name of a key vault instance used to store keys. This setting was only used in version 3.x of the Functions runtime, which is no longer supported. For version 4.x, instead use `AzureWebJobsSecretStorageKeyVaultUri`

. This setting requires you to set `AzureWebJobsSecretStorageType`

to `keyvault`

.

The vault must have an access policy corresponding to the system-assigned managed identity of the hosting resource. The access policy should grant the identity the following secret permissions: `Get`

,`Set`

, `List`

, and `Delete`

.

When your functions run locally, the developer identity is used. Settings must be in the [local.settings.json file](functions-develop-local#local-settings-file).

| Key | Sample value |
|---|---|
| AzureWebJobsSecretStorageKeyVaultName | `<VAULT_NAME>` |

To learn more, see [Manage key storage](function-keys-how-to#manage-key-storage).

## AzureWebJobsSecretStorageKeyVaultTenantId

The tenant ID of the app registration used to access the vault where keys are stored. This setting requires you to set `AzureWebJobsSecretStorageType`

to `keyvault`

. Supported in version 4.x and later versions of the Functions runtime. To learn more, see [Manage key storage](function-keys-how-to#manage-key-storage).

| Key | Sample value |
|---|---|
| AzureWebJobsSecretStorageKeyVaultTenantId | `<TENANT_ID>` |

## AzureWebJobsSecretStorageKeyVaultUri

The URI of a key vault instance used to store keys. Supported in version 4.x and later versions of the Functions runtime. We recommend this setting for using a key vault instance for key storage. This setting requires you to set `AzureWebJobsSecretStorageType`

to `keyvault`

.

The `AzureWebJobsSecretStorageKeyVaultUri`

value should be the full value of **Vault URI** displayed in the **Key Vault overview** tab, including `https://`

.

The vault must have an access policy corresponding to the system-assigned managed identity of the hosting resource. The access policy should grant the identity the following secret permissions: `Get`

,`Set`

, `List`

, and `Delete`

.

When your functions run locally, the developer identity is used, and settings must be in the [local.settings.json file](functions-develop-local#local-settings-file).

| Key | Sample value |
|---|---|
| AzureWebJobsSecretStorageKeyVaultUri | `https://<VAULT_NAME>.vault.azure.net` |

Important

Secrets aren't scoped to individual function apps through the `AzureWebJobsSecretStorageKeyVaultUri`

setting. If multiple function apps are configured to use the same Key Vault they share the same secrets, potentially leading to key collisions or overwrites. To avoid unintended behavior, we recommend that you use a separate Key Vault instance for each function app.

To learn more, see [Manage Key Storage](function-keys-how-to#manage-key-storage).

## AzureWebJobsSecretStorageSas

A Blob Storage SAS URL for a second storage account used for key storage. By default, Functions uses the account set in `AzureWebJobsStorage`

. When using this secret storage option, make sure that `AzureWebJobsSecretStorageType`

isn't explicitly set or is set to `blob`

. To learn more, see [Manage key storage](function-keys-how-to#manage-key-storage).

| Key | Sample value |
|---|---|
| AzureWebJobsSecretStorageSas | `<BLOB_SAS_URL>` |

## AzureWebJobsSecretStorageType

Specifies the repository or provider to use for key storage. Keys are always encrypted before being stored using a secret unique to your function app.

| Key | Value | Description |
|---|---|---|
| AzureWebJobsSecretStorageType | `blob` |
Keys are stored in a Blob storage container in the account provided by the `AzureWebJobsStorage` setting. Blob storage is the default behavior when `AzureWebJobsSecretStorageType` isn't set.To specify a different storage account, use the `AzureWebJobsSecretStorageSas` setting to indicate the SAS URL of a second storage account. |
| AzureWebJobsSecretStorageType | `files` |
Keys are persisted on the file system. This behavior is the default for Functions v1.x. |
| AzureWebJobsSecretStorageType | `keyvault` |
Keys are stored in a key vault instance set by `AzureWebJobsSecretStorageKeyVaultName` . |
| AzureWebJobsSecretStorageType | `kubernetes` |
Supported only when running the Functions runtime in Kubernetes. When `AzureWebJobsKubernetesSecretName` isn't set, the repository is considered read only. In this case, the values must be generated before deployment. The
|

To learn more, see [Manage key storage](function-keys-how-to#manage-key-storage).

## AzureWebJobsStorage

Specifies the connection string for an Azure Storage account that the Functions runtime uses for normal operations. Some uses of this storage account by Functions include key management, timer trigger management, and Event Hubs checkpoints. The storage account must be a general-purpose one that supports blobs, queues, and tables. For more information, see [Storage account requirements](storage-considerations#storage-account-requirements).

| Key | Sample value |
|---|---|
| AzureWebJobsStorage | `DefaultEndpointsProtocol=https;AccountName=...` |

Instead of a connection string, you can use an identity-based connection for this storage account. For more information, see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity).

## AzureWebJobsStorage__accountName

When using an identity-based storage connection, sets the account name of the storage account instead of using the connection string in `AzureWebJobsStorage`

. This syntax is unique to `AzureWebJobsStorage`

and can't be used for other identity-based connections.

| Key | Sample value |
|---|---|
| AzureWebJobsStorage__accountName | `<STORAGE_ACCOUNT_NAME>` |

For sovereign clouds or when using a custom DNS, you must instead use the service-specific `AzureWebJobsStorage__*ServiceUri`

settings.

## AzureWebJobsStorage__blobServiceUri

When using an identity-based storage connection, sets the data plane URI of the blob service of the storage account.

| Key | Sample value |
|---|---|
| AzureWebJobsStorage__blobServiceUri | `https://<STORAGE_ACCOUNT_NAME>.blob.core.windows.net` |

Use this setting instead of `AzureWebJobsStorage__accountName`

in sovereign clouds or when using a custom DNS. For more information, see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity).

## AzureWebJobsStorage__clientId

Sets the client ID of a specific user-assigned identity used to obtain an access token for managed identity authentication. Requires that `AzureWebJobsStorage__credential`

be set to `managedidentity`

. The value is a client ID that corresponds to an identity assigned to the application. You can't set both `AzureWebJobsStorage__managedIdentityResourceId`

and `AzureWebJobsStorage__clientId`

. When not set, the system-assigned identity is used.

## AzureWebJobsStorage__credential

Defines how an access token is obtained for the connection. Use `managedidentity`

for managed identity authentication. When using `managedidentity`

, a managed identity must be available in the hosting environment. Don't set `AzureWebJobsStorage__credential`

in local development scenarios.

## AzureWebJobsStorage__managedIdentityResourceId

Sets the resource identifier of a user-assigned identity used to obtain an access token for managed identity authentication. Requires that `AzureWebJobsStorage__credential`

be set to `managedidentity`

. The value is the resource ID of an identity assigned to the application used for managed identity authentication. You can't set both `AzureWebJobsStorage__managedIdentityResourceId`

and `AzureWebJobsStorage__clientId`

. When not set, the system-assigned identity is used.

## AzureWebJobsStorage__queueServiceUri

When using an identity-based storage connection, sets the data plane URI of the queue service of the storage account.

| Key | Sample value |
|---|---|
| AzureWebJobsStorage__queueServiceUri | `https://<STORAGE_ACCOUNT_NAME>.queue.core.windows.net` |

Use this setting instead of `AzureWebJobsStorage__accountName`

in sovereign clouds or when using a custom DNS. For more information, see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity).

## AzureWebJobsStorage__tableServiceUri

When using an identity-based storage connection, sets data plane URI of a table service of the storage account.

| Key | Sample value |
|---|---|
| AzureWebJobsStorage__tableServiceUri | `https://<STORAGE_ACCOUNT_NAME>.table.core.windows.net` |

Use this setting instead of `AzureWebJobsStorage__accountName`

in sovereign clouds or when using a custom DNS. For more information, see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity).

## AzureWebJobs_TypeScriptPath

Path to the compiler used for TypeScript. Allows you to override the default if you need to.

| Key | Sample value |
|---|---|
| AzureWebJobs_TypeScriptPath | `%HOME%\typescript` |

## DOCKER_REGISTRY_SERVER_PASSWORD

Indicates the password used to access a private container registry. This setting is only required when deploying your containerized function app from a private container registry. For more information, see [Environment variables and app settings in Azure App Service](../app-service/reference-app-settings#custom-containers).

## DOCKER_REGISTRY_SERVER_URL

Indicates the URL of a private container registry. This setting is only required when deploying your containerized function app from a private container registry. For more information, see [Environment variables and app settings in Azure App Service](../app-service/reference-app-settings#custom-containers).

## DOCKER_REGISTRY_SERVER_USERNAME

Indicates the account used to access a private container registry. This setting is only required when deploying your containerized function app from a private container registry. For more information, see [Environment variables and app settings in Azure App Service](../app-service/reference-app-settings#custom-containers).

## DOCKER_SHM_SIZE

Sets the shared memory size (in bytes) when the Python worker is using shared memory. To learn more, see [Shared memory](https://github.com/Azure/azure-functions-python-worker/wiki/Shared-Memory).

| Key | Sample value |
|---|---|
| DOCKER_SHM_SIZE | `268435456` |

The preceding value sets a shared memory size of ~256 MB.

Requires that [FUNCTIONS_WORKER_SHARED_MEMORY_DATA_TRANSFER_ENABLED](#functions_worker_shared_memory_data_transfer_enabled) is set to `1`

.

## ENABLE_ORYX_BUILD

Indicates whether the [Oryx build system](https://github.com/microsoft/Oryx) is used during deployment. `ENABLE_ORYX_BUILD`

must be set to `true`

when doing remote build deployments to Linux. For more information, see [Remote build](functions-deployment-technologies#remote-build).

| Key | Sample value |
|---|---|
| ENABLE_ORYX_BUILD | `true` |

## FUNCTION_APP_EDIT_MODE

Indicates whether you can edit your function app in the Azure portal. Valid values are `readwrite`

and `readonly`

.

| Key | Sample value |
|---|---|
| FUNCTION_APP_EDIT_MODE | `readonly` |

The runtime sets the value based on the language stack and deployment status of your function app. For more information, see [Development limitations in the Azure portal](functions-how-to-use-azure-function-app-settings#development-limitations-in-the-azure-portal).

## FUNCTIONS_EXTENSION_VERSION

The version of the Functions runtime that hosts your function app. A tilde (`~`

) with major version means use the latest version of that major version, for example, `~4`

. When new minor versions of the same major version are available, they're automatically installed in the function app.

| Key | Sample value |
|---|---|
| FUNCTIONS_EXTENSION_VERSION | `~4` |

The following major runtime version values are supported:

| Value | Runtime target | Comment |
|---|---|---|
`~4` |
4.x | Recommended |
`~1` |
1.x | Support ends September 14, 2026 |

A value of `~4`

means that your app runs on version 4.x of the runtime. A value of `~1`

pins your app to version 1.x of the runtime. Runtime versions 2.x and 3.x are no longer supported. For more information, see [Azure Functions runtime versions overview](functions-versions).

If requested by support to pin your app to a specific minor version, use the full version number, for example, `4.0.12345`

. For more information, see [How to target Azure Functions runtime versions](set-runtime-version).

## FUNCTIONS_INPROC_NET8_ENABLED

Indicates whether to an app can use .NET 8 on the in-process model. To use .NET 8 on the in-process model, this value must be set to `1`

. See [Updating to target .NET 8](functions-dotnet-class-library#updating-to-target-net-8) for complete instructions, including other required configuration values.

| Key | Sample value |
|---|---|
| FUNCTIONS_INPROC_NET8_ENABLED | `1` |

Set to `0`

to disable support for .NET 8 on the in-process model.

## FUNCTIONS_NODE_BLOCK_ON_ENTRY_POINT_ERROR

This app setting is a temporary way for Node.js apps to enable a breaking change that makes entry point errors easier to troubleshoot on Node.js v18 or lower. We highly recommend using `true`

, especially for programming model v4 apps, which always use entry point files. The behavior without the breaking change (`false`

) ignores entry point errors and doesn't log them in Application Insights.

Starting with Node.js v20, the app setting has no effect and the breaking change behavior is always enabled.

For Node.js v18 or lower, the app setting is used, and the default behavior depends on if the error happens before or after a model v4 function has been registered:

- If the error is thrown before, the default behavior matches
`false`

. For example, if you're using model v3 or your entry point file doesn't exist. - If the error is thrown after, the default behavior matches
`true`

. For example, if you try to register duplicate model v4 functions.

| Key | Value | Description |
|---|---|---|
| FUNCTIONS_NODE_BLOCK_ON_ENTRY_POINT_ERROR | `true` |
Block on entry point errors and log them in Application Insights. |
| FUNCTIONS_NODE_BLOCK_ON_ENTRY_POINT_ERROR | `false` |
Ignore entry point errors and don't log them in Application Insights. |

## FUNCTIONS_REQUEST_BODY_SIZE_LIMIT

Overrides the default limit on the body size of requests sent to HTTP endpoints. The value is given in bytes, with a default maximum request size of 104,857,600 bytes.

| Key | Sample value |
|---|---|
| FUNCTIONS_REQUEST_BODY_SIZE_LIMIT | `250000000` |

## FUNCTIONS_V2_COMPATIBILITY_MODE

Important

This setting is no longer supported. It was originally provided to enable a short-term workaround for apps that targeted the v2.x runtime. They would be able to instead run on the v3.x runtime while it was still supported. Except for legacy apps that run on version 1.x, all function apps must run on version 4.x of the Functions runtime: `FUNCTIONS_EXTENSION_VERSION=~4`

. For more information, see [Azure Functions runtime versions overview](functions-versions).

## FUNCTIONS_WORKER_PROCESS_COUNT

Specifies the maximum number of language worker processes, with a default value of `1`

. The maximum value allowed is `10`

. Function invocations are evenly distributed among language worker processes. Language worker processes are spawned every 10 seconds until the count set by `FUNCTIONS_WORKER_PROCESS_COUNT`

is reached. Using multiple language worker processes isn't the same as [scaling](functions-scale). Consider using this setting when your workload has a mix of CPU-bound and I/O-bound invocations. This setting applies to all language runtimes, except for .NET running in process (`FUNCTIONS_WORKER_RUNTIME=dotnet`

).

| Key | Sample value |
|---|---|
| FUNCTIONS_WORKER_PROCESS_COUNT | `2` |

## FUNCTIONS_WORKER_RUNTIME

The language or language stack of the worker runtime to load in the function app. This value corresponds to the language being used in your application, for example, `python`

. Starting with version 2.x of the Azure Functions runtime, a given function app can only support a single language.

| Key | Sample value |
|---|---|
| FUNCTIONS_WORKER_RUNTIME | `node` |

Valid values:

| Value | Language/language stack |
|---|---|
`dotnet` |
|

`dotnet-isolated`

[C# (isolated worker process)](dotnet-isolated-process-guide)`java`

[Java](functions-reference-java)`node`

[JavaScript](functions-reference-node?tabs=javascript)[TypeScript](functions-reference-node?tabs=typescript)`powershell`

[PowerShell](functions-reference-powershell)`python`

[Python](functions-reference-python)`custom`

[Other](functions-custom-handlers)## FUNCTIONS_WORKER_SHARED_MEMORY_DATA_TRANSFER_ENABLED

This setting enables the Python worker to use shared memory to improve throughput. Enable shared memory when your Python function app is hitting memory bottlenecks.

| Key | Sample value |
|---|---|
| FUNCTIONS_WORKER_SHARED_MEMORY_DATA_TRANSFER_ENABLED | `1` |

With this setting enabled, you can use the [DOCKER_SHM_SIZE](#docker_shm_size) setting to set the shared memory size. To learn more, see [Shared memory](https://github.com/Azure/azure-functions-python-worker/wiki/Shared-Memory).

## JAVA_APPLICATIONINSIGHTS_ENABLE_TELEMETRY

Indicates whether the Java worker process should output telemetry in an Open Telemetry format to the Application Insights endpoint. Setting this flag to `True`

tells the Functions host to let the Java worker process stream OpenTelemetry logs directly, which prevents duplicate host-level entries. For more information, see [Configure application settings](opentelemetry-howto?pivots=programming-language-java#configure-application-settings).

## JAVA_ENABLE_SDK_TYPES

Enables your function app to use native Azure SDK types in bindings.

Note

Support for binding to SDK types is currently in preview and limited to the Azure Blob Storage SDK. For more information, see [SDK types](functions-reference-java#sdk-types) in the Java reference article.

| Key | Sample value |
|---|---|
| JAVA_ENABLE_SDK_TYPES | `true` |

For more information, see [SDK types](functions-reference-java#sdk-types) in the Java reference article.

## JAVA_OPTS

Used to customize the Java virtual machine (JVM) used to run your Java functions when running on a [Premium plan](functions-premium-plan) or [Dedicated plan](dedicated-plan). When running on a Consumption plan, instead use `languageWorkers__java__arguments`

. For more information, see [Customize JVM](functions-reference-java#customize-jvm).

## languageWorkers__java__arguments

Used to customize the Java virtual machine (JVM) used to run your Java functions when running on a [Consumption plan](functions-premium-plan). This setting does increase the cold start times for Java functions running in a Consumption plan. For a Premium or Dedicated plan, instead use `JAVA_OPTS`

. For more information, see [Customize JVM](functions-reference-java#customize-jvm).

## MDMaxBackgroundUpgradePeriod

Controls the managed dependencies background update period for PowerShell function apps, with a default value of `7.00:00:00`

(weekly).

Each PowerShell worker process initiates checking for module upgrades on the PowerShell Gallery on process start and every `MDMaxBackgroundUpgradePeriod`

after the start. When a new module version is available in the PowerShell Gallery, it's installed to the file system and made available to PowerShell workers. Decreasing this value lets your function app get newer module versions sooner, but it also increases the app resource usage, including network I/O, CPU, and storage. Increasing this value decreases the app's resource usage, but it can also delay delivering new module versions to your app.

| Key | Sample value |
|---|---|
| MDMaxBackgroundUpgradePeriod | `7.00:00:00` |

To learn more, see [Dependency management](functions-reference-powershell#dependency-management).

## MDNewSnapshotCheckPeriod

Specifies how often each PowerShell worker checks whether managed dependency upgrades are installed. The default frequency is `01:00:00`

(hourly).

After new module versions are installed to the file system, every PowerShell worker process must be restarted. Restarting PowerShell workers affects your app availability because it can interrupt current function execution. Until all PowerShell worker processes are restarted, function invocations can use either the old or the new module versions. Restarting all PowerShell workers completes within `MDNewSnapshotCheckPeriod`

.

Within every `MDNewSnapshotCheckPeriod`

, the PowerShell worker checks whether or not managed dependency upgrades are installed. When upgrades are installed, a restart is initiated. Increasing this value decreases the frequency of interruptions because of restarts. However, the increase might also increase the time during which function invocations could use either the old or the new module versions, nondeterministically.

| Key | Sample value |
|---|---|
| MDNewSnapshotCheckPeriod | `01:00:00` |

To learn more, see [Dependency management](functions-reference-powershell#dependency-management).

## MDMinBackgroundUpgradePeriod

The period of time after a previous managed dependency upgrade check before another upgrade check is started, with a default of `1.00:00:00`

(daily).

To avoid excessive module upgrades on frequent Worker restarts, checking for module upgrades isn't performed when any worker already initiated that check in the last `MDMinBackgroundUpgradePeriod`

.

| Key | Sample value |
|---|---|
| MDMinBackgroundUpgradePeriod | `1.00:00:00` |

To learn more, see [Dependency management](functions-reference-powershell#dependency-management).

## OTEL_EXPORTER_OTLP_ENDPOINT

Indicates the URL to which OpenTelemetry-formatted data is exported for ingestion. For more information, see [Use OpenTelemetry with Azure Functions](opentelemetry-howto).

## OTEL_EXPORTER_OTLP_HEADERS

Sets an optional list of headers that are applied to all outgoing data exported to an OpenTelemetry endpoint. You should use this setting when the OpenTelemetry endpoint requires to supply an API key. For more information, see [Use OpenTelemetry with Azure Functions](opentelemetry-howto).

## PIP_INDEX_URL

Overrides the default base URL of the Python Package Index (`https://pypi.org/simple`

) when running a remote build. Because this setting replaces the package index, you might see unexpected behaviour on restore. Only use this setting when you need to use a complete set of custom dependencies. When possible, you should instead use `PIP_EXTRA_URL`

, which lets you reference an additional package index. For more information, see [Custom dependencies](python-build-options#custom-dependencies) in the Python build article.

| Key | Sample value |
|---|---|
| PIP_INDEX_URL | `http://my.custom.package.repo/simple` |

These custom dependencies can be in a package index repository compliant with PEP 503 (the simple repository API) or in a local directory that follows the same format. For more information, see [ pip documentation for --index-url](https://pip.pypa.io/en/stable/cli/pip_wheel/?highlight=index%20url#cmdoption-i).


## PIP_EXTRA_INDEX_URL

The value for this setting indicates an extra index URL for custom packages for Python apps, to use in addition to the `--index-url`

. Use this setting when you need to run a remote build using custom dependencies that are found in an extra package index. For more information, see [Custom dependencies](python-build-options#custom-dependencies) in the Python build article.

| Key | Sample value |
|---|---|
| PIP_EXTRA_INDEX_URL | `http://my.custom.package.repo/simple` |

Should follow the same rules as `--index-url`

. For more information, see [ pip documentation for --extra-index-url](https://pip.pypa.io/en/stable/cli/pip_wheel/?highlight=index%20url#cmdoption-extra-index-url).


## PROJECT

A [continuous deployment](functions-continuous-deployment) setting that tells the Kudu deployment service the folder in a connected repository to location the deployable project.

| Key | Sample value |
|---|---|
| PROJECT | `WebProject/WebProject.csproj` |

## PYTHON_APPLICATIONINSIGHTS_ENABLE_TELEMETRY

Indicates whether the Python worker process should output telemetry in an Open Telemetry format to the Application Insights endpoint. Setting this flag to `True`

tells the Functions host to let the Python worker process export OpenTelemetry data to [Application Insights endpoint](#applicationinsights_connection_string). For more information, see [Configure application settings](opentelemetry-howto?pivots=programming-language-python#configure-application-settings).

## PYTHON_ISOLATE_WORKER_DEPENDENCIES

The configuration is specific to Python function apps. It defines the prioritization of module loading order. By default, this value is set to `0`

.

| Key | Value | Description |
|---|---|---|
| PYTHON_ISOLATE_WORKER_DEPENDENCIES | `0` |
Prioritize loading the Python libraries from internal Python worker's dependencies, which is the default behavior. Non-Microsoft libraries defined in requirements.txt might be shadowed. |
| PYTHON_ISOLATE_WORKER_DEPENDENCIES | `1` |
Prioritize loading the Python libraries from application's package defined in requirements.txt. This value prevents your libraries from colliding with internal Python worker's libraries. |

## PYTHON_ENABLE_DEBUG_LOGGING

Enables debug-level logging in a Python function app. A value of `1`

enables debug-level logging. Without this setting or with a value of `0`

, only information and higher-level logs are sent from the Python worker to the Functions host. Use this setting when debugging or tracing your Python function executions.

When debugging Python functions, make sure to also set a debug or trace [logging level](functions-host-json#logging) in the host.json file, as needed. To learn more, see [How to configure monitoring for Azure Functions](configure-monitoring).

## PYTHON_ENABLE_OPENTELEMETRY

Indicates whether the Python worker process should export telemetry to an Open Telemetry endpoint. Setting this flag to `True`

tells the Functions host to let the Python worker process export OpenTelemetry data to the configured [OTEL_EXPORTER_OTLP_ENDPOINT](#otel_exporter_otlp_endpoint). For more information, see [Configure application settings](opentelemetry-howto?pivots=programming-language-python#configure-application-settings).

## PYTHON_ENABLE_WORKER_EXTENSIONS

The configuration is specific to Python function apps. Setting this value to `1`

allows the worker to load in [Python worker extensions](develop-python-worker-extensions) defined in requirements.txt. It enables your function app to access new features provided by partner packages. It can also change the behavior of function load and invocation in your app. Ensure the extension you choose is trustworthy as you bear the risk of using it. Azure Functions gives no express warranties to any extensions. For how to use an extension, visit the extension's manual page or readme doc. By default, this value sets to `0`

.

| Key | Value | Description |
|---|---|---|
| PYTHON_ENABLE_WORKER_EXTENSIONS | `0` |
Disable any Python worker extension. |
| PYTHON_ENABLE_WORKER_EXTENSIONS | `1` |
Allow Python worker to load extensions from requirements.txt. |

## PYTHON_THREADPOOL_THREAD_COUNT

Specifies the maximum number of threads that a Python language worker would use to run function invocations, with a default value of `1`

for Python version `3.8`

and below. For Python version `3.9`

and above, the value is set to `None`

. This setting doesn't guarantee the number of threads that would be set during executions. The setting allows Python to expand the number of threads to the specified value. The setting only applies to Python functions apps. Additionally, the setting applies to synchronous functions invocation and not for coroutines.

| Key | Sample value | Max value |
|---|---|---|
| PYTHON_THREADPOOL_THREAD_COUNT | 2 | 32 |

## SCALE_CONTROLLER_LOGGING_ENABLED

*This setting is currently in preview.*

This setting controls logging from the Azure Functions scale controller. For more information, see [Scale controller logs](functions-monitoring#scale-controller-logs).

| Key | Sample value |
|---|---|
| SCALE_CONTROLLER_LOGGING_ENABLED | `AppInsights:Verbose` |

The value for this key is supplied in the format `<DESTINATION>:<VERBOSITY>`

, which is defined as follows:

| Property | Description |
|---|---|
`<DESTINATION>` |
The destination to which logs are sent. Valid values are `AppInsights` and `Blob` .When you use `AppInsights` , ensure that the
When you set the destination to `Blob` , logs are created in a blob container named `azure-functions-scale-controller` in the default storage account set in the `AzureWebJobsStorage` application setting. |
`<VERBOSITY>` |
Specifies the level of logging. Supported values are `None` , `Warning` , and `Verbose` .When set to `Verbose` , the scale controller logs a reason for every change in the worker count, and information about the triggers that factor into those decisions. Verbose logs include trigger warnings and the hashes used by the triggers before and after the scale controller runs. |

Tip

Keep in mind that while you leave scale controller logging enabled, it impacts the [potential costs of monitoring your function app](functions-monitoring#application-insights-pricing-and-limits). Consider enabling logging until you collect enough data to understand how the scale controller is behaving, and then disabling it.

## SCM_DO_BUILD_DURING_DEPLOYMENT

Controls remote build behavior during deployment. When `SCM_DO_BUILD_DURING_DEPLOYMENT`

is set to `true`

, the project is built remotely during deployment.

| Key | Sample value |
|---|---|
| SCM_DO_BUILD_DURING_DEPLOYMENT | `true` |

## SCM_LOGSTREAM_TIMEOUT

Controls the timeout, in seconds, when connected to streaming logs. The default value is 7200 (2 hours).

| Key | Sample value |
|---|---|
| SCM_LOGSTREAM_TIMEOUT | `1800` |

The preceding sample value of `1800`

sets a timeout of 30 minutes. For more information, see [Enable streaming execution logs in Azure Functions](streaming-logs).

## WEBSITE_CONTENTAZUREFILECONNECTIONSTRING

Connection string for storage account where the function app code and configuration are stored in event-driven scaling plans. For more information, see [Storage account connection setting](storage-considerations#storage-account-connection-setting).

| Key | Sample value |
|---|---|
| WEBSITE_CONTENTAZUREFILECONNECTIONSTRING | `DefaultEndpointsProtocol=https;AccountName=...` |

This setting is required for both Consumption and Elastic Premium plan apps. It's not required for Dedicated plan apps, which Functions doesn't dynamically scale.

The Flex Consumption plan is now the recommended serverless hosting plan for Azure Functions. It offers faster scaling, reduced cold starts, private networking, and more control over performance and cost. For more information, see [Flex Consumption plan](flex-consumption-plan).

Changing or removing this setting can cause your function app to not start. To learn more, see [this troubleshooting article](functions-recover-storage-account#storage-account-application-settings-were-deleted).

Azure Files doesn't currently support using managed identity when accessing the file share. For more information, see [Azure Files supported authentication scenarios](../storage/files/storage-files-active-directory-overview#supported-authentication-scenarios).

You might use a [KeyVault reference](../app-service/app-service-key-vault-references) for this connection setting. However, additional configuration is required to create and dynamically scale a function app in a Premium or Consumption plan when the storage connection string is maintained in a KeyVault. For more information, see [Considerations for Azure Files mounting](../app-service/app-service-key-vault-references#considerations-for-azure-files-mounting).

## WEBSITE_CONTENTOVERVNET

Important

WEBSITE_CONTENTOVERVNET is a legacy app setting that has been replaced by the [vnetContentShareEnabled](#vnetcontentshareenabled) site property.

A value of `1`

enables your function app to scale across stamps when you have your storage account restricted to a virtual network. You should enable this setting when restricting your storage account to a virtual network. Only required when using `WEBSITE_CONTENTSHARE`

and `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

. To learn more, see [Restrict your storage account to a virtual network](configure-networking-how-to#restrict-your-storage-account-to-a-virtual-network).

| Key | Sample value |
|---|---|
| WEBSITE_CONTENTOVERVNET | `1` |

This app setting is required for cross-stamp scaling on the [Elastic Premium](functions-premium-plan) and [Dedicated (App Service) plans](dedicated-plan) (Standard and higher) when the storage account is VNet-restricted. Without this setting, the function app can only scale within a single stamp (approximately 1-20 instances). Not supported when running on a [Consumption plan](consumption-plan).

Note

You must take special care when routing to the content share in a storage account shared by multiple function apps in the same plan. For more information, see [Consistent routing through virtual networks](storage-considerations#consistent-routing-through-virtual-networks) in the Storage considerations article.

## WEBSITE_CONTENTSHARE

The name of the file share that Functions uses to store function app code and configuration files. This content is required by event-driven scaling plans. Used with `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

. Default is a unique string generated by the runtime, which begins with the function app name. For more information, see [Storage account connection setting](storage-considerations#storage-account-connection-setting).

| Key | Sample value |
|---|---|
| WEBSITE_CONTENTSHARE | `functionapp091999e2` |

This setting is required only for Consumption and Premium plan apps. It's not required for Dedicated plan apps, which aren't dynamically scaled by Functions.

The Flex Consumption plan is now the recommended serverless hosting plan for Azure Functions. It offers faster scaling, reduced cold starts, private networking, and more control over performance and cost. For more information, see [Flex Consumption plan](flex-consumption-plan).

The share is created when your function app is created. Changing or removing this setting can cause your function app to not start. To learn more, see [this troubleshooting article](functions-recover-storage-account#storage-account-application-settings-were-deleted).

The following considerations apply when using an Azure Resource Manager (ARM) template or Bicep file to create a function app during deployment:

- When you don't set a
`WEBSITE_CONTENTSHARE`

value for the main function app or any apps in slots, unique share values are generated for you. Not setting`WEBSITE_CONTENTSHARE`

*is the recommended approach*for an ARM template deployment. - There are scenarios where you must set the
`WEBSITE_CONTENTSHARE`

value to a predefined value, such as when you[use a secured storage account in a virtual network](configure-networking-how-to#restrict-your-storage-account-to-a-virtual-network). In this case, you must set a unique share name for the main function app and the app for each deployment slot. For a storage account secured by a virtual network, you must also create the share itself as part of your automated deployment. For more information, see[Secured deployments](functions-infrastructure-as-code#secured-deployments). - Don't make
`WEBSITE_CONTENTSHARE`

a slot setting. - When you specify
`WEBSITE_CONTENTSHARE`

, the value must follow[this guidance for share names](/en-us/rest/api/storageservices/naming-and-referencing-shares--directories--files--and-metadata#share-names).

## WEBSITE_DNS_SERVER

Sets the DNS server used by an app when resolving IP addresses. This setting is often required when using certain networking functionality, such as [Azure DNS private zones](functions-networking-options#azure-dns-private-zones) and [private endpoints](functions-networking-options#restrict-your-storage-account-to-a-virtual-network).

| Key | Sample value |
|---|---|
| WEBSITE_DNS_SERVER | `168.63.129.16` |

## WEBSITE_ENABLE_BROTLI_ENCODING

Controls whether Brotli encoding is used for compression instead of the default gzip compression. When `WEBSITE_ENABLE_BROTLI_ENCODING`

is set to `1`

, Brotli encoding is used. Otherwise, gzip encoding is used.

## WEBSITE_FUNCTIONS_ARMCACHE_ENABLED

Disables caching when deploying function apps using Azure Resource Manager (ARM) templates.

| Key | Sample value |
|---|---|
| WEBSITE_FUNCTIONS_ARMCACHE_ENABLED | 0 |

## WEBSITE_MAX_DYNAMIC_APPLICATION_SCALE_OUT

The maximum number of instances that the app can scale out to. Default is no limit.

Important

This setting is in preview. An [app property for function max scale out](event-driven-scaling#limit-scale-out) now exists. We recommend this property to limit scale-out.

| Key | Sample value |
|---|---|
| WEBSITE_MAX_DYNAMIC_APPLICATION_SCALE_OUT | `5` |

## WEBSITE_NODE_DEFAULT_VERSION

*Windows only.*
Sets the version of Node.js to use when running your function app on Windows. You should use a tilde (`~`

) to have the runtime use the latest available version of the targeted major version. For example, when set to `~18`

, the latest version of Node.js 18 is used. When a major version is targeted with a tilde, you don't have to manually update the minor version.

| Key | Sample value |
|---|---|
| WEBSITE_NODE_DEFAULT_VERSION | `~18` |

## WEBSITE_OVERRIDE_STICKY_DIAGNOSTICS_SETTINGS

When you perform [a slot swap](functions-deployment-slots#swap-slots) on a function app running on a Premium plan, the swap can fail when the dedicated storage account used by the app is network restricted. This failure is caused by a legacy [application logging feature](../app-service/troubleshoot-diagnostic-logs#enable-application-logging-windows), which both Functions and App Service share. This setting overrides that legacy logging feature and allows the swap to occur.

| Key | Sample value |
|---|---|
| WEBSITE_OVERRIDE_STICKY_DIAGNOSTICS_SETTINGS | `0` |

Add `WEBSITE_OVERRIDE_STICKY_DIAGNOSTICS_SETTINGS`

with a value of `0`

to all slots to make sure that legacy diagnostic settings don't block your swaps. You can also add this setting and value to just the production slot as a [deployment slot ( sticky) setting](functions-deployment-slots#create-a-deployment-setting).

## WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS

By default, the version settings for function apps are specific to each slot. This setting is used when upgrading functions by using [deployment slots](functions-deployment-slots). This approach prevents unanticipated behavior due to changing versions after a swap. Set to `0`

in production and in the slot to make sure that all version settings are also swapped. For more information, see [Upgrade using slots](migrate-version-3-version-4#update-using-slots).

| Key | Sample value |
|---|---|
| WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS | `0` |

## WEBSITE_RUN_FROM_PACKAGE

Enables your function app to run from a package file, which can be locally mounted or deployed to an external URL.

| Key | Sample value |
|---|---|
| WEBSITE_RUN_FROM_PACKAGE | `1` |

Valid values are either a URL that resolves to the location of an external deployment package file, or `1`

. When set to `1`

, the package must be in the `d:\home\data\SitePackages`

folder. When you use zip deployment with `WEBSITE_RUN_FROM_PACKAGE`

enabled, the package is automatically uploaded to this location. For more information, see [Run your functions from a package file](run-functions-from-deployment-package).

When you use `WEBSITE_RUN_FROM_PACKAGE=<URL>`

, the URL must resolve to the package file location in an accessible storage location, such as an Azure Blob Storage container. The container must be private to prevent unauthorized access, which requires you to use either a shared access signature (SAS) in the URL or Microsoft Entra ID authentication to allow access. Using Microsoft Entra ID with managed identities is recommended.

This is an example of setting `WEBSITE_RUN_FROM_PACKAGE`

to the URL of a deployment package in an Azure Blog Storage container:

`WEBSITE_RUN_FROM_PACKAGE=https://contosostorageaccount.blob.core.windows.net/mycontainer/mypackage.zip`


When using SAS, you append the token to the URL as a query parameter.

When you [deploy a package from Azure Blob Storage using a user-assigned managed identity](run-functions-from-deployment-package#fetch-a-package-from-azure-blob-storage-using-a-managed-identity), you must also set [ WEBSITE_RUN_FROM_PACKAGE_BLOB_MI_RESOURCE_ID](#website_run_from_package_blob_mi_resource_id) to the resource ID of the user-assigned managed identity. When you deploy from an external package URL, you must also manually sync triggers. For more information, see

[Trigger syncing](functions-deployment-technologies#trigger-syncing).

## WEBSITE_RUN_FROM_PACKAGE_BLOB_MI_RESOURCE_ID

Indicates the resource ID of a user-assigned managed identity that's used when accessing a deployment package from an external Azure Blob Storage container secured using Microsoft Entra ID. This setting requires that [ WEBSITE_RUN_FROM_PACKAGE](#website_run_from_package) be set to the URL of the deployment package in a private container.

Setting `WEBSITE_RUN_FROM_PACKAGE_BLOB_MI_RESOURCE_ID=SystemAssigned`

is the same as omitting the setting, in which case the system-assigned managed identity for the app is used.

## WEBSITE_SKIP_CONTENTSHARE_VALIDATION

The [WEBSITE_CONTENTAZUREFILECONNECTIONSTRING](#website_contentazurefileconnectionstring) and [WEBSITE_CONTENTSHARE](#website_contentshare) settings have extra validation checks to ensure that the app can be properly started. Creation of application settings fail when the function app can't properly call out to the downstream Storage Account or Key Vault due to networking constraints or other limiting factors. When WEBSITE_SKIP_CONTENTSHARE_VALIDATION is set to `1`

, the validation check is skipped. Otherwise, the value defaults to `0`

and the validation takes place.

| Key | Sample value |
|---|---|
| WEBSITE_SKIP_CONTENTSHARE_VALIDATION | `1` |

If validation is skipped and either the connection string or content share isn't valid, the app isn't able to start properly. In this case, functions return HTTP 500 errors. For more information, see [Troubleshoot error: "Azure Functions Runtime is unreachable"](functions-recover-storage-account).

## WEBSITE_SLOT_NAME

Read-only. Name of the current deployment slot. The name of the production slot is `Production`

.

| Key | Sample value |
|---|---|
| WEBSITE_SLOT_NAME | `Production` |

## WEBSITE_TIME_ZONE

Allows you to set the timezone for your function app.

| Key | OS | Sample value |
|---|---|---|
| WEBSITE_TIME_ZONE | Windows | `Eastern Standard Time` |
| WEBSITE_TIME_ZONE | Linux | `America/New_York` |

The default time zone used with the CRON expressions is Coordinated Universal Time (UTC). To have your CRON expression based on another time zone, create an app setting for your function app named `WEBSITE_TIME_ZONE`

.

The value of this setting depends on the operating system and plan on which your function app runs.

| Operating system | Plan | Value |
|---|---|---|
Windows |
All | Set the value to the name of the desired time zone as given by the second line from each pair given by the Windows command `tzutil.exe /L` |
Linux |
Premium Dedicated |
Set the value to the name of the desired time zone as shown in the
|

Note

`WEBSITE_TIME_ZONE`

and `TZ`

aren't currently supported when running on Linux in a [Flex Consumption](flex-consumption-plan) or [Consumption](consumption-plan) plan. In this case, the setting `WEBSITE_TIME_ZONE`

or `TZ`

can create SSL-related issues and cause metrics to stop working for your app.

For example, Eastern Time in the US (represented by `Eastern Standard Time`

(Windows) or `America/New_York`

(Linux)) currently uses UTC-05:00 during standard time and UTC-04:00 during daylight time. To have a timer trigger fire at 10:00 AM Eastern Time every day, create an app setting for your function app named `WEBSITE_TIME_ZONE`

, set the value to `Eastern Standard Time`

(Windows) or `America/New_York`

(Linux), and then use the following NCRONTAB expression:

```
"0 0 10 * * *"
```


When you use `WEBSITE_TIME_ZONE`

, the time is adjusted for time changes in the specific timezone, including daylight saving time and changes in standard time.

## WEBSITE_USE_PLACEHOLDER

Indicates whether to use a specific [cold start](event-driven-scaling#cold-start) optimization when running on the [Consumption plan](consumption-plan). Set to `0`

to disable the cold-start optimization on the Consumption plan.

| Key | Sample value |
|---|---|
| WEBSITE_USE_PLACEHOLDER | `1` |

## WEBSITE_USE_PLACEHOLDER_DOTNETISOLATED

Indicates whether to use a specific [cold start](event-driven-scaling#cold-start) optimization when running .NET isolated worker process functions on the [Consumption plan](consumption-plan). Set to `0`

to disable the cold-start optimization on the Consumption plan.

| Key | Sample value |
|---|---|
| WEBSITE_USE_PLACEHOLDER_DOTNETISOLATED | `1` |

## WEBSITE_VNET_ROUTE_ALL

Important

WEBSITE_VNET_ROUTE_ALL is a legacy app setting that has been replaced by the [vnetRouteAllEnabled](#vnetrouteallenabled) site setting.

Indicates whether all outbound traffic from the app is routed through the virtual network. A setting value of `1`

indicates that all application traffic is routed through the virtual network. You need this setting when configuring [Regional virtual network integration](functions-networking-options#regional-virtual-network-integration) in the Elastic Premium and Dedicated hosting plans. It's also used when a [virtual network NAT gateway is used to define a static outbound IP address](functions-how-to-use-nat-gateway).

| Key | Sample value |
|---|---|
| WEBSITE_VNET_ROUTE_ALL | `1` |

## WEBSITES_ENABLE_APP_SERVICE_STORAGE

Indicates whether the `/home`

directory is shared across scaled instances, with a default value of `true`

. You should set this value to `false`

when deploying your function app in a container.

## App Service site settings

Some configurations must be maintained at the App Service level as site settings, such as language versions. These settings are managed in the Azure portal, by using REST APIs, or by using Azure CLI or Azure PowerShell. The following are site settings that could be required, depending on your runtime language, OS, and versions.

## AcrUseManagedIdentityCreds

Indicates whether the image is obtained from an Azure Container Registry instance using managed identity authentication. A value of `true`

requires that you use managed identity. We recommend this approach over stored authentication credentials as a security best practice.

## AcrUserManagedIdentityID

Indicates the managed identity to use when obtaining the image from an Azure Container Registry instance. Requires that `AcrUseManagedIdentityCreds`

is set to `true`

. These values are valid:

| Value | Description |
|---|---|
`system` |
The system assigned managed identity of the function app is used. |
`<USER_IDENTITY_RESOURCE_ID>` |
The fully qualified resource ID of a user-assigned managed identity. |

The identity that you specify must be added to the `ACRPull`

role in the container registry. For more information, see [Create and configure a function app on Azure with the image](functions-deploy-container-apps?tabs=acr#create-and-configure-a-function-app-on-azure-with-the-image).

## alwaysOn

On a function app running in a [Dedicated (App Service) plan](dedicated-plan), the Functions runtime goes idle after a few minutes of inactivity, a which point only requests to an HTTP trigger *wakes up* your function app. To make sure that your non-HTTP triggered functions run correctly, including Timer trigger functions, enable Always On for the function app by setting the `alwaysOn`

site setting to a value of `true`

.

## functionsRuntimeAdminIsolationEnabled

Determines whether the built-in administrator (`/admin`

) endpoints in your function app can be accessed. When set to `false`

(the default), the app allows requests to endpoints under `/admin`

when those requests present a [master key](function-keys-how-to#understand-keys) in the request. When `true`

, `/admin`

endpoints can't be accessed, even with a master key.

This property can't be set for apps running on Linux in a Consumption plan. It can't be set for apps running on version 1.x of Azure Functions. If you're using version 1.x, you must first [migrate to version 4.x](migrate-version-1-version-4).

## linuxFxVersion

For function apps running on Linux, `linuxFxVersion`

indicates the language and version for the language-specific worker process. This information is used, along with [ FUNCTIONS_EXTENSION_VERSION](#functions_extension_version), to determine which specific Linux container image is installed to run your function app. This setting can be set to a predefined value or a custom image URI.

This value is set for you when you create your Linux function app. You might need to set it for ARM template and Bicep deployments and in certain upgrade scenarios.

### Valid linuxFxVersion values

You can use the following Azure CLI command to see a table of current `linuxFxVersion`

values, by supported Functions runtime version:

```
az functionapp list-runtimes --os linux --query "[].{stack:join(' ', [runtime, version]), LinuxFxVersion:linux_fx_version, SupportedFunctionsVersions:to_string(supported_functions_versions[])}" --output table
```


The previous command requires you to upgrade to version 2.40 of the Azure CLI.

### Custom images

When you create and maintain your own custom Linux container for your function app, the `linuxFxVersion`

value is instead in the format `DOCKER|<IMAGE_URI>`

, as in the following example:

```
linuxFxVersion = "DOCKER|contoso.com/azurefunctionsimage:v1.0.0"
```


This example indicates the registry source of the deployed container. For more information, see [Working with containers and Azure Functions](functions-how-to-custom-container).

Important

When you create your own containers, you're required to keep the base image of your container updated to the latest supported base image. Supported base images for Azure Functions are language-specific. See the [Azure Functions base image repos](https://mcr.microsoft.com/catalog?search=functions).

The Functions team is committed to publishing monthly updates for these base images. Regular updates include the latest minor version updates and security fixes for both the Functions runtime and languages. You should regularly update your container from the latest base image and redeploy the updated version of your container. For more information, see [Maintaining custom containers](container-concepts#maintaining-custom-containers).

## netFrameworkVersion

Sets the specific version of .NET for C# functions. For more information, see [Update your function app in Azure](migrate-version-3-version-4?pivots=programming-language-csharp#update-your-function-app-in-azure).

## powerShellVersion

Sets the specific version of PowerShell on which your functions run. For more information, see [Changing the PowerShell version](functions-reference-powershell#changing-the-powershell-version).

When running locally, you instead use the [ FUNCTIONS_WORKER_RUNTIME_VERSION](functions-reference-powershell#running-local-on-a-specific-version) setting in the local.settings.json file.

## vnetContentShareEnabled

Apps running in a Premium plan use a file share to store content. The name of this content share is stored in the [ WEBSITE_CONTENTSHARE](#website_contentshare) app setting and its connection string is stored in

[. To route traffic between your function app and content share through a virtual network, you must also set](#website_contentazurefileconnectionstring)

`WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

`vnetContentShareEnabled`

to `true`

. Enabling this site property is required for cross-stamp scaling when [restricting your storage account to a virtual network](configure-networking-how-to#restrict-your-storage-account-to-a-virtual-network)in the Elastic Premium and Dedicated hosting plans. Without this setting, the function app can only scale within a single stamp (approximately 1-20 instances).

Note

You must take special care when routing to the content share in a storage account shared by multiple function apps in the same plan. For more information, see [Consistent routing through virtual networks](storage-considerations#consistent-routing-through-virtual-networks) in the Storage considerations article.

This site property replaces the legacy [ WEBSITE_CONTENTOVERVNET](#website_contentovervnet) setting.

## vnetImagePullEnabled

Functions [supports function apps running in Linux containers](functions-how-to-custom-container). To connect and pull from a container registry inside a virtual network, you must set `vnetImagePullEnabled`

to `true`

. This site property is supported in the Elastic Premium and Dedicated hosting plans. The Flex Consumption plan doesn't rely on site properties or app settings to configure Networking. For more information, see [Flex Consumption plan deprecations](#flex-consumption-plan-deprecations).

## vnetRouteAllEnabled

Indicates whether all outbound traffic from the app is routed through the virtual network. A setting value of `true`

indicates that all application traffic is routed through the virtual network. Use this setting when configuring [Regional virtual network integration](functions-networking-options#regional-virtual-network-integration) in the Elastic Premium and Dedicated plans. It's also used when a [virtual network NAT gateway is used to define a static outbound IP address](functions-how-to-use-nat-gateway). For more information, see [Configure application routing](../app-service/configure-vnet-integration-routing#configure-application-routing).

This site setting replaces the legacy [WEBSITE_VNET_ROUTE_ALL](#website_vnet_route_all) setting.

## Flex Consumption plan deprecations

In the [Flex Consumption plan](flex-consumption-plan), these site properties and application settings are deprecated and shouldn't be used when creating function app resources:

| Setting/property | Reason |
|---|---|
`ENABLE_ORYX_BUILD` |
Replaced by the `remoteBuild` parameter when deploying in Flex Consumption |
`FUNCTIONS_EXTENSION_VERSION` |
App Setting is set by the backend. A value of ~1 can be ignored. |
`FUNCTIONS_WORKER_RUNTIME` |
Replaced by `name` in `properties.functionAppConfig.runtime` |
`FUNCTIONS_WORKER_RUNTIME_VERSION` |
Replaced by `version` in `properties.functionAppConfig.runtime` |
`FUNCTIONS_MAX_HTTP_CONCURRENCY` |
Replaced by scale and concurrency's trigger section |
`FUNCTIONS_WORKER_PROCESS_COUNT` |
Setting not valid |
`FUNCTIONS_WORKER_DYNAMIC_CONCURRENCY_ENABLED` |
Setting not valid |
`SCM_DO_BUILD_DURING_DEPLOYMENT` |
Replaced by the `remoteBuild` parameter when deploying in Flex Consumption |
`WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` |
Replaced by functionAppConfig's deployment section |
`WEBSITE_CONTENTOVERVNET` |
Not used for networking in Flex Consumption |
`WEBSITE_CONTENTSHARE` |
Replaced by functionAppConfig's deployment section |
`WEBSITE_DNS_SERVER` |
DNS is inherited from the integrated virtual network in Flex |
`WEBSITE_MAX_DYNAMIC_APPLICATION_SCALE_OUT` |
Replaced by `maximumInstanceCount` in `properties.functionAppConfig.scaleAndConcurrency` |
`WEBSITE_NODE_DEFAULT_VERSION` |
Replaced by `version` in `properties.functionAppConfig.runtime` |
`WEBSITE_RUN_FROM_PACKAGE` |
Not used for deployments in Flex Consumption |
`WEBSITE_SKIP_CONTENTSHARE_VALIDATION` |
Content share isn't used in Flex Consumption |
`WEBSITE_VNET_ROUTE_ALL` |
Not used for networking in Flex Consumption |
`properties.alwaysOn` |
Not valid |
`properties.containerSize` |
Renamed as `instanceMemoryMB` |
`properties.ftpsState` |
FTPS not supported |
`properties.isReserved` |
Not valid |
`properties.IsXenon` |
Not valid |
`properties.javaVersion` |
Replaced by `version` in `properties.functionAppConfig.runtime` |
`properties.LinuxFxVersion` |
Replaced by `properties.functionAppConfig.runtime` |
`properties.netFrameworkVersion` |
Replaced by `version` in `properties.functionAppConfig.runtime` |
`properties.powerShellVersion` |
Replaced by `version` in `properties.functionAppConfig.runtime` |
`properties.siteConfig.functionAppScaleLimit` |
Renamed as `maximumInstanceCount` |
`properties.siteConfig.preWarmedInstanceCount` |
Renamed as `alwaysReadyInstances` |
`properties.use32BitWorkerProcess` |
32-bit not supported |
`properties.vnetBackupRestoreEnabled` |
Not used for networking in Flex Consumption |
`properties.vnetContentShareEnabled` |
Not used for networking in Flex Consumption |
`properties.vnetImagePullEnabled` |
Not used for networking in Flex Consumption |
`properties.vnetRouteAllEnabled` |
Not used for networking in Flex Consumption |
`properties.windowsFxVersion` |
Not valid |
