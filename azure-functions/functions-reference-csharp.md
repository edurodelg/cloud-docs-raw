---
source_url: https://learn.microsoft.com/en-us/azure/azure-functions/functions-reference-csharp
fetched_at: 2026-01-25T15:35:13.608797
---

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