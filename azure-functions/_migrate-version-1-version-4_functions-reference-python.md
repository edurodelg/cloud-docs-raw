---
merged_at: 2026-01-25T15:41:11.640091
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: migrate-version-1-version-4.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/migrate-version-1-version-4 -->

# Migrate apps from Azure Functions version 1.x to version 4.x

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Java isn't supported by version 1.x of the Azure Functions runtime. Perhaps you're instead looking to [migrate your Java app from version 3.x to version 4.x](migrate-version-3-version-4). If you're migrating a version 1.x function app, select either C# or JavaScript above.

Important

TypeScript isn't supported by version 1.x of the Azure Functions runtime. Perhaps you're instead looking to [migrate your TypeScript app from version 3.x to version 4.x](migrate-version-3-version-4). If you're migrating a version 1.x function app, select either C# or JavaScript above.

Important

PowerShell isn't supported by version 1.x of the Azure Functions runtime. Perhaps you're instead looking to [migrate your PowerShell app from version 3.x to version 4.x](migrate-version-3-version-4). If you're migrating a version 1.x function app, select either C# or JavaScript above.

Important

Python isn't supported by version 1.x of the Azure Functions runtime. Perhaps you're instead looking to [migrate your Python app from version 3.x to version 4.x](migrate-version-3-version-4). If you're migrating a version 1.x function app, select either C# or JavaScript above.

Important

[Support will end for version 1.x of the Azure Functions runtime on September 14, 2026](https://aka.ms/azure-functions-retirements/hostv1). We highly recommend that you migrate your apps to version 4.x by following the instructions in this article.

This article walks you through the process of safely migrating your function app to run on version 4.x of the Functions runtime. Because project migration instructions are language dependent, make sure to choose your development language from the selector at the [top of the article](#top).

If you are running version 1.x of the runtime in Azure Stack Hub, see [Considerations for Azure Stack Hub](#considerations-for-azure-stack-hub) first.

## Identify function apps to migrate

Run the following PowerShell script in Azure Cloud Shell to generate a list of function apps in your subscription that currently target version 1.x:

```
$FunctionApps = Get-AzFunctionApp
$AppInfo = @{}
foreach ($App in $FunctionApps)
{
$AppSettings = Get-AzFunctionAppSetting -Name $App.Name -ResourceGroupName $App.ResourceGroupName
if ($AppSettings.FUNCTIONS_EXTENSION_VERSION -like '*1*')
{
$AppInfo.Add($App.Name, $AppSettings.FUNCTIONS_EXTENSION_VERSION)
}
}
$AppInfo
```


If you run outside of Cloud Shell, you must first set the active subscription:

```
$Subscription = '<SUBSCRIPTION_ID>'
Set-AzContext -Subscription $Subscription | Out-Null
```


In this example, replace '<SUBSCRIPTION_ID>' with the ID of your subscription.

## Choose your target .NET version

On version 1.x of the Functions runtime, your C# function app targets .NET Framework.

When you migrate your function app, you have the opportunity to choose the target version of .NET. You can update your C# project to one of the following versions of .NET that are supported by Functions version 4.x:

| .NET version |
|
|---|

1,2

[Isolated worker model](dotnet-isolated-process-guide)3[Isolated worker model](dotnet-isolated-process-guide)[Isolated worker model](dotnet-isolated-process-guide),[In-process model](functions-dotnet-class-library)2[See policy](https://dotnet.microsoft.com/platform/support/policy/dotnet-framework)[Isolated worker model](dotnet-isolated-process-guide)1 The [isolated worker model](dotnet-isolated-process-guide) supports Long Term Support (LTS) and Standard Term Support (STS) versions of .NET, as well as .NET Framework. The [in-process model](functions-dotnet-class-library) only supports LTS releases of .NET, ending with .NET 8. For a full feature and functionality comparison between the two models, see [Differences between in-process and isolate worker process .NET Azure Functions](dotnet-isolated-in-process-differences).

2 Support ends for the in-process model on November 10, 2026. For more information, see [this support announcement](https://aka.ms/azure-functions-retirements/in-process-model). For continued full support, you should [migrate your apps to the isolated worker model](migrate-dotnet-to-isolated-model).

3 .NET 9 previously had an expected end-of-support date of May 12, 2026. During the .NET 9 service window, the .NET team extended support for STS versions to 24 months, starting with .NET 9. For more information, see [the blog post](https://devblogs.microsoft.com/dotnet/dotnet-sts-releases-supported-for-24-months/).

Tip

**Unless your app depends on a library or API only available to .NET Framework, we recommend updating to .NET 8 on the isolated worker model.** Many apps on version 1.x target .NET Framework only because that is what was available when they were created. Additional capabilities are available to more recent versions of .NET, and if your app is not forced to stay on .NET Framework due to a dependency, you should target a more recent version. .NET 8 is the fully released version with the longest support window from .NET.

Although you can choose to instead use the in-process model, this is not recommended if it can be avoided. [Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model), so you'll need to move to the isolated worker model before then. Doing so while migrating to version 4.x will decrease the total effort required, and the isolated worker model will give your app [additional benefits](dotnet-isolated-in-process-differences), including the ability to more easily target future versions of .NET. If you are moving to the isolated worker model, the [.NET Upgrade Assistant](/en-us/dotnet/core/porting/upgrade-assistant-overview) can also handle many of the necessary code changes for you.

This guide doesn't present specific examples for .NET 10 (preview) or .NET 9. If you need to target one of those versions, you can adapt the .NET 8 examples.

## Prepare for migration

If you haven't already, identify the list of apps that need to be migrated in your current Azure Subscription by using the [Azure PowerShell](#identify-function-apps-to-migrate).

Before you migrate an app to version 4.x of the Functions runtime, you should do the following tasks:

- Review the list of
[behavior changes after version 1.x](#behavior-changes-after-version-1x). Migrating from version 1.x to version 4.x also can affect bindings. - Complete the steps in
[Migrate your local project](#migrate-your-local-project)to migrate your local project to version 4.x. - After migrating your project, fully test the app locally using version 4.x of the
[Azure Functions Core Tools](functions-run-local). - Update your function app in Azure to the new version. If you need to minimize downtime, consider using a
[staging slot](functions-deployment-slots)to test and verify your migrated app in Azure on the new runtime version. You can then deploy your app with the updated version settings to the production slot. For more information, see[Update using slots](#update-using-slots). - Publish your migrated project to the updated function app.

When you use Visual Studio to publish a version 4.x project to an existing function app at a lower version, you're prompted to let Visual Studio update the function app to version 4.x during deployment. This update uses the same process defined in [Update without slots](#update-without-slots).

## Migrate your local project

The following sections describes the updates you must make to your C# project files to be able to run on one of the supported versions of .NET in Functions version 4.x. The updates shown are ones common to most projects. Your project code could require updates not mentioned in this article, especially when using custom NuGet packages.

Migrating a C# function app from version 1.x to version 4.x of the Functions runtime requires you to make changes to your project code. Many of these changes are a result of changes in the C# language and .NET APIs.

Choose the tab that matches your target version of .NET and the desired process model (in-process or isolated worker process).

Tip

If you are moving to an LTS or STS version of .NET using the isolated worker model, the [.NET Upgrade Assistant](/en-us/dotnet/core/porting/upgrade-assistant-overview) can be used to automatically make many of the changes mentioned in the following sections.

### Project file

The following example is a `.csproj`

project file that runs on version 1.x:

```
<Project Sdk="Microsoft.NET.Sdk">
<PropertyGroup>
<TargetFramework>net48</TargetFramework>
<AzureFunctionsVersion>v1</AzureFunctionsVersion>
</PropertyGroup>
<ItemGroup>
<PackageReference Include="Microsoft.NET.Sdk.Functions" Version="1.0.24" />
</ItemGroup>
<ItemGroup>
<Reference Include="Microsoft.CSharp" />
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


Use one of the following procedures to update this XML file to run in Functions version 4.x:

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


### Package and namespace changes

Based on the model you are migrating to, you might need to update or change the packages your application references. When you adopt the target packages, you then need to update the namespace of using statements and some types you reference. You can see the effect of these namespace changes on `using`

statements in the [HTTP trigger template examples](#http-trigger-template) later in this article.

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

The [Notification Hubs](functions-bindings-notification-hubs) and [Mobile Apps](functions-bindings-mobile-apps) bindings are supported only in version 1.x of the runtime. When upgrading to version 4.x of the runtime, you need to remove these bindings in favor of working with these services directly using their SDKs.

### Program.cs file

In most cases, migrating requires you to add the following program.cs file to your project:

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


This example includes [ASP.NET Core integration](dotnet-isolated-process-guide#aspnet-core-integration) to improve performance and provide a familiar programming model when your app uses HTTP triggers. If you do not intend to use HTTP triggers, you can replace the call to `ConfigureFunctionsWebApplication`

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

### host.json file

Settings in the host.json file apply at the function app level, both locally and in Azure. In version 1.x, your host.json file is either empty or it contains some settings that apply to all functions in the function app. For more information, see [Host.json v1](functions-host-json-v1). If your host.json file has setting values, review the [host.json v2 format](functions-host-json) for any changes.

To run on version 4.x, you must add `"version": "2.0"`

to the host.json file. You should also consider adding `logging`

to your configuration, as in the following examples:

```
{
"version": "2.0",
"logging": {
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"excludedTypes": "Request"
},
"enableLiveMetricsFilters": true
}
}
}
```


The `host.json`

file only controls logging from the Functions host runtime, and in the isolated worker model, some of these logs come from your application directly, giving you more control. See [Managing log levels in the isolated worker model](dotnet-isolated-process-guide#managing-log-levels) for details on how to filter these logs.

### local.settings.json file

The local.settings.json file is only used when running locally. For information, see [Local settings file](functions-develop-local#local-settings-file). In version 1.x, the local.settings.json file has only two required values:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "AzureWebJobsStorageConnectionStringValue",
"AzureWebJobsDashboard": "AzureWebJobsStorageConnectionStringValue"
}
}
```


When you migrate to version 4.x, make sure that your local.settings.json file has at least the following elements:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "AzureWebJobsStorageConnectionStringValue",
"FUNCTIONS_WORKER_RUNTIME": "dotnet-isolated"
}
}
```


Note

When migrating from running in-process to running in an isolated worker process, you need to change the `FUNCTIONS_WORKER_RUNTIME`

value to "dotnet-isolated".

### Class name changes

Some key classes changed names between version 1.x and version 4.x. These changes are a result either of changes in .NET APIs or in differences between in-process and isolated worker process. The following table indicates key .NET classes used by Functions that could change when migrating:

| Version 1.x | .NET 8 |
|---|---|
`FunctionName` (attribute) |
`Function` (attribute) |
`TraceWriter` |
`ILogger<T>` , `ILogger` |
`HttpRequestMessage` |
`HttpRequestData` , `HttpRequest` (using
|
`HttpResponseMessage` |
`HttpResponseData` , `IActionResult` (using
|

There might also be class name differences in bindings. For more information, see the reference articles for the specific bindings.

### Other code changes

This section highlights other code changes to consider as you work through the migration. These changes are not needed by all applications, but you should evaluate if any are relevant to your scenarios. Make sure to check [Behavior changes after version 1.x](#behavior-changes-after-version-1x) for additional changes you might need to make to your project.

#### JSON serialization

By default, the isolated worker model uses *System.Text.Json* for JSON serialization. To customize serializer options or switch to JSON.NET (*Newtonsoft.Json*), see [Customizing JSON serialization](dotnet-isolated-process-guide#customizing-json-serialization).

#### Application Insights log levels and filtering

Logs can be sent to Application Insights from both the Functions host runtime and code in your project. The *host.json* allows you to configure rules for host logging, but to control logs coming from your code, you need to configure filtering rules as part of your *Program.cs*. See [Managing log levels in the isolated worker model](dotnet-isolated-process-guide#managing-log-levels) for details on how to filter these logs.

### HTTP trigger template

Most of the code changes between version 1.x and version 4.x can be seen in HTTP triggered functions. The HTTP trigger template for version 1.x looks like the following example:

```
using System.Linq;
using System.Net;
using System.Net.Http;
using System.Threading.Tasks;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
namespace Company.Function
{
public static class HttpTriggerCSharp
{
[FunctionName("HttpTriggerCSharp")]
public static async Task<HttpResponseMessage>
Run([HttpTrigger(AuthorizationLevel.AuthLevelValue, "get", "post",
Route = null)]HttpRequestMessage req, TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
// parse query parameter
string name = req.GetQueryNameValuePairs()
.FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
.Value;
if (name == null)
{
// Get request body
dynamic data = await req.Content.ReadAsAsync<object>();
name = data?.name;
}
return name == null
? req.CreateResponse(HttpStatusCode.BadRequest,
"Please pass a name on the query string or in the request body")
: req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
}
}
```


In version 4.x, the HTTP trigger template looks like the following example:

```
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.Logging;
namespace Company.Function
{
public class HttpTriggerCSharp
{
private readonly ILogger<HttpTriggerCSharp> _logger;
public HttpTriggerCSharp(ILogger<HttpTriggerCSharp> logger)
{
_logger = logger;
}
[Function("HttpTriggerCSharp")]
public IActionResult Run(
[HttpTrigger(AuthorizationLevel.Function, "get")] HttpRequest req)
{
_logger.LogInformation("C# HTTP trigger function processed a request.");
return new OkObjectResult($"Welcome to Azure Functions, {req.Query["name"]}!");
}
}
}
```


To update your project to Azure Functions 4.x:

Update your local installation of

[Azure Functions Core Tools](functions-run-local#install-the-azure-functions-core-tools)to version 4.x.Move to one of the

[Node.js versions supported on version 4.x](functions-reference-node#node-version).Add both

`version`

and`extensionBundle`

elements to the host.json, so that it looks like the following example:`{ "version": "2.0", "extensionBundle": { "id": "Microsoft.Azure.Functions.ExtensionBundle", "version": "[3.3.0, 4.0.0)" } }`

The

`extensionBundle`

element is required because after version 1.x, bindings are maintained as external packages. For more information, see[Extension bundles](extension-bundles).Update your local.settings.json file so that it has at least the following elements:

`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "node" } }`

The

`AzureWebJobsStorage`

setting can be either the Azurite storage emulator or an actual Azure storage account. For more information, see[Local storage emulator](functions-develop-local#local-storage-emulator).

## Update your function app in Azure

You need to update the runtime of the function app host in Azure to version 4.x before you publish your migrated project. The runtime version used by the Functions host is controlled by the `FUNCTIONS_EXTENSION_VERSION`

application setting, but in some cases other settings must also be updated. Both code changes and changes to application settings require your function app to restart.

The easiest way is to [update without slots](#update-without-slots) and then republish your app project. You can also minimize the downtime in your app and simplify rollback by [updating using slots](#update-using-slots).

### Update without slots

The simplest way to update to v4.x is to set the `FUNCTIONS_EXTENSION_VERSION`

application setting to `~4`

on your function app in Azure. You must follow a [different procedure](#update-using-slots) on a site with slots.

```
az functionapp config appsettings set --settings FUNCTIONS_EXTENSION_VERSION=~4 -g <RESOURCE_GROUP_NAME> -n <APP_NAME>
```


You must also set another setting, which differs between Windows and Linux.

When running on Windows, you also need to enable .NET 8.0, which is required by version 4.x of the runtime.

```
az functionapp config set --net-framework-version v8.0 -g <RESOURCE_GROUP_NAME> -n <APP_NAME>
```


.NET 6 is required for function apps in any language running on Windows.

In this example, replace `<APP_NAME>`

with the name of your function app and `<RESOURCE_GROUP_NAME>`

with the name of the resource group.

You can now republish your app project that has been migrated to run on version 4.x.

### Update using slots

Using [deployment slots](functions-deployment-slots) is a good way to update your function app to the v4.x runtime from a previous version. By using a staging slot, you can run your app on the new runtime version in the staging slot and switch to production after verification. Slots also provide a way to minimize downtime during the update. If you need to minimize downtime, follow the steps in [Minimum downtime update](#minimum-downtime-update).

After you've verified your app in the updated slot, you can swap the app and new version settings into production. This swap requires setting [ WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0](functions-app-settings#website_override_sticky_extension_versions) in the production slot. How you add this setting affects the amount of downtime required for the update.

#### Standard update

If your slot-enabled function app can handle the downtime of a full restart, you can update the `WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS`

setting directly in the production slot. Because changing this setting directly in the production slot causes a restart that impacts availability, consider doing this change at a time of reduced traffic. You can then swap in the updated version from the staging slot.

The [ Update-AzFunctionAppSetting](/en-us/powershell/module/az.functions/update-azfunctionappsetting) PowerShell cmdlet doesn't currently support slots. You must use Azure CLI or the Azure portal.

Use the following command to set

`WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0`

in the production slot:`az functionapp config appsettings set --settings WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0 -g <RESOURCE_GROUP_NAME> -n <APP_NAME>`

In this example, replace

`<APP_NAME>`

with the name of your function app and`<RESOURCE_GROUP_NAME>`

with the name of the resource group. This command causes the app running in the production slot to restart.Use the following command to also set

`WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS`

in the staging slot:`az functionapp config appsettings set --settings WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0 -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME>`

Use the following command to change

`FUNCTIONS_EXTENSION_VERSION`

and update the staging slot to the new runtime version:`az functionapp config appsettings set --settings FUNCTIONS_EXTENSION_VERSION=~4 -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME>`

Version 4.x of the Functions runtime requires .NET 6 in Windows. On Linux, .NET apps must also update to .NET 6. Use the following command so that the runtime can run on .NET 6:

When running on Windows, you also need to enable .NET 8.0, which is required by version 4.x of the runtime.

`az functionapp config set --net-framework-version v8.0 -g <RESOURCE_GROUP_NAME> -n <APP_NAME>`

.NET 6 is required for function apps in any language running on Windows.

In this example, replace

`<APP_NAME>`

with the name of your function app and`<RESOURCE_GROUP_NAME>`

with the name of the resource group.If your code project required any updates to run on version 4.x, deploy those updates to the staging slot now.

Confirm that your function app runs correctly in the updated staging environment before swapping.

Use the following command to swap the updated staging slot to production:

`az functionapp deployment slot swap -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME> --target-slot production`


#### Minimum downtime update

To minimize the downtime in your production app, you can swap the `WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS`

setting from the staging slot into production. After that, you can swap in the updated version from a prewarmed staging slot.

Use the following command to set

`WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0`

in the staging slot:`az functionapp config appsettings set --settings WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0 -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME>`

Use the following commands to swap the slot with the new setting into production, and at the same time restore the version setting in the staging slot.

`az functionapp deployment slot swap -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME> --target-slot production az functionapp config appsettings set --settings FUNCTIONS_EXTENSION_VERSION=~3 -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME>`

You may see errors from the staging slot during the time between the swap and the runtime version being restored on staging. This error can happen because having

`WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0`

only in staging during a swap removes the`FUNCTIONS_EXTENSION_VERSION`

setting in staging. Without the version setting, your slot is in a bad state. Updating the version in the staging slot right after the swap should put the slot back into a good state, and you call roll back your changes if needed. However, any rollback of the swap also requires you to directly remove`WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0`

from production before the swap back to prevent the same errors in production seen in staging. This change in the production setting would then cause a restart.Use the following command to again set

`WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0`

in the staging slot:`az functionapp config appsettings set --settings WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0 -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME>`

At this point, both slots have

`WEBSITE_OVERRIDE_STICKY_EXTENSION_VERSIONS=0`

set.Use the following command to change

`FUNCTIONS_EXTENSION_VERSION`

and update the staging slot to the new runtime version:`az functionapp config appsettings set --settings FUNCTIONS_EXTENSION_VERSION=~4 -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME>`

Version 4.x of the Functions runtime requires .NET 6 in Windows. On Linux, .NET apps must also update to .NET 6. Use the following command so that the runtime can run on .NET 6:

When running on Windows, you also need to enable .NET 8.0, which is required by version 4.x of the runtime.

`az functionapp config set --net-framework-version v8.0 -g <RESOURCE_GROUP_NAME> -n <APP_NAME>`

.NET 6 is required for function apps in any language running on Windows.

In this example, replace

`<APP_NAME>`

with the name of your function app and`<RESOURCE_GROUP_NAME>`

with the name of the resource group.If your code project required any updates to run on version 4.x, deploy those updates to the staging slot now.

Confirm that your function app runs correctly in the updated staging environment before swapping.

Use the following command to swap the updated and prewarmed staging slot to production:

`az functionapp deployment slot swap -g <RESOURCE_GROUP_NAME> -n <APP_NAME> --slot <SLOT_NAME> --target-slot production`


## Behavior changes after version 1.x

This section details changes made after version 1.x in both trigger and binding behaviors as well as in core Functions features and behaviors.

### Changes in triggers and bindings

Starting with version 2.x, you must install the extensions for specific triggers and bindings used by the functions in your app. The only exception for this HTTP and timer triggers, which don't require an extension. For more information, see [Register and install binding extensions](functions-bindings-register).

There are also a few changes in the *function.json* or attributes of the function between versions. For example, the Event Hubs `path`

property is now `eventHubName`

. See the [existing binding table](functions-versions#bindings) for links to documentation for each binding.

### Changes in features and functionality

A few features were removed, updated, or replaced after version 1.x. This section details the changes you see in later versions after having used version 1.x.

In version 2.x, the following changes were made:

Keys for calling HTTP endpoints are always stored encrypted in Azure Blob storage. In version 1.x, keys were stored in Azure Files by default. When you migrate an app from version 1.x to version 2.x, existing secrets that are in Azure Files are reset.

The version 2.x runtime doesn't include built-in support for webhook providers. This change was made to improve performance. You can still use HTTP triggers as endpoints for webhooks.

To improve monitoring, the WebJobs dashboard in the portal, which used the

setting is replaced with Azure Application Insights, which uses the`AzureWebJobsDashboard`

setting. For more information, see`APPINSIGHTS_INSTRUMENTATIONKEY`

[Monitor Azure Functions](functions-monitoring).All functions in a function app must share the same language. When you create a function app, you must choose a runtime stack for the app. The runtime stack is specified by the

value in application settings. This requirement was added to improve footprint and startup time. When developing locally, you must also include this setting in the`FUNCTIONS_WORKER_RUNTIME`

[local.settings.json file](functions-develop-local#local-settings-file).The default timeout for functions in an App Service plan is changed to 30 minutes. You can manually change the timeout back to unlimited by using the

[functionTimeout](functions-host-json#functiontimeout)setting in host.json.HTTP concurrency throttles are implemented by default for Consumption plan functions, with a default of 100 concurrent requests per instance. You can change this behavior in the

setting in the host.json file.`maxConcurrentRequests`

Because of

[.NET Core limitations](https://github.com/Azure/azure-functions-host/issues/3414), support for F# script (`.fsx`

files) functions has been removed. Compiled F# functions (.fs) are still supported.The URL format of Event Grid trigger webhooks has been changed to follow this pattern:

`https://{app}/runtime/webhooks/{triggerName}`

.The names of some

[pre-defined custom metrics](analyze-telemetry-data)were changed after version 1.x.`Duration`

was replaced with`MaxDurationMs`

,`MinDurationMs`

, and`AvgDurationMs`

.`Success Rate`

was also renamed to`Success Rate`

.

## Considerations for Azure Stack Hub

[App Service on Azure Stack Hub](/en-us/azure-stack/operator/azure-stack-app-service-overview) does not support version 4.x of Azure Functions. When you are planning a migration off of version 1.x in Azure Stack Hub, you can choose one of the following options:

- Migrate to version 4.x hosted in public cloud Azure Functions using the instructions in this article. Instead of upgrading your existing app, you would create a new app using version 4.x and then deploy your modified project to it.
- Switch to
[WebJobs](../app-service/webjobs-create)hosted on an App Service plan in Azure Stack Hub.


---

<!-- DOCUMENTO FUSIONADO: functions-reference-python.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-reference-python -->

# Azure Functions developer reference guide for Python apps

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions is a serverless compute service that enables you to run event-driven code without provisioning or managing infrastructure. Function executions are triggered by events such as HTTP requests, queue messages, timers, or changes in storage—and scale automatically based on demand.

This guide focuses specifically on building Python-based Azure Functions and helps you:

- Create and run function apps locally
- Understand the Python programming model
- Organize and configure your application
- Deploy and monitor your app in Azure
- Apply best practices for scaling and performance

Looking for a conceptual overview? See the

[Azure Functions Developer Reference].Interested in real-world use cases? Explore the

[Scenarios & Samples]page.

## Getting started

Choose the environment that fits your workflow and jump into Azure Functions for Python:

## Building your function app

This section covers the essential components for creating and structuring your Python function app. Topics include the [programming model](#programming-model), [project structure](#folder-structure), [triggers and bindings](#triggers-and-bindings), and [dependency management](#package-management).

### Programming model

Functions supports two versions of the Python programming model:

| Version | Description |
|---|---|
| 2.x | Use a decorator-based approach to define triggers and bindings directly in your Python code file. You implement each function as a global, stateless method in a `function_app.py` file or a referenced blueprint file. This model version is recommended for new Python apps. |
| 1.x | You define triggers and bindings for each function in a separate `function.json` file. You implement each function as a global, stateless method in your Python code file. This version of the model supports legacy apps. |

This article targets a specific Python model version. Choose your desired version at the [top of the article](#top).

Important

Use the v2 programming model for a **decorator-based approach** to define triggers and bindings directly in your code.

In the Python v1 programming model, each function is defined as a global, stateless `main()`

method inside a file named `__init__.py`

.
The function’s triggers and bindings are configured separately in a `function.json`

file, and the binding `name`

values are used as parameters in your `main()`

method.

**Example**

Here's a simple function that responds to an HTTP request:

```
# __init__.py
def main(req):
user = req.params.get('user')
return f'Hello, {user}!'
```


Here's the corresponding `function.json`

file:

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
}
]
}
```


#### Key concepts

- The function has a single HTTP trigger.
- The
[HttpRequest](/en-us/python/api/azure-functions/azure.functions.httprequest)object contains request headers, query parameters, route parameters, and the message body. This function gets the value of the`name`

query parameter from the`params`

parameter of the[HttpRequest](/en-us/python/api/azure-functions/azure.functions.httprequest)object. - To send a name in this example, append
`?name={name}`

to the exposed function URL. For example, if running locally, the full URL might look like`http://localhost:7071/api/http_trigger?name=Test`

. For examples using bindings, see[Triggers and Bindings](#triggers-and-bindings).

Use the `azure-functions`

SDK and include **type annotations** to improve IntelliSense and editor support:

```
# __init__.py
import azure.functions as func
def http_trigger(req: func.HttpRequest) -> str:
```


```
# requirements.txt
azure-functions
```


#### The `azure-functions`

library

The `azure-functions`

Python library provides the core types used to interact with the Azure Functions runtime. To see all types and methods available, visit the [ azure-functions API](/en-us/python/api/azure-functions/).
Your function code can use

`azure-functions`

to:- Access trigger input data (for example,
`HttpRequest`

,`TimerRequest`

) - Create output values (such as
`HttpResponse`

) - Interact with runtime-provided context and binding data

If you're using `azure-functions`

in your app, it must be included in your project dependencies.

Note

The `azure-functions`

library defines the programming surface for Python Azure Functions, but it isn’t a general-purpose SDK. Use it specifically for authoring and running functions within the Azure Functions runtime.

### Alternative entry point

You can change the default behavior of a function by specifying the `scriptFile`

and `entryPoint`

properties in the `function.json`

file. For example,
the following `function.json`

file directs the runtime to use the `custom_entry()`

method in the `main.py`

file as the entry point for your Azure function.

```
{
"scriptFile": "main.py",
"entryPoint": "custom_entry",
"bindings": [
...
]
}
```


### Folder structure

Use the following structure for a Python Azure Functions project:

```
<project_root>/
│
├── .venv/ # (Optional) Local Python virtual environment
├── .vscode/ # (Optional) VS Code workspace settings
│
├── my_first_function/ # Function directory
│ └── __init__.py # Function code file
│ └── function.json # Function binding configuration file
│
├── my_second_function/
│ └── __init__.py
│ └── function.json
│
├── shared/ # (Optional) Pure helper code with no triggers/bindings
│ └── utils.py
│
├── additional_functions/ # (Optional) Contains blueprints for organizing related Functions
│ └── blueprint_1.py
│
├── tests/ # (Optional) Unit tests for your functions
│ └── test_my_function.py
│
├── .funcignore # Excludes files from being published
├── host.json # Global function app configuration
├── local.settings.json # Local-only app settings (not published)
├── requirements.txt # (Optional) Defines Python dependencies for remote build
├── Dockerfile # (Optional) For custom container deployment
```


#### Key files and folders

| File / Folder | Description | Required for app to run in Azure |
|---|---|---|
`my_first_function/` |
Directory for a single function. | ✅ |
`__init__.py/` |
Main script where the `my_first_function` function code is defined. |
✅ |
`function.json/` |
Contains the binding configuration for the `my_first_function` function. |
✅ |
`host.json` |
Global configuration for all functions in the app. | ✅ |
`requirements.txt` |
Python dependencies installed during publish when using
|

`local.settings.json`

`.funcignore`

`.venv/`

, `tests/`

, `local.settings.json`

).`.venv/`

`.vscode/`

`shared/`

`additional_functions/`

[blueprints](#organizing-with-blueprints).`tests/`

`Dockerfile`

In the Python v2 programming model, Azure Functions uses a **decorator-based approach** to define triggers and bindings directly in your code. Each function is implemented as a **global, stateless method** within a `function_app.py`

file.

**Example**

Here's a simple function that responds to an HTTP request:

```
import azure.functions as func
app = func.FunctionApp()
@app.route("hello")
def http_trigger(req):
user = req.params.get("user")
return f"Hello, {user}!"
```


```
# requirements.txt
azure-functions
```


#### Key concepts

- The code imports the
`azure-functions`

package and uses decorators and types to define the function app. - The function has a single HTTP trigger.
- The
[HttpRequest](/en-us/python/api/azure-functions/azure.functions.httprequest)object contains request headers, query parameters, route parameters, and the message body. This function gets the value of the`name`

query parameter from the`params`

parameter of the[HttpRequest](/en-us/python/api/azure-functions/azure.functions.httprequest)object. - To send a name in this example, append
`?name={name}`

to the exposed function URL. For example, if running locally, the full URL might look like`http://localhost:7071/api/http_trigger?name=Test`

. For examples using bindings, see[Triggers and Bindings](#triggers-and-bindings).

#### The `azure-functions`

library

The `azure-functions`

Python library is a core part of the Azure Functions programming model. It provides the decorators, trigger and binding types, and request/response objects used to define and interact with functions at runtime.
To see all types and decorators available, visit the [ azure-functions API](/en-us/python/api/azure-functions/).
Your function app code depends on this library to:

- Define all functions using the
`FunctionApp`

object - Declare triggers and bindings (for example,
`@app.route`

,`@app.timer_trigger`

) - Access typed inputs and outputs (such as
`HttpRequest`

and`HttpResponse`

, and Out`)

The `azure-functions`

must be included in your project dependencies. To learn more, see [package management](#package-management).

Note

The `azure-functions`

library defines the programming surface for Python Azure Functions, but it isn’t a general-purpose SDK. Use it specifically for authoring and running functions within the Azure Functions runtime.

Use **type annotations** to improve IntelliSense and editor support:

```
def http_trigger(req: func.HttpRequest) -> str:
```


### Organizing with blueprints

For larger or modular apps, use *blueprints* to define functions in separate Python files
and register them with your main app. This separation keeps your code organized and reusable.

To define and register a blueprint:

Define a blueprint in another Python file, such as

`http_blueprint.py`

:`import azure.functions as func bp = func.Blueprint() @bp.route(route="default_template") def default_template(req: func.HttpRequest) -> func.HttpResponse: return func.HttpResponse("Hello World!")`

Register the blueprint in main

`function_app.py`

file:`import azure.functions as func from http_blueprint import bp app = func.FunctionApp() app.register_functions(bp)`


By using blueprints, you can:

- Break up your app into reusable modules
- Keep related functions grouped by file or feature
- Extend or share blueprints across projects

Note

Durable Functions also supports blueprints by using [ azure-functions-durable](https://pypi.org/project/azure-functions-durable).

[View sample →](https://github.com/Azure/azure-functions-durable-python/tree/dev/samples-v2/blueprint)

### Folder structure

Use the following structure for a Python Azure Functions project:

```
<project_root>/
│
├── .venv/ # (Optional) Local Python virtual environment
├── .vscode/ # (Optional) VS Code workspace settings
│
├── function_app.py # Main function entry point (decorator model)
├── shared/ # (Optional) Pure helper code with no triggers/bindings
│ └── utils.py
│
├── additional_functions/ # (Optional) Contains blueprints for organizing related Functions
│ └── blueprint_1.py
│
├── tests/ # (Optional) Unit tests for your functions
│ └── test_my_function.py
│
├── .funcignore # Excludes files from being published
├── host.json # Global function app configuration
├── local.settings.json # Local-only app settings (not published)
├── requirements.txt # (Optional) Defines Python dependencies for remote build
├── Dockerfile # (Optional) For custom container deployment
```


#### Key files and folders

| File / Folder | Description | Required for app to run in Azure |
|---|---|---|
`function_app.py` |
Main script where Azure Functions and triggers are defined using decorators. | ✅ |
`host.json` |
Global configuration for all functions in the app. | ✅ |
`requirements.txt` |
Python dependencies installed during publish when using
|

`local.settings.json`

`.funcignore`

`.venv/`

, `tests/`

, `local.settings.json`

).`.venv/`

`.vscode/`

`shared/`

`additional_functions/`

[blueprints](#organizing-with-blueprints).`tests/`

`Dockerfile`

[NOTE!] Include a

`requirements.txt`

file when you deploy with[remote build]. If you don't use remote build or want to use another file for defining app dependencies, you can perform a[local build]and deploy the app with pre-built dependencies.

For guidance on unit testing, see

[Unit Testing]. For container deployments, see[Deploy with custom containers].

### Triggers and bindings

Azure Functions uses **triggers** to start function execution and **bindings** to connect your code to other services
like storage, queues, and databases. In the Python v2 programming model, you declare bindings by using decorators.

Two main types of bindings exist:

**Triggers**(input that starts the function)**Inputs and outputs**(extra data sources or destinations)

For more information about the available triggers and bindings, see [Triggers and Bindings in Azure Functions](functions-triggers-bindings).

#### Example: Timer Trigger with Blob Input

This function:

- Triggers every 10 minutes
- Reads from a Blob by using
[SDK Type Bindings](#sdk-type-bindings) - Caches results and writes to a temporary file

```
import azure.functions as func
import azurefunctions.extensions.bindings.blob as blob
import logging
import tempfile
CACHED_BLOB_DATA = None
app = func.FunctionApp()
@app.function_name(name="TimerTriggerWithBlob")
@app.schedule(schedule="0 */10 * * * *", arg_name="mytimer")
@app.blob_input(arg_name="client",
path="PATH/TO/BLOB",
connection="BLOB_CONNECTION_SETTING")
def timer_trigger_with_blob(mytimer: func.TimerRequest,
client: blob.BlobClient,
context: func.Context) -> None:
global CACHED_BLOB_DATA
if CACHED_BLOB_DATA is None:
# Download blob and save as a global variable
CACHED_BLOB_DATA = client.download_blob().readall()
# Create temp file prefix
my_prefix = context.invocation_id
temp_file = tempfile.NamedTemporaryFile(prefix=my_prefix)
temp_file.write(CACHED_BLOB_DATA)
logging.info(f"Cached data written to {temp_file.name}")
```


#### Key concepts

- Use SDK type bindings to work with rich types. For more information, see
[SDK type bindings](#sdk-type-bindings). - You can use global variables to cache expensive computations, but their state isn't guaranteed to persist across function executions.
- Temporary files are stored in
`tmp/`

and aren't guaranteed to persist across invocations or scale-out instances. - You can access the invocation context of a function through the
[Context class](/en-us/python/api/azure-functions/azure.functions.context).

#### Example: HTTP Trigger with Cosmos DB Input and Event Hub Output

This function:

- Triggers on an HTTP request
- Reads from a Cosmos DB
- Writes to an Event Hub output
- Returns an HTTP response

```
# __init__.py
import azure.functions as func
def main(req: func.HttpRequest,
documents: func.DocumentList,
event: func.Out[str]) -> func.HttpResponse:
# Content from HttpRequest and Cosmos DB input
http_content = req.params.get("body")
doc_id = documents[0]["id"] if documents else "No documents found"
event.set(f"HttpRequest content: {http_content} | CosmosDB ID: {doc_id}")
return func.HttpResponse(
"Function executed successfully.",
status_code=200
)
```


```
// function.json
{
"scriptFile": "__init__.py",
"entryPoint": "main",
"bindings": [
{
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": ["get", "post"],
"route": "file"
},
{
"type": "http",
"direction": "out",
"name": "$return"
},
{
"type": "cosmosDB",
"direction": "in",
"name": "documents",
"databaseName": "test",
"containerName": "items",
"id": "cosmosdb-input-test",
"connection": "COSMOSDB_CONNECTION_SETTING"
},
{
"type": "eventHub",
"direction": "out",
"name": "event",
"eventHubName": "my-test-eventhub",
"connection": "EVENTHUB_CONNECTION_SETTING"
}
]
}
```


**Key concepts**

- Each function has a single trigger, but it can have multiple bindings.
- Add inputs by specifying the
`direction`

as "in" in`function.json`

. Outputs have a`direction`

of`out`

. - You can access request details through the
`HttpRequest`

object and construct a custom`HttpResponse`

with headers, status code, and body.

```
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="HttpTriggerWithCosmosDB")
@app.route(route="file")
@app.cosmos_db_input(arg_name="documents",
database_name="test",
container_name="items",
connection="COSMOSDB_CONNECTION_SETTING")
@app.event_hub_output(arg_name="event",
event_hub_name="my-test-eventhub",
connection="EVENTHUB_CONNECTION_SETTING")
def http_trigger_with_cosmosdb(req: func.HttpRequest,
documents: func.DocumentList,
event: func.Out[str]) -> func.HttpResponse:
# Content from HttpRequest and Cosmos DB input
http_content = req.params.get('body')
doc_id = documents[0]['id']
event.set("HttpRequest content: " + http_content
+ " | CosmosDB ID: " + doc_id)
return func.HttpResponse(
f"Function executed successfully.",
status_code=200
)
```


#### Key concepts

- Use
`@route()`

or trigger-specific decorators (`@timer_trigger`

,`@queue_trigger`

, and others) to define how your function is invoked. - Add inputs by using decorators like
`@blob_input`

,`@queue_input`

, and others. - Outputs can be:
- Returned directly (if only one output)
- Assigned by using
`Out`

bindings and the`.set()`

method for multiple outputs.

- You can access request details through the
`HttpRequest`

object and construct a custom`HttpResponse`

with headers, status code, and body.

### SDK type bindings

For select triggers and bindings, you can work with data types implemented by the underlying Azure SDKs and frameworks.
By using these *SDK type bindings*, you can interact with binding data as if you were using the underlying service SDK.
For more information, see [supported SDK type bindings](functions-triggers-bindings?pivots=programming-language-python#sdk-types).

Important

SDK type bindings support for Python is only available in the Python v2 programming model.

### Environment variables

Environment variables in Azure Functions let you securely manage configuration values, connection strings, and app secrets without hardcoding them in your function code.

You can define environment variables:

- Locally: in the
[local.settings.json file](functions-develop-local#local-settings-file), during local development. - In Azure: as
[Application Settings](functions-how-to-use-azure-function-app-settings#settings)in your Function App's configuration page in the Azure portal.

Access the variables directly in your code by using `os.environ`

or `os.getenv`

.

```
setting_value = os.getenv("myAppSetting", "default_value")
```


Note

Azure Functions also recognizes system environment variables that configure the Functions runtime and Python worker behavior. These variables aren't explicitly used in your function code but affect how your app runs. For a complete list of system environment variables, see [App settings reference](functions-app-settings).

### Package management

To use other Python packages in your Azure Functions app, list them in a `requirements.txt`

file at the root of your project. These packages are imported by Python's import system, and you can then reference those packages as usual.
To learn more about building and deployment options with external dependencies, see [Build Options for Python Function Apps](python-build-options).

For example, the following sample shows how the `requests`

module is included and used in the function app.

```
<requirements.txt>
requests==2.31.0
```


Install the package locally with `pip install -r requirements.txt`

.

Once the package is installed, you can import and use it in your function code:

```
import azure.functions as func
import requests
def main(req: func.HttpRequest) -> func.HttpResponse:
r = requests.get("https://api.github.com")
return func.HttpResponse(f"Status: {r.status_code}")
```


```
import azure.functions as func
import requests
app = func.FunctionApp()
@app.function_name(name="HttpExample")
@app.route(route="call_api")
def main(req: func.HttpRequest) -> func.HttpResponse:
r = requests.get("https://api.github.com")
return func.HttpResponse(f"Status: {r.status_code}")
```


#### Considerations

- Conflicts with built-in modules:
- Avoid naming your project folders after
[Python standard libraries](https://docs.python.org/3/library/)(for example,`email/`

,`json/`

). - Don't include Python native libraries (like
`logging`

,`asyncio`

, or`uuid`

) in`requirements.txt`

.

- Avoid naming your project folders after
- Deployment:
- To prevent
, ensure all required dependencies are listed in`ModuleNotFound`

errors`requirements.txt`

. - If you update your app's Python version, rebuild and redeploy your app on the new Python version to avoid dependency conflicts with previously built packages.

- To prevent
- Non-PyPI Dependencies:
- You can include dependencies that aren't available on PyPI in your app, such as local packages, wheel files, or private feeds. See
[Custom dependencies in Python Azure Functions](python-build-options#custom-dependencies)for setup instructions.

- You can include dependencies that aren't available on PyPI in your app, such as local packages, wheel files, or private feeds. See
- Azure Functions Python worker dependencies:
- If your package contains certain libraries that might collide with worker's dependencies (for example,
`protobuf`

or`grpcio`

), configure[PYTHON_ISOLATE_WORKER_DEPENDENCIES](functions-app-settings#python_isolate_worker_dependencies)to 1 in app settings to prevent your application from referring to worker's dependencies. For Python 3.13 and above,[this feature is enabled by default](#python-313-updates).

- If your package contains certain libraries that might collide with worker's dependencies (for example,

## Running and deploying

This section provides information about [running functions locally](#running-locally), [Python version support](#supported-python-versions), [build and deployment options](#build-and-deployment), and runtime configuration. Use this information to successfully run your function app in both local and Azure environments.

### Running locally

You can run and test your Python function app on your local machine before deploying to Azure.

#### Using Azure Functions Core Tools

Install [Azure Functions Core Tools](functions-run-local) and start the local runtime by running the `func start`

command from your project root:

```
func start
```


When you start the function app locally, Core Tools displays all the functions it finds for your app:

```
Functions:
http_trigger: http://localhost:7071/api/http_trigger
```


You can learn more about how to use Core Tools by visiting [Develop Azure Functions locally using Core Tools](functions-run-local).

#### Invoking the function directly

By using `azure-functions >= 1.21.0`

, you can also call functions directly by using the Python interpreter without running Core Tools. This approach is useful for quick unit tests:

```
# function_app.py
import azure.functions as func
app = func.FunctionApp(http_auth_level=func.AuthLevel.ANONYMOUS)
@app.route(route="http_trigger")
def http_trigger(req: func.HttpRequest) -> func.HttpResponse:
return "Hello, World!"
# Test the function directly
print(http_trigger(None))
```


To see the output, run the file directly with Python:

```
> python function_app.py
Hello, World!
```


```
# __init__.py
import azure.functions as func
def main(req: func.HttpRequest) -> func.HttpResponse:
return func.HttpResponse("Hello, World!")
# Test the function directly
print(main(None))
```


To see the output, run the file directly with Python:

```
> python __init__.py
Hello, World!
```


This approach doesn't require any extra packages or setup and is ideal for quick validation during development. For more in-depth testing, see [Unit Testing](#unit-testing)

### Supported Python versions

Azure Functions supports the Python versions listed in [Supported languages in Azure Functions](supported-languages).
For more general information, see the [Azure Functions runtime support policy](language-support-policy).

Important

If you change the Python version for your function app, you must rebuild and redeploy the app by using the new version. Existing deployment artifacts and dependencies aren't automatically rebuilt when the Python version changes.

## Build and Deployment

To learn more about the recommended build mechanism for your scenario, see [Build Options](python-build-options). For a general overview of deployment, see [Deployment technologies in Azure Functions](functions-deployment-technologies).

**Deployment Mechanisms Quick Comparison**

Tool / Platform |
Command / Action |
Best Use Case |
|---|---|---|
Azure Functions Core Tools |

`func azure functionapp publish <APP_NAME>`

**AZ CLI**`az functionapp deployment source config-zip`

**Visual Studio Code (Azure Functions Extension)****Command Palette → “Azure Functions: Deploy to Azure…”****GitHub Actions**`Azure/functions-action@v1`

**Azure Pipelines**`AzureFunctionApp@2`

task**Custom Container Deployment**`az functionapp create --image <container>`

**Portal-based Function Creation**[Azure portal](https://portal.azure.com)→ inline editor**simple**, dependency-free functions. Great for demos or learning, but**not recommended**for apps requiring third-party packages.Note

[ Portal-based Function Creation](functions-create-function-app-portal) doesn't support third-party dependencies and isn't recommended for creating production apps. You can't install or reference packages outside

`azure-functions`

and the built-in Python standard library.Important

After 30 September 2028, the option to host your function app on Linux in a Consumption plan is retired. To avoid disruptions, migrate your existing Consumption plan apps that run on Linux to the [Flex Consumption plan](flex-consumption-plan) before that date. Apps running on Windows in a Consumption plan aren't affected by this change.
For more information, see the [Linux Consumption plan retirement notice](https://go.microsoft.com/fwlink/?linkid=2335809).

### Python 3.13+ updates

Starting with Python 3.13, Azure Functions introduces several major runtime and performance improvements that affect how you build and run your apps. Key changes include:

Runtime version control: You can now optionally pin or upgrade your app to specific Python worker versions by referencing the

package in your`azure-functions-runtime`

`requirements.txt`

.Without version control enabled, your app runs on a default version of the Python runtime, which Functions manages. You must modify your

*requirements.txt*file to request the latest released version, a prereleased version, or to pin your app to a specific version of the Python runtime.You enable runtime version control by adding a reference to the Python runtime package to your

*requirements.txt*file, where the value assigned to the package determines the runtime version used.Avoid pinning any production app to prerelease (alpha, beta, or dev) runtime versions.

To be aware of changes, review

[Python runtime release notes](https://github.com/Azure/azure-functions-python-worker/releases)regularly.The following table indicates the versioning behavior based on the version value of this setting in your

*requirements.txt*file:Version Example Behavior No value set `azure-functions-runtime`

Your Python 3.13+ app runs on the latest available version of the Functions Python runtime. This option is best for staying current with platform improvements and features, since your app automatically receives the latest stable runtime updates. Pinned to a specific version `azure-functions-runtime==1.2.0`

Your Python 3.13+ app stays on the pinned runtime version and doesn't receive automatic updates. You must instead manually update your pinned version to take advantage of new features, fixes, and improvements in the runtime. Pinning is recommended for critical production workloads where stability and predictability are essential. Pinning also lets you test your app on prereleased runtime versions during development. No package reference n/a By not setting the `azure-functions-runtime`

, your Python 3.13+ app runs on a default version of the Python runtime that is behind the latest released version. Updates are made periodically by Functions. This option ensures stability and broad compatibility. However, access to the newest features and fixes are delayed until the default version is updated.

Dependency isolation: Your app’s dependencies (like

`grpcio`

or`protobuf`

) are fully isolated from the worker’s dependencies, preventing version conflicts. The app settingwill have no impact for apps running on Python 3.13 or later.`PYTHON_ISOLATE_WORKER_DEPENDENCIES`

Simplified

[HTTP streaming](functions-bindings-http-webhook-trigger?tabs=python-v2&pivots=programming-language-python#http-streams-1)setup—no special app settings required.Removed support for worker extensions and shared memory features.


Runtime version control: You can now optionally pin or upgrade your app to specific Python worker versions by referencing the

package in your`azure-functions-runtime-v1`

`requirements.txt`

.Without version control enabled, your app runs on a default version of the Python runtime, which Functions manages. You must modify your

*requirements.txt*file to request the latest released version, a prereleased version, or to pin your app to a specific version of the Python runtime.You enable runtime version control by adding a reference to the Python runtime package to your

*requirements.txt*file, where the value assigned to the package determines the runtime version used.Avoid pinning any production app to prerelease (alpha, beta, or dev) runtime versions.

To be aware of changes, review

[Python runtime release notes](https://github.com/Azure/azure-functions-python-worker/releases)regularly.The following table indicates the versioning behavior based on the version value of this setting in your

*requirements.txt*file:Version Example Behavior No value set `azure-functions-runtime-v1`

Your Python 3.13+ app runs on the latest available version of the Functions Python runtime. This option is best for staying current with platform improvements and features, since your app automatically receives the latest stable runtime updates. Pinned to a specific version `azure-functions-runtime-v1==1.2.0`

Your Python 3.13+ app stays on the pinned runtime version and doesn't receive automatic updates. You must instead manually update your pinned version to take advantage of new features, fixes, and improvements in the runtime. Pinning is recommended for critical production workloads where stability and predictability are essential. Pinning also lets you test your app on prereleased runtime versions during development. No package reference n/a By not setting the `azure-functions-runtime-v1`

, your Python 3.13+ app runs on a default version of the Python runtime that is behind the latest released version. Updates are made periodically by Functions. This option ensures stability and broad compatibility. However, access to the newest features and fixes are delayed until the default version is updated.

Dependency isolation: Your app’s dependencies (like

`grpcio`

or`protobuf`

) are fully isolated from the worker’s dependencies, preventing version conflicts. The app settingwill have no impact for apps running on Python 3.13 or later.`PYTHON_ISOLATE_WORKER_DEPENDENCIES`

Removed support for worker extensions and shared memory features.


## Observability and testing

This section covers [logging](#logging-and-monitoring), [monitoring](#opentelemetry-support), and [testing capabilities](#unit-testing) to help you debug problems, track performance, and ensure the reliability of your Python function apps.

### Logging and monitoring

Azure Functions exposes a root logger that you can use directly with Python's built-in `logging`

module. Any messages written using this logger are automatically sent to **Application Insights** when your app is running in Azure.

Logging allows you to capture runtime information and diagnose issues without needing any more setup.

#### Logging example with an HTTP trigger

```
import logging
import azure.functions as func
def main(req: func.HttpRequest) -> func.HttpResponse:
logging.debug("Example debug log")
logging.info("Example info log")
logging.warning("Example warning")
logging.error("Example error log")
return func.HttpResponse("OK")
```


```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.route(route="http_trigger")
def http_trigger(req) -> func.HttpResponse:
logging.debug("Example debug log")
logging.info("Example info log")
logging.warning("Example warning")
logging.error("Example error log")
return func.HttpResponse("OK")
```


You can use the full set of logging levels (`debug`

, `info`

, `warning`

, `error`

, `critical`

), and they appear in the Azure portal under Logs or Application Insights.

To learn more about monitoring Azure Functions in the portal, see [Monitor Azure Functions](functions-monitoring).

Note

To view debug logs in Application Insights, more setup is required. You can enable this feature by setting [PYTHON_ENABLE_DEBUG_LOGGING](functions-app-settings#python_enable_debug_logging) to `1`

and setting `logLevel`

to `trace`

or `debug`

in your [host.json file](functions-host-json#logging). By default, debug logs aren't visible in Application Insights.

#### Logging from background threads

If your function starts a new thread and needs to log from that thread, make sure to pass the `context`

argument into the thread. The `context`

contains thread-local storage and the current `invocation_id`

, which must be set on the worker thread in order for logs to be associated properly with the function execution.

```
import logging
import threading
import azure.functions as func
def main(req: func.HttpRequest, context) -> func.HttpResponse:
logging.info("Function started")
t = threading.Thread(target=log_from_thread, args=(context,))
t.start()
return "okay"
def log_from_thread(context):
# Associate the thread with the current invocation
context.thread_local_storage.invocation_id = context.invocation_id
logging.info("Logging from a background thread")
```


```
import azure.functions as func
import logging
import threading
app = func.FunctionApp()
@app.route(route="http_trigger")
def http_trigger(req, context) -> func.HttpResponse:
logging.info("Function started")
t = threading.Thread(target=log_from_thread, args=(context,))
t.start()
return "okay"
def log_from_thread(context):
# Associate the thread with the current invocation
context.thread_local_storage.invocation_id = context.invocation_id
logging.info("Logging from a background thread")
```


#### Configuring custom loggers

You can configure custom loggers in Python when you need more control over logging behavior, such as custom formatting, log filtering, or third-party integrations.
To configure a custom logger, use Python's `logging.getLogger()`

with a custom name and add handlers or formatters as needed.

```
import logging
custom_logger = logging.getLogger('my_custom_logger')
```


### OpenTelemetry support

Azure Functions for Python also supports **OpenTelemetry**, which enables you to emit traces, metrics, and logs in a standardized format. Using OpenTelemetry is especially valuable for distributed applications or scenarios where you want to export telemetry to tools outside of Application Insights (such as Grafana or Jaeger).

See our

[OpenTelemetry Quickstart for Azure Functions (Python)]for setup instructions and sample code.

### Unit testing

Write and run unit tests for your functions by using `pytest`

.
You can test Python functions like other Python code by using standard testing frameworks. For most bindings, you can create a mock input object by creating an instance of an appropriate class from the `azure.functions`

package.

By using `my_function`

as an example, the following example is a mock test of an HTTP-triggered function:

First, create the *<project_root>/function_app.py* file and implement the `my_function`

function as the HTTP trigger.

```
# <project_root>/function_app.py
import azure.functions as func
import logging
app = func.FunctionApp()
# Define the HTTP trigger that accepts the ?value=<int> query parameter
# Double the value and return the result in HttpResponse
@app.function_name(name="my_function")
@app.route(route="hello")
def my_function(req: func.HttpRequest) -> func.HttpResponse:
logging.info('Executing myfunction.')
initial_value: int = int(req.params.get('value'))
doubled_value: int = initial_value * 2
return func.HttpResponse(
body=f"{initial_value} * 2 = {doubled_value}",
status_code=200
)
```


You can start writing test cases for your HTTP trigger.

```
# <project_root>/test_my_function.py
import unittest
import azure.functions as func
from function_app import my_function
class TestFunction(unittest.TestCase):
def test_my_function(self):
# Construct a mock HTTP request.
req = func.HttpRequest(method='GET',
body=None,
url='/api/my_function',
params={'value': '21'})
# Call the function.
func_call = main.build().get_user_function()
resp = func_call(req)
# Check the output.
self.assertEqual(
resp.get_body(),
b'21 * 2 = 42',
)
```


Inside your Python virtual environment folder, you can run the following commands to test the app:

```
pip install pytest
pytest test_my_function.py
```


You see the `pytest`

results in the terminal, like this:

```
============================================================================================================ test session starts ============================================================================================================
collected 1 item
test_my_function.py . [100%]
============================================================================================================= 1 passed in 0.24s =============================================================================================================
```


## Optimization and advanced topics

To learn more about optimizing your Python functions apps, see these articles:

## Related articles

For more information about Functions, see these articles:

[Azure Functions package API documentation](/en-us/python/api/azure-functions/azure.functions)[Best practices for Azure Functions](functions-best-practices)[Azure Functions triggers and bindings](functions-triggers-bindings)[Blob Storage bindings](functions-bindings-storage-blob)[HTTP and webhook bindings](functions-bindings-http-webhook)[Queue Storage bindings](functions-bindings-storage-queue)[Timer triggers](functions-bindings-timer)

[Having issues with using Python? Let us know and file an issue.](https://github.com/Azure/azure-functions-python-worker/issues)
