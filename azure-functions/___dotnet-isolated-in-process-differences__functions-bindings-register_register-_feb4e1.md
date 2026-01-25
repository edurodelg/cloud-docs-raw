---
merged_at: 2026-01-25T15:41:11.632500
merged_files: 2
---

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
