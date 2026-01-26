---
merged_at: 2026-01-26T21:02:36.324401
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __dotnet-isolated-in-process-differences__functions-bindings-register_register-m_6310fa.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _dotnet-isolated-in-process-differences__functions-bindings-register_register-mc_464894.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: dotnet-isolated-in-process-differences.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/dotnet-isolated-in-process-differences -->

# Differences between the isolated worker model and the in-process model for .NET on Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

There are two execution models for .NET functions:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

This article describes the current state of the functional and behavioral differences between the two models. To migrate from the in-process model to the isolated worker model, see [Migrate .NET apps from the in-process model to the isolated worker model](migrate-dotnet-to-isolated-model).

## Execution model comparison table

Use the following table to compare feature and functional differences between the two models:

| Feature/behavior | Isolated worker model | In-process model3 |
|---|---|---|
|

Standard Term Support (STS) versions,

.NET Framework

[Microsoft.Azure.Functions.Worker](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker/)[Microsoft.Azure.Functions.Worker.Sdk](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Sdk)[Microsoft.NET.Sdk.Functions](https://www.nuget.org/packages/Microsoft.NET.Sdk.Functions/)[Microsoft.Azure.Functions.Worker.Extensions.*](https://www.nuget.org/packages?q=Microsoft.Azure.Functions.Worker.Extensions)[Microsoft.Azure.WebJobs.Extensions.*](https://www.nuget.org/packages?q=Microsoft.Azure.WebJobs.Extensions)[Supported](durable/durable-functions-dotnet-isolated-overview)[Supported](durable/durable-functions-overview)JSON serializable types

Arrays/enumerations

[Service SDK types](dotnet-isolated-process-guide#sdk-types)4[JSON serializable](/en-us/dotnet/api/system.text.json.jsonserializeroptions)typesArrays/enumerations

Service SDK types

4[HttpRequestData](/en-us/dotnet/api/microsoft.azure.functions.worker.http.httprequestdata?view=azure-dotnet&preserve-view=true)/[HttpResponseData](/en-us/dotnet/api/microsoft.azure.functions.worker.http.httpresponsedata?view=azure-dotnet&preserve-view=true)[HttpRequest](/en-us/dotnet/api/microsoft.aspnetcore.http.httprequest)/[IActionResult](/en-us/dotnet/api/microsoft.aspnetcore.mvc.iactionresult)(using[ASP.NET Core integration](dotnet-isolated-process-guide#aspnet-core-integration))5[HttpRequest](/en-us/dotnet/api/microsoft.aspnetcore.http.httprequest)/[IActionResult](/en-us/dotnet/api/microsoft.aspnetcore.mvc.iactionresult)5[HttpRequestMessage](/en-us/dotnet/api/system.net.http.httprequestmessage)/[HttpResponseMessage](/en-us/dotnet/api/system.net.http.httpresponsemessage)- single or

[multiple outputs](dotnet-isolated-process-guide#multiple-output-bindings)- arrays of outputs

`out`

parameters,`IAsyncCollector`

1[work with SDK types directly](dotnet-isolated-process-guide#register-azure-clients)[Supported](functions-dotnet-class-library#binding-at-runtime)[Supported](dotnet-isolated-process-guide#dependency-injection)(improved model consistent with .NET ecosystem)[Supported](functions-dotnet-dependency-injection)[Supported](dotnet-isolated-process-guide#middleware)[/](/en-us/dotnet/api/microsoft.extensions.logging.logger-1)`ILogger<T>`

[obtained from](/en-us/dotnet/api/microsoft.extensions.logging.ilogger)`ILogger`

[FunctionContext](/en-us/dotnet/api/microsoft.azure.functions.worker.functioncontext)or by using[dependency injection](dotnet-isolated-process-guide#dependency-injection)[passed to the function](/en-us/dotnet/api/microsoft.extensions.logging.ilogger)`ILogger`

[by using](/en-us/dotnet/api/microsoft.extensions.logging.logger-1)`ILogger<T>`

[dependency injection](functions-dotnet-dependency-injection)[Supported](dotnet-isolated-process-guide#application-insights)[Supported](functions-monitoring#dependencies)[Supported](dotnet-isolated-process-guide#cancellation-tokens)[Supported](functions-dotnet-class-library#cancellation-tokens)2[Configurable optimizations](dotnet-isolated-process-guide#performance-optimizations)[Supported](dotnet-isolated-process-guide#readytorun)[Supported](functions-dotnet-class-library#readytorun)[Supported](flex-consumption-plan#supported-language-stack-versions)[Preview](dotnet-aspire-integration)- When you need to interact with a service using parameters determined at runtime, using the corresponding service SDKs directly is recommended over using imperative bindings. The SDKs are less verbose, cover more scenarios, and have advantages for error handling and debugging purposes. This recommendation applies to both models.
- Cold start times could be additionally affected on Windows when using some preview versions of .NET due to just-in-time loading of preview frameworks. This impact applies to both the in-process and isolated worker models but can be noticeable when comparing across different versions. This delay for preview versions isn't present on Linux plans.
- C# Script functions also run in-process and use the same libraries as in-process class library functions. For more information, see the
[Azure Functions C# script (.csx) developer reference](functions-reference-csharp). - Service SDK types include types from the
[Azure SDK for .NET](/en-us/dotnet/azure/sdk/azure-sdk-for-dotnet)such as[BlobClient](/en-us/dotnet/api/azure.storage.blobs.blobclient). - ASP.NET Core types aren't supported for .NET Framework.

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


---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-register_register-mcp-server-api-center.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-register.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-register -->

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

<!-- DOCUMENTO FUSIONADO: register-mcp-server-api-center.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/register-mcp-server-api-center -->

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

<!-- DOCUMENTO FUSIONADO: _functions-bindings-storage-table_functions-create-storage-blob-triggered-functi_2f5004.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-storage-table.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-table -->

# Azure Tables bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions integrates with [Azure Tables](/en-us/azure/cosmos-db/table/introduction) via [triggers and bindings](functions-triggers-bindings). Integrating with Azure Tables allows you to build functions that read and write data using [Azure Cosmos DB for Table](/en-us/azure/cosmos-db/table/introduction) and [Azure Table Storage](../storage/tables/table-storage-overview).

| Action | Type |
|---|---|
| Read table data in a function |
|

[Output binding](functions-bindings-storage-table-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The process for installing the extension varies depending on the extension version:

This version introduces the ability to [connect using an identity instead of a secret](functions-reference#configure-an-identity-based-connection). For a tutorial on configuring your function apps with managed identities, see the [creating a function app with identity-based connections tutorial](functions-identity-based-connections-tutorial).

This version allows you to bind to types from [ Azure.Data.Tables](/en-us/dotnet/api/azure.data.tables). It also introduces the ability to use Azure Cosmos DB for Table.

This extension is available by installing the [Microsoft.Azure.Functions.Worker.Extensions.Tables NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Tables) into a project using version 5.x or higher of the extensions for [blobs](functions-bindings-storage-blob?tabs=isolated-process,extensionv5) and [queues](functions-bindings-storage-queue?tabs=isolated-process,extensionv5).

Using the .NET CLI:

```
# Install the Azure Tables extension
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Tables --version 1.0.0
# Update the combined Azure Storage extension (to a version which no longer includes Azure Tables)
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Storage --version 5.0.0
```


Note

Azure Blobs, Azure Queues, and Azure Tables now use separate extensions and are referenced individually. For example, to use the triggers and bindings for all three services in your .NET isolated-process app, you should add the following packages to your project:

[Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs)[Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues)[Microsoft.Azure.Functions.Worker.Extensions.Tables](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Tables)

Previously, the extensions shipped together as [Microsoft.Azure.Functions.Worker.Extensions.Storage, version 4.x](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage/4.0.4). This same package also has a [5.x version](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage/5.0.0), which references the split packages for blobs and queues only. When upgrading your package references from older versions, you may therefore need to additionally reference the new [Microsoft.Azure.Functions.Worker.Extensions.Tables](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Tables) NuGet package. Also, when referencing these newer split packages, make sure you are not referencing an older version of the combined storage package, as this will result in conflicts from two definitions of the same bindings.

If you're writing your application using F#, you must also configure this extension as part of the app's [startup configuration](dotnet-isolated-process-guide#start-up-and-configuration). In the call to `ConfigureFunctionsWorkerDefaults()`

or `ConfigureFunctionsWebApplication()`

, add a delegate that takes an `IFunctionsWorkerApplication`

parameter. Then within the body of that delegate, call `ConfigureTablesExtension()`

on the object:

```
let hostBuilder = new HostBuilder()
hostBuilder.ConfigureFunctionsWorkerDefaults(fun (context: HostBuilderContext) (appBuilder: IFunctionsWorkerApplicationBuilder) ->
appBuilder.ConfigureTablesExtension() |> ignore
) |> ignore
```


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

The isolated worker process supports parameter types according to the tables below. Support for binding to types from [Azure.Data.Tables](/en-us/dotnet/api/azure.data.tables) is in preview.

**Azure Tables input binding**

When working with a single table entity, the Azure Tables input binding can bind to the following types:

| Type | Description |
|---|---|
| A JSON serializable type that implements
|

[ITableEntity](/en-us/dotnet/api/azure.data.tables.itableentity)or have a string`RowKey`

property and a string `PartitionKey`

property.[TableEntity](/en-us/dotnet/api/azure.data.tables.tableentity)1When working with multiple entities from a query, the Azure Tables input binding can bind to the following types:

| Type | Description |
|---|---|
`IEnumerable<T>` where `T` implements
|
An enumeration of entities returned by the query. Each entry represents one entity. The type `T` must implement
`RowKey` property and a string `PartitionKey` property. |
1 |

1 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.Tables 1.2.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Tables/1.2.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

**Azure Tables output binding**

When you want the function to write to a single entity, the Azure Tables output binding can bind to the following types:

| Type | Description |
|---|---|
| A JSON serializable type that implements [ITableEntity] | Functions attempts to serialize a plain-old CLR object (POCO) type as the entity. The type must implement [ITableEntity] or have a string `RowKey` property and a string `PartitionKey` property. |

When you want the function to write to multiple entities, the Azure Tables output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single entity types |
An array containing multiple entities. Each entry represents one entity. |

For other output scenarios, create and use a [TableClient](/en-us/dotnet/api/azure.data.tables.tableclient) with other types from [Azure.Data.Tables](/en-us/dotnet/api/azure.data.tables) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.


---

<!-- DOCUMENTO FUSIONADO: functions-create-storage-blob-triggered-function.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-storage-blob-triggered-function -->

# Create a function in Azure that's triggered by Blob storage

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Learn how to create a function triggered when files are uploaded to or updated in a Blob storage container.

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

You've successfully created your new function app. Next, you create a function in the new function app.

## Create an Azure Blob storage triggered function

In your function app, select

**Overview**, and then select**+ Create**under**Functions**.Under

**Select a template**, choose the**Blob trigger**template and select**Next**.In

**Template details**, configure the new trigger with the settings as specified in this table, then select**Create**:Setting Suggested value Description **Job type**Append to app You only see this setting for a Python v2 app. **New Function**Unique in your function app Name of this blob triggered function. **Path**samples-workitems/{name} Location in Blob storage being monitored. The file name of the blob is passed in the binding as the *name*parameter.**Storage account connection**AzureWebJobsStorage You can use the storage account connection already being used by your function app, or create a new one. Azure creates the Blob Storage triggered function based on the provided values. Next, create the

**samples-workitems**container.

## Create the container

Return to the

**Overview**page for your function app, select your**Resource group**, then find and select the storage account in your resource group.In the storage account page, select

**Data storage**>**Containers**>**+ Container**.In the

**Name**field, type`samples-workitems`

, and then select**Create**to create a container.Select the new

`samples-workitems`

container, which you use to test the function by uploading a file to the container.

## Test the function

In a new browser window, return to your function app page and select

**Log stream**, which displays real-time logging for your app.From the

`samples-workitems`

container page, select**Upload**>**Browse for files**, browse to a file on your local computer (such as an image file), and choose the file.Select

**Open**and then**Upload**.Go back to your function app logs and verify that the blob has been read.

Note

When your function app runs in the default Consumption plan, there may be a delay of up to several minutes between the blob being added or updated and the function being triggered. If you need low latency in your blob triggered functions, consider one of these

[other blob trigger options](storage-considerations#trigger-on-a-blob-container).

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

You have created a function that runs when a blob is added to or updated in Blob storage. For more information about Blob storage triggers, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob).

Now that you've created your first function, let's add an output binding to the function that writes a message to a Storage queue.


---

<!-- DOCUMENTO FUSIONADO: _legacy-proxies__functions-bindings-mcp_supported-languages.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: legacy-proxies.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/legacy-proxies -->

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

<!-- DOCUMENTO FUSIONADO: _functions-bindings-mcp_supported-languages.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-mcp.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-mcp -->

# Model Context Protocol bindings for Azure Functions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The [Model Context Protocol (MCP)](https://github.com/modelcontextprotocol) is a client-server protocol intended to enable language models and agents to more efficiently discover and use external data sources and tools.

The Azure Functions MCP extension allows you to use Azure Functions to create remote MCP servers. These servers can host MCP tool trigger functions, which MCP clients, such as language models and agents, can query and access to do specific tasks.

| Action | Type |
|---|---|
| Run a function from an MCP tool call request |
|

Important

The MCP extension doesn't currently support PowerShell apps.

## Prerequisites

- When you use the SSE transport, the MCP extension relies on Azure Queue storage provided by the
[default host storage account](storage-considerations)(`AzureWebJobsStorage`

). When using identity-based connections, make sure that your function app has at least the equivalent of these role-based permissions in the host storage account:[Storage Queue Data Reader](/en-us/azure/role-based-access-control/built-in-roles#storage-queue-data-reader)and[Storage Queue Data Message Processor](/en-us/azure/role-based-access-control/built-in-roles#storage-queue-data-message-processor). - When running locally, the MCP extension requires version 4.0.7030 of the
[Azure Functions Core Tools](functions-run-local), or a later version.

- Requires version 2.1.0 or later of the
`Microsoft.Azure.Functions.Worker`

package. - Requires version 2.0.2 or later of the
`Microsoft.Azure.Functions.Worker.Sdk`

package.

## Install extension

Note

For C#, the Azure Functions MCP extension supports only the [isolated worker model](dotnet-isolated-process-guide).

Add the extension to your project by installing this [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Mcp) in your preferred way:

`Microsoft.Azure.Functions.Worker.Extensions.Mcp`


- Requires version 3.2.2 or later of the
.`azure-functions-java-library`

dependency - Requires version 1.40.0 or later of the
.`azure-functions-maven-plugin`

dependency

- Requires version 4.9.0 or later of the
`@azure/functions`

dependency

- Requires version 1.24.0 or later of the
.`azure-functions`

package

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

You can use the `extensions.mcp`

section in `host.json`

to define MCP server information.

```
{
"version": "2.0",
"extensions": {
"mcp": {
"instructions": "Some test instructions on how to use the server",
"serverName": "TestServer",
"serverVersion": "2.0.0",
"encryptClientState": true,
"messageOptions": {
"useAbsoluteUriForEndpoint": false
},
"system": {
"webhookAuthorizationLevel": "System"
}
}
}
}
```


| Property | Description |
|---|---|
instructions |
Describes to clients how to access the remote MCP server. |
serverName |
A friendly name for the remote MCP server. |
serverVersion |
Current version of the remote MCP server. |
encryptClientState |
Determines if client state is encrypted. Defaults to true. Setting to false may be useful for debugging and test scenarios but isn't recommended for production. |
messageOptions |
Options object for the message endpoint in the SSE transport. |
messageOptions.UseAbsoluteUriForEndpoint |
Defaults to `false` . Only applicable to the server-sent events (SSE) transport; this setting doesn't affect the Streamable HTTP transport. If set to `false` , the message endpoint is provided as a relative URI during initial connections over the SSE transport. If set to `true` , the message endpoint is returned as an absolute URI. Using a relative URI isn't recommended unless you have a specific reason to do so. |
system |
Options object for system-level configuration. |
system.webhookAuthorizationLevel |
Defines the authorization level required for the webhook endpoint. Defaults to "System". Allowed values are "System" and "Anonymous". When you set the value to "Anonymous", an access key is no longer required for requests. Regardless of if a key is required or not, you can use
|

## Connect to your MCP server

To connect to the MCP server exposed by your function app, you need to provide an MCP client with the appropriate endpoint and transport information. The following table shows the transports supported by the Azure Functions MCP extension, along with their corresponding connection endpoint.

| Transport | Endpoint |
|---|---|
| Streamable HTTP | `/runtime/webhooks/mcp` |
Server-Sent Events (SSE)1 |
`/runtime/webhooks/mcp/sse` |

1 Newer protocol versions deprecated the Server-Sent Events transport. Unless your client specifically requires it, you should use the Streamable HTTP transport instead.

When hosted in Azure, by default, the endpoints exposed by the extension also require the [system key](function-keys-how-to) named `mcp_extension`

. If it isn't provided in the `x-functions-key`

HTTP header or in the `code`

query string parameter, your client receives a `401 Unauthorized`

response. You can remove this requirement by setting the `system.webhookAuthorizationLevel`

property in `host.json`

to `Anonymous`

. For more information, see the [host.json settings](#hostjson-settings) section.

You can retrieve the key using any of the methods described in [Get your function access keys](function-keys-how-to#get-your-function-access-keys). The following example shows how to get the key with the Azure CLI:

```
az functionapp keys list --resource-group <RESOURCE_GROUP> --name <APP_NAME> --query systemKeys.mcp_extension --output tsv
```


MCP clients accept this configuration in various ways. Consult the documentation for your chosen client. The following example shows an `mcp.json`

file like you might use to [configure MCP servers for GitHub Copilot in Visual Studio Code](https://code.visualstudio.com/docs/copilot/customization/mcp-servers#_configuration-format). The example sets up two servers, both using the Streamable HTTP transport. The first is for local testing with the Azure Functions Core Tools. The second is for a function app hosted in Azure. The configuration takes input parameters for which Visual Studio Code prompts you when you first run the remote server. Using inputs ensures that secrets like the system key aren't saved to the file and checked into source control.

```
{
"inputs": [
{
"type": "promptString",
"id": "functions-mcp-extension-system-key",
"description": "Azure Functions MCP Extension System Key",
"password": true
},
{
"type": "promptString",
"id": "functionapp-host",
"description": "The host domain of the function app."
}
],
"servers": {
"local-mcp-function": {
"type": "http",
"url": "http://localhost:7071/runtime/webhooks/mcp"
},
"remote-mcp-function": {
"type": "http",
"url": "https://${input:functionapp-host}/runtime/webhooks/mcp",
"headers": {
"x-functions-key": "${input:functions-mcp-extension-system-key}"
}
}
}
}
```


---

<!-- DOCUMENTO FUSIONADO: supported-languages.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/supported-languages -->

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
<!-- Source: N/A -->

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
