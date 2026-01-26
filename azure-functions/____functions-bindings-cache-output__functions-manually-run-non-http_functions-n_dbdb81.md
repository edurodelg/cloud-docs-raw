---
merged_at: 2026-01-26T21:02:36.338609
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __functions-bindings-cache-output__functions-manually-run-non-http_functions-nod_008c2d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-cache-output__functions-manually-run-non-http_functions-node_5a18f5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-cache-output.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache-output -->

# Azure Cache for Redis output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Cache for Redis output bindings lets you change the keys in a cache based on a set of available trigger on the cache.

For information on setup and configuration details, see the [overview](functions-bindings-cache).

## Scope of availability for functions bindings

| Binding Type | Azure Managed Redis | Azure Cache for Redis |
|---|---|---|
| Output | Yes | Yes |

Important

When using Azure Managed Redis or the Enterprise tiers of Azure Cache for Redis, use port 10000 rather than port 6380 or 6379.

Important

The Node.js v4 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Important

The Python v2 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v2 model works, refer to the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

## Example

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

The following example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

Important

For .NET functions, using the *isolated worker* model is recommended over the *in-process* model. For a comparison of the *in-process* and *isolated worker* models, see differences between the *isolated worker* model and the *in-process* model for .NET on Azure Functions.

```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.Functions.Worker.Extensions.Redis.Samples.RedisOutputBinding
{
internal class SetDeleter
{
[Function(nameof(SetDeleter))]
[RedisOutput(Common.connectionString, "DEL")]
public static string Run(
[RedisPubSubTrigger(Common.connectionString, "__keyevent@0__:set")] string key,
ILogger logger)
{
logger.LogInformation($"Deleting recently SET key '{key}'");
return key;
}
}
}
```


```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.WebJobs.Extensions.Redis.Samples.RedisOutputBinding
{
internal class SetDeleter
{
[FunctionName(nameof(SetDeleter))]
public static void Run(
[RedisPubSubTrigger(Common.connectionStringSetting, "__keyevent@0__:set")] string key,
[Redis(Common.connectionStringSetting, "DEL")] out string[] arguments,
ILogger logger)
{
logger.LogInformation($"Deleting recently SET key '{key}'");
arguments = new string[] { key };
}
}
}
```


The following example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

```
package com.function.RedisOutputBinding;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.redis.annotation.*;
public class SetDeleter {
@FunctionName("SetDeleter")
@RedisOutput(
name = "value",
connection = "redisConnectionString",
command = "DEL")
public String run(
@RedisPubSubTrigger(
name = "key",
connection = "redisConnectionString",
channel = "__keyevent@0__:set")
String key,
final ExecutionContext context) {
context.getLogger().info("Deleting recently SET key '" + key + "'");
return key;
}
}
```


This example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

The bindings are defined in the `function.json`` file:

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisConnectionString",
"channel": "__keyevent@0__:set",
"name": "key",
"direction": "in"
},
{
"type": "redis",
"connection": "redisConnectionString",
"command": "DEL",
"name": "$return",
"direction": "out"
}
],
"scriptFile": "index.js"
}
```


This code from the `index.js`

file takes the key from the trigger and returns it to the output binding to delete the cached item.

```
module.exports = async function (context, key) {
context.log("Deleting recently SET key '" + key + "'");
return key;
}
```


This example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

The bindings are defined in this `function.json`

file:

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisLocalhost",
"channel": "__keyevent@0__:set",
"name": "key",
"direction": "in"
},
{
"type": "redis",
"connection": "redisLocalhost",
"command": "DEL",
"name": "retVal",
"direction": "out"
}
],
"scriptFile": "run.ps1"
}
```


This code from the `run.ps1`

file takes the key from the trigger and passes it to the output binding to delete the cached item.

```
param($key, $TriggerMetadata)
Write-Host "Deleting recently SET key '$key'"
Push-OutputBinding -Name retVal -Value $key
```


This example shows a pub/sub trigger on the set event with an output binding to the same Redis instance. The set event triggers the cache and the output binding returns a delete command for the key that triggered the function.

The bindings are defined in this `function.json`

file:

```
{
"bindings": [
{
"type": "redisPubSubTrigger",
"connection": "redisLocalhost",
"channel": "__keyevent@0__:set",
"name": "key",
"direction": "in"
},
{
"type": "redis",
"connection": "redisLocalhost",
"command": "DEL",
"name": "$return",
"direction": "out"
}
],
"scriptFile": "__init__.py"
}
```


This code from the `__init__.py`

file takes the key from the trigger and passes it to the output binding to delete the cached item.

```
import logging
def main(key: str) -> str:
logging.info("Deleting recently SET key '" + key + "'")
return key
```


## Attributes

Note

All commands are supported for this binding.

The way in which you define an output binding parameter depends on whether your C# functions runs [in-process](functions-dotnet-class-library) or in an [isolated worker process](dotnet-isolated-process-guide).

The output binding is defined this way:

| Definition | Example | Description |
|---|---|---|
On an `out` parameter |
`[Redis(<Connection>, <Command>)] out string <Return_Variable>` |
The string variable returned by the method is a key value that the binding uses to execute the command against the specific cache. |

In this case, the type returned by the method is a key value that the binding uses to execute the command against the specific cache.

When your function has multiple output bindings, you can instead apply the binding attribute to the property of a type that is a key value, which the binding uses to execute the command against the specific cache. For more information, see [Multiple output bindings](dotnet-isolated-process-guide#multiple-output-bindings).

Regardless of the C# process mode, the same properties are supported by the output binding attribute:

| Attribute property | Description |
|---|---|
`Connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`Command`

`DEL`

.## Annotations

The `RedisOutput`

annotation supports these properties:

| Property | Description |
|---|---|
`name` |
The name of the specific input binding. |
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`command`

`DEL`

.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| Property | Description |
|---|---|
`name` |
The name of the specific input binding. |
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`command`

`DEL`

.See the [Example section](#example) for complete examples.

## Usage

The output returns a string, which is the key of the cache entry on which apply the specific command.

There are three types of connections that are allowed from an Azure Functions instance to a Redis Cache in your deployments. For local development, you can also use service principal secrets. Use the `appsettings`

to configure each of the following types of client authentication, assuming the `Connection`

was set to `Redis`

in the function.

Important

For optimal security, your function app should use Microsoft Entra ID with managed identities to authorize requests against your cache, if possible. Authorization by using Microsoft Entra ID and managed identities provides superior security and ease of use over shared access key authorization. For more information about using managed identities with your cache, see [Use Microsoft Entra ID for cache authentication](/en-us/azure/azure-cache-for-redis/cache-azure-active-directory-for-authentication).


---

<!-- DOCUMENTO FUSIONADO: _functions-manually-run-non-http_functions-node-troubleshoot.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-manually-run-non-http.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-manually-run-non-http -->

# Manually run a non HTTP-triggered function

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article demonstrates how to manually run a non HTTP-triggered function via specially formatted HTTP request.

In some contexts, such as during development and troubleshooting, you might need to run "on-demand" an Azure Function that is indirectly triggered. Examples of indirect triggers include [functions on a schedule](functions-create-scheduled-function) or functions that run as the [result of events](functions-create-storage-blob-triggered-function).

The procedure described in this article is equivalent to using the **Test/Run** functionality of a function's **Code + Test** tab in the Azure portal. You can also use Visual Studio Code to [manually run functions](functions-develop-vs-code#run-functions).

## Prerequisites

The examples in this article use an HTTP test tool. Make sure to choose a tool that keeps your data secure. For more information, see [HTTP test tools](functions-develop-local#http-test-tools).

## Define the request location

To run a non HTTP-triggered function, you need a way to send a request to Azure to run the function. The URL used to make this request takes a specific form.

**Host name:**The function app's public location that is made up from the function app's name plus*azurewebsites.net*or your custom domain. When you work with[deployment slots](functions-deployment-slots)used for staging, the host name portion is the production host name with`-<slotname>`

appended to it. In the previous example, the URL would be`myfunctiondemos-staging.azurewebsites.net`

for a slot named`staging`

.**Folder path:**To access non HTTP-triggered functions via an HTTP request, you have to send the request through the path`admin/functions`

. APIs under the`/admin/`

path are only accessible with authorization.**Function name:**The name of the function you want to run.

The following considerations apply when making requests to administrator endpoints in your function app:

- When making requests to any endpoint under the
`/admin/`

path, you must supply your app's master key in the`x-functions-key`

header of the request. - When you run locally, authorization isn't enforced and the function's master key isn't required. You can directly
[call the function](#call-the-function)omitting the`x-functions-key`

header. - When accessing function app endpoints in a
[deployment slot](functions-deployment-slots), make sure you use the slot-specific host name in the request URL, along with the slot-specific master key.

## Get the master key

You can get the master key from either the Azure portal or by using the Azure CLI.

Caution

Due to the elevated permissions in your function app granted by the master key, you shouldn't share this key with third parties or distribute it in an application. The key should only be sent to an HTTPS endpoint.

Navigate to your function app in the

[Azure portal](https://portal.azure.com), select**App Keys**, and then the`_master`

key.In the

**Edit key**section, copy the key value to your clipboard, and then select**OK**.

## Call the function

In the Azure portal, navigate top your function app and choose your function.

Select

**Code + Test**, and then select**Logs**. You see messages from the function logged here when you manually run the function from your HTTP test tool.In your HTTP test tool, use the request location you defined as the request URL, make sure that the HTTP request method is POST, and include these two request headers:

Key Value `x-functions-key`

The master key value pasted from the clipboard. `Content-Type`

`application/json`

Make sure that the POST request payload/body is

`{ "input": "<TRIGGER_INPUT>" }`

. The specific`<TRIGGER_INPUT>`

you supply depends on the type of trigger, but it can only be a string, numeric, or boolean value. For services that use JSON payloads, such as Azure Service Bus, the test JSON payload should be escaped and serialized as a string.If you don't want to pass input data to the function, you must still supply an empty dictionary

`{}`

as the body of the POST request. For more information, see the reference article for the specific non-HTTP trigger.Send the HTTP POST request. The response should be an HTTP 202 (Accepted) response.

Next, return to your function in the Azure portal. Review the logs and you see messages coming from the manual call to the function.


The way that you access data sent to the trigger depends on the type of trigger and your function language. For more information, see the reference examples for your [specific trigger](functions-triggers-bindings).


---

<!-- DOCUMENTO FUSIONADO: functions-node-troubleshoot.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-node-troubleshoot -->

# Troubleshoot Node.js apps in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The content of this article changes based on your choice of the Node.js programming model in the selector at the top of the page. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. Learn more about the differences between v3 and v4 in the [migration guide](functions-node-upgrade-v4).

This article provides a guide for troubleshooting common scenarios in Node.js function apps.

The **Diagnose and solve problems** tab in the [Azure portal](https://portal.azure.com) is a useful resource to monitor and diagnose possible issues related to your application. It also supplies potential solutions to your problems based on the diagnosis. For more information, see [Azure Function app diagnostics](functions-diagnostics).

Another useful resource is the **Logs** tab in the [Azure portal](https://portal.azure.com) for your Application Insights instance so that you can run custom [KQL queries](/en-us/azure/data-explorer/kusto/query/). The following example query shows how to view errors and warnings for your app in the past day:

```
let myAppName = "<your app name>";
let startTime = ago(1d);
let endTime = now();
union traces,requests,exceptions
| where cloud_RoleName =~ myAppName
| where timestamp between (startTime .. endTime)
| where severityLevel > 2
```


If those resources didn't solve your problem, the following sections provide advice for specific application issues:

## No functions found

If you see any of the following errors in your logs:

No HTTP triggers found.


No job functions found. Try making your job classes and methods public. If you're using binding extensions (e.g. Azure Storage, ServiceBus, Timers, etc.) make sure you've called the registration method for the extension(s) in your startup code (e.g. builder.AddAzureStorage(), builder.AddServiceBus(), builder.AddTimers(), etc.).


Try the following fixes:

- When running locally, make sure you're using Azure Functions Core Tools v4.0.5382 or higher.
- When running in Azure:
Make sure you're using

[Azure Functions Runtime Version](functions-versions)4.25 or higher.Make sure you're using Node.js v18 or higher.

Set the app setting

`FUNCTIONS_NODE_BLOCK_ON_ENTRY_POINT_ERROR`

to`true`

. This setting is recommended for all model v4 apps and ensures that all entry point errors are visible in your application insights logs. For more information, see[App settings reference for Azure Functions](functions-app-settings#functions_node_block_on_entry_point_error).Check your function app logs for entry point errors. The following example query shows how to view entry point errors for your app in the past day:

`let myAppName = "<your app name>"; let startTime = ago(1d); let endTime = now(); union traces,requests,exceptions | where cloud_RoleName =~ myAppName | where timestamp between (startTime .. endTime) | where severityLevel > 2 | where message has "entry point"`


- Make sure your app has the
[required folder structure](functions-reference-node?pivots=nodejs-model-v3#folder-structure)with a*host.json*at the root and a folder for each function containing a*function.json*file.

## Undici request is not a constructor

If you get the following error in your function app logs:

System.Private.CoreLib: Exception while executing function: Functions.httpTrigger1. System.Private.CoreLib: Result: Failure Exception: undici_1.Request is not a constructor


Make sure you're using Node.js version 18.x or higher.

## Failed to detect the Azure Functions runtime

If you get the following error in your function app logs:

WARNING: Failed to detect the Azure Functions runtime. Switching "@azure/functions" package to test mode - not all features are supported.


Check your `package.json`

file for a reference to `applicationinsights`

and make sure the version is `^2.7.1`

or higher. After updating the version, run `npm install`


## Get help from Microsoft

You can get more help from Microsoft in one of the following ways:

- Search the known issues in the
[Azure Functions Node.js repository](https://github.com/Azure/azure-functions-nodejs-library/issues). If you don't see your issue mentioned, create a new issue and let us know what has happened. - If you're not able to diagnose your problem using this guide, Microsoft support engineers are available to help diagnose issues with your application. Microsoft offers
[various support plans](https://azure.microsoft.com/support/plans). Create a support ticket in the**Support + troubleshooting**section of your function app page in the[Azure portal](https://portal.azure.com).


---

<!-- DOCUMENTO FUSIONADO: functions-deployment-technologies.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-deployment-technologies -->

# Deployment technologies in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can use several different technologies to deploy your Azure Functions project code to Azure. This article provides an overview of the deployment methods available to you and recommendations for the best method to use in various scenarios. It also provides a comprehensive list of and key details about the underlying deployment technologies.

## Deployment methods

The deployment technology you use to publish code to your function app in Azure depends on your specific needs and the point in the development cycle. For example, during development and testing, you can deploy directly from your development tool, such as Visual Studio Code. When your app is in production, you're more likely to publish continuously from source control or by using an automated publishing pipeline, which can include validation and testing.

The following table describes the available deployment methods for your code project.

| Deployment type | Methods | Best for... |
|---|---|---|
| Tools-based | •
•
•
•
|

[local development tools](functions-develop-local#local-development-environments).[Deployment Center (CI/CD)](functions-continuous-deployment)•

[Container deployments](functions-how-to-custom-container#enable-continuous-deployment-to-azure)[Azure Pipelines](functions-how-to-azure-devops)•

[GitHub Actions](functions-how-to-github-actions)Use the best technology for your specific scenario. Many of the deployment methods are based on [zip deployment](#zip-deploy), which is recommended for deployment.

## Deployment technology availability

The deployment method also depends on the hosting plan and operating system on which you run your function app.

Currently, Functions offers five options for hosting your function apps:

[Flex Consumption plan](flex-consumption-plan)[Consumption](consumption-plan)[Elastic Premium plan](functions-premium-plan)[Dedicated (App Service) plan](dedicated-plan)[Azure Container Apps](../container-apps/functions-overview)

Each plan has different behaviors. Not all deployment technologies are available for each hosting plan and operating system. This chart provides information on the supported deployment technologies:

| Deployment technology | Flex Consumption | Consumption | Elastic Premium | Dedicated | Container Apps |
|---|---|---|---|---|---|
|

[Zip deploy](#zip-deploy)[External package URL](#external-package-url)1[Docker container](#docker-container)[Source control](#source-control)[Local Git](#local-git)1[FTPS](#ftps)1[In-portal editing](#portal-editing)21 Deployment technologies that require you to [manually sync triggers](#trigger-syncing) aren't recommended.

2 In-portal editing is disabled when code is deployed to your function app from outside the portal. For more information, including language support details for in-portal editing, see [Language support details](supported-languages#language-support-details).

## Key concepts

Some key concepts are critical to understanding how deployments work in Azure Functions.

### Trigger syncing

When you change any of your triggers, the Functions infrastructure must be aware of the changes. Synchronization happens automatically for many deployment technologies. However, in some cases, you must manually sync your triggers.

You must always manually sync triggers when using these deployment options:

You can manually sync triggers in one of these ways:

Restart your function app in the Azure portal. The Functions host performs a background trigger sync after the application starts.

Use the

command to send an HTTP POST request that calls the`az rest`

`syncfunctiontriggers`

API, as in this example:`az rest --method post --url https://management.azure.com/subscriptions/<SUBSCRIPTION_ID>/resourceGroups/<RESOURCE_GROUP>/providers/Microsoft.Web/sites/<APP_NAME>/syncfunctiontriggers?api-version=2016-08-01`


Keep these considerations in mind for the sync triggers operation:

- You must manually restart your function app any time you deploy an updated version of the deployment package by using the same external package URL.
- For apps running in a Consumption or Elastic Premium plan, you must also
[manually sync triggers](#trigger-syncing)in these scenarios:- When deployments use an external package URL with a resource manager-based deployment by using ARM templates or Bicep or Terraform files.
- When you update the deployment package
*in-place*by using the same external package URL.

- When you add network restrictions to an existing function app, you must guarantee connectivity to the default host storage account set in the
`AzureWebJobsStorage`

app setting. For more information, see[How to use a secured storage account with Azure Functions](configure-networking-how-to).

### Remote build

You can request Azure Functions to perform a remote build of your code project during deployment. In these scenarios, request a remote build instead of building locally:

- You're deploying an app to a Linux-based function app that you developed on a Windows computer. This situation is commonly the case for Python app development. You can end up with incorrect libraries when you build the deployment package locally on Windows.
- Your project has dependencies on a
[custom package index](python-build-options#remote-build-with-an-extra-index-url). - You want to reduce the size of your deployment package.

How you request a remote build depends on whether your app runs in Azure on Windows or Linux.

All function apps running on Windows have a small management app, the `scm`

site provided by [Kudu](https://github.com/projectkudu/kudu). This site handles much of the deployment and build logic for Azure Functions.

When you deploy an app to Windows, the deployment process runs language-specific commands, like `dotnet restore`

(C#) or `npm install`

(JavaScript).

The following considerations apply when using remote builds during deployment:

- Remote builds are supported for function apps running on Linux in the Consumption plan. However, deployment options are limited for these apps because they don't have an
`scm`

(Kudu) site. - Function apps running on Linux in a
[Premium plan](functions-premium-plan)or in a[Dedicated (App Service) plan](dedicated-plan)do have an`scm`

(Kudu) site, but it's limited compared to Windows. - Remote builds don't occur when an app uses
[run-from-package](run-functions-from-deployment-package). To learn how to use remote build in these cases, see[Zip deploy](#zip-deploy). - You might have issues with remote build when your app was created before the feature was made available (August 1, 2019). For older apps, either create a new function app or run
`az functionapp update --resource-group <RESOURCE_GROUP_NAME> --name <APP_NAME>`

to update your function app. This command might take two tries to succeed.

### App content storage

Package-based deployment methods store the package in the storage account associated with the function app, which the [AzureWebJobsStorage](functions-app-settings#azurewebjobsstorage) setting defines. When available, Consumption and Elastic Premium plan apps try to use the Azure Files content share from this account, but you can also maintain the package in another location. Flex Consumption plan apps use a storage container in default storage account, unless you [configure a different storage account to use for deployment](flex-consumption-how-to#configure-deployment-settings). For more information, review the details in **Where app content is stored** in each deployment technology covered in the next section.

Important

The storage account is used to store important app data, sometimes including the application code itself. You should limit access from other apps and users to the storage account.

## Deployment technology details

The following deployment methods are available in Azure Functions. To determine which technologies each hosting plan supports, refer to the [deployment technology availability](#deployment-technology-availability) table.

### One deploy

One deploy is the only deployment technology supported for apps on a [Flex Consumption plan](flex-consumption-plan). The end result is a ready-to-run .zip package that your function app runs on.


How to use it:Deploy by using the[Visual Studio Code]publish feature, or from the command line by using[Azure Functions Core Tools]or the[Azure CLI]. Our[Azure Dev Ops Task]and[GitHub Action]similarly leverage one deploy when they detect that a Flex Consumption app is being deployed to.When you create a Flex Consumption app, you must specify a deployment storage (blob) container as well as an authentication method to it. By default the same storage account as the

`AzureWebJobsStorage`

connection is used, with a connection string as the authentication method. Thus, your[deployment settings]are configured during app create time without any need of application settings.


When to use it:One deploy is the only deployment technology available for function apps running in a Flex Consumption plan.


Where app content is stored:When you create a Flex Consumption function app, you specify a[deployment storage container]. This blob container is where your tools upload the app content you deployed. To change the location, you can visit the Deployment Settings blade in the Azure portal or use the[Azure CLI].

Tip

A **Flex Function App deployment details** diagnostic tool is available in the Azure portal. Open your Flex Consumption app, select **Diagnose and solve problems**, and search for `Flex Function App deployment details`

. This tool displays detailed information about your deployments, including deployment history, package status, and troubleshooting recommendations.

### Zip deploy

Zip deploy is the default and recommended deployment technology for function apps on the Consumption, Elastic Premium, and App Service (Dedicated) plans. The end result is a ready-to-run .zip package that your function app runs on. It differs from [external package URL](#external-package-url) in that the platform is responsible for remote building and storing your app content.


How to use it:Deploy by using your favorite client tool:[Visual Studio Code],[Visual Studio], or from the command line using[Azure Functions Core Tools]or the[Azure CLI]. Our[Azure Dev Ops Task]and[GitHub Action]similarly leverage zip deploy.When you deploy by using zip deploy, you can set your app to

[run from package]. To run from package, set the[application setting value to]`WEBSITE_RUN_FROM_PACKAGE`

`1`

. We recommend zip deployment. It yields faster loading times for your applications, and it's the default for VS Code, Visual Studio, and the Azure CLI.


When to use it:Zip deploy is the default and recommended deployment technology for function apps on the Windows Consumption, Windows and Linux Elastic Premium, and Windows and Linux App Service (Dedicated) plans.


Where app content is stored:App content from a zip deploy is by default stored on the file system, which Azure might back by Azure Files from the storage account you specify when creating the function app. In Linux Consumption, the app content is instead persisted on a blob in the storage account specified by the`AzureWebJobsStorage`

app setting, and the app setting`WEBSITE_RUN_FROM_PACKAGE`

takes on the value of the blob URL.

### External package URL

External package URL is an option if you want to manually control how deployments are performed. You take responsibility for uploading a ready-to-run .zip package containing your built app content to blob storage and referencing this external URL as an application setting on your function app. Whenever your app restarts, it fetches the package, mounts it, and runs in [Run From Package](run-functions-from-deployment-package) mode.


How to use it:Add[to your application settings. The value of this setting should be a blob URL pointing to the location of the specific package you want your app to run. You can add settings either]`WEBSITE_RUN_FROM_PACKAGE`

[in the portal]or[by using the Azure CLI].If you use Azure Blob Storage, your Function app can access the container either by using a managed identity-based connection or with a

[shared access signature (SAS)]. The option you choose affects what kind of URL you use as the value for`WEBSITE_RUN_FROM_PACKAGE`

. Managed identity is recommended for overall security and because SAS tokens expire and must be manually maintained.Whenever you deploy the package file that a function app references, you must

[manually sync triggers], including the initial deployment. When you change the contents of the package file and not the URL itself, you must also restart your function app to sync triggers. Refer to our[how-to guide]on configuring this deployment technology.


When to use it:External package URL is the only supported deployment method for apps running on the Linux Consumption plan when you don't want a[remote build]to occur. This method is also the recommended deployment technology when you[create your app without Azure Files]. For scalable apps running on Linux, you should instead consider[Flex Consumption plan]hosting.


Where app content is stored:You are responsible for uploading your app content to blob storage. You may use any blob storage account, though Azure Blob Storage is recommended.

### Docker container

You can deploy a function app running in a Linux container.


How to use it:[Create your functions in a Linux container]then deploy the container to a Premium or Dedicated plan in Azure Functions or another container host. Use the[Azure Functions Core Tools]to create a customized Dockerfile for your project that you use to build a containerized function app. You can use the container in the following deployments:

- Deploy to Azure Functions resources you create in the Azure portal. For more information, see
[Azure portal create using containers].- Deploy to Azure Functions resources you create from the command line. Requires either a Premium or Dedicated (App Service) plan. To learn how, see
[Create your first containerized Azure Functions].- Deploy to Azure Container Apps. To learn how, see
[Create your first containerized Azure Functions on Azure Container Apps].- Deploy to a Kubernetes cluster. You can deploy to a cluster using
[Azure Functions Core Tools]. Use the[command.]`func kubernetes deploy`


When to use it:Use the Docker container option when you need more control over the Linux environment where your function app runs and where the container is hosted. This deployment mechanism is available only for functions running on Linux.


Where app content is stored:You store app content in the specified container registry as a part of the image.

### Source control

You can enable continuous integration between your function app and a source code repository. When you enable source control, an update to code in the connected source repository triggers deployment of the latest code from the repository. For more information, see the [Continuous deployment for Azure Functions](functions-continuous-deployment).


How to use it:The easiest way to set up publishing from source control is from the Deployment Center in the Functions area of the portal. For more information, see[Continuous deployment for Azure Functions].


When to use it:Using source control is the best practice for teams that collaborate on their function apps. Source control is a good deployment option that enables more sophisticated deployment pipelines. Usually, you enable source control on a staging slot, which you can swap into production after validation of updates from the repository. For more information, see[Azure Functions deployment slots].


Where app content is stored:The source control system stores the app content. The app file system stores a locally cloned and built app content form, which Azure Files from the storage account specified when the function app was created might back.

### Local Git

Use local Git to push code from your local machine to Azure Functions by using Git.


How to use it:Follow the instructions in[Local Git deployment to Azure App Service].


When to use it:To reduce the chance of errors, avoid using deployment methods that require the additional step of[manually syncing triggers]. Use[zip deployment]when possible.


Where app content is stored:App content is stored on the file system, which might be backed by Azure Files from the storage account you specify when creating the function app.

### FTP/S

You can use FTP/S to directly transfer files to Azure Functions, but don't use this deployment method. When you aren't planning on using FTP, disable it. If you choose to use FTP, enforce FTPS. To learn how in the Azure portal, see [Enforce FTPS](../app-service/deploy-ftp#enforce-ftps).


How to use it:Follow the instructions in[FTPS deployment settings]to get the URL and credentials you can use to deploy to your function app by using FTPS.


When to use it:To reduce the chance of errors, avoid using deployment methods that require the additional step of[manually syncing triggers]. Use[zip deployment]when possible.


Where app content is stored:App content is stored on the file system. FTP/FTPS deployments fail when your app's file system is backed by Azure Files in the default host storage account. FTP/FTPS fails with Azure Files as mounted storage because of[FTP limitations].

### Portal editing

In the portal-based editor, you can directly edit the files that are in your function app (essentially deploying every time you save your changes).


How to use it:To edit your functions in the[Azure portal], you must[create your functions in the portal]. To preserve a single source of truth, using any other deployment method makes your function read-only and prevents continued portal editing. To return to a state in which you can edit your files in the Azure portal, you can manually turn the edit mode back to`Read/Write`

and remove any deployment-related application settings (like[).]`WEBSITE_RUN_FROM_PACKAGE`


When to use it:The portal is a good way to get started with Azure Functions. Because of[development limitations in the Azure portal], you should use one of the following client tools for more advanced development work:


Where app content is stored:App content is stored on the file system, which might be backed by Azure Files from the storage account you specify when creating the function app.

## Deployment behaviors

When you deploy updates to your function app code, the deployment behavior depends on your hosting plan:

**Consumption, Elastic Premium, and Dedicated plans:** Currently executing functions are terminated when new code is deployed. After deployment completes, the new code is loaded to begin processing requests. This forceful termination behavior is known as a recreate strategy. For near zero-downtime deployments on Consumption, Elastic Premium, and Dedicated plans, use [deployment slots](#deployment-slots).

Review [Improve the performance and reliability of Azure Functions](performance-reliability#write-functions-to-be-stateless) to learn how to write stateless and defensive functions.

**Flex Consumption plan:** The default behavior also uses the recreate strategy, terminating currently executing functions during deployment. However, Flex Consumption uniquely supports two different site update strategies. You can [configure rolling updates](flex-consumption-site-updates) for zero-downtime deployments.

## Deployment slots

When you deploy your function app to Azure, you can deploy to a separate deployment slot instead of directly to production. Deploying to a deployment slot and then swapping into production after verification is the recommended way to configure [continuous deployment](functions-continuous-deployment).

The way that you deploy to a slot depends on the specific deployment tool you use. For example, when using Azure Functions Core Tools, you include the `--slot`

option to indicate the name of a specific slot for the [ func azure functionapp publish](functions-core-tools-reference#func-azure-functionapp-publish) command.

For more information on deployment slots, see the [Azure Functions Deployment Slots](functions-deployment-slots) documentation.

## Next steps

Read these articles to learn more about deploying your function apps:


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-http-webhook-trigger.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-http-webhook-trigger -->

# Azure Functions HTTP trigger

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The HTTP trigger lets you invoke a function with an HTTP request. You can use an HTTP trigger to build serverless APIs and respond to webhooks.

The default return value for an HTTP-triggered function is:

`HTTP 204 No Content`

with an empty body in Functions 2.x and higher`HTTP 200 OK`

with an empty body in Functions 1.x

To modify the HTTP response, configure an [output binding](functions-bindings-http-webhook-output).

For more information about HTTP bindings, see the [overview](functions-bindings-http-webhook) and [output binding reference](functions-bindings-http-webhook-output).

Tip

If you plan to use the HTTP or WebHook bindings, plan to avoid port exhaustion that can be caused by improper instantiation of `HttpClient`

. For more information, see [How to manage connections in Azure Functions](manage-connections).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

## Example

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The code in this article defaults to .NET Core syntax, used in Functions version 2.x and higher. For information on the 1.x syntax, see the [1.x functions templates](https://github.com/Azure/azure-functions-templates/tree/v1.x/Functions.Templates/Templates).

The following example shows an HTTP trigger that returns a "hello, world" response as an [IActionResult](/en-us/dotnet/api/microsoft.aspnetcore.mvc.iactionresult), using [ASP.NET Core integration in .NET Isolated](dotnet-isolated-process-guide#aspnet-core-integration):

```
[Function("HttpFunction")]
public IActionResult Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get")] HttpRequest req)
{
return new OkObjectResult($"Welcome to Azure Functions, {req.Query["name"]}!");
}
```


The following example shows an HTTP trigger that returns a "hello world" response as an [HttpResponseData](/en-us/dotnet/api/microsoft.azure.functions.worker.http.httpresponsedata) object:

```
[Function(nameof(HttpFunction))]
public static HttpResponseData Run([HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)] HttpRequestData req,
FunctionContext executionContext)
{
var logger = executionContext.GetLogger(nameof(HttpFunction));
logger.LogInformation("message logged");
var response = req.CreateResponse(HttpStatusCode.OK);
response.Headers.Add("Content-Type", "text/plain; charset=utf-8");
response.WriteString("Welcome to .NET isolated worker !!");
return response;
}
```


This section contains the following examples:

[Read parameter from the query string](#read-parameter-from-the-query-string)[Read body from a POST request](#read-body-from-a-post-request)[Read parameter from a route](#read-parameter-from-a-route)[Read POJO body from a POST request](#read-pojo-body-from-a-post-request)

The following examples show the HTTP trigger binding.

#### Read parameter from the query string

This example reads a parameter, named `id`

, from the query string, and uses it to build a JSON document returned to the client, with content type `application/json`

.

```
@FunctionName("TriggerStringGet")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
final ExecutionContext context) {
// Item list
context.getLogger().info("GET parameters are: " + request.getQueryParameters());
// Get named parameter
String id = request.getQueryParameters().getOrDefault("id", "");
// Convert and display
if (id.isEmpty()) {
return request.createResponseBuilder(HttpStatus.BAD_REQUEST)
.body("Document not found.")
.build();
}
else {
// return JSON from to the client
// Generate document
final String name = "fake_name";
final String jsonDocument = "{\"id\":\"" + id + "\", " +
"\"description\": \"" + name + "\"}";
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(jsonDocument)
.build();
}
}
```


#### Read body from a POST request

This example reads the body of a POST request, as a `String`

, and uses it to build a JSON document returned to the client, with content type `application/json`

.

```
@FunctionName("TriggerStringPost")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
final ExecutionContext context) {
// Item list
context.getLogger().info("Request body is: " + request.getBody().orElse(""));
// Check request body
if (!request.getBody().isPresent()) {
return request.createResponseBuilder(HttpStatus.BAD_REQUEST)
.body("Document not found.")
.build();
}
else {
// return JSON from to the client
// Generate document
final String body = request.getBody().get();
final String jsonDocument = "{\"id\":\"123456\", " +
"\"description\": \"" + body + "\"}";
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(jsonDocument)
.build();
}
}
```


#### Read parameter from a route

This example reads a mandatory parameter, named `id`

, and an optional parameter `name`

from the route path, and uses them to build a JSON document returned to the client, with content type `application/json`

.

```
@FunctionName("TriggerStringRoute")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "trigger/{id}/{name=EMPTY}") // name is optional and defaults to EMPTY
HttpRequestMessage<Optional<String>> request,
@BindingName("id") String id,
@BindingName("name") String name,
final ExecutionContext context) {
// Item list
context.getLogger().info("Route parameters are: " + id);
// Convert and display
if (id == null) {
return request.createResponseBuilder(HttpStatus.BAD_REQUEST)
.body("Document not found.")
.build();
}
else {
// return JSON from to the client
// Generate document
final String jsonDocument = "{\"id\":\"" + id + "\", " +
"\"description\": \"" + name + "\"}";
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(jsonDocument)
.build();
}
}
```


#### Read POJO body from a POST request

Here's the code for the `ToDoItem`

class, referenced in this example:

```
public class ToDoItem {
private String id;
private String description;
public ToDoItem(String id, String description) {
this.id = id;
this.description = description;
}
public String getId() {
return id;
}
public String getDescription() {
return description;
}
@Override
public String toString() {
return "ToDoItem={id=" + id + ",description=" + description + "}";
}
}
```


This example reads the body of a POST request. The request body gets automatically de-serialized into a `ToDoItem`

object, and is returned to the client, with content type `application/json`

. The `ToDoItem`

parameter is serialized by the Functions runtime as it is assigned to the `body`

property of the `HttpMessageResponse.Builder`

class.

```
@FunctionName("TriggerPojoPost")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<ToDoItem>> request,
final ExecutionContext context) {
// Item list
context.getLogger().info("Request body is: " + request.getBody().orElse(null));
// Check request body
if (!request.getBody().isPresent()) {
return request.createResponseBuilder(HttpStatus.BAD_REQUEST)
.body("Document not found.")
.build();
}
else {
// return JSON from to the client
// Generate document
final ToDoItem body = request.getBody().get();
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(body)
.build();
}
}
```


The following example shows an HTTP trigger [TypeScript function](functions-reference-node?tabs=typescript). The function looks for a `name`

parameter either in the query string or the body of the [HTTP request](functions-reference-node?tabs=typescript&pivots=nodejs-model-v4#http-request).

```
import { app, HttpRequest, HttpResponseInit, InvocationContext } from '@azure/functions';
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text()) || 'world';
return { body: `Hello, ${name}!` };
}
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: httpTrigger1,
});
```


The following example shows an HTTP trigger [JavaScript function](functions-reference-node). The function looks for a `name`

parameter either in the query string or the body of the [HTTP request](functions-reference-node?tabs=javascript&pivots=nodejs-model-v4#http-request).

```
const { app } = require('@azure/functions');
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: async (request, context) => {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text()) || 'world';
return { body: `Hello, ${name}!` };
},
});
```


The following example shows a trigger binding in a *function.json* file and a [PowerShell function](functions-reference-powershell). The function looks for a `name`

parameter either in the query string or the body of the HTTP request.

```
{
"bindings": [
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "Request",
"methods": [
"get",
"post"
]
},
{
"type": "http",
"direction": "out",
"name": "Response"
}
]
}
```


```
using namespace System.Net
# Input bindings are passed in via param block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell HTTP trigger function processed a request."
# Interact with query parameters or the body of the request.
$name = $Request.Query.Name
if (-not $name) {
$name = $Request.Body.Name
}
$body = "This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response."
if ($name) {
$body = "Hello, $name. This HTTP triggered function executed successfully."
}
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $body
})
```


This example is an HTTP triggered function that uses [HTTP streams](functions-bindings-http-webhook-trigger?tabs=python-v2&pivots=programming-language-python#http-streams-1) to return chunked response data. You might use these capabilities to support scenarios like sending event data through a pipeline for real time visualization or detecting anomalies in large sets of data and providing instant notifications.

```
import time
import azure.functions as func
from azurefunctions.extensions.http.fastapi import Request, StreamingResponse
app = func.FunctionApp(http_auth_level=func.AuthLevel.FUNCTION)
def generate_sensor_data():
"""Generate real-time sensor data."""
for i in range(10):
# Simulate temperature and humidity readings
temperature = 20 + i
humidity = 50 + i
yield f"data: {{'temperature': {temperature}, 'humidity': {humidity}}}\n\n"
time.sleep(1)
@app.route(route="stream", methods=[func.HttpMethod.GET])
async def stream_sensor_data(req: Request) -> StreamingResponse:
"""Endpoint to stream real-time sensor data."""
return StreamingResponse(generate_sensor_data(), media_type="text/event-stream")
```


To learn more, including how to enable HTTP streams in your project, see [HTTP streams](functions-bindings-http-webhook-trigger?tabs=python-v2&pivots=programming-language-python#http-streams-1).

This example shows a trigger binding and a Python function that uses the binding. The function looks for a `name`

parameter either in the query string or the body of the HTTP request.

```
import azure.functions as func
import logging
app = func.FunctionApp()
@app.function_name(name="HttpTrigger1")
@app.route(route="hello", auth_level=func.AuthLevel.ANONYMOUS)
def test_function(req: func.HttpRequest) -> func.HttpResponse:
logging.info('Python HTTP trigger function processed a request.')
return func.HttpResponse(
"This HTTP triggered function executed successfully.",
status_code=200
)
```


## Attributes

Both the [isolated worker model](dotnet-isolated-process-guide) and the [in-process model](functions-dotnet-class-library) use the `HttpTriggerAttribute`

to define the trigger binding. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#http-trigger).

In [isolated worker model](dotnet-isolated-process-guide) function apps, the `HttpTriggerAttribute`

supports the following parameters:

| Parameters | Description |
|---|---|
AuthLevel |
Determines what keys, if any, need to be present on the request in order to invoke the function. For supported values, see
|

**Methods**[customize the HTTP endpoint](#customize-the-http-endpoint).**Route**`<functionname>`

. For more information, see [customize the HTTP endpoint](#customize-the-http-endpoint).## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, the following properties for a trigger are defined in the `route`

decorator, which adds HttpTrigger and HttpOutput binding:

| Property | Description |
|---|---|
`route` |
Route for the http endpoint. If None, it will be set to function name if present or user-defined python function name. |
`trigger_arg_name` |
Argument name for HttpRequest. The default value is 'req'. |
`binding_arg_name` |
Argument name for HttpResponse. The default value is '$return'. |
`methods` |
A tuple of the HTTP methods to which the function responds. |
`auth_level` |
Determines what keys, if any, need to be present on the request in order to invoke the function. |

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the [HttpTrigger](/en-us/java/api/com.microsoft.azure.functions.annotation.httptrigger) annotation, which supports the following settings:

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `app.http()`

method.

| Property | Description |
|---|---|
authLevel |
Determines what keys, if any, need to be present on the request in order to invoke the function. For supported values, see
|

**methods**[customize the HTTP endpoint](#customize-the-http-endpoint).**route**`<functionname>`

. For more information, see [customize the HTTP endpoint](#customize-the-http-endpoint).The following table explains the trigger configuration properties that you set in the *function.json* file, which differs by runtime version.

The following table explains the binding configuration properties that you set in the *function.json* file.

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

**methods**[customize the HTTP endpoint](#customize-the-http-endpoint).**route**`<functionname>`

. For more information, see [customize the HTTP endpoint](#customize-the-http-endpoint).## Usage

This section details how to configure your HTTP trigger function binding.

The [HttpTrigger](/en-us/java/api/com.microsoft.azure.functions.annotation.httptrigger) annotation should be applied to a method parameter of one of the following types:

[HttpRequestMessage<T>](/en-us/java/api/com.microsoft.azure.functions.httprequestmessage).- Any native Java types such as int, String, byte[].
- Nullable values using Optional.
- Any plain-old Java object (POJO) type.

### Payload

The trigger input type is declared as one of the following types:

| Type | Description |
|---|---|
|

*Use of this type requires that the app is configured with*[ASP.NET Core integration in .NET Isolated](dotnet-isolated-process-guide#aspnet-core-integration).This gives you full access to the request object and overall HttpContext.

[HttpRequestData](/en-us/dotnet/api/microsoft.azure.functions.worker.http.httprequestdata)When the trigger parameter is of type `HttpRequestData`

or `HttpRequest`

, custom types can also be bound to other parameters using `Microsoft.Azure.Functions.Worker.Http.FromBodyAttribute`

. Use of this attribute requires [ Microsoft.Azure.Functions.Worker.Extensions.Http version 3.1.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Http). This is a different type than the similar attribute in

`Microsoft.AspNetCore.Mvc`

. When using ASP.NET Core integration, you need a fully qualified reference or `using`

statement. This example shows how to use the attribute to get just the body contents while still having access to the full `HttpRequest`

, using ASP.NET Core integration:```
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
namespace AspNetIntegration
{
public class BodyBindingHttpTrigger
{
[Function(nameof(BodyBindingHttpTrigger))]
public IActionResult Run([HttpTrigger(AuthorizationLevel.Anonymous, "post")] HttpRequest req,
[Microsoft.Azure.Functions.Worker.Http.FromBody] Person person)
{
return new OkObjectResult(person);
}
}
public record Person(string Name, int Age);
}
```


### Customize the HTTP endpoint

By default when you create a function for an HTTP trigger, the function is addressable with a route of the form:

```
https://<APP_NAME>.azurewebsites.net/api/<FUNCTION_NAME>
```


You can customize this route using the optional `route`

property on the HTTP trigger's input binding. You can use any [ASP.NET Core Route Constraint](/en-us/aspnet/core/fundamentals/routing#route-constraints) with your parameters.

The following function code accepts two parameters `category`

and `id`

in the route and writes a response using both parameters.

```
[Function("HttpTrigger1")]
public static HttpResponseData Run([HttpTrigger(AuthorizationLevel.Function, "get", "post",
Route = "products/{category:alpha}/{id:int?}")] HttpRequestData req, string category, int? id,
FunctionContext executionContext)
{
var logger = executionContext.GetLogger("HttpTrigger1");
logger.LogInformation("C# HTTP trigger function processed a request.");
var message = String.Format($"Category: {category}, ID: {id}");
var response = req.CreateResponse(HttpStatusCode.OK);
response.Headers.Add("Content-Type", "text/plain; charset=utf-8");
response.WriteString(message);
return response;
}
```


Route parameters are defined using the `route`

setting of the `HttpTrigger`

annotation. The following function code accepts two parameters `category`

and `id`

in the route and writes a response using both parameters.

```
package com.function;
import java.util.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.*;
public class HttpTriggerJava {
public HttpResponseMessage<String> HttpTrigger(
@HttpTrigger(name = "req",
methods = {"get"},
authLevel = AuthorizationLevel.FUNCTION,
route = "products/{category:alpha}/{id:int}") HttpRequestMessage<String> request,
@BindingName("category") String category,
@BindingName("id") int id,
final ExecutionContext context) {
String message = String.format("Category %s, ID: %d", category, id);
return request.createResponseBuilder(HttpStatus.OK).body(message).build();
}
}
```


As an example, the following TypeScript code defines a `route`

property for an HTTP trigger with two parameters, `category`

and `id`

. The example reads the parameters from the request and returns their values in the response.

```
import { app, HttpRequest, HttpResponseInit, InvocationContext } from '@azure/functions';
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
const category = request.params.category;
const id = request.params.id;
return { body: `Category: ${category}, ID: ${id}` };
}
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
route: 'products/{category:alpha}/{id:int?}',
handler: httpTrigger1,
});
```


As an example, the following JavaScript code defines a `route`

property for an HTTP trigger with two parameters, `category`

and `id`

. The example reads the parameters from the request and returns their values in the response.

```
const { app } = require('@azure/functions');
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
route: 'products/{category:alpha}/{id:int?}',
handler: async (request, context) => {
const category = request.params.category;
const id = request.params.id;
return { body: `Category: ${category}, ID: ${id}` };
},
});
```


As an example, the following code defines a `route`

property for an HTTP trigger with two parameters, `category`

and `id`

:

Route parameters declared in the *function.json* file are accessible as a property of the `$Request.Params`

object.

```
$Category = $Request.Params.category
$Id = $Request.Params.id
$Message = "Category:" + $Category + ", ID: " + $Id
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $Message
})
```


The function execution context is exposed via a parameter declared as `func.HttpRequest`

. This instance allows a function to access data route parameters, query string values and methods that allow you to return HTTP responses.

Once defined, the route parameters are available to the function by calling the `route_params`

method.

```
import logging
import azure.functions as func
def main(req: func.HttpRequest) -> func.HttpResponse:
category = req.route_params.get('category')
id = req.route_params.get('id')
message = f"Category: {category}, ID: {id}"
return func.HttpResponse(message)
```


Using this configuration, the function is now addressable with the following route instead of the original route.

```
https://<APP_NAME>.azurewebsites.net/api/products/electronics/357
```


This configuration allows the function code to support two parameters in the address, *category* and *ID*. For more information on how route parameters are tokenized in a URL, see [Routing in ASP.NET Core](/en-us/aspnet/core/fundamentals/routing#route-constraint-reference).

By default, all function routes are prefixed with `api`

. You can also customize or remove the prefix using the `extensions.http.routePrefix`

property in your [host.json](functions-host-json) file. The following example removes the `api`

route prefix by using an empty string for the prefix in the *host.json* file.

```
{
"extensions": {
"http": {
"routePrefix": ""
}
}
}
```


### Using route parameters

Route parameters that defined a function's `route`

pattern are available to each binding. For example, if you have a route defined as `"route": "products/{id}"`

then a table storage binding can use the value of the `{id}`

parameter in the binding configuration.

The following configuration shows how the `{id}`

parameter is passed to the binding's `rowKey`

.

```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const tableInput = input.table({
connection: 'MyStorageConnectionAppSetting',
partitionKey: 'products',
tableName: 'products',
rowKey: '{id}',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
return { jsonBody: context.extraInputs.get(tableInput) };
}
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
route: 'products/{id}',
extraInputs: [tableInput],
handler: httpTrigger1,
});
```


```
const { app, input } = require('@azure/functions');
const tableInput = input.table({
connection: 'MyStorageConnectionAppSetting',
partitionKey: 'products',
tableName: 'products',
rowKey: '{id}',
});
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
route: 'products/{id}',
extraInputs: [tableInput],
handler: async (request, context) => {
return { jsonBody: context.extraInputs.get(tableInput) };
},
});
```


```
{
"type": "table",
"direction": "in",
"name": "product",
"partitionKey": "products",
"tableName": "products",
"rowKey": "{id}"
}
```


When you use route parameters, an `invoke_URL_template`

is automatically created for your function. Your clients can use the URL template to understand the parameters they need to pass in the URL when calling your function using its URL. Navigate to one of your HTTP-triggered functions in the [Azure portal](https://portal.azure.com) and select **Get function URL**.

You can programmatically access the `invoke_URL_template`

by using the Azure Resource Manager APIs for [List Functions](/en-us/rest/api/appservice/webapps/listfunctions) or [Get Function](/en-us/rest/api/appservice/webapps/getfunction).

### HTTP streams

You can now stream requests to and responses from your HTTP endpoint in Node.js v4 function apps. For more information, see [HTTP streams](functions-reference-node?pivots=nodejs-model-v4#http-streams).

### HTTP streams

HTTP streams support in Python lets you accept and return data from your HTTP endpoints using FastAPI request and response APIs enabled in your functions. These APIs enable the host to process data in HTTP messages as chunks instead of having to read an entire message into memory.

### Prerequisites

[Azure Functions runtime](functions-versions?pivots=programming-language-python)version 4.34.1, or a later version.[Python](https://www.python.org/downloads/)version 3.8, or a later[supported version](functions-reference-python?tabs=get-started&pivots=python-mode-decorators#supported-python-versions).

Important

HTTP streams is only supported for the Python v2 programming model.

### Enable HTTP streams

HTTP streams are disabled by default. You need to enable this feature in your application settings and also update your code to use the FastAPI package. Note that when enabling HTTP streams, the function app will default to using HTTP streaming, and the original HTTP functionality will not work.

Add the

`azurefunctions-extensions-http-fastapi`

extension package to the`requirements.txt`

file in the project, which should include at least these packages:`azure-functions azurefunctions-extensions-http-fastapi`

Add this code to the

`function_app.py`

file in the project, which imports the FastAPI extension:`from azurefunctions.extensions.http.fastapi import Request, StreamingResponse`

When you deploy to Azure, add the following

[application setting](functions-how-to-use-azure-function-app-settings#settings)in your function app:`"PYTHON_ENABLE_INIT_INDEXING": "1"`

When running locally, you also need to add these same settings to the

`local.settings.json`

project file.

### HTTP streams examples

After you enable the HTTP streaming feature, you can create functions that stream data over HTTP.

This example is an HTTP triggered function that receives and processes streaming data from a client in real time. It demonstrates streaming upload capabilities that can be helpful for scenarios like processing continuous data streams and handling event data from IoT devices.

```
import azure.functions as func
from azurefunctions.extensions.http.fastapi import JSONResponse, Request
app = func.FunctionApp(http_auth_level=func.AuthLevel.FUNCTION)
@app.route(route="streaming_upload", methods=[func.HttpMethod.POST])
async def streaming_upload(req: Request) -> JSONResponse:
"""Handle streaming upload requests."""
# Process each chunk of data as it arrives
async for chunk in req.stream():
process_data_chunk(chunk)
# Once all data is received, return a JSON response indicating successful processing
return JSONResponse({"status": "Data uploaded and processed successfully"})
def process_data_chunk(chunk: bytes):
"""Process each data chunk."""
# Add custom processing logic here
pass
```


### Calling HTTP streams

You must use an HTTP client library to make streaming calls to a function's FastAPI endpoints. The client tool or browser you're using might not natively support streaming or could only return the first chunk of data.

You can use a client script like this to send streaming data to an HTTP endpoint:

```
import httpx # Be sure to add 'httpx' to 'requirements.txt'
import asyncio
async def stream_generator(file_path):
chunk_size = 2 * 1024 # Define your own chunk size
with open(file_path, 'rb') as file:
while chunk := file.read(chunk_size):
yield chunk
print(f"Sent chunk: {len(chunk)} bytes")
async def stream_to_server(url, file_path):
timeout = httpx.Timeout(60.0, connect=60.0)
async with httpx.AsyncClient(timeout=timeout) as client:
response = await client.post(url, content=stream_generator(file_path))
return response
async def stream_response(response):
if response.status_code == 200:
async for chunk in response.aiter_raw():
print(f"Received chunk: {len(chunk)} bytes")
else:
print(f"Error: {response}")
async def main():
print('helloworld')
# Customize your streaming endpoint served from core tool in variable 'url' if different.
url = 'http://localhost:7071/api/streaming_upload'
file_path = r'<file path>'
response = await stream_to_server(url, file_path)
print(response)
if __name__ == "__main__":
asyncio.run(main())
```


Important

If you are using HTTP streams, all HTTP functions in the app need to use streaming. Combining streaming and non-streaming HTTP functions within the same app is not supported.

### Working with client identities

If your function app is using [App Service Authentication / Authorization](../app-service/overview-authentication-authorization), you can view information about authenticated clients from your code. This information is available as [request headers injected by the platform](../app-service/configure-authentication-user-identities#access-user-claims-in-app-code).

You can also read this information from binding data.

Note

Access to authenticated client information is currently only available for .NET languages. It also isn't supported in version 1.x of the Functions runtime.

Information regarding authenticated clients is available as a [ClaimsPrincipal](/en-us/dotnet/api/system.security.claims.claimsprincipal), which is available as part of the request context as shown in the following example:

The authenticated user is available via [HTTP Headers](../app-service/configure-authentication-user-identities#access-user-claims-in-app-code).

The authenticated user is available via [HTTP Headers](../app-service/configure-authentication-user-identities#access-user-claims-in-app-code).

### Authorization level

The authorization level is a string value that indicates the kind of [authorization key](#authorization-keys) that's required to access the function endpoint. For an HTTP triggered function, the authorization level can be one of the following values:

| Level value | Description |
|---|---|
anonymous |
No access key is required. |
function |
A function-specific key is required to access the endpoint. |
admin |
The master key is required to access the endpoint. |

When a level isn't explicitly set, authorization defaults to the `function`

level.

When a level isn't explicitly set, the default authorization depends on the version of the Node.js model:

### Function access keys

Functions lets you use access keys to make it harder to access your function endpoints. Unless the authorization level on an HTTP triggered function is set to `anonymous`

, requests must include an access key in the request. For more information, see [Work with access keys in Azure Functions](function-keys-how-to).

### Access key authorization

Most HTTP trigger templates require an access key in the request. So your HTTP request normally looks like the following URL:

```
https://<APP_NAME>.azurewebsites.net/api/<FUNCTION_NAME>?code=<API_KEY>
```


Function apps that run in containers use the domain of the container host. For an example HTTP endpoint hosted in Azure Container Apps, see the example in [this Container Apps hosting article](functions-deploy-container-apps#verify-your-functions-on-azure).

The key can be included in a query string variable named `code`

, as mentioned earlier. It can also be included in an `x-functions-key`

HTTP header. The value of the key can be any function key defined for the function, or any host key.

You can allow anonymous requests, which don't require keys. You can also require that the master key is used. You change the default authorization level by using the `authLevel`

property in the binding JSON.

Note

When running functions locally, authorization is disabled regardless of the specified authorization level setting. After publishing to Azure, the `authLevel`

setting in your trigger is enforced. Keys are still required when running [locally in a container](functions-create-container-registry#build-the-container-image-and-verify-locally).

### Webhooks

Note

Webhook mode is only available for version 1.x of the Functions runtime. This change was made to improve the performance of HTTP triggers in version 2.x and higher.

In version 1.x, webhook templates provide another validation for webhook payloads. In version 2.x and higher, the base HTTP trigger still works and is the recommended approach for webhooks.

#### WebHook type

The `webHookType`

binding property indicates the type if webhook supported by the function, which also dictates the supported payload. The webhook type can be one of the following values:

| Type value | Description |
|---|---|
`genericJson` |
A general-purpose webhook endpoint without logic for a specific provider. This setting restricts requests to only those using HTTP POST and with the `application/json` content type. |
`github` |
The function responds to
`authLevel` property with GitHub webhooks. |

`slack`

[Slack webhooks](https://api.slack.com/outgoing-webhooks). Don't use the`authLevel`

property with Slack webhooks.When setting the `webHookType`

property, don't also set the `methods`

property on the binding.

#### GitHub webhooks

To respond to GitHub webhooks, first create your function with an HTTP Trigger, and set the **webHookType** property to `github`

. Then copy its URL and API key into the **Add webhook** page of your GitHub repository.

#### Slack webhooks

The Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with the token from Slack. See [Authorization keys](#authorization-keys).

### Webhooks and keys

Webhook authorization is handled by the webhook receiver component, part of the HTTP trigger, and the mechanism varies based on the webhook type. Each mechanism does rely on a key. By default, the function key named "default" is used. To use a different key, configure the webhook provider to send the key name with the request in one of the following ways:

**Query string**: The provider passes the key name in the`clientid`

query string parameter, such as`https://<APP_NAME>.azurewebsites.net/api/<FUNCTION_NAME>?clientid=<KEY_NAME>`

.**Request header**: The provider passes the key name in the`x-functions-clientid`

header.

## Invoke HTTP triggers

You can invoke your HTTP-triggered functions using an HTTP client. The examples in this section use [ curl](https://github.com/curl/curl), but you can use any HTTP client tool that keeps your data secure. For more information, see

[HTTP test tools](functions-develop-local#http-test-tools).

The request you need to make might be different between a local version of your code and when hosted in Azure. By default, when you run your project using the Azure Functions Core Tools, access key authorization requirements are removed. However, any requirements you've configured will still be enforced when hosted.

### Invoke locally

The [Azure Functions Core Tools](functions-develop-local) registers a `localhost`

endpoint for your function app, which you can use to invoke your functions. During application startup, the specific port being used is displayed in the console. The output also lists the available functions, and for each HTTP-triggered function, the output also includes the function's route template.

Use this information to construct the URL to provide to your API client. You also need to specify any headers, parameters, and request body information your function requires. The following example sends an HTTP POST request with a JSON body:

```
curl --request POST http://localhost:7071/api/Function1 --header "Content-Type: application/json" --data '{"message":"test data"}'
```


### Invoke in Azure

When invoking an HTTP-triggered function hosted in Azure, you need to consider your networking configuration. The HTTP client must have network access to the app, so if you have [inbound networking restrictions](functions-networking-options#inbound-networking-features) enabled, the client might need to be within a virtual network or specific IP ranges. Your domain configuration determines the base URL you need to use for the request.

Note

Newly created function apps can generate a unique default host name that uses the naming convention `<app-name>-<random-hash>.<region>.azurewebsites.net`

. An example is `myapp-ds27dh7271aah175.westus-01.azurewebsites.net`

. Existing app names remain unchanged.

For more information, see the [blog post about creating an app with a unique default host name](https://techcommunity.microsoft.com/blog/appsonazureblog/secure-unique-default-hostnames-ga-on-app-service-web-apps-and-public-preview-on/4303571).

Unless you selected the anonymous [authorization level](#http-auth) in your trigger definition, your request may also need to [include an access key](function-keys-how-to#use-access-keys).

The following example sends an HTTP POST request with a function body, including the access key in the query string:

```
curl --request POST "https://<your-function-app-base-url>/api/Function1?code=<your-function-key>" --header "Content-Type: application/json" --data '{"message":"test data"}'
```


## Content types

Passing binary and form data to a non-C# function requires that you use the appropriate content-type header. Supported content types include `octet-stream`

for binary data and [multipart types](https://www.iana.org/assignments/media-types/media-types.xhtml#multipart).

#### Known issues

In non-C# functions, requests sent with the content-type `image/jpeg`

results in a `string`

value passed to the function. In cases like these, you can manually convert the `string`

value to a byte array to access the raw binary data.

### Limits

The HTTP request size and URL lengths are both limited based on [settings defined in the host](https://github.com/Azure/azure-functions-host/blob/dev/src/WebJobs.Script.WebHost/web.config#L19). For more information, see [Service limits](functions-scale#service-limits).

If a function that uses the HTTP trigger doesn't complete within 230 seconds, the [Azure Load Balancer](../app-service/faq-availability-performance-application-issues#why-does-my-request-time-out-after-230-seconds-) will time out and return an HTTP 502 error. The function will continue running but will be unable to return an HTTP response. For long-running functions, we recommend that you follow async patterns and return a location where you can ping the status of the request. For information about how long a function can run, see [Scale and hosting - Consumption plan](functions-scale#timeout).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-queue-output -->

# Azure Queue storage output bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions can create new Azure Queue storage messages by setting up an output binding.

For information on setup and configuration details, see the [overview](functions-bindings-storage-queue).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

## Example

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

```
[Function(nameof(QueueInputOutputFunction))]
[QueueOutput("output-queue")]
public string[] QueueInputOutputFunction([QueueTrigger("input-queue")] Album myQueueItem, FunctionContext context)
{
// Use a string array to return more than one message.
string[] messages = {
$"Album name = {myQueueItem.Name}",
$"Album songs = {myQueueItem.Songs}"};
_logger.LogInformation("{msg1},{msg2}", messages[0], messages[1]);
// Queue Output messages
return messages;
}
```


For an end-to-end example of how to configure an output binding to Queue storage, see one of these articles:

The following example shows a Java function that creates a queue message for when triggered by an HTTP request.

```
@FunctionName("httpToQueue")
@QueueOutput(name = "item", queueName = "myqueue-items", connection = "MyStorageConnectionAppSetting")
public String pushToQueue(
@HttpTrigger(name = "request", methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS)
final String message,
@HttpOutput(name = "response") final OutputBinding<String> result) {
result.setValue(message + " has been added.");
return message;
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@QueueOutput`

annotation on parameters whose value would be written to Queue storage. The parameter type should be `OutputBinding<T>`

, where `T`

is any native Java type of a POJO.

For an end-to-end example of how to configure an output binding to Queue storage, see one of these articles:

The following example shows an HTTP triggered [TypeScript function](functions-reference-node?tabs=typescript) that creates a queue item for each HTTP request received.

```
import { app, HttpRequest, HttpResponseInit, InvocationContext, output } from '@azure/functions';
const queueOutput = output.storageQueue({
queueName: 'outqueue',
connection: 'MyStorageConnectionAppSetting',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
const body = await request.text();
context.extraOutputs.set(queueOutput, body);
return { body: 'Created queue item.' };
}
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraOutputs: [queueOutput],
handler: httpTrigger1,
});
```


To output multiple messages, return an array instead of a single object. For example:

```
context.extraOutputs.set(queueOutput, ['message 1', 'message 2']);
```


The following example shows an HTTP triggered [JavaScript function](functions-reference-node) that creates a queue item for each HTTP request received.

```
const { app, output } = require('@azure/functions');
const queueOutput = output.storageQueue({
queueName: 'outqueue',
connection: 'MyStorageConnectionAppSetting',
});
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraOutputs: [queueOutput],
handler: async (request, context) => {
const body = await request.text();
context.extraOutputs.set(queueOutput, body);
return { body: 'Created queue item.' };
},
});
```


To output multiple messages, return an array instead of a single object. For example:

```
context.extraOutputs.set(queueOutput, ['message 1', 'message 2']);
```


For an end-to-end example of how to configure an output binding to Queue storage, see one of these articles:

The following code examples demonstrate how to output a queue message from an HTTP-triggered function. The configuration section with the `type`

of `queue`

defines the output binding.

```
{
"bindings": [
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "Request",
"methods": [
"get",
"post"
]
},
{
"type": "http",
"direction": "out",
"name": "Response"
},
{
"type": "queue",
"direction": "out",
"name": "Msg",
"queueName": "outqueue",
"connection": "MyStorageConnectionAppSetting"
}
]
}
```


Using this binding configuration, a PowerShell function can create a queue message using `Push-OutputBinding`

. In this example, a message is created from a query string or body parameter.

```
using namespace System.Net
# Input bindings are passed in via param block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell HTTP trigger function processed a request."
# Interact with query parameters or the body of the request.
$message = $Request.Query.Message
Push-OutputBinding -Name Msg -Value $message
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = 200
Body = "OK"
})
```


To send multiple messages at once, define a message array and use `Push-OutputBinding`

to send messages to the Queue output binding.

```
using namespace System.Net
# Input bindings are passed in via param block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell HTTP trigger function processed a request."
# Interact with query parameters or the body of the request.
$message = @("message1", "message2")
Push-OutputBinding -Name Msg -Value $message
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = 200
Body = "OK"
})
```


For an end-to-end example of how to configure an output binding to Queue storage, see one of these articles:

The following example demonstrates how to output single and multiple values to storage queues. The configuration needed for *function.json* is the same either way. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="QueueOutput1")
@app.route(route="message")
@app.queue_output(arg_name="msg",
queue_name="<QUEUE_NAME>",
connection="<CONNECTION_SETTING>")
def main(req: func.HttpRequest, msg: func.Out[str]) -> func.HttpResponse:
input_msg = req.params.get('name')
logging.info(input_msg)
msg.set(input_msg)
logging.info(f'name: {name}')
return 'OK'
```


For an end-to-end example of how to configure an output binding to Queue storage, see one of these articles:

## Attributes

The attribute that defines an output binding in C# libraries depends on the mode in which the C# class library runs.

When running in an isolated worker process, you use the [QueueOutputAttribute](https://github.com/Azure/azure-functions-dotnet-worker/blob/main/extensions/Worker.Extensions.Storage.Queues/src/QueueOutputAttribute.cs), which takes the name of the queue, as shown in the following example:

```
[Function(nameof(QueueInputOutputFunction))]
[QueueOutput("output-queue")]
public string[] QueueInputOutputFunction([QueueTrigger("input-queue")] Album myQueueItem, FunctionContext context)
```


Only returned variables are supported when running in an isolated worker process. Output parameters can't be used.

## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, the following properties on the `queue_output`

:

| Property | Description |
|---|---|
`arg_name` |
The name of the variable that represents the queue in function code. |
`queue_name` |
The name of the queue. |
`connection` |
The name of an app setting or setting collection that specifies how to connect to Azure Queues. See
|

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

The [QueueOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.queueoutput) annotation allows you to write a message as the output of a function. The following example shows an HTTP-triggered function that creates a queue message.

```
package com.function;
import java.util.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.*;
public class HttpTriggerQueueOutput {
@FunctionName("HttpTriggerQueueOutput")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.FUNCTION) HttpRequestMessage<Optional<String>> request,
@QueueOutput(name = "message", queueName = "messages", connection = "MyStorageConnectionAppSetting") OutputBinding<String> message,
final ExecutionContext context) {
message.setValue(request.getQueryParameters().get("name"));
return request.createResponseBuilder(HttpStatus.OK).body("Done").build();
}
}
```


| Property | Description |
|---|---|
`name` |
Declares the parameter name in the function signature. When the function is triggered, this parameter's value has the contents of the queue message. |
`queueName` |
Declares the queue name in the storage account. |
`connection` |
Points to the storage account connection string. |

The parameter associated with the [QueueOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.queueoutput) annotation is typed as an [OutputBinding<T>](/en-us/java/api/com.microsoft.azure.functions.outputbinding) instance.

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `output.storageQueue()`

method.

| Property | Description |
|---|---|
queueName |
The name of the queue. |
connection |
The name of an app setting or setting collection that specifies how to connect to Azure Queues. See
|

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

The following table explains the binding configuration properties that you set in the *function.json* file.

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

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

See the [Example section](#example) for complete examples.

## Usage

The usage of the Queue output binding depends on the extension package version and the C# modality used in your function app, which can be one of the following:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see usage details for the mode and version.

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

There are two options for writing to a queue from a function by using the [QueueOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.queueoutput) annotation:

**Return value**: By applying the annotation to the function itself, the return value of the function is written to the queue.**Imperative**: To explicitly set the message value, apply the annotation to a specific parameter of the type, where`OutputBinding<T>`

`T`

is a POJO or any native Java type. With this configuration, passing a value to the`setValue`

method writes the value to the queue.

Output to the queue message is available via `Push-OutputBinding`

where you pass arguments that match the name designated by binding's `name`

parameter in the *function.json* file.

There are two options for writing from your function to the configured queue:

**Return value**: Set the`name`

property in*function.json*to`$return`

. With this configuration, the function's return value is persisted as a Queue storage message.**Imperative**: Pass a value to the[set](/en-us/python/api/azure-functions/azure.functions.out#set-val--t-----none)method of the parameter declared as an[Out](/en-us/python/api/azure-functions/azure.functions.out)type. The value passed to`set`

is persisted as a Queue storage message.

The output function parameter must be defined as `func.Out[func.QueueMessage]`

, `func.Out[str]`

, or `func.Out[bytes]`

. Refer to the [output example](#example) for details.

## Connections

The `connection`

property is a reference to environment configuration that specifies how the app should connect to Azure Queues. It may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections).

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

To obtain a connection string, follow the steps shown at [Manage storage account access keys](../storage/common/storage-account-keys-manage).

This connection string should be stored in an application setting with a name matching the value specified by the `connection`

property of the binding configuration.

If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name here. For example, if you set `connection`

to "MyStorage", the Functions runtime looks for an app setting that is named "AzureWebJobsMyStorage." If you leave `connection`

empty, the Functions runtime uses the default Storage connection string in the app setting that is named `AzureWebJobsStorage`

.

### Identity-based connections

If you're using [version 5.x or higher of the extension](functions-bindings-storage-queue#storage-extension-5x-and-higher) ([bundle 3.x or higher](functions-bindings-storage-queue?tabs=extensionv3#install-bundle) for non-.NET language stacks), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). To use an identity, you define settings under a common prefix that maps to the `connection`

property in the trigger and binding configuration.

If you're setting `connection`

to "AzureWebJobsStorage", see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity). For all other connections, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Queue Service URI | `<CONNECTION_NAME_PREFIX>__queueServiceUri` 1 |
The data plane URI of the queue service to which you're connecting, using the HTTPS scheme. | https://<storage_account_name>.queue.core.windows.net |

1 `<CONNECTION_NAME_PREFIX>__serviceUri`

can be used as an alias. If both forms are provided, the `queueServiceUri`

form is used. The `serviceUri`

form can't be used when the overall connection configuration is to be used across blobs, queues, and/or tables.

Other properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

You will need to create a role assignment that provides access to your queue at runtime. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) are not sufficient. The following table shows built-in roles that are recommended when using the Queue Storage extension in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles |
|---|---|
| Trigger |
|

[Storage Queue Data Contributor](../role-based-access-control/built-in-roles#storage-queue-data-contributor),[Storage Queue Data Message Sender](../role-based-access-control/built-in-roles#storage-queue-data-message-sender)## Exceptions and return codes

| Binding | Reference |
|---|---|
| Queue |
|

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-how-to-custom-container -->

# Work with containers and Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article demonstrates the support that Azure Functions provides for containerized function apps that run in an Azure Container Apps environment. For more information, see [Azure Container Apps hosting of Azure Functions](functions-container-apps-hosting).

Important

A new hosting method for running Azure Functions directly in Azure Container Apps is now available. See [Native Azure Functions Support in Azure Container Apps](https://techcommunity.microsoft.com/blog/appsonazureblog/announcing-native-azure-functions-support-in-azure-container-apps/4414039). This integration allows you to use the full features and capabilities of Azure Container Apps. You also benefit from the functions programming model and simplicity of autoscaling provided by Azure Functions.

We recommend this approach for most new workloads. For more information, see [Azure Functions on Azure Container Apps](../container-apps/functions-overview).

This article demonstrates the support that Azure Functions provides for function apps that run in Linux containers.

Choose the hosting environment for your containerized function app at the top of this article.

If you want to jump right in, the following article shows you how to create your first function in a Linux container and deploy the image from a container registry to a supported Azure hosting service:


[Create your first containerized Azure Functions on Azure Container Apps]

To learn more about deployments to Azure Container Apps, see [Azure Container Apps hosting of Azure Functions](functions-container-apps-hosting).

Important

This article currently shows how to connect to the default storage account by using a connection string. For the best security, instead create a managed identity-based connection to Azure Storage using Microsoft Entra authentication. For more information, see [Connections](functions-reference#connections).

## Create containerized function apps

Functions makes it easy to deploy and run your function apps as Linux containers, which you create and maintain. Functions maintains a set of [language-specific base images](https://mcr.microsoft.com/catalog?search=functions) that you can use when creating containerized function apps.

Important

When you create your own containers, you're required to keep the base image of your container updated to the latest supported base image. Supported base images for Azure Functions are language-specific. See the [Azure Functions base image repos](https://mcr.microsoft.com/catalog?search=functions).

The Functions team is committed to publishing monthly updates for these base images. Regular updates include the latest minor version updates and security fixes for both the Functions runtime and languages. You should regularly update your container from the latest base image and redeploy the updated version of your container. For more information, see [Maintaining custom containers](container-concepts#maintaining-custom-containers).

For a complete example of how to create the local containerized function app from the command line and publish the image to a container registry, see [Create a function app in a local Linux container](functions-create-container-registry).

## Generate the Dockerfile

Functions tooling provides a Docker option that generates a Dockerfile with your functions code project. You can use this file with Docker to create your functions in a container that derives from the correct base image, which includes language and version.

The way you create a Dockerfile depends on how you create your project.

When you create a Functions project using

[Azure Functions Core Tools](functions-run-local), include the`--docker`

option when you run thecommand, as in the following example:`func init`

`func init --docker`

You can also add a Dockerfile to an existing project by using the

`--docker-only`

option when you run thecommand in an existing project folder, as in the following example:`func init`

`func init --docker-only`


For a complete example, see [Create a function app in a local Linux container](functions-create-container-registry#create-and-test-the-local-functions-project).

## Create your function app in a container

With a Functions-generated Dockerfile in your code project, you can use Docker to create the containerized function app on your local computer. The following `docker build`

command creates an image of your containerized functions from the project in the local directory:

```
docker build --tag <DOCKER_ID>/<IMAGE_NAME>:v1.0.0 .
```


For an example of how to create the container, see [Build the container image and verify locally](functions-create-container-registry#build-the-container-image-and-verify-locally).

## Update an image in the registry

When you make changes to your functions code project or need to update to the latest base image, rebuild the container locally. Republish the updated image to your chosen container registry. The following command rebuilds the image from the root folder with an updated version number and pushes it to your registry:

```
az acr build --registry <REGISTRY_NAME> --image <LOGIN_SERVER>/azurefunctionsimage:v1.0.1 .
```


Replace `<REGISTRY_NAME>`

with your Container Registry instance and `<LOGIN_SERVER>`

with the sign-in server name.

Update an existing deployment to use the new image. You can update the function app to use the new image either by using the Azure CLI or in the [Azure portal](https://portal.azure.com):

```
az functionapp config container set --image <IMAGE_NAME> --registry-password <SECURE_PASSWORD>--registry-username <USER_NAME> --name <APP_NAME> --resource-group <RESOURCE_GROUP>
```


In this example, `<IMAGE_NAME>`

is the full name of the new image with version. Private registries require you to supply a username and password. Store these credentials securely.

You should also consider [enabling continuous deployment](#enable-continuous-deployment-to-azure).

## Create a containerized function app using the Azure portal

When you create a function app in the [Azure portal](https://portal.azure.com), you can choose to deploy the function app from an image in a container registry. To learn how to create a containerized function app in a container registry, see [Create your function app in a container](#create-your-function-app-in-a-container).

The following steps create and deploy an existing containerized function app from a container registry.

From the Azure portal menu or the

**Home**page, select**Create a resource**.In the

**New**page, select**Compute**>**Function App**.Under

**Select a hosting option**, choose**Functions Premium**>**Select**.This action creates a function app hosted by Azure Functions in the

[Premium plan](functions-premium-plan), which supports dynamic scaling. You can also choose to run in an**App Service plan**, but in this kind of dedicated plan you must manage the[scaling of your function app](functions-scale).On the

**Basics**page, use the function app settings as specified in the following table:Setting Suggested value Description **Subscription**Your subscription The subscription in which you create your function app. [Resource Group](../azure-resource-manager/management/overview)*myResourceGroup*Name for the new resource group in which you create your function app. You should create a resource group because there are [known limitations when creating new function apps in an existing resource group](functions-scale#limitations-for-creating-new-function-apps-in-an-existing-resource-group).**Function App name**An app name Name that identifies your new function app. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

.**Secure unique default hostname**Enabled Enable this feature so you don't have to worry about domain name collisions, regardless of your app name. **Do you want to deploy code or container image?**Container image Deploy a containerized function app from a registry. To create a function app in registry, see [Create a function app in a local Linux container](functions-create-container-registry).**Region**Preferred region Select a [region](https://azure.microsoft.com/regions/)that's near you or near other services that your functions can access.**Linux plan**New plan (default) Creates a new Premium plan to host your app. You can also choose an existing premium plan. **Pricing plan**Elastic Premium EP1 `EP1`

is the most affordable plan. You can choose a larger plan if you need to.**Zone Redundancy**Disabled You don't need this feature in a nonproduction app. Accept the default options of creating a new storage account on the

**Storage**tab and a new Application Insight instance on the**Monitoring**tab. You can also choose to use an existing storage account or Application Insights instance.Select

**Review + create**to review the app configuration selections.On the

**Review + create**page, review your settings, and then select**Create**to provision the function app using a default base image.After your function app resource is created, select

**Go to resource**. In the function app page, select**Deployment Center**.In the

**Deployment Center**, you can connect your container registry as the source of the image. You can also enable GitHub Actions or Azure Pipelines for more robust continuous deployment of updates to your container in the registry.

## Create a containerized function app using the Azure portal

When you create a Container Apps-hosted function app in the [Azure portal](https://portal.azure.com), you can choose to deploy your function app from an image in a container registry. To learn how to create a containerized function app in a container registry, see [Create your function app in a container](#create-your-function-app-in-a-container).

The following steps create and deploy an existing containerized function app from a container registry.

From the Azure portal menu or the

**Home**page, select**Create a resource**.In the

**New**page, select**Compute**>**Function App**.Under

**Select a hosting option**, choose**Container Apps environment**>**Select**.On the

**Basics**page, use the function app settings as specified in the following table:Setting Suggested value Description **Subscription**Your subscription The subscription in which you create your function app. [Resource Group](../azure-resource-manager/management/overview)*myResourceGroup*Name for the new resource group in which you create your function app. You should create a resource group because there are [known limitations when creating new function apps in an existing resource group](functions-scale#limitations-for-creating-new-function-apps-in-an-existing-resource-group).**Function App name**Unique name *Name that identifies your new function app. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

.**Region**Preferred region Select a [region](https://azure.microsoft.com/regions/)that's near you or near other services that your functions can access.*App name must be unique within the Azure Container Apps environment.Still on the

**Basics**page, accept the suggested new environment for**Azure Container Apps environment**. To minimize costs, the new default environment is created in the**Consumption + Dedicated**with the default workload profile and without zone redundancy. For more information, see[Azure Container Apps hosting of Azure Functions](functions-container-apps-hosting).You can also choose to use an existing Container Apps environment. To create a custom environment, instead select

**Create new**. In the**Create Container Apps Environment**page, you can add nondefault workload profiles or enable zone redundancy. To learn about environments, see[Azure Container Apps environments](../container-apps/environment).Select the

**Deployment**tab and unselect**Use quickstart image**. Otherwise, the function app is deployed from the base image for your function app language.Choose your

**Image type**, public or private. Choose**Private**if you're using Azure Container Registry or some other private registry. Supply the**Image**name, including the registry prefix. If you're using a private registry, provide the image registry authentication credentials. The**Public**setting only supports images stored publicly in Docker Hub.Under

**Container resource allocation**, select your desired number of CPU cores and available memory. If your environment has other workload profiles added, you can select a nondefault**Workload profile**. Choices  affect the cost of hosting your app. See the[Container Apps pricing page](https://azure.microsoft.com/pricing/details/container-apps/)to estimate your potential costs.Select

**Review + create**to review the app configuration selections.On the

**Review + create**page, review your settings, and then select**Create**to provision the function app and deploy your container image from the registry.

## Work with images in Azure Functions

When your function app container is deployed from a registry, Functions maintains information about the source image.

Use the following commands to get data about the image or change the deployment image used:

: returns information about the image used for deployment.`az functionapp config container show`

: change registry settings or update the image used for deployment, as shown in the previous example.`az functionapp config container set`


## Use Container Apps workload profiles

Workload profiles are feature of Container Apps that let you better control your deployment resources. Azure Functions on Azure Container Apps also supports workload profiles. For more information, see [Workload profiles in Azure Container Apps](../container-apps/workload-profiles-overview).

You can also set the amount of CPU and memory resources allocated to your app.

You can create and manage both workload profiles and resource allocations using the Azure CLI or in the Azure portal.

You enable workload profiles when you create your container app environment. For an example, see [Create a container app in a profile](../container-apps/workload-profiles-manage-cli#create-a-container-app-in-a-profile).

You can add, edit, and delete profiles in your environment. For an example, see [Add profiles](../container-apps/workload-profiles-manage-cli#add-profiles).

When you create a containerized function app in an environment that has workload profiles enabled, you should also specify the profile in which to run. Specify the profile by using the `--workload-profile-name`

parameter of the [ az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create) command, like in this example:

```
az functionapp create --name <APP_NAME> --storage-account <STORAGE_NAME> --environment MyContainerappEnvironment --resource-group AzureFunctionsContainers-rg --functions-version 4 --runtime <LANGUAGE_STACK> --image <IMAGE_URI> --workload-profile-name <PROFILE_NAME> --cpu <CPU_COUNT> --memory <MEMORY_SIZE>
```


In the [az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create) command, the `--environment`

parameter specifies the Container Apps environment and the `--image`

parameter specifies the image to use for the function app. In this example, replace `<STORAGE_NAME>`

with the name you used in the previous section for the storage account. Also, replace `<APP_NAME>`

with a name appropriate to you that is unique in the environment.

To set the resources allocated to your app, replace `<CPU_COUNT>`

with your desired number of virtual CPUs, with a minimum of 0.5 up to the maximum allowed by the profile. For `<MEMORY_SIZE>`

, choose a dedicated memory amount from 1 GB up to the maximum allowed by the profile.

You can use the [az functionapp container set](/en-us/cli/azure/functionapp/config/container#az-functionapp-config-container-set) command to manage the allocated resources and the workload profile used by your app.

```
az functionapp container set --name <APP_NAME> --resource-group AzureFunctionsContainers-rg --workload-profile-name <PROFILE_NAME> --cpu <CPU_COUNT> --memory <MEMORY_SIZE>
```


## Use application settings

Azure Functions lets you work with application settings for containerized function apps in the standard way. For more information, see [Use application settings](functions-how-to-use-azure-function-app-settings#settings).

Tip

By default, a containerized function app monitors port 80 for incoming requests. If your app must use a different port, use the [ WEBSITES_PORT application setting](../app-service/reference-app-settings#custom-containers) to change this port.

## Enable continuous deployment to Azure

When you host your containerized function app on Azure Container Apps, there are two ways to set up continuous deployment from a source code repository:

You aren't currently able to continuously deploy containers based on image changes in a container registry. You must instead use these source-code based continuous deployment pipelines.

## Enable continuous deployment to Azure

Important

Webhook-based deployment isn't currently supported when running your container in an [Elastic Premium plan](functions-premium-plan). If you need to use the continuous deployment method described in this section, instead deploy your container in an [App Service plan](dedicated-plan). When running in an Elastic Premium plan, you need to manually restart your app whenever you make updates to your container in the repository.

You can also configure continuous deployment from a source code repository using either [Azure Pipelines](functions-how-to-azure-devops#deploy-a-container) or [GitHub Actions](https://github.com/Azure/azure-functions-on-container-apps/blob/main/samples/GitHubActions/Func_on_ACA_GitHubAction_deployment.yml).

You can enable Azure Functions to automatically update your deployment of an image whenever you update the image in the registry.

Use the following command to enable continuous deployment and to get the webhook URL:

`az functionapp deployment container config --enable-cd --query CI_CD_URL --output tsv --name <APP_NAME> --resource-group AzureFunctionsContainers-rg`

The

[az functionapp deployment container config](/en-us/cli/azure/functionapp/deployment/container#az-functionapp-deployment-container-config)command enables continuous deployment and returns the deployment webhook URL. You can retrieve this URL at any time by using the[az functionapp deployment container show-cd-url](/en-us/cli/azure/functionapp/deployment/container#az-functionapp-deployment-container-show-cd-url)command.As before, replace

`<APP_NAME>`

with your function app name.Copy the deployment webhook URL to the clipboard.

Open

[Docker Hub](https://hub.docker.com/), sign in, and select**Repositories**on the navigation bar. Locate and select the image, select the**Webhooks**tab, specify a**Webhook name**, paste your URL in**Webhook URL**, and then select**Create**.With the webhook set, Azure Functions redeploys your image whenever you update it in Docker Hub.


## Enable SSH connections

SSH enables secure communication between a container and a client. With SSH enabled, you can connect to your container using App Service Advanced Tools (Kudu). For easy connection to your container using SSH, Azure Functions provides a base image that has SSH already enabled. You only need to edit your *Dockerfile*, then rebuild, and redeploy the image. You can then connect to the container through the Advanced Tools (Kudu).

In your

*Dockerfile*, append the string`-appservice`

to the base image in your`FROM`

instruction, as in the following example:`FROM mcr.microsoft.com/azure-functions/node:4-node18-appservice`

This example uses the SSH-enabled version of the Node.js version 18 base image. Visit the

[Azure Functions base image repos](https://mcr.microsoft.com/en-us/catalog?search=functions)to verify that you're using the latest version of the SSH-enabled base image.Rebuild the image by using the

`docker build`

command, replace the`<DOCKER_ID>`

with your Docker Hub account ID, as in the following example.`docker build --tag <DOCKER_ID>/azurefunctionsimage:v1.0.0 .`

Push the updated image to Docker Hub, which should take considerably less time than the first push. Only the updated segments of the image need to be uploaded now.

`docker push <DOCKER_ID>/azurefunctionsimage:v1.0.0`

Azure Functions automatically redeploys the image to your functions app. The process takes place in less than a minute.

In the

[Azure portal](https://portal.azure.com), locate your function app. In the left menu, select**Development Tools**>**SSH**. Select**Go**. Connecting might take a few moments if Azure is still updating the container image.After a connection is established with your container, run the

`top`

command to view the currently running processes.

## Related content

The following articles provide more information about deploying and managing containers:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-mysql-trigger -->

# Azure Database for MySQL trigger binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Database for MySQL trigger bindings monitor the user table for changes (inserts and updates) and invoke the function with updated row data.

Azure Database for MySQL trigger bindings use `az_func_updated_at`

and column data to monitor the user table for changes. As such, you need to alter the table structure to allow change tracking on the MySQL table before you use the trigger support. You can enable the change tracking on a table through the following query. For example, enable it on the `Products`

table:

```
ALTER TABLE Products
ADD az_func_updated_at TIMESTAMP DEFAULT
CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP;
```


The table for leases contains all columns that correspond to the primary key from the user table and three more columns: `az_func_AttemptCount`

, `az_func_LeaseExpirationTime`

, and `az_func_SyncCompletedTime`

. If any of the primary key columns have the same name, the result is an error message that lists conflicts. In this case, the listed primary key columns must be renamed for the trigger to work.

## Functionality overview

When the trigger function starts, it initiates two separate loops: the change polling loop and the lease renewal loop. These loops run continuously until the function is stopped.

The Azure Database for MySQL trigger binding uses the polling loop to check for changes. The polling loop triggers the user function when it detects changes. At a high level, the loop looks like this example:

```
while (true) {
1. Get list of changes on table - up to a maximum number controlled by the MySql_Trigger_MaxBatchSize setting
2. Trigger function with list of changes
3. Wait for delay controlled by MySql_Trigger_PollingIntervalMs setting
}
```


Changes are processed in the order that they're made. The oldest changes are processed first. Consider these points about change processing:

- If changes occur in multiple rows at once, the exact order in which they're sent to the function is based on the ascending order of the
`az_func_updated_at`

column and primary key columns. - Changes are batched for a row. If multiple changes occur in a row between each iteration of the loop, only the latest change entry that exists for that row is considered.

Note

Currently, managed identities aren't supported for connections between Azure Functions and Azure Database for MySQL.

## Example usage

More samples for the Azure Database for MySQL trigger are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples).

The example refers to a `Product`

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
{
if (obj is Product)
{
var that = obj as Product;
return this.ProductId == that.ProductId && this.Name == that.Name && this.Cost == that.Cost;
}
return false;
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


You enable change tracking on the database by adding one column to the table:

```
ALTER TABLE <table name>
ADD COLUMN az_func_updated_at TIMESTAMP
DEFAULT CURRENT_TIMESTAMP
ON UPDATE CURRENT_TIMESTAMP;
```


The Azure Database for MySQL trigger binds to `IReadOnlyList<MySqlChange<T>>`

, which lists `MySqlChange`

objects. Each object has two properties:

`Item`

: The item that was changed. The type of the item should follow the table schema, as seen in the`ToDoItem`

class.`Operation`

: A value from the`MySqlChangeOperation`

enumeration. The possible value is`Update`

for both inserts and updates.

The following example shows a [C# function](functions-dotnet-class-library) that's invoked when changes occur in the `Product`

table:

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.MySql;
using Microsoft.Extensions.Logging;
using AzureMySqlSamples.Common;
namespace AzureMySqlSamples.TriggerBindingSamples
{
private static readonly Action<ILogger, string, Exception> _loggerMessage = LoggerMessage.Define<string>(LogLevel.Information, eventId: new EventId(0, "INFO"), formatString: "{Message}");
[Function(nameof(ProductsTrigger))]
public static void Run(
[MySqlTrigger("Products", "MySqlConnectionString")]
IReadOnlyList<MySqlChange<Product>> changes, FunctionContext context)
{
ILogger logger = context.GetLogger("ProductsTrigger");
// The output is used to inspect the trigger binding parameter in test methods.
foreach (MySqlChange<Product> change in changes)
{
Product product = change.Item;
_loggerMessage(logger, $"Change operation: {change.Operation}", null);
_loggerMessage(logger, $"Product Id: {product.ProductId}, Name: {product.Name}, Cost: {product.Cost}", null);
}
}
}
```


## Example usage

More samples for the Azure Database for MySQL trigger are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-java).

The example refers to a `Product`

class, a `MySqlChangeProduct`

class, a `MySqlChangeOperation`

enumeration, and a corresponding database table.

In a separate file named Product.java:

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
public Product(int productId, String name, int cost) {
ProductId = productId;
Name = name;
Cost = cost;
}
}
```


In a separate file named MySqlChangeProduct.java:

```
package com.function.Common;
public class MySqlChangeProduct {
private MySqlChangeOperation Operation;
private Product Item;
public MySqlChangeProduct() {
}
public MySqlChangeProduct(MySqlChangeOperation operation, Product item) {
this.Operation = operation;
this.Item = item;
}
}
```


In a separate file named MySqlChangeOperation.java:

```
package com.function.Common;
import com.google.gson.annotations.SerializedName;
public enum MySqlChangeOperation {
@SerializedName("0")
Update
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


You enable change tracking on the database by adding the following column to the table:

```
ALTER TABLE <table name>
ADD COLUMN az_func_updated_at TIMESTAMP
DEFAULT CURRENT_TIMESTAMP
ON UPDATE CURRENT_TIMESTAMP;
```


The Azure Database for MySQL trigger binds to `MySqlChangeProduct[]`

, which is an array of `MySqlChangeProduct`

objects. Each object has two properties:

`item`

: The item that was changed. The type of the item should follow the table schema, as seen in the`Product`

class.`operation`

: A value from the`MySqlChangeOperation`

enumeration. The possible value is`Update`

for both inserts and updates.

The following example shows a Java function that's invoked when changes occur in the `Product`

table:

```
/**
* Copyright (c) Microsoft Corporation. All rights reserved.
* Licensed under the MIT License. See License.txt in the project root for
* license information.
*/
package com.function;
import com.microsoft.azure.functions.ExecutionContext;
import com.microsoft.azure.functions.annotation.FunctionName;
import com.microsoft.azure.functions.mysql.annotation.MySqlTrigger;
import com.function.Common.MySqlChangeProduct;
import com.google.gson.Gson;
import java.util.logging.Level;
public class ProductsTrigger {
@FunctionName("ProductsTrigger")
public void run(
@MySqlTrigger(
name = "changes",
tableName = "Products",
connectionStringSetting = "MySqlConnectionString")
MySqlChangeProduct[] changes,
ExecutionContext context) {
context.getLogger().log(Level.INFO, "MySql Changes: " + new Gson().toJson(changes));
}
}
```


## Example usage

More samples for the Azure Database for MySQL trigger are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-powershell).

The example refers to a `Product`

database table:

```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


You enable change tracking on the database by adding one column to the table:

```
ALTER TABLE <table name>
ADD COLUMN az_func_updated_at TIMESTAMP
DEFAULT CURRENT_TIMESTAMP
ON UPDATE CURRENT_TIMESTAMP;
```


The Azure Database for MySQL trigger binds to `Product`

, which lists objects. Each object has two properties:

`item`

: The item that was changed. The structure of the item follows the table schema.`operation`

: The possible value is`Update`

for both inserts and updates.

The following example shows a PowerShell function that's invoked when changes occur in the `Product`

table.

The following example is binding data in the function.json file:

```
{
"bindings": [
{
"name": "changes",
"type": "mysqlTrigger",
"direction": "in",
"tableName": "Products",
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
param($changes)
# The output is used to inspect the trigger binding parameter in test methods.
# Use -Compress to remove new lines and spaces for testing purposes.
$changesJson = $changes | ConvertTo-Json -Compress
Write-Host "MySql Changes: $changesJson"
```


## Example usage

More samples for the Azure Database for MySQL trigger are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-js).

The example refers to a `Product`

database table:

```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


You enable change tracking on the database by adding one column to the table:

```
ALTER TABLE <table name>
ADD COLUMN az_func_updated_at TIMESTAMP
DEFAULT CURRENT_TIMESTAMP
ON UPDATE CURRENT_TIMESTAMP;
```


The Azure Database for MySQL trigger binds to `Changes`

, which is an array of objects. Each object has two properties:

`item`

: The item that was changed. The structure of the item follows the table schema.`operation`

: The possible value is`Update`

for both inserts and updates.

The following example shows a JavaScript function that's invoked when changes occur in the `Product`

table.

The following example is binding data in the function.json file:

```
{
"bindings": [
{
"name": "changes",
"type": "mysqlTrigger",
"direction": "in",
"tableName": "Products",
"connectionStringSetting": "MySqlConnectionString",
}
],
"disabled": false
}
```


The [Configuration](#configuration) section explains these properties.

The following example is sample JavaScript code for the function in the `index.js`

file:

```
module.exports = async function (context, changes) {
context.log(`MySql Changes: ${JSON.stringify(changes)}`)
}
```


## Example usage

More samples for the Azure Database for MySQL trigger are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-python).

The example refers to a `Product`

database table:

```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


You enable change tracking on the database by adding one column to the table:

```
ALTER TABLE <table name>
ADD COLUMN az_func_updated_at TIMESTAMP
DEFAULT CURRENT_TIMESTAMP
ON UPDATE CURRENT_TIMESTAMP;
```


Note

You must use Azure Functions version 1.22.0b4 for Python.

The Azure Database for MySQL trigger binds to a variable named `Product`

, which lists objects. Each object has two properties:

`item`

: The item that was changed. The structure of the item follows the table schema.`operation`

: The possible value is`Update`

for both inserts and updates.

The following example shows a Python function that's invoked when changes occur in the `Product`

table.

The following example is sample Python code for the function_app.py file:

```
import json
import logging
import azure.functions as func
app = func.FunctionApp()
# The function is triggered when a change (insert, update)
# is made to the Products table.
@app.function_name(name="ProductsTrigger")
@app.mysql_trigger(arg_name="products",
table_name="Products",
connection_string_setting="MySqlConnectionString")
def products_trigger(products: str) -> None:
logging.info("MySQL Changes: %s", json.loads(products))
```


## Attributes

| Attribute property | Description |
|---|---|
`TableName` |
Required. The name of the table that the trigger monitors. |
`ConnectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database that contains the table monitored for changes. The name of the connection string setting corresponds to the application setting (in local.settings.json for local development) that contains the
|

`LeasesTableName`

`Leases_{FunctionId}_{TableId}`

.## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@MySQLTrigger`

annotation on parameters whose values would come from Azure Database for MySQL. This annotation supports the following elements:

| Element | Description |
|---|---|
`name` |
Required. The name of the parameter that the trigger binds to. |
`tableName` |
Required. The name of the table that the trigger monitors. |
`connectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database that contains the table monitored for changes. The name of the connection string setting corresponds to the application setting (in local.settings.json for local development) that contains the
|

`LeasesTableName`

`Leases_{FunctionId}_{TableId}`

.## Configuration

The following table explains the binding configuration properties that you set in the function.json file:

| Property | Description |
|---|---|
`name` |
Required. The name of the parameter that the trigger binds to. |
`type` |
Required. Must be set to `MysqlTrigger` . |
`direction` |
Required. Must be set to `in` . |
`tableName` |
Required. The name of the table that the trigger monitors. |
`connectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database that contains the table monitored for changes. The name of the connection string setting corresponds to the application setting (in local.settings.json for local development) that contains the
|

`LeasesTableName`

`Leases_{FunctionId}_{TableId}`

.## Optional configuration

You can configure the following optional settings for the Azure Database for MySQL trigger for local development or for cloud deployments.

### host.json

This section describes the configuration settings available for this binding in version 2.x and later. Settings in the host.json file apply to all functions in a function app instance. For more information about function app configuration settings, see [host.json reference for Azure Functions](functions-host-json).

| Setting | Default | Description |
|---|---|---|
`MaxBatchSize` |
`100` |
The maximum number of changes processed with each iteration of the trigger loop before they're sent to the triggered function. |
`PollingIntervalMs` |
`1000` |
The delay in milliseconds between processing each batch of changes. (1,000 ms is 1 second.) |
`MaxChangesPerWorker` |
`1000` |
The upper limit on the number of pending changes in the user table that are allowed per application worker. If the count of changes exceeds this limit, it might result in a scale-out. The setting applies only for Azure function apps with
|

#### Example host.json file

Here's an example host.json file with the optional settings:

```
{
"version": "2.0",
"extensions": {
"MySql": {
"MaxBatchSize": 300,
"PollingIntervalMs": 1000,
"MaxChangesPerWorker": 100
}
},
"logging": {
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"excludedTypes": "Request"
}
},
"logLevel": {
"default": "Trace"
}
}
}
```


### local.setting.json

The local.settings.json file stores app settings and settings that local development tools use. Settings in the local.settings.json file are used only when you're running your project locally. When you publish your project to Azure, be sure to also add any required settings to the app settings for the function app.

Important

Because the local.settings.json file might contain secrets, such as connection strings, you should never store it in a remote repository. Tools that support Azure Functions provide ways to synchronize settings in the local.settings.json file with the [app settings](functions-how-to-use-azure-function-app-settings#settings) in the function app to which your project is deployed.

| Setting | Default | Description |
|---|---|---|
`MySql_Trigger_BatchSize` |
`100` |
The maximum number of changes processed with each iteration of the trigger loop before they're sent to the triggered function. |
`MySql_Trigger_PollingIntervalMs` |
`1000` |
The delay in milliseconds between processing each batch of changes. (1,000 ms is 1 second.) |
`MySql_Trigger_MaxChangesPerWorker` |
`1000` |
The upper limit on the number of pending changes in the user table that are allowed per application worker. If the count of changes exceeds this limit, it might result in a scale-out. The setting applies only for Azure function apps with
|

#### Example local.settings.json file

Here's an example local.settings.json file with the optional settings:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "UseDevelopmentStorage=true",
"FUNCTIONS_WORKER_RUNTIME": "dotnet",
"MySqlConnectionString": "",
"MySql_Trigger_MaxBatchSize": 300,
"MySql_Trigger_PollingIntervalMs": 1000,
"MySql_Trigger_MaxChangesPerWorker": 100
}
}
```


## Set up change tracking (required)

Setting up change tracking for use with the Azure Database for MySQL trigger requires you to add a column in a table by using a function. You can complete these steps from any MySQL tool that supports running queries, including [Visual Studio Code](/en-us/sql/tools/visual-studio-code/mssql-extensions) or [Azure Data Studio](/en-us/azure-data-studio/download-azure-data-studio).

Azure Database for MySQL trigger bindings use `az_func_updated_at`

and column data to monitor the user table for changes. As such, you need to alter the table structure to allow change tracking on the MySQL table before you use the trigger support. You can enable the change tracking on a table through the following query. For example, enable it on the `Products`

table:

```
ALTER TABLE Products;
ADD az_func_updated_at
TIMESTAMP DEFAULT CURRENT_TIMESTAMP
ON UPDATE CURRENT_TIMESTAMP;
```


The table for leases contains all columns that correspond to the primary key from the user table and two more columns: `az_func_AttemptCount`

and `az_func_LeaseExpirationTime`

. If any of the primary key columns have the same name, the result is an error message that lists conflicts. In this case, the listed primary key columns must be renamed for the trigger to work.

## Enable runtime-driven scaling

Optionally, your functions can scale automatically based on the number of changes that are pending to be processed in the user table. To allow your functions to scale properly on the Premium plan when you're using Azure Database for MySQL triggers, you need to enable runtime scale monitoring.

In the Azure portal, in your function app, select

**Configuration**.On the

**Function runtime settings**tab, for**Runtime Scale Monitoring**, select**On**.

## Retry support

### Startup retries

If an exception occurs during startup, the host runtime automatically attempts to restart the trigger listener with an exponential backoff strategy. These retries continue until either the listener is successfully started or the startup is canceled.

### Function exception retries

If an exception occurs in the user function during change processing, the batch of rows currently being processed is retried again in 60 seconds. Other changes are processed as normal during this time, but the rows in the batch that caused the exception are ignored until the time-out period elapses.

If the function execution fails five consecutive times for a particular row, that row is ignored for all future changes. Because the rows in a batch aren't deterministic, rows in a failed batch might end up in different batches in subsequent invocations. This behavior means that not all rows in the failed batch are necessarily ignored. If other rows in the batch caused the exception, the "good" rows might end up in a different batch that doesn't fail in future invocations.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-table-input -->

# Azure Tables input bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the Azure Tables input binding to read a table in [Azure Cosmos DB for Table](/en-us/azure/cosmos-db/table/introduction) or [Azure Table Storage](../storage/tables/table-storage-overview).

For information on setup and configuration details, see the [overview](functions-bindings-storage-table).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

## Example

The usage of the binding depends on the extension package version and the C# modality used in your function app, which can be one of the following:

An [isolated worker process class library](dotnet-isolated-process-guide) compiled C# function runs in a process isolated from the runtime.

Choose a version to see examples for the mode and version.

The following `MyTableData`

class represents a row of data in the table:

```
public class MyTableData : Azure.Data.Tables.ITableEntity
{
public string Text { get; set; }
public string PartitionKey { get; set; }
public string RowKey { get; set; }
public DateTimeOffset? Timestamp { get; set; }
public ETag ETag { get; set; }
}
```


The following function, which is started by a Queue Storage trigger, reads a row key from the queue, which is used to get the row from the input table. The expression `{queueTrigger}`

binds the row key to the message metadata, which is the message string.

```
[Function("TableFunction")]
[TableOutput("OutputTable", Connection = "AzureWebJobsStorage")]
public static MyTableData Run(
[QueueTrigger("table-items")] string input,
[TableInput("MyTable", "<PartitionKey>", "{queueTrigger}")] MyTableData tableInput,
FunctionContext context)
{
var logger = context.GetLogger("TableFunction");
logger.LogInformation($"PK={tableInput.PartitionKey}, RK={tableInput.RowKey}, Text={tableInput.Text}");
return new MyTableData()
{
PartitionKey = "queue",
RowKey = Guid.NewGuid().ToString(),
Text = $"Output record with rowkey {input} created at {DateTime.Now}"
};
}
```


The following Queue-triggered function returns the first 5 entities as an `IEnumerable<T>`

, with the partition key value set as the queue message.

```
[Function("TestFunction")]
public static void Run([QueueTrigger("myqueue", Connection = "AzureWebJobsStorage")] string partition,
[TableInput("inTable", "{queueTrigger}", Take = 5, Filter = "Text eq 'test'",
Connection = "AzureWebJobsStorage")] IEnumerable<MyTableData> tableInputs,
FunctionContext context)
{
var logger = context.GetLogger("TestFunction");
logger.LogInformation(partition);
foreach (MyTableData tableInput in tableInputs)
{
logger.LogInformation($"PK={tableInput.PartitionKey}, RK={tableInput.RowKey}, Text={tableInput.Text}");
}
}
```


The `Filter`

and `Take`

properties are used to limit the number of entities returned.

The following example shows an HTTP triggered function which returns a list of person objects who are in a specified partition in Table storage. In the example, the partition key is extracted from the http route, and the tableName and connection are from the function settings.

```
public class Person {
private String PartitionKey;
private String RowKey;
private String Name;
public String getPartitionKey() { return this.PartitionKey; }
public void setPartitionKey(String key) { this.PartitionKey = key; }
public String getRowKey() { return this.RowKey; }
public void setRowKey(String key) { this.RowKey = key; }
public String getName() { return this.Name; }
public void setName(String name) { this.Name = name; }
}
@FunctionName("getPersonsByPartitionKey")
public Person[] get(
@HttpTrigger(name = "getPersons", methods = {HttpMethod.GET}, authLevel = AuthorizationLevel.FUNCTION, route="persons/{partitionKey}") HttpRequestMessage<Optional<String>> request,
@BindingName("partitionKey") String partitionKey,
@TableInput(name="persons", partitionKey="{partitionKey}", tableName="%MyTableName%", connection="MyConnectionString") Person[] persons,
final ExecutionContext context) {
context.getLogger().info("Got query for person related to persons with partition key: " + partitionKey);
return persons;
}
```


The TableInput annotation can also extract the bindings from the json body of the request, like the following example shows.

```
@FunctionName("GetPersonsByKeysFromRequest")
public HttpResponseMessage get(
@HttpTrigger(name = "getPerson", methods = {HttpMethod.GET}, authLevel = AuthorizationLevel.FUNCTION, route="query") HttpRequestMessage<Optional<String>> request,
@TableInput(name="persons", partitionKey="{partitionKey}", rowKey = "{rowKey}", tableName="%MyTableName%", connection="MyConnectionString") Person person,
final ExecutionContext context) {
if (person == null) {
return request.createResponseBuilder(HttpStatus.NOT_FOUND)
.body("Person not found.")
.build();
}
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(person)
.build();
}
```


The following example uses a filter to query for persons with a specific name in an Azure Table, and limits the number of possible matches to 10 results.

```
@FunctionName("getPersonsByName")
public Person[] get(
@HttpTrigger(name = "getPersons", methods = {HttpMethod.GET}, authLevel = AuthorizationLevel.FUNCTION, route="filter/{name}") HttpRequestMessage<Optional<String>> request,
@BindingName("name") String name,
@TableInput(name="persons", filter="Name eq '{name}'", take = "10", tableName="%MyTableName%", connection="MyConnectionString") Person[] persons,
final ExecutionContext context) {
context.getLogger().info("Got query for person related to persons with name: " + name);
return persons;
}
```


The following example shows a table input binding that uses a queue trigger to read a single table row. The binding specifies a `partitionKey`

and a `rowKey`

. The `rowKey`

value "{queueTrigger}" indicates that the row key comes from the queue message string.

```
import { app, input, InvocationContext } from '@azure/functions';
const tableInput = input.table({
tableName: 'Person',
partitionKey: 'Test',
rowKey: '{queueTrigger}',
connection: 'MyStorageConnectionAppSetting',
});
interface PersonEntity {
PartitionKey: string;
RowKey: string;
Name: string;
}
export async function storageQueueTrigger1(queueItem: unknown, context: InvocationContext): Promise<void> {
context.log('Node.js queue trigger function processed work item', queueItem);
const person = <PersonEntity>context.extraInputs.get(tableInput);
context.log('Person entity name: ' + person.Name);
}
app.storageQueue('storageQueueTrigger1', {
queueName: 'myqueue-items',
connection: 'MyStorageConnectionAppSetting',
extraInputs: [tableInput],
handler: storageQueueTrigger1,
});
```


```
const { app, input } = require('@azure/functions');
const tableInput = input.table({
tableName: 'Person',
partitionKey: 'Test',
rowKey: '{queueTrigger}',
connection: 'MyStorageConnectionAppSetting',
});
app.storageQueue('storageQueueTrigger1', {
queueName: 'myqueue-items',
connection: 'MyStorageConnectionAppSetting',
extraInputs: [tableInput],
handler: (queueItem, context) => {
context.log('Node.js queue trigger function processed work item', queueItem);
const person = context.extraInputs.get(tableInput);
context.log('Person entity name: ' + person.Name);
},
});
```


The following function uses a queue trigger to read a single table row as input to a function.

In this example, the binding configuration specifies an explicit value for the table's `partitionKey`

and uses an expression to pass to the `rowKey`

. The `rowKey`

expression, `{queueTrigger}`

, indicates that the row key comes from the queue message string.

Binding configuration in *function.json*:

```
{
"bindings": [
{
"queueName": "myqueue-items",
"connection": "MyStorageConnectionAppSetting",
"name": "MyQueueItem",
"type": "queueTrigger",
"direction": "in"
},
{
"name": "PersonEntity",
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


PowerShell code in *run.ps1*:

```
param($MyQueueItem, $PersonEntity, $TriggerMetadata)
Write-Host "PowerShell queue trigger function processed work item: $MyQueueItem"
Write-Host "Person entity name: $($PersonEntity.Name)"
```


The following function uses an HTTP trigger to read a single table row as input to a function.

In this example, binding configuration specifies an explicit value for the table's `partitionKey`

and uses an expression to pass to the `rowKey`

. The `rowKey`

expression, `{id}`

indicates that the row key comes from the `{id}`

part of the route in the request.

```
import json
import azure.functions as func
app = func.FunctionApp()
@app.route(route="messages/{id}")
@app.table_input(arg_name="messageJSON",
connection="AzureWebJobsStorage",
table_name="messages",
row_key='{id}',
partition_key="message")
def table_in_binding(req: func.HttpRequest, messageJSON):
message = json.loads(messageJSON)
return func.HttpResponse(f"Table row: {messageJSON}")
```


With this simple binding, you can't programmatically handle a case in which no row that has a row key ID is found. For more fine-grained data selection, use the [storage SDK](/en-us/azure/developer/python/sdk/examples/azure-sdk-example-storage-use?tabs=cmd).

## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#table-input).

In [C# class libraries](dotnet-isolated-process-guide), the `TableInputAttribute`

supports the following properties:

| Attribute property | Description |
|---|---|
TableName |
The name of the table. |
PartitionKey |
Optional. The partition key of the table entity to read. |
RowKey |
Optional. The row key of the table entity to read. |
Take |
Optional. The maximum number of entities to read into an
`IEnumerable<T>` |

`RowKey`

.**Filter**[. Can't be used with](/en-us/dotnet/api/system.collections.generic.ienumerable-1)`IEnumerable<T>`

`RowKey`

.**Connection**[Connections](#connections).## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@TableInput`

annotation on parameters whose value would come from Table storage. This annotation can be used with native Java types, POJOs, or nullable values using `Optional<T>`

. This annotation supports the following elements:

| Element | Description |
|---|---|
|
The name of the variable that represents the table or entity in function code. |
|
The name of the table. |
|
Optional. The partition key of the table entity to read. |
|
Optional. The row key of the table entity to read. |
|
Optional. The maximum number of entities to read. |
|
Optional. An OData filter expression for table input. |
|
The name of an app setting or setting collection that specifies how to connect to the table service. See
|

## Configuration

The following table explains the properties that you can set on the `options`

object passed to the `input.table()`

method.

| Property | Description |
|---|---|
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

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

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

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Connections

The `connection`

property is a reference to environment configuration that specifies how the app should connect to your table service. It may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections)

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

To obtain a connection string for tables in Azure Table storage, follow the steps shown at [Manage storage account access keys](../storage/common/storage-account-keys-manage). To obtain a connection string for tables in Azure Cosmos DB for Table, follow the steps shown at the [Azure Cosmos DB for Table FAQ](/en-us/azure/cosmos-db/table/table-api-faq#what-is-the-connection-string-that-i-need-to-use-to-connect-to-the-api-for-table-).

This connection string should be stored in an application setting with a name matching the value specified by the `connection`

property of the binding configuration.

If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name here. For example, if you set `connection`

to "MyStorage", the Functions runtime looks for an app setting that is named "AzureWebJobsMyStorage". If you leave `connection`

empty, the Functions runtime uses the default Storage connection string in the app setting that is named `AzureWebJobsStorage`

.

### Identity-based connections

If you're using [the Tables API extension](functions-bindings-storage-table#table-api-extension), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). This only applies when accessing tables in Azure Storage. To use an identity, you define settings under a common prefix that maps to the `connection`

property in the trigger and binding configuration.

If you're setting `connection`

to "AzureWebJobsStorage", see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity). For all other connections, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Table Service URI | `<CONNECTION_NAME_PREFIX>__tableServiceUri` 1 |
The data plane URI of the Azure Storage table service to which you're connecting, using the HTTPS scheme. | https://<storage_account_name>.table.core.windows.net |

1 `<CONNECTION_NAME_PREFIX>__serviceUri`

can be used as an alias. If both forms are provided, the `tableServiceUri`

form is used. The `serviceUri`

form can't be used when the overall connection configuration is to be used across blobs, queues, and/or tables.

Other properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

The `serviceUri`

form can't be used when the overall connection configuration is to be used across blobs, queues, and/or tables in Azure Storage. The URI can only designate the table service. As an alternative, you can provide a URI specifically for each service under the same prefix, allowing a single connection to be used.

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

You'll need to create a role assignment that provides access to your Azure Storage table service at runtime. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) aren't sufficient. The following table shows built-in roles that are recommended when using the Azure Tables extension against Azure Storage in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles (Azure Storage1) |
|---|---|
| Input binding |
|

[Storage Table Data Contributor](../role-based-access-control/built-in-roles#storage-table-data-contributor)1 If your app is instead connecting to tables in Azure Cosmos DB for Table, using an identity isn't supported and the connection must use a connection string.

## Usage

The usage of the binding depends on the extension package version, and the C# modality used in your function app, which can be one of the following:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see usage details for the mode and version.

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

The [TableInput](/en-us/java/api/com.microsoft.azure.functions.annotation.tableinput) attribute gives you access to the table row that triggered the function.

Data is passed to the input parameter as specified by the `name`

key in the *function.json* file. Specifying The `partitionKey`

and `rowKey`

allows you to filter to specific records.

Table data is passed to the function as a JSON string. De-serialize the message by calling `json.loads`

as shown in the input [example](#example).

For specific usage details, see [Example](#example).
