---
merged_at: 2026-01-26T21:02:36.328308
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-dotnet-class-library -->

# Develop legacy C# class library functions using Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

This article is an introduction to developing Azure Functions by using C# in .NET class libraries. These class libraries are used to run *in-process with the Functions runtime*. Your .NET functions can alternatively run _isolated from the Functions *runtime*, which offers several advantages. To learn more, see [the isolated worker model](dotnet-isolated-process-guide). For a comprehensive comparison between these two models, see [Differences between the in-process model and the isolated worker model](dotnet-isolated-in-process-differences).

Important

This article supports .NET class library functions that run in-process with the runtime. Your C# functions can also run out-of-process and isolated from the Functions runtime. The isolated worker process model is the only way to run non-LTS versions of .NET and .NET Framework apps in current versions of the Functions runtime. To learn more, see [.NET isolated worker process functions](dotnet-isolated-process-guide).
For a comprehensive comparison between isolated worker process and in-process .NET Functions, see [Differences between in-process and isolate worker process .NET Azure Functions](dotnet-isolated-in-process-differences).

As a C# developer, you might also be interested in one of the following articles:

| Getting started | Concepts | Guided learning/samples |
|---|---|---|

Azure Functions supports C# and C# script programming languages. If you're looking for guidance on [using C# in the Azure portal](functions-create-function-app-portal), see [C# script (.csx) developer reference](functions-reference-csharp).

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

### Updating to target .NET 8

Apps using the in-process model can target .NET 8 by following the steps outlined in this section. However, if you choose to exercise this option, you should still begin planning your [migration to the isolated worker model](migrate-dotnet-to-isolated-model) in advance of [support ending for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model).

Many apps can change the configuration of the function app in Azure without updates to code or redeployment. To run .NET 8 with the in-process model, three configurations are required:

- The
[application setting](functions-how-to-use-azure-function-app-settings)`FUNCTIONS_WORKER_RUNTIME`

must be set with the value "dotnet". - The application setting
`FUNCTIONS_EXTENSION_VERSION`

must be set with the value "~4". - The application setting
`FUNCTIONS_INPROC_NET8_ENABLED`

must be set with the value "1". - You must
[update the stack configuration](update-language-versions#update-the-stack-configuration)to reference .NET 8.

Support for .NET 8 still uses version 4.x of the Functions runtime, and no change to the configured runtime version is required.

To update your local project, first make sure you're using the latest versions of local tools. Then ensure that the project references [version 4.4.0 or later of Microsoft.NET.Sdk.Functions](https://www.nuget.org/packages/Microsoft.NET.Sdk.Functions/4.4.0). You can then change your `TargetFramework`

to "net8.0". You must also update `local.settings.json`

to include both `FUNCTIONS_WORKER_RUNTIME`

set to "dotnet" and `FUNCTIONS_INPROC_NET8_ENABLED`

set to "1".

The following example is a minimal `project`

file with these changes:

```
<Project Sdk="Microsoft.NET.Sdk">
<PropertyGroup>
<TargetFramework>net8.0</TargetFramework>
<AzureFunctionsVersion>v4</AzureFunctionsVersion>
</PropertyGroup>
<ItemGroup>
<PackageReference Include="Microsoft.NET.Sdk.Functions" Version="4.4.0" />
</ItemGroup>
<ItemGroup>
<None Update="host.json">
<CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
</None>
<None Update="local.settings.json">
<CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
<CopyToPublishDirectory>Never</CopyToPublishDirectory>
</None>
</ItemGroup>
</Project>
```


The following example is a minimal `local.settings.json`

file with these changes:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "UseDevelopmentStorage=true",
"FUNCTIONS_INPROC_NET8_ENABLED": "1",
"FUNCTIONS_WORKER_RUNTIME": "dotnet"
}
}
```


If your app uses [ Microsoft.Azure.DurableTask.Netherite.AzureFunctions](https://www.nuget.org/packages/Microsoft.Azure.DurableTask.Netherite.AzureFunctions), ensure it targets version 1.5.3 or later. Due to a behavior change in .NET 8, apps with older versions of the package throw an ambiguous constructor exception.

You might need to make other changes to your app based on the version support of its other dependencies.

Version 4.x of the Functions runtime provides equivalent functionality for .NET 6 and .NET 8. The in-process model doesn't include other features or updates that integrate with new .NET 8 capabilities. For example, the runtime doesn't support keyed services. To take full advantage of the latest .NET 8 capabilities and enhancements, you must [migrate to the isolated worker model](migrate-dotnet-to-isolated-model).

## Functions class library project

In Visual Studio, the **Azure Functions** project template creates a C# class library project that contains the following files:

[host.json](functions-host-json)- stores configuration settings that affect all functions in the project when running locally or in Azure.[local.settings.json](functions-develop-local#local-settings-file)- stores app settings and connection strings that are used when running locally. This file contains secrets and isn't published to your function app in Azure. Instead,[add app settings to your function app](functions-develop-vs#function-app-settings).

When you build the project, a folder structure that looks like the following example is generated in the build output directory:

```
<framework.version>
| - bin
| - MyFirstFunction
| | - function.json
| - MySecondFunction
| | - function.json
| - host.json
```


This directory is what gets deployed to your function app in Azure. The binding extensions required in [version 2.x](functions-versions) of the Functions runtime are [added to the project as NuGet packages](functions-develop-vs?tabs=in-process#add-bindings).

Important

The build process creates a *function.json* file for each function. This *function.json* file isn't meant to be edited directly. You can't change binding configuration or disable the function by editing this file. To learn how to disable a function, see [How to disable functions](disable-function).

## Methods recognized as functions

In a class library, a function is a method with a `FunctionName`

and a trigger attribute, as shown in the following example:

```
public static class SimpleExample
{
[FunctionName("QueueTrigger")]
public static void Run(
[QueueTrigger("myqueue-items")] string myQueueItem,
ILogger log)
{
log.LogInformation($"C# function processed: {myQueueItem}");
}
}
```


The `FunctionName`

attribute marks the method as a function entry point. The name must be unique within a project, start with a letter and only contain letters, numbers, `_`

, and `-`

, up to 127 characters in length. Project templates often create a method named `Run`

, but the method name can be any valid C# method name. The preceding example shows a static method being used, but functions aren't required to be static.

The trigger attribute specifies the trigger type and binds input data to a method parameter. The example function is triggered by a queue message, and the queue message is passed to the method in the `myQueueItem`

parameter.

## Method signature parameters

The method signature might contain parameters other than the one used with the trigger attribute. Here are some of the other parameters that you can include:

[Input and output bindings](functions-triggers-bindings)marked as such by decorating them with attributes.- An
`ILogger`

or`TraceWriter`

([version 1.x-only](functions-versions#creating-1x-apps)) parameter for[logging](#logging). - A
`CancellationToken`

parameter for[graceful shutdown](#cancellation-tokens). [Binding expressions](functions-bindings-expressions-patterns)parameters to get trigger metadata.

The order of parameters in the function signature doesn't matter. For example, you can put trigger parameters before or after other bindings, and you can put the logger parameter before or after trigger or binding parameters.

### Output bindings

A function can have zero or multiple output bindings defined by using output parameters.

The following example modifies the preceding one by adding an output queue binding named `myQueueItemCopy`

. The function writes the contents of the message that triggers the function to a new message in a different queue.

```
public static class SimpleExampleWithOutput
{
[FunctionName("CopyQueueMessage")]
public static void Run(
[QueueTrigger("myqueue-items-source")] string myQueueItem,
[Queue("myqueue-items-destination")] out string myQueueItemCopy,
ILogger log)
{
log.LogInformation($"CopyQueueMessage function processed: {myQueueItem}");
myQueueItemCopy = myQueueItem;
}
}
```


Values assigned to output bindings are written when the function exits. You can use more than one output binding in a function by assigning values to multiple output parameters.

The binding reference articles ([Storage queues](functions-bindings-storage-queue), for example) explain which parameter types you can use with trigger, input, or output binding attributes.

### Binding expressions example

The following code gets the name of the queue to monitor from an app setting, and it gets the queue message creation time in the `insertionTime`

parameter.

```
public static class BindingExpressionsExample
{
[FunctionName("LogQueueMessage")]
public static void Run(
[QueueTrigger("%queueappsetting%")] string myQueueItem,
DateTimeOffset insertionTime,
ILogger log)
{
log.LogInformation($"Message content: {myQueueItem}");
log.LogInformation($"Created at: {insertionTime}");
}
}
```


## Autogenerated function.json

The build process creates a *function.json* file in a function folder in the build folder. As noted earlier, this file isn't meant to be edited directly. You can't change binding configuration or disable the function by editing this file.

The purpose of this file is to provide information to the scale controller to use for [scaling decisions on the Consumption plan](event-driven-scaling). For this reason, the file only has trigger info, not input/output bindings.

The generated *function.json* file includes a `configurationSource`

property that tells the runtime to use .NET attributes for bindings, rather than *function.json* configuration. Here's an example:

```
{
"generatedBy": "Microsoft.NET.Sdk.Functions-1.0.0.0",
"configurationSource": "attributes",
"bindings": [
{
"type": "queueTrigger",
"queueName": "%input-queue-name%",
"name": "myQueueItem"
}
],
"disabled": false,
"scriptFile": "..\\bin\\FunctionApp1.dll",
"entryPoint": "FunctionApp1.QueueTrigger.Run"
}
```


## Microsoft.NET.Sdk.Functions

The *function.json* file generation is performed by the NuGet package [Microsoft.NET.Sdk.Functions](https://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).

The following example shows the relevant parts of the `.csproj`

files that have different target frameworks of the same `Sdk`

package:

```
<PropertyGroup>
<TargetFramework>net8.0</TargetFramework>
<AzureFunctionsVersion>v4</AzureFunctionsVersion>
</PropertyGroup>
<ItemGroup>
<PackageReference Include="Microsoft.NET.Sdk.Functions" Version="4.5.0" />
</ItemGroup>
```


Important

Starting with version 4.0.6517 of the Core Tools, in-process model projects must reference [version 4.5.0 or later of Microsoft.NET.Sdk.Functions](https://www.nuget.org/packages/Microsoft.NET.Sdk.Functions/4.5.0). If an earlier version is used, the

`func start`

command will error.Among the `Sdk`

package dependencies are triggers and bindings. A 1.x project refers to 1.x triggers and bindings because those triggers and bindings target the .NET Framework, while 4.x triggers and bindings target .NET Core.

The `Sdk`

package also depends on [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json), and indirectly on [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage). These dependencies make sure that your project uses the versions of those packages that work with the Functions runtime version that the project targets. For example, `Newtonsoft.Json`

has version 11 for .NET Framework 4.6.1, but the Functions runtime that targets .NET Framework 4.6.1 is only compatible with `Newtonsoft.Json`

9.0.1. So your function code in that project also has to use `Newtonsoft.Json`

9.0.1.

The source code for `Microsoft.NET.Sdk.Functions`

is available in the GitHub repo [azure-functions-vs-build-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).

## Local runtime version

Visual Studio uses the [Azure Functions Core Tools](functions-run-local#install-the-azure-functions-core-tools) to run Functions projects on your local computer. The Core Tools is a command-line interface for the Functions runtime.

If you install the Core Tools using the Windows installer (MSI) package or by using npm, it doesn't affect the Core Tools version used by Visual Studio. For the Functions runtime version 1.x, Visual Studio stores Core Tools versions in *%USERPROFILE%\AppData\Local\Azure.Functions.Cli* and uses the latest version stored there. For Functions 4.x, the Core Tools are included in the **Azure Functions and Web Jobs Tools** extension. For Functions 1.x, you can see what version is being used in the console output when you run a Functions project:

```
[3/1/2018 9:59:53 AM] Starting Host (HostId=contoso2-1518597420, Version=2.0.11353.0, ProcessId=22020, Debug=False, Attempt=0, FunctionsExtensionVersion=)
```


## ReadyToRun

You can compile your function app as [ReadyToRun binaries](/en-us/dotnet/core/deploying/ready-to-run). ReadyToRun is a form of ahead-of-time compilation that can improve startup performance to help reduce the impact of [cold-start](event-driven-scaling#cold-start) when running in a [Consumption plan](consumption-plan).

ReadyToRun is available in .NET 6 and later versions and requires [version 4.0 of the Azure Functions runtime](functions-versions).

To compile your project as ReadyToRun, update your project file by adding the `<PublishReadyToRun>`

and `<RuntimeIdentifier>`

elements. The following example is the configuration for publishing to a Windows 32-bit function app.

```
<PropertyGroup>
<TargetFramework>net8.0</TargetFramework>
<AzureFunctionsVersion>v4</AzureFunctionsVersion>
<PublishReadyToRun>true</PublishReadyToRun>
<RuntimeIdentifier>win-x86</RuntimeIdentifier>
</PropertyGroup>
```


Important

Starting in .NET 6, support for Composite ReadyToRun compilation has been added. Check out [ReadyToRun Cross platform and architecture restrictions](/en-us/dotnet/core/deploying/ready-to-run).

You can also build your app with ReadyToRun from the command line. For more information, see the `-p:PublishReadyToRun=true`

option in [ dotnet publish](/en-us/dotnet/core/tools/dotnet-publish).

## Supported types for bindings

Each binding has its own supported types; for instance, a blob trigger attribute can be applied to a string parameter, a POCO parameter, a `CloudBlockBlob`

parameter, or any of several other supported types. The [binding reference article for blob bindings](functions-bindings-storage-blob-trigger#usage) lists all supported parameter types. For more information, see [Triggers and bindings](functions-triggers-bindings) and the [binding reference docs for each binding type](functions-triggers-bindings#related-content).

Tip

If you plan to use the HTTP or WebHook bindings, plan to avoid port exhaustion that can be caused by improper instantiation of `HttpClient`

. For more information, see [How to manage connections in Azure Functions](manage-connections).

## Binding to method return value

You can use a method return value for an output binding, by applying the attribute to the method return value. For examples, see [Triggers and bindings](functions-triggers-bindings).

Use the return value only if a successful function execution always results in a return value to pass to the output binding. Otherwise, use `ICollector`

or `IAsyncCollector`

, as shown in the following section.

## Writing multiple output values

To write multiple values to an output binding, or if a successful function invocation might not result in anything to pass to the output binding, use the [ ICollector](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or

[types. These types are write-only collections that are written to the output binding when the method completes.](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs)

`IAsyncCollector`

This example writes multiple queue messages into the same queue using `ICollector`

:

```
public static class ICollectorExample
{
[FunctionName("CopyQueueMessageICollector")]
public static void Run(
[QueueTrigger("myqueue-items-source-3")] string myQueueItem,
[Queue("myqueue-items-destination")] ICollector<string> myDestinationQueue,
ILogger log)
{
log.LogInformation($"C# function processed: {myQueueItem}");
myDestinationQueue.Add($"Copy 1: {myQueueItem}");
myDestinationQueue.Add($"Copy 2: {myQueueItem}");
}
}
```


## Async

To make a function [asynchronous](/en-us/dotnet/csharp/programming-guide/concepts/async/), use the `async`

keyword and return a `Task`

object.

```
public static class AsyncExample
{
[FunctionName("BlobCopy")]
public static async Task RunAsync(
[BlobTrigger("sample-images/{blobName}")] Stream blobInput,
[Blob("sample-images-copies/{blobName}", FileAccess.Write)] Stream blobOutput,
CancellationToken token,
ILogger log)
{
log.LogInformation($"BlobCopy function processed.");
await blobInput.CopyToAsync(blobOutput, 4096, token);
}
}
```


You can't use `out`

parameters in async functions. For output bindings, use the [function return value](#binding-to-method-return-value) or a [collector object](#writing-multiple-output-values) instead.

## Cancellation tokens

A function can accept a [CancellationToken](/en-us/dotnet/api/system.threading.cancellationtoken) parameter, which enables the operating system to notify your code when the function is about to be terminated. You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.

Consider the case when you have a function that processes messages in batches. The following Azure Service Bus-triggered function processes an array of [ServiceBusReceivedMessage](/en-us/dotnet/api/azure.messaging.servicebus.servicebusreceivedmessage) objects, which represents a batch of incoming messages to be processed by a specific function invocation:

```
using Azure.Messaging.ServiceBus;
using System.Threading;
namespace ServiceBusCancellationToken
{
public static class servicebus
{
[FunctionName("servicebus")]
public static void Run([ServiceBusTrigger("csharpguitar", Connection = "SB_CONN")]
ServiceBusReceivedMessage[] messages, CancellationToken cancellationToken, ILogger log)
{
try
{
foreach (var message in messages)
{
if (cancellationToken.IsCancellationRequested)
{
log.LogInformation("A cancellation token was received. Taking precautionary actions.");
//Take precautions like noting how far along you are with processing the batch
log.LogInformation("Precautionary activities --complete--.");
break;
}
else
{
//business logic as usual
log.LogInformation($"Message: {message} was processed.");
}
}
}
catch (Exception ex)
{
log.LogInformation($"Something unexpected happened: {ex.Message}");
}
}
}
}
```


## Logging

In your function code, you can write output to logs that appear as traces in Application Insights. The recommended way to write to the logs is to include a parameter of type [ILogger](/en-us/dotnet/api/microsoft.extensions.logging.ilogger), which is typically named `log`

. Version 1.x of the Functions runtime used `TraceWriter`

, which also writes to Application Insights, but doesn't support structured logging. Don't use `Console.Write`

to write your logs, since this data isn't captured by Application Insights.

### ILogger

In your function definition, include an [ILogger](/en-us/dotnet/api/microsoft.extensions.logging.ilogger) parameter, which supports [structured logging](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging).

With an `ILogger`

object, you call `Log<level>`

[extension methods on ILogger](/en-us/dotnet/api/microsoft.extensions.logging.loggerextensions#methods) to create logs. The following code writes `Information`

logs with category `Function.<YOUR_FUNCTION_NAME>.User.`

:

```
public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, ILogger logger)
{
logger.LogInformation("Request for item with key={itemKey}.", id);
```


To learn more about how Functions implements `ILogger`

, see [Collecting telemetry data](functions-monitoring#collecting-telemetry-data). Categories prefixed with `Function`

assume you're using an `ILogger`

instance. If you choose to instead use an `ILogger<T>`

, the category name might instead be based on `T`

.

### Structured logging

The order of placeholders, not their names, determines which parameters are used in the log message. Suppose you have the following code:

```
string partitionKey = "partitionKey";
string rowKey = "rowKey";
logger.LogInformation("partitionKey={partitionKey}, rowKey={rowKey}", partitionKey, rowKey);
```


If you keep the same message string and reverse the order of the parameters, the resulting message text would have the values in the wrong places.

Placeholders are handled this way so that you can do structured logging. Application Insights stores the parameter name-value pairs and the message string. The result is that the message arguments become fields that you can query on.

If your logger method call looks like the previous example, you can query the field `customDimensions.prop__rowKey`

. The `prop__`

prefix is added to ensure there are no collisions between fields the runtime adds and fields your function code adds.

You can also query on the original message string by referencing the field `customDimensions.prop__{OriginalFormat}`

.

Here's a sample JSON representation of `customDimensions`

data:

```
{
"customDimensions": {
"prop__{OriginalFormat}":"C# Queue trigger function processed: {message}",
"Category":"Function",
"LogLevel":"Information",
"prop__message":"c9519cbf-b1e6-4b9b-bf24-cb7d10b1bb89"
}
}
```


### Log custom telemetry

There's a Functions-specific version of the Application Insights SDK that you can use to send custom telemetry data from your functions to Application Insights: [Microsoft.Azure.WebJobs.Logging.ApplicationInsights](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Logging.ApplicationInsights). Use the following command from the command prompt to install this package:

```
dotnet add package Microsoft.Azure.WebJobs.Logging.ApplicationInsights --version <VERSION>
```


In this command, replace `<VERSION>`

with a version of this package that supports your installed version of [Microsoft.Azure.WebJobs](https://www.nuget.org/packages/Microsoft.Azure.WebJobs/).

The following C# examples uses the [custom telemetry API](/en-us/azure/azure-monitor/app/api-custom-events-metrics). The example is for a .NET class library, but the Application Insights code is the same for C# script.

Version 2.x and later versions of the runtime use newer features in Application Insights to automatically correlate telemetry with the current operation. There's no need to manually set the operation `Id`

, `ParentId`

, or `Name`

fields.

```
using System;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Logging;
using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;
using Microsoft.ApplicationInsights.Extensibility;
using System.Linq;
namespace functionapp0915
{
public class HttpTrigger2
{
private readonly TelemetryClient telemetryClient;
/// Using dependency injection will guarantee that you use the same configuration for telemetry collected automatically and manually.
public HttpTrigger2(TelemetryConfiguration telemetryConfiguration)
{
this.telemetryClient = new TelemetryClient(telemetryConfiguration);
}
[FunctionName("HttpTrigger2")]
public Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = null)]
HttpRequest req, ExecutionContext context, ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
DateTime start = DateTime.UtcNow;
// Parse query parameter
string name = req.Query
.FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
.Value;
// Write an event to the customEvents table.
var evt = new EventTelemetry("Function called");
evt.Context.User.Id = name;
this.telemetryClient.TrackEvent(evt);
// Generate a custom metric, in this case let's use ContentLength.
this.telemetryClient.GetMetric("contentLength").TrackValue(req.ContentLength);
// Log a custom dependency in the dependencies table.
var dependency = new DependencyTelemetry
{
Name = "GET api/planets/1/",
Target = "swapi.co",
Data = "https://swapi.co/api/planets/1/",
Timestamp = start,
Duration = DateTime.UtcNow - start,
Success = true
};
dependency.Context.User.Id = name;
this.telemetryClient.TrackDependency(dependency);
return Task.FromResult<IActionResult>(new OkResult());
}
}
}
```


In this example, the custom metric data gets aggregated by the host before being sent to the customMetrics table. To learn more, see the [GetMetric](/en-us/azure/azure-monitor/app/api-custom-events-metrics#getmetric) documentation in Application Insights.

When running locally, you must add the `APPINSIGHTS_INSTRUMENTATIONKEY`

setting, with the Application Insights key, to the [local.settings.json](functions-develop-local#local-settings-file) file.

Don't call `TrackRequest`

or `StartOperation<RequestTelemetry>`

because you see duplicate requests for a function invocation. The Functions runtime automatically tracks requests.

Don't set `telemetryClient.Context.Operation.Id`

. This global setting causes incorrect correlation when many functions are running simultaneously. Instead, create a new telemetry instance (`DependencyTelemetry`

, `EventTelemetry`

) and modify its `Context`

property. Then pass in the telemetry instance to the corresponding `Track`

method on `TelemetryClient`

(`TrackDependency()`

, `TrackEvent()`

, `TrackMetric()`

). This method ensures that the telemetry has the correct correlation details for the current function invocation.

## Testing functions

The following articles show how to run an in-process C# class library function locally for testing purposes:

## Environment variables

To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`

, as shown in the following code example:

```
public static class EnvironmentVariablesExample
{
[FunctionName("GetEnvironmentVariables")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, ILogger log)
{
log.LogInformation($"C# Timer trigger function executed at: {DateTime.Now}");
log.LogInformation(GetEnvironmentVariable("AzureWebJobsStorage"));
log.LogInformation(GetEnvironmentVariable("WEBSITE_SITE_NAME"));
}
private static string GetEnvironmentVariable(string name)
{
return name + ": " +
System.Environment.GetEnvironmentVariable(name, EnvironmentVariableTarget.Process);
}
}
```


App settings can be read from environment variables both when developing locally and when running in Azure. When developing locally, app settings come from the `Values`

collection in the *local.settings.json* file. In both environments, local and Azure, `GetEnvironmentVariable("<app setting name>")`

retrieves the value of the named app setting. For instance, when you're running locally, "My Site Name" would be returned if your *local.settings.json* file contains `{ "Values": { "WEBSITE_SITE_NAME": "My Site Name" } }`

.

The [System.Configuration.ConfigurationManager.AppSettings](/en-us/dotnet/api/system.configuration.configurationmanager.appsettings) property is an alternative API for getting app setting values, but we recommend that you use `GetEnvironmentVariable`

as shown here.

## Binding at runtime

In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed to the [ declarative](https://en.wikipedia.org/wiki/Declarative_programming) bindings in attributes. Imperative binding is useful when binding parameters need to be computed at runtime rather than design time. With this pattern, you can bind to supported input and output bindings on-the-fly in your function code.

Define an imperative binding as follows:

**Do not**include an attribute in the function signature for your desired imperative bindings.Pass in an input parameter

or`Binder binder`

.`IBinder binder`

Use the following C# pattern to perform the data binding.

`using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...))) { ... }`

`BindingTypeAttribute`

is the .NET attribute that defines your binding, and`T`

is an input or output type that's supported by that binding type.`T`

can't be an`out`

parameter type (such as`out JObject`

). For example, the Mobile Apps table output binding supports[six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use[ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs)or[IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs)with imperative binding.

### Single attribute example

The following example code creates a [Storage blob output binding](functions-bindings-storage-blob-output) with blob path that's defined at run time, then writes a string to the blob.

```
public static class IBinderExample
{
[FunctionName("CreateBlobUsingBinder")]
public static void Run(
[QueueTrigger("myqueue-items-source-4")] string myQueueItem,
IBinder binder,
ILogger log)
{
log.LogInformation($"CreateBlobUsingBinder function processed: {myQueueItem}");
using (var writer = binder.Bind<TextWriter>(new BlobAttribute(
$"samples-output/{myQueueItem}", FileAccess.Write)))
{
writer.Write("Hello World!");
};
}
}
```


[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Extensions.Storage/Blobs/BlobAttribute.cs) defines the [Storage blob](functions-bindings-storage-blob) input or output binding, and [TextWriter](/en-us/dotnet/api/system.io.textwriter) is a supported output binding type.

### Multiple attributes example

The preceding example gets the app setting for the function app's main Storage account connection string (which is `AzureWebJobsStorage`

). You can specify a custom app setting to use for the Storage account by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing the attribute array into `BindAsync<T>()`

. Use a `Binder`

parameter, not `IBinder`

. For example:

```
public static class IBinderExampleMultipleAttributes
{
[FunctionName("CreateBlobInDifferentStorageAccount")]
public async static Task RunAsync(
[QueueTrigger("myqueue-items-source-binder2")] string myQueueItem,
Binder binder,
ILogger log)
{
log.LogInformation($"CreateBlobInDifferentStorageAccount function processed: {myQueueItem}");
var attributes = new Attribute[]
{
new BlobAttribute($"samples-output/{myQueueItem}", FileAccess.Write),
new StorageAccountAttribute("MyStorageAccount")
};
using (var writer = await binder.BindAsync<TextWriter>(attributes))
{
await writer.WriteAsync("Hello World!!");
}
}
}
```


## Triggers and bindings

This table shows the bindings that are supported in the major versions of the Azure Functions runtime:

| Type | 4.x1 |
1.x2 |
Trigger | Input | Output |
|---|---|---|---|---|---|
|

[Azure Cosmos DB](functions-bindings-cosmosdb-v2)[Azure Data Explorer](functions-bindings-azure-data-explorer)[Azure SQL](functions-bindings-azure-sql)[Dapr](functions-bindings-dapr)4[Event Grid](functions-bindings-event-grid)[Event Hubs](functions-bindings-event-hubs)[HTTP and webhooks](functions-bindings-http-webhook)[IoT Hub](functions-bindings-event-iot)[Kafka](functions-bindings-kafka)3[Mobile Apps](functions-bindings-mobile-apps)[Model Context Protocol](functions-bindings-mcp)[Notification Hubs](functions-bindings-notification-hubs)[Queue Storage](functions-bindings-storage-queue)[Redis](functions-bindings-cache)[RabbitMQ](functions-bindings-rabbitmq)3[SendGrid](functions-bindings-sendgrid)[Service Bus](functions-bindings-service-bus)[Azure SignalR Service](functions-bindings-signalr-service)[Table Storage](functions-bindings-storage-table)[Timer](functions-bindings-timer)[Twilio](functions-bindings-twilio)- Register all bindings except HTTP and timer. See
[Register Azure Functions binding extensions](functions-bindings-register). This step isn't required when using version 1.x of the Functions runtime. [Support ends for version 1.x of the Azure Functions runtime on September 14, 2026](https://aka.ms/azure-functions-retirements/hostv1).[Migrate your apps to version 4.x](migrate-version-1-version-4)for full support.- Triggers aren't supported in the Consumption plan. This binding type requires
[runtime-driven triggers](functions-networking-options#elastic-premium-plan-with-virtual-network-triggers). - This binding type is supported in Kubernetes, Azure IoT Edge, and other self-hosted modes only.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/scenario-custom-remote-mcp-server -->

# Quickstart: Build a custom remote MCP server using Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you create a custom remote Model Context Protocol (MCP) server from a template project using the Azure Developer CLI (`azd`

). The MCP server uses the Azure Functions MCP server extension to provide tools for AI models, agents, and assistants. After running the project locally and verifying your code using GitHub Copilot, you deploy it to a new serverless function app in Azure Functions that follows current best practices for secure and scalable deployments.

Tip

Functions also enables you to deploy an existing MCP server code project to a Flex Consumption plan app without having to make changes to your code project. For more information, see [Quickstart: Host existing MCP servers on Azure Functions](scenario-host-mcp-server-sdks).

Because the new app runs on the Flex Consumption plan, which follows a *pay-for-what-you-use* billing model, completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

Important

While [creating custom MCP servers](functions-bindings-mcp) is supported for all Functions languages, this quickstart scenario currently only has examples for C#, Python, and TypeScript. To complete this quickstart, select one of these supported languages at the top of the article.

This article supports version 4 of the Node.js programming model for Azure Functions.

This article supports version 2 of the Python programming model for Azure Functions.

## Prerequisites

[Java 17 Developer Kit](/en-us/azure/developer/java/fundamentals/java-support-on-azure)- If you use another
[supported version of Java](supported-languages?pivots=programming-language-java#languages-by-runtime-version), you must update the project's pom.xml file. - Set the
`JAVA_HOME`

environment variable to the install location of the correct version of the Java Development Kit (JDK).

- If you use another
[Apache Maven 3.8.x](https://maven.apache.org)

[Visual Studio Code](https://code.visualstudio.com/)with these extensions:[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions). This extension requires[Azure Functions Core Tools](functions-run-local)and attempts to install it when not available.

[Azure CLI](/en-us/cli/azure/install-azure-cli). You can also run Azure CLI commands in[Azure Cloud Shell](../cloud-shell/overview).An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Initialize the project

Use the `azd init`

command to create a local Azure Functions code project from a template.

- In Visual Studio Code, open a folder or workspace where you want to create your project.

In the Terminal, run this

`azd init`

command:`azd init --template remote-mcp-functions-dotnet -e mcpserver-dotnet`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/remote-mcp-functions-dotnet)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also used in the name of the resource group you create in Azure.

In your local terminal or command prompt, run this

`azd init`

command:`azd init --template remote-mcp-functions-java -e mcpserver-java`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/remote-mcp-functions-java)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also used in names of the resources you create in Azure.

In your local terminal or command prompt, run this

`azd init`

command:`azd init --template remote-mcp-functions-typescript -e mcpserver-ts`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/remote-mcp-functions-typescript)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also used in names of the resources you create in Azure.

In your local terminal or command prompt, run this

`azd init`

command:`azd init --template remote-mcp-functions-python -e mcpserver-python`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/remote-mcp-functions-python)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also used in names of the resources you create in Azure.

## Start the storage emulator

Use the Azurite emulator to simulate an Azure Storage account connection when running your code project locally.

If you haven't already,

[install Azurite](/en-us/azure/storage/common/storage-use-azurite#install-azurite).Press

`F1`. In the command palette, search for and run the command`Azurite: Start`

to start the local storage emulator.

## Run your MCP server locally

Visual Studio Code integrates with [Azure Functions Core tools](functions-run-local) to let you run this project on your local development computer by using the Azurite emulator.

To start the function locally, press

`F5`or the**Run and Debug**icon in the left-hand side Activity bar. The**Terminal**panel displays the output from Core Tools. Your app starts in the**Terminal**panel, and you can see the name of the functions that are running locally.Make a note of the local MCP server endpoint (like

`http://localhost:7071/runtime/webhooks/mcp`

), which you use to configure GitHub Copilot in Visual Studio Code.

## Verify using GitHub Copilot

To verify your code, add the running project as an MCP server for GitHub Copilot in Visual Studio Code:

Press

`F1`. In the command palette, search for and run**MCP: Add Server**.Choose

**HTTP (Server-Sent Events)**for the transport type.Enter the URL of the MCP endpoint you copied in the previous step.

Use the generated

**Server ID**and select**Workspace**to save the MCP server connection to your Workspace settings.Open the command palette and run

**MCP: List Servers**and verify that the server you added is listed and running.In Copilot chat, select

**Agent**mode and run this prompt:`Say Hello`

When prompted to run the tool, select

**Allow in this Workspace**so you don't have to keep granting permission. The prompt runs and returns a`Hello World`

response and function execution information is written to the logs.Now, select some code in one of your project files and run this prompt:

`Save this snippet as snippet1`

Copilot stores the snippet and responds to your request with information about how to retrieve the snippet by using the

`getSnippets`

tool. Again, you can review the function execution in the logs and verify that the`saveSnippets`

function ran.In Copilot chat, run this prompt:

`Retrieve snippet1 and apply to NewFile`

Copilot retrieves the snippets, adds it to a file called

`NewFile`

, and does whatever else it thinks is needed to make the code snippet work in your project. The Functions logs show that the`getSnippets`

endpoint was called.When you're done testing, press Ctrl+C to stop the Functions host.


## Review the code (optional)

You can review the code that defines the MCP server tools:

The function code for the MCP server tools is defined in the `src`

folder. The `McpToolTrigger`

attribute exposes the functions as MCP Server tools:

```
[Function(nameof(SayHello))]
public string SayHello(
[McpToolTrigger(HelloToolName, HelloToolDescription)] ToolInvocationContext context
)
{
logger.LogInformation("C# MCP tool trigger function processed a request.");
return "Hello I am MCP Tool!";
}
```


```
[Function(nameof(GetSnippet))]
public object GetSnippet(
[McpToolTrigger(GetSnippetToolName, GetSnippetToolDescription)]
ToolInvocationContext context,
[BlobInput(BlobPath)] string snippetContent
)
{
return snippetContent;
}
[Function(nameof(SaveSnippet))]
[BlobOutput(BlobPath)]
public string SaveSnippet(
[McpToolTrigger(SaveSnippetToolName, SaveSnippetToolDescription)]
ToolInvocationContext context,
[McpToolProperty(SnippetNamePropertyName, SnippetNamePropertyDescription, true)]
string name,
[McpToolProperty(SnippetPropertyName, SnippetPropertyDescription, true)]
string snippet
)
{
return snippet;
}
}
```


You can view the complete project template in the [Azure Functions .NET MCP Server](https://github.com/Azure-Samples/remote-mcp-functions-dotnet) GitHub repository.

The function code for the MCP server tools is defined in the `src/main/java/com/function/`

folder. The `@McpToolTrigger`

annotation exposes the functions as MCP Server tools:

```
description = "The messages to be logged.",
isRequired = true,
isArray = true)
String messages,
final ExecutionContext functionExecutionContext
) {
functionExecutionContext.getLogger().info("Hello, World!");
functionExecutionContext.getLogger().info("Tool Name: " + mcpToolInvocationContext.getName());
functionExecutionContext.getLogger().info("Transport Type: " + mcpToolInvocationContext.getTransportType());
// Handle different transport types
if (mcpToolInvocationContext.isHttpStreamable()) {
functionExecutionContext.getLogger().info("Session ID: " + mcpToolInvocationContext.getSessionid());
} else if (mcpToolInvocationContext.isHttpSse()) {
if (mcpToolInvocationContext.getClientinfo() != null) {
functionExecutionContext.getLogger().info("Client: " +
mcpToolInvocationContext.getClientinfo().get("name").getAsString() + " v" +
```


```
// Write the snippet content to the output blob
outputBlob.setValue(snippet);
return "Successfully saved snippet '" + snippetName + "' with " + snippet.length() + " characters.";
}
/**
* Azure Function that handles retrieving a text snippet from Azure Blob Storage.
* <p>
* The function is triggered by an MCP Tool Trigger. The snippet name is provided
* as an MCP tool property, and the snippet content is read from the blob at the
* path derived from the snippet name.
*
* @param mcpToolInvocationContext The JSON input from the MCP tool trigger.
* @param snippetName The name of the snippet to retrieve, provided as an MCP tool property.
* @param inputBlob The Azure Blob input binding that fetches the snippet content.
* @param functionExecutionContext The execution context for logging.
*/
@FunctionName("GetSnippets")
@StorageAccount("AzureWebJobsStorage")
public String getSnippet(
@McpToolTrigger(
name = "getSnippets",
description = "Gets a text snippet from your snippets collection.")
String mcpToolInvocationContext,
@McpToolProperty(
name = SNIPPET_NAME_PROPERTY_NAME,
propertyType = "string",
description = "The name of the snippet.",
isRequired = true)
String snippetName,
@BlobInput(name = "inputBlob", path = BLOB_PATH)
String inputBlob,
final ExecutionContext functionExecutionContext
) {
// Log the entire incoming JSON for debugging
functionExecutionContext.getLogger().info(mcpToolInvocationContext);
// Log the snippet name and the fetched snippet content from the blob
```


You can view the complete project template in the [Azure Functions Java MCP Server](https://github.com/Azure-Samples/remote-mcp-functions-java) GitHub repository.

The function code for the MCP server tools is defined in the `src/function_app.py`

file. The MCP function annotations expose these functions as MCP Server tools:

```
tool_properties_save_snippets_json = json.dumps([prop.to_dict() for prop in tool_properties_save_snippets_object])
tool_properties_get_snippets_json = json.dumps([prop.to_dict() for prop in tool_properties_get_snippets_object])
@app.generic_trigger(
arg_name="context",
type="mcpToolTrigger",
toolName="hello_mcp",
description="Hello world.",
toolProperties="[]",
)
def hello_mcp(context) -> None:
"""
```


```
@app.generic_trigger(
arg_name="context",
type="mcpToolTrigger",
toolName="save_snippet",
description="Save a snippet with a name.",
toolProperties=tool_properties_save_snippets_json,
)
@app.generic_output_binding(arg_name="file", type="blob", connection="AzureWebJobsStorage", path=_BLOB_PATH)
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


You can view the complete project template in the [Azure Functions Python MCP Server](https://github.com/Azure-Samples/remote-mcp-functions-python) GitHub repository.

The function code for the MCP server tools is defined in the `src`

folder. The MCP function registration exposes these functions as MCP Server tools:

```
export async function mcpToolHello(_toolArguments:unknown, context: InvocationContext): Promise<string> {
console.log(_toolArguments);
// Get name from the tool arguments
const mcptoolargs = context.triggerMetadata.mcptoolargs as {
name?: string;
};
const name = mcptoolargs?.name;
console.info(`Hello ${name}, I am MCP Tool!`);
return `Hello ${name || 'World'}, I am MCP Tool!`;
}
// Register the hello tool
app.mcpTool('hello', {
toolName: 'hello',
description: 'Simple hello world MCP Tool that responses with a hello message.',
toolProperties:{
name: arg.string().describe('Required property to identify the caller.').optional()
},
handler: mcpToolHello
});
```


```
// SaveSnippet function - saves a snippet with a name
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


You can view the complete project template in the [Azure Functions TypeScript MCP Server](https://github.com/Azure-Samples/remote-mcp-functions-typescript) GitHub repository.

After verifying the MCP server tools locally, you can publish the project to Azure.

## Deploy to Azure

This project is configured to use the `azd up`

command to deploy this project to a new function app in a Flex Consumption plan in Azure. The project includes a set of Bicep files that `azd`

uses to create a secure deployment to a Flex consumption plan that follows best practices.

In Visual Studio Code, press

`F1`to open the command palette. Search for and run the command`Azure Developer CLI (azd): Package, Provison and Deploy (up)`

. Then, sign in by using your Azure account.If you're not already signed in, authenticate with your Azure account.

When prompted, provide these required deployment parameters:

Parameter Description *Azure subscription*Subscription in which your resources are created. *Azure location*Azure region in which to create the resource group that contains the new Azure resources. Only regions that currently support the Flex Consumption plan are shown. After the command completes successfully, you see links to the resources you created.


## Connect to your remote MCP server

Your MCP server is now running in Azure. When you access the tools, you need to include a system key in your request. This key provides a degree of access control for clients accessing your remote MCP server. After you get this key, you can connect GitHub Copilot to your remote server.

Run this script that uses

`azd`

and the Azure CLI to print out both the MCP server URL and the system key (`mcp_extension`

) required to access the tools:`eval $(azd env get-values --output dotenv) MCP_EXTENSION_KEY=$(az functionapp keys list --resource-group $AZURE_RESOURCE_GROUP \ --name $AZURE_FUNCTION_NAME --query "systemKeys.mcp_extension" -o tsv) printf "MCP Server URL: %s\n" "https://$SERVICE_API_NAME.azurewebsites.net/runtime/webhooks/mcp" printf "MCP Server key: %s\n" "$MCP_EXTENSION_KEY"`

In Visual Studio Code, press

`F1`to open the command palette, search for and run the command`MCP: Open Workspace Folder MCP Configuraton`

, which opens the`mcp.json`

configuration file.In the

`mcp.json`

configuration, find the named MCP server you added earlier, change the`url`

value to your remote MCP server URL, and add a`headers.x-functions-key`

element, which contains your copied MCP server access key, as in this example:`{ "servers": { "remote-mcp-function": { "type": "http", "url": "https://contoso.azurewebsites.net/runtime/webhooks/mcp", "headers": { "x-functions-key": "A1bC2dE3fH4iJ5kL6mN7oP8qR9sT0u..." } } } }`

Select the

**Start**button above your server name in the open`mcp.json`

to restart the remote MCP server, this time using your deployed app.

## Verify your deployment

You can now have GitHub Copilot use your remote MCP tools just as you did locally, but now the code runs securely in Azure. Replay the same commands you used earlier to ensure everything works correctly.

## Clean up resources

When you're done working with your MCP server and related resources, use this command to delete the function app and its related resources from Azure to avoid incurring further costs:

```
azd down --no-prompt
```


Note

The `--no-prompt`

option instructs `azd`

to delete your resource group without confirmation from you. This command doesn't affect your local code project.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-versions -->

# Azure Functions runtime versions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Azure Functions currently supports two versions of the runtime host. The following table details the currently supported runtime versions, their support level, and when they should be used:]

| Version | Support level | Description |
|---|---|---|
| 4.x | GA | Check out Recommended runtime version for functions in all languages.
|
| 1.x | GA (
|

**Support will end for version 1.x on September 14, 2026.**We highly recommend you[migrate your apps to version 4.x](migrate-version-1-version-4?pivots=programming-language-csharp), which supports .NET Framework 4.8, .NET 8, .NET 9, and .NET 10 Preview.Important

As of December 13, 2022, function apps running on versions 2.x and 3.x of the Azure Functions runtime reached the end of extended support. For more information, see [Retired versions](#retired-versions).

This article details some of the differences between supported versions, how you can create each version, and how to change the version on which your functions run.

## Levels of support

There are two levels of support:

**Generally available (GA)**- Fully supported and approved for production use.**Preview**- Not yet supported, but expected to reach GA status in the future.

## Languages

All functions in a function app must share the same language. You choose the language of functions in your function app when you create the app. The language of your function app is maintained in the [FUNCTIONS_WORKER_RUNTIME](functions-app-settings#functions_worker_runtime) setting, and can't be changed when there are existing functions.

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

For information about the language versions of previously supported versions of the Functions runtime, see [Retired runtime versions](language-support-policy#language-support-related-resources).

## Run on a specific version

The version of the Functions runtime used by published apps in Azure is dictated by the [ FUNCTIONS_EXTENSION_VERSION](functions-app-settings#functions_extension_version) application setting. In some cases and for certain languages, other settings can apply.

By default, function apps created in the Azure portal, by the Azure CLI, or from Visual Studio tools are set to version 4.x. You can modify this version if needed. You can only downgrade the runtime version to 1.x after you create your function app but before you add any functions. Updating to a later major version is allowed even with apps that have existing functions.

### Migrating existing function apps

When your app has existing functions, you must take precautions before moving to a later major runtime version. The following articles detail breaking changes between major versions, including language-specific breaking changes. They also provide you with step-by-step instructions for a successful migration of your existing function app.

### Changing the version of apps in Azure

The following major runtime version values are used:

| Value | Runtime target |
|---|---|
`~4` |
4.x |
`~1` |
1.x |

Important

Don't arbitrarily change this app setting, because other app setting changes and changes to your function code might be required. For existing function apps, follow the [migration instructions](#migrating-existing-function-apps).

### Pinning to a specific minor version

To resolve issues that your function app could have when running on the latest major version, you must temporarily pin your app to a specific minor version. Pinning gives you time to get your app running correctly on the latest major version. The way that you pin to a minor version differs between Windows and Linux. To learn more, see [How to target Azure Functions runtime versions](set-runtime-version).

Older minor versions are periodically removed from Functions. For the latest news about Azure Functions releases, including the removal of specific older minor versions, monitor [Azure App Service announcements](https://github.com/Azure/app-service-announcements/issues).

## Minimum extension versions

There's technically not a correlation between binding extension versions and the Functions runtime version. However, starting with version 4.x the Functions runtime enforces a minimum version for all trigger and binding extensions.

If you receive a warning about a package not meeting a minimum required version, you should update that NuGet package to the minimum version as you normally would. The minimum version requirements for extensions used in Functions v4.x can be found in [the linked configuration file](https://github.com/Azure/azure-functions-host/blob/dev/src/WebJobs.Script/extensionrequirements.json).

For C# script, update the extension bundle reference in the *host.json* as follows:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.0.0, 5.0.0)"
}
}
```


There's technically not a correlation between extension bundle versions and the Functions runtime version. However, starting with version 4.x the Functions runtime enforces a minimum version for extension bundles.

If you receive a warning about your extension bundle version not meeting a minimum required version, update your existing extension bundle reference in the *host.json* as follows:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.0.0, 5.0.0)"
}
}
```


To learn more about extension bundles, see [Extension bundles](extension-bundles).

## Retired versions

Important

[Support will end for version 1.x of the Azure Functions runtime on September 14, 2026](https://aka.ms/azure-functions-retirements/hostv1). We highly recommend that you [migrate your apps to version 4.x](migrate-version-1-version-4) for full support.

These versions of the Functions runtime reached the end of extended support on December 13, 2022.

| Version | Current support level | Previous support level |
|---|---|---|
| 3.x | Out of support | GA |
| 2.x | Out of support | GA |

As soon as possible, you should migrate your apps to version 4.x to obtain full support. For a complete set of language-specific migration instructions, see [Migrate apps to Azure Functions version 4.x](migrate-version-3-version-4).

Apps using versions 2.x and 3.x can still be created and deployed from your CI/CD DevOps pipeline, and all existing apps continue to run without breaking changes. However, your apps aren't eligible for new features, security patches, and performance optimizations. You can only get related service support after you upgrade your apps to version 4.x.

Versions 2.x and 3.x are no longer supported due to the end of support for .NET Core 3.1, which was a core dependency. This requirement affects all [languages supported by Azure Functions](supported-languages).

## Locally developed application versions

You can make the following updates to function apps to locally change the targeted versions.

### Visual Studio runtime versions

In Visual Studio, you select the runtime version when you create a project. Azure Functions tools for Visual Studio supports the two major runtime versions. The correct version is used when debugging and publishing based on project settings. The version settings are defined in the *.csproj* file in the following properties:

```
<TargetFramework>net8.0</TargetFramework>
<AzureFunctionsVersion>v4</AzureFunctionsVersion>
```


If you're using the [isolated worker model](dotnet-isolated-process-guide), you can choose, `net9.0`

, `net8.0`

, or `net48`

as the target framework. You can also choose to use [preview support](dotnet-isolated-process-guide#preview-net-versions) for `net10.0`

. If you're using the [in-process model](functions-dotnet-class-library), you can choose `net8.0`

or `net6.0`

, and you must include the `Microsoft.NET.Sdk.Functions`

extension set to at least `4.4.0`

. .NET 10 is not supported by the in-process model; if you are on the in-process model and wish to use .NET 10, [migrate your app to the isolated worker model](migrate-dotnet-to-isolated-model).

.NET 6 was previously supported on the isolated worker model and the in-process model, but it reached the end of official support on [November 12, 2024](https://dotnet.microsoft.com/platform/support/policy/dotnet-core#lifecycle).
.NET 7 was previously supported on the isolated worker model but reached the end of official support on [May 14, 2024](https://dotnet.microsoft.com/platform/support/policy/dotnet-core#lifecycle).

### Visual Studio Code and Azure Functions Core Tools

[Azure Functions Core Tools](functions-run-local) is used for command-line development and also by the [Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions) for Visual Studio Code. For more information, see [Install the Azure Functions Core Tools](functions-run-local#install-the-azure-functions-core-tools).

For Visual Studio Code development, you might also need to update the user setting for the `azureFunctions.projectRuntime`

to match the version of the tools installed. This setting also updates the templates and languages used during function app creation.

## Bindings

Starting with version 2.x, the runtime uses a new [binding extensibility model](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) that offers these advantages:

Support for non-Microsoft binding extensions.

Decoupling of runtime and bindings. This change allows binding extensions to be versioned and released independently. You can, for example, opt to upgrade to a version of an extension that relies on a newer version of an underlying SDK.

A lighter execution environment, where only the bindings in use are known and loaded by the runtime.


Except for HTTP and timer triggers, all bindings must be explicitly added to the function app project, or registered in the portal. For more information, see [Azure Functions binding expression patterns](functions-bindings-expressions-patterns).

This table shows the bindings that are supported in the major versions of the Azure Functions runtime:

| Type | 4.x1 |
1.x2 |
Trigger | Input | Output |
|---|---|---|---|---|---|
|

[Azure Cosmos DB](functions-bindings-cosmosdb-v2)[Azure Data Explorer](functions-bindings-azure-data-explorer)[Azure SQL](functions-bindings-azure-sql)[Dapr](functions-bindings-dapr)4[Event Grid](functions-bindings-event-grid)[Event Hubs](functions-bindings-event-hubs)[HTTP and webhooks](functions-bindings-http-webhook)[IoT Hub](functions-bindings-event-iot)[Kafka](functions-bindings-kafka)3[Mobile Apps](functions-bindings-mobile-apps)[Model Context Protocol](functions-bindings-mcp)[Notification Hubs](functions-bindings-notification-hubs)[Queue Storage](functions-bindings-storage-queue)[Redis](functions-bindings-cache)[RabbitMQ](functions-bindings-rabbitmq)3[SendGrid](functions-bindings-sendgrid)[Service Bus](functions-bindings-service-bus)[Azure SignalR Service](functions-bindings-signalr-service)[Table Storage](functions-bindings-storage-table)[Timer](functions-bindings-timer)[Twilio](functions-bindings-twilio)- Register all bindings except HTTP and timer. See
[Register Azure Functions binding extensions](functions-bindings-register). This step isn't required when using version 1.x of the Functions runtime. [Support ends for version 1.x of the Azure Functions runtime on September 14, 2026](https://aka.ms/azure-functions-retirements/hostv1).[Migrate your apps to version 4.x](migrate-version-1-version-4)for full support.- Triggers aren't supported in the Consumption plan. This binding type requires
[runtime-driven triggers](functions-networking-options#elastic-premium-plan-with-virtual-network-triggers). - This binding type is supported in Kubernetes, Azure IoT Edge, and other self-hosted modes only.

## Function app timeout duration

The `functionTimeout`

property in the [host.json](functions-host-json#functiontimeout) project file sets the timeout duration for functions in a function app. This property applies specifically to function executions. After the trigger starts function execution, the function needs to return or respond within the timeout duration. When an execution exceeds this duration, a timeout error occurs and the language worker process restarts. For C# apps running in-process, the host process itself restarts. To avoid timeouts and subsequent process restarts, it's important to [write robust functions](functions-best-practices#write-robust-functions). For more information, see [Improve Azure Functions performance and reliability](performance-reliability#make-sure-background-tasks-complete).

The following table shows the default and maximum values (in minutes) for specific plans:

| Plan | Default | Maximum1 |
|---|---|---|
|
30 | Unbounded2 |
|
304 |
Unbounded2 |
|
304 |
Unbounded3 |
|
30 | Unbounded5 |
|
5 | 10 |

- Regardless of the function app timeout setting, 230 seconds is the maximum amount of time that an HTTP triggered function can take to respond to a request. This limit exists because of the
[default idle timeout of Azure Load Balancer](../app-service/faq-availability-performance-application-issues#why-does-my-request-time-out-after-230-seconds). For longer processing times, consider using the[Durable Functions async pattern](durable/durable-functions-overview#async-http)or[defer the actual work and return an immediate response](performance-reliability#avoid-long-running-functions). - There's no maximum execution timeout duration enforced. However, the grace period given to a function execution is 60 minutes
[during scale in](event-driven-scaling#scale-in-behaviors)for the Flex Consumption and Premium plans, and a grace period of 10 minutes is given during platform updates. - Requires the App Service plan be set to
[Always On](/en-us/azure/azure-functions/dedicated-plan#always-on). A grace period of 10 minutes is given during platform updates. - The default timeout for version 1.x of the Functions host runtime is
*unbounded*. - When the
[minimum number of replicas](../container-apps/scale-app#scale-definition)is set to zero, the default timeout depends on the specific triggers used in the app.

These values assume that the Azure Functions host process starts and runs correctly. There's a maximum timeout of 60 seconds for the language-specific worker process to also start. The worker process startup timeout isn't currently configurable.

## Related content

For more information, see the following resources:

---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _create-resources-azure-powershell_functions-bindings-openai-assistantpost-input.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: create-resources-azure-powershell.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/create-resources-azure-powershell -->

# Create function app resources in Azure using PowerShell

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure PowerShell example scripts in this article create function apps and other resources required to host your functions in Azure. A function app provides an execution context in which your functions are executed. All functions running in a function app share the same resources and connections, and they're all scaled together.

After the resources are created, you can deploy your project files to the new function app. To learn more, see [Deployment methods](functions-deployment-technologies#deployment-methods).

Every function app requires your PowerShell scripts to create the following resources:

| Resource | cmdlet | Description |
|---|---|---|
| Resource group |
|

[resource group](../azure-resource-manager/management/overview)in which you'll create your function app.[New-AzStorageAccount](/en-us/powershell/module/az.storage/new-azstorageaccount)[storage account](../storage/common/storage-account-create)used by your function app. Storage account names must be between 3 and 24 characters in length and can contain numbers and lowercase letters only. You can also use an existing account, which must meet the[storage account requirements](storage-considerations#storage-account-requirements).[New-AzFunctionAppPlan](/en-us/powershell/module/az.functions/new-azfunctionappplan)[Consumption plan](consumption-plan), since Consumption plans are created when you run`New-AzFunctionApp`

. For more information, see [Azure Functions hosting options](functions-scale).[New-AzFunctionApp](/en-us/powershell/module/az.functions/new-azfunctionapp)`-Name`

parameter must be a globally unique name across all of Azure App Service. Valid characters in `-Name`

are `a-z`

(case insensitive), `0-9`

, and `-`

. Most examples create a function app that supports C# functions. You can change the language by using the `-Runtime`

parameter, with supported values of `DotNet`

, `Java`

, `Node`

, `PowerShell`

, and `Python`

. Use the `-RuntimeVersion`

to choose a [specific language version](supported-languages#languages-by-runtime-version).This article contains the following examples:

[Create a serverless function app for C#](#create-a-serverless-function-app-for-c)[Create a serverless function app for Python](#create-a-serverless-function-app-for-python)[Create a scalable function app in a Premium plan](#create-a-scalable-function-app-in-a-premium-plan)[Create a function app in a Dedicated plan](#create-a-function-app-in-a-dedicated-plan)[Create a function app with a named Storage connection](#create-a-function-app-with-a-named-storage-connection)[Create a function app with an Azure Cosmos DB connection](#create-a-function-app-with-an-azure-cosmos-db-connection)[Create a function app with continuous deployment](#create-a-function-app-with-continuous-deployment)[Create a serverless Python function app and mount file share](#create-a-serverless-python-function-app-and-mount-file-share)

## Prerequisites

- If you choose to use Azure PowerShell locally:
[Install the latest version of the Az PowerShell module](/en-us/powershell/azure/install-azure-powershell).- Connect to your Azure account using the
[Connect-AzAccount](/en-us/powershell/module/az.accounts/connect-azaccount)cmdlet.

- If you choose to use Azure Cloud Shell:
- See
[Overview of Azure Cloud Shell](/en-us/azure/cloud-shell/overview)for more information.

- See

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Create a serverless function app for C#

The following script creates a serverless C# function app in the default Consumption plan:

```
# Function app and storage account names must be unique.
# Variable block
$randomIdentifier = Get-Random
$location = "eastus"
$resourceGroup = "msdocs-azure-functions-rg-$randomIdentifier"
$tag = @{script = "create-function-app-consumption"}
$storage = "msdocsaccount$randomIdentifier"
$functionApp = "msdocs-serverless-function-$randomIdentifier"
$skuStorage = "Standard_LRS"
$functionsVersion = "4"
# Create a resource group
Write-Host "Creating $resourceGroup in $location..."
New-AzResourceGroup -Name $resourceGroup -Location $location -Tag $tag
# Create an Azure storage account in the resource group.
Write-Host "Creating $storage"
New-AzStorageAccount -Name $storage -Location $location -ResourceGroupName $resourceGroup -SkuName $skuStorage
# Create a serverless function app in the resource group.
Write-Host "Creating $functionApp"
New-AzFunctionApp -Name $functionApp -StorageAccountName $storage -Location $location -ResourceGroupName $resourceGroup -Runtime DotNet-Isolated -FunctionsVersion $functionsVersion
```


## Create a serverless function app for Python

The following script creates a serverless Python function app in a Consumption plan:

```
# Function app and storage account names must be unique.
# Variable block
$randomIdentifier = Get-Random
$location = "eastus"
$resourceGroup = "msdocs-azure-functions-rg-$randomIdentifier"
$tag = @{script = "create-function-app-consumption-python"}
$storage = "msdocsaccount$randomIdentifier"
$functionApp = "msdocs-serverless-python-function-$randomIdentifier"
$skuStorage = "Standard_LRS"
$functionsVersion = "4"
$pythonVersion = "3.9" #Allowed values: 3.7, 3.8, and 3.9
# Create a resource group
Write-Host "Creating $resourceGroup in $location..."
New-AzResourceGroup -Name $resourceGroup -Location $location -Tag $tag
# Create an Azure storage account in the resource group.
Write-Host "Creating $storage"
New-AzStorageAccount -Name $storage -Location $location -ResourceGroupName $resourceGroup -SkuName $skuStorage
# Create a serverless Python function app in the resource group.
Write-Host "Creating $functionApp"
New-AzFunctionApp -Name $functionApp -StorageAccountName $storage -Location $location -ResourceGroupName $resourceGroup -OSType Linux -Runtime Python -RuntimeVersion $pythonVersion -FunctionsVersion $functionsVersion
```


## Create a scalable function app in a Premium plan

The following script creates a C# function app in an Elastic Premium plan that supports [dynamic scale](event-driven-scaling):

```
# Function app and storage account names must be unique.
# Variable block
$randomIdentifier = Get-Random
$location = "eastus"
$resourceGroup = "msdocs-azure-functions-rg-$randomIdentifier"
$tag = @{script = "create-function-app-premium-plan"}
$storage = "msdocsaccount$randomIdentifier"
$premiumPlan = "msdocs-premium-plan-$randomIdentifier"
$functionApp = "msdocs-function-$randomIdentifier"
$skuStorage = "Standard_LRS" # Allowed values: Standard_LRS, Standard_GRS, Standard_RAGRS, Standard_ZRS, Premium_LRS, Premium_ZRS, Standard_GZRS, Standard_RAGZRS
$skuPlan = "EP1"
$functionsVersion = "4"
# Create a resource group
Write-Host "Creating $resourceGroup in $location..."
New-AzResourceGroup -Name $resourceGroup -Location $location -Tag $tag
# Create an Azure storage account in the resource group.
Write-Host "Creating $storage"
New-AzStorageAccount -Name $storage -Location $location -ResourceGroupName $resourceGroup -SkuName $skuStorage
# Create a Premium plan
Write-Host "Creating $premiumPlan"
New-AzFunctionAppPlan -Name $premiumPlan -ResourceGroupName $resourceGroup -Location $location -Sku $skuPlan -WorkerType Windows
# Create a Function App
Write-Host "Creating $functionApp"
New-AzFunctionApp -Name $functionApp -StorageAccountName $storage -PlanName $premiumPlan -ResourceGroupName $resourceGroup -Runtime DotNet -FunctionsVersion $functionsVersion
```


## Create a function app in a Dedicated plan

The following script creates a function app hosted in a Dedicated plan, which isn't scaled dynamically by Functions:

```
# Function app and storage account names must be unique.
# Variable block
$randomIdentifier = Get-Random
$location = "eastus"
$resourceGroup = "msdocs-azure-functions-rg-$randomIdentifier"
$tag = @{script = "create-function-app-app-service-plan"}
$storage = "msdocsaccount$randomIdentifier"
$appServicePlan = "msdocs-app-service-plan-$randomIdentifier"
$functionApp = "msdocs-serverless-function-$randomIdentifier"
$skuStorage = "Standard_LRS"
$skuPlan = "B1"
$functionsVersion = "4"
# Create a resource group
Write-Host "Creating $resourceGroup in $location..."
New-AzResourceGroup -Name $resourceGroup -Location $location -Tag $tag
# Create an Azure storage account in the resource group.
Write-Host "Creating $storage"
New-AzStorageAccount -Name $storage -Location $location -ResourceGroupName $resourceGroup -SkuName $skuStorage
# Create an App Service plan
Write-Host "Creating $appServicePlan"
New-AzFunctionAppPlan -Name $appServicePlan -ResourceGroupName $resourceGroup -Location $location -Sku $skuPlan -WorkerType Windows
# Create a Function App
Write-Host "Creating $functionApp"
New-AzFunctionApp -Name $functionApp -StorageAccountName $storage -PlanName $appServicePlan -ResourceGroupName $resourceGroup -Runtime DotNet -FunctionsVersion $functionsVersion
```


## Create a function app with a named Storage connection

The following script creates a function app with a named Storage connection in application settings:

```
# Function app and storage account names must be unique.
# Variable block
$randomIdentifier = Get-Random
$location = "eastus"
$resourceGroup = "msdocs-azure-functions-rg-$randomIdentifier"
$tag = @{script = "create-function-app-connect-to-storage-account"}
$storage = "msdocsaccount$randomIdentifier"
$functionApp = "msdocs-serverless-function-$randomIdentifier"
$skuStorage = "Standard_LRS"
$functionsVersion = "4"
# Create a resource group
Write-Host "Creating $resourceGroup in $location..."
New-AzResourceGroup -Name $resourceGroup -Location $location -Tag $tag
# Create an Azure storage account in the resource group.
Write-Host "Creating $storage"
New-AzStorageAccount -Name $storage -Location $location -ResourceGroupName $resourceGroup -SkuName $skuStorage
# Create a serverless function app in the resource group.
Write-Host "Creating $functionApp"
New-AzFunctionApp -Name $functionApp -StorageAccountName $storage -Location $location -ResourceGroupName $resourceGroup -Runtime DotNet -FunctionsVersion $functionsVersion
# Get the storage account connection string.
$connstr = (Get-AzStorageAccount -StorageAccountName $storage -ResourceGroupName $resourceGroup).Context.ConnectionString
# Update function app settings to connect to the storage account.
Update-AzFunctionAppSetting -Name $functionApp -ResourceGroupName $resourceGroup -AppSetting @{StorageConStr = $connstr}
```


## Create a function app with an Azure Cosmos DB connection

The following script creates a function app and a connected Azure Cosmos DB account:

```
# Function app and storage account names must be unique.
# Variable block
$randomIdentifier = Get-Random
$location = "eastus"
$resourceGroup = "msdocs-azure-functions-rg-$randomIdentifier"
$tag = @{script = "create-function-app-connect-to-cosmos-db"}
$storage = "msdocsaccount$randomIdentifier"
$functionApp = "msdocs-serverless-function-$randomIdentifier"
$skuStorage = "Standard_LRS"
$functionsVersion = "4"
# Create a resource group
Write-Host "Creating $resourceGroup in $location..."
New-AzResourceGroup -Name $resourceGroup -Location $location -Tag $tag
# Create an Azure storage account in the resource group.
Write-Host "Creating $storage"
New-AzStorageAccount -Name $storage -Location $location -ResourceGroupName $resourceGroup -SkuName $skuStorage
# Create a serverless function app in the resource group.
Write-Host "Creating $functionApp"
New-AzFunctionApp -Name $functionApp -StorageAccountName $storage -Location $location -ResourceGroupName $resourceGroup -Runtime DotNet -FunctionsVersion $functionsVersion
# Create an Azure Cosmos DB database account using the same function app name.
Write-Host "Creating $functionApp"
New-AzCosmosDBAccount -Name $functionApp -ResourceGroupName $resourceGroup -Location $location
# Get the Azure Cosmos DB connection string.
$endpoint = (Get-AzCosmosDBAccount -Name $functionApp -ResourceGroupName $resourceGroup).DocumentEndpoint
Write-Host $endpoint
$key = (Get-AzCosmosDBAccountKey -Name $functionApp -ResourceGroupName $resourceGroup).PrimaryMasterKey
Write-Host $key
# Configure function app settings to use the Azure Cosmos DB connection string.
Update-AzFunctionAppSetting -Name $functionApp -ResourceGroupName $resourceGroup -AppSetting @{CosmosDB_Endpoint = $endpoint; CosmosDB_Key = $key}
```


## Create a function app with continuous deployment

The following script creates a function app that has continuous deployment configured to publish from a public GitHub repository:

```
# Function app and storage account names must be unique.
# Variable block
$randomIdentifier = Get-Random
$location = "eastus"
$resourceGroup = "msdocs-azure-functions-rg-$randomIdentifier"
$tag = @{script = "deploy-function-app-with-function-github"}
$storage = "msdocsaccount$randomIdentifier"
$functionApp = "mygithubfunc$randomIdentifier"
$skuStorage = "Standard_LRS"
$functionsVersion = "4"
$runtime = "Node"
# Public GitHub repository containing an Azure Functions code project.
$gitrepo = "https://github.com/Azure-Samples/functions-quickstart-javascript"
<# Set GitHub personal access token (PAT) to enable authenticated GitHub deployment in your subscription when using a private repo.
$token = <Replace with a GitHub access token when using a private repo.>
$propertiesObject = @{
token = $token
}
Set-AzResource -PropertyObject $propertiesObject -ResourceId /providers/Microsoft.Web/sourcecontrols/GitHub -ApiVersion 2018-02-01 -Force
#>
# Create a resource group
Write-Host "Creating $resourceGroup in $location..."
New-AzResourceGroup -Name $resourceGroup -Location $location -Tag $tag
# Create an Azure storage account in the resource group.
Write-Host "Creating $storage"
New-AzStorageAccount -Name $storage -Location $location -ResourceGroupName $resourceGroup -SkuName $skuStorage
# Create a function app in the resource group.
Write-Host "Creating $functionApp"
New-AzFunctionApp -Name $functionApp -StorageAccountName $storage -Location $location -ResourceGroupName $resourceGroup -Runtime $runtime -FunctionsVersion $functionsVersion
# Configure GitHub deployment from a public GitHub repo and deploy once.
$propertiesObject = @{
repoUrl = $gitrepo
branch = 'main'
isManualIntegration = $True # $False when using a private repo
}
Set-AzResource -PropertyObject $propertiesObject -ResourceGroupName $resourceGroup -ResourceType Microsoft.Web/sites/sourcecontrols -ResourceName $functionApp/web -ApiVersion 2018-02-01 -Force
# Connect to function application
Invoke-RestMethod -Uri "https://$functionApp.azurewebsites.net/api/httpexample?name=Azure"
```


## Create a serverless Python function app and mount file share

The following script creates a Python function app on Linux and creates and mounts an external Azure Files share:

```
# Function app and storage account names must be unique.
# Variable block
$randomIdentifier = Get-Random
$location = "eastus"
$resourceGroup = "msdocs-azure-functions-rg-$randomIdentifier"
$tag = @{script = "functions-cli-mount-files-storage-linux"}
$storage = "msdocsaccount$randomIdentifier"
$functionApp = "msdocs-serverless-function-$randomIdentifier"
$skuStorage = "Standard_LRS"
$functionsVersion = "4"
$pythonVersion = "3.9" #Allowed values: 3.7, 3.8, and 3.9
$share = "msdocs-fileshare-$randomIdentifier"
$directory = "msdocs-directory-$randomIdentifier"
$shareId = "msdocs-share-$randomIdentifier"
$mountPath = "/mounted-$randomIdentifier"
# Create a resource group
Write-Host "Creating $resourceGroup in $location..."
New-AzResourceGroup -Name $resourceGroup -Location $location -Tag $tag
# Create an Azure storage account in the resource group.
Write-Host "Creating $storage"
New-AzStorageAccount -Name $storage -Location $location -ResourceGroupName $resourceGroup -SkuName $skuStorage
# Get the storage account key.
$keys = Get-AzStorageAccountKey -Name $storage -ResourceGroupName $resourceGroup
$storageKey = $keys[0].Value
## Create a serverless Python function app in the resource group.
Write-Host "Creating $functionApp"
New-AzFunctionApp -Name $functionApp -StorageAccountName $storage -Location $location -ResourceGroupName $resourceGroup -OSType Linux -Runtime Python -RuntimeVersion $pythonVersion -FunctionsVersion $functionsVersion
# Create a share in Azure Files.
Write-Host "Creating $share"
$storageContext = New-AzStorageContext -StorageAccountName $storage -StorageAccountKey $storageKey
New-AzStorageShare -Name $share -Context $storageContext
# Create a directory in the share.
Write-Host "Creating $directory in $share"
New-AzStorageDirectory -ShareName $share -Path $directory -Context $storageContext
# Add a storage account configuration to the function app
Write-Host "Adding $storage configuration"
$storagePath = New-AzWebAppAzureStoragePath -Name $shareid -Type AzureFiles -ShareName $share -AccountName $storage -MountPath $mountPath -AccessKey $storageKey
Set-AzWebApp -Name $functionApp -ResourceGroupName $resourceGroup -AzureStoragePath $storagePath
# Get a function app's storage account configurations.
(Get-AzWebApp -Name $functionApp -ResourceGroupName $resourceGroup).AzureStoragePath
```


Mounted file shares are only supported on Linux. For more information, see [Mount file shares](storage-considerations#mount-file-shares).

## Clean up resources

In the preceding steps, you created Azure resources in a resource group. If you don't expect to need these resources in the future, delete the resource group by running the following PowerShell command:

```
Remove-AzResourceGroup -Name myResourceGroup
```


This command might take a minute to run.

## Next steps

For more information on Azure PowerShell, see [Azure PowerShell documentation](/en-us/powershell/azure).


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-openai-assistantpost-input.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai-assistantpost-input -->

# Azure OpenAI assistant post input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Azure OpenAI extension for Azure Functions is currently in preview.

The Azure OpenAI assistant post input binding lets you send prompts to assistant chat bots.

For information on setup and configuration details of the Azure OpenAI extension, see [Azure OpenAI extensions for Azure Functions](functions-bindings-openai). To learn more about Azure OpenAI assistants, see [Azure OpenAI Assistants API](/en-us/azure/ai-services/openai/concepts/assistants).

Note

References and examples are only provided for the [Node.js v4 model](functions-reference-node?pivots=nodejs-model-v4).

Note

References and examples are only provided for the [Python v2 model](functions-reference-python?pivots=python-mode-decorators#programming-model).

Note

While both C# process models are supported, only [isolated worker model](dotnet-isolated-process-guide) examples are provided.

## Example

This example demonstrates the creation process, where the HTTP POST function that sends user prompts to the assistant chat bot. The response to the prompt is returned in the HTTP response.

```
/// <summary>
/// HTTP POST function that sends user prompts to the assistant chat bot.
/// </summary>
[Function(nameof(PostUserQuery))]
public static IActionResult PostUserQuery(
[HttpTrigger(AuthorizationLevel.Anonymous, "post", Route = "assistants/{assistantId}")] HttpRequestData req,
string assistantId,
[AssistantPostInput("{assistantId}", "{Query.message}", ChatModel = "%CHAT_MODEL_DEPLOYMENT_NAME%", ChatStorageConnectionSetting = DefaultChatStorageConnectionSetting, CollectionName = DefaultCollectionName)] AssistantState state)
{
return new OkObjectResult(state.RecentMessages.Any() ? state.RecentMessages[state.RecentMessages.Count - 1].Content : "No response returned.");
}
```


This example demonstrates the creation process, where the HTTP POST function that sends user prompts to the assistant chat bot. The response to the prompt is returned in the HTTP response.

```
/*
* HTTP POST function that sends user prompts to the assistant chat bot.
*/
@FunctionName("PostUserResponse")
public HttpResponseMessage postUserResponse(
@HttpTrigger(
name = "req",
methods = {HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "assistants/{assistantId}")
HttpRequestMessage<Optional<String>> request,
@BindingName("assistantId") String assistantId,
@AssistantPost(name="newMessages", id = "{assistantId}", chatModel = "%CHAT_MODEL_DEPLOYMENT_NAME%", userMessage = "{Query.message}", chatStorageConnectionSetting = DEFAULT_CHATSTORAGE, collectionName = DEFAULT_COLLECTION) AssistantState state,
final ExecutionContext context) {
List<AssistantMessage> recentMessages = state.getRecentMessages();
String response = recentMessages.isEmpty() ? "No response returned." : recentMessages.get(recentMessages.size() - 1).getContent();
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(response)
.build();
}
```


This example demonstrates the creation process, where the HTTP POST function that sends user prompts to the assistant chat bot. The response to the prompt is returned in the HTTP response.

```
const { app, input, output } = require("@azure/functions");
const assistantPostInput = input.generic({
type: 'assistantPost',
id: '{assistantId}',
chatModel: '%CHAT_MODEL_DEPLOYMENT_NAME%',
userMessage: '{Query.message}',
chatStorageConnectionSetting: CHAT_STORAGE_CONNECTION_SETTING,
collectionName: COLLECTION_NAME
})
app.http('PostUserResponse', {
methods: ['POST'],
route: 'assistants/{assistantId}',
authLevel: 'anonymous',
extraInputs: [assistantPostInput],
handler: async (_, context) => {
const chatState = context.extraInputs.get(assistantPostInput)
const content = chatState.recentMessages[0].content
return {
status: 200,
body: content,
headers: {
'Content-Type': 'text/plain'
}
};
}
})
```


```
import { HttpRequest, InvocationContext, app, input, output } from "@azure/functions"
const assistantPostInput = input.generic({
type: 'assistantPost',
id: '{assistantId}',
chatModel: '%CHAT_MODEL_DEPLOYMENT_NAME%',
userMessage: '{Query.message}',
chatStorageConnectionSetting: CHAT_STORAGE_CONNECTION_SETTING,
collectionName: COLLECTION_NAME
})
app.http('PostUserResponse', {
methods: ['POST'],
route: 'assistants/{assistantId}',
authLevel: 'anonymous',
extraInputs: [assistantPostInput],
handler: async (_, context) => {
const chatState: any = context.extraInputs.get(assistantPostInput)
const content = chatState.recentMessages[0].content
return {
status: 200,
body: content,
headers: {
'Content-Type': 'text/plain'
}
};
}
})
```


This example demonstrates the creation process, where the HTTP POST function that sends user prompts to the assistant chat bot. The response to the prompt is returned in the HTTP response.

Here's the *function.json* file for post user query:

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
"post"
]
},
{
"type": "http",
"direction": "out",
"name": "Response"
},
{
"name": "State",
"type": "assistantPost",
"direction": "in",
"dataType": "string",
"id": "{assistantId}",
"userMessage": "{Query.message}",
"chatModel": "%CHAT_MODEL_DEPLOYMENT_NAME%",
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
$recent_message_content = "No recent messages!"
if ($State.recentMessages.Count -gt 0) {
$recent_message_content = $State.recentMessages[0].content
}
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $recent_message_content
Headers = @{
"Content-Type" = "text/plain"
}
})
```


This example demonstrates the creation process, where the HTTP POST function that sends user prompts to the assistant chat bot. The response to the prompt is returned in the HTTP response.

```
@apis.function_name("PostUserQuery")
@apis.route(route="assistants/{assistantId}", methods=["POST"])
@apis.assistant_post_input(
arg_name="state",
id="{assistantId}",
user_message="{Query.message}",
chat_model="%CHAT_MODEL_DEPLOYMENT_NAME%",
chat_storage_connection_setting=DEFAULT_CHAT_STORAGE_SETTING,
collection_name=DEFAULT_CHAT_COLLECTION_NAME,
)
def post_user_response(req: func.HttpRequest, state: str) -> func.HttpResponse:
# Parse the JSON string into a dictionary
data = json.loads(state)
# Extract the content of the recentMessage
recent_message_content = data["recentMessages"][0]["content"]
return func.HttpResponse(
recent_message_content, status_code=200, mimetype="text/plain"
)
```


## Attributes

Apply the `PostUserQuery`

attribute to define an assistant post input binding, which supports these parameters:

| Parameter | Description |
|---|---|
Id |
The ID of the assistant to update. |
UserMessage |
Gets or sets the user message for the chat completion model, encoded as a string. |
AIConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
ChatModel |
Optional. Gets or sets the ID of the model to use as a string, with a default value of `gpt-3.5-turbo` . |
Temperature |
Optional. Gets or sets the sampling temperature to use, as a string between `0` and `2` . Higher values (`0.8` ) make the output more random, while lower values like (`0.2` ) make output more focused and deterministic. You should use either `Temperature` or `TopP` , but not both. |
TopP |
Optional. Gets or sets an alternative to sampling with temperature, called nucleus sampling, as a string. In this sampling method, the model considers the results of the tokens with `top_p` probability mass. So `0.1` means only the tokens comprising the top 10% probability mass are considered. You should use either `Temperature` or `TopP` , but not both. |
MaxTokens |
Optional. Gets or sets the maximum number of tokens to generate in the completion, as a string with a default of `100` . The token count of your prompt plus `max_tokens` can't exceed the model's context length. Most models have a context length of 2,048 tokens (except for the newest models, which support 4096). |
IsReasoningModel |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Annotations

The `PostUserQuery`

annotation enables you to define an assistant post input binding, which supports these parameters:

| Element | Description |
|---|---|
name |
The name of the output binding. |
id |
The ID of the assistant to update. |
userMessage |
Gets or sets the user message for the chat completion model, encoded as a string. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
chatModel |
Gets or sets the ID of the model to use as a string, with a default value of `gpt-3.5-turbo` . |
temperature |
Optional. Gets or sets the sampling temperature to use, as a string between `0` and `2` . Higher values (`0.8` ) make the output more random, while lower values like (`0.2` ) make output more focused and deterministic. You should use either `Temperature` or `TopP` , but not both. |
topP |
Optional. Gets or sets an alternative to sampling with temperature, called nucleus sampling, as a string. In this sampling method, the model considers the results of the tokens with `top_p` probability mass. So `0.1` means only the tokens comprising the top 10% probability mass are considered. You should use either `Temperature` or `TopP` , but not both. |
maxTokens |
Optional. Gets or sets the maximum number of tokens to generate in the completion, as a string with a default of `100` . The token count of your prompt plus `max_tokens` can't exceed the model's context length. Most models have a context length of 2,048 tokens (except for the newest models, which support 4096). |
isReasoningModel |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Decorators

During the preview, define the output binding as a `generic_output_binding`

binding of type `postUserQuery`

, which supports these parameters:

| Parameter | Description |
|---|---|
arg_name |
The name of the variable that represents the binding parameter. |
id |
The ID of the assistant to update. |
user_message |
Gets or sets the user message for the chat completion model, encoded as a string. |
ai_connection_name |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
chat_model |
Gets or sets the ID of the model to use as a string, with a default value of `gpt-3.5-turbo` . |
temperature |
Optional. Gets or sets the sampling temperature to use, as a string between `0` and `2` . Higher values (`0.8` ) make the output more random, while lower values like (`0.2` ) make output more focused and deterministic. You should use either `Temperature` or `TopP` , but not both. |
top_p |
Optional. Gets or sets an alternative to sampling with temperature, called nucleus sampling, as a string. In this sampling method, the model considers the results of the tokens with `top_p` probability mass. So `0.1` means only the tokens comprising the top 10% probability mass are considered. You should use either `Temperature` or `TopP` , but not both. |
max_tokens |
Optional. Gets or sets the maximum number of tokens to generate in the completion, as a string with a default of `100` . The token count of your prompt plus `max_tokens` can't exceed the model's context length. Most models have a context length of 2,048 tokens (except for the newest models, which support 4096). |
is_reasoning _model |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Configuration

The binding supports these configuration properties that you set in the function.json file.

| Property | Description |
|---|---|
type |
Must be `PostUserQuery` . |
direction |
Must be `out` . |
name |
The name of the output binding. |
id |
The ID of the assistant to update. |
userMessage |
Gets or sets the user message for the chat completion model, encoded as a string. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
chatModel |
Gets or sets the ID of the model to use as a string, with a default value of `gpt-3.5-turbo` . |
temperature |
Optional. Gets or sets the sampling temperature to use, as a string between `0` and `2` . Higher values (`0.8` ) make the output more random, while lower values like (`0.2` ) make output more focused and deterministic. You should use either `Temperature` or `TopP` , but not both. |
topP |
Optional. Gets or sets an alternative to sampling with temperature, called nucleus sampling, as a string. In this sampling method, the model considers the results of the tokens with `top_p` probability mass. So `0.1` means only the tokens comprising the top 10% probability mass are considered. You should use either `Temperature` or `TopP` , but not both. |
maxTokens |
Optional. Gets or sets the maximum number of tokens to generate in the completion, as a string with a default of `100` . The token count of your prompt plus `max_tokens` can't exceed the model's context length. Most models have a context length of 2,048 tokens (except for the newest models, which support 4096). |
isReasoningModel |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Configuration

The binding supports these properties, which are defined in your code:

| Property | Description |
|---|---|
id |
The ID of the assistant to update. |
userMessage |
Gets or sets the user message for the chat completion model, encoded as a string. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
chatModel |
Gets or sets the ID of the model to use as a string, with a default value of `gpt-3.5-turbo` . |
temperature |
Optional. Gets or sets the sampling temperature to use, as a string between `0` and `2` . Higher values (`0.8` ) make the output more random, while lower values like (`0.2` ) make output more focused and deterministic. You should use either `Temperature` or `TopP` , but not both. |
topP |
Optional. Gets or sets an alternative to sampling with temperature, called nucleus sampling, as a string. In this sampling method, the model considers the results of the tokens with `top_p` probability mass. So `0.1` means only the tokens comprising the top 10% probability mass are considered. You should use either `Temperature` or `TopP` , but not both. |
maxTokens |
Optional. Gets or sets the maximum number of tokens to generate in the completion, as a string with a default of `100` . The token count of your prompt plus `max_tokens` can't exceed the model's context length. Most models have a context length of 2,048 tokens (except for the newest models, which support 4096). |
isReasoningModel |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Usage

See the [Example section](#example) for complete examples.


---

<!-- DOCUMENTO FUSIONADO: functions-dotnet-class-library.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-dotnet-class-library -->

# Develop legacy C# class library functions using Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

This article is an introduction to developing Azure Functions by using C# in .NET class libraries. These class libraries are used to run *in-process with the Functions runtime*. Your .NET functions can alternatively run _isolated from the Functions *runtime*, which offers several advantages. To learn more, see [the isolated worker model](dotnet-isolated-process-guide). For a comprehensive comparison between these two models, see [Differences between the in-process model and the isolated worker model](dotnet-isolated-in-process-differences).

Important

This article supports .NET class library functions that run in-process with the runtime. Your C# functions can also run out-of-process and isolated from the Functions runtime. The isolated worker process model is the only way to run non-LTS versions of .NET and .NET Framework apps in current versions of the Functions runtime. To learn more, see [.NET isolated worker process functions](dotnet-isolated-process-guide).
For a comprehensive comparison between isolated worker process and in-process .NET Functions, see [Differences between in-process and isolate worker process .NET Azure Functions](dotnet-isolated-in-process-differences).

As a C# developer, you might also be interested in one of the following articles:

| Getting started | Concepts | Guided learning/samples |
|---|---|---|

Azure Functions supports C# and C# script programming languages. If you're looking for guidance on [using C# in the Azure portal](functions-create-function-app-portal), see [C# script (.csx) developer reference](functions-reference-csharp).

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

### Updating to target .NET 8

Apps using the in-process model can target .NET 8 by following the steps outlined in this section. However, if you choose to exercise this option, you should still begin planning your [migration to the isolated worker model](migrate-dotnet-to-isolated-model) in advance of [support ending for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model).

Many apps can change the configuration of the function app in Azure without updates to code or redeployment. To run .NET 8 with the in-process model, three configurations are required:

- The
[application setting](functions-how-to-use-azure-function-app-settings)`FUNCTIONS_WORKER_RUNTIME`

must be set with the value "dotnet". - The application setting
`FUNCTIONS_EXTENSION_VERSION`

must be set with the value "~4". - The application setting
`FUNCTIONS_INPROC_NET8_ENABLED`

must be set with the value "1". - You must
[update the stack configuration](update-language-versions#update-the-stack-configuration)to reference .NET 8.

Support for .NET 8 still uses version 4.x of the Functions runtime, and no change to the configured runtime version is required.

To update your local project, first make sure you're using the latest versions of local tools. Then ensure that the project references [version 4.4.0 or later of Microsoft.NET.Sdk.Functions](https://www.nuget.org/packages/Microsoft.NET.Sdk.Functions/4.4.0). You can then change your `TargetFramework`

to "net8.0". You must also update `local.settings.json`

to include both `FUNCTIONS_WORKER_RUNTIME`

set to "dotnet" and `FUNCTIONS_INPROC_NET8_ENABLED`

set to "1".

The following example is a minimal `project`

file with these changes:

```
<Project Sdk="Microsoft.NET.Sdk">
<PropertyGroup>
<TargetFramework>net8.0</TargetFramework>
<AzureFunctionsVersion>v4</AzureFunctionsVersion>
</PropertyGroup>
<ItemGroup>
<PackageReference Include="Microsoft.NET.Sdk.Functions" Version="4.4.0" />
</ItemGroup>
<ItemGroup>
<None Update="host.json">
<CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
</None>
<None Update="local.settings.json">
<CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
<CopyToPublishDirectory>Never</CopyToPublishDirectory>
</None>
</ItemGroup>
</Project>
```


The following example is a minimal `local.settings.json`

file with these changes:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "UseDevelopmentStorage=true",
"FUNCTIONS_INPROC_NET8_ENABLED": "1",
"FUNCTIONS_WORKER_RUNTIME": "dotnet"
}
}
```


If your app uses [ Microsoft.Azure.DurableTask.Netherite.AzureFunctions](https://www.nuget.org/packages/Microsoft.Azure.DurableTask.Netherite.AzureFunctions), ensure it targets version 1.5.3 or later. Due to a behavior change in .NET 8, apps with older versions of the package throw an ambiguous constructor exception.

You might need to make other changes to your app based on the version support of its other dependencies.

Version 4.x of the Functions runtime provides equivalent functionality for .NET 6 and .NET 8. The in-process model doesn't include other features or updates that integrate with new .NET 8 capabilities. For example, the runtime doesn't support keyed services. To take full advantage of the latest .NET 8 capabilities and enhancements, you must [migrate to the isolated worker model](migrate-dotnet-to-isolated-model).

## Functions class library project

In Visual Studio, the **Azure Functions** project template creates a C# class library project that contains the following files:

[host.json](functions-host-json)- stores configuration settings that affect all functions in the project when running locally or in Azure.[local.settings.json](functions-develop-local#local-settings-file)- stores app settings and connection strings that are used when running locally. This file contains secrets and isn't published to your function app in Azure. Instead,[add app settings to your function app](functions-develop-vs#function-app-settings).

When you build the project, a folder structure that looks like the following example is generated in the build output directory:

```
<framework.version>
| - bin
| - MyFirstFunction
| | - function.json
| - MySecondFunction
| | - function.json
| - host.json
```


This directory is what gets deployed to your function app in Azure. The binding extensions required in [version 2.x](functions-versions) of the Functions runtime are [added to the project as NuGet packages](functions-develop-vs?tabs=in-process#add-bindings).

Important

The build process creates a *function.json* file for each function. This *function.json* file isn't meant to be edited directly. You can't change binding configuration or disable the function by editing this file. To learn how to disable a function, see [How to disable functions](disable-function).

## Methods recognized as functions

In a class library, a function is a method with a `FunctionName`

and a trigger attribute, as shown in the following example:

```
public static class SimpleExample
{
[FunctionName("QueueTrigger")]
public static void Run(
[QueueTrigger("myqueue-items")] string myQueueItem,
ILogger log)
{
log.LogInformation($"C# function processed: {myQueueItem}");
}
}
```


The `FunctionName`

attribute marks the method as a function entry point. The name must be unique within a project, start with a letter and only contain letters, numbers, `_`

, and `-`

, up to 127 characters in length. Project templates often create a method named `Run`

, but the method name can be any valid C# method name. The preceding example shows a static method being used, but functions aren't required to be static.

The trigger attribute specifies the trigger type and binds input data to a method parameter. The example function is triggered by a queue message, and the queue message is passed to the method in the `myQueueItem`

parameter.

## Method signature parameters

The method signature might contain parameters other than the one used with the trigger attribute. Here are some of the other parameters that you can include:

[Input and output bindings](functions-triggers-bindings)marked as such by decorating them with attributes.- An
`ILogger`

or`TraceWriter`

([version 1.x-only](functions-versions#creating-1x-apps)) parameter for[logging](#logging). - A
`CancellationToken`

parameter for[graceful shutdown](#cancellation-tokens). [Binding expressions](functions-bindings-expressions-patterns)parameters to get trigger metadata.

The order of parameters in the function signature doesn't matter. For example, you can put trigger parameters before or after other bindings, and you can put the logger parameter before or after trigger or binding parameters.

### Output bindings

A function can have zero or multiple output bindings defined by using output parameters.

The following example modifies the preceding one by adding an output queue binding named `myQueueItemCopy`

. The function writes the contents of the message that triggers the function to a new message in a different queue.

```
public static class SimpleExampleWithOutput
{
[FunctionName("CopyQueueMessage")]
public static void Run(
[QueueTrigger("myqueue-items-source")] string myQueueItem,
[Queue("myqueue-items-destination")] out string myQueueItemCopy,
ILogger log)
{
log.LogInformation($"CopyQueueMessage function processed: {myQueueItem}");
myQueueItemCopy = myQueueItem;
}
}
```


Values assigned to output bindings are written when the function exits. You can use more than one output binding in a function by assigning values to multiple output parameters.

The binding reference articles ([Storage queues](functions-bindings-storage-queue), for example) explain which parameter types you can use with trigger, input, or output binding attributes.

### Binding expressions example

The following code gets the name of the queue to monitor from an app setting, and it gets the queue message creation time in the `insertionTime`

parameter.

```
public static class BindingExpressionsExample
{
[FunctionName("LogQueueMessage")]
public static void Run(
[QueueTrigger("%queueappsetting%")] string myQueueItem,
DateTimeOffset insertionTime,
ILogger log)
{
log.LogInformation($"Message content: {myQueueItem}");
log.LogInformation($"Created at: {insertionTime}");
}
}
```


## Autogenerated function.json

The build process creates a *function.json* file in a function folder in the build folder. As noted earlier, this file isn't meant to be edited directly. You can't change binding configuration or disable the function by editing this file.

The purpose of this file is to provide information to the scale controller to use for [scaling decisions on the Consumption plan](event-driven-scaling). For this reason, the file only has trigger info, not input/output bindings.

The generated *function.json* file includes a `configurationSource`

property that tells the runtime to use .NET attributes for bindings, rather than *function.json* configuration. Here's an example:

```
{
"generatedBy": "Microsoft.NET.Sdk.Functions-1.0.0.0",
"configurationSource": "attributes",
"bindings": [
{
"type": "queueTrigger",
"queueName": "%input-queue-name%",
"name": "myQueueItem"
}
],
"disabled": false,
"scriptFile": "..\\bin\\FunctionApp1.dll",
"entryPoint": "FunctionApp1.QueueTrigger.Run"
}
```


## Microsoft.NET.Sdk.Functions

The *function.json* file generation is performed by the NuGet package [Microsoft.NET.Sdk.Functions](https://www.nuget.org/packages/Microsoft.NET.Sdk.Functions).

The following example shows the relevant parts of the `.csproj`

files that have different target frameworks of the same `Sdk`

package:

```
<PropertyGroup>
<TargetFramework>net8.0</TargetFramework>
<AzureFunctionsVersion>v4</AzureFunctionsVersion>
</PropertyGroup>
<ItemGroup>
<PackageReference Include="Microsoft.NET.Sdk.Functions" Version="4.5.0" />
</ItemGroup>
```


Important

Starting with version 4.0.6517 of the Core Tools, in-process model projects must reference [version 4.5.0 or later of Microsoft.NET.Sdk.Functions](https://www.nuget.org/packages/Microsoft.NET.Sdk.Functions/4.5.0). If an earlier version is used, the

`func start`

command will error.Among the `Sdk`

package dependencies are triggers and bindings. A 1.x project refers to 1.x triggers and bindings because those triggers and bindings target the .NET Framework, while 4.x triggers and bindings target .NET Core.

The `Sdk`

package also depends on [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json), and indirectly on [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage). These dependencies make sure that your project uses the versions of those packages that work with the Functions runtime version that the project targets. For example, `Newtonsoft.Json`

has version 11 for .NET Framework 4.6.1, but the Functions runtime that targets .NET Framework 4.6.1 is only compatible with `Newtonsoft.Json`

9.0.1. So your function code in that project also has to use `Newtonsoft.Json`

9.0.1.

The source code for `Microsoft.NET.Sdk.Functions`

is available in the GitHub repo [azure-functions-vs-build-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).

## Local runtime version

Visual Studio uses the [Azure Functions Core Tools](functions-run-local#install-the-azure-functions-core-tools) to run Functions projects on your local computer. The Core Tools is a command-line interface for the Functions runtime.

If you install the Core Tools using the Windows installer (MSI) package or by using npm, it doesn't affect the Core Tools version used by Visual Studio. For the Functions runtime version 1.x, Visual Studio stores Core Tools versions in *%USERPROFILE%\AppData\Local\Azure.Functions.Cli* and uses the latest version stored there. For Functions 4.x, the Core Tools are included in the **Azure Functions and Web Jobs Tools** extension. For Functions 1.x, you can see what version is being used in the console output when you run a Functions project:

```
[3/1/2018 9:59:53 AM] Starting Host (HostId=contoso2-1518597420, Version=2.0.11353.0, ProcessId=22020, Debug=False, Attempt=0, FunctionsExtensionVersion=)
```


## ReadyToRun

You can compile your function app as [ReadyToRun binaries](/en-us/dotnet/core/deploying/ready-to-run). ReadyToRun is a form of ahead-of-time compilation that can improve startup performance to help reduce the impact of [cold-start](event-driven-scaling#cold-start) when running in a [Consumption plan](consumption-plan).

ReadyToRun is available in .NET 6 and later versions and requires [version 4.0 of the Azure Functions runtime](functions-versions).

To compile your project as ReadyToRun, update your project file by adding the `<PublishReadyToRun>`

and `<RuntimeIdentifier>`

elements. The following example is the configuration for publishing to a Windows 32-bit function app.

```
<PropertyGroup>
<TargetFramework>net8.0</TargetFramework>
<AzureFunctionsVersion>v4</AzureFunctionsVersion>
<PublishReadyToRun>true</PublishReadyToRun>
<RuntimeIdentifier>win-x86</RuntimeIdentifier>
</PropertyGroup>
```


Important

Starting in .NET 6, support for Composite ReadyToRun compilation has been added. Check out [ReadyToRun Cross platform and architecture restrictions](/en-us/dotnet/core/deploying/ready-to-run).

You can also build your app with ReadyToRun from the command line. For more information, see the `-p:PublishReadyToRun=true`

option in [ dotnet publish](/en-us/dotnet/core/tools/dotnet-publish).

## Supported types for bindings

Each binding has its own supported types; for instance, a blob trigger attribute can be applied to a string parameter, a POCO parameter, a `CloudBlockBlob`

parameter, or any of several other supported types. The [binding reference article for blob bindings](functions-bindings-storage-blob-trigger#usage) lists all supported parameter types. For more information, see [Triggers and bindings](functions-triggers-bindings) and the [binding reference docs for each binding type](functions-triggers-bindings#related-content).

Tip

If you plan to use the HTTP or WebHook bindings, plan to avoid port exhaustion that can be caused by improper instantiation of `HttpClient`

. For more information, see [How to manage connections in Azure Functions](manage-connections).

## Binding to method return value

You can use a method return value for an output binding, by applying the attribute to the method return value. For examples, see [Triggers and bindings](functions-triggers-bindings).

Use the return value only if a successful function execution always results in a return value to pass to the output binding. Otherwise, use `ICollector`

or `IAsyncCollector`

, as shown in the following section.

## Writing multiple output values

To write multiple values to an output binding, or if a successful function invocation might not result in anything to pass to the output binding, use the [ ICollector](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or

[types. These types are write-only collections that are written to the output binding when the method completes.](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs)

`IAsyncCollector`

This example writes multiple queue messages into the same queue using `ICollector`

:

```
public static class ICollectorExample
{
[FunctionName("CopyQueueMessageICollector")]
public static void Run(
[QueueTrigger("myqueue-items-source-3")] string myQueueItem,
[Queue("myqueue-items-destination")] ICollector<string> myDestinationQueue,
ILogger log)
{
log.LogInformation($"C# function processed: {myQueueItem}");
myDestinationQueue.Add($"Copy 1: {myQueueItem}");
myDestinationQueue.Add($"Copy 2: {myQueueItem}");
}
}
```


## Async

To make a function [asynchronous](/en-us/dotnet/csharp/programming-guide/concepts/async/), use the `async`

keyword and return a `Task`

object.

```
public static class AsyncExample
{
[FunctionName("BlobCopy")]
public static async Task RunAsync(
[BlobTrigger("sample-images/{blobName}")] Stream blobInput,
[Blob("sample-images-copies/{blobName}", FileAccess.Write)] Stream blobOutput,
CancellationToken token,
ILogger log)
{
log.LogInformation($"BlobCopy function processed.");
await blobInput.CopyToAsync(blobOutput, 4096, token);
}
}
```


You can't use `out`

parameters in async functions. For output bindings, use the [function return value](#binding-to-method-return-value) or a [collector object](#writing-multiple-output-values) instead.

## Cancellation tokens

A function can accept a [CancellationToken](/en-us/dotnet/api/system.threading.cancellationtoken) parameter, which enables the operating system to notify your code when the function is about to be terminated. You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.

Consider the case when you have a function that processes messages in batches. The following Azure Service Bus-triggered function processes an array of [ServiceBusReceivedMessage](/en-us/dotnet/api/azure.messaging.servicebus.servicebusreceivedmessage) objects, which represents a batch of incoming messages to be processed by a specific function invocation:

```
using Azure.Messaging.ServiceBus;
using System.Threading;
namespace ServiceBusCancellationToken
{
public static class servicebus
{
[FunctionName("servicebus")]
public static void Run([ServiceBusTrigger("csharpguitar", Connection = "SB_CONN")]
ServiceBusReceivedMessage[] messages, CancellationToken cancellationToken, ILogger log)
{
try
{
foreach (var message in messages)
{
if (cancellationToken.IsCancellationRequested)
{
log.LogInformation("A cancellation token was received. Taking precautionary actions.");
//Take precautions like noting how far along you are with processing the batch
log.LogInformation("Precautionary activities --complete--.");
break;
}
else
{
//business logic as usual
log.LogInformation($"Message: {message} was processed.");
}
}
}
catch (Exception ex)
{
log.LogInformation($"Something unexpected happened: {ex.Message}");
}
}
}
}
```


## Logging

In your function code, you can write output to logs that appear as traces in Application Insights. The recommended way to write to the logs is to include a parameter of type [ILogger](/en-us/dotnet/api/microsoft.extensions.logging.ilogger), which is typically named `log`

. Version 1.x of the Functions runtime used `TraceWriter`

, which also writes to Application Insights, but doesn't support structured logging. Don't use `Console.Write`

to write your logs, since this data isn't captured by Application Insights.

### ILogger

In your function definition, include an [ILogger](/en-us/dotnet/api/microsoft.extensions.logging.ilogger) parameter, which supports [structured logging](https://softwareengineering.stackexchange.com/questions/312197/benefits-of-structured-logging-vs-basic-logging).

With an `ILogger`

object, you call `Log<level>`

[extension methods on ILogger](/en-us/dotnet/api/microsoft.extensions.logging.loggerextensions#methods) to create logs. The following code writes `Information`

logs with category `Function.<YOUR_FUNCTION_NAME>.User.`

:

```
public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, ILogger logger)
{
logger.LogInformation("Request for item with key={itemKey}.", id);
```


To learn more about how Functions implements `ILogger`

, see [Collecting telemetry data](functions-monitoring#collecting-telemetry-data). Categories prefixed with `Function`

assume you're using an `ILogger`

instance. If you choose to instead use an `ILogger<T>`

, the category name might instead be based on `T`

.

### Structured logging

The order of placeholders, not their names, determines which parameters are used in the log message. Suppose you have the following code:

```
string partitionKey = "partitionKey";
string rowKey = "rowKey";
logger.LogInformation("partitionKey={partitionKey}, rowKey={rowKey}", partitionKey, rowKey);
```


If you keep the same message string and reverse the order of the parameters, the resulting message text would have the values in the wrong places.

Placeholders are handled this way so that you can do structured logging. Application Insights stores the parameter name-value pairs and the message string. The result is that the message arguments become fields that you can query on.

If your logger method call looks like the previous example, you can query the field `customDimensions.prop__rowKey`

. The `prop__`

prefix is added to ensure there are no collisions between fields the runtime adds and fields your function code adds.

You can also query on the original message string by referencing the field `customDimensions.prop__{OriginalFormat}`

.

Here's a sample JSON representation of `customDimensions`

data:

```
{
"customDimensions": {
"prop__{OriginalFormat}":"C# Queue trigger function processed: {message}",
"Category":"Function",
"LogLevel":"Information",
"prop__message":"c9519cbf-b1e6-4b9b-bf24-cb7d10b1bb89"
}
}
```


### Log custom telemetry

There's a Functions-specific version of the Application Insights SDK that you can use to send custom telemetry data from your functions to Application Insights: [Microsoft.Azure.WebJobs.Logging.ApplicationInsights](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Logging.ApplicationInsights). Use the following command from the command prompt to install this package:

```
dotnet add package Microsoft.Azure.WebJobs.Logging.ApplicationInsights --version <VERSION>
```


In this command, replace `<VERSION>`

with a version of this package that supports your installed version of [Microsoft.Azure.WebJobs](https://www.nuget.org/packages/Microsoft.Azure.WebJobs/).

The following C# examples uses the [custom telemetry API](/en-us/azure/azure-monitor/app/api-custom-events-metrics). The example is for a .NET class library, but the Application Insights code is the same for C# script.

Version 2.x and later versions of the runtime use newer features in Application Insights to automatically correlate telemetry with the current operation. There's no need to manually set the operation `Id`

, `ParentId`

, or `Name`

fields.

```
using System;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Logging;
using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;
using Microsoft.ApplicationInsights.Extensibility;
using System.Linq;
namespace functionapp0915
{
public class HttpTrigger2
{
private readonly TelemetryClient telemetryClient;
/// Using dependency injection will guarantee that you use the same configuration for telemetry collected automatically and manually.
public HttpTrigger2(TelemetryConfiguration telemetryConfiguration)
{
this.telemetryClient = new TelemetryClient(telemetryConfiguration);
}
[FunctionName("HttpTrigger2")]
public Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = null)]
HttpRequest req, ExecutionContext context, ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
DateTime start = DateTime.UtcNow;
// Parse query parameter
string name = req.Query
.FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
.Value;
// Write an event to the customEvents table.
var evt = new EventTelemetry("Function called");
evt.Context.User.Id = name;
this.telemetryClient.TrackEvent(evt);
// Generate a custom metric, in this case let's use ContentLength.
this.telemetryClient.GetMetric("contentLength").TrackValue(req.ContentLength);
// Log a custom dependency in the dependencies table.
var dependency = new DependencyTelemetry
{
Name = "GET api/planets/1/",
Target = "swapi.co",
Data = "https://swapi.co/api/planets/1/",
Timestamp = start,
Duration = DateTime.UtcNow - start,
Success = true
};
dependency.Context.User.Id = name;
this.telemetryClient.TrackDependency(dependency);
return Task.FromResult<IActionResult>(new OkResult());
}
}
}
```


In this example, the custom metric data gets aggregated by the host before being sent to the customMetrics table. To learn more, see the [GetMetric](/en-us/azure/azure-monitor/app/api-custom-events-metrics#getmetric) documentation in Application Insights.

When running locally, you must add the `APPINSIGHTS_INSTRUMENTATIONKEY`

setting, with the Application Insights key, to the [local.settings.json](functions-develop-local#local-settings-file) file.

Don't call `TrackRequest`

or `StartOperation<RequestTelemetry>`

because you see duplicate requests for a function invocation. The Functions runtime automatically tracks requests.

Don't set `telemetryClient.Context.Operation.Id`

. This global setting causes incorrect correlation when many functions are running simultaneously. Instead, create a new telemetry instance (`DependencyTelemetry`

, `EventTelemetry`

) and modify its `Context`

property. Then pass in the telemetry instance to the corresponding `Track`

method on `TelemetryClient`

(`TrackDependency()`

, `TrackEvent()`

, `TrackMetric()`

). This method ensures that the telemetry has the correct correlation details for the current function invocation.

## Testing functions

The following articles show how to run an in-process C# class library function locally for testing purposes:

## Environment variables

To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`

, as shown in the following code example:

```
public static class EnvironmentVariablesExample
{
[FunctionName("GetEnvironmentVariables")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, ILogger log)
{
log.LogInformation($"C# Timer trigger function executed at: {DateTime.Now}");
log.LogInformation(GetEnvironmentVariable("AzureWebJobsStorage"));
log.LogInformation(GetEnvironmentVariable("WEBSITE_SITE_NAME"));
}
private static string GetEnvironmentVariable(string name)
{
return name + ": " +
System.Environment.GetEnvironmentVariable(name, EnvironmentVariableTarget.Process);
}
}
```


App settings can be read from environment variables both when developing locally and when running in Azure. When developing locally, app settings come from the `Values`

collection in the *local.settings.json* file. In both environments, local and Azure, `GetEnvironmentVariable("<app setting name>")`

retrieves the value of the named app setting. For instance, when you're running locally, "My Site Name" would be returned if your *local.settings.json* file contains `{ "Values": { "WEBSITE_SITE_NAME": "My Site Name" } }`

.

The [System.Configuration.ConfigurationManager.AppSettings](/en-us/dotnet/api/system.configuration.configurationmanager.appsettings) property is an alternative API for getting app setting values, but we recommend that you use `GetEnvironmentVariable`

as shown here.

## Binding at runtime

In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed to the [ declarative](https://en.wikipedia.org/wiki/Declarative_programming) bindings in attributes. Imperative binding is useful when binding parameters need to be computed at runtime rather than design time. With this pattern, you can bind to supported input and output bindings on-the-fly in your function code.

Define an imperative binding as follows:

**Do not**include an attribute in the function signature for your desired imperative bindings.Pass in an input parameter

or`Binder binder`

.`IBinder binder`

Use the following C# pattern to perform the data binding.

`using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...))) { ... }`

`BindingTypeAttribute`

is the .NET attribute that defines your binding, and`T`

is an input or output type that's supported by that binding type.`T`

can't be an`out`

parameter type (such as`out JObject`

). For example, the Mobile Apps table output binding supports[six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use[ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs)or[IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs)with imperative binding.

### Single attribute example

The following example code creates a [Storage blob output binding](functions-bindings-storage-blob-output) with blob path that's defined at run time, then writes a string to the blob.

```
public static class IBinderExample
{
[FunctionName("CreateBlobUsingBinder")]
public static void Run(
[QueueTrigger("myqueue-items-source-4")] string myQueueItem,
IBinder binder,
ILogger log)
{
log.LogInformation($"CreateBlobUsingBinder function processed: {myQueueItem}");
using (var writer = binder.Bind<TextWriter>(new BlobAttribute(
$"samples-output/{myQueueItem}", FileAccess.Write)))
{
writer.Write("Hello World!");
};
}
}
```


[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Extensions.Storage/Blobs/BlobAttribute.cs) defines the [Storage blob](functions-bindings-storage-blob) input or output binding, and [TextWriter](/en-us/dotnet/api/system.io.textwriter) is a supported output binding type.

### Multiple attributes example

The preceding example gets the app setting for the function app's main Storage account connection string (which is `AzureWebJobsStorage`

). You can specify a custom app setting to use for the Storage account by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing the attribute array into `BindAsync<T>()`

. Use a `Binder`

parameter, not `IBinder`

. For example:

```
public static class IBinderExampleMultipleAttributes
{
[FunctionName("CreateBlobInDifferentStorageAccount")]
public async static Task RunAsync(
[QueueTrigger("myqueue-items-source-binder2")] string myQueueItem,
Binder binder,
ILogger log)
{
log.LogInformation($"CreateBlobInDifferentStorageAccount function processed: {myQueueItem}");
var attributes = new Attribute[]
{
new BlobAttribute($"samples-output/{myQueueItem}", FileAccess.Write),
new StorageAccountAttribute("MyStorageAccount")
};
using (var writer = await binder.BindAsync<TextWriter>(attributes))
{
await writer.WriteAsync("Hello World!!");
}
}
}
```


## Triggers and bindings

This table shows the bindings that are supported in the major versions of the Azure Functions runtime:

| Type | 4.x1 |
1.x2 |
Trigger | Input | Output |
|---|---|---|---|---|---|
|

[Azure Cosmos DB](functions-bindings-cosmosdb-v2)[Azure Data Explorer](functions-bindings-azure-data-explorer)[Azure SQL](functions-bindings-azure-sql)[Dapr](functions-bindings-dapr)4[Event Grid](functions-bindings-event-grid)[Event Hubs](functions-bindings-event-hubs)[HTTP and webhooks](functions-bindings-http-webhook)[IoT Hub](functions-bindings-event-iot)[Kafka](functions-bindings-kafka)3[Mobile Apps](functions-bindings-mobile-apps)[Model Context Protocol](functions-bindings-mcp)[Notification Hubs](functions-bindings-notification-hubs)[Queue Storage](functions-bindings-storage-queue)[Redis](functions-bindings-cache)[RabbitMQ](functions-bindings-rabbitmq)3[SendGrid](functions-bindings-sendgrid)[Service Bus](functions-bindings-service-bus)[Azure SignalR Service](functions-bindings-signalr-service)[Table Storage](functions-bindings-storage-table)[Timer](functions-bindings-timer)[Twilio](functions-bindings-twilio)- Register all bindings except HTTP and timer. See
[Register Azure Functions binding extensions](functions-bindings-register). This step isn't required when using version 1.x of the Functions runtime. [Support ends for version 1.x of the Azure Functions runtime on September 14, 2026](https://aka.ms/azure-functions-retirements/hostv1).[Migrate your apps to version 4.x](migrate-version-1-version-4)for full support.- Triggers aren't supported in the Consumption plan. This binding type requires
[runtime-driven triggers](functions-networking-options#elastic-premium-plan-with-virtual-network-triggers). - This binding type is supported in Kubernetes, Azure IoT Edge, and other self-hosted modes only.
