---
merged_at: 2026-01-25T15:41:11.659992
merged_files: 2
---

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
