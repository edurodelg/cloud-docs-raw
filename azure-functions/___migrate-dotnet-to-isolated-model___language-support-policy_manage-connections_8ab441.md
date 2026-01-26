---
merged_at: 2026-01-26T21:02:36.362264
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _migrate-dotnet-to-isolated-model___language-support-policy_manage-connections_f_180dea.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: migrate-dotnet-to-isolated-model.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model -->

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


---

<!-- DOCUMENTO FUSIONADO: __language-support-policy_manage-connections_functions-how-to-azure-devops.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _language-support-policy_manage-connections.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: language-support-policy.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/language-support-policy -->

# Azure Functions language stack support policy

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains the support policy for the language stacks supported by Azure Functions. Guidance is language-specific. Make sure to choose your preferred development language at the [top of the article](#top).

## Retirement process

The Functions runtime includes the Functions host and programming language-specific workers. To maintain full-support coverage when running your functions in Azure, Functions support aligns with end-of-life support for a given language. To help you keep your apps up-to-date and supported, Functions implements a phased reduction in support as language stack versions reach their end-of-life dates. Support ends on the earlier of: the community end-of-support date for the language or the end-of-support date for the underlying base operating system. Retirement dates are published at general availability (GA) to allow time for upgrade planning and testing.

**Notification phase**:The Functions team sends you notification emails about upcoming language version retirements that affect your function apps. When you receive this notification, you should prepare to upgrade these apps to use to a supported version.

**Retirement phase**:After the language end-of-life date, function apps that use retired language versions can still be created and deployed, and they continue to run on the platform. However, these apps aren't eligible for new features, security patches, and performance optimizations until after you upgrade them to a supported language version. Further, if required, in certain cases we will limit the number of instances allocated to these apps including limit scaling to 1 instance.

Important

If you're running function apps using an unsupported runtime or language version, you might encounter issues and performance implications and are required to upgrade before receiving support for your function app. As such, you're highly encouraged to upgrade the language version of such an app to a supported version. TO learn how, see

[Update language stack versions in Azure Functions](update-language-versions).

## Retirement policy exceptions

Any Functions-supported exceptions to language-specific retirement policies are documented here:

There are currently no exceptions to the general retirement policy.


## Language support-related resources

Use these resources to better understand and plan for language support-related changes in your function apps.

| Resource | Details |
|---|---|
Supported versions |
|

**Language version support timelines**[.NET support policy page](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)**Configuring language versions**[Isolated worker model](dotnet-isolated-process-guide#supported-versions)[In-process model](functions-dotnet-class-library#supported-versions)| Resource | Details |
|---|---|
Supported versions |
|

**Language version support timelines**[Node.js release page on GitHub](https://github.com/nodejs/Release#release-schedule)**Configuring language versions**[Setting the Node version](functions-reference-node#setting-the-node-version)| Resource | Details |
|---|---|
Supported versions |
|

**Language version support timelines**[Node.js release page on GitHub](https://github.com/nodejs/Release#release-schedule)**Configuring language versions**[Setting the Node version](functions-reference-node#setting-the-node-version)| Resource | Details |
|---|---|
Supported versions |
|

**Language version support timelines**[Java support on Azure and Azure Stack](/en-us/azure/developer/java/fundamentals/java-support-on-azure)**Configuring language versions**[Update the stack configuration](update-language-versions#update-the-stack-configuration)| Resource | Details |
|---|---|
Supported versions |
|

**Language version support timelines**[PowerShell Support Lifecycle](/en-us/powershell/scripting/powershell-support-lifecycle#powershell-end-of-support-dates)**Configuring language versions**[Changing the PowerShell version](functions-reference-python#supported-python-versions)| Resource | Details |
|---|---|
Supported versions |
|

**Language version support timelines**[Python developer's guide](https://devguide.python.org/#status-of-python-branches)**Configuring language versions**[Changing Python version](set-runtime-version?tabs=azure-portal&pivots=platform-linux#manual-version-updates-on-linux)## Frequently asked questions

This section provides you with answers to questions that are frequently asked about language support policies.

### Which versions of my preferred language does Functions currently support?

For the up-to-date list of supported language stack versions, see [Supported languages in Azure Functions](supported-languages#languages-by-runtime-version).

### How long will Functions continue to support my language version?

Support ends on the earlier of: the community end-of-support date for the language or the end-of-support date for the underlying base operating system. Retirement dates are published at general availability (GA) to allow time for upgrade planning and testing. For the expected end-of-life dates of currently supported versions, see [Supported languages in Azure Functions](supported-languages#languages-by-runtime-version).

### What happens when my runtime version reaches the end of support?

After a previously supported Functions runtime version reaches its end-of-support, Microsoft no longer provides bug fixes, security updates, or patches. Apps using retired versions may also face performance degradation. You must upgrade to a supported version to maintain security and stability.

### Can I continue to use an unsupported language stack or runtime version?

You can continue to use previously supported language stacks and Functions runtime versions beyond the end-of-support date. However, you must take into account that unsupported runtime versions don't receive updates, security patches, or official support from Microsoft. Your apps might also face performance degradation when using retired runtime versions.

### How do I upgrade my function app to a newer supported language stack or runtime version?

To make sure that your app is compatible with both the latest supported Functions runtime version and the latest version of your language stack, see [Update language stack versions in Azure Functions](update-language-versions)

### How do I check which language stack and runtime version is being used by my function app?

Azure provides these methods to check the current runtime version used by your function app:

The language stack used by your function app is determined based on the value of the `FUNCTIONS_WORKER_RUNTIME`

application setting. For more information, see [Work with application settings](functions-how-to-use-azure-function-app-settings#settings).

## Related articles

To learn more about how to upgrade your function app's language version, see these articles:


---

<!-- DOCUMENTO FUSIONADO: manage-connections.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/manage-connections -->

# Manage connections in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Functions in a function app share resources. Among those shared resources are connections: HTTP connections, database connections, and connections to services such as Azure Storage. When many functions are running concurrently in a Consumption plan, it's possible to run out of available connections. This article explains how to code your functions to avoid using more connections than they need.

Note

Connection limits described in this article apply only when running in a [Consumption plan](consumption-plan). However, the techniques described here may be beneficial when running on any plan.

## Connection limit

The number of available connections in a Consumption plan is limited partly because a function app in this plan runs in a [sandbox environment](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox). One of the restrictions that the sandbox imposes on your code is a limit on the number of outbound connections, which is currently 600 active (1,200 total) connections per instance. When you reach this limit, the functions runtime writes the following message to the logs: `Host thresholds exceeded: Connections`

. For more information, see the [Functions service limits](functions-scale#service-limits).

This limit is per instance. When the [scale controller adds function app instances](event-driven-scaling) to handle more requests, each instance has an independent connection limit. That means there's no global connection limit, and you can have much more than 600 active connections across all active instances.

When troubleshooting, make sure that you have enabled Application Insights for your function app. Application Insights lets you view metrics for your function apps like executions. For more information, see [View telemetry in Application Insights](analyze-telemetry-data#view-telemetry-in-application-insights).

## Static clients

To avoid holding more connections than necessary, reuse client instances rather than creating new ones with each function invocation. We recommend reusing client connections for any language that you might write your function in. For example, .NET clients like the [HttpClient](/en-us/dotnet/api/system.net.http.httpclient?view=netcore-3.1&preserve-view=true), [DocumentClient](/en-us/dotnet/api/microsoft.azure.documents.client.documentclient), and Azure Storage clients can manage connections if you use a single, static client.

Here are some guidelines to follow when you're using a service-specific client in an Azure Functions application:

*Do not*create a new client with every function invocation.*Do*create a single, static client that every function invocation can use.*Consider*creating a single, static client in a shared helper class if different functions use the same service.

## Client code examples

This section demonstrates best practices for creating and using clients from your function code.

### HTTP requests

Here's an example of C# function code that creates a static [HttpClient](/en-us/dotnet/api/system.net.http.httpclient?view=netcore-3.1&preserve-view=true) instance:

```
// Create a single, static HttpClient
private static HttpClient httpClient = new HttpClient();
public static async Task Run(string input)
{
var response = await httpClient.GetAsync("https://example.com");
// Rest of function
}
```


A common question about [HttpClient](/en-us/dotnet/api/system.net.http.httpclient?view=netcore-3.1&preserve-view=true) in .NET is "Should I dispose of my client?" In general, you dispose of objects that implement `IDisposable`

when you're done using them. But you don't dispose of a static client because you aren't done using it when the function ends. You want the static client to live for the duration of your application.

### Azure Cosmos DB clients

[CosmosClient](/en-us/dotnet/api/microsoft.azure.cosmos.cosmosclient) connects to an Azure Cosmos DB instance. The Azure Cosmos DB documentation recommends that you [use a singleton Azure Cosmos DB client for the lifetime of your application](/en-us/azure/cosmos-db/performance-tips-dotnet-sdk-v3-sql#sdk-usage). The following example shows one pattern for doing that in a function:

```
#r "Microsoft.Azure.Cosmos"
using Microsoft.Azure.Cosmos;
private static Lazy<CosmosClient> lazyClient = new Lazy<CosmosClient>(InitializeCosmosClient);
private static CosmosClient cosmosClient => lazyClient.Value;
private static CosmosClient InitializeCosmosClient()
{
// Perform any initialization here
var uri = "https://youraccount.documents.azure.com:443";
var authKey = "authKey";
return new CosmosClient(uri, authKey);
}
public static async Task Run(string input)
{
Container container = cosmosClient.GetContainer("database", "collection");
MyItem item = new MyItem{ id = "myId", partitionKey = "myPartitionKey", data = "example" };
await container.UpsertItemAsync(document);
// Rest of function
}
```


Also, create a file named "function.proj" for your trigger and add the below content :

```
<Project Sdk="Microsoft.NET.Sdk">
<PropertyGroup>
<TargetFramework>netcoreapp3.1</TargetFramework>
</PropertyGroup>
<ItemGroup>
<PackageReference Include="Microsoft.Azure.Cosmos" Version="3.23.0" />
</ItemGroup>
</Project>
```


## SqlClient connections

Your function code can use the .NET Framework Data Provider for SQL Server ([SqlClient](/en-us/dotnet/api/system.data.sqlclient)) to make connections to a SQL relational database. This is also the underlying provider for data frameworks that rely on ADO.NET, such as [Entity Framework](/en-us/ef/ef6/). Unlike [HttpClient](/en-us/dotnet/api/system.net.http.httpclient) and [DocumentClient](/en-us/dotnet/api/microsoft.azure.documents.client.documentclient) connections, ADO.NET implements connection pooling by default. But because you can still run out of connections, you should optimize connections to the database. For more information, see [SQL Server Connection Pooling (ADO.NET)](/en-us/dotnet/framework/data/adonet/sql-server-connection-pooling).

Tip

Some data frameworks, such as Entity Framework, typically get connection strings from the **ConnectionStrings** section of a configuration file. In this case, you must explicitly add SQL database connection strings to the **Connection strings** collection of your function app settings and in the [local.settings.json file](functions-develop-local#local-settings-file) in your local project. If you're creating an instance of [SqlConnection](/en-us/dotnet/api/system.data.sqlclient.sqlconnection) in your function code, you should store the connection string value in **Application settings** with your other connections.

## Next steps

For more information about why we recommend static clients, see [Improper instantiation antipattern](/en-us/azure/architecture/antipatterns/improper-instantiation/).

For more Azure Functions performance tips, see [Optimize the performance and reliability of Azure Functions](functions-best-practices).


---

<!-- DOCUMENTO FUSIONADO: functions-how-to-azure-devops.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-how-to-azure-devops -->

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

<!-- DOCUMENTO FUSIONADO: __functions-bindings-notification-hubs_performance-reliability__functions-bindin_fa006b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-notification-hubs_performance-reliability.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-notification-hubs.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-notification-hubs -->

# Azure Notification Hubs output bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to send push notifications by using [Azure Notification Hubs](../notification-hubs/notification-hubs-push-notification-overview) bindings in Azure Functions. Azure Functions supports output bindings for Notification Hubs.

You must configure Notification Hubs for the Platform Notifications Service (PNS) you want to use. For more information about how to get push notifications in your client app from Notification Hubs, see [Quickstart: Set up push notifications in a notification hub](../notification-hubs/configure-notification-hub-portal-pns-settings).

Important

Google has [deprecated Google Cloud Messaging (GCM) in favor of Firebase Cloud Messaging (FCM)](https://developers.google.com/cloud-messaging/faq). However, output bindings for Notification Hubs doesn't support FCM. To send notifications using FCM, use the [Firebase API](https://firebase.google.com/docs/cloud-messaging/server#choosing-a-server-option) directly in your function or use [template notifications](../notification-hubs/notification-hubs-templates-cross-platform-push-messages).

## Packages: Functions 1.x

Important

[Support will end for version 1.x of the Azure Functions runtime on September 14, 2026](https://aka.ms/azure-functions-retirements/hostv1). We highly recommend that you [migrate your apps to version 4.x](migrate-version-1-version-4) for full support.

The Notification Hubs bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs) NuGet package, version 1.x. Source code for the package is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/v2.x/src/WebJobs.Extensions.NotificationHubs) GitHub repository.

The following table lists how to add support for output binding in each development environment.

| Development environment | To add support in Functions 1.x |
|---|---|
| Local development: C# class library |
|

## Packages: Functions 2.x and higher

Output binding isn't available in Functions 2.x and higher.

## Example: template

The notifications you send can be native notifications or [template notifications](../notification-hubs/notification-hubs-templates-cross-platform-push-messages). A native notification targets a specific client platform, as configured in the `platform`

property of the output binding. A template notification can be used to target multiple platforms.

Template examples for each language:

[C# script: out parameter](#c-script-template-example-out-parameter)[C# script: asynchronous](#c-script-template-example-asynchronous)[C# script: JSON](#c-script-template-example-json)[C# script: library types](#c-script-template-example-library-types)[F#](#f-template-example)[JavaScript](#javascript-template-example)

### C# script template example: out parameter

This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages) that contains a `message`

placeholder in the template:

```
using System;
using System.Threading.Tasks;
using System.Collections.Generic;
public static void Run(string myQueueItem, out IDictionary<string, string> notification, TraceWriter log)
{
log.Info($"C# Queue trigger function processed: {myQueueItem}");
notification = GetTemplateProperties(myQueueItem);
}
private static IDictionary<string, string> GetTemplateProperties(string message)
{
Dictionary<string, string> templateProperties = new Dictionary<string, string>();
templateProperties["message"] = message;
return templateProperties;
}
```


### C# script template example: asynchronous

If you're using asynchronous code, out parameters aren't allowed. In this case, use `IAsyncCollector`

to return your template notification. The following code is an asynchronous example of the previous example:

```
using System;
using System.Threading.Tasks;
using System.Collections.Generic;
public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
log.Info($"C# Queue trigger function processed: {myQueueItem}");
log.Info($"Sending Template Notification to Notification Hub");
await notification.AddAsync(GetTemplateProperties(myQueueItem));
}
private static IDictionary<string, string> GetTemplateProperties(string message)
{
Dictionary<string, string> templateProperties = new Dictionary<string, string>();
templateProperties["user"] = "A new user wants to be added : " + message;
return templateProperties;
}
```


### C# script template example: JSON

This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages) that contains a `message`

placeholder in the template using a valid JSON string:

```
using System;
public static void Run(string myQueueItem, out string notification, TraceWriter log)
{
log.Info($"C# Queue trigger function processed: {myQueueItem}");
notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```


### C# script template example: library types

This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/):

```
#r "Microsoft.Azure.NotificationHubs"
using System;
using System.Threading.Tasks;
using Microsoft.Azure.NotificationHubs;
public static void Run(string myQueueItem, out Notification notification, TraceWriter log)
{
log.Info($"C# Queue trigger function processed: {myQueueItem}");
notification = GetTemplateNotification(myQueueItem);
}
private static TemplateNotification GetTemplateNotification(string message)
{
Dictionary<string, string> templateProperties = new Dictionary<string, string>();
templateProperties["message"] = message;
return new TemplateNotification(templateProperties);
}
```


### F# template example

This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages) that contains `location`

and `message`

:

```
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```


### JavaScript template example

This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages) that contains `location`

and `message`

:

```
module.exports = async function (context, myTimer) {
var timeStamp = new Date().toISOString();
if (myTimer.IsPastDue)
{
context.log('Node.js is running late!');
}
context.log('Node.js timer trigger function ran!', timeStamp);
context.bindings.notification = {
location: "Redmond",
message: "Hello from Node!"
};
};
```


## Example: APNS native

This C# script example shows how to send a native Apple Push Notification Service (APNS) notification:

```
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"
using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;
public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
log.Info($"C# Queue trigger function processed: {myQueueItem}");
// In this example, the queue item is a new user to be processed in the form of a JSON string with
// a "name" value.
//
// The JSON format for a native Apple Push Notification Service (APNS) notification is:
// { "aps": { "alert": "notification message" }}
log.LogInformation($"Sending APNS notification of a new user");
dynamic user = JsonConvert.DeserializeObject(myQueueItem);
string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants to be added (" +
user.name + ")\" }}";
log.LogInformation($"{apnsNotificationPayload}");
await notification.AddAsync(new AppleNotification(apnsNotificationPayload));
}
```


## Example: WNS native

This C# script example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native Windows Push Notification Service (WNS) toast notification:

```
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"
using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;
public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
log.Info($"C# Queue trigger function processed: {myQueueItem}");
// In this example, the queue item is a new user to be processed in the form of a JSON string with
// a "name" value.
//
// The XML format for a native WNS toast notification is ...
// <?xml version="1.0" encoding="utf-8"?>
// <toast>
// <visual>
// <binding template="ToastText01">
// <text id="1">notification message</text>
// </binding>
// </visual>
// </toast>
log.Info($"Sending WNS toast notification of a new user");
dynamic user = JsonConvert.DeserializeObject(myQueueItem);
string wnsNotificationPayload = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
"<toast><visual><binding template=\"ToastText01\">" +
"<text id=\"1\">" +
"A new user wants to be added (" + user.name + ")" +
"</text>" +
"</binding></visual></toast>";
log.Info($"{wnsNotificationPayload}");
await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));
}
```


## Attributes

In [C# class libraries](functions-dotnet-class-library), use the [NotificationHub](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) attribute.

The attribute's constructor parameters and properties are described in the [Configuration](#configuration) section.

## Configuration

The following table lists the binding configuration properties that you set in the *function.json* file and the `NotificationHub`

attribute:

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Set to `notificationHub` . |
direction |
n/a | Set to `out` . |
name |
n/a | Variable name used in function code for the notification hub message. |
tagExpression |
TagExpression |
Tag expressions allow you to specify that notifications be delivered to a set of devices that are registered to receive notifications matching the tag expression. For more information, see
|

**hubName****HubName****connection****ConnectionStringSetting***DefaultFullSharedAccessSignature*value for your notification hub. For more information, see[Connection string setup](#connection-string-setup).**platform****Platform**[Notification Hubs templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages). When**platform**is set, it must be one of the following values:`apns`

: Apple Push Notification Service. For more information on configuring the notification hub for APNS and receiving the notification in a client app, see[Send push notifications to .NET MAUI apps using Azure Notification Hubs via a backend service](/en-us/dotnet/maui/data-cloud/push-notifications).`adm`

:[Amazon Device Messaging](https://developer.amazon.com/device-messaging). For more information on configuring the notification hub for Azure Deployment Manager (ADM) and receiving the notification in a Kindle app, see[Send push notifications to Android devices using Firebase SDK](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started).`wns`

:[Windows Push Notification Services](/en-us/windows/uwp/design/shell/tiles-and-notifications/windows-push-notification-services--wns--overview)targeting Windows platforms. WNS also supports Windows Phone 8.1 and later. For more information, see[Send notifications to Universal Windows Platform apps using Azure Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification).`mpns`

:[Microsoft Push Notification Service](/en-us/previous-versions/windows/apps/ff402558(v=vs.105)). This platform supports Windows Phone 8 and earlier Windows Phone platforms. For more information, see[Send notifications to Universal Windows Platform apps using Azure Notification Hubs](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns).

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

### function.json file example

Here's an example of a Notification Hubs binding in a *function.json* file:

```
{
"bindings": [
{
"type": "notificationHub",
"direction": "out",
"name": "notification",
"tagExpression": "",
"hubName": "my-notification-hub",
"connection": "MyHubConnectionString",
"platform": "apns"
}
],
"disabled": false
}
```


### Connection string setup

To use a notification hub output binding, you must configure the connection string for the hub.

Important

The Notification Hubs binding doesn't support Microsoft Entra authentication and managed identities. You can use Azure Key Vault to centrally manage your notification hub connection string and help with key rotation. To learn more, see [Manage Connections](manage-connections).

You can select an existing notification hub or create a new one from the **Integrate** tab in the Azure portal. You can also configure the connection string manually.

To configure the connection string to an existing notification hub:

Navigate to your notification hub in the

[Azure portal](https://portal.azure.com), choose**Access policies**, and select the copy button next to the**DefaultFullSharedAccessSignature**policy.The connection string for the

*DefaultFullSharedAccessSignature*policy is copied to your notification hub. This connection string lets your function send notification messages to the hub.Navigate to your function app in the Azure portal, expand

**Settings**, and then select**Environment variables**.From the

**App setting**tab, select**+ Add**to add a key such as**MyHubConnectionString**. The**Name**of this app setting is the output binding connection setting in*function.json*or the .NET attribute. For more information, see[Configuration](#configuration).For the value, paste the copied

*DefaultFullSharedAccessSignature*connection string from your notification hub, and then select**Apply**.

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Exceptions and return codes

| Binding | Reference |
|---|---|
| Notification Hub |
|


---

<!-- DOCUMENTO FUSIONADO: performance-reliability.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/performance-reliability -->

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

<!-- DOCUMENTO FUSIONADO: _functions-bindings-cache-trigger-redispubsub_functions-add-openai-text-completi_21520d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-cache-trigger-redispubsub.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache-trigger-redispubsub -->

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

<!-- DOCUMENTO FUSIONADO: functions-add-openai-text-completion.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-add-openai-text-completion -->

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
