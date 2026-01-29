---
merged_at: 2026-01-29T15:49:53.276136
merged_files: 2
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-reference-csharp -->

# Azure Functions legacy C# script (.csx) developer reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article is an introduction to developing Azure Functions by using C# script (*.csx*).

Important

C# script apps run in the host process and are supported primarily to provide a convenient in-portal experience to help you quickly get started creating and running C# functions. For production-quality apps, you should instead develop your C# functions locally as a [compiled C# class library project that uses the isolated process model](dotnet-isolated-process-guide). To learn how to migrate a C# script project to a C# class library (isolated worker) project, see [Convert a C# script app to a C# project](#convert-a-c-script-app-to-a-c-project).

Azure Functions lets you develop functions using C# in one of the following ways:

| Type | Execution process | Code extension | Development environment | Reference |
|---|---|---|---|---|
| C# script | in-process | .csx |
|

[This article](#create-a-c-script-app)[Visual Studio](functions-develop-vs)[Visual Studio Code](functions-develop-vs-code)[Core Tools](functions-run-local)[.NET isolated worker process functions](dotnet-isolated-process-guide)[Visual Studio](functions-develop-vs)[Visual Studio Code](functions-develop-vs-code)[Core Tools](functions-run-local)[In-process C# class library functions](functions-dotnet-class-library)Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

## How .csx works

Data flows into your C# function via method arguments. Argument names are specified in a `function.json`

file, and there are predefined names for accessing things like the function logger and cancellation tokens.

The *.csx* format allows you to write less "boilerplate" and focus on writing just a C# function. Instead of wrapping everything in a namespace and class, just define a `Run`

method. Include any assembly references and namespaces at the beginning of the file as usual.

A function app's *.csx* files are compiled when an instance is initialized. This compilation step means things like cold start may take longer for C# script functions compared to C# class libraries. This compilation step is also why C# script functions are editable in the Azure portal, while C# class libraries aren't.

C# script code always runs in the same process as the Functions host.

## Folder structure

The folder structure for a C# script project looks like the following example:

```
FunctionsProject
| - MyFirstFunction
| | - run.csx
| | - function.json
| | - function.proj
| - MySecondFunction
| | - run.csx
| | - function.json
| | - function.proj
| - host.json
| - extensions.csproj
| - bin
```


There's a shared [host.json](functions-host-json) file that can be used to configure the function app. Each function has its own code file (.csx) and binding configuration file (function.json).

The binding extensions required in [version 2.x and later versions](functions-versions) of the Functions runtime are defined in the `extensions.csproj`

file, with the actual library files in the `bin`

folder. When developing locally, you must [register binding extensions](extension-bundles). When you develop functions in the Azure portal, this registration is done for you.

## Create a C# script app

There are currently two ways to create a C# script app:

Create a C# script project by passing the `--csx`

option when running the [ func init](functions-core-tools-reference#func-init) command. You must also set

`--worker-runtime`

to `dotnet`

, as in this example:```
func init --worker-runtime dotnet --csx
```


When working with a C# script app, you must supply the `--csx`

option for other Core Tools where it's supported.

When deploying your C# script project to a function app in Azure, you can only deploy it to an app that uses the [in-process model for C#](functions-dotnet-class-library).

Keep these considerations in mind before creating a C# script app:

- C# script is supported primarily to provide a convenient in-portal experience to help you quickly get started creating and running C# functions. For production-quality apps, you should instead develop your C# functions locally as a
[compiled C# class library project](dotnet-isolated-process-guide). - C# script is only supported when running
[in-process with the Functions host](functions-dotnet-class-library), which is a[legacy execution mode for C#](https://aka.ms/azure-functions-retirements/in-process-model). - You can't host C# script apps in the
[Flex Consumption plan](flex-consumption-plan), which is the recommended plan for dynamic scale apps. This is because the Flex Consumption plan only supports C# apps that use the[isolated worker model](dotnet-isolated-process-guide).

## Binding to arguments

Input or output data is bound to a C# script function parameter via the `name`

property in the *function.json* configuration file. The following example shows a *function.json* file and *run.csx* file for a queue-triggered function. The parameter that receives data from the queue message is named `myQueueItem`

because that's the value of the `name`

property.

```
{
"disabled": false,
"bindings": [
{
"type": "queueTrigger",
"direction": "in",
"name": "myQueueItem",
"queueName": "myqueue-items",
"connection":"MyStorageConnectionAppSetting"
}
]
}
```


```
#r "Microsoft.WindowsAzure.Storage"
using Microsoft.Extensions.Logging;
using Microsoft.WindowsAzure.Storage.Queue;
using System;
public static void Run(CloudQueueMessage myQueueItem, ILogger log)
{
log.LogInformation($"C# Queue trigger function processed: {myQueueItem.AsString}");
}
```


The `#r`

statement is explained [later in this article](#referencing-external-assemblies).

## Connections

When possible, use managed identity-based connections in your triggers and bindings. For more information, see the [Function developer guide](functions-reference#connections).

## Supported types for bindings

Each binding has its own supported types; for instance, a blob trigger can be used with a string parameter, a POCO parameter, a `CloudBlockBlob`

parameter, or any of several other supported types. The [binding reference article for blob bindings](functions-bindings-storage-blob-trigger#usage) lists all supported parameter types for blob triggers. For more information, see [Triggers and bindings](functions-triggers-bindings) and the [binding reference docs for each binding type](functions-triggers-bindings#related-content).

Tip

If you plan to use the HTTP or WebHook bindings, plan to avoid port exhaustion that can be caused by improper instantiation of `HttpClient`

. For more information, see [How to manage connections in Azure Functions](manage-connections).

## Referencing custom classes

If you need to use a custom Plain Old CLR Object (POCO) class, you can include the class definition inside the same file or put it in a separate file.

The following example shows a *run.csx* example that includes a POCO class definition.

```
public static void Run(string myBlob, out MyClass myQueueItem)
{
log.Verbose($"C# Blob trigger function processed: {myBlob}");
myQueueItem = new MyClass() { Id = "myid" };
}
public class MyClass
{
public string Id { get; set; }
}
```


A POCO class must have a getter and setter defined for each property.

## Reusing .csx code

You can use classes and methods defined in other *.csx* files in your *run.csx* file. To do that, use `#load`

directives in your *run.csx* file. In the following example, a logging routine named `MyLogger`

is shared in *myLogger.csx* and loaded into *run.csx* using the `#load`

directive:

Example *run.csx*:

```
#load "mylogger.csx"
using Microsoft.Extensions.Logging;
public static void Run(TimerInfo myTimer, ILogger log)
{
log.LogInformation($"Log by run.csx: {DateTime.Now}");
MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```


Example *mylogger.csx*:

```
public static void MyLogger(ILogger log, string logtext)
{
log.LogInformation(logtext);
}
```


Using a shared *.csx* file is a common pattern when you want to strongly type the data passed between functions by using a POCO object. In the following simplified example, an HTTP trigger and queue trigger share a POCO object named `Order`

to strongly type the order data:

Example *run.csx* for HTTP trigger:

```
#load "..\shared\order.csx"
using System.Net;
using Microsoft.Extensions.Logging;
public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, ILogger log)
{
log.LogInformation("C# HTTP trigger function received an order.");
log.LogInformation(req.ToString());
log.LogInformation("Submitting to processing queue.");
if (req.orderId == null)
{
return new HttpResponseMessage(HttpStatusCode.BadRequest);
}
else
{
await outputQueueItem.AddAsync(req);
return new HttpResponseMessage(HttpStatusCode.OK);
}
}
```


Example *run.csx* for queue trigger:

```
#load "..\shared\order.csx"
using System;
using Microsoft.Extensions.Logging;
public static void Run(Order myQueueItem, out Order outputQueueItem, ILogger log)
{
log.LogInformation($"C# Queue trigger function processed order...");
log.LogInformation(myQueueItem.ToString());
outputQueueItem = myQueueItem;
}
```


Example *order.csx*:

```
public class Order
{
public string orderId {get; set; }
public string custName {get; set;}
public string custAddress {get; set;}
public string custEmail {get; set;}
public string cartId {get; set; }
public override String ToString()
{
return "\n{\n\torderId : " + orderId +
"\n\tcustName : " + custName +
"\n\tcustAddress : " + custAddress +
"\n\tcustEmail : " + custEmail +
"\n\tcartId : " + cartId + "\n}";
}
}
```


You can use a relative path with the `#load`

directive:

`#load "mylogger.csx"`

loads a file located in the function folder.`#load "loadedfiles\mylogger.csx"`

loads a file located in a folder in the function folder.`#load "..\shared\mylogger.csx"`

loads a file located in a folder at the same level as the function folder, that is, directly under*wwwroot*.

The `#load`

directive works only with *.csx* files, not with *.cs* files.

## Binding to method return value

You can use a method return value for an output binding, by using the name `$return`

in *function.json*.

```
{
"name": "$return",
"type": "blob",
"direction": "out",
"path": "output-container/{id}"
}
```


Here's the C# script code using the return value, followed by an async example:

```
public static string Run(WorkItem input, ILogger log)
{
string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
log.LogInformation($"C# script processed queue message. Item={json}");
return json;
}
```


```
public static Task<string> Run(WorkItem input, ILogger log)
{
string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
log.LogInformation($"C# script processed queue message. Item={json}");
return Task.FromResult(json);
}
```


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
public static void Run(ICollector<string> myQueue, ILogger log)
{
myQueue.Add("Hello");
myQueue.Add("World!");
}
```


## Logging

To log output to your streaming logs in C#, include an argument of type [ILogger](/en-us/dotnet/api/microsoft.extensions.logging.ilogger). We recommend that you name it `log`

. Avoid using `Console.Write`

in Azure Functions.

```
public static void Run(string myBlob, ILogger log)
{
log.LogInformation($"C# Blob trigger function processed: {myBlob}");
}
```


Note

For information about a newer logging framework that you can use instead of `TraceWriter`

, see the [ILogger](functions-dotnet-class-library#ilogger) documentation in the .NET class library developer guide.

### Custom metrics logging

You can use the `LogMetric`

extension method on `ILogger`

to create custom metrics in Application Insights. Here's a sample method call:

```
logger.LogMetric("TestMetric", 1234);
```


This code is an alternative to calling `TrackMetric`

by using the Application Insights API for .NET.

## Async

To make a function [asynchronous](/en-us/dotnet/csharp/programming-guide/concepts/async/), use the `async`

keyword and return a `Task`

object.

```
public async static Task ProcessQueueMessageAsync(
string blobName,
Stream blobInput,
Stream blobOutput)
{
await blobInput.CopyToAsync(blobOutput, 4096);
}
```


You can't use `out`

parameters in async functions. For output bindings, use the [function return value](#binding-to-method-return-value) or a [collector object](#writing-multiple-output-values) instead.

## Cancellation tokens

A function can accept a [CancellationToken](/en-us/dotnet/api/system.threading.cancellationtoken) parameter, which enables the operating system to notify your code when the function is about to be terminated. You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.

The following example shows how to check for impending function termination.

```
using System;
using System.IO;
using System.Threading;
public static void Run(
string inputText,
TextWriter logger,
CancellationToken token)
{
for (int i = 0; i < 100; i++)
{
if (token.IsCancellationRequested)
{
logger.WriteLine("Function was cancelled at iteration {0}", i);
break;
}
Thread.Sleep(5000);
logger.WriteLine("Normal processing for queue message={0}", inputText);
}
}
```


## Importing namespaces

If you need to import namespaces, you can do so as usual, with the `using`

clause.

```
using System.Net;
using System.Threading.Tasks;
using Microsoft.Extensions.Logging;
public static Task<HttpResponseMessage> Run(HttpRequestMessage req, ILogger log)
```


The following namespaces are automatically imported and are therefore optional:

`System`

`System.Collections.Generic`

`System.IO`

`System.Linq`

`System.Net.Http`

`System.Threading.Tasks`

`Microsoft.Azure.WebJobs`

`Microsoft.Azure.WebJobs.Host`


## Referencing external assemblies

For framework assemblies, add references by using the `#r "AssemblyName"`

directive.

```
#r "System.Web.Http"
using System.Net;
using System.Net.Http;
using System.Threading.Tasks;
using Microsoft.Extensions.Logging;
public static Task<HttpResponseMessage> Run(HttpRequestMessage req, ILogger log)
```


The following assemblies are automatically added by the Azure Functions hosting environment:

`mscorlib`

`System`

`System.Core`

`System.Xml`

`System.Net.Http`

`Microsoft.Azure.WebJobs`

`Microsoft.Azure.WebJobs.Host`

`Microsoft.Azure.WebJobs.Extensions`

`System.Web.Http`

`System.Net.Http.Formatting`


The following assemblies may be referenced by simple-name, by runtime version:

In code, assemblies are referenced like the following example:

```
#r "AssemblyName"
```


## Referencing custom assemblies

To reference a custom assembly, you can use either a *shared* assembly or a *private* assembly:

Shared assemblies are shared across all functions within a function app. To reference a custom assembly, upload the assembly to a folder named

`bin`

in the root folder (wwwroot) of your function app.Private assemblies are part of a given function's context, and support side-loading of different versions. Private assemblies should be uploaded in a

`bin`

folder in the function directory. Reference the assemblies using the file name, such as`#r "MyAssembly.dll"`

.

For information on how to upload files to your function folder, see the section on [package management](#using-nuget-packages).

### Watched directories

The directory that contains the function script file is automatically watched for changes to assemblies. To watch for assembly changes in other directories, add them to the `watchDirectories`

list in [host.json](functions-host-json).

## Using NuGet packages

The way that both binding extension packages and other NuGet packages are added to your function app depends on the [targeted version of the Functions runtime](functions-versions).

By default, the [supported set of Functions extension NuGet packages](functions-triggers-bindings#supported-bindings) are made available to your C# script function app by using extension bundles. To learn more, see [Extension bundles](extension-bundles).

If for some reason you can't use extension bundles in your project, you can also use the Azure Functions Core Tools to install extensions based on bindings defined in the function.json files in your app. When using Core Tools to register extensions, make sure to use the `--csx`

option. To learn more, see [func extensions install](functions-core-tools-reference#func-extensions-install).

By default, Core Tools reads the function.json files and adds the required packages to an *extensions.csproj* C# class library project file in the root of the function app's file system (wwwroot). Because Core Tools uses dotnet.exe, you can use it to add any NuGet package reference to this extensions file. During installation, Core Tools builds the extensions.csproj to install the required libraries. Here's an example *extensions.csproj* file that adds a reference to *Microsoft.ProjectOxford.Face* version *1.1.0*:

```
<Project Sdk="Microsoft.NET.Sdk">
<PropertyGroup>
<TargetFramework>netstandard2.0</TargetFramework>
</PropertyGroup>
<ItemGroup>
<PackageReference Include="Microsoft.ProjectOxford.Face" Version="1.1.0" />
</ItemGroup>
</Project>
```


Note

For C# script (.csx), you must set `TargetFramework`

to a value of `netstandard2.0`

. Other target frameworks, such as `net8.0`

, aren't supported.

To use a custom NuGet feed, specify the feed in a *Nuget.Config* file in the function app root folder. For more information, see [Configuring NuGet behavior](/en-us/nuget/consume-packages/configuring-nuget-behavior).

If you're working on your project only in the portal, you'll need to manually create the extensions.csproj file or a Nuget.Config file directly in the site. To learn more, see [Manually install extensions](functions-how-to-use-azure-function-app-settings#manually-install-extensions).

## Environment variables

To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`

, as shown in the following code example:

```
public static void Run(TimerInfo myTimer, ILogger log)
{
log.LogInformation($"C# Timer trigger function executed at: {DateTime.Now}");
log.LogInformation(GetEnvironmentVariable("AzureWebJobsStorage"));
log.LogInformation(GetEnvironmentVariable("WEBSITE_SITE_NAME"));
}
public static string GetEnvironmentVariable(string name)
{
return name + ": " +
System.Environment.GetEnvironmentVariable(name, EnvironmentVariableTarget.Process);
}
```


## Retry policies

Functions supports two built-in retry policies. For more information, see [Retry policies](functions-bindings-error-pages#retry-policies).

Here's the retry policy in the *function.json* file:

```
{
"disabled": false,
"bindings": [
{
....
}
],
"retry": {
"strategy": "fixedDelay",
"maxRetryCount": 4,
"delayInterval": "00:00:10"
}
}
```


function.json property |
Description |
|---|---|
| strategy | Use `fixedDelay` . |
| maxRetryCount | Required. The maximum number of retries allowed per function execution. `-1` means to retry indefinitely. |
| delayInterval | The delay that's used between retries. Specify it as a string with the format `HH:mm:ss` . |

## Binding at runtime

In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed to the [ declarative](https://en.wikipedia.org/wiki/Declarative_programming) bindings in

*function.json*. Imperative binding is useful when binding parameters need to be computed at runtime rather than design time. With this pattern, you can bind to supported input and output bindings on-the-fly in your function code.

Define an imperative binding as follows:

**Do not**include an entry in*function.json*for your desired imperative bindings.- Pass in an input parameter
or`Binder binder`

.`IBinder binder`

- Use the following C# pattern to perform the data binding.

```
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
...
}
```


`BindingTypeAttribute`

is the .NET attribute that defines your binding and `T`

is an input or output type that's
supported by that binding type. `T`

can't be an `out`

parameter type (such as `out JObject`

). For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [ IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for

`T`

.### Single attribute example

The following example code creates a [Storage blob output binding](functions-bindings-storage-blob-output) with blob path that's defined at run time, then writes a string to the blob.

```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;
public static async Task Run(string input, Binder binder)
{
using (var writer = await binder.BindAsync<TextWriter>(new BlobAttribute("samples-output/path")))
{
writer.Write("Hello World!!");
}
}
```


[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Extensions.Storage/Blobs/BlobAttribute.cs)
defines the [Storage blob](functions-bindings-storage-blob) input or output binding, and
[TextWriter](/en-us/dotnet/api/system.io.textwriter) is a supported output binding type.

### Multiple attributes example

The preceding example gets the app setting for the function app's main Storage account connection string (which is `AzureWebJobsStorage`

). You can specify a custom app setting to use for the Storage account by adding the
[StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)
and passing the attribute array into `BindAsync<T>()`

. Use a `Binder`

parameter, not `IBinder`

. For example:

```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;
public static async Task Run(string input, Binder binder)
{
var attributes = new Attribute[]
{
new BlobAttribute("samples-output/path"),
new StorageAccountAttribute("MyStorageAccount")
};
using (var writer = await binder.BindAsync<TextWriter>(attributes))
{
writer.Write("Hello World!");
}
}
```


The following table lists the .NET attributes for each binding type and the packages in which they're defined.

## Convert a C# script app to a C# project

The easiest way to convert a C# script function app to a compiled C# class library project is to start with a new project. You can then, for each function, migrate the code and configuration from each run.csx file and function.json file in a function folder to a single new .cs class library code file. For example, when you have a C# script function named `HelloWorld`

you'll have two files: `HelloWorld/run.csx`

and `HelloWorld/function.json`

. For this function, you create a code file named `HelloWorld.cs`

in your new class library project.

If you are using C# scripting for portal editing, you can [download the app content to your local machine](deployment-zip-push#download-your-function-app-files). Choose the **Site content** option instead of **Content and Visual Studio project**. You don't need to generate a project, and don't include application settings in the download. You're defining a new development environment, and this environment shouldn't have the same permissions as your hosted app environment.

These instructions show you how to convert C# script functions (which run in-process with the Functions host) to C# class library functions that run in an [isolated worker process](dotnet-isolated-process-guide).

Complete the

**Create a functions app project**section from your preferred quickstart:

If your original C# script code includes an

`extensions.csproj`

file or any`function.proj`

files, copy the package references from these file and add them to the new project's`.csproj`

file in the same`ItemGroup`

with the Functions core dependencies.Tip

Conversion provides a good opportunity to update to the latest versions of your dependencies. Doing so may require additional code changes in a later step.

Copy the contents of the original

`host.json`

file into the new project's`host.json`

file, except for the`extensionBundles`

section (compiled C# projects don't use[extension bundles](extension-bundles)and you must explicitly add references to all extensions used by your functions). When merging host.json files, remember that theschema is versioned, with most apps using version 2.0. The contents of the`host.json`

`extensions`

section can differ based on specific versions of the binding extensions used by your functions. See individual extension reference articles to learn how to correctly configure the host.json for your specific versions.For any

[shared files referenced by a](#reusing-csx-code), create a new`#load`

directive`.cs`

file for each of these shared references. It's simplest to create a new`.cs`

file for each shared class definition. If there are static methods without a class, you need to define new classes for these methods.Perform the following tasks for each

`<FUNCTION_NAME>`

folder in your original project:Create a new file named

`<FUNCTION_NAME>.cs`

, replacing`<FUNCTION_NAME>`

with the name of the folder that defined your C# script function. You can create a new function code file from one of the trigger-specific templates in the following way:Using the

`func new --name <FUNCTION_NAME>`

command and choosing the correct trigger template at the prompt.Copy the

`using`

statements from your`run.csx`

file and add them to the new file. You do not need any`#r`

directives.For any

`#load`

statement in your`run.csx`

file, add a new`using`

statement for the namespace you used for the shared code.In the new file, define a class for your function under the namespace you are using for the project.

Create a new method named

`RunHandler`

or something similar. This new method serves as the new entry point for the function.Copy the static method that represents your function, along with any functions it calls, from

`run.csx`

into your new class as a second method. From the new method you created in the previous step, call into this static method. This indirection step is helpful for navigating any differences as you continue the upgrade. You can keep the original method exactly the same and simply control its inputs from the new context. You may need to create parameters on the new method which you then pass into the static method call. After you have confirmed that the migration has worked as intended, you can remove this extra level of indirection.For each binding in the

`function.json`

file, add the corresponding attribute to your new method. To quickly find binding examples, see[Manually add bindings based on examples](add-bindings-existing-function?tabs=csharp).Add any extension packages required by the bindings to your project, if you haven't already done so.


Recreate any application settings required by your app in the

`Values`

collection of the[local.settings.json file](functions-develop-local#local-settings-file).Verify that your project runs locally:

Use

`func start`

to run your app from the command line. For more information, see[Run functions locally](functions-run-local#start).Publish your project to a new function app in Azure:

[Create your Azure resources](how-to-create-function-azure-cli?pivots=programming-language-csharp#create-supporting-azure-resources-for-your-function)and deploy the code project to Azure by using the`func azure functionapp publish <APP_NAME>`

command. For more information, see[Deploy project files](functions-run-local#project-file-deployment).

### Example function conversion

This section shows an example of the migration for a single function.

The original function in C# scripting has two files:

`HelloWorld/function.json`

`HelloWorld/run.csx`


The contents of `HelloWorld/function.json`

are:

```
{
"bindings": [
{
"authLevel": "FUNCTION",
"name": "req",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
]
},
{
"name": "$return",
"type": "http",
"direction": "out"
}
]
}
```


The contents of `HelloWorld/run.csx`

are:

```
#r "Newtonsoft.Json"
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
public static async Task<IActionResult> Run(HttpRequest req, ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
string name = req.Query["name"];
string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
dynamic data = JsonConvert.DeserializeObject(requestBody);
name = name ?? data?.name;
string responseMessage = string.IsNullOrEmpty(name)
? "This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response."
: $"Hello, {name}. This HTTP triggered function executed successfully.";
return new OkObjectResult(responseMessage);
}
```


After migrating to the isolated worker model with ASP.NET Core integration, these are replaced by a single `HelloWorld.cs`

:

```
using System.Net;
using Microsoft.Azure.Functions.Worker;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Logging;
using Microsoft.AspNetCore.Routing;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
namespace MyFunctionApp
{
public class HelloWorld
{
private readonly ILogger _logger;
public HelloWorld(ILoggerFactory loggerFactory)
{
_logger = loggerFactory.CreateLogger<HelloWorld>();
}
[Function("HelloWorld")]
public async Task<IActionResult> RunHandler([HttpTrigger(AuthorizationLevel.Function, "get")] HttpRequest req)
{
return await Run(req, _logger);
}
// From run.csx
public static async Task<IActionResult> Run(HttpRequest req, ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
string name = req.Query["name"];
string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
dynamic data = JsonConvert.DeserializeObject(requestBody);
name = name ?? data?.name;
string responseMessage = string.IsNullOrEmpty(name)
? "This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response."
: $"Hello, {name}. This HTTP triggered function executed successfully.";
return new OkObjectResult(responseMessage);
}
}
}
```


## Binding configuration and examples

This section contains references and examples for defining triggers and bindings in C# script.

### Blob trigger

The following table explains the binding configuration properties for C# script that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `blobTrigger` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to `in` . This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that represents the blob in function code. |
path |
The
|

**connection**[Connections](functions-bindings-storage-blob-trigger#connections).The following example shows a blob trigger definition in a *function.json* file and code that uses the binding. The function writes a log when a blob is added or updated in the `samples-workitems`

[container](../storage/blobs/storage-blobs-introduction#blob-storage-resources).

Here's the binding data in the *function.json* file:

```
{
"disabled": false,
"bindings": [
{
"name": "myBlob",
"type": "blobTrigger",
"direction": "in",
"path": "samples-workitems/{name}",
"connection":"MyStorageAccountAppSetting"
}
]
}
```


The string `{name}`

in the blob trigger path `samples-workitems/{name}`

creates a [binding expression](functions-bindings-expressions-patterns) that you can use in function code to access the file name of the triggering blob. For more information, see [Blob name patterns](functions-bindings-storage-blob-trigger#blob-name-patterns).

Here's C# script code that binds to a `Stream`

:

```
public static void Run(Stream myBlob, string name, ILogger log)
{
log.LogInformation($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```


Here's C# script code that binds to a `CloudBlockBlob`

:

```
#r "Microsoft.WindowsAzure.Storage"
using Microsoft.WindowsAzure.Storage.Blob;
public static void Run(CloudBlockBlob myBlob, string name, ILogger log)
{
log.LogInformation($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```


### Blob input

The following table explains the binding configuration properties for C# script that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `blob` . |
direction |
Must be set to `in` . |
name |
The name of the variable that represents the blob in function code. |
path |
The path to the blob. |
connection |
The name of an app setting or setting collection that specifies how to connect to Azure Blobs. See
|

The following example shows blob input and output bindings in a *function.json* file and C# script code that uses the bindings. The function makes a copy of a text blob. The function is triggered by a queue message that contains the name of the blob to copy. The new blob is named *{originalblobname}-Copy*.

In the *function.json* file, the `queueTrigger`

metadata property is used to specify the blob name in the `path`

properties:

```
{
"bindings": [
{
"queueName": "myqueue-items",
"connection": "MyStorageConnectionAppSetting",
"name": "myQueueItem",
"type": "queueTrigger",
"direction": "in"
},
{
"name": "myInputBlob",
"type": "blob",
"path": "samples-workitems/{queueTrigger}",
"connection": "MyStorageConnectionAppSetting",
"direction": "in"
},
{
"name": "myOutputBlob",
"type": "blob",
"path": "samples-workitems/{queueTrigger}-Copy",
"connection": "MyStorageConnectionAppSetting",
"direction": "out"
}
],
"disabled": false
}
```


Here's the C# script code:

```
public static void Run(string myQueueItem, string myInputBlob, out string myOutputBlob, ILogger log)
{
log.LogInformation($"C# Queue trigger function processed: {myQueueItem}");
myOutputBlob = myInputBlob;
}
```


### Blob output

The following table explains the binding configuration properties for C# script that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `blob` . |
direction |
Must be set to `out` . |
name |
The name of the variable that represents the blob in function code. |
path |
The path to the blob. |
connection |
The name of an app setting or setting collection that specifies how to connect to Azure Blobs. See
|

The following example shows blob input and output bindings in a *function.json* file and C# script code that uses the bindings. The function makes a copy of a text blob. The function is triggered by a queue message that contains the name of the blob to copy. The new blob is named *{originalblobname}-Copy*.

In the *function.json* file, the `queueTrigger`

metadata property is used to specify the blob name in the `path`

properties:

```
{
"bindings": [
{
"queueName": "myqueue-items",
"connection": "MyStorageConnectionAppSetting",
"name": "myQueueItem",
"type": "queueTrigger",
"direction": "in"
},
{
"name": "myInputBlob",
"type": "blob",
"path": "samples-workitems/{queueTrigger}",
"connection": "MyStorageConnectionAppSetting",
"direction": "in"
},
{
"name": "myOutputBlob",
"type": "blob",
"path": "samples-workitems/{queueTrigger}-Copy",
"connection": "MyStorageConnectionAppSetting",
"direction": "out"
}
],
"disabled": false
}
```


Here's the C# script code:

```
public static void Run(string myQueueItem, string myInputBlob, out string myOutputBlob, ILogger log)
{
log.LogInformation($"C# Queue trigger function processed: {myQueueItem}");
myOutputBlob = myInputBlob;
}
```


### RabbitMQ trigger

The following example shows a RabbitMQ trigger binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding. The function reads and logs the RabbitMQ message.

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


Here's the C# script code:

```
using System;
public static void Run(string myQueueItem, ILogger log)
{
log.LogInformation($"C# Script RabbitMQ trigger function processed: {myQueueItem}");
}
```


### Queue trigger

The following table explains the binding configuration properties for C# script that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `queueTrigger` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
In the function.json file only. Must be set to `in` . This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that contains the queue item payload in the function code. |
queueName |
The name of the queue to poll. |
connection |
The name of an app setting or setting collection that specifies how to connect to Azure Queues. See
|

The following example shows a queue trigger binding in a *function.json* file and C# script code that uses the binding. The function polls the `myqueue-items`

queue and writes a log each time a queue item is processed.

Here's the *function.json* file:

```
{
"disabled": false,
"bindings": [
{
"type": "queueTrigger",
"direction": "in",
"name": "myQueueItem",
"queueName": "myqueue-items",
"connection":"MyStorageConnectionAppSetting"
}
]
}
```


Here's the C# script code:

```
#r "Microsoft.WindowsAzure.Storage"
using Microsoft.Extensions.Logging;
using Microsoft.WindowsAzure.Storage.Queue;
using System;
public static void Run(CloudQueueMessage myQueueItem,
DateTimeOffset expirationTime,
DateTimeOffset insertionTime,
DateTimeOffset nextVisibleTime,
string queueTrigger,
string id,
string popReceipt,
int dequeueCount,
ILogger log)
{
log.LogInformation($"C# Queue trigger function processed: {myQueueItem.AsString}\n" +
$"queueTrigger={queueTrigger}\n" +
$"expirationTime={expirationTime}\n" +
$"insertionTime={insertionTime}\n" +
$"nextVisibleTime={nextVisibleTime}\n" +
$"id={id}\n" +
$"popReceipt={popReceipt}\n" +
$"dequeueCount={dequeueCount}");
}
```


### Queue output

The following table explains the binding configuration properties for C# script that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `queue` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to `out` . This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that represents the queue in function code. Set to `$return` to reference the function return value. |
queueName |
The name of the queue. |
connection |
The name of an app setting or setting collection that specifies how to connect to Azure Queues. See
|

The following example shows an HTTP trigger binding in a *function.json* file and C# script code that uses the binding. The function creates a queue item with a **CustomQueueMessage** object payload for each HTTP request received.

Here's the *function.json* file:

```
{
"bindings": [
{
"type": "httpTrigger",
"direction": "in",
"authLevel": "function",
"name": "input"
},
{
"type": "http",
"direction": "out",
"name": "$return"
},
{
"type": "queue",
"direction": "out",
"name": "$return",
"queueName": "outqueue",
"connection": "MyStorageConnectionAppSetting"
}
]
}
```


Here's C# script code that creates a single queue message:

```
public class CustomQueueMessage
{
public string PersonName { get; set; }
public string Title { get; set; }
}
public static CustomQueueMessage Run(CustomQueueMessage input, ILogger log)
{
return input;
}
```


You can send multiple messages at once by using an `ICollector`

or `IAsyncCollector`

parameter. Here's C# script code that sends multiple messages, one with the HTTP request data and one with hard-coded values:

```
public static void Run(
CustomQueueMessage input,
ICollector<CustomQueueMessage> myQueueItems,
ILogger log)
{
myQueueItems.Add(input);
myQueueItems.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```


### Table input

This section outlines support for the [Tables API version of the extension](functions-bindings-storage-table?tabs=in-process,table-api) only.

The following table explains the binding configuration properties for C# script that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `table` . This property is set automatically when you create the binding in the Azure portal. |
direction |
Must be set to `in` . This property is set automatically when you create the binding in the Azure portal. |
name |
The name of the variable that represents the table or entity in function code. |
tableName |
The name of the table. |
partitionKey |
Optional. The partition key of the table entity to read. |
rowKey |
Optional. The row key of the table entity to read. Can't be used with `take` or `filter` . |
take |
Optional. The maximum number of entities to return. Can't be used with `rowKey` . |
filter |
Optional. An OData filter expression for the entities to return from the table. Can't be used with `rowKey` . |
connection |
The name of an app setting or setting collection that specifies how to connect to the table service. See
|

The following example shows a table input binding in a *function.json* file and C# script code that uses the binding. The function uses a queue trigger to read a single table row.

The *function.json* file specifies a `partitionKey`

and a `rowKey`

. The `rowKey`

value `{queueTrigger}`

indicates that the row key comes from the queue message string.

```
{
"bindings": [
{
"queueName": "myqueue-items",
"connection": "MyStorageConnectionAppSetting",
"name": "myQueueItem",
"type": "queueTrigger",
"direction": "in"
},
{
"name": "personEntity",
"type": "table",
"tableName": "Person",
"partitionKey": "Test",
"rowKey": "{queueTrigger}",
"connection": "MyStorageConnectionAppSetting",
"direction": "in"
}
],
"disabled": false
}
```


Here's the C# script code:

```
#r "Azure.Data.Tables"
using Microsoft.Extensions.Logging;
using Azure.Data.Tables;
public static void Run(string myQueueItem, Person personEntity, ILogger log)
{
log.LogInformation($"C# Queue trigger function processed: {myQueueItem}");
log.LogInformation($"Name in Person entity: {personEntity.Name}");
}
public class Person : ITableEntity
{
public string Name { get; set; }
public string PartitionKey { get; set; }
public string RowKey { get; set; }
public DateTimeOffset? Timestamp { get; set; }
public ETag ETag { get; set; }
}
```


### Table output

This section outlines support for the [Tables API version of the extension](functions-bindings-storage-table?tabs=in-process,table-api) only.

The following table explains the binding configuration properties for C# script that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `table` . This property is set automatically when you create the binding in the Azure portal. |
direction |
Must be set to `out` . This property is set automatically when you create the binding in the Azure portal. |
name |
The variable name used in function code that represents the table or entity. Set to `$return` to reference the function return value. |
tableName |
The name of the table to which to write. |
partitionKey |
The partition key of the table entity to write. |
rowKey |
The row key of the table entity to write. |
connection |
The name of an app setting or setting collection that specifies how to connect to the table service. See
|

The following example shows a table output binding in a *function.json* file and C# script code that uses the binding. The function writes multiple table entities.

Here's the *function.json* file:

```
{
"bindings": [
{
"name": "input",
"type": "manualTrigger",
"direction": "in"
},
{
"tableName": "Person",
"connection": "MyStorageConnectionAppSetting",
"name": "tableBinding",
"type": "table",
"direction": "out"
}
],
"disabled": false
}
```


Here's the C# script code:

```
public static void Run(string input, ICollector<Person> tableBinding, ILogger log)
{
for (int i = 1; i < 10; i++)
{
log.LogInformation($"Adding Person entity {i}");
tableBinding.Add(
new Person() {
PartitionKey = "Test",
RowKey = i.ToString(),
Name = "Name" + i.ToString() }
);
}
}
public class Person
{
public string PartitionKey { get; set; }
public string RowKey { get; set; }
public string Name { get; set; }
}
```


### Timer trigger

The following table explains the binding configuration properties for C# script that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `timerTrigger` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to `in` . This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that represents the timer object in function code. |
schedule |
A
`TimeSpan` can be used only for a function app that runs on an App Service Plan. You can put the schedule expression in an app setting and set this property to the app setting name wrapped in % signs, as in this example: "%ScheduleAppSetting%". |

**runOnStartup**`true`

, the function is invoked when the runtime starts. For example, the runtime starts when the function app wakes up after going idle due to inactivity. when the function app restarts due to function changes, and when the function app scales out. *Use with caution.***runOnStartup**should rarely if ever be set to`true`

, especially in production.**useMonitor**`true`

or `false`

to indicate whether the schedule should be monitored. Schedule monitoring persists schedule occurrences to aid in ensuring the schedule is maintained correctly even when function app instances restart. If not set explicitly, the default is `true`

for schedules that have a recurrence interval greater than or equal to 1 minute. For schedules that trigger more than once per minute, the default is `false`

.The following example shows a timer trigger binding in a *function.json* file and a C# script function that uses the binding. The function writes a log indicating whether this function invocation is due to a missed schedule occurrence. The [ TimerInfo](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) object is passed into the function.

Here's the binding data in the *function.json* file:

```
{
"schedule": "0 */5 * * * *",
"name": "myTimer",
"type": "timerTrigger",
"direction": "in"
}
```


Here's the C# script code:

```
public static void Run(TimerInfo myTimer, ILogger log)
{
if (myTimer.IsPastDue)
{
log.LogInformation("Timer is running late!");
}
log.LogInformation($"C# Timer trigger function executed at: {DateTime.Now}" );
}
```


### HTTP trigger

The following table explains the trigger configuration properties that you set in the *function.json* file:

| function.json property | Description |
|---|---|
type |
Required - must be set to `httpTrigger` . |
direction |
Required - must be set to `in` . |
name |
Required - the variable name used in function code for the request or request body. |
authLevel |
Determines what keys, if any, need to be present on the request in order to invoke the function. For supported values, see
|

**methods**[customize the HTTP endpoint](functions-bindings-http-webhook-trigger#customize-the-http-endpoint).**route**`<functionname>`

. For more information, see [customize the HTTP endpoint](functions-bindings-http-webhook-trigger#customize-the-http-endpoint).**webHookType***Supported only for the version 1.x runtime.*Configures the HTTP trigger to act as a

[webhook](https://en.wikipedia.org/wiki/Webhook)receiver for the specified provider. For supported values, see[WebHook type](functions-bindings-http-webhook-trigger#webhook-type).The following example shows a trigger binding in a *function.json* file and a C# script function that uses the binding. The function looks for a `name`

parameter either in the query string or the body of the HTTP request.

Here's the *function.json* file:

```
{
"disabled": false,
"bindings": [
{
"authLevel": "function",
"name": "req",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
]
},
{
"name": "$return",
"type": "http",
"direction": "out"
}
]
}
```


Here's C# script code that binds to `HttpRequest`

:

```
#r "Newtonsoft.Json"
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
public static async Task<IActionResult> Run(HttpRequest req, ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
string name = req.Query["name"];
string requestBody = String.Empty;
using (StreamReader streamReader = new StreamReader(req.Body))
{
requestBody = await streamReader.ReadToEndAsync();
}
dynamic data = JsonConvert.DeserializeObject(requestBody);
name = name ?? data?.name;
return name != null
? (ActionResult)new OkObjectResult($"Hello, {name}")
: new BadRequestObjectResult("Please pass a name on the query string or in the request body");
}
```


You can bind to a custom object instead of `HttpRequest`

. This object is created from the body of the request and parsed as JSON. Similarly, a type can be passed to the HTTP response output binding and returned as the response body, along with a `200`

status code.

```
using System.Net;
using System.Threading.Tasks;
using Microsoft.Extensions.Logging;
public static string Run(Person person, ILogger log)
{
return person.Name != null
? (ActionResult)new OkObjectResult($"Hello, {person.Name}")
: new BadRequestObjectResult("Please pass an instance of Person.");
}
public class Person {
public string Name {get; set;}
}
```


### HTTP output

The following table explains the binding configuration properties that you set in the *function.json* file.

| Property | Description |
|---|---|
type |
Must be set to `http` . |
direction |
Must be set to `out` . |
name |
The variable name used in function code for the response, or `$return` to use the return value. |

### Event Hubs trigger

The following table explains the trigger configuration properties that you set in the *function.json* file:

| function.json property | Description |
|---|---|
type |
Must be set to `eventHubTrigger` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to `in` . This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that represents the event item in function code. |
eventHubName |
Functions 2.x and higher. The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. Can be referenced via
`%eventHubName%` . In version 1.x, this property is named `path` . |

**consumerGroup**[consumer group](../event-hubs/event-hubs-features#event-consumers)used to subscribe to events in the hub. If omitted, the`$Default`

consumer group is used.**connection**[Connections](functions-bindings-event-hubs-trigger#connections).The following example shows an Event Hubs trigger binding in a *function.json* file and a C# script function that uses the binding. The function logs the message body of the Event Hubs trigger.

The following examples show Event Hubs binding data in the *function.json* file for Functions runtime version 2.x and later versions.

```
{
"type": "eventHubTrigger",
"name": "myEventHubMessage",
"direction": "in",
"eventHubName": "MyEventHub",
"connection": "myEventHubReadConnectionAppSetting"
}
```


Here's the C# script code:

```
using System;
public static void Run(string myEventHubMessage, TraceWriter log)
{
log.Info($"C# function triggered to process a message: {myEventHubMessage}");
}
```


To get access to event metadata in function code, bind to an [EventData](/en-us/dotnet/api/microsoft.servicebus.messaging.eventdata) object. You can also access the same properties by using binding expressions in the method signature. The following example shows both ways to get the same data:

```
#r "Microsoft.Azure.EventHubs"
using System.Text;
using System;
using Microsoft.ServiceBus.Messaging;
using Microsoft.Azure.EventHubs;
public void Run(EventData myEventHubMessage,
DateTime enqueuedTimeUtc,
Int64 sequenceNumber,
string offset,
TraceWriter log)
{
log.Info($"Event: {Encoding.UTF8.GetString(myEventHubMessage.Body)}");
log.Info($"EnqueuedTimeUtc={myEventHubMessage.SystemProperties.EnqueuedTimeUtc}");
log.Info($"SequenceNumber={myEventHubMessage.SystemProperties.SequenceNumber}");
log.Info($"Offset={myEventHubMessage.SystemProperties.Offset}");
// Metadata accessed by using binding expressions
log.Info($"EnqueuedTimeUtc={enqueuedTimeUtc}");
log.Info($"SequenceNumber={sequenceNumber}");
log.Info($"Offset={offset}");
}
```


To receive events in a batch, make `string`

or `EventData`

an array:

```
public static void Run(string[] eventHubMessages, TraceWriter log)
{
foreach (var message in eventHubMessages)
{
log.Info($"C# function triggered to process a message: {message}");
}
}
```


### Event Hubs output

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `eventHub` . |
direction |
Must be set to `out` . This parameter is set automatically when you create the binding in the Azure portal. |
name |
The variable name used in function code that represents the event. |
eventHubName |
Functions 2.x and higher. The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. In Functions 1.x, this property is named `path` . |
connection |
The name of an app setting or setting collection that specifies how to connect to Event Hubs. To learn more, see
|

The following example shows an event hub trigger binding in a *function.json* file and a C# script function that uses the binding. The function writes a message to an event hub.

The following examples show Event Hubs binding data in the *function.json* file for Functions runtime version 2.x and later versions.

```
{
"type": "eventHub",
"name": "outputEventHubMessage",
"eventHubName": "myeventhub",
"connection": "MyEventHubSendAppSetting",
"direction": "out"
}
```


Here's C# script code that creates one message:

```
using System;
using Microsoft.Extensions.Logging;
public static void Run(TimerInfo myTimer, out string outputEventHubMessage, ILogger log)
{
String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
log.LogInformation(msg);
outputEventHubMessage = msg;
}
```


Here's C# script code that creates multiple messages:

```
public static void Run(TimerInfo myTimer, ICollector<string> outputEventHubMessage, ILogger log)
{
string message = $"Message created at: {DateTime.Now}";
log.LogInformation(message);
outputEventHubMessage.Add("1 " + message);
outputEventHubMessage.Add("2 " + message);
}
```


### Event Grid trigger

The following table explains the binding configuration properties for C# script that you set in the *function.json* file. There are no constructor parameters or properties to set in the `EventGridTrigger`

attribute.

| function.json property | Description |
|---|---|
type |
Required - must be set to `eventGridTrigger` . |
direction |
Required - must be set to `in` . |
name |
Required - the variable name used in function code for the parameter that receives the event data. |

The following example shows an Event Grid trigger defined in the *function.json* file.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"type": "eventGridTrigger",
"name": "eventGridEvent",
"direction": "in"
}
],
"disabled": false
}
```


Here's an example of a C# script function that uses an `EventGridEvent`

binding parameter:

```
#r "Azure.Messaging.EventGrid"
using Azure.Messaging.EventGrid;
using Microsoft.Extensions.Logging;
public static void Run(EventGridEvent eventGridEvent, ILogger log)
{
log.LogInformation(eventGridEvent.Data.ToString());
}
```


Here's an example of a C# script function that uses a `JObject`

binding parameter:

```
#r "Newtonsoft.Json"
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;
public static void Run(JObject eventGridEvent, TraceWriter log)
{
log.Info(eventGridEvent.ToString(Formatting.Indented));
}
```


### Event Grid output

The following table explains the binding configuration properties for C# script that you set in the *function.json* file.

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

The following example shows the Event Grid output binding data in the *function.json* file.

```
{
"type": "eventGrid",
"name": "outputEvent",
"topicEndpointUri": "MyEventGridTopicUriSetting",
"topicKeySetting": "MyEventGridTopicKeySetting",
"direction": "out"
}
```


Here's C# script code that creates one event:

```
#r "Microsoft.Azure.EventGrid"
using System;
using Microsoft.Azure.EventGrid.Models;
using Microsoft.Extensions.Logging;
public static void Run(TimerInfo myTimer, out EventGridEvent outputEvent, ILogger log)
{
outputEvent = new EventGridEvent("message-id", "subject-name", "event-data", "event-type", DateTime.UtcNow, "1.0");
}
```


Here's C# script code that creates multiple events:

```
#r "Microsoft.Azure.EventGrid"
using System;
using Microsoft.Azure.EventGrid.Models;
using Microsoft.Extensions.Logging;
public static void Run(TimerInfo myTimer, ICollector<EventGridEvent> outputEvent, ILogger log)
{
outputEvent.Add(new EventGridEvent("message-id-1", "subject-name", "event-data", "event-type", DateTime.UtcNow, "1.0"));
outputEvent.Add(new EventGridEvent("message-id-2", "subject-name", "event-data", "event-type", DateTime.UtcNow, "1.0"));
}
```


### Service Bus trigger

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `serviceBusTrigger` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to `in` . This property is set automatically when you create the trigger in the Azure portal. |
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

when the trigger should automatically call complete after processing, or if the function code will manually call complete.Setting to

`false`

is only supported in C#.If set to

`true`

, the trigger completes the message automatically if the function execution completes successfully, and abandons the message otherwise.<br/When set to

`false`

, you are responsible for calling [ServiceBusReceiver](/en-us/dotnet/api/azure.messaging.servicebus.servicebusreceiver)methods to complete, abandon, or deadletter the message, session, or batch. When an exception is thrown (and none of the`ServiceBusReceiver`

methods are called), then the lock remains. Once the lock expires, the message is re-queued with the `DeliveryCount`

incremented and the lock is automatically renewed.This property is available only in Azure Functions 2.x and higher.

The following example shows a Service Bus trigger binding in a *function.json* file and a C# script function that uses the binding. The function reads message metadata and logs a Service Bus queue message.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"queueName": "testqueue",
"connection": "MyServiceBusConnection",
"name": "myQueueItem",
"type": "serviceBusTrigger",
"direction": "in"
}
],
"disabled": false
}
```


Here's the C# script code:

```
using System;
public static void Run(string myQueueItem,
Int32 deliveryCount,
DateTime enqueuedTimeUtc,
string messageId,
TraceWriter log)
{
log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
log.Info($"EnqueuedTimeUtc={enqueuedTimeUtc}");
log.Info($"DeliveryCount={deliveryCount}");
log.Info($"MessageId={messageId}");
}
```


### Service Bus output

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `serviceBus` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to `out` . This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that represents the queue or topic message in function code. Set to "$return" to reference the function return value. |
queueName |
Name of the queue. Set only if sending queue messages, not for a topic. |
topicName |
Name of the topic. Set only if sending topic messages, not for a queue. |
connection |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

**accessRights**(v1 only)`manage`

and `listen`

. The default is `manage`

, which indicates that the `connection`

has the **Manage**permission. If you use a connection string that does not have the**Manage**permission, set`accessRights`

to "listen". Otherwise, the Functions runtime might fail trying to do operations that require manage rights. In Azure Functions version 2.x and higher, this property is not available because the latest version of the Service Bus SDK doesn't support manage operations.The following example shows a Service Bus output binding in a *function.json* file and a C# script function that uses the binding. The function uses a timer trigger to send a queue message every 15 seconds.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"schedule": "0/15 * * * * *",
"name": "myTimer",
"runsOnStartup": true,
"type": "timerTrigger",
"direction": "in"
},
{
"name": "outputSbQueue",
"type": "serviceBus",
"queueName": "testqueue",
"connection": "MyServiceBusConnection",
"direction": "out"
}
],
"disabled": false
}
```


Here's C# script code that creates a single message:

```
public static void Run(TimerInfo myTimer, ILogger log, out string outputSbQueue)
{
string message = $"Service Bus queue message created at: {DateTime.Now}";
log.LogInformation(message);
outputSbQueue = message;
}
```


Here's C# script code that creates multiple messages:

```
public static async Task Run(TimerInfo myTimer, ILogger log, IAsyncCollector<string> outputSbQueue)
{
string message = $"Service Bus queue messages created at: {DateTime.Now}";
log.LogInformation(message);
await outputSbQueue.AddAsync("1 " + message);
await outputSbQueue.AddAsync("2 " + message);
}
```


### Azure Cosmos DB v2 trigger

This section outlines support for the [version 4.x+ of the extension](functions-bindings-cosmosdb-v2?tabs=in-process,extensionv4) only.

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `cosmosDBTrigger` . |
direction |
Must be set to `in` . This parameter is set automatically when you create the trigger in the Azure portal. |
name |
The variable name used in function code that represents the list of documents with changes. |
connection |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see
|

**databaseName****containerName****leaseConnection**When not set, the

`connection`

value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases container must have write permissions.**leaseDatabaseName**`databaseName`

setting is used.**leaseContainerName**`leases`

is used.**createLeaseContainerIfNotExists**`true`

, the leases container is automatically created when it doesn't already exist. The default value is `false`

. When using Microsoft Entra identities if you set the value to `true`

, creating containers is not [an allowed operation](/en-us/azure/cosmos-db/troubleshoot-forbidden#non-data-operations-are-not-allowed)and your Function won't be able to start.**leasesContainerThroughput**`createLeaseContainerIfNotExists`

is set to `true`

. This parameter is automatically set when the binding is created using the portal.**leaseContainerPrefix****feedPollDelay****leaseAcquireInterval****leaseExpirationInterval****leaseRenewInterval****maxItemsPerInvocation**[transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions)is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch.**startFromBeginning**`true`

when there are leases already created has no effect.**startFromTime**`2021-02-16T14:19:29Z`

. This is only used to set the initial trigger state. After the trigger has a lease state, changing this value has no effect.**preferredLocations**The following example shows an Azure Cosmos DB trigger binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding. The function writes log messages when Azure Cosmos DB records are added or modified.

Here's the binding data in the *function.json* file:

```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseContainerName": "leases",
"connection": "<connection-app-setting>",
"databaseName": "Tasks",
"containerName": "Items",
"createLeaseContainerIfNotExists": true
}
```


Here's the C# script code:

```
using System;
using System.Collections.Generic;
using Microsoft.Extensions.Logging;
// Customize the model with your own desired properties
public class ToDoItem
{
public string id { get; set; }
public string Description { get; set; }
}
public static void Run(IReadOnlyList<ToDoItem> documents, ILogger log)
{
log.LogInformation("Documents modified " + documents.Count);
log.LogInformation("First document Id " + documents[0].id);
}
```


### Azure Cosmos DB v2 input

This section outlines support for the [version 4.x+ of the extension](functions-bindings-cosmosdb-v2?tabs=in-process,extensionv4) only.

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `cosmosDB` . |
direction |
Must be set to `in` . |
name |
The variable name used in function code that represents the list of documents with changes. |
connection |
The name of an app setting or setting container that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see
|

**databaseName****containerName****partitionKey**[partitioned](/en-us/azure/cosmos-db/partitioning-overview#logical-partitions)containers.**id**[binding expressions](functions-bindings-expressions-patterns). Don't set both the`id`

and `sqlQuery`

properties. If you don't set either one, the entire container is retrieved.**sqlQuery**`SELECT * FROM c where c.departmentId = {departmentId}`

. Don't set both the `id`

and `sqlQuery`

properties. If you don't set either one, the entire container is retrieved.**preferredLocations**`East US,South Central US,North Europe`

.This section contains the following examples:

[Queue trigger, look up ID from string](#queue-trigger-look-up-id-from-string-c-script)[Queue trigger, get multiple docs, using SqlQuery](#queue-trigger-get-multiple-docs-using-sqlquery-c-script)[HTTP trigger, look up ID from query string](#http-trigger-look-up-id-from-query-string-c-script)[HTTP trigger, look up ID from route data](#http-trigger-look-up-id-from-route-data-c-script)[HTTP trigger, get multiple docs, using SqlQuery](#http-trigger-get-multiple-docs-using-sqlquery-c-script)[HTTP trigger, get multiple docs, using DocumentClient](#http-trigger-get-multiple-docs-using-documentclient-c-script)

The HTTP trigger examples refer to a simple `ToDoItem`

type:

```
namespace CosmosDBSamplesV2
{
public class ToDoItem
{
public string Id { get; set; }
public string Description { get; set; }
}
}
```


#### Queue trigger, look up ID from string

The following example shows an Azure Cosmos DB input binding in a *function.json* file and a C# script function that uses the binding. The function reads a single document and updates the document's text value.

Here's the binding data in the *function.json* file:

```
{
"name": "inputDocument",
"type": "cosmosDB",
"databaseName": "MyDatabase",
"collectionName": "MyCollection",
"id" : "{queueTrigger}",
"partitionKey": "{partition key value}",
"connectionStringSetting": "MyAccount_COSMOSDB",
"direction": "in"
}
```


Here's the C# script code:

```
using System;
// Change input document contents using Azure Cosmos DB input binding
public static void Run(string myQueueItem, dynamic inputDocument)
{
inputDocument.text = "This has changed.";
}
```


#### Queue trigger, get multiple docs, using SqlQuery

The following example shows an Azure Cosmos DB input binding in a *function.json* file and a C# script function that uses the binding. The function retrieves multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.

The queue trigger provides a parameter `departmentId`

. A queue message of `{ "departmentId" : "Finance" }`

would return all records for the finance department.

Here's the binding data in the *function.json* file:

```
{
"name": "documents",
"type": "cosmosDB",
"direction": "in",
"databaseName": "MyDb",
"collectionName": "MyCollection",
"sqlQuery": "SELECT * from c where c.departmentId = {departmentId}",
"connectionStringSetting": "CosmosDBConnection"
}
```


Here's the C# script code:

```
public static void Run(QueuePayload myQueueItem, IEnumerable<dynamic> documents)
{
foreach (var doc in documents)
{
// operate on each document
}
}
public class QueuePayload
{
public string departmentId { get; set; }
}
```


#### HTTP trigger, look up ID from query string

The following example shows a C# script function that retrieves a single document. The function is triggered by an HTTP request that uses a query string to specify the ID and partition key value to look up. That ID and partition key value are used to retrieve a `ToDoItem`

document from the specified database and collection.

Here's the *function.json* file:

```
{
"bindings": [
{
"authLevel": "anonymous",
"name": "req",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
]
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"type": "cosmosDB",
"name": "toDoItem",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connectionStringSetting": "CosmosDBConnection",
"direction": "in",
"Id": "{Query.id}",
"PartitionKey" : "{Query.partitionKeyValue}"
}
],
"disabled": false
}
```


Here's the C# script code:

```
using System.Net;
using Microsoft.Extensions.Logging;
public static HttpResponseMessage Run(HttpRequestMessage req, ToDoItem toDoItem, ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
if (toDoItem == null)
{
log.LogInformation($"ToDo item not found");
}
else
{
log.LogInformation($"Found ToDo item, Description={toDoItem.Description}");
}
return req.CreateResponse(HttpStatusCode.OK);
}
```


#### HTTP trigger, look up ID from route data

The following example shows a C# script function that retrieves a single document. The function is triggered by an HTTP request that uses route data to specify the ID and partition key value to look up. That ID and partition key value are used to retrieve a `ToDoItem`

document from the specified database and collection.

Here's the *function.json* file:

```
{
"bindings": [
{
"authLevel": "anonymous",
"name": "req",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
],
"route":"todoitems/{partitionKeyValue}/{id}"
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"type": "cosmosDB",
"name": "toDoItem",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connectionStringSetting": "CosmosDBConnection",
"direction": "in",
"id": "{id}",
"partitionKey": "{partitionKeyValue}"
}
],
"disabled": false
}
```


Here's the C# script code:

```
using System.Net;
using Microsoft.Extensions.Logging;
public static HttpResponseMessage Run(HttpRequestMessage req, ToDoItem toDoItem, ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
if (toDoItem == null)
{
log.LogInformation($"ToDo item not found");
}
else
{
log.LogInformation($"Found ToDo item, Description={toDoItem.Description}");
}
return req.CreateResponse(HttpStatusCode.OK);
}
```


#### HTTP trigger, get multiple docs, using SqlQuery

The following example shows a C# script function that retrieves a list of documents. The function is triggered by an HTTP request. The query is specified in the `SqlQuery`

attribute property.

Here's the *function.json* file:

```
{
"bindings": [
{
"authLevel": "anonymous",
"name": "req",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
]
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"type": "cosmosDB",
"name": "toDoItems",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connectionStringSetting": "CosmosDBConnection",
"direction": "in",
"sqlQuery": "SELECT top 2 * FROM c order by c._ts desc"
}
],
"disabled": false
}
```


Here's the C# script code:

```
using System.Net;
using Microsoft.Extensions.Logging;
public static HttpResponseMessage Run(HttpRequestMessage req, IEnumerable<ToDoItem> toDoItems, ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
foreach (ToDoItem toDoItem in toDoItems)
{
log.LogInformation(toDoItem.Description);
}
return req.CreateResponse(HttpStatusCode.OK);
}
```


#### HTTP trigger, get multiple docs, using DocumentClient

The following example shows a C# script function that retrieves a list of documents. The function is triggered by an HTTP request. The code uses a `DocumentClient`

instance provided by the Azure Cosmos DB binding to read a list of documents. The `DocumentClient`

instance could also be used for write operations.

Here's the *function.json* file:

```
{
"bindings": [
{
"authLevel": "anonymous",
"name": "req",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
]
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"type": "cosmosDB",
"name": "client",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connectionStringSetting": "CosmosDBConnection",
"direction": "inout"
}
],
"disabled": false
}
```


Here's the C# script code:

```
#r "Microsoft.Azure.Documents.Client"
using System.Net;
using Microsoft.Azure.Documents.Client;
using Microsoft.Azure.Documents.Linq;
using Microsoft.Extensions.Logging;
public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, DocumentClient client, ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
Uri collectionUri = UriFactory.CreateDocumentCollectionUri("ToDoItems", "Items");
string searchterm = req.GetQueryNameValuePairs()
.FirstOrDefault(q => string.Compare(q.Key, "searchterm", true) == 0)
.Value;
if (searchterm == null)
{
return req.CreateResponse(HttpStatusCode.NotFound);
}
log.LogInformation($"Searching for word: {searchterm} using Uri: {collectionUri.ToString()}");
IDocumentQuery<ToDoItem> query = client.CreateDocumentQuery<ToDoItem>(collectionUri)
.Where(p => p.Description.Contains(searchterm))
.AsDocumentQuery();
while (query.HasMoreResults)
{
foreach (ToDoItem result in await query.ExecuteNextAsync())
{
log.LogInformation(result.Description);
}
}
return req.CreateResponse(HttpStatusCode.OK);
}
```


### Azure Cosmos DB v2 output

This section outlines support for the [version 4.x+ of the extension](functions-bindings-cosmosdb-v2?tabs=in-process,extensionv4) only.

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
connection |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see
|

**databaseName****containerName****createIfNotExists***false*because new containers are created with reserved throughput, which has cost implications. For more information, see the[pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).**partitionKey**`createIfNotExists`

is true, it defines the partition key path for the created container. May include binding parameters.**containerThroughput**`createIfNotExists`

is true, it defines the [throughput](/en-us/azure/cosmos-db/set-throughput)of the created container.**preferredLocations**`East US,South Central US,North Europe`

.This section contains the following examples:

#### Queue trigger, write one doc

The following example shows an Azure Cosmos DB output binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding. The function uses a queue input binding for a queue that receives JSON in the following format:

```
{
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


The function creates Azure Cosmos DB documents in the following format for each record:

```
{
"id": "John Henry-123456",
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


Here's the binding data in the *function.json* file:

```
{
"name": "employeeDocument",
"type": "cosmosDB",
"databaseName": "MyDatabase",
"collectionName": "MyCollection",
"createIfNotExists": true,
"connectionStringSetting": "MyAccount_COSMOSDB",
"direction": "out"
}
```


Here's the C# script code:

```
#r "Newtonsoft.Json"
using Microsoft.Azure.WebJobs.Host;
using Newtonsoft.Json.Linq;
using Microsoft.Extensions.Logging;
public static void Run(string myQueueItem, out object employeeDocument, ILogger log)
{
log.LogInformation($"C# Queue trigger function processed: {myQueueItem}");
dynamic employee = JObject.Parse(myQueueItem);
employeeDocument = new {
id = employee.name + "-" + employee.employeeId,
name = employee.name,
employeeId = employee.employeeId,
address = employee.address
};
}
```


#### Queue trigger, write docs using IAsyncCollector

To create multiple documents, you can bind to `ICollector<T>`

or `IAsyncCollector<T>`

where `T`

is one of the supported types.

This example refers to a simple `ToDoItem`

type:

```
namespace CosmosDBSamplesV2
{
public class ToDoItem
{
public string id { get; set; }
public string Description { get; set; }
}
}
```


Here's the function.json file:

```
{
"bindings": [
{
"name": "toDoItemsIn",
"type": "queueTrigger",
"direction": "in",
"queueName": "todoqueueforwritemulti",
"connectionStringSetting": "AzureWebJobsStorage"
},
{
"type": "cosmosDB",
"name": "toDoItemsOut",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connectionStringSetting": "CosmosDBConnection",
"direction": "out"
}
],
"disabled": false
}
```


Here's the C# script code:

```
using System;
using Microsoft.Extensions.Logging;
public static async Task Run(ToDoItem[] toDoItemsIn, IAsyncCollector<ToDoItem> toDoItemsOut, ILogger log)
{
log.LogInformation($"C# Queue trigger function processed {toDoItemsIn?.Length} items");
foreach (ToDoItem toDoItem in toDoItemsIn)
{
log.LogInformation($"Description={toDoItem.Description}");
await toDoItemsOut.AddAsync(toDoItem);
}
}
```


### Azure Cosmos DB v1 trigger

The following example shows an Azure Cosmos DB trigger binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding. The function writes log messages when Azure Cosmos DB records are modified.

Here's the binding data in the *function.json* file:

```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseCollectionName": "leases",
"connectionStringSetting": "<connection-app-setting>",
"databaseName": "Tasks",
"collectionName": "Items",
"createLeaseCollectionIfNotExists": true
}
```


Here's the C# script code:

```
#r "Microsoft.Azure.Documents.Client"
using System;
using Microsoft.Azure.Documents;
using System.Collections.Generic;
public static void Run(IReadOnlyList<Document> documents, TraceWriter log)
{
log.Info("Documents modified " + documents.Count);
log.Info("First document Id " + documents[0].Id);
}
```


### Azure Cosmos DB v1 input

This section contains the following examples:

[Queue trigger, look up ID from string](#queue-trigger-look-up-id-from-string-c-script)[Queue trigger, get multiple docs, using SqlQuery](#queue-trigger-get-multiple-docs-using-sqlquery-c-script)[HTTP trigger, look up ID from query string](#http-trigger-look-up-id-from-query-string-c-script)[HTTP trigger, look up ID from route data](#http-trigger-look-up-id-from-route-data-c-script)[HTTP trigger, get multiple docs, using SqlQuery](#http-trigger-get-multiple-docs-using-sqlquery-c-script)[HTTP trigger, get multiple docs, using DocumentClient](#http-trigger-get-multiple-docs-using-documentclient-c-script)

The HTTP trigger examples refer to a simple `ToDoItem`

type:

```
namespace CosmosDBSamplesV1
{
public class ToDoItem
{
public string Id { get; set; }
public string Description { get; set; }
}
}
```


#### Queue trigger, look up ID from string

The following example shows an Azure Cosmos DB input binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding. The function reads a single document and updates the document's text value.

Here's the binding data in the *function.json* file:

```
{
"name": "inputDocument",
"type": "documentDB",
"databaseName": "MyDatabase",
"collectionName": "MyCollection",
"id" : "{queueTrigger}",
"partitionKey": "{partition key value}",
"connection": "MyAccount_COSMOSDB",
"direction": "in"
}
```


Here's the C# script code:

```
using System;
// Change input document contents using Azure Cosmos DB input binding
public static void Run(string myQueueItem, dynamic inputDocument)
{
inputDocument.text = "This has changed.";
}
```


#### Queue trigger, get multiple docs, using SqlQuery

The following example shows an Azure Cosmos DB input binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding. The function retrieves multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.

The queue trigger provides a parameter `departmentId`

. A queue message of `{ "departmentId" : "Finance" }`

would return all records for the finance department.

Here's the binding data in the *function.json* file:

```
{
"name": "documents",
"type": "documentdb",
"direction": "in",
"databaseName": "MyDb",
"collectionName": "MyCollection",
"sqlQuery": "SELECT * from c where c.departmentId = {departmentId}",
"connection": "CosmosDBConnection"
}
```


Here's the C# script code:

```
public static void Run(QueuePayload myQueueItem, IEnumerable<dynamic> documents)
{
foreach (var doc in documents)
{
// operate on each document
}
}
public class QueuePayload
{
public string departmentId { get; set; }
}
```


#### HTTP trigger, look up ID from query string

The following example shows a [C# script function](functions-reference-csharp) that retrieves a single document. The function is triggered by an HTTP request that uses a query string to specify the ID to look up. That ID is used to retrieve a `ToDoItem`

document from the specified database and collection.

Here's the *function.json* file:

```
{
"bindings": [
{
"authLevel": "anonymous",
"name": "req",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
]
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"type": "documentDB",
"name": "toDoItem",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connection": "CosmosDBConnection",
"direction": "in",
"Id": "{Query.id}"
}
],
"disabled": true
}
```


Here's the C# script code:

```
using System.Net;
public static HttpResponseMessage Run(HttpRequestMessage req, ToDoItem toDoItem, TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
if (toDoItem == null)
{
log.Info($"ToDo item not found");
}
else
{
log.Info($"Found ToDo item, Description={toDoItem.Description}");
}
return req.CreateResponse(HttpStatusCode.OK);
}
```


#### HTTP trigger, look up ID from route data

The following example shows a [C# script function](functions-reference-csharp) that retrieves a single document. The function is triggered by an HTTP request that uses route data to specify the ID to look up. That ID is used to retrieve a `ToDoItem`

document from the specified database and collection.

Here's the *function.json* file:

```
{
"bindings": [
{
"authLevel": "anonymous",
"name": "req",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
],
"route":"todoitems/{id}"
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"type": "documentDB",
"name": "toDoItem",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connection": "CosmosDBConnection",
"direction": "in",
"Id": "{id}"
}
],
"disabled": false
}
```


Here's the C# script code:

```
using System.Net;
public static HttpResponseMessage Run(HttpRequestMessage req, ToDoItem toDoItem, TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
if (toDoItem == null)
{
log.Info($"ToDo item not found");
}
else
{
log.Info($"Found ToDo item, Description={toDoItem.Description}");
}
return req.CreateResponse(HttpStatusCode.OK);
}
```


#### HTTP trigger, get multiple docs, using SqlQuery

The following example shows a [C# script function](functions-reference-csharp) that retrieves a list of documents. The function is triggered by an HTTP request. The query is specified in the `SqlQuery`

attribute property.

Here's the *function.json* file:

```
{
"bindings": [
{
"authLevel": "anonymous",
"name": "req",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
]
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"type": "documentDB",
"name": "toDoItems",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connection": "CosmosDBConnection",
"direction": "in",
"sqlQuery": "SELECT top 2 * FROM c order by c._ts desc"
}
],
"disabled": false
}
```


Here's the C# script code:

```
using System.Net;
public static HttpResponseMessage Run(HttpRequestMessage req, IEnumerable<ToDoItem> toDoItems, TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
foreach (ToDoItem toDoItem in toDoItems)
{
log.Info(toDoItem.Description);
}
return req.CreateResponse(HttpStatusCode.OK);
}
```


#### HTTP trigger, get multiple docs, using DocumentClient

The following example shows a [C# script function](functions-reference-csharp) that retrieves a list of documents. The function is triggered by an HTTP request. The code uses a `DocumentClient`

instance provided by the Azure Cosmos DB binding to read a list of documents. The `DocumentClient`

instance could also be used for write operations.

Here's the *function.json* file:

```
{
"bindings": [
{
"authLevel": "anonymous",
"name": "req",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
]
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"type": "documentDB",
"name": "client",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connection": "CosmosDBConnection",
"direction": "inout"
}
],
"disabled": false
}
```


Here's the C# script code:

```
#r "Microsoft.Azure.Documents.Client"
using System.Net;
using Microsoft.Azure.Documents.Client;
using Microsoft.Azure.Documents.Linq;
public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, DocumentClient client, TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
Uri collectionUri = UriFactory.CreateDocumentCollectionUri("ToDoItems", "Items");
string searchterm = req.GetQueryNameValuePairs()
.FirstOrDefault(q => string.Compare(q.Key, "searchterm", true) == 0)
.Value;
if (searchterm == null)
{
return req.CreateResponse(HttpStatusCode.NotFound);
}
log.Info($"Searching for word: {searchterm} using Uri: {collectionUri.ToString()}");
IDocumentQuery<ToDoItem> query = client.CreateDocumentQuery<ToDoItem>(collectionUri)
.Where(p => p.Description.Contains(searchterm))
.AsDocumentQuery();
while (query.HasMoreResults)
{
foreach (ToDoItem result in await query.ExecuteNextAsync())
{
log.Info(result.Description);
}
}
return req.CreateResponse(HttpStatusCode.OK);
}
```


### Azure Cosmos DB v1 output

This section contains the following examples:

- Queue trigger, write one doc
- Queue trigger, write docs using
`IAsyncCollector`


#### Queue trigger, write one doc

The following example shows an Azure Cosmos DB output binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding. The function uses a queue input binding for a queue that receives JSON in the following format:

```
{
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


The function creates Azure Cosmos DB documents in the following format for each record:

```
{
"id": "John Henry-123456",
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


Here's the binding data in the *function.json* file:

```
{
"name": "employeeDocument",
"type": "documentDB",
"databaseName": "MyDatabase",
"collectionName": "MyCollection",
"createIfNotExists": true,
"connection": "MyAccount_COSMOSDB",
"direction": "out"
}
```


Here's the C# script code:

```
#r "Newtonsoft.Json"
using Microsoft.Azure.WebJobs.Host;
using Newtonsoft.Json.Linq;
public static void Run(string myQueueItem, out object employeeDocument, TraceWriter log)
{
log.Info($"C# Queue trigger function processed: {myQueueItem}");
dynamic employee = JObject.Parse(myQueueItem);
employeeDocument = new {
id = employee.name + "-" + employee.employeeId,
name = employee.name,
employeeId = employee.employeeId,
address = employee.address
};
}
```


#### Queue trigger, write docs using IAsyncCollector

To create multiple documents, you can bind to `ICollector<T>`

or `IAsyncCollector<T>`

where `T`

is one of the supported types.

This example refers to a simple `ToDoItem`

type:

```
namespace CosmosDBSamplesV1
{
public class ToDoItem
{
public string Id { get; set; }
public string Description { get; set; }
}
}
```


Here's the function.json file:

```
{
"bindings": [
{
"name": "toDoItemsIn",
"type": "queueTrigger",
"direction": "in",
"queueName": "todoqueueforwritemulti",
"connection": "AzureWebJobsStorage"
},
{
"type": "documentDB",
"name": "toDoItemsOut",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connection": "CosmosDBConnection",
"direction": "out"
}
],
"disabled": false
}
```


Here's the C# script code:

```
using System;
public static async Task Run(ToDoItem[] toDoItemsIn, IAsyncCollector<ToDoItem> toDoItemsOut, TraceWriter log)
{
log.Info($"C# Queue trigger function processed {toDoItemsIn?.Length} items");
foreach (ToDoItem toDoItem in toDoItemsIn)
{
log.Info($"Description={toDoItem.Description}");
await toDoItemsOut.AddAsync(toDoItem);
}
}
```


### Azure SQL trigger

More samples for the Azure SQL trigger are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-csx).

The example refers to a `ToDoItem`

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


[Change tracking](functions-bindings-azure-sql-trigger#set-up-change-tracking-required) is enabled on the database and on the table:

```
ALTER DATABASE [SampleDatabase]
SET CHANGE_TRACKING = ON
(CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON);
ALTER TABLE [dbo].[ToDo]
ENABLE CHANGE_TRACKING;
```


The SQL trigger binds to a `IReadOnlyList<SqlChange<T>>`

, a list of `SqlChange`

objects each with two properties:

**Item:**the item that was changed. The type of the item should follow the table schema as seen in the`ToDoItem`

class.**Operation:**a value from`SqlChangeOperation`

enum. The possible values are`Insert`

,`Update`

, and`Delete`

.

The following example shows a SQL trigger in a function.json file and a [C# script function](functions-reference-csharp) that is invoked when there are changes to the `ToDo`

table:

The following is binding data in the function.json file:

```
{
"name": "todoChanges",
"type": "sqlTrigger",
"direction": "in",
"tableName": "dbo.ToDo",
"connectionStringSetting": "SqlConnectionString"
}
```


The following is the C# script function:

```
#r "Newtonsoft.Json"
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
public static void Run(IReadOnlyList<SqlChange<ToDoItem>> todoChanges, ILogger log)
{
log.LogInformation($"C# SQL trigger function processed a request.");
foreach (SqlChange<ToDoItem> change in todoChanges)
{
ToDoItem toDoItem = change.Item;
log.LogInformation($"Change operation: {change.Operation}");
log.LogInformation($"Id: {toDoItem.Id}, Title: {toDoItem.title}, Url: {toDoItem.url}, Completed: {toDoItem.completed}");
}
}
```


### Azure SQL input

More samples for the Azure SQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-csx).

This section contains the following examples:

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


#### HTTP trigger, get row by ID from query string

The following example shows an Azure SQL input binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding. The function is triggered by an HTTP request that uses a query string to specify the ID. That ID is used to retrieve a `ToDoItem`

record with the specified query.

Note

The HTTP query string parameter is case-sensitive.

Here's the binding data in the *function.json* file:

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


Here's the C# script code:

```
#r "Newtonsoft.Json"
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
using System.Collections.Generic;
public static IActionResult Run(HttpRequest req, ILogger log, IEnumerable<ToDoItem> todoItem)
{
return new OkObjectResult(todoItem);
}
```


#### HTTP trigger, delete rows

The following example shows an Azure SQL input binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding to execute a stored procedure with input from the HTTP request query parameter. In this example, the stored procedure deletes a single record or all records depending on the value of the parameter.

The stored procedure `dbo.DeleteToDo`

must be created on the SQL database.

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


Here's the binding data in the *function.json* file:

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


```
using System;
using System.Collections.Generic;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Logging;
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
[Sql(commandText: "DeleteToDo", commandType: System.Data.CommandType.StoredProcedure,
parameters: "@Id={Query.id}", connectionStringSetting: "SqlConnectionString")]
IEnumerable<ToDoItem> toDoItems)
{
return new OkObjectResult(toDoItems);
}
}
}
```


Here's the C# script code:

```
#r "Newtonsoft.Json"
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
using System.Collections.Generic;
public static IActionResult Run(HttpRequest req, ILogger log, IEnumerable<ToDoItem> todoItems)
{
return new OkObjectResult(todoItems);
}
```


### Azure SQL output

More samples for the Azure SQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-csx).

This section contains the following examples:

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


#### HTTP trigger, write records to a table

The following example shows a SQL output binding in a function.json file and a [C# script function](functions-reference-csharp) that adds records to a table, using data provided in an HTTP POST request as a JSON body.

The following is binding data in the function.json file:

```
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"post"
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
"direction": "out",
"commandText": "dbo.ToDo",
"connectionStringSetting": "SqlConnectionString"
}
```


The following is sample C# script code:

```
#r "Newtonsoft.Json"
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
public static IActionResult Run(HttpRequest req, ILogger log, out ToDoItem todoItem)
{
log.LogInformation("C# HTTP trigger function processed a request.");
string requestBody = new StreamReader(req.Body).ReadToEnd();
todoItem = JsonConvert.DeserializeObject<ToDoItem>(requestBody);
return new OkObjectResult(todoItem);
}
```


#### HTTP trigger, write to two tables

The following example shows a SQL output binding in a function.json file and a [C# script function](functions-reference-csharp) that adds records to a database in two different tables (`dbo.ToDo`

and `dbo.RequestLog`

), using data provided in an HTTP POST request as a JSON body and multiple output bindings.

The second table, `dbo.RequestLog`

, corresponds to the following definition:

```
CREATE TABLE dbo.RequestLog (
Id int identity(1,1) primary key,
RequestTimeStamp datetime2 not null,
ItemCount int not null
)
```


The following is binding data in the function.json file:

```
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"post"
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
"direction": "out",
"commandText": "dbo.ToDo",
"connectionStringSetting": "SqlConnectionString"
},
{
"name": "requestLog",
"type": "sql",
"direction": "out",
"commandText": "dbo.RequestLog",
"connectionStringSetting": "SqlConnectionString"
}
```


The following is sample C# script code:

```
#r "Newtonsoft.Json"
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
public static IActionResult Run(HttpRequest req, ILogger log, out ToDoItem todoItem, out RequestLog requestLog)
{
log.LogInformation("C# HTTP trigger function processed a request.");
string requestBody = new StreamReader(req.Body).ReadToEnd();
todoItem = JsonConvert.DeserializeObject<ToDoItem>(requestBody);
requestLog = new RequestLog();
requestLog.RequestTimeStamp = DateTime.Now;
requestLog.ItemCount = 1;
return new OkObjectResult(todoItem);
}
public class RequestLog {
public DateTime RequestTimeStamp { get; set; }
public int ItemCount { get; set; }
}
```


### RabbitMQ output

The following example shows a RabbitMQ output binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding. The function reads in the message from an HTTP trigger and outputs it to the RabbitMQ queue.

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


Here's the C# script code:

```
using System;
using Microsoft.Extensions.Logging;
public static void Run(string input, out string outputMessage, ILogger log)
{
log.LogInformation(input);
outputMessage = input;
}
```


### SendGrid output

The following example shows a SendGrid output binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"type": "queueTrigger",
"name": "mymsg",
"queueName": "myqueue",
"connection": "AzureWebJobsStorage",
"direction": "in"
},
{
"type": "sendGrid",
"name": "$return",
"direction": "out",
"apiKey": "SendGridAPIKeyAsAppSetting",
"from": "{FromEmail}",
"to": "{ToEmail}"
}
]
}
```


Here's the C# script code:

```
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;
using Microsoft.Azure.WebJobs.Host;
public static SendGridMessage Run(Message mymsg, ILogger log)
{
SendGridMessage message = new SendGridMessage()
{
Subject = $"{mymsg.Subject}"
};
message.AddContent("text/plain", $"{mymsg.Content}");
return message;
}
public class Message
{
public string ToEmail { get; set; }
public string FromEmail { get; set; }
public string Subject { get; set; }
public string Content { get; set; }
}
```


### SignalR trigger

Here's example binding data in the *function.json* file:

```
{
"type": "signalRTrigger",
"name": "invocation",
"hubName": "SignalRTest",
"category": "messages",
"event": "SendMessage",
"parameterNames": [
"message"
],
"direction": "in"
}
```


And, here's the code:

```
#r "Microsoft.Azure.WebJobs.Extensions.SignalRService"
using System;
using Microsoft.Azure.WebJobs.Extensions.SignalRService;
using Microsoft.Extensions.Logging;
public static void Run(InvocationContext invocation, string message, ILogger logger)
{
logger.LogInformation($"Receive {message} from {invocationContext.ConnectionId}.");
}
```


### SignalR input

The following example shows a SignalR connection info input binding in a *function.json* file and a [C# Script function](functions-reference-csharp) that uses the binding to return the connection information.

Here's binding data in the *function.json* file:

Example function.json:

```
{
"type": "signalRConnectionInfo",
"name": "connectionInfo",
"hubName": "chat",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "in"
}
```


Here's the C# Script code:

```
#r "Microsoft.Azure.WebJobs.Extensions.SignalRService"
using Microsoft.Azure.WebJobs.Extensions.SignalRService;
public static SignalRConnectionInfo Run(HttpRequest req, SignalRConnectionInfo connectionInfo)
{
return connectionInfo;
}
```


You can set the `userId`

property of the binding to the value from either header using a [binding expression](functions-bindings-signalr-service-input#binding-expressions-for-http-trigger): `{headers.x-ms-client-principal-id}`

or `{headers.x-ms-client-principal-name}`

.

Example function.json:

```
{
"type": "signalRConnectionInfo",
"name": "connectionInfo",
"hubName": "chat",
"userId": "{headers.x-ms-client-principal-id}",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "in"
}
```


Here's the C# Script code:

```
#r "Microsoft.Azure.WebJobs.Extensions.SignalRService"
using Microsoft.Azure.WebJobs.Extensions.SignalRService;
public static SignalRConnectionInfo Run(HttpRequest req, SignalRConnectionInfo connectionInfo)
{
// connectionInfo contains an access key token with a name identifier
// claim set to the authenticated user
return connectionInfo;
}
```


### SignalR output

Here's binding data in the *function.json* file:

Example function.json:

```
{
"type": "signalR",
"name": "signalRMessages",
"hubName": "<hub_name>",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "out"
}
```


Here's the C# Script code:

```
#r "Microsoft.Azure.WebJobs.Extensions.SignalRService"
using Microsoft.Azure.WebJobs.Extensions.SignalRService;
public static Task Run(
object message,
IAsyncCollector<SignalRMessage> signalRMessages)
{
return signalRMessages.AddAsync(
new SignalRMessage
{
Target = "newMessage",
Arguments = new [] { message }
});
}
```


You can send a message only to connections that have been authenticated to a user by setting the *user ID* in the SignalR message.

Example function.json:

```
{
"type": "signalR",
"name": "signalRMessages",
"hubName": "<hub_name>",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "out"
}
```


Here's the C# script code:

```
#r "Microsoft.Azure.WebJobs.Extensions.SignalRService"
using Microsoft.Azure.WebJobs.Extensions.SignalRService;
public static Task Run(
object message,
IAsyncCollector<SignalRMessage> signalRMessages)
{
return signalRMessages.AddAsync(
new SignalRMessage
{
// the message will only be sent to this user ID
UserId = "userId1",
Target = "newMessage",
Arguments = new [] { message }
});
}
```


You can send a message only to connections that have been added to a group by setting the *group name* in the SignalR message.

Example function.json:

```
{
"type": "signalR",
"name": "signalRMessages",
"hubName": "<hub_name>",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "out"
}
```


Here's the C# Script code:

```
#r "Microsoft.Azure.WebJobs.Extensions.SignalRService"
using Microsoft.Azure.WebJobs.Extensions.SignalRService;
public static Task Run(
object message,
IAsyncCollector<SignalRMessage> signalRMessages)
{
return signalRMessages.AddAsync(
new SignalRMessage
{
// the message will be sent to the group with this name
GroupName = "myGroup",
Target = "newMessage",
Arguments = new [] { message }
});
}
```


SignalR Service allows users or connections to be added to groups. Messages can then be sent to a group. You can use the `SignalR`

output binding to manage groups.

The following example adds a user to a group.

Example *function.json*

```
{
"type": "signalR",
"name": "signalRGroupActions",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"hubName": "chat",
"direction": "out"
}
```


*Run.csx*

```
#r "Microsoft.Azure.WebJobs.Extensions.SignalRService"
using Microsoft.Azure.WebJobs.Extensions.SignalRService;
public static Task Run(
HttpRequest req,
ClaimsPrincipal claimsPrincipal,
IAsyncCollector<SignalRGroupAction> signalRGroupActions)
{
var userIdClaim = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier);
return signalRGroupActions.AddAsync(
new SignalRGroupAction
{
UserId = userIdClaim.Value,
GroupName = "myGroup",
Action = GroupAction.Add
});
}
```


The following example removes a user from a group.

Example *function.json*

```
{
"type": "signalR",
"name": "signalRGroupActions",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"hubName": "chat",
"direction": "out"
}
```


*Run.csx*

```
#r "Microsoft.Azure.WebJobs.Extensions.SignalRService"
using Microsoft.Azure.WebJobs.Extensions.SignalRService;
public static Task Run(
HttpRequest req,
ClaimsPrincipal claimsPrincipal,
IAsyncCollector<SignalRGroupAction> signalRGroupActions)
{
var userIdClaim = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier);
return signalRGroupActions.AddAsync(
new SignalRGroupAction
{
UserId = userIdClaim.Value,
GroupName = "myGroup",
Action = GroupAction.Remove
});
}
```


### Twilio output

The following example shows a Twilio output binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding. The function uses an `out`

parameter to send a text message.

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


Here's C# script code:

```
#r "Newtonsoft.Json"
#r "Twilio"
#r "Microsoft.Azure.WebJobs.Extensions.Twilio"
using System;
using Microsoft.Extensions.Logging;
using Newtonsoft.Json;
using Microsoft.Azure.WebJobs.Extensions.Twilio;
using Twilio.Rest.Api.V2010.Account;
using Twilio.Types;
public static void Run(string myQueueItem, out CreateMessageOptions message, ILogger log)
{
log.LogInformation($"C# Queue trigger function processed: {myQueueItem}");
// In this example the queue item is a JSON string representing an order that contains the name of a
// customer and a mobile number to send text updates to.
dynamic order = JsonConvert.DeserializeObject(myQueueItem);
string msg = "Hello " + order.name + ", thank you for your order.";
// You must initialize the CreateMessageOptions variable with the "To" phone number.
message = new CreateMessageOptions(new PhoneNumber("+1704XXXXXXX"));
// A dynamic message can be set instead of the body in the output binding. In this example, we use
// the order information to personalize a text message.
message.Body = msg;
}
```


You can't use out parameters in asynchronous code. Here's an asynchronous C# script code example:

```
#r "Newtonsoft.Json"
#r "Twilio"
#r "Microsoft.Azure.WebJobs.Extensions.Twilio"
using System;
using Microsoft.Extensions.Logging;
using Newtonsoft.Json;
using Microsoft.Azure.WebJobs.Extensions.Twilio;
using Twilio.Rest.Api.V2010.Account;
using Twilio.Types;
public static async Task Run(string myQueueItem, IAsyncCollector<CreateMessageOptions> message, ILogger log)
{
log.LogInformation($"C# Queue trigger function processed: {myQueueItem}");
// In this example the queue item is a JSON string representing an order that contains the name of a
// customer and a mobile number to send text updates to.
dynamic order = JsonConvert.DeserializeObject(myQueueItem);
string msg = "Hello " + order.name + ", thank you for your order.";
// You must initialize the CreateMessageOptions variable with the "To" phone number.
CreateMessageOptions smsText = new CreateMessageOptions(new PhoneNumber("+1704XXXXXXX"));
// A dynamic message can be set instead of the body in the output binding. In this example, we use
// the order information to personalize a text message.
smsText.Body = msg;
await message.AddAsync(smsText);
}
```


### Warmup trigger

The following example shows a warmup trigger in a *function.json* file and a [C# script function](functions-reference-csharp) that runs on each new instance when it's added to your app.

Not supported for version 1.x of the Functions runtime.

Here's the *function.json* file:

```
{
"bindings": [
{
"type": "warmupTrigger",
"direction": "in",
"name": "warmupContext"
}
]
}
```


```
public static void Run(WarmupContext warmupContext, ILogger log)
{
log.LogInformation("Function App instance is warm.");
}
```

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-infrastructure-as-code -->

# Automate resource deployment for your function app in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can use a Bicep file or an Azure Resource Manager (ARM) template to automate the process of deploying your function app. During the deployment, you can use existing Azure resources or create new ones.

You can obtain these benefits in your production apps by using deployment automation, both infrastructure-as-code (IaC) and continuous integration and deployment (CI/CD):

**Consistency**: Define your infrastructure in code to ensure consistent deployments across environments.**Version Control**: Track changes to your infrastructure and application configurations in source control, along with your project code.**Automation**: Automate deployment, which reduces manual errors and shortens release process.**Scalability**: Easily replicate infrastructure for multiple environments, such as development, testing, and production.**Disaster Recovery**: Quickly recreate infrastructure after failures or during migrations.

This article shows you how to automate the creation of Azure resources and deployment configurations for Azure Functions. To learn more about continuous deployment of your project code, see [Continuous deployment for Azure Functions](functions-continuous-deployment).

The template code to create the required Azure resources depends on the desired hosting options for your function app. This article supports the following hosting options:

| Hosting option | Deployment type | Sample templates |
|---|---|---|
|

[Bicep](https://github.com/Azure/azure-quickstart-templates/blob/master/quickstarts/microsoft.web/function-app-flex-managed-identities/main.bicep)[ARM template](https://github.com/Azure/azure-quickstart-templates/blob/master/quickstarts/microsoft.web/function-app-flex-managed-identities/azuredeploy.json)[Terraform](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/tree/main/IaC/terraformazurerm)[Premium plan](functions-premium-plan)[Bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-premium-plan/main.bicep)[ARM template](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-premium-plan/azuredeploy.json)[Dedicated plan](dedicated-plan)[Bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-dedicated-plan/main.bicep)[ARM template](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-dedicated-plan/azuredeploy.json)[Azure Container Apps](../container-apps/functions-overview)[Bicep](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/ACAKindfunctionapp)[Consumption plan](consumption-plan)[Bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-windows-consumption/main.bicep)[ARM template](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-windows-consumption/azuredeploy.json)Make sure to select your hosting plan at the top of the article.

Important

After 30 September 2028, the option to host your function app on Linux in a Consumption plan is retired. To avoid disruptions, migrate your existing Consumption plan apps that run on Linux to the [Flex Consumption plan](flex-consumption-plan) before that date. Apps running on Windows in a Consumption plan aren't affected by this change.
For more information, see the [Linux Consumption plan retirement notice](https://go.microsoft.com/fwlink/?linkid=2335809).

When using this article, keep these considerations in mind:

There's no canonical way to structure an ARM template.

A Bicep deployment can be modularized into multiple Bicep files and

[Azure Verified Modules (AVMs)](https://azure.github.io/Azure-Verified-Modules/overview/introduction/).This article assumes that you have a basic understanding of

[creating Bicep files](../azure-resource-manager/bicep/file)or[authoring Azure Resource Manager templates](../azure-resource-manager/templates/syntax).

- Examples are shown as individual sections for specific resources. For a broad set of complete Bicep file and ARM template examples, see
[these function app deployment examples](/en-us/samples/browse/?expanded=azure&terms=%22azure%20functions%22&products=azure-resource-manager).

- Examples are shown as individual sections for specific resources. For Bicep,
[Azure Verified Modules (AVM)](https://azure.github.io/Azure-Verified-Modules/)are shown, when available. For a broad set of complete Bicep file and ARM template examples, see[these Flex Consumption app deployment examples](/en-us/samples/browse/?expanded=azure&terms=%22azure%20functions%20flex%22&products=azure-resource-manager).

- Examples are shown as individual sections for specific resources.

## Required resources

You must create or configure these resources for an Azure Functions-hosted deployment:

| Resource | Requirement | Syntax and properties reference |
|---|---|---|
| A
|

[Microsoft.Storage/storageAccounts](/en-us/azure/templates/microsoft.storage/storageaccounts)[Application Insights](#create-application-insights)component[Microsoft.Insights/components](/en-us/azure/templates/microsoft.insights/components)*[hosting plan](#create-the-hosting-plan)[Microsoft.Web/serverfarms](/en-us/azure/templates/microsoft.web/serverfarms)[function app](#create-the-function-app)[Microsoft.Web/sites](/en-us/azure/templates/microsoft.web/sites)You must create or configure these resources for an Azure Functions-hosted deployment:

| Resource | Requirement | Syntax and properties reference |
|---|---|---|
| A
|

[Microsoft.Storage/storageAccounts](/en-us/azure/templates/microsoft.storage/storageaccounts)[Application Insights](#create-application-insights)component[Microsoft.Insights/components](/en-us/azure/templates/microsoft.insights/components)*[function app](#create-the-function-app)[Microsoft.Web/sites](/en-us/azure/templates/microsoft.web/sites)An Azure Container Apps-hosted deployment typically consists of these resources:

| Resource | Requirement | Syntax and properties reference |
|---|---|---|
| A
|

[Microsoft.Storage/storageAccounts](/en-us/azure/templates/microsoft.storage/storageaccounts)[Application Insights](#create-application-insights)component[Microsoft.Insights/components](/en-us/azure/templates/microsoft.insights/components)*[managed environment](../container-apps/functions-overview#)[Microsoft.App/managedEnvironments](/en-us/azure/templates/microsoft.app/managedenvironments)[function app](#create-the-function-app)[Microsoft.Web/sites](/en-us/azure/templates/microsoft.web/sites)An Azure Arc-hosted deployment typically consists of these resources:

| Resource | Requirement | Syntax and properties reference |
|---|---|---|
| A
|

[Microsoft.Storage/storageAccounts](/en-us/azure/templates/microsoft.storage/storageaccounts)[Application Insights](#create-application-insights)component[Microsoft.Insights/components](/en-us/azure/templates/microsoft.insights/components)1[App Service Kubernetes environment](../app-service/overview-arc-integration#app-service-kubernetes-environment)[Microsoft.ExtendedLocation/customLocations](/en-us/azure/templates/microsoft.extendedlocation/customlocations)[function app](#create-the-function-app)[Microsoft.Web/sites](/en-us/azure/templates/microsoft.web/sites)*If you don't already have a Log Analytics Workspace that can be used by your Application Insights instance, you also need to create this resource.

When you deploy multiple resources in a single Bicep file or ARM template, the order in which resources are created is important. This requirement is a result of dependencies between resources. For such dependencies, make sure to use the `dependsOn`

element to define the dependency in the dependent resource. For more information, see either [Define the order for deploying resources in ARM templates](../azure-resource-manager/templates/resource-dependency) or [Resource dependencies in Bicep](../azure-resource-manager/bicep/resource-dependencies).

## Prerequisites

- The examples are designed to execute in the context of an existing resource group.
- Both Application Insights and storage logs require you to have an existing
[Azure Log Analytics workspace](/en-us/azure/azure-monitor/logs/log-analytics-overview). Workspaces can be shared between services, and as a rule of thumb you should create a workspace in each geographic region to improve performance. For an example of how to create a Log Analytics workspace, see[Create a Log Analytics workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace?tabs=azure-resource-manager#create-a-workspace). You can find the fully qualified workspace resource ID in a workspace page in the[Azure portal](https://portal.azure.com)under**Settings**>**Properties**>**Resource ID**.

- This article assumes that you have already created a
[managed environment](../container-apps/environment)in Azure Container Apps. You need both the name and the ID of the managed environment to create a function app hosted on Container Apps.

- This article assumes that you have already created an
[App Service-enabled custom location](../app-service/overview-arc-integration)on an[Azure Arc-enabled Kubernetes cluster](/en-us/azure/azure-arc/kubernetes/overview). You need both the custom location ID and the Kubernetes environment ID to create a function app hosted in an Azure Arc custom location.

## Create storage account

All function apps require an Azure storage account. You need a general purpose account that supports blobs, tables, queues, and files. For more information, see [Azure Functions storage account requirements](storage-considerations#storage-account-requirements).

Important

The storage account is used to store important app data, sometimes including the application code itself. You should limit access from other apps and users to the storage account.

This example section creates a Standard general purpose v2 storage account:

```
resource storageAccount 'Microsoft.Storage/storageAccounts@2023-05-01' = {
name: storageAccountName
location: location
kind: 'StorageV2'
sku: {
name: 'Standard_LRS'
}
properties: {
supportsHttpsTrafficOnly: true
defaultToOAuthAuthentication: true
allowBlobPublicAccess: false
}
}
```


For more context, see the complete [main.bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-linux-consumption/main.bicep#L37) file in the templates repository.

For more context, see the complete [storage-PrivateEndpoint.bicep](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd/blob/main/infra/app/storage-PrivateEndpoint.bicep) file in the sample repository.

You need to set the connection string of this storage account as the `AzureWebJobsStorage`

app setting, which Functions requires. The templates in this article construct this connection string value based on the created storage account, which is a best practice. For more information, see [Application configuration](#application-configuration).

### Deployment container

Deployments to an app running in the Flex Consumption plan require a container in Azure Blob Storage as the deployment source. You can use either the default storage account or you can specify a separate storage account. For more information, see [Configure deployment settings](flex-consumption-how-to#configure-deployment-settings).

This deployment account must already be configured when you create your app, including the specific container used for deployments. To learn more about configuring deployments, see [Deployment sources](#deployment-sources).

This example shows how to create a container in the storage account:

```
}
// Azure Functions Flex Consumption
module functionApp 'br/public:avm/res/web/site:0.16.0' = {
name: 'functionapp'
scope: rg
params: {
kind: 'functionapp,linux'
name: functionAppName_resolved
location: location
tags: union(tags, { 'azd-service-name': 'api' })
serverFarmResourceId: appServicePlan.outputs.resourceId
managedIdentities: {
systemAssigned: true
}
functionAppConfig: {
deployment: {
storage: {
type: 'blobContainer'
value: '${storage.outputs.primaryBlobEndpoint}${deploymentStorageContainerName}'
authentication: {
type: 'SystemAssignedIdentity'
}
```


This example shows how to use the [AVM for storage accounts](https://github.com/Azure/bicep-registry-modules/tree/main/avm/res/storage/storage-account) to create the blob storage container along with the storage account. For the snippet in context, see [this deployment example](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/IaC/bicep/main.bicep#L133).

Other deployment settings are [configured with the app itself](#deployment-sources).

### Enable storage logs

Because the storage account is used for important function app data, you should monitor the account for modification of that content. To monitor your storage account, you need to configure Azure Monitor resource logs for Azure Storage. In this example section, a Log Analytics workspace named `myLogAnalytics`

is used as the destination for these logs.

```
resource blobService 'Microsoft.Storage/storageAccounts/blobServices@2021-09-01' existing = {
name:'default'
parent:storageAccountName
}
resource storageDataPlaneLogs 'Microsoft.Insights/diagnosticSettings@2021-05-01-preview' = {
name: '${storageAccountName}-logs'
scope: blobService
properties: {
workspaceId: myLogAnalytics.id
logs: [
{
category: 'StorageWrite'
enabled: true
}
]
metrics: [
{
category: 'Transaction'
enabled: true
}
]
}
}
```


This same workspace can be used for the Application Insights resource defined later. For more information, including how to work with these logs, see [Monitoring Azure Storage](../storage/blobs/monitor-blob-storage).

## Create Application Insights

You should be using Application Insights for monitoring your function app executions. Application Insights now requires an Azure Log Analytics workspace, which can be shared. These examples assume you're using an existing workspace and have the fully qualified resource ID for the workspace. For more information, see [Azure Log Analytics workspace](/en-us/azure/azure-monitor/logs/log-analytics-overview).

In this example section, the Application Insights resource is defined with the type `Microsoft.Insights/components`

and the kind `web`

:

```
resource applicationInsight 'Microsoft.Insights/components@2020-02-02' = {
name: applicationInsightsName
location: appInsightsLocation
tags: tags
kind: 'web'
properties: {
Application_Type: 'web'
WorkspaceResourceId: '<FULLY_QUALIFIED_RESOURCE_ID>'
}
}
```


For more context, see the complete [main.bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-linux-consumption/main.bicep#L60) file in the templates repository.

The connection must be provided to the function app using the [ APPLICATIONINSIGHTS_CONNECTION_STRING](functions-app-settings#applicationinsights_connection_string) application setting. For more information, see

[Application configuration](#application-configuration).

The examples in this article obtain the connection string value for the created instance. Older versions might instead use [ APPINSIGHTS_INSTRUMENTATIONKEY](functions-app-settings#appinsights_instrumentationkey) to set the instrumentation key, which is no longer recommended.

## Create the hosting plan

Apps hosted in an Azure Functions [Flex Consumption plan](flex-consumption-plan), [Premium plan](functions-premium-plan), or [Dedicated (App Service) plan](dedicated-plan) must have the hosting plan explicitly defined.

Flex Consumption is a Linux-based hosting plan that builds on the Consumption *pay for what you use* serverless billing model. The plan features support for private networking, instance memory size selection, and improved managed identity support.

A Flex Consumption plan is a special type of `serverfarm`

resource. You can specify it by using `FC1`

for the `Name`

property value in the `sku`

property with a `tier`

value of `FlexConsumption`

.

This example section creates a Flex Consumption plan:

```
scaleAndConcurrency: {
maximumInstanceCount: maximumInstanceCount
instanceMemoryMB: instanceMemoryMB
}
runtime: {
name: functionAppRuntime
version: functionAppRuntimeVersion
}
}
siteConfig: {
alwaysOn: false
}
configs: [{
name: 'appsettings'
properties:{
```


This example uses the [AVM for App Service plans](https://github.com/Azure/bicep-registry-modules/tree/main/avm/res/web/serverfarm). For the snippet in context, see [this deployment example](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/IaC/bicep/main.bicep#L156).

Because the Flex Consumption plan currently only supports Linux, you must also set the `reserved`

property to `true`

.

The Premium plan offers the same scaling as the Consumption plan but includes dedicated resources and extra capabilities. To learn more, see [Azure Functions Premium Plan](functions-premium-plan).

A Premium plan is a special type of `serverfarm`

resource. You can specify it by using either `EP1`

, `EP2`

, or `EP3`

for the `Name`

property value in the `sku`

property. The way that you define the Functions hosting plan depends on whether your function app runs on Windows or on Linux. This example section creates an `EP1`

plan:

```
resource hostingPlan 'Microsoft.Web/serverfarms@2022-03-01' = {
name: hostingPlanName
location: location
sku: {
name: 'EP1'
tier: 'ElasticPremium'
family: 'EP'
}
kind: 'elastic'
properties: {
maximumElasticWorkerCount: 20
}
}
```


For more context, see the complete [main.bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-premium-plan/main.bicep#L62) file in the templates repository.

For more information about the `sku`

object, see [ SkuDefinition](/en-us/azure/templates/microsoft.web/serverfarms#skudescription) or review the example templates.

In the Dedicated (App Service) plan, your function app runs on dedicated VMs on Basic, Standard, and Premium SKUs in App Service plans, similar to web apps. For more information, see [Dedicated plan](dedicated-plan).

For a sample Bicep file/Azure Resource Manager template, see [Function app on Azure App Service plan](https://azure.microsoft.com/resources/templates/function-app-create-dedicated/).

In Functions, the Dedicated plan is just a regular App Service plan, which is defined by a `serverfarm`

resource. You must provide at least the `name`

value. For a list of supported plan names, see the `--sku`

setting in [ az appservice plan create](/en-us/cli/azure/appservice/plan#az-appservice-plan-create) for the current list of supported values for a Dedicated plan.

The way that you define the hosting plan depends on whether your function app runs on Windows or on Linux:

```
resource hostingPlanName 'Microsoft.Web/serverfarms@2022-03-01' = {
name: hostingPlanName
location: location
sku: {
tier: 'Standard'
name: 'S1'
size: 'S1'
family: 'S'
capacity: 1
}
}
```


For more context, see the complete [main.bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-dedicated-plan/main.bicep#L62) file in the templates repository.

## Create the hosting plan

You don't need to explicitly define a Consumption hosting plan resource. When you skip this resource definition, a plan is automatically either created or selected on a per-region basis when you create the function app resource itself.

You can explicitly define a Consumption plan as a special type of `serverfarm`

resource, which you specify using the value `Dynamic`

for the `computeMode`

and `sku`

properties. This example section shows you how to explicitly define a consumption plan. The way that you define a hosting plan depends on whether your function app runs on Windows or on Linux.

```
resource hostingPlan 'Microsoft.Web/serverfarms@2022-03-01' = {
name: hostingPlanName
location: location
sku: {
name: 'Y1'
tier: 'Dynamic'
size: 'Y1'
family: 'Y'
capacity: 0
}
properties: {
computeMode: 'Dynamic'
}
}
```


For more context, see the complete [main.bicep](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-windows-consumption/main.bicep#L40) file in the templates repository.

## Kubernetes environment

Azure Functions can be deployed to [Azure Arc-enabled Kubernetes](../app-service/overview-arc-integration) either as a code project or a containerized function app.

To create the app and plan resources, you must have already [created an App Service Kubernetes environment](../app-service/manage-create-arc-environment) for an Azure Arc-enabled Kubernetes cluster. The examples in this article assume you have the resource ID of the custom location (`customLocationId`

) and App Service Kubernetes environment (`kubeEnvironmentId`

) to which you're deploying, which are set in this example:

```
param kubeEnvironmentId string
param customLocationId string
```


Both sites and plans must reference the custom location through an `extendedLocation`

field. As shown in this truncated example, `extendedLocation`

sits outside of `properties`

, as a peer to `kind`

and `location`

:

```
resource hostingPlan 'Microsoft.Web/serverfarms@2022-03-01' = {
...
{
extendedLocation: {
name: customLocationId
}
}
}
```


The plan resource should use the Kubernetes (`K1`

) value for `SKU`

, the `kind`

field should be `linux,kubernetes`

, and the `reserved`

property should be `true`

, since it's a Linux deployment. You must also set the `extendedLocation`

and `kubeEnvironmentProfile.id`

to the custom location ID and the Kubernetes environment ID, respectively, which might look like this example section:

```
resource hostingPlan 'Microsoft.Web/serverfarms@2022-03-01' = {
name: hostingPlanName
location: location
kind: 'linux,kubernetes'
sku: {
name: 'K1'
tier: 'Kubernetes'
}
extendedLocation: {
name: customLocationId
}
properties: {
kubeEnvironmentProfile: {
id: kubeEnvironmentId
}
reserved: true
}
}
```


## Create the function app

The function app resource is defined by a resource of type `Microsoft.Web/sites`

and `kind`

that includes `functionapp`

, at a minimum.

The way that you define a function app resource depends on whether you're hosting on Linux or on Windows:

For a list of application settings required when running on Windows, see [Application configuration](#application-configuration). For a sample Bicep file/Azure Resource Manager template, see the [function app hosted on Windows in a Consumption plan](https://github.com/Azure-Samples/function-app-arm-templates/tree/main/function-app-windows-consumption) template.

For a list of application settings required when running on Windows, see [Application configuration](#application-configuration).

Flex Consumption replaces many of the standard application settings and site configuration properties used in Bicep and ARM template deployments. For more information, see [Application configuration](#application-configuration).

```
AzureWebJobsStorage__blobServiceUri: 'https://${storage.outputs.name}.blob.${environment().suffixes.storage}'
AzureWebJobsStorage__queueServiceUri: 'https://${storage.outputs.name}.queue.${environment().suffixes.storage}'
AzureWebJobsStorage__tableServiceUri: 'https://${storage.outputs.name}.table.${environment().suffixes.storage}'
// Application Insights settings are always included
APPLICATIONINSIGHTS_CONNECTION_STRING: applicationInsights.outputs.connectionString
APPLICATIONINSIGHTS_AUTHENTICATION_STRING: 'Authorization=AAD'
}
}]
}
}
// Consolidated Role Assignments
module rbacAssignments 'rbac.bicep' = {
name: 'rbacAssignments'
scope: rg
params: {
storageAccountName: storage.outputs.name
appInsightsName: applicationInsights.outputs.name
managedIdentityPrincipalId: functionApp.outputs.?systemAssignedMIPrincipalId ?? ''
userIdentityPrincipalId: principalId
allowUserIdentityPrincipal: !empty(principalId)
}
}
// Outputs
output AZURE_LOCATION string = location
output AZURE_TENANT_ID string = tenant().tenantId
output AZURE_FUNCTION_NAME string = functionApp.outputs.name
output APPLICATIONINSIGHTS_CONNECTION_STRING string = applicationInsights.outputs.connectionString
```


This example uses the [AVM for function apps](https://github.com/Azure/bicep-registry-modules/tree/main/avm/res/web/serverfarm). For the snippet in context, see [this deployment example](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/IaC/bicep/main.bicep#L173).

Note

If you choose to optionally define your Consumption plan, you must set the `serverFarmId`

property on the app so that it points to the resource ID of the plan. Make sure that the function app has a `dependsOn`

setting that also references the plan. If you didn't explicitly define a plan, one gets created for you.

Set the `serverFarmId`

property on the app so that it points to the resource ID of the plan. Make sure that the function app has a `dependsOn`

setting that also references the plan.

```
resource functionAppName_resource 'Microsoft.Web/sites@2022-03-01' = {
name: functionAppName
location: location
kind: 'functionapp'
properties: {
serverFarmId: hostingPlanName.id
siteConfig: {
appSettings: [
{
name: 'APPLICATIONINSIGHTS_CONNECTION_STRING'
value: applicationInsightsName.properties.ConnectionString
}
{
name: 'AzureWebJobsStorage'
value: 'DefaultEndpointsProtocol=https;AccountName=${storageAccountName};EndpointSuffix=${environment().suffixes.storage};AccountKey=${storageAccount.listKeys().keys[0].value}'
}
{
name: 'WEBSITE_CONTENTAZUREFILECONNECTIONSTRING'
value: 'DefaultEndpointsProtocol=https;AccountName=${storageAccountName};EndpointSuffix=${environment().suffixes.storage};AccountKey=${storageAccount.listKeys().keys[0].value}'
}
{
name: 'WEBSITE_CONTENTSHARE'
value: toLower(functionAppName)
}
{
name: 'FUNCTIONS_EXTENSION_VERSION'
value: '~4'
}
{
name: 'FUNCTIONS_WORKER_RUNTIME'
value: 'node'
}
{
name: 'WEBSITE_NODE_DEFAULT_VERSION'
value: '~14'
}
]
}
}
}
```


For a complete end-to-end example, see this [main.bicep file](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-windows-consumption/main.bicep).

```
resource functionApp 'Microsoft.Web/sites@2022-03-01' = {
name: functionAppName
location: location
kind: 'functionapp'
properties: {
serverFarmId: hostingPlan.id
siteConfig: {
alwaysOn: true
appSettings: [
{
name: 'APPLICATIONINSIGHTS_CONNECTION_STRING'
value: applicationInsightsName.properties.ConnectionString
}
{
name: 'AzureWebJobsStorage'
value: 'DefaultEndpointsProtocol=https;AccountName=${storageAccountName};EndpointSuffix=${environment().suffixes.storage};AccountKey=${storageAccount.listKeys().keys[0].value}'
}
{
name: 'FUNCTIONS_EXTENSION_VERSION'
value: '~4'
}
{
name: 'FUNCTIONS_WORKER_RUNTIME'
value: 'node'
}
{
name: 'WEBSITE_NODE_DEFAULT_VERSION'
value: '~14'
}
]
}
}
}
```


For a complete end-to-end example, see this [main.bicep file](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-dedicated-plan/main.bicep).

## Deployment sources

You can use the [ linuxFxVersion](functions-app-settings#linuxfxversion) site setting to request that a specific Linux container be deployed to your app when it's created. More settings are required to access images in a private repository. For more information, see

[Application configuration](#application-configuration).

Important

When you create your own containers, you're required to keep the base image of your container updated to the latest supported base image. Supported base images for Azure Functions are language-specific. See the [Azure Functions base image repos](https://mcr.microsoft.com/catalog?search=functions).

The Functions team is committed to publishing monthly updates for these base images. Regular updates include the latest minor version updates and security fixes for both the Functions runtime and languages. You should regularly update your container from the latest base image and redeploy the updated version of your container. For more information, see [Maintaining custom containers](container-concepts#maintaining-custom-containers).

Your Bicep file or ARM template can optionally also define a deployment for your function code, which could include these methods:

The Flex Consumption plan maintains your project code in zip-compressed package file in a blob storage container known as the *deployment container*. You can configure both the storage account and container used for deployment. For more information, see [Deployment](flex-consumption-plan#deployment).

You must use * one deploy* to publish your code package to the deployment container. During an ARM template or Bicep deployment, you can do this by

[defining a package source](#deployment-package)that uses the

`/onedeploy`

extension. If you choose to instead directly upload your package to the container, the package doesn't get automatically deployed.### Deployment container

The specific storage account and container used for deployments, the authentication method, and credentials are set in the `functionAppConfig.deployment.storage`

element of the `properties`

for the site. The container and any application settings must exist when the app is created. For an example of how to create the storage container, see [Deployment container](#deployment-container).

This example uses a system assigned managed identity to access the specified blob storage container, which is created elsewhere in the deployment:

```
// Consolidated Role Assignments
module rbacAssignments 'rbac.bicep' = {
name: 'rbacAssignments'
scope: rg
params: {
storageAccountName: storage.outputs.name
appInsightsName: applicationInsights.outputs.name
managedIdentityPrincipalId: functionApp.outputs.?systemAssignedMIPrincipalId ?? ''
userIdentityPrincipalId: principalId
allowUserIdentityPrincipal: !empty(principalId)
}
}
// Outputs
output AZURE_LOCATION string = location
output AZURE_TENANT_ID string = tenant().tenantId
output AZURE_FUNCTION_NAME string = functionApp.outputs.name
output APPLICATIONINSIGHTS_CONNECTION_STRING string = applicationInsights.outputs.connectionString
```


This example uses the [AVM for function apps](https://github.com/Azure/bicep-registry-modules/tree/main/avm/res/web/site). For the snippet in context, see [this deployment example](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/IaC/bicep/main.bicep#L185).

When using managed identities, you must also enable the function app to access the storage account using the identity, as shown in this example:

```
module storageRoleAssignment_User 'br/public:avm/ptn/authorization/resource-role-assignment:0.1.2' = if (allowUserIdentityPrincipal && !empty(userIdentityPrincipalId)) {
name: 'storageRoleAssignment-User-${uniqueString(storageAccount.id, userIdentityPrincipalId)}'
params: {
resourceId: storageAccount.id
roleDefinitionId: roleDefinitions.storageBlobDataOwner
principalId: userIdentityPrincipalId
principalType: 'User'
description: 'Storage Blob Data Owner role for user identity (development/testing)'
roleName: 'Storage Blob Data Owner'
}
}
```


This example uses the [AVM for resource-scoped role assignment](https://github.com/Azure/bicep-registry-modules/tree/main/avm/ptn/authorization/resource-role-assignment). For the snippet in context, see [this deployment example](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/IaC/bicep/rbac.bicep#L45).

This example requires you to know the GUID value for the role being assigned. You can get this ID value for any friendly role name by using the [az role definition list](/en-us/cli/azure/role/definition#az-role-definition-list) command, as in this example:

```
az role definition list --output tsv --query "[?roleName=='Storage Blob Data Owner'].{name:name}"
```


When using a connection string instead of managed identities, you need to instead set the `authentication.type`

to `StorageAccountConnectionString`

and set `authentication.storageAccountConnectionStringName`

to the name of the application setting that contains the deployment storage account connection string.

### Deployment package

The Flex Consumption plan uses *one deploy* for deploying your code project. The code package itself is the same as you would use for zip deployment in other Functions hosting plans. However, the name of the package file itself must be `released-package.zip`

.

To include a one deploy package in your template, use the `/onedeploy`

resource definition for the remote URL that contains the deployment package. The Functions host must be able to access both this remote package source and the deployment container.

This example adds a one deploy source to an existing app:

```
@description('The name of the function app.')
param functionAppName string
@description('The location into which the resources should be deployed.')
param location string = resourceGroup().location
@description('The zip content URL for released-package.zip.')
param packageUri string
resource functionAppName_OneDeploy 'Microsoft.Web/sites/extensions@2022-09-01' = {
name: '${functionAppName}/onedeploy'
location: location
properties: {
packageUri: packageUri
remoteBuild: false
}
}
```


Your Bicep file or ARM template can optionally also define a deployment for your function code using a [zip deployment package](deployment-zip-push).

To successfully deploy your application by using Azure Resource Manager, it's important to understand how resources are deployed in Azure. In most examples, top-level configurations are applied by using `siteConfig`

. It's important to set these configurations at a top level, because they convey information to the Functions runtime and deployment engine. Top-level information is required before the child `sourcecontrols/web`

resource is applied. Although it's possible to configure these settings in the child-level `config/appSettings`

resource, in some cases your function app must be deployed *before* `config/appSettings`

is applied.

## Zip deployment package

Zip deployment is a recommended way to deploy your function app code. By default, functions that use zip deployment run in the deployment package itself. For more information, including the requirements for a deployment package, see [Zip deployment for Azure Functions](deployment-zip-push). When using resource deployment automation, you can reference the .zip deployment package in your Bicep or ARM template.

To use zip deployment in your template, set the `WEBSITE_RUN_FROM_PACKAGE`

setting in the app to `1`

and include the `/zipDeploy`

resource definition.

For a Consumption plan on Linux, instead set the URI of the deployment package directly in the `WEBSITE_RUN_FROM_PACKAGE`

setting, as shown in [this example template](https://github.com/Azure-Samples/function-app-arm-templates/tree/main/function-app-linux-consumption#L152).

This example adds a zip deployment source to an existing app:

```
@description('The name of the function app.')
param functionAppName string
@description('The location into which the resources should be deployed.')
param location string = resourceGroup().location
@description('The zip content url.')
param packageUri string
resource functionAppName_ZipDeploy 'Microsoft.Web/sites/extensions@2021-02-01' = {
name: '${functionAppName}/ZipDeploy'
location: location
properties: {
packageUri: packageUri
}
}
```


Keep the following things in mind when including zip deployment resources in your template:

- Consumption plans on Linux don't support
`WEBSITE_RUN_FROM_PACKAGE = 1`

. You must instead set the URI of the deployment package directly in the`WEBSITE_RUN_FROM_PACKAGE`

setting. For more information, see[WEBSITE_RUN_FROM_PACKAGE](functions-app-settings#website_run_from_package). For an example template, see[Function app hosted on Linux in a Consumption plan](https://github.com/Azure-Samples/function-app-arm-templates/tree/main/function-app-linux-consumption).

The

`packageUri`

must be a location that can be accessed by Functions. Consider using Azure blob storage with a shared access signature (SAS). After the SAS expires, Functions can no longer access the share for deployments. When you regenerate your SAS, remember to update the`WEBSITE_RUN_FROM_PACKAGE`

setting with the new URI value.When setting

`WEBSITE_RUN_FROM_PACKAGE`

to a URI, you must[manually sync triggers](functions-deployment-technologies#trigger-syncing).Make sure to always set all required application settings in the

`appSettings`

collection when adding or updating settings. Existing settings not explicitly set are removed by the update. For more information, see[Application configuration](#application-configuration).Functions doesn't support Web Deploy (

`msdeploy`

) for package deployments. You must instead use zip deployment in your deployment pipelines and automation. For more information, see[Zip deployment for Azure Functions](deployment-zip-push).

## Remote builds

The deployment process assumes that the .zip file that you use or a zip deployment contains a ready-to-run app. This means that by default no customizations are run.

There are scenarios that require you to rebuild your app remotely. One such example is when you need to include Linux-specific packages in Python or Node.js apps that you developed on a Windows computer. In this case, you can configure Functions to perform a remote build on your code after the zip deployment.

The way that you request a remote build depends on the operating system to which you're deploying:

When an app is deployed to Windows, language-specific commands (like `dotnet restore`

for C# apps or `npm install`

for Node.js apps) are run.

To enable the same build processes that you get with continuous integration, add `SCM_DO_BUILD_DURING_DEPLOYMENT=true`

to your application settings in your deployment code and remove the `WEBSITE_RUN_FROM_PACKAGE`

entirely.

## Linux containers

If you're deploying a [containerized function app](functions-how-to-custom-container) to an Azure Functions Premium or Dedicated plan, you must:

- Set the
site setting with the identifier of your container image.`linuxFxVersion`

- Set any required
settings when obtaining the container from a private registry.`DOCKER_REGISTRY_SERVER_*`

- Set
application setting to`WEBSITES_ENABLE_APP_SERVICE_STORAGE`

`false`

.

If some settings are missing, the application provisioning might fail with this HTTP/500 error:


`Function app provisioning failed.`


For more information, see [Application configuration](#application-configuration).

```
resource functionApp 'Microsoft.Web/sites@2022-03-01' = {
name: functionAppName
location: location
kind: 'functionapp'
properties: {
serverFarmId: hostingPlan.id
siteConfig: {
appSettings: [
{
name: 'AzureWebJobsStorage'
value: 'DefaultEndpointsProtocol=https;AccountName=${storageAccountName};AccountKey=${storageAccount.listKeys().keys[0].value}'
}
{
name: 'FUNCTIONS_WORKER_RUNTIME'
value: 'node'
}
{
name: 'WEBSITE_NODE_DEFAULT_VERSION'
value: '~14'
}
{
name: 'FUNCTIONS_EXTENSION_VERSION'
value: '~4'
}
{
name: 'DOCKER_REGISTRY_SERVER_URL'
value: dockerRegistryUrl
}
{
name: 'DOCKER_REGISTRY_SERVER_USERNAME'
value: dockerRegistryUsername
}
{
name: 'DOCKER_REGISTRY_SERVER_PASSWORD'
value: dockerRegistryPassword
}
{
name: 'WEBSITES_ENABLE_APP_SERVICE_STORAGE'
value: 'false'
}
]
linuxFxVersion: 'DOCKER|myacr.azurecr.io/myimage:mytag'
}
}
dependsOn: [
storageAccount
]
}
```


When deploying [containerized functions to Azure Container Apps](../container-apps/functions-overview), your template must:

- Set the
`kind`

field to a value of`functionapp,linux,container,azurecontainerapps`

. - Set the
`managedEnvironmentId`

site property to the fully qualified URI of the Container Apps environment. - Add a resource link in the site's
`dependsOn`

collection when creating a`Microsoft.App/managedEnvironments`

resource at the same time as the site.

The definition of a containerized function app deployed from a private container registry to an existing Container Apps environment might look like this example:

```
resource functionApp 'Microsoft.Web/sites@2022-03-01' = {
name: functionAppName
kind: 'functionapp,linux,container,azurecontainerapps'
location: location
properties: {
serverFarmId: hostingPlanName
siteConfig: {
linuxFxVersion: 'DOCKER|myacr.azurecr.io/myimage:mytag'
appSettings: [
{
name: 'FUNCTIONS_EXTENSION_VERSION'
value: '~4'
}
{
name: 'AzureWebJobsStorage'
value: 'DefaultEndpointsProtocol=https;AccountName=${storageAccountName};AccountKey=${storageAccount.listKeys().keys[0].value}'
}
{
name: 'APPLICATIONINSIGHTS_CONNECTION_STRING'
value: applicationInsightsName.properties.ConnectionString
}
]
}
managedEnvironmentId: managedEnvironmentId
}
dependsOn: [
storageAccount
hostingPlan
]
}
```


When deploying functions to Azure Arc, the value you set for the `kind`

field of the function app resource depends on the type of deployment:

| Deployment type | `kind` field value |
|---|---|
| Code-only deployment | `functionapp,linux,kubernetes` |
| Container deployment | `functionapp,linux,kubernetes,container` |

You must also set the `customLocationId`

as you did for the [hosting plan resource](#create-the-hosting-plan).

The definition of a containerized function app, using a .NET 6 quickstart image, might look like this example:

```
resource functionApp 'Microsoft.Web/sites@2022-03-01' = {
name: functionAppName
kind: 'kubernetes,functionapp,linux,container'
location: location
extendedLocation: {
name: customLocationId
}
properties: {
serverFarmId: hostingPlanName
siteConfig: {
linuxFxVersion: 'DOCKER|mcr.microsoft.com/azure-functions/4-dotnet-isolated6.0-appservice-quickstart'
appSettings: [
{
name: 'FUNCTIONS_EXTENSION_VERSION'
value: '~4'
}
{
name: 'AzureWebJobsStorage'
value: 'DefaultEndpointsProtocol=https;AccountName=${storageAccountName};AccountKey=${storageAccount.listKeys().keys[0].value}'
}
{
name: 'APPLICATIONINSIGHTS_CONNECTION_STRING'
value: applicationInsightsName.properties.ConnectionString
}
]
alwaysOn: true
}
}
dependsOn: [
storageAccount
hostingPlan
]
}
```


## Application configuration

In a Flex Consumption plan, you configure your function app in Azure with two types of properties:

| Configuration | `Microsoft.Web/sites` property |
|---|---|
| Application configuration | `functionAppConfig` |
| Application settings | `siteConfig.appSettings` collection |

These application configurations are maintained in `functionAppConfig`

:

| Behavior | Setting in `functionAppConfig` |
|---|---|
|

`scaleAndConcurrency.alwaysReady`

[Deployment source](#deployment-sources)`deployment`

[Instance size](flex-consumption-plan#instance-sizes)`scaleAndConcurrency.instanceMemoryMB`

[HTTP trigger concurrency](functions-concurrency#http-trigger-concurrency)`scaleAndConcurrency.triggers.http.perInstanceConcurrency`

[Language runtime](functions-app-settings#functions_worker_runtime)`runtime.name`

[Language version](supported-languages)`runtime.version`

[Maximum instance count](event-driven-scaling#flex-consumption-plan)`scaleAndConcurrency.maximumInstanceCount`

[Site update strategy](flex-consumption-site-updates)`siteUpdateStrategy.type`

The Flex Consumption plan also supports these application settings:

- Connection string-based settings:
- Managed identity-based settings:

Functions provides the following options for configuring your function app in Azure:

| Configuration | `Microsoft.Web/sites` property |
|---|---|
| Site settings | `siteConfig` |
| Application settings | `siteConfig.appSettings` collection |

These site settings are required on the `siteConfig`

property:

These site settings are required only when using managed identities to obtain the image from an Azure Container Registry instance:

These application settings are required (or recommended) for a specific operating system and hosting option:

These application settings are required for container deployments:

These settings are only required when deploying from a private container registry:

Keep these considerations in mind when working with site and application settings using Bicep files or ARM templates:

- The optional
`alwaysReady`

setting contains an array of one or more`{name,instanceCount}`

objects, with one for each[per-function scale group](flex-consumption-plan#per-function-scaling). These are the scale groups being used to make always-ready scale decisions. This example sets always-ready counts for both the`http`

group and a single function named`helloworld`

, which is of a nongrouped trigger type:`alwaysReady: [ { name: 'http' instanceCount: 2 } { name: 'function:helloworld' instanceCount: 1 } ]`


- There are important considerations for when you should set
`WEBSITE_CONTENTSHARE`

in an automated deployment. For detailed guidance, see thereference.`WEBSITE_CONTENTSHARE`


- For container deployments, also set
to`WEBSITES_ENABLE_APP_SERVICE_STORAGE`

`false`

, since your app content is provided in the container itself.

You should always define your application settings as a

`siteConfig/appSettings`

collection of the`Microsoft.Web/sites`

resource being created, as is done in the examples in this article. This definition guarantees the settings your function app needs to run are available on initial startup.When adding or updating application settings using templates, make sure that you include all existing settings with the update. You must do this because the underlying update REST API calls replace the entire

`/config/appsettings`

resource. If you remove the existing settings, your function app won't run. To programmatically update individual application settings, you can instead use the Azure CLI, Azure PowerShell, or the Azure portal to make these changes. For more information, see[Work with application settings](functions-how-to-use-azure-function-app-settings#settings).When possible, you should use managed identity-based connections to other Azure services, including the

`AzureWebJobsStorage`

connection. For more information, see[Configure an identity-based connection](functions-reference#configure-an-identity-based-connection).

## Slot deployments

Functions lets you deploy different versions of your code to unique endpoints in your function app. This option makes it easier to develop, validate, and deploy functions updates without impacting functions running in production. Deployment slots is a feature of Azure App Service. The number of slots available [depends on your hosting plan](functions-scale#service-limits). For more information, see [Azure Functions deployment slots](functions-deployment-slots) functions.

A slot resource is defined in the same way as a function app resource (`Microsoft.Web/sites`

), but instead you use the `Microsoft.Web/sites/slots`

resource identifier. For an example deployment (in both Bicep and ARM templates) that creates both a production and a staging slot in a Premium plan, see [Azure Function App with a Deployment Slot](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-deployment-slot).

To learn about how to swap slots by using templates, see [Automate with Resource Manager templates](../app-service/deploy-staging-slots#automate-with-resource-manager-templates).

Keep the following considerations in mind when working with slot deployments:

Don't explicitly set the

`WEBSITE_CONTENTSHARE`

setting in the deployment slot definition. This setting is generated for you when the app is created in the deployment slot.When you swap slots, some application settings are considered "sticky," in that they stay with the slot and not with the code being swapped. You can define such a

*slot setting*by including`"slotSetting":true`

in the specific application setting definition in your template. For more information, see[Manage settings](functions-deployment-slots#manage-settings).

## Secured deployments

You can create your function app in a deployment where one or more of the resources have been secured by integrating with virtual networks. Virtual network integration for your function app is defined by a `Microsoft.Web/sites/networkConfig`

resource. This integration depends on both the referenced function app and virtual network resources. Your function app might also depend on other private networking resources, such as private endpoints and routes. For more information, see [Azure Functions networking options](functions-networking-options).

These projects provide Bicep-based examples of how to deploy your function apps in a virtual network, including with network access restrictions:

[High-scale HTTP triggered function connects to an event hub secured by a virtual network](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/README.md): An HTTP triggered function (.NET isolated worker mode) accepts calls from any source and then sends the body of those HTTP calls to a secure event hub running in a virtual network by using virtual network integration.[Function is triggered by a Service Bus queue secured in a virtual network](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/README.md): A Python function is triggered by a Service Bus queue secured in a virtual network. The queue is accessed in the virtual network using private endpoint. A virtual machine in the virtual network is used to send messages.

When creating a deployment that uses a secured storage account, you must both explicitly set the `WEBSITE_CONTENTSHARE`

setting and create the file share resource named in this setting. Make sure you create a `Microsoft.Storage/storageAccounts/fileServices/shares`

resource using the value of `WEBSITE_CONTENTSHARE`

, as shown in this example ([ARM template](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-private-endpoints-storage-private-endpoints/azuredeploy.json#L467)|[Bicep file](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-private-endpoints-storage-private-endpoints/main.bicep#L351)). You'll also need to set the site property `vnetContentShareEnabled`

to true.

Note

When these settings aren't part of a deployment that uses a secured storage account, you see this error during deployment validation: `Could not access storage account using provided connection string`

.

These projects provide both Bicep and ARM template examples of how to deploy your function apps in a virtual network, including with network access restrictions:

| Restricted scenario | Description |
|---|---|
|

[Virtual network integration](functions-networking-options#virtual-network-integration).[Create a function app that accesses a secured storage account](https://github.com/Azure-Samples/function-app-arm-templates/blob/main/function-app-storage-private-endpoints)[Restrict your storage account to a virtual network](configure-networking-how-to#restrict-your-storage-account-to-a-virtual-network).[Create a function app and storage account that both use private endpoints](https://github.com/Azure-Samples/function-app-arm-templates/tree/main/function-app-private-endpoints-storage-private-endpoints)[Private endpoints](functions-networking-options#private-endpoints).### Restricted network settings

You might also need to use these settings when your function app has network restrictions:

| Setting | Value | Description |
|---|---|---|
`WEBSITE_CONTENTOVERVNET` |

`1`

[Restrict your storage account to a virtual network](functions-networking-options#restrict-your-storage-account-to-a-virtual-network).`vnetrouteallenabled`

`1`

[Regional virtual network integration](functions-networking-options#regional-virtual-network-integration). This site setting supersedes the application setting[.](functions-app-settings#website_vnet_route_all)`WEBSITE_VNET_ROUTE_ALL`

### Considerations for network restrictions

When you're restricting access to the storage account through the private endpoints, you aren't able to access the storage account through the portal or any device outside the virtual network. You can give access to your secured IP address or virtual network in the storage account by [Managing the default network access rule](../storage/common/storage-network-security-set-default-access).

## Function access keys

Host-level [function access keys](function-keys-how-to) are defined as Azure resources. This means that you can create and manage host keys in your ARM templates and Bicep files. A host key is defined as a resource of type `Microsoft.Web/sites/host/functionKeys`

. This example creates a host-level access key named `my_custom_key`

when the function app is created:

```
resource functionKey 'Microsoft.Web/sites/host/functionKeys@2022-09-01' = {
name: '${parameters('name')}/default/my_custom_key'
properties: {
name: 'my_custom_key'
}
dependsOn: [
resourceId('Microsoft.Web/Sites', parameters('name'))
]
}
```


In this example, the `name`

parameter is the name of the new function app. You must include a `dependsOn`

setting to guarantee that the key is created with the new function app. Finally, the `properties`

object of the host key can also include a `value`

property that can be used to set a specific key.

When you don't set the `value`

property, Functions automatically generates a new key for you when the resource is created, which is recommended. To learn more about access keys, including security best practices for working with access keys, see [Work with access keys in Azure Functions](function-keys-how-to).

## Create your template

Experts with Bicep or ARM templates can manually code their deployments using a simple text editor. For the rest of us, there are several ways to make the development process easier:

**Visual Studio Code**: There are extensions available to help you work with both[Bicep files](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-bicep)and[ARM templates](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools). You can use these tools to help make sure that your code is correct, and they provide some[basic validation](functions-infrastructure-as-code?tabs=vs-code#validate-your-template).**Azure portal**: When you[create your function app and related resources in the portal](functions-create-function-app-portal), the final**Review + create**screen has a**Download a template for automation**link.This link shows you the ARM template generated based on the options you chose in portal. This template can seem a bit complex when you're creating a function app with many new resources. However, it can provide a good reference for how your ARM template might look.


## Validate your template

When you manually create your deployment template file, it's important to validate your template before deployment. All deployment methods validate your template syntax and raise a `validation failed`

error message as shown in the following JSON formatted example:

```
{"error":{"code":"InvalidTemplate","message":"Deployment template validation failed: 'The resource 'Microsoft.Web/sites/func-xyz' is not defined in the template. Please see https://aka.ms/arm-template for usage details.'.","additionalInfo":[{"type":"TemplateViolation","info":{"lineNumber":0,"linePosition":0,"path":""}}]}}
```


The following methods can be used to validate your template before deployment:

The following [Azure resource group deployment v2 task](/en-us/azure/devops/pipelines/tasks/deploy/azure-resource-group-deployment?view=azure-devops&preserve-view=true) with `deploymentMode: 'Validation'`

instructs Azure Pipelines to validate the template.

```
- task: AzureResourceManagerTemplateDeployment@3
inputs:
deploymentScope: 'Resource Group'
subscriptionId: # Required subscription ID
action: 'Create Or Update Resource Group'
resourceGroupName: # Required resource group name
location: # Required when action == Create Or Update Resource Group
templateLocation: 'Linked artifact'
csmFile: # Required when TemplateLocation == Linked Artifact
csmParametersFile: # Optional
deploymentMode: 'Validation'
```


You can also create a test resource group to find [preflight](../azure-resource-manager/troubleshooting/quickstart-troubleshoot-arm-deployment?tabs=azure-cli#fix-preflight-error) and [deployment](../azure-resource-manager/troubleshooting/quickstart-troubleshoot-arm-deployment?tabs=azure-cli#fix-deployment-error) errors.

## Deploy your template

You can use any of the following ways to deploy your Bicep file and template:

### Deploy to Azure button

Note

This method doesn't support deploying Bicep files currently.

Replace `<url-encoded-path-to-azuredeploy-json>`

with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of the raw path of your `azuredeploy.json`

file in GitHub.

Here's an example that uses markdown:

```
[![Deploy to Azure](https://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```


Here's an example that uses HTML:

```
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="https://azuredeploy.net/deploybutton.png"></a>
```


### Deploy using PowerShell

The following PowerShell commands create a resource group and deploy a Bicep file or ARM template that creates a function app with its required resources. To run locally, you must have [Azure PowerShell](/en-us/powershell/azure/install-azure-powershell) installed. To sign in to Azure, you must first run [ Connect-AzAccount](/en-us/powershell/module/az.accounts/connect-azaccount).

```
# Register Resource Providers if they're not already registered
Register-AzResourceProvider -ProviderNamespace "microsoft.web"
Register-AzResourceProvider -ProviderNamespace "microsoft.storage"
# Create a resource group for the function app
New-AzResourceGroup -Name "MyResourceGroup" -Location 'West Europe'
# Deploy the template
New-AzResourceGroupDeployment -ResourceGroupName "MyResourceGroup" -TemplateFile main.bicep -Verbose
```


To test out this deployment, you can use a [template like this one](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.web/function-app-create-dynamic) that creates a function app on Windows in a Consumption plan.

## Next steps

Learn more about how to develop and configure Azure Functions.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-how-to-github-actions -->

# Continuous delivery by using GitHub Actions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can use a [GitHub Actions workflow](https://docs.github.com/actions/learn-github-actions/introduction-to-github-actions#the-components-of-github-actions) to define a workflow to automatically build and deploy code to your function app in Azure Functions.

A YAML file (.yml) that defines the workflow configuration is maintained in the `/.github/workflows/`

path in your repository. This definition contains the actions and parameters that make up the workflow, which is specific to the development language of your functions. A GitHub Actions workflow for Functions performs the following tasks, regardless of language:

- Set up the environment.
- Build the code project.
- Deploy the package to a function app in Azure.

The Azure Functions action handles the deployment to an existing function app in Azure.

You can create a workflow configuration file for your deployment manually. You can also generate the file from a set of language-specific templates in one of these ways:

- In the Azure portal
- Using the Azure CLI
- From your GitHub repository

If you don't want to create your YAML file by hand, select a different method at the top of the article.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).A GitHub account. If you don't have one, sign up for

[free](https://github.com/join).A working function app hosted on Azure with source code in a GitHub repository.


[Azure CLI](/en-us/cli/azure/install-azure-cli), when developing locally. You can also use the Azure CLI in Azure Cloud Shell.

## Generate deployment credentials

Since GitHub Actions uses your publish profile to access your function app during deployment, you first need to get your publish profile and store it securely as a [GitHub secret](https://docs.github.com/en/actions/reference/encrypted-secrets).

Important

The publish profile is a valuable credential that allows access to Azure resources. Make sure you always transport and store it securely. In GitHub, the publish profile must only be stored in GitHub secrets.

### Download your publish profile

To download the publishing profile of your function app:

In the

[Azure portal](https://portal.azure.com), locate the page for your function app, expand**Settings**>**Configuration**in the left column.In the

**Configuration**page, select the**General settings**tab and make sure that**SCM Basic Auth Publishing Credentials**is turned**On**. When this setting is**Off**, you can't use publish profiles, so select**On**and then**Save**.Go back to the function app's

**Overview**page, and then select**Get publish profile**.Save and copy the contents of the file.


### Add the GitHub secret

In

[GitHub](https://github.com/), go to your repository.Go to

**Settings**.Select

**Secrets and variables > Actions**.Select

**New repository secret**.Add a new secret with the name

`AZURE_FUNCTIONAPP_PUBLISH_PROFILE`

and the value set to the contents of the publishing profile file.Select

**Add secret**.

GitHub can now authenticate to your function app in Azure.

## Create the workflow from a template

The best way to manually create a workflow configuration is to start from the officially supported template.

Choose either

**Windows**or**Linux**to make sure that you get the template for the correct operating system.Copy the language-specific template from the Azure Functions actions repository using the following link:

Update the

`env.AZURE_FUNCTIONAPP_NAME`

parameter with the name of your function app resource in Azure. You may optionally need to update the parameter that sets the language version used by your app, such as`DOTNET_VERSION`

for C#.Add this new YAML file in the

`/.github/workflows/`

path in your repository.

## Create the workflow configuration in the portal

When you use the portal to enable GitHub Actions, Functions creates a workflow file based on your application stack and commits it to your GitHub repository in the correct directory.

The portal automatically gets your publish profile and adds it to the GitHub secrets for your repository.

### During function app create

You can get started quickly with GitHub Actions through the Deployment tab when you create a function in Azure portal. To add a GitHub Actions workflow when you create a new function app:

In the

[Azure portal](https://portal.azure.com), select**Deployment**in the**Create Function App**flow.Enable

**Continuous Deployment**if you want each code update to trigger a code push to Azure portal.Enter your GitHub organization, repository, and branch.

Complete configuring your function app. Your GitHub repository now includes a new workflow file in

`/.github/workflows/`

.

### For an existing function app

To add a GitHub Actions workflow to an existing function app:

Navigate to your function app in the

[Azure portal](https://portal.azure.com)and select**Deployment Center**.For

**Source**select**GitHub**. If you don't see the default message*Building with GitHub Actions*, select**Change provider**choose**GitHub Actions**and select**OK**.If you haven't already authorized GitHub access, select

**Authorize**. Provide your GitHub credentials and select**Sign in**. To authorize a different GitHub account, select**Change Account**and sign in with another account.Select your GitHub

**Organization**,**Repository**, and**Branch**. To deploy with GitHub Actions, you must have write access to this repository.In

**Authentication settings**, choose whether to have GitHub Actions authenticate with a**User-assigned identity**or using**Basic authentication**credentials. For basic authentication, the current credentials are used.Select

**Preview file**to see the workflow file that gets added to your GitHub repository in`github/workflows/`

.Select

**Save**to add the workflow file to your repository.

## Add workflow configuration to your repository

You can use the [ az functionapp deployment github-actions add](/en-us/cli/azure/functionapp/deployment/github-actions) command to generate a workflow configuration file from the correct template for your function app. The new YAML file is then stored in the correct location (

`/.github/workflows/`

) in the GitHub repository you provide, while the publish profile file for your app is added to GitHub secrets in the same repository.Run this

`az functionapp`

command, replacing the values`githubUser/githubRepo`

,`MyResourceGroup`

, and`MyFunctionapp`

:`az functionapp deployment github-actions add --repo "githubUser/githubRepo" -g MyResourceGroup -n MyFunctionapp --login-with-github`

This command uses an interactive method to retrieve a personal access token for your GitHub account.

In your terminal window, you should see something like the following message:

`Please navigate to https://github.com/login/device and enter the user code XXXX-XXXX to activate and retrieve your GitHub personal access token.`

Copy the unique

`XXXX-XXXX`

code, browse to[https://github.com/login/device](https://github.com/login/device), and enter the code you copied. After entering your code, you should see something like the following message:`Verified GitHub repo and branch Getting workflow template using runtime: java Filling workflow template with name: func-app-123, branch: main, version: 8, slot: production, build_path: . Adding publish profile to GitHub Fetching publish profile with secrets for the app 'func-app-123' Creating new workflow file: .github/workflows/master_func-app-123.yml`

Go to your GitHub repository and select

**Actions**. Verify that your workflow ran.

## Create the workflow configuration file

You can create the GitHub Actions workflow configuration file from the Azure Functions templates directly from your GitHub repository.

In

[GitHub](https://github.com/), go to your repository.Select

**Actions**and**New workflow**.Search for

*functions*.In the displayed functions app workflows authored by Microsoft Azure, find the one that matches your code language and select

**Configure**.In the newly created YAML file, update the

`env.AZURE_FUNCTIONAPP_NAME`

parameter with the name of your function app resource in Azure. You may optionally need to update the parameter that sets the language version used by your app, such as`DOTNET_VERSION`

for C#.Verify that the new workflow file is being saved in

`/.github/workflows/`

and select**Commit changes...**.

## Update a workflow configuration

If for some reason, you need to update or change an existing workflow configuration, just navigate to the `/.github/workflows/`

location in your repository, open the specific YAML file, make any needed changes, and then commit the updates to the repository.

## Example: workflow configuration file

The following template example uses version 1 of the `functions-action`

and a `publish profile`

for authentication. The template depends on your chosen language and the operating system on which your function app is deployed:

```
name: Deploy DotNet project to Azure Function App
on:
[push]
env:
AZURE_FUNCTIONAPP_NAME: 'your-app-name' # set this to your function app name on Azure
AZURE_FUNCTIONAPP_PACKAGE_PATH: '.' # set this to the path to your function app project, defaults to the repository root
DOTNET_VERSION: '6.0.x' # set this to the dotnet version to use (e.g. '2.1.x', '3.1.x', '5.0.x')
jobs:
build-and-deploy:
runs-on: windows-latest
environment: dev
steps:
- name: 'Checkout GitHub Action'
uses: actions/checkout@v3
- name: Setup DotNet ${{ env.DOTNET_VERSION }} Environment
uses: actions/setup-dotnet@v3
with:
dotnet-version: ${{ env.DOTNET_VERSION }}
- name: 'Resolve Project Dependencies Using Dotnet'
shell: pwsh
run: |
pushd './${{ env.AZURE_FUNCTIONAPP_PACKAGE_PATH }}'
dotnet build --configuration Release --output ./output
popd
- name: 'Run Azure Functions Action'
uses: Azure/functions-action@v1
id: fa
with:
app-name: ${{ env.AZURE_FUNCTIONAPP_NAME }}
package: '${{ env.AZURE_FUNCTIONAPP_PACKAGE_PATH }}/output'
publish-profile: ${{ secrets.AZURE_FUNCTIONAPP_PUBLISH_PROFILE }}
```


## Azure Functions action

The Azure Functions action (`Azure/functions-action`

) defines how your code is published to an existing function app in Azure, or to a specific slot in your app.

### Parameters

The following parameters are required for all function app plans:

| Parameter | Explanation |
|---|---|
app-name |
The name of your function app. |
package |
This is the location in your project to be published. By default, this value is set to `.` , which means all files and folders in the GitHub repository will be deployed. |

The following parameters are required for the Flex Consumption plan:

| Parameter | Explanation |
|---|---|
sku |
Set this to `flexconsumption` when authenticating with publish-profile. When using RBAC credentials or deploying to a non-Flex Consumption plan, the Action can resolve the value, so the parameter does not need to be included. |
remote-build |
Set this to `true` to enable a build action from Kudu when the package is deployed to a Flex Consumption app. Oryx build is always performed during a remote build in Flex Consumption; do not set scm-do-build-during-deployment or enable-oryx-build. By default, this parameter is set to `false` . |

The following parameters are specific to the Consumption, Elastic Premium, and App Service (Dedicated) plans:

| Parameter | Explanation |
|---|---|
scm-do-build-during-deployment |
(Optional) Allow the Kudu site (e.g. `https://<APP_NAME>.scm.azurewebsites.net/` ) to perform pre-deployment operations, such as
`false` . Set this to `true` when you do want to control deployment behaviors using Kudu instead of resolving dependencies in your GitHub workflow. For more information, see the
`SCM_DO_BUILD_DURING_DEPLOYMENT` |
enable-oryx-build |
(Optional) Allow Kudu site to resolve your project dependencies with Oryx. By default, this is set to `false` . If you want to use
scm-do-build-during-deployment and enable-oryx-build to `true` . |

Optional parameters for all function app plans:

| Parameter | Explanation |
|---|---|
slot-name |
This is the
publish-profile parameter contains the credentials for the slot instead of the production site. Currently not supported in Flex Consumption. |

**publish-profile****respect-pom-xml**`true`

and set `package`

to `.`

. By default, this parameter is set to `false`

, which means that the `package`

parameter must point to your app's artifact location, such as `./target/azure-functions/`

**respect-funcignore**`true`

when your repository has a .funcignore file and you want to use it exclude paths and files, such as text editor configurations, .vscode/, or a Python virtual environment (.venv/). The default setting is `false`

.### Considerations

Keep the following considerations in mind when using the Azure Functions action:

When using GitHub Actions, the way that your code is deployed depends on your hosting plan, as shown in this table:

Hosting plan Deployment method [Flex Consumption](flex-consumption-plan)[One deploy](functions-deployment-technologies#one-deploy)[Elastic Premium](functions-premium-plan)[Zip deploy](deployment-zip-push)to apps on the[Consumption](consumption-plan)[Dedicated (App Service)](dedicated-plan)[Zip deploy](deployment-zip-push)to apps on the[Consumption](consumption-plan)[Consumption](consumption-plan)Windows: [Zip deploy](deployment-zip-push)

Linux:[external package URL](functions-deployment-technologies#external-package-url)** The ability to run your apps on Linux in a Consumption plan is planned for retirement. For more information, see

[Azure Functions Consumption plan hosting](consumption-plan).The credentials required by GitHub to connection to Azure for deployment are stored as Secrets in your GitHub repository and accessed in the deployment as

`secrets.<SECRET_NAME>`

.The easiest way for GitHub Actions to authenticate with Azure Functions for deployment is by using a publish profile. You can also authenticate using a service principal. To learn more, see

[this GitHub Actions repository](https://github.com/Azure/functions-action).The actions for setting up the environment and running a build are generated from the templates, and are language specific.

The templates use

`env`

elements to define settings unique to your build and deployment.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-how-to-azure-devops -->

# Continuous delivery with Azure Pipelines

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use [Azure Pipelines](/en-us/azure/devops/pipelines/) to automatically deploy your code project to a function app in Azure. Azure Pipelines lets you build, test, and deploy with continuous integration (CI) and continuous delivery (CD) using [Azure DevOps](/en-us/azure/devops/).

YAML pipelines are defined using a YAML file in your repository. A step is the smallest building block of a pipeline and can be a script or task (prepackaged script). [Learn about the key concepts and components that make up a pipeline](/en-us/azure/devops/pipelines/get-started/key-pipelines-concepts).

You use the `AzureFunctionApp`

task to deploy your code. There are now two versions of `AzureFunctionApp`

, which are compared in this table:

| Comparison/version |
|
|---|

[AzureFunctionApp@1](/en-us/azure/devops/pipelines/tasks/reference/azure-function-app-v1)

[Flex Consumption plan](flex-consumption-plan)** Enhanced validation support makes pipelines less likely to fail because of errors.

Choose your task version at the top of the article.

Note

Upgrade from `AzureFunctionApp@1`

to `AzureFunctionApp@2`

for access to new features and long-term support.

## Prerequisites

An Azure DevOps organization. If you don't have one, you can

[create one for free](/en-us/azure/devops/pipelines/get-started/pipelines-sign-up). If your team already has one, then make sure you're an administrator of the Azure DevOps project that you want to use.An ability to run pipelines on Microsoft-hosted agents. You can either purchase a

[parallel job](/en-us/azure/devops/pipelines/licensing/concurrent-jobs)or you can request a free tier.If you plan to use GitHub instead of Azure Repos, you also need a GitHub repository. If you don't have a GitHub account, you can

[create one for free](https://github.com).An existing function app in Azure that has its source code in a supported repository. If you don't yet have an Azure Functions code project, you can create one by completing the following language-specific article:


Remember to upload the local code project to your GitHub or Azure Repos repository after you publish it to your function app.

## Build your app

- Sign in to your Azure DevOps organization and navigate to your project.
- In your project, navigate to the
**Pipelines**page. Then choose the action to create a new pipeline. - Walk through the steps of the wizard by first selecting
**GitHub**as the location of your source code. - You might be redirected to GitHub to sign in. If so, enter your GitHub credentials.
- When the list of repositories appears, select your sample app repository.
- Azure Pipelines will analyze your repository and recommend a template. Select
**Save and run**, then select**Commit directly to the main branch**, and then choose**Save and run**again. - A new run is started. Wait for the run to finish.

### Example YAML build pipelines

The following language-specific pipelines can be used for building apps.

You can use the following sample to create a YAML file to build a .NET app:

```
pool:
vmImage: 'windows-latest'
steps:
- task: UseDotNet@2
displayName: 'Install .NET 8.0 SDK'
inputs:
packageType: 'sdk'
version: '8.0.x'
installationPath: $(Agent.ToolsDirectory)/dotnet
- script: |
dotnet restore
dotnet build --configuration Release
- task: DotNetCoreCLI@2
displayName: 'dotnet publish'
inputs:
command: publish
arguments: '--configuration Release --output $(System.DefaultWorkingDirectory)/publish_output'
projects: 'csharp/*.csproj'
publishWebProjects: false
modifyOutputPath: false
zipAfterPublish: false
- task: ArchiveFiles@2
displayName: "Archive files"
inputs:
rootFolderOrFile: "$(System.DefaultWorkingDirectory)/publish_output"
includeRootFolder: false
archiveFile: "$(System.DefaultWorkingDirectory)/build$(Build.BuildId).zip"
- task: PublishBuildArtifacts@1
inputs:
PathtoPublish: '$(System.DefaultWorkingDirectory)/build$(Build.BuildId).zip'
artifactName: 'drop'
```


- Sign in to your Azure DevOps organization and navigate to your project.
- In your project, navigate to the
**Pipelines**page. Then select**New pipeline**. - Select one of these options for
**Where is your code?**:**GitHub**: You might be redirected to GitHub to sign in. If so, enter your GitHub credentials. When this connection is your first GitHub connection, the wizard also walks you through the process of connecting DevOps to your GitHub accounts.**Azure Repos Git**: You're immediately able to choose a repository in your current DevOps project.

- When the list of repositories appears, select your sample app repository.
- Azure Pipelines analyzes your repository and in
**Configure your pipeline**provides a list of potential templates. Choose the appropriate**function app**template for your language. If you don't see the correct template select**Show more**. - Select
**Save and run**, then select**Commit directly to the main branch**, and then choose**Save and run**again. - A new run is started. Wait for the run to finish.

### Example YAML build pipelines

The following language-specific pipelines can be used for building apps.

You can use the following sample to create a YAML file to build a .NET app.

If you see errors when building your app, verify that the version of .NET that you use matches your Azure Functions version. For more information, see [Azure Functions runtime versions overview](functions-versions).

```
pool:
vmImage: 'windows-latest'
steps:
- task: UseDotNet@2
displayName: 'Install .NET 8.0 SDK'
inputs:
packageType: 'sdk'
version: '8.0.x'
installationPath: $(Agent.ToolsDirectory)/dotnet
- script: |
dotnet restore
dotnet build --configuration Release
- task: DotNetCoreCLI@2
displayName: 'dotnet publish'
inputs:
command: publish
arguments: '--configuration Release --output $(System.DefaultWorkingDirectory)/publish_output'
projects: 'csharp/*.csproj'
publishWebProjects: false
modifyOutputPath: false
zipAfterPublish: false
- task: ArchiveFiles@2
displayName: "Archive files"
inputs:
rootFolderOrFile: "$(System.DefaultWorkingDirectory)/publish_output"
includeRootFolder: false
archiveFile: "$(System.DefaultWorkingDirectory)/build$(Build.BuildId).zip"
- task: PublishBuildArtifacts@1
inputs:
PathtoPublish: '$(System.DefaultWorkingDirectory)/build$(Build.BuildId).zip'
artifactName: 'drop'
```


## Deploy your app

You'll deploy with the [Azure Function App Deploy v2](/en-us/azure/devops/pipelines/tasks/reference/azure-function-app-v2) task. This task requires an [Azure service connection](/en-us/azure/devops/pipelines/library/service-endpoints) as an input. An Azure service connection stores the credentials to connect from Azure Pipelines to Azure. You should create a connection that uses [workload identity federation](/en-us/azure/devops/pipelines/library/connect-to-azure#create-an-azure-resource-manager-service-connection-that-uses-workload-identity-federation).

To deploy to Azure Functions, add this snippet at the end of your `azure-pipelines.yml`

file, depending on whether your app runs on Linux or Windows:

```
trigger:
- main
variables:
# Azure service connection established during pipeline creation
azureSubscription: <Name of your Azure subscription>
appName: <Name of the function app>
# Agent VM image name
vmImageName: 'windows-latest'
- task: AzureFunctionApp@2 # Add this at the end of your file
inputs:
azureSubscription: <Name of your Azure subscription>
appType: functionApp # this specifies a Windows-based function app
appName: $(appName)
package: $(System.DefaultWorkingDirectory)/build$(Build.BuildId).zip
deploymentMethod: 'auto' # 'auto' | 'zipDeploy' | 'runFromPackage'. Required. Deployment method. Default: auto.
#Uncomment the next lines to deploy to a deployment slot
#Note that deployment slots is not supported for Linux Dynamic SKU
#deployToSlotOrASE: true
#resourceGroupName: '<RESOURCE_GROUP>'
#slotName: '<SLOT_NAME>'
```


The default `appType`

is Windows (`functionApp`

). You can specify Linux by setting the `appType`

to `functionAppLinux`

. A [Flex Consumption](/en-us/azure/azure-functions/flex-consumption-plan) app runs on Linux, and you to must set both `appType: functionAppLinux`

and `isFlexConsumption: true`

.

The snippet assumes that the build steps in your YAML file produce the zip archive in the `$(System.ArtifactsDirectory)`

folder on your agent.

You deploy using the [Azure Function App Deploy](/en-us/azure/devops/pipelines/tasks/deploy/azure-function-app) task. This task requires an [Azure service connection](/en-us/azure/devops/pipelines/library/service-endpoints) as an input. An Azure service connection stores the credentials to connect from Azure Pipelines to Azure.

Important

Deploying to a Flex Consumption app isn't supported using @v1 of the `AzureFunctionApp`

task.

To deploy to Azure Functions, add this snippet at the end of your `azure-pipelines.yml`

file:

```
trigger:
- main
variables:
# Azure service connection established during pipeline creation
azureSubscription: <Name of your Azure subscription>
appName: <Name of the function app>
# Agent VM image name
vmImageName: 'ubuntu-latest'
- task: DownloadBuildArtifacts@1 # Add this at the end of your file
inputs:
buildType: 'current'
downloadType: 'single'
artifactName: 'drop'
itemPattern: '**/*.zip'
downloadPath: '$(System.ArtifactsDirectory)'
- task: AzureFunctionApp@1
inputs:
azureSubscription: $(azureSubscription)
appType: functionAppLinux # default is functionApp
appName: $(appName)
package: $(System.ArtifactsDirectory)/**/*.zip
```


This snippet sets the `appType`

to `functionAppLinux`

, which is required when deploying to an app that runs on Linux. The default `appType`

is Windows (`functionApp`

).

The example assumes that the build steps in your YAML file produce the zip archive in the `$(System.ArtifactsDirectory)`

folder on your agent.

## Deploy a container

Tip

We recommend using the Azure Functions support in Azure Container Apps for hosting your function app in a custom Linux container. For more information, see [Azure Functions on Azure Container Apps overview](../container-apps/functions-overview).

When deploying a containerized function app, the deployment task you use depends on the specific hosting environment.

You can use the [Azure Container Apps Deploy](/en-us/azure/devops/pipelines/tasks/reference/azure-container-apps-v1) task (`AzureContainerApps`

) to deploy a function app image to an Azure Container App instance that is optimized for Azure Functions.

This code deploys the base image for a .NET 8 isolated process model function app:

```
trigger:
- main
pool:
vmImage: 'ubuntu-latest'
steps:
- task: AzureContainerApps@1
inputs:
azureSubscription: <Name of your Azure subscription>
imageToDeploy: 'mcr.microsoft.com/azure-functions/dotnet-isolated:4-dotnet-isolated8.0'
containerAppName: <Name of your container app>
resourceGroup: <Name of the resource group>
```


Ideally, you would build your own custom container in the pipeline instead of using a base image, as shown in this example. For more information, see [Deploy to Azure Container Apps from Azure Pipelines](../container-apps/azure-pipelines).

## Deploy to a slot

Important

The Flex Consumption plan doesn't currently support slots.
Linux apps also don't support slots when running in a Consumption plan, and [support for these apps is being retired in the future](consumption-plan).

```
trigger:
- main
variables:
# Azure service connection established during pipeline creation
azureSubscription: <Name of your Azure subscription>
appName: <Name of the function app>
# Agent VM image name
vmImageName: 'windows-latest'
- task: AzureFunctionApp@2 # Add this at the end of your file
inputs:
azureSubscription: <Name of your Azure subscription>
appType: functionApp # this specifies a Windows-based function app
appName: $(appName)
package: $(System.DefaultWorkingDirectory)/build$(Build.BuildId).zip
deploymentMethod: 'auto' # 'auto' | 'zipDeploy' | 'runFromPackage'. Required. Deployment method. Default: auto.
deployToSlotOrASE: true
resourceGroupName: '<RESOURCE_GROUP>'
slotName: '<SLOT_NAME>'
```


You can configure your function app to have multiple slots. Slots allow you to safely deploy your app and test it before making it available to your customers.

The following YAML snippet shows how to deploy to a staging slot, and then swap to a production slot:

```
- task: AzureFunctionApp@1
inputs:
azureSubscription: <Azure service connection>
appType: functionAppLinux
appName: <Name of the function app>
package: $(System.ArtifactsDirectory)/**/*.zip
deployToSlotOrASE: true
resourceGroupName: <Name of the resource group>
slotName: staging
- task: AzureAppServiceManage@0
inputs:
azureSubscription: <Azure service connection>
WebAppName: <name of the function app>
ResourceGroupName: <name of resource group>
SourceSlot: staging
SwapWithProduction: true
```


When using [deployment slots](functions-deployment-slots), you can also add the following task to perform a slot swap as part of your deployment.

```
- task: AzureAppServiceManage@0
inputs:
azureSubscription: <AZURE_SERVICE_CONNECTION>
WebAppName: <APP_NAME>
ResourceGroupName: <RESOURCE_GROUP>
SourceSlot: <SLOT_NAME>
SwapWithProduction: true
```


## Create a pipeline with Azure CLI

To create a build pipeline in Azure, use the `az functionapp devops-pipeline create`

[command](/en-us/cli/azure/functionapp/devops-pipeline#az-functionapp-devops-pipeline-create). The build pipeline is created to build and release any code changes that are made in your repo. The command generates a new YAML file that defines the build and release pipeline and then commits it to your repo. The prerequisites for this command depend on the location of your code.

If your code is in GitHub:

You must have

**write**permissions for your subscription.You must be the project administrator in Azure DevOps.

You must have permissions to create a GitHub personal access token (PAT) that has sufficient permissions. For more information, see

[GitHub PAT permission requirements.](/en-us/azure/devops/pipelines/repos/github#repository-permissions-for-personal-access-token-pat-authentication)You must have permissions to commit to the main branch in your GitHub repository so you can commit the autogenerated YAML file.


If your code is in Azure Repos:

You must have

**write**permissions for your subscription.You must be the project administrator in Azure DevOps.


## Next steps

- Review the
[Azure Functions overview](functions-overview). - Review the
[Azure DevOps overview](/en-us/azure/devops/pipelines/).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model -->

# Migrate C# apps from the in-process model to the isolated worker model

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

[Support for the in-process model ends on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you migrate your apps to the isolated worker model by following the instructions in this article.

This article walks you through the process of safely migrating your .NET function app from the [in-process model](functions-dotnet-class-library) to the [isolated worker model](dotnet-isolated-process-guide). To learn about the high-level differences between these models, see the [execution mode comparison](dotnet-isolated-in-process-differences).

This guide assumes that your app is running on version 4.x of the Functions runtime. If not, you should use the following guides to upgrade your host version. These host-version migration guides also help you migrate to the isolated worker model as you work through them.

[Migrate apps from Azure Functions version 2.x and 3.x to version 4.x](migrate-version-3-version-4)[Migrate apps from Azure Functions version 1.x to version 4.x](migrate-version-1-version-4)

When supported, this article takes advantage of [ASP.NET Core integration](dotnet-isolated-process-guide#aspnet-core-integration) in the isolated worker model, which improves performance and provides a familiar programming model when your app uses HTTP triggers.

## Identify function apps to migrate

Use the following Azure PowerShell script to generate a list of function apps in your subscription that currently use the in-process model.

The script uses the subscription that Azure PowerShell is currently configured to use. You can change the subscription by first running `Set-AzContext -Subscription '<YOUR SUBSCRIPTION ID>'`

and replacing `<YOUR SUBSCRIPTION ID>`

with the ID of the subscription you would like to evaluate.

```
$FunctionApps = Get-AzFunctionApp
$AppInfo = @{}
foreach ($App in $FunctionApps)
{
if ($App.Runtime -eq 'dotnet')
{
$AppInfo.Add($App.Name, $App.Runtime)
}
}
$AppInfo
```


## Choose your target .NET version

On version 4.x of the Functions runtime, your .NET function app targets .NET 6 or .NET 8 when using the in-process model.

When you migrate your function app, you have the opportunity to choose the target version of .NET. You can update your C# project to one of the following versions of .NET that are supported by Functions version 4.x:

| .NET version |
|
|---|

1,2

[Isolated worker model](dotnet-isolated-process-guide)3[Isolated worker model](dotnet-isolated-process-guide)[Isolated worker model](dotnet-isolated-process-guide),[In-process model](functions-dotnet-class-library)2[See policy](https://dotnet.microsoft.com/platform/support/policy/dotnet-framework)[Isolated worker model](dotnet-isolated-process-guide)1 The [isolated worker model](dotnet-isolated-process-guide) supports Long Term Support (LTS) and Standard Term Support (STS) versions of .NET, as well as .NET Framework. The [in-process model](functions-dotnet-class-library) only supports LTS releases of .NET, ending with .NET 8. For a full feature and functionality comparison between the two models, see [Differences between in-process and isolate worker process .NET Azure Functions](dotnet-isolated-in-process-differences).

2 Support ends for the in-process model on November 10, 2026. For more information, see [this support announcement](https://aka.ms/azure-functions-retirements/in-process-model). For continued full support, you should [migrate your apps to the isolated worker model](migrate-dotnet-to-isolated-model).

3 .NET 9 previously had an expected end-of-support date of May 12, 2026. During the .NET 9 service window, the .NET team extended support for STS versions to 24 months, starting with .NET 9. For more information, see [the blog post](https://devblogs.microsoft.com/dotnet/dotnet-sts-releases-supported-for-24-months/).

Tip

**We recommend upgrading to .NET 8 on the isolated worker model.** This provides a quick migration path to the fully released version with the longest support window from .NET.

This guide doesn't present specific examples for .NET 10 (preview) or .NET 9. If you need to target one of those versions, you can adapt the .NET 8 examples.

## Prepare for migration

Before you migrate an app to the isolated worker model, you should thoroughly review the contents of this guide. You should also familiarize yourself with the features of the [isolated worker model](dotnet-isolated-process-guide) and the [differences between the two models](dotnet-isolated-in-process-differences).

To migrate the application:

- Migrate your local project to the isolated worker model by following the steps in
[Migrate your local project](#migrate-your-local-project). - After migrating your project, fully test the app locally using version 4.x of the
[Azure Functions Core Tools](functions-run-local). [Update your function app in Azure](#update-your-function-app-in-azure)to the isolated model.

## Migrate your local project

The section outlines the various changes that you need to make to your local project to move it to the isolated worker model. Some of the steps change based on your target version of .NET. Use the tabs to select the instructions that match your desired version.

Tip

If you're moving to an LTS or STS version of .NET, the [.NET Upgrade Assistant](/en-us/dotnet/core/porting/upgrade-assistant-overview) can be used to automatically make many of the changes mentioned in the following sections.

First, convert the project file and update your dependencies. As you do, you see build errors for the project. In subsequent steps, you'll make the corresponding changes to remove these errors.

### Project file

The following example is a *.csproj* project file that uses .NET 8 on version 4.x:

```
<Project Sdk="Microsoft.NET.Sdk">
<PropertyGroup>
<TargetFramework>net8.0</TargetFramework>
<AzureFunctionsVersion>v4</AzureFunctionsVersion>
<RootNamespace>My.Namespace</RootNamespace>
</PropertyGroup>
<ItemGroup>
<PackageReference Include="Microsoft.NET.Sdk.Functions" Version="4.1.1" />
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


Use one of the following procedures to update this XML file to run in the isolated worker model:

These steps assume a local C# project; if your app instead uses C# script (*.csx* files), you should [convert to the project model](functions-reference-csharp#convert-a-c-script-app-to-a-c-project) before continuing.

The following changes are required in the *.csproj* XML project file:

Set the value of

`PropertyGroup`

.`TargetFramework`

to`net8.0`

.Set the value of

`PropertyGroup`

.`AzureFunctionsVersion`

to`v4`

.Add the following

`OutputType`

element to the`PropertyGroup`

:`<OutputType>Exe</OutputType>`

In the

`ItemGroup`

.`PackageReference`

list, replace the package reference to`Microsoft.NET.Sdk.Functions`

with the following references:`<FrameworkReference Include="Microsoft.AspNetCore.App" /> <PackageReference Include="Microsoft.Azure.Functions.Worker" Version="1.21.0" /> <PackageReference Include="Microsoft.Azure.Functions.Worker.Sdk" Version="1.17.2" /> <PackageReference Include="Microsoft.Azure.Functions.Worker.Extensions.Http.AspNetCore" Version="1.2.1" /> <PackageReference Include="Microsoft.ApplicationInsights.WorkerService" Version="2.22.0" /> <PackageReference Include="Microsoft.Azure.Functions.Worker.ApplicationInsights" Version="1.2.0" />`

Make note of any references to other packages in the

`Microsoft.Azure.WebJobs.*`

namespaces. You'll replace these packages in a later step.Add the following new

`ItemGroup`

:`<ItemGroup> <Using Include="System.Threading.ExecutionContext" Alias="ExecutionContext"/> </ItemGroup>`


After you make these changes, your updated project should look like the following example:

```
<Project Sdk="Microsoft.NET.Sdk">
<PropertyGroup>
<TargetFramework>net8.0</TargetFramework>
<AzureFunctionsVersion>v4</AzureFunctionsVersion>
<RootNamespace>My.Namespace</RootNamespace>
<OutputType>Exe</OutputType>
<ImplicitUsings>enable</ImplicitUsings>
<Nullable>enable</Nullable>
</PropertyGroup>
<ItemGroup>
<FrameworkReference Include="Microsoft.AspNetCore.App" />
<PackageReference Include="Microsoft.Azure.Functions.Worker" Version="1.21.0" />
<PackageReference Include="Microsoft.Azure.Functions.Worker.Sdk" Version="1.17.2" />
<PackageReference Include="Microsoft.Azure.Functions.Worker.Extensions.Http.AspNetCore" Version="1.2.1" />
<PackageReference Include="Microsoft.ApplicationInsights.WorkerService" Version="2.22.0" />
<PackageReference Include="Microsoft.Azure.Functions.Worker.ApplicationInsights" Version="1.2.0" />
<!-- Other packages may also be in this list -->
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
<ItemGroup>
<Using Include="System.Threading.ExecutionContext" Alias="ExecutionContext"/>
</ItemGroup>
</Project>
```


Changing your project's target framework might also require changes to parts of your toolchain, outside of project code. For example, in VS Code, you might need to update the `azureFunctions.deploySubpath`

extension setting through user settings or your project's *.vscode/settings.json* file. Check for any dependencies on the framework version that might exist outside of your project code, as part of build steps or a CI/CD pipeline.

### Package references

When migrating to the isolated worker model, you need to change the packages your application references.

If you haven't already, update your project to reference the latest stable versions of:

Depending on the triggers and bindings your app uses, your app might need to reference a different set of packages. The following table shows the replacements for some of the most commonly used extensions:

| Scenario | Changes to package references |
|---|---|
| Timer trigger | Add
|
| Storage bindings | Replace`Microsoft.Azure.WebJobs.Extensions.Storage` with
|
| Blob bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.Storage.Blobs` with the latest version of
|
| Queue bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.Storage.Queues` with the latest version of
|
| Table bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.Tables` with the latest version of
|
| Cosmos DB bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.CosmosDB` and/or `Microsoft.Azure.WebJobs.Extensions.DocumentDB` with the latest version of
|
| Service Bus bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.ServiceBus` with the latest version of
|
| Event Hubs bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.EventHubs` with the latest version of
|
| Event Grid bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.EventGrid` with the latest version of
|
| SignalR Service bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.SignalRService` with the latest version of
|
| Durable Functions | Replace references to`Microsoft.Azure.WebJobs.Extensions.DurableTask` with the latest version of
|
| Durable Functions (SQL storage provider) |
Replace references to`Microsoft.DurableTask.SqlServer.AzureFunctions` with the latest version of
|
| Durable Functions (Netherite storage provider) |
Replace references to`Microsoft.Azure.DurableTask.Netherite.AzureFunctions` with the latest version of
|
| SendGrid bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.SendGrid` with the latest version of
|
| Kafka bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.Kafka` with the latest version of
|
| RabbitMQ bindings | Replace references to`Microsoft.Azure.WebJobs.Extensions.RabbitMQ` with the latest version of
|
| Dependency injection and startup config |
Remove references to`Microsoft.Azure.Functions.Extensions` (The isolated worker model provides this functionality by default.) |

See [Supported bindings](functions-triggers-bindings#supported-bindings) for a complete list of extensions to consider, and consult each extension's documentation for full installation instructions for the isolated process model. Be sure to install the latest stable version of any packages you are targeting.

Tip

Any changes to extension versions during this process might require you to update your `host.json`

file as well. Be sure to read the documentation of each extension that you use.
For example, the Service Bus extension has breaking changes in the structure between versions 4.x and 5.x. For more information, see [Azure Service Bus bindings for Azure Functions](/en-us/azure/azure-functions/functions-bindings-service-bus?tabs=isolated-process%2Cextensionv5%2Cextensionv3&pivots=programming-language-csharp#hostjson-settings).

**Your isolated worker model application should not reference any packages in the Microsoft.Azure.WebJobs.* namespaces or Microsoft.Azure.Functions.Extensions.** If you have any remaining references to these, they should be removed.


Tip

Your app might also depend on Azure SDK types, either as part of your triggers and bindings or as a standalone dependency. You should take this opportunity to update these as well. The latest versions of the Functions extensions work with the latest versions of the [Azure SDK for .NET](/en-us/dotnet/azure/sdk/azure-sdk-for-dotnet), almost all of the packages for which are the form `Azure.*`

.

### Program.cs file

When migrating to run in an isolated worker process, you must add a *Program.cs* file to your project with the following contents:

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
var host = new HostBuilder()
.ConfigureFunctionsWebApplication()
.ConfigureServices(services => {
services.AddApplicationInsightsTelemetryWorkerService();
services.ConfigureFunctionsApplicationInsights();
})
.Build();
host.Run();
```


This example includes [ASP.NET Core integration](dotnet-isolated-process-guide#aspnet-core-integration) to improve performance and provide a familiar programming model when your app uses HTTP triggers. If you don't intend to use HTTP triggers, you can replace the call to `ConfigureFunctionsWebApplication`

with a call to `ConfigureFunctionsWorkerDefaults`

. If you do so, you can remove the reference to `Microsoft.Azure.Functions.Worker.Extensions.Http.AspNetCore`

from your project file. However, for the best performance, even for functions with other trigger types, you should keep the `FrameworkReference`

to ASP.NET Core.

The *Program.cs* file replaces any file that has the `FunctionsStartup`

attribute, which is typically a *Startup.cs* file. In places where your `FunctionsStartup`

code would reference `IFunctionsHostBuilder.Services`

, you can instead add statements within the `.ConfigureServices()`

method of the `HostBuilder`

in your *Program.cs*. To learn more about working with *Program.cs*, see [Start-up and configuration](dotnet-isolated-process-guide#start-up-and-configuration) in the isolated worker model guide.

The default *Program.cs* examples previously described include setup of [Application Insights](dotnet-isolated-process-guide#application-insights). In your *Program.cs*, you must also configure any log filtering that should apply to logs coming from code in your project. In the isolated worker model, the *host.json* file only controls events emitted by the Functions host runtime. If you don't configure filtering rules in *Program.cs*, you might see differences in the log levels present for various categories in your telemetry.

Although you can register custom configuration sources as part of the `HostBuilder`

, these similarly apply only to code in your project. The platform also needs trigger and binding configuration, and this should be provided through the [application settings](../app-service/configure-common#configure-app-settings), [Key Vault references](../app-service/app-service-key-vault-references?toc=/azure/azure-functions/toc.json), or [App Configuration references](../app-service/app-service-configuration-references?toc=/azure/azure-functions/toc.json) features.

After you move everything from any existing `FunctionsStartup`

to the *Program.cs* file, you can delete the `FunctionsStartup`

attribute and the class it was applied to.

### Function signature changes

Some key types change between the in-process model and the isolated worker model. Many of these relate to the attributes, parameters, and return types that make up the function signature. For each of your functions, you must make changes to:

- The function attribute, which also sets the function's name
- How the function obtains an
`ILogger`

/`ILogger<T>`

- Trigger and binding attributes and parameters

The rest of this section walks you through each of these steps.

#### Function attributes

The `Function`

attribute in the isolated worker model replaces the `FunctionName`

attribute. The new attribute has the same signature, and the only difference is in the name. You can therefore just perform a string replacement across your project.

#### Logging

In the in-process model, you could include an optional `ILogger`

parameter for your function, or you could use dependency injection to get an `ILogger<T>`

. If your app already used dependency injection, the same mechanisms work in the isolated worker model.

However, for any Functions that relied on the `ILogger`

method parameter, you need to make a change. We recommended that you use dependency injection to obtain an `ILogger<T>`

. Use the following steps to migrate the function's logging mechanism:

In your function class, add a

`private readonly ILogger<MyFunction> _logger;`

property, replacing`MyFunction`

with the name of your function class.Create a constructor for your function class that takes in the

`ILogger<T>`

as a parameter:`public MyFunction(ILogger<MyFunction> logger) { _logger = logger; }`

Replace both instances of

`MyFunction`

in the preceding code snippet with the name of your function class.For logging operations in your function code, replace references to the

`ILogger`

parameter with`_logger`

.Remove the

`ILogger`

parameter from your function signature.

To learn more, see [Logging in the isolated worker model](dotnet-isolated-process-guide#logging).

#### Trigger and binding changes

When you [changed your package references in a previous step](#package-references), you introduced errors for your triggers and bindings that you can now fix:

Remove any

`using Microsoft.Azure.WebJobs;`

statements.Add a

`using Microsoft.Azure.Functions.Worker;`

statement.For each binding attribute, change the attribute's name as specified in its reference documentation, which you can find in the

[Supported bindings](functions-triggers-bindings#supported-bindings)index. In general, the attribute names change as follows:**Triggers typically remain named the same way.**For example,`QueueTrigger`

is the attribute name for both models.**Input bindings typically need**For example, if you used the`Input`

added to their name.`CosmosDB`

input binding attribute in the in-process model, the attribute would now be`CosmosDBInput`

.**Output bindings typically need**For example, if you used the`Output`

added to their name.`Queue`

output binding attribute in the in-process model, this attribute would now be`QueueOutput`

.

Update the attribute parameters to reflect the isolated worker model version, as specified in the binding's reference documentation.

For example, in the in-process model, a blob output binding is represented by a

`[Blob(...)]`

attribute that includes an`Access`

property. In the isolated worker model, the blob output attribute would be`[BlobOutput(...)]`

. The binding no longer requires the`Access`

property, so that parameter can be removed. So`[Blob("sample-images-sm/{fileName}", FileAccess.Write, Connection = "MyStorageConnection")]`

would become`[BlobOutput("sample-images-sm/{fileName}", Connection = "MyStorageConnection")]`

.Move output bindings out of the function parameter list. If you have just one output binding, you can apply this to the return type of the function. If you have multiple outputs, create a new class with properties for each output, and apply the attributes to those properties. To learn more, see

[Multiple output bindings](dotnet-isolated-process-guide#multiple-output-bindings).Consult each binding's reference documentation for the types it allows you to bind to. In some cases, you might need to change the type. For output bindings, if the in-process model version used an

`IAsyncCollector<T>`

, you can replace this with binding to an array of the target type:`T[]`

. You can also consider replacing the output binding with a client object for the service it represents, either as the binding type for an input binding if available, or by[injecting a client yourself](dotnet-isolated-process-guide#register-azure-clients).If your function includes an

`IBinder`

parameter, remove it. Replace the functionality with a client object for the service it represents, either as the binding type for an input binding if available, or by[injecting a client yourself](dotnet-isolated-process-guide#register-azure-clients).Update the function code to work with any new types.


### local.settings.json file

The *local.settings.json* file is only used when running locally. For information, see [Local settings file](functions-develop-local#local-settings-file).

When migrating from running in-process to running in an isolated worker process, you need to change the `FUNCTIONS_WORKER_RUNTIME`

value to *dotnet-isolated*. Make sure that your *local.settings.json* file has at least the following elements:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "UseDevelopmentStorage=true",
"FUNCTIONS_WORKER_RUNTIME": "dotnet-isolated"
}
}
```


The value you have for `AzureWebJobsStorage`

might be different. You don't need to change its value as part of the migration.

### host.json file

No changes are required to your *host.json* file. However, if your Application Insights configuration is in this file from your in-process model project, you might want to make additional changes in your *Program.cs* file. The *host.json* file only controls logging from the Functions host runtime, and in the isolated worker model, some of these logs come from your application directly, giving you more control. See [Managing log levels in the isolated worker model](dotnet-isolated-process-guide#managing-log-levels) for details on how to filter these logs.

### Other code changes

This section highlights other code changes to consider as you work through the migration. These changes aren't needed by all applications, but you should evaluate if any are relevant to your scenarios.

#### JSON serialization

By default, the isolated worker model uses *System.Text.Json* for JSON serialization. To customize serializer options or switch to JSON.NET (*Newtonsoft.Json*), see [Customizing JSON serialization](dotnet-isolated-process-guide#customizing-json-serialization).

#### Application Insights log levels and filtering

Logs can be sent to Application Insights from both the Functions host runtime and code in your project. The *host.json* allows you to configure rules for host logging, but to control logs coming from your code, you need to configure filtering rules as part of your *Program.cs*. See [Managing log levels in the isolated worker model](dotnet-isolated-process-guide#managing-log-levels) for details on how to filter these logs.

### Example function migrations

#### HTTP trigger example

An HTTP trigger for the in-process model might look like the following example:

```
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Extensions.Logging;
namespace Company.Function
{
public static class HttpTriggerCSharp
{
[FunctionName("HttpTriggerCSharp")]
public static IActionResult Run(
[HttpTrigger(AuthorizationLevel.Function, "get", Route = null)] HttpRequest req,
ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
return new OkObjectResult($"Welcome to Azure Functions, {req.Query["name"]}!");
}
}
}
```


An HTTP trigger for the migrated version might look like the following example:

```
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.Logging;
namespace Company.Function
{
public class HttpTriggerCSharp(ILogger<HttpTriggerCSharp> logger)
{
[Function("HttpTriggerCSharp")]
public IActionResult Run(
[HttpTrigger(AuthorizationLevel.Function, "get")] HttpRequest req)
{
logger.LogInformation("C# HTTP trigger function processed a request.");
return new OkObjectResult($"Welcome to Azure Functions, {req.Query["name"]}!");
}
}
}
```


## Update your function app in Azure

Updating your function app to the isolated model involves two changes that should be completed together, because if you only complete one, the app is in an error state. Both of these changes also cause the app process to restart. For these reasons, you should perform the update using a [staging slot](functions-deployment-slots). Staging slots help minimize downtime for your app and allow you to test and verify your migrated code with your updated configuration in Azure. You can then deploy your fully migrated app to the production slot through a swap operation.

Important

When an app's deployed payload doesn't match the configured runtime, it's in [an error state](errors-diagnostics/diagnostic-events/azfd0013). During the migration process, you put the app into this state, ideally only temporarily. Deployment slots help mitigate the effect of this, because the error state will be resolved in your staging (nonproduction) environment before the changes are applied as single update to your production environment. Slots also defend against any mistakes and allow you to detect any other issues before reaching production.

During the process, you might still see errors in logs coming from your staging (nonproduction) slot. This is expected, though these should go away as you proceed through the steps. Before you perform the slot swap operation, you should confirm that these errors stop being raised and that your application is working as expected.

Use the following steps to use deployment slots to update your function app to the isolated worker model:

[Create a deployment slot](functions-deployment-slots#add-a-slot)if you haven't already. You might also want to familiarize yourself with the slot swap process and ensure that you can make updates to the existing application with minimal disruption.Change the configuration of the staging (nonproduction) slot to use the isolated worker model by setting the

`FUNCTIONS_WORKER_RUNTIME`

application setting to`dotnet-isolated`

.`FUNCTIONS_WORKER_RUNTIME`

should**not**be marked as a*slot setting*.If you're also targeting a different version of .NET as part of your update, you should also change the stack configuration. To do so, see

[Update the stack configuration](update-language-versions?pivots=programming-language-csharp#update-the-stack-configuration). You can use the same instructions for any future .NET version updates you make.If you have any automated infrastructure provisioning such as a CI/CD pipeline, make sure that the automations are also updated to keep

`FUNCTIONS_WORKER_RUNTIME`

set to`dotnet-isolated`

and to target the correct .NET version.Publish your migrated project to the staging (nonproduction) slot of your function app.

If you use Visual Studio to publish an isolated worker model project to an existing app or slot that uses the in-process model, it can also complete the previous step for you at the same time. If you didn't complete the previous step, Visual Studio prompts you to update the function app during deployment. Visual Studio presents this as a single operation, but these are still two separate operations. You might still see errors in your logs from the staging (nonproduction) slot during the interim state.

Confirm that your application is working as expected within the staging (nonproduction) slot.

Perform a

[slot swap operation](functions-deployment-slots#swap-slots)to apply the changes you made in your staging (nonproduction) slot to the production slot. A slot swap happens as a single update, which avoids introducing the interim error state in your production environment.Confirm that your application is working as expected within the production slot.


Once you complete these steps, the migration is complete, and your app runs on the isolated model. Congratulations! Repeat the steps from this guide as necessary for [any other apps that need migration](#identify-function-apps-to-migrate).
