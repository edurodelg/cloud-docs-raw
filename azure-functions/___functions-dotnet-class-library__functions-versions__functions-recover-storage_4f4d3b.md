---
merged_at: 2026-02-01T08:17:25.341042
merged_files: 2
---


---
<!-- Source: N/A -->

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

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-recover-storage-account -->

# Troubleshoot error: "Azure Functions Runtime is unreachable"

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article helps you troubleshoot the following error string that appears in the Azure portal:

"Error: Azure Functions Runtime is unreachable. Click here for details on storage configuration."


This issue occurs when the Functions runtime can't start. The most common reason for this is that the function app lost access to its storage account. For more information, see [Storage account requirements](storage-considerations#storage-account-requirements).

The rest of this article helps you troubleshoot specific causes of this error, including how to identify and resolve each case.

## Storage account was deleted

Every function app requires a storage account that is used by the Functions host to operate. If that default host storage account is deleted, your function app won't run.

Start by looking up your storage account name in your application settings. Either `AzureWebJobsStorage`

or `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

contains the name of your storage account as part of a connection string. For more information, see [App settings reference for Azure Functions](functions-app-settings#azurewebjobsstorage).

Search for your storage account in the Azure portal to see whether it still exists. If it has been deleted, re-create the storage account and replace your storage connection strings. Your function code is lost, and you need to redeploy it.

## Storage account application settings were deleted

In the preceding step, if you can't find a storage account connection string, it was likely deleted or overwritten. Deleting application settings most commonly happens when you're using deployment slots or Azure Resource Manager scripts to set application settings.

### Required application settings

- Required:
- Required for Elastic Premium and Consumption plan functions:

For more information, see [App settings reference for Azure Functions](functions-app-settings).

### Guidance

- Don't check
**slot setting**for any of these settings. If you swap deployment slots, the function app breaks. - Don't modify these settings as part of automated deployments.
- These settings must be provided and valid at creation time. An automated deployment that doesn't contain these settings results in a function app that doesn't run, even if the settings are added later.

## Storage account credentials are invalid

The previously discussed storage account connection strings must be updated if you regenerate storage keys. For more information about storage key management, see [Create an Azure Storage account](../storage/common/storage-account-create).

## Storage account is inaccessible

Your function app must be able to access the storage account. Common issues that block a function app's access to a storage account are:

The function app is deployed to your App Service Environment (ASE) without the correct network rules to allow traffic to and from the storage account.

The storage account firewall is enabled and not configured to allow traffic to and from functions. For more information, see

[Configure Azure Storage firewalls and virtual networks](../storage/common/storage-network-security?toc=/azure/storage/files/toc.json).Verify that the

`allowSharedKeyAccess`

setting is set to`true`

, which is its default value. For more information, see[Prevent Shared Key authorization for an Azure Storage account](../storage/common/shared-key-authorization-prevent?tabs=portal#verify-that-shared-key-access-is-not-allowed).

## Daily execution quota is full

If you have a daily execution quota configured, your function app is temporarily disabled, which causes many of the portal controls to become unavailable.

To verify the quota in the [Azure portal](https://portal.azure.com), select **Platform Features** > **Function App Settings** in your function app. If you're over the **Daily Usage Quota** that you set, the following message is displayed:

"The Function App has reached daily usage quota and has been stopped until the next 24 hours time frame."


To resolve this issue, remove or increase the daily quota, and then restart your app. Otherwise, the execution of your app is blocked until the next day.

## App is behind a firewall

Your function app might be unreachable for either of the following reasons:

Your function app is hosted in an

[internally load balanced App Service Environment](../app-service/environment/create-ilb-ase)and it's configured to block inbound internet traffic.Your function app has

[inbound IP restrictions](functions-networking-options#inbound-networking-features)that are configured to block internet access.

The Azure portal makes calls directly to the running app to fetch the list of functions, and it makes HTTP calls to the Kudu endpoint. Platform-level settings under the **Platform Features** tab are still available.

To verify your ASE configuration:

- Go to the network security group (NSG) of the subnet where the ASE resides.
- Validate the inbound rules to allow traffic that's coming from the public IP of the computer where you're accessing the application.

You can also use the portal from a computer that's connected to the virtual network that's running your app or to a virtual machine that's running in your virtual network.

For more information about inbound rule configuration, see [Networking considerations for an App Service Environment](../app-service/environment/network-info#network-security-groups).

## Container errors on Linux

For function apps that run on Linux in a container, the `Azure Functions runtime is unreachable`

error can occur as a result of problems with the container. Use the following procedure to review the container logs for errors:

Navigate to the Kudu endpoint for the function app, which is located at

`https://<FUNCTION_APP>.scm.azurewebsites.net`

, where`<FUNCTION_APP>`

is the name of your app.Download the Docker logs .zip file and review the contents on your local computer.

Check for any logged errors that indicate that the container is unable to start successfully.


## Container image unavailable

Errors can occur when the container image being referenced is unavailable or fails to start correctly. Check for any logged errors that indicate that the container is unable to start successfully.

You need to correct any errors that prevent the container from starting for the function app run correctly.

When the container image can't be found, you see a `manifest unknown`

error in the Docker logs. In this case, you can use the Azure CLI commands documented at [How to target Azure Functions runtime versions](set-runtime-version?tabs=azurecli#manual-version-updates-on-linux) to change the container image being referenced. If you've deployed a [custom container image](functions-how-to-custom-container), you need to fix the image and redeploy the updated version to the referenced registry.

## App container has conflicting ports

Your function app might be in an unresponsive state due to conflicting port assignment upon startup. This situation can happen in the following cases:

- Your container has separate services running where one or more services are tying to bind to the same port as the function app.
- You added an Azure Hybrid Connection that shares the same port value as the function app.

By default, the container in which your function app runs uses port `:80`

. When other services in the same container are also trying to using port `:80`

, the function app can fail to start. If your logs show port conflicts, change the default ports.

## Host ID collision

Starting with version 3.x of the Functions runtime, [host ID collision](storage-considerations#host-id-considerations) are detected and logged as a warning. In version 4.x, an error is logged and the host is stopped. If the runtime can't start for your function app, [review the logs](analyze-telemetry-data). If there's a warning or an error about host ID collisions, follow the mitigation steps in [Host ID considerations](storage-considerations#host-id-considerations).

## Read-only app settings

Changing any *read-only* [App Service application settings](../app-service/reference-app-settings#app-environment) can put your function app into an unreachable state.

## ASP.NET authentication overrides

*Applies only to C# apps running in-process with the Functions host.*

Configuring ASP.NET authentication in a Functions startup class can override services that are required for the Azure portal to communicate with the host. This includes, but isn't limited to, any calls to `AddAuthentication()`

. If the host's authentication services are overridden and the portal can't communicate with the host, it considers the app unreachable. This issue might result in errors such as: `No authentication handler is registered for the scheme 'ArmToken'.`


## Next steps

Learn about monitoring your function apps:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-signalr-service -->

# SignalR Service bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This set of articles explains how to authenticate and send real-time messages to clients connected to [Azure SignalR Service](https://azure.microsoft.com/services/signalr-service/) by using SignalR Service bindings in Azure Functions. Azure Functions runtime version 2.x and higher supports input and output bindings for SignalR Service.

| Action | Type |
|---|---|
| Handle messages from SignalR Service |
|

[Input binding](functions-bindings-signalr-service-input)[Output binding](functions-bindings-signalr-service-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

Add the extension to your project by installing this [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.SignalRService/).

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

## Add dependency

To use the SignalR Service annotations in Java functions, you need to add a dependency to the *azure-functions-java-library-signalr* artifact (version 1.0 or higher) to your *pom.xml* file.

```
<dependency>
<groupId>com.microsoft.azure.functions</groupId>
<artifactId>azure-functions-java-library-signalr</artifactId>
<version>1.0.0</version>
</dependency>
```


## Connections

You can use [connection string](#connection-string) or [Microsoft Entra identity](#identity-based-connections) to connect to Azure SignalR Service.

### Connection string

For instructions on how to retrieve the connection string for your Azure SignalR Service, see [Connection strings in Azure SignalR Service](../azure-signalr/concept-connection-string#how-to-get-connection-strings)

This connection string should be stored in an application setting with a name `AzureSignalRConnectionString`

. You can customize the application setting name with the `connectionStringSetting`

property of the binding configuration.

### Identity-based connections

If you're using version 1.7.0 or higher, instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis).

First of all, you should make sure your Microsoft Entra identity has role [SignalR Service Owner](../role-based-access-control/built-in-roles#signalr-service-owner).

Then you would define settings with a common prefix `AzureSignalRConnectionString`

. You can customize prefix name with the `connectionStringSetting`

property of the binding configuration.

In this mode, the settings include following items:

| Property | Environment variable template | Description | Required | Example value |
|---|---|---|---|---|
| Service URI | `AzureSignalRConnectionString__serviceUri` |
The URI of your service endpoint. When you only configure "Service URI", the extensions would attempt to use
|

`AzureSignalRConnectionString__credential`

`managedidentity`

if your deployed Azure Function intends to use managed identity authentication. This value is only valid when a managed identity is available in the hosting environment.`AzureSignalRConnectionString__clientId`

`credential`

is set to `managedidentity`

, this property can be set to specify the user-assigned identity to be used when obtaining a token. The property accepts a client ID corresponding to a user-assigned identity assigned to the application. It's invalid to specify both a Resource ID and a client ID. If not specified, the system-assigned identity is used. This property is used differently in [local development scenarios](functions-reference#local-development-with-identity-based-connections), when`credential`

shouldn't be set.`AzureSignalRConnectionString__managedIdentityResourceId`

`credential`

is set to `managedidentity`

, this property can be set to specify the resource Identifier to be used when obtaining a token. The property accepts a resource identifier corresponding to the resource ID of the user-defined managed identity. It's invalid to specify both a resource ID and a client ID. If neither are specified, the system-assigned identity is used. This property is used differently in [local development scenarios](functions-reference#local-development-with-identity-based-connections), when`credential`

shouldn't be set.Note

When using `local.settings.json`

file at local, [Azure App Configuration](../azure-app-configuration/quickstart-azure-functions-csharp), or [Key Vault](/en-us/azure/key-vault/general/overview) to provide settings for identity-based connections, replace `__`

with `:`

in the setting name to ensure names are resolved correctly.

For example, `AzureSignalRConnectionString:serviceUri`

.

#### Multiple endpoints setting

You can also configure multiple endpoints and specify identity settings per endpoint.

In this case, prefix your settings with `Azure__SignalR__Endpoints__{endpointName}`

. The `{endpointName}`

is an arbitrary name assigned by you to associate a group of settings to a service endpoint. The prefix `Azure__SignalR__Endpoints__{endpointName}`

can't be customized by `connectionStringSetting`

property.

| Property | Environment variable template | Description | Required | Example value |
|---|---|---|---|---|
| Service URI | `Azure__SignalR__Endpoints__{endpointName}__serviceUri` |
The URI your service endpoint. When you only configure "Service URI", the extensions would attempt to use
|

`Azure__SignalR__Endpoints__{endpointName}__type`

`Primary`

. Valid values are `Primary`

and `Secondary`

, case-insensitive.`Secondary`

`Azure__SignalR__Endpoints__{endpointName}__credential`

`managedidentity`

if your deployed Azure Function intends to use managed identity authentication. This value is only valid when a managed identity is available in the hosting environment.`Azure__SignalR__Endpoints__{endpointName}__clientId`

`credential`

is set to `managedidentity`

, this property can be set to specify the user-assigned identity to be used when obtaining a token. The property accepts a client ID corresponding to a user-assigned identity assigned to the application. It's invalid to specify both a Resource ID and a client ID. If not specified, the system-assigned identity is used. This property is used differently in [local development scenarios](functions-reference#local-development-with-identity-based-connections), when`credential`

shouldn't be set.`Azure__SignalR__Endpoints__{endpointName}__managedIdentityResourceId`

`credential`

is set to `managedidentity`

, this property can be set to specify the resource Identifier to be used when obtaining a token. The property accepts a resource identifier corresponding to the resource ID of the user-defined managed identity. It's invalid to specify both a resource ID and a client ID. If neither are specified, the system-assigned identity is used. This property is used differently in [local development scenarios](functions-reference#local-development-with-identity-based-connections), when`credential`

shouldn't be set.For more information about multiple endpoints, see [Scale SignalR Service with multiple instances](../azure-signalr/signalr-howto-scale-multi-instances?pivots=serverless-mode#for-signalr-functions-extensions)

For optimal security, your function app should use managed identities when connecting to the Azure SignalR service instead of using a connection string, which contains a shared secret key. For more information, see [Authorize requests to Azure SignalR Service resources with Microsoft Entra managed identities](../azure-signalr/signalr-howto-authorize-managed-identity#azure-signalr-service-bindings-in-azure-functions).

## Next steps

For details on how to configure and use SignalR Service and Azure Functions together, refer to [Azure Functions development and configuration with Azure SignalR Service](../azure-signalr/signalr-concept-serverless-development-config).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-develop-local -->

# Code and test Azure Functions locally

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Whenever possible, you should create and validate your Azure Functions code project in a local development environment. Azure Functions Core Tools provides a local runtime version of Azure Functions that integrates with popular development tools for an integrated development, debugging, and deployments. Your local functions can even connect to live Azure services.

This article provides some shared guidance for local development, such as working with the [local.settings.json file](#local-settings-file). It also links to development environment-specific guidance.

Tip

You can find detailed information about how to develop functions locally in the linked IDE-specific guidance articles.

## Local development environments

The way in which you develop functions on your local computer depends on your [language](supported-languages) and tooling preferences. Make sure to choose your preferred language at the [top of the article](#top).

Tip

All local development relies on Azure Functions Core Tools to provide the Functions runtime for debugging in a local environment.

You can use these development environments to code functions locally in your preferred language:

| Environment | Description |
|---|---|
|

**Azure development**workload of[Visual Studio](https://www.visualstudio.com/vs/). Lets you compile and deploy your C# function code to Azure as a .NET class library. Includes the Core Tools for local testing. To learn more, see[Create your first C# function in Azure using Visual Studio](functions-create-your-first-function-visual-studio)[Visual Studio Code](functions-develop-vs-code)[Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)adds Functions support to Visual Studio Code. Requires the Core Tools. Supports development on Linux, macOS, and Windows. To learn more, see[Create your first function using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-csharp).[Command prompt or terminal](functions-run-local)[Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools)provides the core runtime and templates for creating functions, which enable local development. Supports development on Linux, macOS, and Windows. To learn more, see[Create a C# function in Azure from the command line](how-to-create-function-azure-cli?pivots=programming-language-csharp).| Environment | Description |
|---|---|
|

[Create your first function with Java and Maven](how-to-create-function-azure-cli?pivots=programming-language-java).[Visual Studio Code](functions-develop-vs-code)[Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)adds Functions support to Visual Studio Code. Requires the Core Tools. Supports development on Linux, macOS, and Windows. To learn more, see[Create your first function using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-java).[IntelliJ IDEA](functions-create-maven-intellij)[Create your first Java function in Azure using IntelliJ](functions-create-maven-intellij).[Eclipse](functions-create-maven-eclipse)[Create your first Java function in Azure using Ecplise](functions-create-maven-eclipse).| Environment | Description |
|---|---|
|

[Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)adds Functions support to Visual Studio Code. Requires the Core Tools. Supports development on Linux, macOS, and Windows. To learn more, see[Create your first function using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-javascript).[Command prompt or terminal](functions-run-local)[Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools)provides the core runtime and templates for creating functions, which enable local development. Supports development on Linux, macOS, and Windows. To learn more, see[Create a Node.js function in Azure from the command line](how-to-create-function-azure-cli?pivots=programming-language-javascript).| Environment | Description |
|---|---|
|

[Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)adds Functions support to Visual Studio Code. Requires the Core Tools. Supports development on Linux, macOS, and Windows. To learn more, see[Create your first function using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-powershell).[Command prompt or terminal](functions-run-local)[Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools)provides the core runtime and templates for creating functions, which enable local development. Supports development on Linux, macOS, and Windows. To learn more, see[Create a PowerShell function in Azure from the command line](how-to-create-function-azure-cli?pivots=programming-language-powershell).| Environment | Description |
|---|---|
|

[Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)adds Functions support to Visual Studio Code. Requires the Core Tools. Supports development on Linux, macOS, and Windows. To learn more, see[Create your first function using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-python).[Command prompt or terminal](functions-run-local)[Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools)provides the core runtime and templates for creating functions, which enable local development. Supports development on Linux, macOS, and Windows. To learn more, see[Create a Python function in Azure from the command line](how-to-create-function-azure-cli?pivots=programming-language-python).Each of these local development environments lets you create function app projects and use predefined function templates to create new functions. Each uses the Core Tools so that you can test and debug your functions against the real Functions runtime on your own machine just as you would any other app. You can also publish your function app project from any of these environments to Azure.

## Local project files

A Functions project directory contains the following files in the project root folder, regardless of language:

| File name | Description |
|---|---|
| host.json | To learn more, see the
|

[local settings file](#local-settings-file).[local settings file](#local-settings-file).Other files in the project depend on your language and specific functions. For more information, see the developer guide for your language.

### Local settings file

The `local.settings.json`

file stores app settings and settings used by local development tools. Settings in the `local.settings.json`

file are used only when you're running your project locally. When you publish your project to Azure, be sure to also add any required settings to the app settings for the function app.

Important

Because the `local.settings.json`

file might contain secrets, such as connection strings, you should use caution committing to source control. Tools that support Functions provide ways to synchronize settings in the `local.settings.json`

file with the [app settings](functions-how-to-use-azure-function-app-settings#settings) in the function app to which your project is deployed.

The `local.settings.json`

file has this structure:

```
{
"IsEncrypted": false,
"Values": {
"FUNCTIONS_WORKER_RUNTIME": "<language worker>",
"AzureWebJobsStorage": "<connection-string>",
"MyBindingConnection": "<binding-connection-string>",
"AzureWebJobs.HttpExample.Disabled": "true"
},
"Host": {
"LocalHttpPort": 7071,
"CORS": "*",
"CORSCredentials": false
},
"ConnectionStrings": {
"SQLConnectionString": "<sqlclient-connection-string>"
}
}
```


These settings are supported when you run projects locally:

| Setting | Description |
|---|---|
`IsEncrypted` |
When this setting is set to `true` , all values are encrypted with a local machine key. Used with `func settings` commands. Default value is `false` . You might want to encrypt the local.settings.json file on your local computer when it contains secrets, such as service connection strings. The host automatically decrypts settings when it runs. Use the `func settings decrypt` command before trying to read locally encrypted settings. |
`Values` |
Collection of application settings used when a project is running locally. These key-value (string-string) pairs correspond to application settings in your function app in Azure, like
`AzureWebJobsStorage` |

`Connection`

for the [Blob storage trigger](functions-bindings-storage-blob-trigger#configuration). For these properties, you need an application setting defined in the

`Values`

array. See the subsequent table for a list of commonly used settings. Values must be strings and not JSON objects or arrays. Setting names can't include a double underline (

`__`

) and shouldn't include a colon (`:`

). Double underline characters are reserved by the runtime, and the colon is reserved to support [dependency injection](functions-dotnet-dependency-injection#working-with-options-and-settings).

`Host`

`LocalHttpPort`

`func host start`

and `func run`

). The `--port`

command-line option takes precedence over this setting. For example, when running in Visual Studio IDE, you may change the port number by navigating to the "Project Properties -> Debug" window and explicitly specifying the port number in a `host start --port <your-port-number>`

command that can be supplied in the "Application Arguments" field.`CORS`

[cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing). Origins are supplied as a comma-separated list with no spaces. The wildcard value (*) is supported, which allows requests from any origin.`CORSCredentials`

`true`

, allows `withCredentials`

requests.`ConnectionStrings`

`ConnectionStrings`

section of a configuration file, like [Entity Framework](/en-us/ef/ef6/). Connection strings in this object are added to the environment with the provider type of[System.Data.SqlClient](/en-us/dotnet/api/system.data.sqlclient). Items in this collection aren't published to Azure with other app settings. You must explicitly add these values to the`Connection strings`

collection of your function app settings. If you're creating a [in your function code, you should store the connection string value with your other connections in](/en-us/dotnet/api/system.data.sqlclient.sqlconnection)`SqlConnection`

**Application Settings**in the portal.The following application settings can be included in the ** Values** array when running locally:

| Setting | Values | Description |
|---|---|---|
`AzureWebJobsStorage` |
Storage account connection string, or`UseDevelopmentStorage=true` |
Contains the connection string for an Azure storage account. Required when using triggers other than HTTP. For more information, see the
`AzureWebJobsStorage` |

When you have the

[Azurite Emulator](../storage/common/storage-use-azurite)installed locally and you set

[to](functions-app-settings#azurewebjobsstorage)

`AzureWebJobsStorage`

`UseDevelopmentStorage=true`

, Core Tools uses the emulator. For more information, see [Local storage emulator](#local-storage-emulator).

`AzureWebJobs.<FUNCTION_NAME>.Disabled`

`true`

|`false`

`"AzureWebJobs.<FUNCTION_NAME>.Disabled": "true"`

to the collection, where `<FUNCTION_NAME>`

is the name of the function. To learn more, see [How to disable functions in Azure Functions](disable-function#disable-functions-locally).`FUNCTIONS_WORKER_RUNTIME`

`dotnet`

`dotnet-isolated`

`node`

`java`

`powershell`

`python`

[reference.](functions-app-settings#functions_worker_runtime)`FUNCTIONS_WORKER_RUNTIME`

`FUNCTIONS_WORKER_RUNTIME_VERSION`

`~7`

`powerShellVersion`

site configuration setting, when it runs in Azure, which can be [set in the portal](functions-reference-powershell#changing-the-powershell-version).To learn how to use values from the `values`

array as environment variables in your function code, see [Environment variables](functions-reference-node#environment-variables) in the developer guide.

To learn how to use values from the `values`

array as environment variables in your function code, see [Environment variables](functions-reference-java#environment-variables) in the developer guide.

To learn how to use values from the `values`

array as environment variables in your function code, see [Environment variables](functions-reference-powershell#environment-variables) in the developer guide.

To learn how to use values from the `values`

array as environment variables in your function code, see [Environment variables](functions-reference-python#environment-variables) in the developer guide.

## Synchronize settings

When you develop your functions locally, any local settings required by your app must also be present in app settings of the function app to which your code is deployed. You might also need to download current settings from the function app to your local project. While you can [manually configure app settings in the Azure portal](functions-how-to-use-azure-function-app-settings?tabs=portal#settings), the following tools also let you synchronize app settings with local settings in your project:

## Triggers and bindings

When you develop your functions locally, you need to take trigger and binding behaviors into consideration. For HTTP triggers, you can call the HTTP endpoint on the local computer, using `http://localhost/`

. For non-HTTP triggered functions, there are several options to run locally:

- The easiest way to test bindings during local development is to use connection strings that target live Azure services. You can target live services by adding the appropriate connection string settings in the
`Values`

array in the local.settings.json file. When you do this, local executions during testing might affect your production services. Instead, consider setting-up separate services to use during development and testing, and then switch to different services during production. - For storage-based triggers, you can use a
[local storage emulator](#local-storage-emulator). - You can manually run non-HTTP trigger functions by using special administrator endpoints. For more information, see
[Manually run a non-HTTP-triggered function](functions-manually-run-non-http).

During local testing, you must be running the host provided by Core Tools (func.exe) locally. For more information, see [Azure Functions Core Tools](functions-run-local).

## HTTP test tools

During development, it's easy to call any of your function endpoints from a web browser when they support the HTTP GET method. However, for other HTTP methods that support payloads, such as POST or PUT, you need to use an HTTP test tool to create and send these HTTP requests to your function endpoints.

Caution

For scenarios where your requests must include sensitive data, make sure to use a tool that protects your data and reduces the risk of exposing any sensitive data to the public. Sensitive data you should protect might include: credentials, secrets, access tokens, API keys, geolocation data, even personal data.

You can keep your data secure by choosing an HTTP test tool that works either offline or locally, doesn't sync your data to the cloud, and doesn't require that you sign in to an online account. Some tools can also protect your data from accidental exposure by implementing specific security features.

Avoid using tools that centrally store your HTTP request history (including sensitive information), don't follow best security practices, or don't respect data privacy concerns.

Consider using one of these tools for securely sending HTTP requests to your function endpoints:

[Visual Studio Code](https://code.visualstudio.com/download)with an[extension from Visual Studio Marketplace](https://marketplace.visualstudio.com/vscode), such as[REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)[PowerShell Invoke-RestMethod](/en-us/powershell/module/microsoft.powershell.utility/invoke-restmethod)[Microsoft Edge - Network Console tool](/en-us/microsoft-edge/devtools-guide-chromium/network-console/network-console-tool)[Bruno](https://www.usebruno.com/)[curl](https://curl.se/)

## Local storage emulator

During local development, you can use the local [Azurite emulator](../storage/common/storage-use-azurite) when testing functions with Azure Storage bindings (Queue Storage, Blob Storage, and Table Storage), without having to connect to remote storage services. Azurite integrates with Visual Studio Code and Visual Studio, and you can also run it from the command prompt using npm. For more information, see [Use the Azurite emulator for local Azure Storage development](../storage/common/storage-use-azurite).

The following setting in the `Values`

collection of the local.settings.json file tells the local Functions host to use Azurite for the default `AzureWebJobsStorage`

connection:

```
"AzureWebJobsStorage": "UseDevelopmentStorage=true"
```


With this setting value, any Azure Storage trigger or binding that uses `AzureWebJobsStorage`

as its connection connects to Azurite when running locally. Keep these considerations in mind when using storage emulation during local execution:

- You must have Azurite installed and running.
- You should test with an actual storage connection to Azure services before publishing to Azure.
- When you publish your project, don't publish the
`AzureWebJobsStorage`

setting as`UseDevelopmentStorage=true`

. In Azure, the`AzureWebJobsStorage`

setting must always be the connection string of the storage account used by your function app. For more information, see.`AzureWebJobsStorage`


## Related articles

- To learn more about local development of functions using Visual Studio, see
[Develop Azure Functions using Visual Studio](functions-develop-vs).

- To learn more about local development of functions using Visual Studio Code on a Mac, Linux, or Windows computer, see
[Develop Azure Functions by using Visual Studio Code](functions-develop-vs-code). - To learn more about developing functions from the command prompt or terminal, see
[Work with Azure Functions Core Tools](functions-run-local).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-mysql -->

# Overview of Azure Database for MySQL bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This set of articles explains how to work with [Azure Database for MySQL](/en-us/azure/mysql/index) bindings in Azure Functions. Azure Functions supports input bindings, output bindings and trigger bindings in general availability for Azure Database for MySQL

| Action | Type |
|---|---|
| Read data from a database |
|

[Output binding](functions-bindings-azure-mysql-output)[Trigger binding](functions-bindings-azure-mysql-trigger)## Install the extension

The extension NuGet package that you install depends on the C# mode you're using in your function app:

Functions run in an isolated C# worker process. To learn more, see [Guide for running C# Azure functions in an isolated worker process](dotnet-isolated-process-guide).

Add the extension to your project by installing [this NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.MySql/1.0.129/).

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.MySql --version 1.0.129
```


## Install the bundle

The extension for Azure Database for MySQL bindings is part of the v4 [extension bundle](extension-bundles). This bundle is specified in your host.json project file.

### Bundle v4.x

You can use the extension bundle by adding or replacing the following code in your host.json file:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
}
}
```


## Install the bundle

The extension for Azure Database for MySQL bindings is part of the v4 [extension bundle](extension-bundles). This bundle is specified in your host.json project file.

### Bundle v4.x

You can use the extension bundle by adding or replacing the following code in your host.json file:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
}
}
```


## Install the bundle

The extension for Azure Database for MySQL bindings is part of the v4 [extension bundle](extension-bundles). This bundle is specified in your host.json project file.

### Bundle v4.x

You can use the extension bundle by adding or replacing the following code in your host.json file:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
}
}
```


## Update packages

You can use the extension bundle with an update to the pom.xml file in your Java Azure Functions project, as shown in the following snippet:

```
<dependency>
<groupId>com.microsoft.azure.functions</groupId>
<artifactId>azure-functions-java-library-mysql</artifactId>
<version>1.0.2</version>
</dependency>
```


## MySQL connection string

Azure Database for MySQL bindings for Azure Functions have a required property for the connection string. These bindings pass the connection string to the MySql.Data.MySqlClient library and provide support as defined in the [MySqlClient ConnectionString documentation](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html). Notable keywords include:

`server`

: The host on which the server instance is running. The value can be a host name, IPv4 address, or IPv6 address.`uid`

: The MySQL user account to provide for the authentication process.`pwd`

: The password to use for the authentication process.`database`

: The default database for the connection. If no database is specified, the connection has no default database.

## Considerations

- Azure Database for MySQL bindings support version 4.x and later of the Azure Functions runtime.
- You can find source code for the Azure Database for MySQL bindings in
[this GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/src). - These bindings require connectivity to Azure Database for MySQL.
- Output bindings against tables with columns of spatial data types
`GEOMETRY`

,`POINT`

, and`POLYGON`

aren't supported. Data upserts fail.

## Samples

In addition to the samples for C#, Java, JavaScript, PowerShell, and Python available in the [GitHub repository for Azure Database for MySQL bindings](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples), more are available in [Azure Samples](https://github.com/Azure-Samples).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-http-webhook -->

# Azure Functions HTTP triggers and bindings overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions may be invoked via HTTP requests to build serverless APIs and respond to [webhooks](https://en.wikipedia.org/wiki/Webhook).

| Action | Type |
|---|---|
| Run a function from an HTTP request |
|

[Output binding](functions-bindings-http-webhook-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

Add the extension to your project by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Http), version 3.x.

Note

An additional extension package is needed for [ASP.NET Core integration in .NET Isolated](dotnet-isolated-process-guide#aspnet-core-integration)

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

Note

For a reference of host.json in Functions 1.x, see [host.json reference for Azure Functions 1.x](functions-host-json-v1#http).

```
{
"extensions": {
"http": {
"routePrefix": "api",
"maxOutstandingRequests": 200,
"maxConcurrentRequests": 100,
"dynamicThrottlesEnabled": true,
"hsts": {
"isEnabled": true,
"maxAge": "10"
},
"customHeaders": {
"X-Content-Type-Options": "nosniff"
}
}
}
}
```


| Property | Default | Description | ||||||||||
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| customHeaders | none | Allows you to set custom headers in the HTTP response. The previous example adds the `X-Content-Type-Options` header to the response to avoid content type sniffing. This custom header applies to all HTTP triggered functions in the function app. |
||||||||||
| dynamicThrottlesEnabled | true* |
When enabled, this setting causes the request processing pipeline to periodically check system performance counters like `connections/threads/processes/memory/cpu/etc` and if any of those counters are over a built-in high threshold (80%), requests will be rejected with a `429 "Too Busy"` response until the counter(s) return to normal levels.*The default in a Consumption plan is `true` . The default in the Premium and Dedicated plans is `false` . |
||||||||||
| hsts | not enabled | When `isEnabled` is set to `true` , the
`HstsOptions` class |

| Property | Description |
|---|---|
| excludedHosts | A string array of host names for which the HSTS header isn't added. |
| includeSubDomains | Boolean value that indicates whether the includeSubDomain parameter of the Strict-Transport-Security header is enabled. |
| maxAge | String that defines the max-age parameter of the Strict-Transport-Security header. |
| preload | Boolean that indicates whether the preload parameter of the Strict-Transport-Security header is enabled. |

**The default for a Consumption plan is 100. The default for the Premium and Dedicated plans is unbounded (`-1`

).**The default for a Consumption plan is 200. The default for the Premium and Dedicated plans is unbounded (`-1`

).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-sendgrid -->

# Azure Functions SendGrid bindings

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to send email by using [SendGrid](https://sendgrid.com/docs/User_Guide/index.html) bindings in Azure Functions. Azure Functions supports an output binding for SendGrid.

This is reference information for Azure Functions developers. If you're new to Azure Functions, start with the following resources:

C# developer references:


## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

Add the extension to your project by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.SendGrid), version 3.x.

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

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

We don't currently have an example for using the SendGrid binding in a function app running in an isolated worker process.

The following example shows a SendGrid output binding in a *function.json* file and a [JavaScript function](functions-reference-node) that uses the binding.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"name": "$return",
"type": "sendGrid",
"direction": "out",
"apiKey" : "MySendGridKey",
"to": "{ToEmail}",
"from": "{FromEmail}",
"subject": "SendGrid output bindings"
}
]
}
```


The [configuration](#configuration) section explains these properties.

Here's the JavaScript code:

```
module.exports = function (context, input) {
var message = {
"personalizations": [ { "to": [ { "email": "sample@sample.com" } ] } ],
from: { email: "sender@contoso.com" },
subject: "Azure news",
content: [{
type: 'text/plain',
value: input
}]
};
return message;
};
```


Complete PowerShell examples aren't currently available for SendGrid bindings.

The following example shows an HTTP-triggered function that sends an email using the SendGrid binding. You can provide default values in the binding configuration. For instance, the *from* email address is configured in *function.json*.

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"type": "httpTrigger",
"authLevel": "function",
"direction": "in",
"name": "req",
"methods": ["get", "post"]
},
{
"type": "http",
"direction": "out",
"name": "$return"
},
{
"type": "sendGrid",
"name": "sendGridMessage",
"direction": "out",
"apiKey": "SendGrid_API_Key",
"from": "sender@contoso.com"
}
]
}
```


The following function shows how you can provide custom values for optional properties.

```
import logging
import json
import azure.functions as func
def main(req: func.HttpRequest, sendGridMessage: func.Out[str]) -> func.HttpResponse:
value = "Sent from Azure Functions"
message = {
"personalizations": [ {
"to": [{
"email": "user@contoso.com"
}]}],
"subject": "Azure Functions email with SendGrid",
"content": [{
"type": "text/plain",
"value": value }]}
sendGridMessage.set(json.dumps(message))
return func.HttpResponse(f"Sent")
```


The following example uses the `@SendGridOutput`

annotation from the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime) to send an email using the SendGrid output binding.

```
package com.function;
import java.util.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.*;
public class HttpTriggerSendGrid {
@FunctionName("HttpTriggerSendGrid")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = { HttpMethod.GET, HttpMethod.POST },
authLevel = AuthorizationLevel.FUNCTION)
HttpRequestMessage<Optional<String>> request,
@SendGridOutput(
name = "message",
dataType = "String",
apiKey = "SendGrid_API_Key",
to = "user@contoso.com",
from = "sender@contoso.com",
subject = "Azure Functions email with SendGrid",
text = "Sent from Azure Functions")
OutputBinding<String> message,
final ExecutionContext context) {
final String toAddress = "user@contoso.com";
final String value = "Sent from Azure Functions";
StringBuilder builder = new StringBuilder()
.append("{")
.append("\"personalizations\": [{ \"to\": [{ \"email\": \"%s\"}]}],")
.append("\"content\": [{\"type\": \"text/plain\", \"value\": \"%s\"}]")
.append("}");
final String body = String.format(builder.toString(), toAddress, value);
message.setValue(body);
return request.createResponseBuilder(HttpStatus.OK).body("Sent").build();
}
}
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the output binding. C# script instead uses a function.json configuration file.

In [isolated worker process](dotnet-isolated-process-guide) function apps, the `SendGridOutputAttribute`

supports the following parameters:

| Attribute/annotation property | Description |
|---|---|
ApiKey |
The name of an app setting that contains your API key. If not set, the default app setting name is `AzureWebJobsSendGridApiKey` . |
To |
(Optional) The recipient's email address. |
From |
(Optional) The sender's email address. |
Subject |
(Optional) The subject of the email. |
Text |
(Optional) The email content. |

## Annotations

The [SendGridOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.sendgridoutput) annotation allows you to declaratively configure the SendGrid binding by providing the following configuration values.

## Configuration

The following table lists the binding configuration properties available in the *function.json* file and the `SendGrid`

attribute/annotation.

function.json property |
Description |
|---|---|
type |
Must be set to `sendGrid` . |
direction |
Must be set to `out` . |
name |
The variable name used in function code for the request or request body. This value is `$return` when there's only one return value. |
apiKey |
The name of an app setting that contains your API key. If not set, the default app setting name is AzureWebJobsSendGridApiKey. |
to |
(Optional) The recipient's email address. |
from |
(Optional) The sender's email address. |
subject |
(Optional) The subject of the email. |
text |
(Optional) The email content. |

Optional properties may have default values defined in the binding and either added or overridden programmatically.

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## host.json settings

This section describes the configuration settings available for this binding in version 2.x and later. Settings in the host.json file apply to all functions in a function app instance. For more information about function app configuration settings, see [host.json reference for Azure Functions](functions-host-json).

Note

For a reference of host.json in Functions 1.x, see [host.json reference for Azure Functions 1.x](functions-host-json-v1).

```
{
"version": "2.0",
"extensions": {
"sendGrid": {
"from": "Azure Functions <samples@functions.com>"
}
}
}
```


| Property | Default | Description |
|---|---|---|
from |
n/a | The sender's email address across all functions. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-queue -->

# Azure Queue storage trigger and bindings for Azure Functions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions can run as new Azure Queue storage messages are created and can write queue messages within a function.

| Action | Type |
|---|---|
| Run a function as queue storage data changes |
|

[Output binding](functions-bindings-storage-queue-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

This version introduces the ability to [connect using an identity instead of a secret](functions-reference#configure-an-identity-based-connection). For a tutorial on configuring your function apps with managed identities, see the [creating a function app with identity-based connections tutorial](functions-identity-based-connections-tutorial).

This version allows you to bind to types from [Azure.Storage.Queues](/en-us/dotnet/api/azure.storage.queues).

This version supports configuration of triggers and bindings through [.NET Aspire integration](dotnet-aspire-integration#connection-configuration-with-aspire).

Add the extension to your project by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues), version 5.x.

Using the .NET CLI:

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues
```


Note

Azure Blobs, Azure Queues, and Azure Tables now use separate extensions and are referenced individually. For example, to use the triggers and bindings for all three services in your .NET isolated-process app, you should add the following packages to your project:

[Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs)[Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues)[Microsoft.Azure.Functions.Worker.Extensions.Tables](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Tables)

Previously, the extensions shipped together as [Microsoft.Azure.Functions.Worker.Extensions.Storage, version 4.x](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage/4.0.4). This same package also has a [5.x version](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage/5.0.0), which references the split packages for blobs and queues only. When upgrading your package references from older versions, you may therefore need to additionally reference the new [Microsoft.Azure.Functions.Worker.Extensions.Tables](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Tables) NuGet package. Also, when referencing these newer split packages, make sure you are not referencing an older version of the combined storage package, as this will result in conflicts from two definitions of the same bindings.

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

The isolated worker process supports parameter types according to the tables below. Support for binding to types from [Azure.Storage.Queues](/en-us/dotnet/api/azure.storage.queues) is in preview.

**Queue trigger**

The queue trigger can bind to the following types:

| Type | Description |
|---|---|
`string` |
The message content as a string. Use when the message is simple text.. |
`byte[]` |
The bytes of the message. |
| JSON serializable types | When a queue message contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

[BinaryData](/en-us/dotnet/api/system.binarydata)11 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues 5.2.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues/5.2.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

**Queue output binding**

When you want the function to write a single message, the queue output binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The message content as a string. Use when the message is simple text. |
`byte[]` |
The bytes of the message. |
| JSON serializable types | An object representing the content of a JSON message. Functions tries to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write multiple messages, the queue output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single message types |
An array containing content for multiple messages. Each entry represents one message. |

For other output scenarios, create and use a [QueueClient](/en-us/dotnet/api/azure.storage.queues.queueclient) with other types from [Azure.Storage.Queues](/en-us/dotnet/api/azure.storage.queues) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

## host.json settings

This section describes the configuration settings available for this binding in version 2.x and later. Settings in the host.json file apply to all functions in a function app instance. For more information about function app configuration settings, see [host.json reference for Azure Functions](functions-host-json).

Note

For a reference of host.json in Functions 1.x, see [host.json reference for Azure Functions 1.x](functions-host-json-v1).

```
{
"version": "2.0",
"extensions": {
"queues": {
"maxPollingInterval": "00:00:02",
"visibilityTimeout" : "00:00:30",
"batchSize": 16,
"maxDequeueCount": 5,
"newBatchThreshold": 8,
"messageEncoding": "base64"
}
}
}
```


| Property | Default | Description |
|---|---|---|
| maxPollingInterval | 00:01:00 | The maximum interval between queue polls. The minimum interval is 00:00:00.100 (100 ms). Intervals increment up to `maxPollingInterval` . The default value of `maxPollingInterval` is 00:01:00 (1 min). `maxPollingInterval` must not be less than 00:00:00.100 (100 ms). In Functions 2.x and later, the data type is a `TimeSpan` . In Functions 1.x, it is in milliseconds. |
| visibilityTimeout | 00:00:00 | The time interval between retries when processing of a message fails. |
| batchSize | 16 | The number of queue messages that the Functions runtime retrieves simultaneously and processes in parallel. When the number being processed gets down to the `newBatchThreshold` , the runtime gets another batch and starts processing those messages. So the maximum number of concurrent messages being processed per function is `batchSize` plus `newBatchThreshold` . This limit applies separately to each queue-triggered function. If you want to avoid parallel execution for messages received on one queue, you can set `batchSize` to 1. However, this setting eliminates concurrency as long as your function app runs only on a single virtual machine (VM). If the function app scales out to multiple VMs, each VM could run one instance of each queue-triggered function.The maximum `batchSize` is 32. |
| maxDequeueCount | 5 | The number of times to try processing a message before moving it to the poison queue. |
| newBatchThreshold | N*batchSize/2 | Whenever the number of messages being processed concurrently gets down to this number, the runtime retrieves another batch.`N` represents the number of vCPUs available when running on App Service or Premium Plans. Its value is `1` for the Consumption Plan. |
| messageEncoding | base64 | This setting is only available in
`base64` and `none` . |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-rabbitmq-trigger -->

# RabbitMQ trigger for Azure Functions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the RabbitMQ trigger to respond to messages from a RabbitMQ queue.

Note

The RabbitMQ bindings are only fully supported on [Elastic Premium](functions-premium-plan) and [Dedicated (App Service)](dedicated-plan) plans. [Flex Consumption](flex-consumption-plan) and [Consumption](consumption-plan) plans aren't yet supported.

RabbitMQ bindings aren't supported by the Azure Functions v1.x runtime.

For information on setup and configuration details, see the [overview](functions-bindings-rabbitmq).

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


The following Java function uses the `@RabbitMQTrigger`

annotation from the [Java RabbitMQ types](https://mvnrepository.com/artifact/com.microsoft.azure.functions/azure-functions-java-library-rabbitmq) to describe the configuration for a RabbitMQ queue trigger. The function grabs the message placed on the queue and adds it to the logs.

```
@FunctionName("RabbitMQTriggerExample")
public void run(
@RabbitMQTrigger(connectionStringSetting = "rabbitMQConnectionAppSetting", queueName = "queue") String input,
final ExecutionContext context)
{
context.getLogger().info("Java HTTP trigger processed a request." + input);
}
```


The following example shows a RabbitMQ trigger binding in a *function.json* file and a [JavaScript function](functions-reference-node) that uses the binding. The function reads and logs a RabbitMQ message.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"name": "myQueueItem",
"type": "rabbitMQTrigger",
"direction": "in",
"queueName": "queue",
"connectionStringSetting": "rabbitMQConnectionAppSetting"
}
]
}
```


Here's the JavaScript script code:

```
module.exports = async function (context, myQueueItem) {
context.log('JavaScript RabbitMQ trigger function processed work item', myQueueItem);
};
```


The following example demonstrates how to read a RabbitMQ queue message via a trigger.

A RabbitMQ binding is defined in *function.json* where *type* is set to `RabbitMQTrigger`

.

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"name": "myQueueItem",
"type": "rabbitMQTrigger",
"direction": "in",
"queueName": "queue",
"connectionStringSetting": "rabbitMQConnectionAppSetting"
}
]
}
```


```
import logging
import azure.functions as func
def main(myQueueItem) -> None:
logging.info('Python RabbitMQ trigger function processed a queue item: %s', myQueueItem)
```


PowerShell examples aren't currently available.

## Attributes

Both [isolated worker process](dotnet-isolated-process-guide) and [in-process](functions-dotnet-class-library) C# libraries use `RabbitMQTriggerAttribute`

to define the function, where specific properties of the attribute depend on the extension version.

The attribute's constructor accepts these parameters:

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

.## Annotations

The `RabbitMQTrigger`

annotation allows you to create a function that runs when a RabbitMQ message is created.

The annotation supports the following configuration options:

| Parameter | Description |
|---|---|
queueName |
Name of the queue from which to receive messages. |
connectionStringSetting |
The name of the app setting that contains the connection string for your RabbitMQ server. This setting only takes an app setting key name, you can't directly set a connection string value. For more information, see
|

**disableCertificateValidation**`true`

indicating that certificate validation should be disabled. Default value is `false`

. Not recommended for production. Does not apply when SSL is disabled.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `RabbitMQTrigger` . |
direction |
Must be set to `in` . |
name |
The name of the variable that represents the queue in function code. |
queueName |
Name of the queue from which to receive messages. |
connectionStringSetting |
The name of the app setting that contains the connection string for your RabbitMQ server. This setting only takes an app setting key name, you can't directly set a connection string value. For more information, see
|

**disableCertificateValidation**`true`

indicating that certificate validation should be disabled. Default value is `false`

. Not recommended for production. Does not apply when SSL is disabled.When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

See the [Example section](#example) for complete examples.

## Usage

The parameter type supported by the RabbitMQ trigger depends on the C# modality used.

The RabbitMQ bindings currently support only string and serializable object types when running in an isolated process.

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

### Dead letter queues

Dead letter queues and exchanges can't be controlled or configured from the RabbitMQ trigger. To use dead letter queues, pre-configure the queue used by the trigger in RabbitMQ. Refer to the [RabbitMQ documentation](https://www.rabbitmq.com/dlx.html).

### Enable Runtime Scaling

In order for the RabbitMQ trigger to scale out to multiple instances, the **Runtime Scale Monitoring** setting must be enabled.

In the portal, this setting can be found under **Configuration** > **Function runtime settings** for your function app.


In the Azure CLI, you can enable **Runtime Scale Monitoring** by using this command:

```
az resource update -resource-group <RESOURCE_GROUP> -name <APP_NAME>/config/web \
--set properties.functionsRuntimeScaleMonitoringEnabled=1 \
--resource-type Microsoft.Web/sites
```


### Monitoring a RabbitMQ endpoint

To monitor your queues and exchanges for a certain RabbitMQ endpoint:

- Enable the
[RabbitMQ management plugin](https://www.rabbitmq.com/management.html) - Browse to
`http://{node-hostname}:15672`

and log in with your user name and password.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-deploy-container -->

# Create your first containerized Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you create a function app running in a Linux container and deploy it to Azure Functions.

Deploying your function code to Azure Functions in a container requires [Premium plan](functions-premium-plan) or [Dedicated (App Service) plan](dedicated-plan) hosting. Completing this article incurs costs of a few US dollars in your Azure account, which you can minimize by [cleaning-up resources](#clean-up-resources) when you're done.

Tip

When you need to run your event-driven functions in Azure in the same environment as other microservices, APIs, websites, workflows, or any container hosted programs, consider instead hosting your containerized function apps in Azure Container Apps. Functions provides integrated support for developing, deploying, and managing containerized function apps on Container Apps. For more information, see [Azure Container Apps hosting of Azure Functions](../container-apps/functions-overview).

## Choose your development language

First, you use Azure Functions tools to create your project code as a function app in a Docker container using a language-specific Linux base image. Make sure to select your language of choice at the top of the article.

Core Tools automatically generates a Dockerfile for your project that uses the most up-to-date version of the correct base image for your functions language. You should regularly update your container from the latest base image and redeploy from the updated version of your container. For more information, see [Creating containerized function apps](functions-how-to-custom-container#creating-containerized-function-apps).

## Prerequisites

Before you begin, you must have the following requirements in place:

Install the

[.NET 8.0 SDK](https://dotnet.microsoft.com/download).Install

[Azure Functions Core Tools](functions-run-local#v2)version 4.0.5198, or a later version.

- Install
[Azure Functions Core Tools](functions-run-local#v2)version 4.x.

- Install a version of
[Node.js](https://nodejs.org/)that is[supported by Azure Functions](functions-reference-node#supported-versions).

- Install a version of Python that is
[supported by Azure Functions](functions-reference-python#supported-python-versions).

- Install the
[.NET 6 SDK](https://dotnet.microsoft.com/download).

Install a version of the

[Java Developer Kit](/en-us/azure/developer/java/fundamentals/java-jdk-long-term-support)that is[supported by Azure Functions](functions-reference-java#supported-versions).Install

[Apache Maven](https://maven.apache.org)version 3.0 or above.

[Azure CLI](/en-us/cli/azure/install-azure-cli)version 2.4 or a later version.

If you don't have an [Azure subscription](../guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing), create an [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

To publish the containerized function app image you create to a container registry, you need a Docker ID and [Docker](https://docs.docker.com/install/) running on your local computer. If you don't have a Docker ID, you can [create a Docker account](https://hub.docker.com/signup).

You also need to complete the [Create a container registry](/en-us/azure/container-registry/container-registry-get-started-portal#create-a-container-registry) section of the Container Registry quickstart to create a registry instance. Make a note of your fully qualified login server name.

## Create and activate a virtual environment

In a suitable folder, run the following commands to create and activate a virtual environment named `.venv`

. Make sure to use one of the [Python versions](functions-reference-python#supported-python-versions) supported by Azure Functions.

```
python -m venv .venv
```


```
source .venv/bin/activate
```


If Python didn't install the venv package on your Linux distribution, run the following command:

```
sudo apt-get install python3-venv
```


You run all subsequent commands in this activated virtual environment.

## Create and test the local functions project

In a terminal or command prompt, run the following command for your chosen language to create a function app project in the current folder:

```
func init --worker-runtime dotnet-isolated --docker
```


```
func init --worker-runtime node --language javascript --docker
```


```
func init --worker-runtime powershell --docker
```


```
func init --worker-runtime python --docker
```


```
func init --worker-runtime node --language typescript --docker
```


In an empty folder, run the following command to generate the Functions project from a [Maven archetype](https://maven.apache.org/guides/introduction/introduction-to-archetypes.html):

```
mvn archetype:generate -DarchetypeGroupId=com.microsoft.azure -DarchetypeArtifactId=azure-functions-archetype -DjavaVersion=8 -Ddocker
```


The `-DjavaVersion`

parameter tells the Functions runtime which version of Java to use. Use `-DjavaVersion=11`

if you want your functions to run on Java 11. When you don't specify `-DjavaVersion`

, Maven defaults to Java 8. For more information, see [Java versions](functions-reference-java#java-versions).

Important

The `JAVA_HOME`

environment variable must be set to the install location of the correct version of the JDK to complete this article.

Maven asks you for values needed to finish generating the project on deployment. Follow the prompts and provide the following information:

| Prompt | Value | Description |
|---|---|---|
groupId |
`com.fabrikam` |
A value that uniquely identifies your project across all projects, following the
|

**artifactId**`fabrikam-functions`

**version**`1.0-SNAPSHOT`

**package**`com.fabrikam.functions`

Type `Y`

or press Enter to confirm.

Maven creates the project files in a new folder named *artifactId*, which in this example is `fabrikam-functions`

.

The `--docker`

option generates a *Dockerfile* for the project, which defines a suitable container for use with Azure Functions and the selected runtime.

Navigate into the project folder:

```
cd fabrikam-functions
```


Use the following command to add a function to your project, where the `--name`

argument is the unique name of your function and the `--template`

argument specifies the function's trigger. `func new`

creates a C# code file in your project.

```
func new --name HttpExample --template "HTTP trigger"
```


Use the following command to add a function to your project, where the `--name`

argument is the unique name of your function and the `--template`

argument specifies the function's trigger. `func new`

creates a subfolder matching the function name that contains a configuration file named *function.json*.

```
func new --name HttpExample --template "HTTP trigger"
```


To test the function locally, start the local Azure Functions runtime host in the root of the project folder. To ensure the function can be called later when hosted in Docker, check that the authorization level is set to AuthorizationLevel.Anonymous, or set it if not already configured.

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


```
mvn clean package
mvn azure-functions:run
```


After you see the `HttpExample`

endpoint written to the output, navigate to that endpoint. You should see a welcome message in the response output.

After you see the `HttpExample`

endpoint written to the output, navigate to `http://localhost:7071/api/HttpExample?name=Functions`

. The browser must display a "hello" message that echoes back `Functions`

, the value supplied to the `name`

query parameter.

Press **Ctrl**+**C** (**Command**+**C** on macOS) to stop the host.

## Build the container image and verify locally

(Optional) Examine the *Dockerfile* in the root of the project folder. The *Dockerfile* describes the required environment to run the function app on Linux. The complete list of supported base images for Azure Functions can be found in the [Azure Functions base image page](https://hub.docker.com/_/microsoft-azure-functions-base).

In the root project folder, run the [docker build](https://docs.docker.com/engine/reference/commandline/build/) command, provide a name as `azurefunctionsimage`

, and tag as `v1.0.0`

. Replace `<DOCKER_ID>`

with your Docker Hub account ID. This command builds the Docker image for the container.

```
docker build --tag <DOCKER_ID>/azurefunctionsimage:v1.0.0 .
```


When the command completes, you can run the new container locally.

To verify the build, run the image in a local container using the [docker run](https://docs.docker.com/engine/reference/commandline/run/) command, replace `<DOCKER_ID>`

again with your Docker Hub account ID, and add the ports argument as `-p 8080:80`

:

```
docker run -p 8080:80 -it <DOCKER_ID>/azurefunctionsimage:v1.0.0
```


After the image starts in the local container, browse to `http://localhost:8080/api/HttpExample`

, which must display the same greeting message as before. Because the HTTP triggered function you created uses anonymous authorization, you can call the function running in the container without having to obtain an access key. For more information, see [authorization keys](functions-bindings-http-webhook-trigger#authorization-keys).

After the image starts in the local container, browse to `http://localhost:8080/api/HttpExample?name=Functions`

, which must display the same "hello" message as before. Because the HTTP triggered function you created uses anonymous authorization, you can call the function running in the container without having to obtain an access key. For more information, see [authorization keys](functions-bindings-http-webhook-trigger#authorization-keys).

After verifying the function app in the container, press **Ctrl**+**C** (**Command**+**C** on macOS) to stop execution.

## Publish the container image to a registry

To make your container image available for deployment to a hosting environment, you must push it to a container registry. As a security best practice, you should use an Azure Container Registry instance and enforce managed identity-based connections. Docker Hub requires you to authenticate using shared secrets, which make your deployments more vulnerable.

Azure Container Registry is a private registry service for building, storing, and managing container images and related artifacts. You should use a private registry service for publishing your containers to Azure services.

Use this command to sign in to your registry instance using your current Azure credentials:

`az acr login --name <REGISTRY_NAME>`

In the previous command, replace

`<REGISTRY_NAME>`

with the name of your Container Registry instance.Use this command to tag your image with the fully qualified name of your registry login server:

`docker tag <DOCKER_ID>/azurefunctionsimage:v1.0.0 <LOGIN_SERVER>/azurefunctionsimage:v1.0.0`

Replace

`<LOGIN_SERVER>`

with the fully qualified name of your registry login server and`<DOCKER_ID>`

with your Docker ID.Use this command to push the container to your registry instance:

`docker push <LOGIN_SERVER>/azurefunctionsimage:v1.0.0`


## Create supporting Azure resources for your function

Before you can deploy your container to Azure, you need to create three resources:

- A
[resource group](../azure-resource-manager/management/overview), which is a logical container for related resources. - A
[Storage account](../storage/common/storage-account-create), which is used to maintain state and other information about your functions. - A function app, which provides the environment for executing your function code. A function app maps to your local function project and lets you group functions as a logical unit for easier management, deployment, and sharing of resources.

Important

This article currently shows how to connect to both the Azure Storage account and your container registry by using connection strings and other shared secret credentials. For the best security, you should instead use only a managed identity-based connection to both your storage account and to Azure Container Registry using Microsoft Entra authentication. For more information, see the [Functions developer guide](functions-reference#connections).

Use the following commands to create these items. Both Azure CLI and PowerShell are supported. To create your Azure resources using Azure PowerShell, you also need the [Az PowerShell module](/en-us/powershell/azure/install-az-ps), version 5.9.0 or later.

If you haven't done already, sign in to Azure.

`az login`

The

command signs you into your Azure account.`az login`

Create a resource group named

`AzureFunctionsContainers-rg`

in your chosen region.`az group create --name AzureFunctionsContainers-rg --location <REGION>`

The

command creates a resource group. In the above command, replace`az group create`

`<REGION>`

with a region near you, using an available region code returned from the[az account list-locations](/en-us/cli/azure/account#az-account-list-locations)command.Create a general-purpose storage account in your resource group and region.

`az storage account create --name <STORAGE_NAME> --location <REGION> --resource-group AzureFunctionsContainers-rg --sku Standard_LRS`

The

command creates the storage account.`az storage account create`

In the previous example, replace

`<STORAGE_NAME>`

with a name that is appropriate to you and unique in Azure Storage. Storage names must contain 3 to 24 characters numbers and lowercase letters only.`Standard_LRS`

specifies a general-purpose account[supported by Functions](storage-considerations#storage-account-requirements).Use the command to create a Premium plan for Azure Functions named

`myPremiumPlan`

in the**Elastic Premium 1**pricing tier (`--sku EP1`

), in your`<REGION>`

, and in a Linux container (`--is-linux`

).`az functionapp plan create --resource-group AzureFunctionsContainers-rg --name myPremiumPlan --location <REGION> --number-of-workers 1 --sku EP1 --is-linux`

We use the Premium plan here, which can scale as needed. For more information about hosting, see

[Azure Functions hosting plans comparison](functions-scale). For more information on how to calculate costs, see the[Functions pricing page](https://azure.microsoft.com/pricing/details/functions/).The command also creates an associated Azure Application Insights instance in the same resource group, with which you can monitor your function app and view logs. For more information, see

[Monitor Azure Functions](functions-monitoring). The instance incurs no costs until you activate it.

## Create and configure a function app on Azure with the image

A function app on Azure manages the execution of your functions in your Azure Functions hosting plan. In this section, you use the Azure resources from the previous section to create a function app from an image in a container registry and configure it with a connection string to Azure Storage.

Create a function app using the following command, depending on your container registry:

`az functionapp create --name <APP_NAME> --storage-account <STORAGE_NAME> --resource-group AzureFunctionsContainers-rg --plan myPremiumPlan --image <LOGIN_SERVER>/azurefunctionsimage:v1.0.0 --registry-username <USERNAME> --registry-password <SECURE_PASSWORD>`

In this example, replace

`<STORAGE_NAME>`

with the name you used in the previous section for the storage account. Also, replace`<APP_NAME>`

with a globally unique name appropriate to you and`<DOCKER_ID>`

or`<LOGIN_SERVER>`

with your Docker Hub account ID or Container Registry server, respectively. When you're deploying from a custom container registry, the image name indicates the URL of the registry.When you first create the function app, it pulls the initial image from your Docker Hub. You can also

[Enable continuous deployment](functions-how-to-custom-container#enable-continuous-deployment-to-azure)to Azure from your container registry.Tip

You can use the

in the`DisableColor`

setting*host.json*file to prevent ANSI control characters from being written to the container logs.Use the following command to get the connection string for the storage account you created:

`az storage account show-connection-string --resource-group AzureFunctionsContainers-rg --name <STORAGE_NAME> --query connectionString --output tsv`

The connection string for the storage account is returned by using the

command.`az storage account show-connection-string`

Important

This article currently shows how to connect to the default storage account by using a connection string. For the best security, you should instead create a managed identity-based connection to Azure Storage using Microsoft Entra authentication. For more information, see the

[Functions developer guide](functions-reference#connections).Replace

`<STORAGE_NAME>`

with the name of the storage account you created earlier.Use the following command to add the setting to the function app:

`az functionapp config appsettings set --name <APP_NAME> --resource-group AzureFunctionsContainers-rg --settings AzureWebJobsStorage=<CONNECTION_STRING>`

The

command creates the setting.`az functionapp config appsettings set`

In this command, replace

`<APP_NAME>`

with the name of your function app and`<CONNECTION_STRING>`

with the connection string from the previous step. The connection should be a long encoded string that begins with`DefaultEndpointProtocol=`

.The function can now use this connection string to access the storage account.


## Verify your functions on Azure

With the image deployed to your function app in Azure, you can now invoke the function through HTTP requests.

Run the following

command to get the URL of your new function:`az functionapp function show`

`az functionapp function show --resource-group AzureFunctionsContainers-rg --name <APP_NAME> --function-name HttpExample --query invokeUrlTemplate`

Replace

`<APP_NAME>`

with the name of your function app.

- Use the URL you just obtained to call the
`HttpExample`

function endpoint, appending the query string`?name=Functions`

.

- Use the URL you just obtained to call the
`HttpExample`

function endpoint.

When you navigate to this URL, the browser must display similar output as when you ran the function locally.

## Clean up resources

If you want to continue working with Azure Function using the resources you created in this article, you can leave all those resources in place. Because you created a Premium Plan for Azure Functions, you'll incur one or two USD per day in ongoing costs.

To avoid ongoing costs, delete the `AzureFunctionsContainers-rg`

resource group to clean up all the resources in that group:

```
az group delete --name AzureFunctionsContainers-rg
```

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-kafka-output -->

# Apache Kafka output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The output binding enables an Azure Functions app to send messages to a Kafka topic.

Important

Kafka bindings are available for Functions on the [Flex Consumption plan](flex-consumption-plan), [Elastic Premium Plan](functions-premium-plan), and [Dedicated (App Service) plan](dedicated-plan). They are only supported on version 4.x of the Functions runtime.

## Example

How you use the binding depends on the C# modality in your function app. You can use one of the following modalities:

A compiled C# function that uses an [isolated worker process class library](dotnet-isolated-process-guide) that runs in a process that's separate from the runtime.

The attributes you use depend on the specific event provider.

The following example uses a custom return type named `MultipleOutputType`

, which consists of an HTTP response and a Kafka output.

```
[Function("KafkaOutput")]
public static MultipleOutputType Output(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = null)] HttpRequestData req,
FunctionContext executionContext)
{
var log = executionContext.GetLogger("HttpFunction");
log.LogInformation("C# HTTP trigger function processed a request.");
string message = req.FunctionContext
.BindingContext
.BindingData["message"]
.ToString();
var response = req.CreateResponse(HttpStatusCode.OK);
return new MultipleOutputType()
{
Kevent = message,
HttpResponse = response
};
}
```


In the `MultipleOutputType`

class, `Kevent`

is the output binding variable for the Kafka binding.

```
public class MultipleOutputType
{
[KafkaOutput("BrokerList",
"topic",
Username = "ConfluentCloudUserName",
Password = "ConfluentCloudPassword",
Protocol = BrokerProtocol.SaslSsl,
AuthenticationMode = BrokerAuthenticationMode.Plain
)]
public string Kevent { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
```


To send a batch of events, pass a string array to the output type, as shown in the following example:

```
[Function("KafkaOutputMany")]
public static MultipleOutputTypeForBatch Output(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = null)] HttpRequestData req,
FunctionContext executionContext)
{
var log = executionContext.GetLogger("HttpFunction");
log.LogInformation("C# HTTP trigger function processed a request.");
var response = req.CreateResponse(HttpStatusCode.OK);
string[] messages = new string[2];
messages[0] = "one";
messages[1] = "two";
return new MultipleOutputTypeForBatch()
{
Kevents = messages,
HttpResponse = response
};
}
```


The string array is defined as the `Kevents`

property on the class, and the output binding is defined on this property:

```
public class MultipleOutputTypeForBatch
{
[KafkaOutput("BrokerList",
"topic",
Username = "ConfluentCloudUserName",
Password = "ConfluentCloudPassword",
Protocol = BrokerProtocol.SaslSsl,
AuthenticationMode = BrokerAuthenticationMode.Plain
)]
public string[] Kevents { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
```


The following function adds headers to the Kafka output data:

```
[Function("KafkaOutputWithHeaders")]
public static MultipleOutputType Output(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = null)] HttpRequestData req,
FunctionContext executionContext)
{
var log = executionContext.GetLogger("HttpFunction");
log.LogInformation("C# HTTP trigger function processed a request.");
string message = req.FunctionContext
.BindingContext
.BindingData["message"]
.ToString();
string kevent = "{ \"Offset\":364,\"Partition\":0,\"Topic\":\"kafkaeventhubtest1\",\"Timestamp\":\"2022-04-09T03:20:06.591Z\", \"Value\": \"" + message + "\", \"Headers\": [{ \"Key\": \"test\", \"Value\": \"dotnet-isolated\" }] }";
var response = req.CreateResponse(HttpStatusCode.OK);
return new MultipleOutputType()
{
Kevent = kevent,
HttpResponse = response
};
}
```


For a complete set of working .NET examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/dotnet-isolated/confluent).

The usage of the output binding depends on your version of the Node.js programming model.

In the Node.js v4 model, you define your output binding directly in your function code. For more information, see the [Azure Functions Node.js developer guide](functions-reference-node?pivots=nodejs-model-v4).

In these examples, the event providers are either Confluent or Azure Event Hubs. These examples show a Kafka output binding for a function that an HTTP request triggers and sends data from the request to the Kafka topic.

```
import {
app,
HttpRequest,
HttpResponseInit,
InvocationContext,
output,
} from "@azure/functions";
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
export async function kafkaOutputWithHttp(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const body = await request.text();
const queryName = request.query.get("name");
const parsedbody = JSON.parse(body);
const name = queryName || parsedbody.name || "world";
context.extraOutputs.set(kafkaOutput, `Hello, ${parsedbody.name}!`);
context.log(
`Sending message to kafka: ${context.extraOutputs.get(kafkaOutput)}`
);
return {
body: `Message sent to kafka with value: ${context.extraOutputs.get(
kafkaOutput
)}`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputWithHttp,
});
```


To send events in a batch, send an array of messages, as shown in these examples:

```
const { app, output } = require("@azure/functions");
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
async function kafkaOutputManyWithHttp(request, context) {
context.log(`Http function processed request for url "${request.url}"`);
const queryName = request.query.get("name");
const body = await request.text();
const parsedbody = body ? JSON.parse(body) : {};
parsedbody.name = parsedbody.name || "world";
const name = queryName || parsedbody.name;
context.extraOutputs.set(kafkaOutput, `Message one. Hello, ${name}!`);
context.extraOutputs.set(kafkaOutput, `Message two. Hello, ${name}!`);
return {
body: `Messages sent to kafka.`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputManyWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputManyWithHttp,
});
```


These examples show how to send an event message with headers to a Kafka topic:

```
import {
app,
HttpRequest,
HttpResponseInit,
InvocationContext,
output,
} from "@azure/functions";
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
export async function kafkaOutputWithHttp(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const body = await request.text();
const parsedbody = JSON.parse(body);
// assuming body is of the format { "key": "key", "value": {JSON object} }
context.extraOutputs.set(
kafkaOutput,
`{ "Offset":364,"Partition":0,"Topic":"test-topic","Timestamp":"2022-04-09T03:20:06.591Z", "Value": "${JSON.stringify(
parsedbody.value
).replace(/"/g, '\\"')}", "Key":"${
parsedbody.key
}", "Headers": [{ "Key": "language", "Value": "javascript" }] }`
);
context.log(
`Sending message to kafka: ${context.extraOutputs.get(kafkaOutput)}`
);
return {
body: `Message sent to kafka with value: ${context.extraOutputs.get(
kafkaOutput
)}`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputWithHttp,
});
```


For a complete set of working JavaScript examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/javascript-v4/src/functions).

```
import {
app,
HttpRequest,
HttpResponseInit,
InvocationContext,
output,
} from "@azure/functions";
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
export async function kafkaOutputWithHttp(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const body = await request.text();
const queryName = request.query.get("name");
const parsedbody = JSON.parse(body);
const name = queryName || parsedbody.name || "world";
context.extraOutputs.set(kafkaOutput, `Hello, ${parsedbody.name}!`);
context.log(
`Sending message to kafka: ${context.extraOutputs.get(kafkaOutput)}`
);
return {
body: `Message sent to kafka with value: ${context.extraOutputs.get(
kafkaOutput
)}`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputWithHttp,
});
```


To send events in a batch, send an array of messages, as shown in these examples:

```
import {
app,
HttpRequest,
HttpResponseInit,
InvocationContext,
output,
} from "@azure/functions";
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
export async function kafkaOutputManyWithHttp(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const queryName = request.query.get("name");
const body = await request.text();
const parsedbody = body ? JSON.parse(body) : {};
parsedbody.name = parsedbody.name || "world";
const name = queryName || parsedbody.name;
context.extraOutputs.set(kafkaOutput, `Message one. Hello, ${name}!`);
context.extraOutputs.set(kafkaOutput, `Message two. Hello, ${name}!`);
return {
body: `Messages sent to kafka.`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputManyWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputManyWithHttp,
});
```


These examples show how to send an event message with headers to a Kafka topic:

```
import {
app,
HttpRequest,
HttpResponseInit,
InvocationContext,
output,
} from "@azure/functions";
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
export async function kafkaOutputWithHttp(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const body = await request.text();
const parsedbody = JSON.parse(body);
// assuming body is of the format { "key": "key", "value": {JSON object} }
context.extraOutputs.set(
kafkaOutput,
`{ "Offset":364,"Partition":0,"Topic":"test-topic","Timestamp":"2022-04-09T03:20:06.591Z", "Value": "${JSON.stringify(
parsedbody.value
).replace(/"/g, '\\"')}", "Key":"${
parsedbody.key
}", "Headers": [{ "Key": "language", "Value": "typescript" }] }`
);
context.log(
`Sending message to kafka: ${context.extraOutputs.get(kafkaOutput)}`
);
return {
body: `Message sent to kafka with value: ${context.extraOutputs.get(
kafkaOutput
)}`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputWithHttp,
});
```


For a complete set of working TypeScript examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/typescript-v4/src/functions).

The specific properties of the function.json file depend on your event provider, which in these examples are either Confluent or Azure Event Hubs. The following examples show a Kafka output binding for a function that an HTTP request triggers and sends data from the request to the Kafka topic.

The following function.json defines the trigger for the specific provider in these examples:

```
{
"bindings": [
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "Request",
"methods": [
"get"
]
},
{
"type": "kafka",
"name": "outputMessage",
"brokerList": "BrokerList",
"topic": "topic",
"username" : "%ConfluentCloudUserName%",
"password" : "%ConfluentCloudPassword%",
"protocol": "SASLSSL",
"authenticationMode": "PLAIN",
"direction": "out"
},
{
"type": "http",
"direction": "out",
"name": "Response"
}
]
}
```


The following code sends a message to the topic:

```
using namespace System.Net
# Input bindings are passed in via param block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell HTTP trigger function processed a request."
# Interact with query parameters or the body of the request.
$message = $Request.Query.Message
$message
Push-OutputBinding -Name outputMessage -Value ($message)
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
})
```


The following code sends multiple messages as an array to the same topic:

```
using namespace System.Net
# Input bindings are passed in via param block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell HTTP trigger function processed a request."
$message = @("one", "two")
Push-OutputBinding -Name outputMessage -Value ($message)
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
})
```


The following example shows how to send an event message with headers to the same Kafka topic:

```
using namespace System.Net
# Input bindings are passed in via param block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell HTTP trigger function processed a request."
# Interact with query parameters or the body of the request.
$message = $Request.Query.Message
if (-not $message) {
$message = $Request.Body.Message
}
$kevent = @{
Offset = 364
Partition = 0
Topic = "kafkaeventhubtest1"
Timestamp = "2022-04-09T03:20:06.591Z"
Value = $message
Headers= @(@{
Key= "test"
Value= "powershell"
}
)
}
Push-OutputBinding -Name Message -Value $kevent
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = 'ok'
})
```


For a complete set of working PowerShell examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/powershell/).

The usage of the output binding depends on your version of the Python programming model.

In the Python v2 model, you define your output binding directly in your function code using decorators. For more information, see the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

These examples show a Kafka output binding for a function that an HTTP request triggers and sends data from the request to the Kafka topic.

```
input_msg = req.params.get('message')
outputMessage.set(input_msg)
return 'OK'
@KafkaOutput.function_name(name="KafkaOutputMany")
@KafkaOutput.route(route="kafka_output_many")
@KafkaOutput.kafka_output(arg_name="outputMessage", topic="KafkaTopic", broker_list="KafkaBrokerList", username="KafkaUsername", password="KafkaPassword", protocol="SaslSsl", authentication_mode="Plain", data_type="string")
def kafka_output_many(req: func.HttpRequest, outputMessage: func.Out[str] ) -> func.HttpResponse:
outputMessage.set(json.dumps(['one', 'two']))
return 'OK'
```


To send events in a batch, send an array of messages, as shown in these examples:

```
@KafkaOutput.route(route="kafka_output_with_headers")
@KafkaOutput.kafka_output(arg_name="out", topic="KafkaTopic", broker_list="KafkaBrokerList", username="KafkaUsername", password="KafkaPassword", protocol="SaslSsl", authentication_mode="Plain")
def kafka_output_with_headers(req: func.HttpRequest, out: func.Out[str]) -> func.HttpResponse:
message = req.params.get('message')
kevent = { "Offset":0,"Partition":0,"Topic":"dummy","Timestamp":"2022-04-09T03:20:06.591Z", "Value": message, "Headers": [{ "Key": "test", "Value": "python" }] }
out.set(json.dumps(kevent))
return 'OK'
@KafkaOutput.function_name(name="KafkaOutputManyWithHeaders")
@KafkaOutput.route(route="kafka_output_many_with_headers")
@KafkaOutput.kafka_output(arg_name="out", topic="KafkaTopic", broker_list="KafkaBrokerList", username="KafkaUsername", password="KafkaPassword", protocol="SaslSsl", authentication_mode="Plain")
def kafka_output_many_with_headers(req: func.HttpRequest, out: func.Out[str]) -> func.HttpResponse:
kevent = [{ "Offset": 364, "Partition":0,"Topic":"kafkaeventhubtest1","Timestamp":"2022-04-09T03:20:06.591Z", "Value": "one", "Headers": [{ "Key": "test", "Value": "python" }] },
```


These examples show how to send an event message with headers to a Kafka topic:

For a complete set of working Python examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/python-v2/).

The annotations you use to configure the output binding depend on the specific event provider.

The following function sends a message to the Kafka topic.

```
@FunctionName("KafkaOutput")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> request,
@KafkaOutput(
name = "kafkaOutput",
topic = "topic",
brokerList="%BrokerList%",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
protocol = BrokerProtocol.SASLSSL
) OutputBinding<String> output,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
// Parse query parameter
String query = request.getQueryParameters().get("message");
String message = request.getBody().orElse(query);
context.getLogger().info("Message:" + message);
output.setValue(message);
return request.createResponseBuilder(HttpStatus.OK).body("Ok").build();
```


The following example shows how to send multiple messages to a Kafka topic.

```
@FunctionName("KafkaOutputMany")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> request,
@KafkaOutput(
name = "kafkaOutput",
topic = "topic",
brokerList="%BrokerList%",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
protocol = BrokerProtocol.SASLSSL
) OutputBinding<String[]> output,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
String[] messages = new String[2];
messages[0] = "one";
messages[1] = "two";
output.setValue(messages);
return request.createResponseBuilder(HttpStatus.OK).body("Ok").build();
}
```


In this example, the output binding parameter is changed to string array.

The last example uses these `KafkaEntity`

and `KafkaHeader`

classes:

```
public class KafkaEntity {
public int Offset;
public int Partition;
public String Timestamp;
public String Topic;
public String Value;
public KafkaHeaders Headers[];
public KafkaEntity(int Offset, int Partition, String Topic, String Timestamp, String Value,KafkaHeaders[] headers) {
this.Offset = Offset;
this.Partition = Partition;
this.Topic = Topic;
this.Timestamp = Timestamp;
this.Value = Value;
this.Headers = headers;
}
```


```
public class KafkaHeaders{
public String Key;
public String Value;
public KafkaHeaders(String key, String value) {
this.Key = key;
this.Value = value;
}
```


The following example function sends a message with headers to a Kafka topic.

```
@FunctionName("KafkaOutputWithHeaders")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> request,
@KafkaOutput(
name = "kafkaOutput",
topic = "topic",
brokerList="%BrokerList%",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
protocol = BrokerProtocol.SASLSSL
) OutputBinding<KafkaEntity> output,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
// Parse query parameter
String query = request.getQueryParameters().get("message");
String message = request.getBody().orElse(query);
KafkaHeaders[] headers = new KafkaHeaders[1];
headers[0] = new KafkaHeaders("test", "java");
KafkaEntity kevent = new KafkaEntity(364, 0, "topic", "2022-04-09T03:20:06.591Z", message, headers);
output.setValue(kevent);
return request.createResponseBuilder(HttpStatus.OK).body("Ok").build();
}
```


For a complete set of working Java examples for Confluent, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/java/confluent/src/main/java/com/contoso/kafka).

## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the `Kafka`

attribute to define the function trigger.

The following table explains the properties you can set by using this attribute:

| Parameter | Description |
|---|---|
BrokerList |
(Required) The list of Kafka brokers to which the output is sent. See
|

**Topic****AvroSchema****KeyAvroSchema****KeyDataType**`KeyAvroSchema`

is set, this value is generic record. Accepted values are `Int`

, `Long`

, `String`

, and `Binary`

.**MaxMessageBytes**`1`

.**BatchSize**`10000`

.**EnableIdempotence**`true`

, guarantees that messages are successfully produced exactly once and in the original produce order, with a default value of `false`

**MessageTimeoutMs**`300000`

. A time of `0`

is infinite. This value is the maximum time used to deliver a message (including retries). Delivery error occurs when either the retry count or the message timeout are exceeded.**RequestTimeoutMs**`5000`

.**MaxRetries**`2`

. Retrying may cause reordering, unless `EnableIdempotence`

is set to `true`

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

The `KafkaOutput`

annotation enables you to create a function that writes to a specific topic. Supported options include the following elements:

| Element | Description |
|---|---|
name |
The name of the variable that represents the brokered data in function code. |
brokerList |
(Required) The list of Kafka brokers to which the output is sent. See
|

**topic****dataType**`string`

, the input is treated as just a string. When `binary`

, the message is received as binary data, and Functions tries to deserialize it to an actual parameter type byte[].**avroSchema**[Currently not supported for Java](https://github.com/Azure/azure-functions-java-library/issues/198).)**maxMessageBytes**`1`

.**batchSize**`10000`

.**enableIdempotence**`true`

, guarantees that messages are successfully produced exactly once and in the original produce order, with a default value of `false`

.**messageTimeoutMs**`300000`

. A time of `0`

is infinite. This value is the maximum time used to deliver a message (including retries). Delivery error occurs when either the retry count or the message timeout are exceeded.**requestTimeoutMs**`5000`

.**maxRetries**`2`

. Retrying might cause reordering, unless `EnableIdempotence`

is set to `true`

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

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****schemaRegistryUrl**[Connections](#connections)for more information.**schemaRegistryUsername**[Connections](#connections)for more information.**schemaRegistryPassword**[Connections](#connections)for more information.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

function.json property |
Description |
|---|---|
type |
Set to `kafka` . |
direction |
Set to `out` . |
name |
The name of the variable that represents the brokered data in function code. |
brokerList |
(Required) The list of Kafka brokers to which the output is sent. See
|

**topic****avroSchema****keyAvroSchema****keyDataType**`keyAvroSchema`

is set, this value is generic record. Accepted values are `Int`

, `Long`

, `String`

, and `Binary`

.**maxMessageBytes**`1`

.**batchSize**`10000`

.**enableIdempotence**`true`

, guarantees that messages are successfully produced exactly once and in the original produce order, with a default value of `false`

.**messageTimeoutMs**`300000`

. A time of `0`

is infinite. This value is the maximum time used to deliver a message (including retries). Delivery error occurs when either the retry count or the message timeout are exceeded.**requestTimeoutMs**`5000`

.**maxRetries**`2`

. Retrying might cause reordering, unless `EnableIdempotence`

is set to `true`

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

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****sslCertificatePEM**[Connections](#connections)for more information.**sslKeyPEM**[Connections](#connections)for more information.**sslCaPEM**[Connections](#connections)for more information.**sslCertificateandKeyPEM**[Connections](#connections)for more information.**schemaRegistryUrl**[Connections](#connections)for more information.**schemaRegistryUsername**[Connections](#connections)for more information.**schemaRegistryPassword**[Connections](#connections)for more information.**oAuthBearerMethod**`oidc`

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
Set to `kafka` . |
direction |
Set to `out` . |
name |
The name of the variable that represents the brokered data in function code. |
broker_list |
(Required) The list of Kafka brokers to which the output is sent. See
|

**topic****avroSchema****maxMessageBytes**`1`

.**batchSize**`10000`

.**enableIdempotence**`true`

, guarantees that messages are successfully produced exactly once and in the original produce order, with a default value of `false`

.**messageTimeoutMs**`300000`

. A time of `0`

is infinite. This value is the maximum time used to deliver a message (including retries). Delivery error occurs when either the retry count or the message timeout are exceeded.**requestTimeoutMs**`5000`

.**maxRetries**`2`

. Retrying might cause reordering, unless `EnableIdempotence`

is set to `true`

.**authentication_mode**`NOTSET`

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

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****schema_registry_url**[Connections](#connections)for more information.**schema_registry_username**[Connections](#connections)for more information.**schema_registry_password**[Connections](#connections)for more information.**o_auth_bearer_method**`oidc`

and `default`

.**o_auth_bearer_client_id**`o_auth_bearer_method`

is set to `oidc`

, this specifies the OAuth bearer client ID. See [Connections](#connections)for more information.**o_auth_bearer_client_secret**`o_auth_bearer_method`

is set to `oidc`

, this specifies the OAuth bearer client secret. See [Connections](#connections)for more information.**o_auth_bearer_scope****o_auth_bearer_token_endpoint_url**`oidc`

method is used. See [Connections](#connections)for more information.Note

Certificate PEM-related properties and Avro key-related properties aren't yet available in the Python library.

## Usage

The offset, partition, and timestamp for the event are generated at runtime. You can set only the value and headers inside the function. You set the topic in the function.json file.

Make sure you have access to the Kafka topic where you want to write. You configure the binding with access and connection credentials to the Kafka topic.

In a Premium plan, you must enable runtime scale monitoring for the Kafka output to scale out to multiple instances. To learn more, see [Enable runtime scaling](functions-bindings-kafka#enable-runtime-scaling).

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-data-explorer-input -->

# Azure Data Explorer input bindings for Azure Functions (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Data Explorer input binding retrieves data from a database.

## Examples

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

More samples for the Azure Data Explorer input binding (out of process) are available in the [GitHub repository](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-outofproc).

This section contains the following examples:

The examples refer to a `Product`

class and the Products table, both of which are defined in the previous sections.

### HTTP trigger, get row by ID from query string

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a single record. The function is triggered by an HTTP request that uses a query string to specify the ID. That ID is used to retrieve a `Product`

record with the specified query.

Note

The HTTP query string parameter is case sensitive.

```
using System.Text.Json.Nodes;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.Kusto;
using Microsoft.Azure.Functions.Worker.Http;
using Microsoft.Azure.WebJobs.Extensions.Kusto.SamplesOutOfProc.OutputBindingSamples.Common;
namespace Microsoft.Azure.WebJobs.Extensions.Kusto.SamplesOutOfProc.InputBindingSamples
{
public static class GetProductsQuery
{
[Function("GetProductsQuery")]
public static JsonArray Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "getproductsquery")] HttpRequestData req,
[KustoInput(Database: "productsdb",
KqlCommand = "declare query_parameters (productId:long);Products | where ProductID == productId",
KqlParameters = "@productId={Query.productId}",Connection = "KustoConnectionString")] JsonArray products)
{
return products;
}
}
}
```


### HTTP trigger, get multiple rows from route parameter

The following example shows a [C# function](functions-dotnet-class-library) that retrieves records returned by the query (based on the name of the product, in this case). The function is triggered by an HTTP request that uses route data to specify the value of a query parameter. That parameter is used to filter the `Product`

records in the specified query.

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.Kusto;
using Microsoft.Azure.Functions.Worker.Http;
using Microsoft.Azure.WebJobs.Extensions.Kusto.SamplesOutOfProc.OutputBindingSamples.Common;
namespace Microsoft.Azure.WebJobs.Extensions.Kusto.SamplesOutOfProc.InputBindingSamples
{
public static class GetProductsFunction
{
[Function("GetProductsFunction")]
public static IEnumerable<Product> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "getproductsfn/{name}")] HttpRequestData req,
[KustoInput(Database: "productsdb",
KqlCommand = "declare query_parameters (name:string);GetProductsByName(name)",
KqlParameters = "@name={name}",Connection = "KustoConnectionString")] IEnumerable<Product> products)
{
return products;
}
}
}
```


More samples for the Java Azure Data Explorer input binding are available in the [GitHub repository](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-java).

This section contains the following examples:

The examples refer to a `Product`

class (in a separate file `Product.java`

) and a corresponding database table.

```
package com.microsoft.azure.kusto.common;
import com.fasterxml.jackson.annotation.JsonProperty;
public class Product {
@JsonProperty("ProductID")
public long ProductID;
@JsonProperty("Name")
public String Name;
@JsonProperty("Cost")
public double Cost;
public Product() {
}
public Product(long ProductID, String name, double Cost) {
this.ProductID = ProductID;
this.Name = name;
this.Cost = Cost;
}
}
```


### HTTP trigger, get multiple rows

The example uses a route parameter to specify the name of the ID of the products. All matching products are retrieved from the products table.

```
package com.microsoft.azure.kusto.inputbindings;
import com.microsoft.azure.functions.HttpMethod;
import com.microsoft.azure.functions.HttpRequestMessage;
import com.microsoft.azure.functions.HttpResponseMessage;
import com.microsoft.azure.functions.HttpStatus;
import com.microsoft.azure.functions.annotation.AuthorizationLevel;
import com.microsoft.azure.functions.annotation.FunctionName;
import com.microsoft.azure.functions.annotation.HttpTrigger;
import com.microsoft.azure.functions.kusto.annotation.KustoInput;
import com.microsoft.azure.kusto.common.Product;
import java.util.Optional;
public class GetProducts {
@FunctionName("GetProducts")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {
HttpMethod.GET}, authLevel = AuthorizationLevel.ANONYMOUS, route = "getproducts/{productId}") HttpRequestMessage<Optional<String>> request,
@KustoInput(name = "getjproducts", kqlCommand = "declare query_parameters (productId:long);Products | where ProductID == productId",
kqlParameters = "@productId={productId}", database = "productsdb", connection = "KustoConnectionString") Product[] products) {
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(products)
.build();
}
}
```


### HTTP trigger, get row by ID from query string

The following example shows a query for the products table by the product name. The function is triggered by an HTTP request that uses a query string to specify the value of a query parameter. That parameter is used to filter the `Product`

records in the specified query.

```
package com.microsoft.azure.kusto.inputbindings;
import com.microsoft.azure.functions.HttpMethod;
import com.microsoft.azure.functions.HttpRequestMessage;
import com.microsoft.azure.functions.HttpResponseMessage;
import com.microsoft.azure.functions.HttpStatus;
import com.microsoft.azure.functions.annotation.AuthorizationLevel;
import com.microsoft.azure.functions.annotation.FunctionName;
import com.microsoft.azure.functions.annotation.HttpTrigger;
import com.microsoft.azure.functions.kusto.annotation.KustoInput;
import com.microsoft.azure.kusto.common.Product;
import java.util.Optional;
public class GetProductsQueryString {
@FunctionName("GetProductsQueryString")
public HttpResponseMessage run(@HttpTrigger(name = "req", methods = {
HttpMethod.GET}, authLevel = AuthorizationLevel.ANONYMOUS, route = "getproducts") HttpRequestMessage<Optional<String>> request,
@KustoInput(name = "getjproductsquery", kqlCommand = "declare query_parameters (name:string);GetProductsByName(name)",
kqlParameters = "@name={Query.name}", database = "productsdb", connection = "KustoConnectionString") Product[] products) {
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(products)
.build();
}
}
```


More samples for the Azure Data Explorer input binding are available in the [GitHub repository](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-node).

This section contains the following examples:

The examples refer to a database table:

### HTTP trigger, get multiple rows

The following example shows an Azure Data Explorer input binding in a *function.json* file and a JavaScript function that reads from a query and returns the results in the HTTP response.

The following binding data is in the *function.json* file:

```
{
"bindings": [
{
"authLevel": "function",
"name": "req",
"direction": "in",
"type": "httpTrigger",
"methods": [
"get"
],
"route": "getproducts/{productId}"
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"name": "productget",
"type": "kusto",
"database": "productsdb",
"direction": "in",
"kqlCommand": "declare query_parameters (productId:long);Products | where ProductID == productId",
"kqlParameters": "@productId={productId}",
"connection": "KustoConnectionString"
}
],
"disabled": false
}
```


The [configuration](#configuration) section explains these properties.

The following snippet is sample JavaScript code:

```
module.exports = async function (context, req, productget) {
return {
status: 200,
body: productget
};
}
```


### HTTP trigger, get row by name from query string

The following example shows a query for the products table by the product name. The function is triggered by an HTTP request that uses a query string to specify the value of a query parameter. That parameter is used to filter the `Product`

records in the specified query.

The following binding data is in the *function.json* file:

```
{
"bindings": [
{
"authLevel": "function",
"name": "req",
"direction": "in",
"type": "httpTrigger",
"methods": [
"get"
],
"route": "getproductsfn"
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"name": "productfnget",
"type": "kusto",
"database": "productsdb",
"direction": "in",
"kqlCommand": "declare query_parameters (name:string);GetProductsByName(name)",
"kqlParameters": "@name={Query.name}",
"connection": "KustoConnectionString"
}
],
"disabled": false
}
```


The [configuration](#configuration) section explains these properties.

The following snippet is sample JavaScript code:

```
module.exports = async function (context, req, producproductfngettget) {
return {
status: 200,
body: productfnget
};
}
```


More samples for the Azure Data Explorer input binding are available in the [GitHub repository](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-python).

This section contains the following examples:

### HTTP trigger, get multiple rows

The following example shows an Azure Data Explorer input binding in a *function.json* file and a Python function that reads from a query and returns the results in the HTTP response.

The following binding data is in the *function.json* file:

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"authLevel": "Anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"get"
],
"route": "getproducts/{productId}"
},
{
"type": "http",
"direction": "out",
"name": "$return"
},
{
"name": "productsdb",
"type": "kusto",
"database": "sdktestsdb",
"direction": "in",
"kqlCommand": "declare query_parameters (productId:long);Products | where ProductID == productId",
"kqlParameters": "@productId={Query.productId}",
"connection": "KustoConnectionString"
}
]
}
```


The [configuration](#configuration) section explains these properties.

The following snippet is sample Python code:

```
import azure.functions as func
from Common.product import Product
def main(req: func.HttpRequest, products: str) -> func.HttpResponse:
return func.HttpResponse(
products,
status_code=200,
mimetype="application/json"
)
```


### HTTP trigger, get row by ID from query string

The following example shows a query for the products table by the product name. The function is triggered by an HTTP request that uses a query string to specify the value of a query parameter. That parameter is used to filter the `Product`

records in the specified query.

The following binding data is in the *function.json* file:

```
{
"bindings": [
{
"authLevel": "function",
"name": "req",
"direction": "in",
"type": "httpTrigger",
"methods": [
"get"
],
"route": "getproductsfn"
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"name": "productfnget",
"type": "kusto",
"database": "productsdb",
"direction": "in",
"kqlCommand": "declare query_parameters (name:string);GetProductsByName(name)",
"kqlParameters": "@name={Query.name}",
"connection": "KustoConnectionString"
}
],
"disabled": false
}
```


The [configuration](#configuration) section explains these properties.

The following snippet is sample Python code:

```
import azure.functions as func
def main(req: func.HttpRequest, products: str) -> func.HttpResponse:
return func.HttpResponse(
products,
status_code=200,
mimetype="application/json"
)
```


## Attributes

The [C# library](functions-dotnet-class-library) uses the [KustoAttribute](https://github.com/Azure/Webjobs.Extensions.Kusto/blob/main/src/KustoAttribute.cs) attribute to declare the Azure Data Explorer bindings on the function, which has the following properties.

| Attribute property | Description |
|---|---|
| Database | Required. The database against which the query must be executed. |
| Connection | Required. The name of the variable that holds the connection string, resolved through environment variables or through function app settings. Defaults to look up on the variable `KustoConnectionString` . At runtime, this variable is looked up against the environment. Documentation on the connection string is at
`"KustoConnectionString": "Data Source=https://your_cluster.kusto.windows.net;Database=your_Database;Fed=True;AppClientId=your_AppId;AppKey=your_AppKey;Authority Id=your_TenantId` . |
| KqlCommand | Required. The `KqlQuery` parameter that must be executed. Can be a KQL query or a KQL function call. |
| KqlParameters | Optional. Parameters that act as predicate variables for `KqlCommand` . For example, "@name={name},@Id={id}", where {name} and {id} are substituted at runtime with actual values acting as predicates. The parameter name and the parameter value can't contain a comma (`,` ) or an equal sign (`=` ). |
| ManagedServiceIdentity | Optional. You can use a managed identity to connect to Azure Data Explorer. To use a system managed identity, use "system." Any other identity names are interpreted as a user managed identity. |

## Annotations

The [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime) uses the [ @KustoInput](https://github.com/Azure/Webjobs.Extensions.Kusto/blob/main/java-library/src/main/java/com/microsoft/azure/functions/kusto/annotation/KustoInput.java) annotation (

`com.microsoft.azure.functions.kusto.annotation.KustoInput`

).| Element | Description |
|---|---|
| name | Required. The name of the variable that represents the query results in function code. |
| database | Required. The database against which the query must be executed. |
| connection | Required. The name of the variable that holds the connection string, resolved through environment variables or through function app settings. Defaults to look up on the variable `KustoConnectionString` . At runtime, this variable is looked up against the environment. Documentation on the connection string is at
`"KustoConnectionString": "Data Source=https://your_cluster.kusto.windows.net;Database=your_Database;Fed=True;AppClientId=your_AppId;AppKey=your_AppKey;Authority Id=your_TenantId` . |
| kqlCommand | Required. The `KqlQuery` parameter that must be executed. Can be a KQL query or a KQL function call. |
| kqlParameters | Optional. Parameters that act as predicate variables for `KqlCommand` . For example, "@name={name},@Id={id}", where {name} and {id} are substituted at runtime with actual values acting as predicates. The parameter name and the parameter value can't contain a comma (`,` ) or an equal sign (`=` ). |
| managedServiceIdentity | A managed identity can be used to connect to Azure Data Explorer. To use a system managed identity, use "system." Any other identity names are interpreted as a user managed identity. |

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
| type | Required. Must be set to `kusto` . |
| direction | Required. Must be set to `in` . |
| name | Required. The name of the variable that represents the query results in function code. |
| database | Required. The database against which the query must be executed. |
| connection | Required. The name of the variable that holds the connection string, resolved through environment variables or through function app settings. Defaults to look up on the variable `KustoConnectionString` . At runtime, this variable is looked up against the environment. Documentation on the connection string is at
`"KustoConnectionString": "Data Source=https://your_cluster.kusto.windows.net;Database=your_Database;Fed=True;AppClientId=your_AppId;AppKey=your_AppKey;Authority Id=your_TenantId` . |
| kqlCommand | Required. The `KqlQuery` parameter that must be executed. Can be a KQL query or a KQL function call. |
| kqlParameters | Optional. Parameters that act as predicate variables for `KqlCommand` . For example, "@name={name},@Id={id}", where {name} and {id} are substituted at runtime with actual values acting as predicates. The parameter name and the parameter value can't contain a comma (`,` ) or an equal sign (`=` ). |
| managedServiceIdentity | A managed identity can be used to connect to Azure Data Explorer. To use a system managed identity, use "system." Any other identity names are interpreted as a user managed identity. |

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

The attribute's constructor takes the database and the attributes `KQLCommand`

and `KQLParameters`

and the connection setting name. The KQL command can be a KQL statement or a KQL function. The connection string setting name corresponds to the application setting (in `local.settings.json`

for local development) that contains the [Kusto connection strings](/en-us/azure/data-explorer/kusto/api/connection-strings/kusto). For example: `"KustoConnectionString": "Data Source=https://your_cluster.kusto.windows.net;Database=your_Database;Fed=True;AppClientId=your_AppId;AppKey=your_AppKey;Authority Id=your_TenantId`

. Queries executed by the input binding are parameterized. The values provided in the KQL parameters are used at runtime.

Important

For optimal security, your function app should use managed identities when connecting to Azure Data Explorer instead of using a connection string, which contains keys. For more information, see [Kusto connection strings](/en-us/azure/data-explorer/kusto/api/connection-strings/kusto). For mananaged identity-based connections, you must set the `managedServiceIdentity`

property in the binding definition.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai-textcompletion-input -->

# Azure OpenAI text completion input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Azure OpenAI extension for Azure Functions is currently in preview.

The Azure OpenAI text completion input binding allows you to bring the results text completion APIs into your code executions. You can define the binding to use both predefined prompts with parameters or pass through an entire prompt.

For information on setup and configuration details of the Azure OpenAI extension, see [Azure OpenAI extensions for Azure Functions](functions-bindings-openai). To learn more about Azure OpenAI completions, see [Learn how to generate or manipulate text](/en-us/azure/ai-services/openai/how-to/completions).

Note

References and examples are only provided for the [Node.js v4 model](functions-reference-node?pivots=nodejs-model-v4).

Note

References and examples are only provided for the [Python v2 model](functions-reference-python?pivots=python-mode-decorators#programming-model).

Note

While both C# process models are supported, only [isolated worker model](dotnet-isolated-process-guide) examples are provided.

## Example

This example demonstrates the *templating* pattern, where the HTTP trigger function takes a `name`

parameter and embeds it into a text prompt, which is then sent to the Azure OpenAI completions API by the extension. The response to the prompt is returned in the HTTP response.

```
[Function(nameof(WhoIs))]
public static IActionResult WhoIs(
[HttpTrigger(AuthorizationLevel.Function, Route = "whois/{name}")] HttpRequestData req,
[TextCompletionInput("Who is {name}?", ChatModel = "%CHAT_MODEL_DEPLOYMENT_NAME%")] TextCompletionResponse response)
{
return new OkObjectResult(response.Content);
}
```


This example takes a prompt as input, sends it directly to the completions API, and returns the response as the output.

```
[Function(nameof(GenericCompletion))]
public static IActionResult GenericCompletion(
[HttpTrigger(AuthorizationLevel.Function, "post")] HttpRequestData req,
[TextCompletionInput("{Prompt}", ChatModel = "%CHAT_MODEL_DEPLOYMENT_NAME%")] TextCompletionResponse response,
ILogger log)
{
string text = response.Content;
return new OkObjectResult(text);
}
```


This example demonstrates the *templating* pattern, where the HTTP trigger function takes a `name`

parameter and embeds it into a text prompt, which is then sent to the Azure OpenAI completions API by the extension. The response to the prompt is returned in the HTTP response.

```
@FunctionName("WhoIs")
public HttpResponseMessage whoIs(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "whois/{name}")
HttpRequestMessage<Optional<String>> request,
@BindingName("name") String name,
@TextCompletion(prompt = "Who is {name}?", chatModel = "%CHAT_MODEL_DEPLOYMENT_NAME%", name = "response", isReasoningModel = false) TextCompletionResponse response,
final ExecutionContext context) {
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(response.getContent())
.build();
}
```


This example takes a prompt as input, sends it directly to the completions API, and returns the response as the output.

```
@FunctionName("GenericCompletion")
public HttpResponseMessage genericCompletion(
@HttpTrigger(
name = "req",
methods = {HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@TextCompletion(prompt = "{prompt}", chatModel = "%CHAT_MODEL_DEPLOYMENT_NAME%", name = "response", isReasoningModel = false) TextCompletionResponse response,
final ExecutionContext context) {
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(response.getContent())
.build();
}
```


This example demonstrates the *templating* pattern, where the HTTP trigger function takes a `name`

parameter and embeds it into a text prompt, which is then sent to the Azure OpenAI completions API by the extension. The response to the prompt is returned in the HTTP response.

```
const { app, input } = require("@azure/functions");
// This OpenAI completion input requires a {name} binding value.
const openAICompletionInput = input.generic({
prompt: 'Who is {name}?',
maxTokens: '100',
type: 'textCompletion',
chatModel: '%CHAT_MODEL_DEPLOYMENT_NAME%'
})
app.http('whois', {
methods: ['GET'],
route: 'whois/{name}',
authLevel: 'function',
extraInputs: [openAICompletionInput],
handler: async (_request, context) => {
var response = context.extraInputs.get(openAICompletionInput)
return { body: response.content.trim() }
}
});
```


This example demonstrates the *templating* pattern, where the HTTP trigger function takes a `name`

parameter and embeds it into a text prompt, which is then sent to the Azure OpenAI completions API by the extension. The response to the prompt is returned in the HTTP response.

```
import { app, input } from "@azure/functions";
// This OpenAI completion input requires a {name} binding value.
const openAICompletionInput = input.generic({
prompt: 'Who is {name}?',
maxTokens: '100',
type: 'textCompletion',
chatModel: '%CHAT_MODEL_DEPLOYMENT_NAME%'
})
app.http('whois', {
methods: ['GET'],
route: 'whois/{name}',
authLevel: 'function',
extraInputs: [openAICompletionInput],
handler: async (_request, context) => {
var response: any = context.extraInputs.get(openAICompletionInput)
return { body: response.content.trim() }
}
});
```


This example demonstrates the *templating* pattern, where the HTTP trigger function takes a `name`

parameter and embeds it into a text prompt, which is then sent to the Azure OpenAI completions API by the extension. The response to the prompt is returned in the HTTP response.

Here's the *function.json* file for `TextCompletionResponse`

:

```
{
"bindings": [
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "Request",
"route": "whois/{name}",
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
"type": "textCompletion",
"direction": "in",
"name": "TextCompletionResponse",
"prompt": "Who is {name}?",
"maxTokens": "100",
"chatModel": "%CHAT_MODEL_DEPLOYMENT_NAME%"
}
]
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

The code simply returns the text from the completion API as the response:

```
using namespace System.Net
param($Request, $TriggerMetadata, $TextCompletionResponse)
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $TextCompletionResponse.Content
})
```


This example demonstrates the *templating* pattern, where the HTTP trigger function takes a `name`

parameter and embeds it into a text prompt, which is then sent to the Azure OpenAI completions API by the extension. The response to the prompt is returned in the HTTP response.

```
@app.route(route="whois/{name}", methods=["GET"])
@app.text_completion_input(
arg_name="response",
prompt="Who is {name}?",
max_tokens="100",
chat_model="%CHAT_MODEL_DEPLOYMENT_NAME%",
)
def whois(req: func.HttpRequest, response: str) -> func.HttpResponse:
response_json = json.loads(response)
return func.HttpResponse(response_json["content"], status_code=200)
```


This example takes a prompt as input, sends it directly to the completions API, and returns the response as the output.

```
@app.route(route="genericcompletion", methods=["POST"])
@app.text_completion_input(
arg_name="response",
prompt="{Prompt}",
chat_model="%CHAT_MODEL_DEPLOYMENT_NAME%",
)
def genericcompletion(
req: func.HttpRequest,
response: str
) -> func.HttpResponse:
response_json = json.loads(response)
return func.HttpResponse(response_json["content"], status_code=200)
```


## Attributes

The specific attribute you apply to define a text completion input binding depends on your C# process mode.

In the [isolated worker model](dotnet-isolated-process-guide), apply `TextCompletionInput`

to define a text completion input binding.

The attribute supports these parameters:

| Parameter | Description |
|---|---|
Prompt |
Gets or sets the prompt to generate completions for, encoded as a string. |
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

The `TextCompletion`

annotation enables you to define a text completion input binding, which supports these parameters:

| Element | Description |
|---|---|
name |
Gets or sets the name of the input binding. |
prompt |
Gets or sets the prompt to generate completions for, encoded as a string. |
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

During the preview, define the input binding as a `generic_input_binding`

binding of type `textCompletion`

, which supports these parameters:

| Parameter | Description |
|---|---|
arg_name |
The name of the variable that represents the binding parameter. |
prompt |
Gets or sets the prompt to generate completions for, encoded as a string. |
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
Must be `textCompletion` . |
direction |
Must be `in` . |
name |
The name of the input binding. |
prompt |
Gets or sets the prompt to generate completions for, encoded as a string. |
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
prompt |
Gets or sets the prompt to generate completions for, encoded as a string. |
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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-add-output-binding-cosmos-db-vs-code -->

# Connect Azure Functions to Azure Cosmos DB using Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions lets you connect Azure services and other resources to functions without having to write your own integration code. These *bindings*, which represent both input and output, are declared within the function definition. Data from bindings is provided to the function as parameters. A *trigger* is a special type of input binding. Although a function has only one trigger, it can have multiple input and output bindings. To learn more, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings).

This article shows you how to use Visual Studio Code to connect [Azure Cosmos DB](/en-us/azure/cosmos-db/introduction) to the function you created in the previous quickstart article. The output binding that you add to this function writes data from the HTTP request to a JSON document stored in an Azure Cosmos DB container.

Before you begin, you must complete the [quickstart: Create a C# function in Azure using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-csharp). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

Before you begin, you must complete the [quickstart: Create a JavaScript function in Azure using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-javascript?pivot=nodejs-model-v3). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

Note

This article currently only supports [Node.js v3 for Functions](functions-reference-node?pivots=nodejs-model-v3).

Before you begin, you must complete the [quickstart: Create a Python function in Azure using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-python). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

## Configure your environment

Before you get started, make sure to install the [Azure Databases extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-cosmosdb) for Visual Studio Code.

## Create your Azure Cosmos DB account

Now, you create an Azure Cosmos DB account as a [serverless account type](/en-us/azure/cosmos-db/serverless). This consumption-based mode makes Azure Cosmos DB a strong option for serverless workloads.

In Visual Studio Code, select

**View**>**Command Palette...**then in the command palette search for`Azure Databases: Create Server...`

Provide the following information at the prompts:

Prompt Selection **Select an Azure Database Server**Choose **Core (NoSQL)**to create a document database that you can query by using a SQL syntax or a Query Copilot ([Preview](/en-us/azure/cosmos-db/nosql/query/how-to-enable-use-copilot)) converting natural language prompts to queries.[Learn more about the Azure Cosmos DB](/en-us/azure/cosmos-db/introduction).**Account name**Enter a unique name to identify your Azure Cosmos DB account. The account name can use only lowercase letters, numbers, and hyphens (-), and must be between 3 and 31 characters long. **Select a capacity model**Select **Serverless**to create an account in[serverless](/en-us/azure/cosmos-db/serverless)mode.**Select a resource group for new resources**Choose the resource group where you created your function app in the [previous article](how-to-create-function-vs-code?pivot=programming-language-csharp).**Select a location for new resources**Select a geographic location to host your Azure Cosmos DB account. Use the location that's closest to you or your users to get the fastest access to your data. After your new account is provisioned, a message is displayed in notification area.


## Create an Azure Cosmos DB database and container

Select the Azure icon in the Activity bar, expand

**Resources**>**Azure Cosmos DB**, right-click (Ctrl+select on macOS) your account, and select**Create database...**.Provide the following information at the prompts:

Prompt Selection **Database name**Type `my-database`

.**Enter and ID for your collection**Type `my-container`

.**Enter the partition key for the collection**Type `/id`

as the[partition key](/en-us/azure/cosmos-db/partitioning-overview).Select

**OK**to create the container and database.

## Update your function app settings

In the [previous quickstart article](how-to-create-function-vs-code?pivot=programming-language-csharp), you created a function app in Azure. In this article, you update your app to write JSON documents to the Azure Cosmos DB container you've created. To connect to your Azure Cosmos DB account, you must add its connection string to your app settings. You then download the new setting to your local.settings.json file so you can connect to your Azure Cosmos DB account when running locally.

In Visual Studio Code, right-click (Ctrl+select on macOS) on your new Azure Cosmos DB account, and select

**Copy Connection String**.Press

`F1`to open the command palette, then search for and run the command`Azure Functions: Add New Setting...`

.Choose the function app you created in the previous article. Provide the following information at the prompts:

Prompt Selection **Enter new app setting name**Type `CosmosDbConnectionString`

.**Enter value for "CosmosDbConnectionString"**Paste the connection string of your Azure Cosmos DB account you copied. You can also configure [Microsoft Entra identity](functions-bindings-cosmosdb-v2-trigger#connections)as an alternative.This creates an application setting named connection

`CosmosDbConnectionString`

in your function app in Azure. Now, you can download this setting to your local.settings.json file.Press

`F1`again to open the command palette, then search for and run the command`Azure Functions: Download Remote Settings...`

.Choose the function app you created in the previous article. Select

**Yes to all**to overwrite the existing local settings.

This downloads all of the setting from Azure to your local project, including the new connection string setting. Most of the downloaded settings aren't used when running locally.

## Register binding extensions

Because you're using an Azure Cosmos DB output binding, you must have the corresponding bindings extension installed before you run the project.

Except for HTTP and timer triggers, bindings are implemented as extension packages. Run the following [dotnet add package](/en-us/dotnet/core/tools/dotnet-add-package) command in the Terminal window to add the Azure Cosmos DB extension package to your project.

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.CosmosDB
```


Your project has been configured to use [extension bundles](extension-bundles), which automatically installs a predefined set of extension packages.

Extension bundles usage is enabled in the *host.json* file at the root of the project, which appears as follows:

```
{
"version": "2.0",
"logging": {
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"excludedTypes": "Request"
}
}
},
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
},
"concurrency": {
"dynamicConcurrencyEnabled": true,
"snapshotPersistenceEnabled": true
},
"extensions": {
"cosmosDB": {
"connectionMode": "Gateway"
}
}
}
```


Your project has been configured to use [extension bundles](extension-bundles), which automatically installs a predefined set of extension packages.

Extension bundles usage is enabled in the *host.json* file at the root of the project, which appears as follows:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[3.*, 4.0.0)"
}
}
```


Now, you can add the Azure Cosmos DB output binding to your project.

## Add an output binding

In a C# class library project, the bindings are defined as binding attributes on the function method.

Open the *HttpExample.cs* project file and add the following classes:

```
public class MultiResponse
{
[CosmosDBOutput("my-database", "my-container",
Connection = "CosmosDbConnectionSetting", CreateIfNotExists = true)]
public MyDocument Document { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
public class MyDocument {
public string id { get; set; }
public string message { get; set; }
}
```


The `MyDocument`

class defines an object that gets written to the database. The connection string for the Storage account is set by the `Connection`

property. In this case, you could omit `Connection`

because you're already using the default storage account.

The `MultiResponse`

class allows you to both write to the specified collection in the Azure Cosmos DB and return an HTTP success message. Because you need to return a `MultiResponse`

object, you need to also update the method signature.

Specific attributes specify the name of the container and the name of its parent database. The connection string for your Azure Cosmos DB account is set by the `CosmosDbConnectionString`

.

Binding attributes are defined directly in your function code. The [Azure Cosmos DB output configuration](functions-bindings-cosmosdb-v2-output#configuration) describes the fields required for an Azure Cosmos DB output binding.

For this `MultiResponse`

scenario, you need to add an `extraOutputs`

output binding to the function.

```
app.http('HttpExample', {
methods: ['GET', 'POST'],
extraOutputs: [sendToCosmosDb],
handler: async (request, context) => {
```


Add the following properties to the binding configuration:

```
const sendToCosmosDb = output.cosmosDB({
databaseName: 'my-database',
containerName: 'my-container',
createIfNotExists: false,
connection: 'CosmosDBConnectionString',
});
```


Binding attributes are defined directly in the *function_app.py* file. You use the `cosmos_db_output`

decorator to add an [Azure Cosmos DB output binding](functions-bindings-triggers-python#azure-cosmos-db-output-binding):

```
@app.cosmos_db_output(arg_name="outputDocument", database_name="my-database",
container_name="my-container", connection="CosmosDbConnectionString")
```


In this code, `arg_name`

identifies the binding parameter referenced in your code, `database_name`

and `container_name`

are the database and collection names that the binding writes to, and `connection`

is the name of an application setting that contains the connection string for the Azure Cosmos DB account, which is in the `CosmosDbConnectionString`

setting in the *local.settings.json* file.

## Add code that uses the output binding

Replace the existing Run method with the following code:

```
[Function("HttpExample")]
public static MultiResponse Run([HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequestData req,
FunctionContext executionContext)
{
var logger = executionContext.GetLogger("HttpExample");
logger.LogInformation("C# HTTP trigger function processed a request.");
var message = "Welcome to Azure Functions!";
var response = req.CreateResponse(HttpStatusCode.OK);
response.Headers.Add("Content-Type", "text/plain; charset=utf-8");
response.WriteString(message);
// Return a response to both HTTP trigger and Azure Cosmos DB output binding.
return new MultiResponse()
{
Document = new MyDocument
{
id = System.Guid.NewGuid().ToString(),
message = message
},
HttpResponse = response
};
}
```


Add code that uses the `extraInputs`

output binding object on `context`

to send a JSON document to the named output binding function, `sendToCosmosDb`

. Add this code before the `return`

statement.

```
context.extraOutputs.set(sendToCosmosDb, {
// create a random ID
id:
new Date().toISOString() + Math.random().toString().substring(2, 10),
name: name,
});
```


At this point, your function should look as follows:

```
const { app, output } = require('@azure/functions');
const sendToCosmosDb = output.cosmosDB({
databaseName: 'my-database',
containerName: 'my-container',
createIfNotExists: false,
connection: 'CosmosDBConnectionString',
});
app.http('HttpExampleToCosmosDB', {
methods: ['GET', 'POST'],
extraOutputs: [sendToCosmosDb],
handler: async (request, context) => {
try {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text());
if (!name) {
return { status: 404, body: 'Missing required data' };
}
// Output to Database
context.extraOutputs.set(sendToCosmosDb, {
// create a random ID
id:
new Date().toISOString() + Math.random().toString().substring(2, 10),
name: name,
});
const responseMessage = name
? 'Hello, ' +
name +
'. This HTTP triggered function executed successfully.'
: 'This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response.';
// Return to HTTP client
return { body: responseMessage };
} catch (error) {
context.log(`Error: ${error}`);
return { status: 500, body: 'Internal Server Error' };
}
},
});
```


This code now returns a `MultiResponse`

object that contains both a document and an HTTP response.

Update *HttpExample\function_app.py* to match the following code. Add the `outputDocument`

parameter to the function definition and `outputDocument.set()`

under the `if name:`

statement:

```
import azure.functions as func
import logging
app = func.FunctionApp()
@app.function_name(name="HttpTrigger1")
@app.route(route="hello", auth_level=func.AuthLevel.FUNCTION)
@app.queue_output(arg_name="msg", queue_name="outqueue", connection="AzureWebJobsStorage")
@app.cosmos_db_output(arg_name="outputDocument", database_name="my-database", container_name="my-container", connection="CosmosDbConnectionString")
def test_function(req: func.HttpRequest, msg: func.Out[func.QueueMessage],
outputDocument: func.Out[func.Document]) -> func.HttpResponse:
logging.info('Python HTTP trigger function processed a request.')
logging.info('Python Cosmos DB trigger function processed a request.')
name = req.params.get('name')
if not name:
try:
req_body = req.get_json()
except ValueError:
pass
else:
name = req_body.get('name')
if name:
outputDocument.set(func.Document.from_dict({"id": name}))
msg.set(name)
return func.HttpResponse(f"Hello {name}!")
else:
return func.HttpResponse(
"Please pass a name on the query string or in the request body",
status_code=400
)
```


The document `{"id": "name"}`

is created in the database collection specified in the binding.

## Run the function locally

Visual Studio Code integrates with [Azure Functions Core tools](functions-run-local) to let you run this project on your local development computer before you publish to Azure. If you don't already have Core Tools installed locally, you are prompted to install it the first time you run your project.

To call your function, press

`F5`to start the function app project. The**Terminal**panel displays the output from Core Tools. Your app starts in the**Terminal**panel. You can see the URL endpoint of your HTTP-triggered function running locally.If you don't already have Core Tools installed, select

**Install**to install Core Tools when prompted to do so.

If you have trouble running on Windows, make sure that the default terminal for Visual Studio Code isn't set to**WSL Bash**.With the Core Tools running, go to the

**Azure: Functions**area. Under**Functions**, expand**Local Project**>**Functions**. Right-click (Windows) or`Ctrl -`click (macOS) the`HttpExample`

function and choose**Execute Function Now...**.In the

**Enter request body**, press`Enter`to send a request message to your function.When the function executes locally and returns a response, a notification is raised in Visual Studio Code. Information about the function execution is shown in the

**Terminal**panel.Press

`Ctrl + C`to stop Core Tools and disconnect the debugger.

## Run the function locally

As in the previous article, press

`F5`to start the function app project and Core Tools.With Core Tools running, go to the

**Azure: Functions**area. Under**Functions**, expand**Local Project**>**Functions**. Right-click (Ctrl-click on Mac) the`HttpExample`

function and choose**Execute Function Now...**.In

**Enter request body**you see the request message body value of`{ "name": "Azure" }`

. Press Enter to send this request message to your function.After a response is returned, press

`Ctrl + C`to stop Core Tools.

### Verify that a JSON document has been created

On the Azure portal, go back to your Azure Cosmos DB account and select

**Data Explorer**.Expand your database and container, and select

**Items**to list the documents created in your container.Verify that a new JSON document has been created by the output binding.


## Redeploy and verify the updated app

In Visual Studio Code, press F1 to open the command palette. In the command palette, search for and select

`Azure Functions: Deploy to function app...`

.Choose the function app that you created in the first article. Because you're redeploying your project to the same app, select

**Deploy**to dismiss the warning about overwriting files.After deployment completes, you can again use the

**Execute Function Now...**feature to trigger the function in Azure. This command automatically retrieves the function access key and uses it when calling the HTTP trigger endpoint.Again

[check the documents created in your Azure Cosmos DB container](#verify-that-a-json-document-has-been-created)to verify that the output binding again generates a new JSON document.

## Clean up resources

In Azure, *resources* refer to function apps, functions, storage accounts, and so forth. They're grouped into *resource groups*, and you can delete everything in a group by deleting the group.

You created resources to complete these quickstarts. You might be billed for these resources, depending on your [account status](https://azure.microsoft.com/account/) and [service pricing](https://azure.microsoft.com/pricing/). If you don't need the resources anymore, here's how to delete them:

In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azure: Open in portal`

.Choose your function app and press

`Enter`. The function app page opens in the Azure portal.In the

**Overview**tab, select the named link next to**Resource group**.On the

**Resource group**page, review the list of included resources, and verify that they're the ones you want to delete.Select

**Delete resource group**, and follow the instructions.Deletion may take a couple of minutes. When it's done, a notification appears for a few seconds. You can also select the bell icon at the top of the page to view the notification.


## Next steps

You've updated your HTTP triggered function to write JSON documents to an Azure Cosmos DB container. Now you can learn more about developing Functions using Visual Studio Code:

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

A **Flex Consumption Deployment** diagnostic tool is available in the Azure portal. Open your Flex Consumption app, select **Diagnose and solve problems**, and search for `Flex Consumption Deployment`

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

of the[extension bundle](extension-bundles), or a later version.**Regions**: While the Flex Consumption plan is available in many Azure regions, not all regions are currently supported. To learn more, see[View currently supported regions](flex-consumption-how-to#view-currently-supported-regions).**Deployments**: Deployment slots aren't currently supported. For zero downtime deployments with Flex Consumption, see[Site update strategies in Flex Consumption](flex-consumption-site-updates).**Azure Storage as a local share**: Network File System (NFS) file shares aren't available for Flex Consumption. Only Server Message Block (SMB) and Azure Blobs (read-only) are supported.**Scale**: The lowest maximum scale is currently`1`

. The highest currently supported value is`1000`

.**PowerShell Managed dependencies**: Flex Consumption doesn't support[managed dependencies in PowerShell](functions-reference-powershell#managed-dependencies-feature). You must instead[upload modules with app content](functions-reference-powershell#including-modules-in-app-content).**Certificates**: Loading certificates with the WEBSITE_LOAD_CERTIFICATES app setting, managed certificates, app service certificates, and other platform certificate-based features like endToEndEncryptionEnabled are currently not supported.**Timezones**:`WEBSITE_TIME_ZONE`

and`TZ`

app settings aren't currently supported when running on Flex Consumption plan.**Azure Functions Runtime Version and Proxies**: Flex Consumption only supports version 4.x and later of the Azure Functions runtime. Azure Functions proxies was a feature of versions 1.x through 3.x of the Azure Functions runtime and is not available in Flex Consumption.

## Related articles

[Azure Functions hosting options](functions-scale)
[Create and manage function apps in the Flex Consumption plan](flex-consumption-how-to)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-develop-vs -->

# Develop Azure Functions using Visual Studio

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Visual Studio provides a way to develop, test, and deploy C# class library functions to Azure. If this experience is your first with Azure Functions, see [Azure Functions overview](functions-overview).

To get started right away, consider completing the [Functions quickstart for Visual Studio](functions-create-your-first-function-visual-studio).

This article provides detailed information about how to use Visual Studio to develop C# class library functions and publish them to Azure.
There are two models for developing C# class library functions: the [isolated worker model](dotnet-isolated-process-guide) and the [in-process model](functions-dotnet-class-library).

You're reading the isolated worker model version of this article. You can select your preferred model at the top of the article.

You're reading the in-process model version of this article. You can select your preferred model at the top of the article.

Important

[Support for the in-process model ends on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We recommend that you [migrate your apps to the isolated worker model](migrate-dotnet-to-isolated-model).

Unless otherwise noted, procedures and examples shown are for Visual Studio 2022. For more information about Visual Studio 2022 releases, see the [release notes](/en-us/visualstudio/releases/2022/release-notes) or the [preview release notes](/en-us/visualstudio/releases/2022/release-notes-preview).

## Prerequisites

Visual Studio 2022, including the

**Azure development**workload.Other resources that you need, such as an Azure Storage account, are created in your subscription during the publishing process.

-
If you don't have an Azure account, create a

[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

## Create an Azure Functions project

The Azure Functions project template in Visual Studio creates a C# class library project that you can publish to a function app in Azure. You can use a function app to group functions as a logical unit for easier management, deployment, scaling, and sharing of resources.

From the Visual Studio menu, select

**File**>**New**>**Project**.In the

**Create a new project**dialog, enter**functions**in the search box, select the**Azure Functions**template, and then select**Next**.In the

**Configure your new project**dialog, for**Project name**, enter a name for your project, and then select**Next**. The function app name must be valid as a C# namespace, so don't use underscores, hyphens, or any other nonalphanumeric characters.In the

**Additional information**dialog, take the actions listed in the following table:Setting Action Description **Functions worker**Select **.NET 8.0 Isolated (Long Term Support)**.Visual Studio creates a function project that runs in an [isolated worker process](dotnet-isolated-process-guide). The isolated worker process also supports other versions of .NET and .NET Framework that don't offer long term support (LTS). For more information, see[Azure Functions runtime versions overview](functions-versions).**Function**Select **Http trigger**.Visual Studio creates a function triggered by an HTTP request. **Use Azurite for runtime storage account (AzureWebJobsStorage)**Select this checkbox. Because a function app in Azure requires a storage account, one is assigned or created when you publish your project to Azure. An HTTP trigger doesn't use a Storage account connection string. All other trigger types require a valid Storage account connection string. **Authorization level**Select **Anonymous**.When you use this authorization setting, any client can trigger the created function without providing a key. This configuration makes it easy to test your new function. For more information, see [Authorization level](functions-bindings-http-webhook-trigger#http-auth).Setting Action Description **Functions worker**Select **.NET 8.0 In-process (Long Term Support)**.Visual Studio creates a function project that runs in-process with version 4.x of the Functions runtime. For more information, see [Azure Functions runtime versions overview](functions-versions).**Function**Select **Http trigger**.Visual Studio creates a function triggered by an HTTP request. **Use Azurite for runtime storage account (AzureWebJobsStorage)**Select this checkbox. Because a function app in Azure requires a storage account, one is assigned or created when you publish your project to Azure. An HTTP trigger doesn't use a Storage account connection string. All other trigger types require a valid Storage account connection string. **Authorization level**Select **Anonymous**When you use this authorization setting, any client can trigger the created function without providing a key. This configuration makes it easy to test your new function. For more information, see [Authorization level](functions-bindings-http-webhook-trigger#http-auth).Make sure you set the

**Authorization level**to**Anonymous**. If you select the default level of**Function**, you're required to present the[function key](function-keys-how-to)in requests to access your function endpoint.Select

**Create**to create the function project and HTTP trigger function.

After you create a Functions project, the project template creates a C# project, installs the `Microsoft.Azure.Functions.Worker`

and `Microsoft.Azure.Functions.Worker.Sdk`

NuGet packages, and sets the target framework.

After you create a Functions project, the project template creates a C# project, installs the `Microsoft.NET.Sdk.Functions`

NuGet package, and sets the target framework.

The new project has the following files:

*host.json*: This file provides a way for you to configure the Functions host. These settings apply both when running locally and in Azure. For more information, see[host.json reference](functions-host-json).*local.settings.json*: This file maintains settings that you use when you run functions locally. These settings aren't used when your app runs in Azure. For more information, see[Work with app settings locally](#local-settings).Important

Because the

*local.settings.json*file can contain secrets, you must exclude it from your project source control. In the**Properties**dialog for this file, make sure the**Copy to Output Directory**setting is set to**Copy if newer**.

For more information, see [Project structure](dotnet-isolated-process-guide#project-structure) in the isolated worker guide.

For more information, see [Functions class library project](functions-dotnet-class-library#functions-class-library-project).

## Work with app settings locally

When your function app runs in Azure, settings required by your functions are [stored encrypted in app settings](functions-how-to-use-azure-function-app-settings#settings). During local development, these settings are instead added to the `Values`

collection in the *local.settings.json* file. The *local.settings.json* file also stores settings used by local development tools.

Items in the `Values`

collection in your project's *local.settings.json* file are intended to mirror items in your function app's [application settings](functions-how-to-use-azure-function-app-settings#settings) in Azure.

Visual Studio doesn't automatically upload the settings in *local.settings.json* when you publish the project. To make sure that these settings also exist in your function app in Azure, upload them after you publish your project. For more information, see [Function app settings](#function-app-settings). The values in a `ConnectionStrings`

collection aren't published.

Your code can also read the function app settings values as environment variables. For more information, see [Environment variables](functions-dotnet-class-library#environment-variables).

## Configure the project for local development

The Functions runtime uses a Storage account internally. During development, you can use a valid Storage account for this internal account, or you can use the [Azurite emulator](../storage/common/storage-use-azurite).

For all trigger types other than HTTP and webhooks, you need to set the value of the `Values.AzureWebJobsStorage`

key in the *local.settings.json* file:

- For a Storage account, set the value to the connection string of your storage account.
- For the emulator, set the value to
`UseDevelopmentStorage=true`

.

If you use the emulator, change this setting to an actual storage account connection string before deployment. For more information, see [Local storage emulator](functions-develop-local#local-storage-emulator).

To set the storage account connection string, take the following steps:

Sign in to the

[Azure portal](https://portal.azure.com), and then go to your storage account.Select

**Security + networking**>**Access keys**. Under**key1**, copy the**Connection string**value.In your Visual Studio project, open the

*local.settings.json*file. Set the value of the`AzureWebJobsStorage`

key to the connection string you copied.Repeat the previous step to add unique keys to the

`Values`

array for any other connections required by your functions.

## Add a function to your project

In C# class library functions, the bindings that the functions use are defined by applying attributes in the code. When you create your function triggers from the provided templates, the trigger attributes are applied for you.

In

**Solution Explorer**, right-click your project node and select**Add**>**New Azure Function**.In the

**Add New Item**dialog, select**Azure Function**, and then select**Add**.Select a trigger, and then set the required binding properties. If you select a Storage service trigger and you want to configure the connection, select the checkbox for configuring the trigger connection. The following example shows the settings for creating a Queue Storage trigger function.

Select

**Add**. If you select the checkbox for configuring a storage connection in the previous step, the**Connect to dependency**page appears. Select an Azurite storage emulator or**Azure Storage**, and then select**Next**.- If you select an Azurite storage emulator, the
**Connect to Storage Azurite emulator**page appears. Take the following steps:- Select
**Next**. - On the
**Summary of changes**page, select**Finish**. Visual Studio configures the dependency and creates the trigger class.

- Select
- If you select
**Azure Storage**, the**Connect to Azure Storage**page appears. Take the following steps:- Select a storage account, and then select
**Next**. Visual Studio tries to connect to your Azure account and retrieve an endpoint. - Select
**Next**. - On the
**Summary of changes**page, select**Finish**. Visual Studio configures the dependency and creates the trigger class.

- Select a storage account, and then select

This trigger example uses an application setting for the storage connection with a key named

`QueueStorage`

. This key, stored in the[local.settings.json file](functions-develop-local#local-settings-file), either references the Azurite emulator or a Storage account.- If you select an Azurite storage emulator, the
Examine the newly added class. For example, the following C# class represents a basic Queue Storage trigger function:

A

`Run()`

method is attributed with`Function`

. This attribute indicates that the method is the entry point for the function.`using System; using Azure.Storage.Queues.Models; using Microsoft.Azure.Functions.Worker; using Microsoft.Extensions.Logging; namespace Company.Function; public class QueueTriggerCSharp { private readonly ILogger<QueueTriggerCSharp> _logger; public QueueTriggerCSharp(ILogger<QueueTriggerCSharp> logger) { _logger = logger; } [Function(nameof(QueueTriggerCSharp))] public void Run([QueueTrigger("PathValue", Connection = "ConnectionValue")] QueueMessage message) { _logger.LogInformation("C# Queue trigger function processed: {messageText}", message.MessageText); } }`

A static

`Run()`

method is attributed with`FunctionName`

. This attribute indicates that the method is the entry point for the function.`using System; using Microsoft.Azure.WebJobs; using Microsoft.Azure.WebJobs.Host; using Microsoft.Extensions.Logging; namespace Company.Function { public class QueueTriggerCSharp { [FunctionName("QueueTriggerCSharp")] public void Run([QueueTrigger("PathValue", Connection = "ConnectionValue")]string myQueueItem, ILogger log) { log.LogInformation($"C# Queue trigger function processed: {myQueueItem}"); } } }`


A binding-specific attribute is applied to each binding parameter supplied to the entry point method. The attribute takes the binding information as parameters.

In the preceding code, the first parameter has a `QueueTrigger`

attribute applied, which indicates a Queue Storage trigger function. The queue name and connection string setting name are passed as parameters to the `QueueTrigger`

attribute. In your class:

- The queue name parameter should match the name of the queue you use in an earlier step to create the trigger, such as
`myqueue-items`

. - The connection string setting name should match the one you use in an earlier step to create the trigger, such as
`QueueStorage`

.

For more information, see [Azure Queue storage trigger for Azure Functions](functions-bindings-storage-queue-trigger).

Use the preceding procedure to add more functions to your function app project. Each function in the project can have a different trigger, but a function must have exactly one trigger. For more information, see [Azure Functions triggers and bindings](functions-triggers-bindings).

## Add bindings

As with triggers, input and output bindings are added to your function as binding attributes. To add bindings to a function, take the following steps:

Make sure you

[configure the project for local development](#configure-the-project-for-local-development).Add the appropriate NuGet extension package for each specific binding. For binding-specific NuGet package requirements, see the reference article for the binding. For example, for package requirements for the Azure Event Hubs trigger, see

[Azure Event Hubs trigger and bindings for Azure Functions](functions-bindings-event-hubs).Use the following command in the Package Manager Console to install a specific package:

`Install-Package Microsoft.Azure.Functions.Worker.Extensions.<BINDING_TYPE> -Version <TARGET_VERSION>`

`Install-Package Microsoft.Azure.WebJobs.Extensions.<BINDING_TYPE> -Version <TARGET_VERSION>`

In this code, replace

`<BINDING_TYPE>`

with the specific name of the binding extension, and replace`<TARGET_VERSION>`

with a specific version of the package, such as`4.0.0`

. Valid versions are listed on the individual package pages at[NuGet.org](https://nuget.org).If there are app settings that the binding needs, add them to the

`Values`

collection in the[local setting file](functions-develop-local#local-settings-file).The function uses these values when it runs locally. When the function runs in the function app in Azure, it uses the

[function app settings](#function-app-settings). Visual Studio makes it easy to[publish local settings to Azure](#function-app-settings).Add the appropriate binding attribute to the method signature. In the following code, a queue message triggers the

`Run`

function. The output binding then creates a new queue message with the same text in a different queue.`public class QueueTrigger { private readonly ILogger _logger; public QueueTrigger(ILoggerFactory loggerFactory) { _logger = loggerFactory.CreateLogger<QueueTrigger>(); } [Function("CopyQueueMessage")] [QueueOutput("myqueue-items-destination", Connection = "QueueStorage")] public string Run([QueueTrigger("myqueue-items-source", Connection = "QueueStorage")] string myQueueItem) { _logger.LogInformation($"C# Queue trigger function processed: {myQueueItem}"); return myQueueItem; } }`

The

`QueueOutput`

attribute defines the binding on the method. For multiple output bindings, you instead place this attribute on a string property of the returned object. For more information, see[Multiple output bindings](dotnet-isolated-process-guide#multiple-output-bindings).`public static class SimpleExampleWithOutput { [FunctionName("CopyQueueMessage")] public static void Run( [QueueTrigger("myqueue-items-source", Connection = "QueueStorage")] string myQueueItem, [Queue("myqueue-items-destination", Connection = "QueueStorage")] out string myQueueItemCopy, ILogger log) { log.LogInformation($"CopyQueueMessage function processed: {myQueueItem}"); myQueueItemCopy = myQueueItem; } }`

The

`Queue`

attribute on the`out`

parameter defines the output binding.The connection to Queue Storage is obtained from the

`QueueStorage`

setting. For more information, see the reference article for the specific binding.

For a full list of the bindings supported by Functions, see [Supported bindings](functions-triggers-bindings?tabs=csharp#supported-bindings). For a more complete example of this scenario, see [Connect functions to Azure Storage using Visual Studio](functions-add-output-binding-storage-queue-vs).

## Run functions locally

You can use Azure Functions Core Tools to run Functions projects on your local development computer. When you select **F5** to debug a Functions project, the local Functions host (`func.exe`

) starts to listen on a local port (usually 7071). Any callable function endpoints are written to the output, and you can use these endpoints for testing your functions. For more information, see [Develop Azure Functions locally using Core Tools](functions-run-local). You're prompted to install these tools the first time you start a function from Visual Studio.

Important

Starting with version 4.0.6517 of the Core Tools, in-process model projects must reference [version 4.5.0 or later of Microsoft.NET.Sdk.Functions](https://www.nuget.org/packages/Microsoft.NET.Sdk.Functions/4.5.0). If you use an earlier version, the

`func start`

command generates an error.To start your function in Visual Studio in debug mode, take the following steps:

Select

**F5**. If prompted, accept the request from Visual Studio to download and install Azure Functions Core Tools. You might also need to turn on a firewall exception so that the tools can handle HTTP requests.When the project runs, test your code the same way you test a deployed function.

When you run Visual Studio in debug mode, breakpoints are hit as expected.


For a more detailed testing scenario that uses Visual Studio, see [Test functions](#test-functions), later in this article.

## Publish to Azure

When you publish your Functions project to Azure, Visual Studio uses [zip deployment](functions-deployment-technologies#zip-deploy) to deploy the project files. When possible, you should also select **Run from package file** so that the project runs in the deployment (.zip) package. For more information, see [Run your functions from a package file in Azure](run-functions-from-deployment-package).

Don't deploy to Functions by using Web Deploy (`msdeploy`

).

Use the following steps to publish your project to a function app in Azure:

In

**Solution Explorer**, right-click the project and then select**Publish**.On the

**Publish**page, make the following selections:- On
**Target**, select**Azure**, and then select**Next**. - On
**Specific target**, select**Azure Function App**, and then select**Next**. - On
**Functions instance**, select**Create new**.

- On
Create a new instance by using the values specified in the following table:

Setting Value Description **Name**A globally unique name The name must uniquely identify your new function app. Accept the suggested name or enter a new name. The following characters are valid: `a-z`

,`0-9`

, and`-`

.**Subscription name**The name of your subscription The function app is created in an Azure subscription. Accept the default subscription or select a different one from the list. [Resource group](../azure-resource-manager/management/overview)The name of your resource group The function app is created in a resource group. Select **New**to create a new resource group. You can also select an existing resource group from the list.[Plan Type](functions-scale)**Flex Consumption**When you publish your project to a function app that runs in a [Flex Consumption plan](flex-consumption-plan), you might pay only for executions of your functions app. Other hosting plans can incur higher costs.**IMPORTANT:**

When creating a Flex Consumption plan, you must first select**App service plan**and then reselect**Flex Consumption**to clear an issue with the dialog.**Operating system****Linux**The Flex Consumption plan currently requires Linux. **Location**The location of the app service Select a location in an [Azure region supported by the Flex Consumption plan](flex-consumption-how-to#view-currently-supported-regions). When an unsupported region is selected, the**Create**button is grayed-out.**Instance memory size****2048**The [memory size of the virtual machine instances](flex-consumption-plan#instance-sizes)in which the app runs is unique to the Flex Consumption plan.[Azure Storage](storage-considerations)A general-purpose storage account The Functions runtime requires a Storage account. Select **New**to configure a general-purpose storage account. You can also use an existing account that meets the[storage account requirements](storage-considerations#storage-account-requirements).[Application Insights](functions-monitoring)An Application Insights instance You should turn on Application Insights integration for your function app. Select **New**to create a new instance, either in a new or in an existing Log Analytics workspace. You can also use an existing instance.Select

**Create**to create a function app and its related resources in Azure. The status of resource creation is shown in the lower-left corner of the window.Select

**Finish**. The**Publish profile creation progress**window appears. When the profile is created, select**Close**.On the publish profile page, select

**Publish**to deploy the package that contains your project files to your new function app in Azure.When deployment is complete, the root URL of the function app in Azure is shown on the publish profile page.

On the publish profile page, go to the

**Hosting**section. Select the ellipsis (**...**), and then select**Open in Azure portal**. The new function app Azure resource opens in the Azure portal.

## Function app settings

Visual Studio doesn't upload app settings automatically when you publish your project. If you add settings to the *local.settings.json* file, you must also add them to the function app in Azure.

The easiest way to upload the required settings to your function app in Azure is to manage them in Visual Studio. On the publish profile page, go to the **Hosting** section. Select the ellipsis (**...**), and then select **Manage Azure App Service settings**.

When you make the selection, the **Application settings** dialog opens for the function app. You can use this dialog to add application settings or modify existing ones.


For each setting, the **Local** value is the value in the *local.settings.json* file, and the **Remote** value is the value in the function app in Azure.

- To create an app setting, select
**Add setting**. - To copy a setting value from the
**Local**field to the**Remote**field, select**Insert value from Local**.

Pending changes are written to the local settings file and the function app when you select **OK**.

Note

By default, the *local.settings.json* file isn't checked into source control. As a result, if you clone a local Functions project from source control, the project doesn't have a *local.settings.json* file. You need to manually create the *local.settings.json* file in the project root so that the **Application settings** dialog works as expected.

You can also manage application settings in one of these other ways:

- Use the
[Azure portal](functions-how-to-use-azure-function-app-settings#settings). - Use the
.`--publish-local-settings`

publish option in the Azure Functions Core Tools - Use the
[Azure CLI](/en-us/cli/azure/functionapp/config/appsettings#az-functionapp-config-appsettings-set).

## Remote debugging

To debug your function app remotely, you must publish a debug configuration of your project. You also need to turn on remote debugging in your function app in Azure.

This section assumes a debug configuration to your function app is published.

### Remote debugging considerations

- Remote debugging isn't recommended on a production service.
- To use remote debugging, you must host your function app in a Premium or App Service plan.
- Remote debugging is currently only supported when running your C# app on Windows.
- If you have the Just My Code feature turned on in Visual Studio, turn it off. For instructions, see
[Enable or disable Just My Code](/en-us/visualstudio/debugger/just-my-code#BKMK_Enable_or_disable_Just_My_Code). - Avoid long stops at breakpoints when you use remote debugging. When a process is stopped for longer than a few minutes, Azure treats it as an unresponsive process and shuts it down.
- While you're debugging, the server sends data to Visual Studio, which can affect bandwidth charges. For information about bandwidth rates, see
[Pricing calculator](https://azure.microsoft.com/pricing/calculator/). - Remote debugging is automatically turned off in your function app after 48 hours. After that point, you need to turn remote debugging back on.

### Attach the debugger

When you debug an isolated worker process app, you currently need to attach the remote debugger to a separate .NET process. Several other configuration steps are also required.

To attach a remote debugger to a function app running in a process separate from the Functions host, take the following steps:

On the publish profile page, go to the

**Hosting**section. Select the ellipsis (**...**), and then select**Attach debugger**.Visual Studio connects to your function app and turns on remote debugging if it's not already turned on.

Note

Because the remote debugger can't connect to the host process, an error message might appear. In any case, the local debugger can't access your breakpoints or provide a way for you to inspect variables or step through code.

On the Visual Studio

**Debug**menu, select**Attach to Process**.In the

**Attach to Process**dialog, take the following steps:- Next to
**Connection type**, select**Microsoft Azure App Services**. - Next to
**Connection target**, select**Find**.

- Next to
In the

**Azure Attach to Process**dialog, search for and select your function app, and then select**OK**.If prompted, allow Visual Studio access through your local firewall.

Back in the

**Attach to Process**dialog, select**Show processes for all users**. Select**dotnet.exe**, and then select**Attach**.

When the operation finishes, you're attached to your C# class library code running in an isolated worker process. At this point, you can debug your function app as normal.

To attach a remote debugger to a function app running in-process with the Functions host, take the following steps.

On the publish profile page, go to the **Hosting** section. Select the ellipsis (**...**), and then select **Attach debugger**.

Visual Studio connects to your function app and turns on remote debugging if it's not already turned on. It also locates and attaches the debugger to the host process for the app. At this point, you can debug your function app as normal.

When you finish debugging, you should [turn off remote debugging](#turn-off-remote-debugging).

### Turn off remote debugging

After you finish remote debugging your code, you should turn off remote debugging in the [Azure portal](https://portal.azure.com). Remote debugging is automatically turned off after 48 hours, in case you forget.

On the publish profile page, go to the

**Hosting**section. Select the ellipsis (**...**), and then select**Open in Azure portal**. The Azure portal opens to the function app your project is deployed to.In the function app, select

**Settings**>**Configuration**, and then go to the**General settings**tab. Next to**Remote debugging**, select**Off**. Select**Save**, and then select**Continue**.

After the function app restarts, you can no longer remotely connect to your remote processes. You can use this same tab in the Azure portal to turn on remote debugging outside of Visual Studio.

## Monitor functions

The recommended way to monitor your functions is by integrating your function app with Application Insights. You should turn on this integration when you create your function app during Visual Studio publishing.

If the integration isn't set up during publishing for some reason, you should still turn on [Application Insights integration](configure-monitoring#enable-application-insights-integration) for your function app in Azure.

For more information about using Application Insights for monitoring, see [Monitor executions in Azure Functions](functions-monitoring).

## Test functions

This section describes how to create a C# in-process model project that you can test by using [xUnit](https://github.com/xunit/xunit), an open-source unit testing tool for .NET.

### Step 1: Setup

Follow these steps to configure the environment, including the app project and functions, required to support your tests:

In Visual Studio, create an Azure Functions project named

**Functions**.Create an HTTP function from the template:

- In
**Solution Explorer**, right-click the**Functions**project, and then select**Add**>**New Azure Function**. - In the
**Add New Item**dialog, select**Azure Function**, and then select**Add**. - Select
**Http trigger**, and then select**Add**. - Rename the new class
*MyHttpTrigger*.

- In
Create a timer function from the template:

- In
**Solution Explorer**, right-click the**Functions**project, and then select**Add**>**New Azure Function**. - In the
**Add New Item**dialog, select**Azure Function**, and then select**Add**. - Select
**Timer trigger**, and then select**Add**. - Rename the new class
*MyTimerTrigger*.

- In
Create an

[xUnit Test app](https://xunit.net/docs/getting-started/v3/getting-started)in the solution:- In
**Solution Explorer**, right-click the solution that contains your**Functions**project, and then select**Add**>**New Project**. - Select the
**xUnit Test Project**template, and then select**Next**. - Name the project
**Functions.Tests**.

- In
Remove the default test files from the

**Functions.Tests**project.Use NuGet to add a reference from the test app to

[Microsoft.AspNetCore.Mvc](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc/). You can use Package Manager Console, or you can take the following steps:- In
**Solution Explorer**, right-click the**Functions.Tests**project, and then select**Manage NuGet Packages**. - Search for and install
**Microsoft.AspNetCore.Mvc**.

- In
In the

**Functions.Tests**app,[add a reference](/en-us/visualstudio/ide/managing-references-in-a-project)to the**Functions**app:- In
**Solution Explorer**, right-click the**Functions.Tests**project, and then select**Add**>**Project Reference**. - Select the
**Functions**project, and then select**OK**.

- In

### Step 2: Create test classes

In this section, you create the classes that you use to run the automated tests.

Each function takes an implementation of [ ILogger](/en-us/dotnet/api/microsoft.extensions.logging.ilogger) to handle message logging. In some tests, no messages are logged, or it doesn't matter how logging is implemented. Other tests need to evaluate logged messages to determine whether a test should pass.

Create a class in your

**Functions.Tests**project named`NullScope`

and add the following code. This class provides a mock scope. In a later step, you create an implementation of`ILogger`

that uses this scope.`using System; namespace Functions.Tests { public class NullScope : IDisposable { public static NullScope Instance { get; } = new NullScope(); private NullScope() { } public void Dispose() { } } }`

Create a class in your

**Functions.Tests**project named`ListLogger`

and add the following code. This class maintains an internal list of messages to evaluate during testing. To implement the required`ILogger`

interface, the class uses the mock scope from the`NullScope`

class. The test cases pass the mock scope to the`ListLogger`

class.`using Microsoft.Extensions.Logging; using System; using System.Collections.Generic; using System.Text; namespace Functions.Tests { public class ListLogger : ILogger { public IList<string> Logs; public IDisposable BeginScope<TState>(TState state) => NullScope.Instance; public bool IsEnabled(LogLevel logLevel) => false; public ListLogger() { this.Logs = new List<string>(); } public void Log<TState>(LogLevel logLevel, EventId eventId, TState state, Exception exception, Func<TState, Exception, string> formatter) { string message = formatter(state, exception); this.Logs.Add(message); } } }`

The

`ListLogger`

class implements the following members, as contracted by the`ILogger`

interface:`BeginScope`

: Scopes add context to your logging. In this case, the test points to the static instance on the`NullScope`

class to allow the test to function.`IsEnabled`

: A default value of`false`

is provided.`Log`

: This method uses the provided`formatter`

function to format the message. The method then adds the resulting text to the`Logs`

collection.

The

`Logs`

collection is an instance of`List<string>`

and is initialized in the constructor.Create a code file in the

**Functions.Tests**project named*LoggerTypes.cs*and add the following code:`namespace Functions.Tests { public enum LoggerTypes { Null, List } }`

This enumeration specifies the type of logger that the tests use.

Create a class in the

**Functions.Tests**project named`TestFactory`

and add the following code:`using Microsoft.AspNetCore.Http; using Microsoft.AspNetCore.Http.Internal; using Microsoft.Extensions.Logging; using Microsoft.Extensions.Logging.Abstractions; using Microsoft.Extensions.Primitives; using System.Collections.Generic; namespace Functions.Tests { public class TestFactory { public static IEnumerable<object[]> Data() { return new List<object[]> { new object[] { "name", "Bernardo" }, new object[] { "name", "Ananya" }, new object[] { "name", "Vlad" } }; } private static Dictionary<string, StringValues> CreateDictionary(string key, string value) { var qs = new Dictionary<string, StringValues> { { key, value } }; return qs; } public static HttpRequest CreateHttpRequest(string queryStringKey, string queryStringValue) { var context = new DefaultHttpContext(); var request = context.Request; request.Query = new QueryCollection(CreateDictionary(queryStringKey, queryStringValue)); return request; } public static ILogger CreateLogger(LoggerTypes type = LoggerTypes.Null) { ILogger logger; if (type == LoggerTypes.List) { logger = new ListLogger(); } else { logger = NullLoggerFactory.Instance.CreateLogger("Null Logger"); } return logger; } } }`

The

`TestFactory`

class implements the following members:`Data`

: This property returns an[IEnumerable](/en-us/dotnet/api/system.collections.ienumerable)collection of sample data. The key-value pairs represent values that are passed into a query string.`CreateDictionary`

: This method accepts a key-value pair as an argument. It returns a new instance of`Dictionary`

that's used to create an instance of`QueryCollection`

to represent query string values.`CreateHttpRequest`

: This method creates an HTTP request that's initialized with the given query string parameters.`CreateLogger`

: This method returns an implementation of`ILogger`

that's used for testing. The`ILogger`

implementation depends on the specified logger type. If a list type is specified, the`ListLogger`

instance keeps track of logged messages that are available for evaluation in tests.

Create a class in the

**Functions.Tests**project named`FunctionsTests`

and add the following code:`using Microsoft.AspNetCore.Mvc; using Microsoft.Extensions.Logging; using Xunit; namespace Functions.Tests { public class FunctionsTests { private readonly ILogger logger = TestFactory.CreateLogger(); [Fact] public async void Http_trigger_should_return_known_string() { var request = TestFactory.CreateHttpRequest("name", "Bernardo"); var response = (OkObjectResult)await MyHttpTrigger.Run(request, logger); Assert.Equal("Hello, Bernardo. This HTTP triggered function executed successfully.", response.Value); } [Theory] [MemberData(nameof(TestFactory.Data), MemberType = typeof(TestFactory))] public async void Http_trigger_should_return_known_string_from_member_data(string queryStringKey, string queryStringValue) { var request = TestFactory.CreateHttpRequest(queryStringKey, queryStringValue); var response = (OkObjectResult)await MyHttpTrigger.Run(request, logger); Assert.Equal($"Hello, {queryStringValue}. This HTTP triggered function executed successfully.", response.Value); } [Fact] public void Timer_should_log_message() { var logger = (ListLogger)TestFactory.CreateLogger(LoggerTypes.List); new MyTimerTrigger().Run(null, logger); var msg = logger.Logs[0]; Assert.Contains("C# Timer trigger function executed at", msg); } } }`

This class implements the following members:

`Http_trigger_should_return_known_string`

: This test uses the query string value`name=Bernardo`

to create a request to an HTTP function. This test checks that the expected response is returned.`Http_trigger_should_return_string_from_member_data`

: This test uses xUnit attributes to provide sample data to the HTTP function.`Timer_should_log_message`

: This test creates an instance of`ListLogger`

and passes it to a timer function. After the function runs, the log is checked to make sure the expected message is present.

To access application settings in your tests, you can

[inject](functions-dotnet-dependency-injection)an`IConfiguration`

implementation with mocked environment variable values into your function.

### Step 3: Run tests

To run the tests in Visual Studio, select **View** > **Test Explorer**. In **Test Explorer**, select **Run** > **Run All Tests in View**.


### Step 4: Debug tests

To debug the tests, set a breakpoint on a test. In **Test Explorer**, select **Run** > **Debug Last Run**.
