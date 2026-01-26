---
merged_at: 2026-01-26T23:29:57.704744
merged_files: 2
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/migrate-version-3-version-4 -->

# Migrate apps from Azure Functions version 3.x to version 4.x

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions version 4.x is highly backwards compatible to version 3.x. Most apps should safely migrate to 4.x without requiring significant code changes. For more information about Functions runtime versions, see [Azure Functions runtime versions overview](functions-versions).

Important

As of December 13, 2022, function apps running on versions 2.x and 3.x of the Azure Functions runtime have reached the end of extended support. For more information, see [Retired versions](functions-versions#retired-versions).

This article walks you through the process of safely migrating your function app to run on version 4.x of the Functions runtime. Because project migration instructions are language dependent, make sure to choose your development language from the selector at the top of the article.

## Identify function apps to migrate

Use the following PowerShell script to generate a list of function apps in your subscription that currently target versions 2.x or 3.x:

```
$Subscription = '<YOUR SUBSCRIPTION ID>'
Set-AzContext -Subscription $Subscription | Out-Null
$FunctionApps = Get-AzFunctionApp
$AppInfo = @{}
foreach ($App in $FunctionApps)
{
if ($App.ApplicationSettings["FUNCTIONS_EXTENSION_VERSION"] -like '*3*')
{
$AppInfo.Add($App.Name, $App.ApplicationSettings["FUNCTIONS_EXTENSION_VERSION"])
}
}
$AppInfo
```


## Choose your target .NET version

On version 3.x of the Functions runtime, your C# function app targets .NET Core 3.1 using the in-process model or .NET 5 using the isolated worker model.

When you migrate your function app, you have the opportunity to choose the target version of .NET. You can update your C# project to one of the following versions of .NET that are supported by Functions version 4.x:

| .NET version |
|
|---|

1,2

[Isolated worker model](dotnet-isolated-process-guide)3[Isolated worker model](dotnet-isolated-process-guide)[Isolated worker model](dotnet-isolated-process-guide),[In-process model](functions-dotnet-class-library)2[See policy](https://dotnet.microsoft.com/platform/support/policy/dotnet-framework)[Isolated worker model](dotnet-isolated-process-guide)1 The [isolated worker model](dotnet-isolated-process-guide) supports Long Term Support (LTS) and Standard Term Support (STS) versions of .NET, as well as .NET Framework. The [in-process model](functions-dotnet-class-library) only supports LTS releases of .NET, ending with .NET 8. For a full feature and functionality comparison between the two models, see [Differences between in-process and isolate worker process .NET Azure Functions](dotnet-isolated-in-process-differences).

2 Support ends for the in-process model on November 10, 2026. For more information, see [this support announcement](https://aka.ms/azure-functions-retirements/in-process-model). For continued full support, you should [migrate your apps to the isolated worker model](migrate-dotnet-to-isolated-model).

3 .NET 9 previously had an expected end-of-support date of May 12, 2026. During the .NET 9 service window, the .NET team extended support for STS versions to 24 months, starting with .NET 9. For more information, see [the blog post](https://devblogs.microsoft.com/dotnet/dotnet-sts-releases-supported-for-24-months/).

Tip

**We recommend updating to .NET 8 on the isolated worker model.** .NET 8 is the fully released version with the longest support window from .NET.

Although you can choose to instead use the in-process model, we don't recommend this approach if you can avoid it. [Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model), so you'll need to move to the isolated worker model before then. Doing so while migrating to version 4.x will decrease the total effort required, and the isolated worker model will give your app [additional benefits](dotnet-isolated-in-process-differences), including the ability to more easily target future versions of .NET. If you're moving to the isolated worker model, the [.NET Upgrade Assistant](/en-us/dotnet/core/porting/upgrade-assistant-overview) can also handle many of the necessary code changes for you.

This guide doesn't present specific examples for .NET 10 (preview) or .NET 9. If you need to target one of those versions, you can adapt the .NET 8 examples.

## Prepare for migration

If you haven't already, identify the list of apps that need to be migrated in your current Azure Subscription by using the [Azure PowerShell](#identify-function-apps-to-migrate).

Before you migrate an app to version 4.x of the Functions runtime, you should do the following tasks:

- Review the list of
[breaking changes between 3.x and 4.x](#breaking-changes-between-3x-and-4x). - Complete the steps in
[Migrate your local project](#migrate-your-local-project)to migrate your local project to version 4.x. - After migrating your project, fully test the app locally using version 4.x of the
[Azure Functions Core Tools](functions-run-local). [Run the pre-upgrade validator](#run-the-pre-upgrade-validator)on the app hosted in Azure, and resolve any identified issues.- Update your function app in Azure to the new version. If you need to minimize downtime, consider using a
[staging slot](functions-deployment-slots)to test and verify your migrated app in Azure on the new runtime version. You can then deploy your app with the updated version settings to the production slot. For more information, see[Update using slots](#update-using-slots). - Publish your migrated project to the updated function app.

When you use Visual Studio to publish a version 4.x project to an existing function app at a lower version, you're prompted to let Visual Studio update the function app to version 4.x during deployment. This update uses the same process defined in [Update without slots](#update-without-slots).

## Migrate your local project

Upgrading instructions are language dependent. If you don't see your language, choose it from the selector at the [top of the article](#top).

Choose the tab that matches your target version of .NET and the desired process model (in-process or isolated worker process).

Tip

If you're moving to an LTS or STS version of .NET using the isolated worker model, the [.NET Upgrade Assistant](/en-us/dotnet/core/porting/upgrade-assistant-overview) can be used to automatically make many of the changes mentioned in the following sections.

### Project file

The following example is a `.csproj`

project file that uses .NET Core 3.1 on version 3.x:

```
<Project Sdk="Microsoft.NET.Sdk">
<PropertyGroup>
<TargetFramework>netcoreapp3.1</TargetFramework>
<AzureFunctionsVersion>v3</AzureFunctionsVersion>
</PropertyGroup>
<ItemGroup>
<PackageReference Include="Microsoft.NET.Sdk.Functions" Version="3.0.13" />
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

Based on the model you're migrating to, you might need to update or change the packages your application references. When you adopt the target packages, you then need to update the namespace of using statements and some types you reference. You can see the effect of these namespace changes on `using`

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

### Program.cs file

When migrating to run in an isolated worker process, you must add the following program.cs file to your project:

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

### local.settings.json file

The local.settings.json file is only used when running locally. For information, see [Local settings file](functions-develop-local#local-settings-file).

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

### host.json file

No changes are required to your `host.json`

file. However, if your Application Insights configuration in this file from your in-process model project, you might want to make other changes in your `Program.cs`

file. The `host.json`

file only controls logging from the Functions host runtime, and in the isolated worker model, some of these logs come from your application directly, giving you more control. See [Managing log levels in the isolated worker model](dotnet-isolated-process-guide#managing-log-levels) for details on how to filter these logs.

### Class name changes

Some key classes changed names between versions. These changes are a result either of changes in .NET APIs or in differences between in-process and isolated worker process. The following table indicates key .NET classes used by Functions that could change when migrating:

| .NET Core 3.1 | .NET 5 | .NET 8 |
|---|---|---|
`FunctionName` (attribute) |
`Function` (attribute) |
`Function` (attribute) |
`ILogger` |
`ILogger` |
`ILogger` , `ILogger<T>` |
`HttpRequest` |
`HttpRequestData` |
`HttpRequestData` , `HttpRequest` (using
|
`IActionResult` |
`HttpResponseData` |
`HttpResponseData` , `IActionResult` (using
|
`FunctionsStartup` (attribute) |
Uses
`Program.cs` |

[instead](#programcs-file)`Program.cs`

There might also be class name differences in bindings. For more information, see the reference articles for the specific bindings.

### Other code changes

This section highlights other code changes to consider as you work through the migration. These changes aren't needed by all applications, but you should evaluate if any are relevant to your scenarios. Make sure to check [Breaking changes between 3.x and 4.x](#breaking-changes-between-3x-and-4x) for other changes you might need to make to your project.

#### JSON serialization

By default, the isolated worker model uses *System.Text.Json* for JSON serialization. To customize serializer options or switch to JSON.NET (*Newtonsoft.Json*), see [Customizing JSON serialization](dotnet-isolated-process-guide#customizing-json-serialization).

#### Application Insights log levels and filtering

Logs can be sent to Application Insights from both the Functions host runtime and code in your project. The *host.json* allows you to configure rules for host logging, but to control logs coming from your code, you need to configure filtering rules as part of your *Program.cs*. See [Managing log levels in the isolated worker model](dotnet-isolated-process-guide#managing-log-levels) for details on how to filter these logs.

### HTTP trigger template

The differences between in-process and isolated worker process can be seen in HTTP triggered functions. The HTTP trigger template for version 3.x (in-process) looks like the following example:

```
using System;
using System.IO;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Logging;
using Newtonsoft.Json;
namespace Company.Function
{
public static class HttpTriggerCSharp
{
[FunctionName("HttpTriggerCSharp")]
public static async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.AuthLevelValue, "get", "post", Route = null)] HttpRequest req,
ILogger log)
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


The HTTP trigger template for the migrated version looks like the following example:

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

[Azure Functions Core Tools](functions-run-local#install-the-azure-functions-core-tools)to version 4.x.Update your app's

[Azure Functions extensions bundle](extension-bundles)to 2.x or above. For more information, see[breaking changes](#breaking-changes-between-3x-and-4x).

If needed, move to one of the

[Java versions supported on version 4.x](functions-reference-java#supported-versions).Update the app's

`POM.xml`

file to modify the`FUNCTIONS_EXTENSION_VERSION`

setting to`~4`

, as in the following example:`<configuration> <resourceGroup>${functionResourceGroup}</resourceGroup> <appName>${functionAppName}</appName> <region>${functionAppRegion}</region> <appSettings> <property> <name>WEBSITE_RUN_FROM_PACKAGE</name> <value>1</value> </property> <property> <name>FUNCTIONS_EXTENSION_VERSION</name> <value>~4</value> </property> </appSettings> </configuration>`


- If needed, move to one of the
[Node.js versions supported on version 4.x](functions-reference-node#node-version).

- Take this opportunity to upgrade to PowerShell 7.2, which is recommended. For more information, see
[PowerShell versions](functions-reference-powershell#powershell-versions).

- If you're using Python 3.6, move to one of the
[supported versions](functions-reference-python#supported-python-versions).

### Run the pre-upgrade validator

Azure Functions provides a pre-upgrade validator to help you identify potential issues when migrating your function app to 4.x. To run the pre-upgrade validator:

In the

[Azure portal](https://portal.azure.com), navigate to your function app.Open the

**Diagnose and solve problems**page.In

**Function App Diagnostics**, start typing`Functions 4.x Pre-Upgrade Validator`

and then choose it from the list.After validation completes, review the recommendations and address any issues in your app. If you need to make changes to your app, make sure to validate the changes against version 4.x of the Functions runtime, either

[locally using Azure Functions Core Tools v4](#migrate-your-local-project)or by[using a staging slot](#update-using-slots).

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


## Breaking changes between 3.x and 4.x

The following are key breaking changes to be aware of before upgrading a 3.x app to 4.x, including language-specific breaking changes. For a full list, see Azure Functions GitHub issues labeled [ Breaking Change: Approved](https://github.com/Azure/azure-functions/issues?q=is%3Aissue+label%3A%22Breaking+Change%3A+Approved%22+is%3A%22closed+OR+open%22).

If you don't see your programming language, go select it from the [top of the page](#top).

### Runtime

Azure Functions Proxies was a feature in versions 1.x through 3.x of the Azure Functions runtime. This feature isn't supported in version 4.x. For more information, see

[Serverless REST APIs using Azure Functions](functions-proxies).Logging to Azure Storage using

*AzureWebJobsDashboard*is no longer supported in 4.x. You should instead use[Application Insights](functions-monitoring). ([#1923](https://github.com/Azure/Azure-Functions/issues/1923))Azure Functions 4.x now enforces

[minimum version requirements for extensions](functions-versions#minimum-extension-versions). Update to the latest version of affected extensions. For non-.NET languages,[update](extension-bundles)to extension bundle version 2.x or later. ([#1987](https://github.com/Azure/Azure-Functions/issues/1987))Default and maximum timeouts are now enforced in 4.x for function apps running on Linux in a Consumption plan. (

[#1915](https://github.com/Azure/Azure-Functions/issues/1915))Azure Functions 4.x uses

`Azure.Identity`

and`Azure.Security.KeyVault.Secrets`

for the Key Vault provider and has deprecated the use of Microsoft.Azure.KeyVault. For more information about how to configure function app settings, see the Key Vault option in[Manage key storage](function-keys-how-to#manage-key-storage). ([#2048](https://github.com/Azure/Azure-Functions/issues/2048))Function apps that share storage accounts now fail to start when their host IDs are the same. For more information, see

[Host ID considerations](storage-considerations#host-id-considerations). ([#2049](https://github.com/Azure/Azure-Functions/issues/2049))

Azure Functions 4.x supports newer versions of .NET. See

[Supported languages in Azure Functions](supported-languages)for a full list of versions.`InvalidHostServicesException`

is now a fatal error. ([#2045](https://github.com/Azure/Azure-Functions/issues/2045))`EnableEnhancedScopes`

is enabled by default. ([#1954](https://github.com/Azure/Azure-Functions/issues/1954))Remove

`HttpClient`

as a registered service. ([#1911](https://github.com/Azure/Azure-Functions/issues/1911))

- Default thread count has been updated. Functions that aren't thread-safe or have high memory usage could be impacted. (
[#1962](https://github.com/Azure/Azure-Functions/issues/1962))

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai-assistantpost-input -->

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/python-memory-profiler-reference -->

# Profile Python apps memory usage in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

During development or after deploying your local Python function app project to Azure, it's a good practice to analyze for potential memory bottlenecks in your functions. Such bottlenecks can decrease the performance of your functions and lead to errors. The following instructions show you how to use the [memory-profiler](https://pypi.org/project/memory-profiler) Python package, which provides line-by-line memory consumption analysis of your functions as they execute.

Note

Memory profiling is intended only for memory footprint analysis in development environments. Please do not apply the memory profiler on production function apps.

## Prerequisites

Before you start developing a Python function app, you must meet these requirements:

[Python 3.7 or above](https://www.python.org/downloads). To check the full list of supported Python versions in Azure Functions, see the[Python developer guide](functions-reference-python#supported-python-versions).The

[Azure Functions Core Tools](functions-run-local#v2), version 4.x or greater. Check your version with`func --version`

. To learn about updating, see[Azure Functions Core Tools on GitHub](https://github.com/Azure/azure-functions-core-tools).[Visual Studio Code](https://code.visualstudio.com/)installed on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).An active Azure subscription.


If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Memory profiling process

In your requirements.txt, add

`memory-profiler`

to ensure the package is bundled with your deployment. If you're developing on your local machine, you may want to[activate a Python virtual environment](how-to-create-function-azure-cli?pivots=programming-language-python#create-venv)and do a package resolution by`pip install -r requirements.txt`

.In your function script (for example,

*__init__.py*for the Python v1 programming model and*function_app.py*for the v2 model), add the following lines above the`main()`

function. These lines ensure the root logger reports the child logger names, so that the memory profiling logs are distinguishable by the prefix`memory_profiler_logs`

.`import logging import memory_profiler root_logger = logging.getLogger() root_logger.handlers[0].setFormatter(logging.Formatter("%(name)s: %(message)s")) profiler_logstream = memory_profiler.LogFile('memory_profiler_logs', True)`

Apply the following decorator above any functions that need memory profiling. The decorator doesn't work directly on the trigger entrypoint

`main()`

method. You need to create subfunctions and decorate them. Also, due to a memory-profiler known issue, when applying to an async coroutine, the coroutine return value is always`None`

.`@memory_profiler.profile(stream=profiler_logstream)`

Test the memory profiler on your local machine by using Azure Functions Core Tools command

`func host start`

. When you invoke the functions, they should generate a memory usage report. The report contains file name, line of code, memory usage, memory increment, and the line content in it.To check the memory profiling logs on an existing function app instance in Azure, you can query the memory profiling logs for recent invocations with

[Kusto](/en-us/azure/azure-monitor/logs/log-query-overview)queries in Application Insights, Logs.`traces | where timestamp > ago(1d) | where message startswith_cs "memory_profiler_logs:" | parse message with "memory_profiler_logs: " LineNumber " " TotalMem_MiB " " IncreMem_MiB " " Occurrences " " Contents | union ( traces | where timestamp > ago(1d) | where message startswith_cs "memory_profiler_logs: Filename: " | parse message with "memory_profiler_logs: Filename: " FileName | project timestamp, FileName, itemId ) | project timestamp, LineNumber=iff(FileName != "", FileName, LineNumber), TotalMem_MiB, IncreMem_MiB, Occurrences, Contents, RequestId=itemId | order by timestamp asc`


## Example

Here's an example of performing memory profiling on an asynchronous and a synchronous HTTP trigger, named "HttpTriggerAsync" and "HttpTriggerSync" respectively. We'll build a Python function app that simply sends out GET requests to the Microsoft's home page.

### Create a Python function app

A Python function app should follow Azure Functions specified [folder structure](functions-reference-python#folder-structure). To scaffold the project, we recommend using the Azure Functions Core Tools by running the following commands:

```
func init PythonMemoryProfilingDemo --python
cd PythonMemoryProfilingDemo
func new -l python -t HttpTrigger -n HttpTriggerAsync -a anonymous
func new -l python -t HttpTrigger -n HttpTriggerSync -a anonymous
```


### Update file contents

The *requirements.txt* defines the packages that are used in our project. Besides the Azure Functions SDK and memory-profiler, we introduce `aiohttp`

for asynchronous HTTP requests and `requests`

for synchronous HTTP calls.

```
# requirements.txt
azure-functions
memory-profiler
aiohttp
requests
```


Create the asynchronous HTTP trigger.

Replace the code in the asynchronous HTTP trigger *HttpTriggerAsync/__init__.py* with the following code, which configures the memory profiler, root logger format, and logger streaming binding.

```
# HttpTriggerAsync/__init__.py
import azure.functions as func
import aiohttp
import logging
import memory_profiler
# Update root logger's format to include the logger name. Ensure logs generated
# from memory profiler can be filtered by "memory_profiler_logs" prefix.
root_logger = logging.getLogger()
root_logger.handlers[0].setFormatter(logging.Formatter("%(name)s: %(message)s"))
profiler_logstream = memory_profiler.LogFile('memory_profiler_logs', True)
async def main(req: func.HttpRequest) -> func.HttpResponse:
await get_microsoft_page_async('https://microsoft.com')
return func.HttpResponse(
f"Microsoft page loaded.",
status_code=200
)
@memory_profiler.profile(stream=profiler_logstream)
async def get_microsoft_page_async(url: str):
async with aiohttp.ClientSession() as client:
async with client.get(url) as response:
await response.text()
# @memory_profiler.profile does not support return for coroutines.
# All returns become None in the parent functions.
# GitHub Issue: https://github.com/pythonprofilers/memory_profiler/issues/289
```


Create the synchronous HTTP trigger.

Replace the code in the asynchronous HTTP trigger *HttpTriggerSync/__init__.py* with the following code.

```
# HttpTriggerSync/__init__.py
import azure.functions as func
import requests
import logging
import memory_profiler
# Update root logger's format to include the logger name. Ensure logs generated
# from memory profiler can be filtered by "memory_profiler_logs" prefix.
root_logger = logging.getLogger()
root_logger.handlers[0].setFormatter(logging.Formatter("%(name)s: %(message)s"))
profiler_logstream = memory_profiler.LogFile('memory_profiler_logs', True)
def main(req: func.HttpRequest) -> func.HttpResponse:
content = profile_get_request('https://microsoft.com')
return func.HttpResponse(
f"Microsoft page response size: {len(content)}",
status_code=200
)
@memory_profiler.profile(stream=profiler_logstream)
def profile_get_request(url: str):
response = requests.get(url)
return response.content
```


### Profile Python function app in local development environment

After you make the above changes, there are a few more steps to initialize a Python virtual environment for Azure Functions runtime.

Open a Windows PowerShell or any Linux shell as you prefer.

Create a Python virtual environment by

`py -m venv .venv`

in Windows, or`python3 -m venv .venv`

in Linux.Activate the Python virtual environment with

`.venv\Scripts\Activate.ps1`

in Windows PowerShell or`source .venv/bin/activate`

in Linux shell.Restore the Python dependencies with

`pip install -r requirements.txt`

Start the Azure Functions runtime locally with Azure Functions Core Tools

`func host start`

Send a GET request to

`https://localhost:7071/api/HttpTriggerAsync`

or`https://localhost:7071/api/HttpTriggerSync`

.It should show a memory profiling report similar to the following section in Azure Functions Core Tools.

`Filename: <ProjectRoot>\HttpTriggerAsync\__init__.py Line # Mem usage Increment Occurrences Line Contents ============================================================ 19 45.1 MiB 45.1 MiB 1 @memory_profiler.profile 20 async def get_microsoft_page_async(url: str): 21 45.1 MiB 0.0 MiB 1 async with aiohttp.ClientSession() as client: 22 46.6 MiB 1.5 MiB 10 async with client.get(url) as response: 23 47.6 MiB 1.0 MiB 4 await response.text()`


## Next steps

For more information about Azure Functions Python development, see the following resources:

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
