---
merged_at: 2026-01-26T23:29:57.701298
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-mcp -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/supported-languages -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-compare-logic-apps-ms-flow-webjobs -->

# Choose the right integration and automation services in Azure

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article compares the following Microsoft cloud services:

[Microsoft Power Automate](https://make.powerautomate.com/)(was Microsoft Flow)[Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/)[Azure Functions](https://azure.microsoft.com/services/functions/)[Azure App Service WebJobs](../app-service/webjobs-create)

All of these services can solve integration problems and automate business processes. They can all define input, actions, conditions, and output. You can run each of them on a schedule or trigger. Each service has unique advantages, and this article explains the differences.

Note

If you're looking for a more general comparison between Azure Functions and other Azure compute options, see the following articles:

For a summary and comparison of automation service options in Azure,
see [Choose the Automation services in Azure](../automation/automation-services).

## Compare Azure Logic Apps and Microsoft Power Automate

These services are both *designer-first* integration platforms where you can build and run automated workflows. Both platforms integrate with various Software-as-a-Service (SaaS) and enterprise applications. Both provide similar workflow designers, and while [their connectors share some overlap](/en-us/connectors/connector-reference/), each platform also offers their own unique connectors.

Power Automate empowers business users, office workers, and citizen developers to build simple integrations without having to work with IT or developers or to write code. One example might be an approval workflow for a SharePoint document library. Azure Logic Apps supports integrations ranging from little-to-no-code scenarios to more advanced, codeful, and complex workflows. Examples include B2B processes or scenarios that require enterprise-level interactions with Azure DevOps. A business workflow can also grow from simple to complete over time.

To help you determine whether you want to use Azure Logic Apps or Power Automate for a specific integration, see the [Capability comparison table](/en-us/azure/logic-apps/power-automate-migration#compare-capability-details).

## Compare Azure Functions and Azure Logic Apps

These Azure services enable you to build and run serverless workloads. Azure Functions is a serverless compute service, while Azure Logic Apps is a serverless workflow integration platform. Both can create complex *orchestrations*. An orchestration is a collection of functions, which are called *actions* in Azure Logic Apps, that you can run to complete a complex task. For example, to process a batch of orders, you might execute many instances of a function in parallel, wait for all instances to finish, and then execute a function that computes a result on the aggregate.

For Azure Functions, you develop orchestrations by writing code and using the [Durable Functions extension](durable/durable-functions-overview). For Azure Logic Apps, you create orchestrations by using a visual designer or by editing Azure Resource Manager templates.

You can mix and match services when you build an orchestration. For example, you can call functions from logic app workflows and call logic app workflows from functions. Choose how to build each orchestration based on the services' capabilities or your personal preference. The following table lists some key differences between these services:

## Compare Functions and WebJobs

Like Azure Functions, Azure App Service WebJobs with the WebJobs SDK is a *code-first* integration service that is designed for developers. Both are built on [Azure App Service](../app-service/overview) and support features such as [source control integration](../app-service/deploy-continuous-deployment), [authentication](../app-service/overview-authentication-authorization), and [monitoring with Application Insights integration](functions-monitoring).

### WebJobs and the WebJobs SDK

You can use the *WebJobs* feature of App Service to run a script or code in the context of an App Service web app. The *WebJobs SDK* is a framework designed for WebJobs that simplifies the code you write to respond to events in Azure services. For example, you might respond to the creation of an image blob in Azure Storage by creating a thumbnail image. The WebJobs SDK runs as a .NET console application, which you can deploy to a WebJob.

WebJobs and the WebJobs SDK work best together, but you can use WebJobs without the WebJobs SDK and vice versa. A WebJob can run any program or script that runs in the App Service sandbox. A WebJobs SDK console application can run anywhere console applications run, such as on-premises servers.

### Comparison table

Azure Functions is built on the WebJobs SDK, so it shares many of the same event triggers and connections to other Azure services. Here are some factors to consider when you're choosing between Azure Functions and WebJobs with the WebJobs SDK:

| Functions | WebJobs with WebJobs SDK | |
|---|---|---|
|
✔ | |
|
✔ | |
|
✔ | |
|
✔ | |
Trigger events |
|

[Timer](functions-bindings-timer)[Azure Storage queues and blobs](functions-bindings-storage-blob)[Azure Service Bus queues and topics](functions-bindings-service-bus)[Azure Cosmos DB](functions-bindings-cosmosdb)[Azure Event Hubs](functions-bindings-event-hubs)[File system](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Files/FileTriggerAttribute.cs)**Supported languages**F#

JavaScript

Java

Python

PowerShell

1**Package managers**21 WebJobs (without the WebJobs SDK) supports languages such as C#, Java, JavaScript, Bash, .cmd, .bat, PowerShell, PHP, TypeScript, Python, and more. A WebJob can run any program or script that can run in the App Service sandbox.

2 WebJobs (without the WebJobs SDK) supports npm and NuGet.

### Summary

Azure Functions offers more developer productivity than Azure App Service WebJobs does. It also offers more options for programming languages, development environments, Azure service integration, and pricing. For most scenarios, it's the best choice.

Here are two scenarios for which WebJobs might be the best choice:

- You need more control over the code that listens for events, the
`JobHost`

object. Functions offers a limited number of ways to customize`JobHost`

behavior in the[host.json](functions-host-json)file. Sometimes you need to do things that you can't specify by using a string in a JSON file. For example, only the WebJobs SDK lets you configure a custom retry policy for Azure Storage. - You have an App Service app for which you want to run code snippets, and you want to manage them together in the same Azure DevOps environment.

For other scenarios where you want to run code snippets for integrating Azure or external services, choose Azure Functions over WebJobs with the WebJobs SDK.

## Power Automate, Logic Apps, Functions, and WebJobs together

You don't have to choose just one of these services. They integrate with each other and with external services.

A Power Automate flow can call an Azure Logic Apps workflow. An Azure Logic Apps workflow can call a function in Azure Functions, and vice versa. For example, see [Create a function that integrates with Azure Logic Apps](functions-twitter-email).

Between Power Automate, Azure Logic Apps, and Functions, the integration experience between these services continues to improve over time. You can build a component in one service and use that component in the other services.

For more information about integration services, see the following articles:

[Leveraging Azure Functions & Azure App Service for integration scenarios by Christopher Anderson](https://www.biztalk360.com/integrate-2016-resources/leveraging-azure-functions-azure-app-service-integration-scenarios/)[Integrations Made Simple by Charles Lamanna](https://www.biztalk360.com/integrate-2016-resources/integrations-made-simple/)[Azure Logic Apps Live webcast](https://aka.ms/logicappslive)[Power Automate frequently asked questions](/en-us/power-automate/frequently-asked-questions)

## Next steps

Get started by creating your first flow, logic app workflow, or function app. Select any of the following links:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache-input -->

# Azure Cache for Redis input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When a function runs, the Azure Cache for Redis input binding retrieves data from a cache and passes it to your function as an input parameter.

For information on setup and configuration details, see the [overview](functions-bindings-cache).

## Scope of availability for functions bindings

| Binding Type | Azure Managed Redis | Azure Cache for Redis |
|---|---|---|
| Input | Yes | Yes |

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

Important

For .NET functions, using the *isolated worker* model is recommended over the *in-process* model. For a comparison of the *in-process* and *isolated worker* models, see differences between the *isolated worker* model and the *in-process* model for .NET on Azure Functions.

The following code uses the key from the pub/sub trigger to obtain and log the value from an input binding using a `GET`

command:

```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.Functions.Worker.Extensions.Redis.Samples.RedisInputBinding
{
public class SetGetter
{
private readonly ILogger<SetGetter> logger;
public SetGetter(ILogger<SetGetter> logger)
{
this.logger = logger;
}
[Function(nameof(SetGetter))]
public void Run(
[RedisPubSubTrigger(Common.connectionStringSetting, "__keyevent@0__:set")] string key,
[RedisInput(Common.connectionStringSetting, "GET {Message}")] string value)
{
logger.LogInformation($"Key '{key}' was set to value '{value}'");
}
}
}
```


More samples for the Azure Cache for Redis input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-redis-extension).

The following code uses the key from the pub/sub trigger to obtain and log the value from an input binding using a `GET`

command:

```
package com.function.RedisInputBinding;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.redis.annotation.*;
public class SetGetter {
@FunctionName("SetGetter")
public void run(
@RedisPubSubTrigger(
name = "key",
connection = "redisConnectionString",
channel = "__keyevent@0__:set")
String key,
@RedisInput(
name = "value",
connection = "redisConnectionString",
command = "GET {Message}")
String value,
final ExecutionContext context) {
context.getLogger().info("Key '" + key + "' was set to value '" + value + "'");
}
}
```


This function.json defines both a pub/sub trigger and an input binding to the GET message on an Azure Cache for Redis instance:

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
"command": "GET {Message}",
"name": "value",
"direction": "in"
}
],
"scriptFile": "index.js"
}
```


This JavaScript code (from index.js) retrieves and logs the cached value related to the key provided by the pub/sub trigger.

```
module.exports = async function (context, key, value) {
context.log("Key '" + key + "' was set to value '" + value + "'");
}
```


This function.json defines both a pub/sub trigger and an input binding to the GET message on an Azure Cache for Redis instance:

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
"command": "GET {Message}",
"name": "value",
"direction": "in"
}
],
"scriptFile": "run.ps1"
}
```


This PowerShell code (from run.ps1) retrieves and logs the cached value related to the key provided by the pub/sub trigger.

```
param($key, $value, $TriggerMetadata)
Write-Host "Key '$key' was set to value '$value'"
```


The following example uses a pub/sub trigger with an input binding to the GET message on an Azure Cache for Redis instance. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

This function.json defines both a pub/sub trigger and an input binding to the GET message on an Azure Cache for Redis instance:

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
"command": "GET {Message}",
"name": "value",
"direction": "in"
}
]
}
```


This Python code (from __init__.py) retrieves and logs the cached value related to the key provided by the pub/sub trigger:

```
import logging
def main(key: str, value: str):
logging.info("Key '" + key + "' was set to value '" + value + "'")
```


The [configuration](#configuration) section explains these properties.

## Attributes

Note

Not all commands are supported for this binding. At the moment, only read commands that return a single output are supported. The full list can be found [here](https://github.com/Azure/azure-functions-redis-extension/blob/main/src/Microsoft.Azure.WebJobs.Extensions.Redis/Bindings/RedisAsyncConverter.cs#L63)

| Attribute property | Description |
|---|---|
`Connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`Command`

`GET key`

, `HGET key field`

.## Annotations

The `RedisInput`

annotation supports these properties:

| Property | Description |
|---|---|
`name` |
The name of the specific input binding. |
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`command`

`GET key`

or `HGET key field`

.## Configuration

The following table explains the binding configuration properties that you set in the function.json file.

| function.json property | Description |
|---|---|
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`command`

`GET key`

, `HGET key field`

.Note

Python v2 and Node.js v4 for Functions don't use function.json to define the function. Both of these new language versions aren't currently supported by Azure Redis Cache bindings.

See the [Example section](#example) for complete examples.

## Usage

The input binding expects to receive a string from the cache.

When you use a custom type as the binding parameter, the extension tries to deserialize a JSON-formatted string into the custom type of this parameter.

Important

For optimal security, your function app should use Microsoft Entra ID with managed identities to authorize requests against your cache, if possible. Authorization by using Microsoft Entra ID and managed identities provides superior security and ease of use over shared access key authorization. For more information about using managed identities with your cache, see [Use Microsoft Entra ID for cache authentication](/en-us/azure/azure-cache-for-redis/cache-azure-active-directory-for-authentication).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-core-tools-reference -->

# Azure Functions Core Tools reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides reference documentation for the Azure Functions Core Tools. With this local runtime and command-line tools, you can develop, manage, and deploy Azure Functions projects from your local computer. To learn more about using Core Tools, see [Work with Azure Functions Core Tools](functions-run-local).

Core Tools commands are organized into the following contexts, each providing a unique set of actions.

| Command context | Description |
|---|---|
`func` |

`func azure`

`func azurecontainerapps`

`func durable`

[Durable Functions](durable/durable-functions-overview).`func extensions`

`func kubernetes`

`func settings`

`func templates`

Before using the commands in this article, you must [install the Core Tools](functions-run-local#install-the-azure-functions-core-tools).

`func init`


Creates a new Functions project in a specific language.

```
func init <PROJECT_FOLDER>
```


When you supply `<PROJECT_FOLDER>`

, the project is created in a new folder with this name. Otherwise, the current folder is used.

`func init`

supports the following options, which don't support version 1.x unless otherwise noted:

| Option | Description |
|---|---|
`--csx` |
Creates .NET functions as C# script, which is the version 1.x behavior. Valid only with `--worker-runtime dotnet` . |
`--docker` |
Creates a Dockerfile for a container using a base image that is based on the chosen `--worker-runtime` . Use this option when you plan to deploy a containerized function app. |
`--docker-only` |
Adds a Dockerfile to an existing project. Prompts for the worker-runtime if not specified or set in local.settings.json. Use this option when you plan to deploy a containerized function app and the project already exists. |
`--force` |
Initialize the project even when there are existing files in the project. This setting overwrites existing files with the same name. Other files in the project folder aren't affected. |
`--language` |
Initializes a language-specific project. Currently supported when `--worker-runtime` set to `node` . Options are `typescript` and `javascript` . You can also use `--worker-runtime javascript` or `--worker-runtime typescript` . |
`--managed-dependencies` |
Installs managed dependencies. Currently, only the PowerShell worker runtime supports this functionality. |
`--model` |
Sets the desired programming model for a target language when more than one model is available. Supported options are `V1` and `V2` for Python and `V3` and `V4` for Node.js. For more information, see the
|
`--source-control` |
Controls whether a git repository is created. By default, a repository isn't created. When `true` , a repository is created. |
`--worker-runtime` |
Sets the language runtime for the project. Supported values are: `csharp` , `dotnet` , `dotnet-isolated` , `javascript` ,`node` (defaults to JavaScript), `powershell` , `python` , and `typescript` . For Java, use
`custom` . When not set, you're prompted to choose your runtime during initialization. |
`--target-framework` |
Sets the target framework for the function app project. Valid only with `--worker-runtime dotnet-isolated` . Supported values are: `net10.0` (preview), `net9.0` , `net8.0` (default), `net6.0` , and `net48` (.NET Framework 4.8). |

Note

When you use either `--docker`

or `--docker-only`

options, Core Tools automatically create the Dockerfile for C#, JavaScript, Python, and PowerShell functions. For Java functions, you must manually create the Dockerfile. For more information, see [Creating containerized function apps](functions-how-to-custom-container#creating-containerized-function-apps).

`func logs`


Gets logs for functions running in a Kubernetes cluster.

```
func logs --platform kubernetes --name <APP_NAME>
```


The `func logs`

action supports the following options:

| Option | Description |
|---|---|
`--platform` |
Hosting platform for the function app. Supported options: `kubernetes` . |
`--name` |
Function app name in Azure. |

For more information, see [Azure Functions on Kubernetes with KEDA](functions-kubernetes-keda).

`func new`


Creates a new function in the current project based on a template.

```
func new
```


When you run `func new`

without the `--template`

option, you're prompted to choose a template. In version 1.x, you must use the `--language`

option to set the language.

The `func new`

action supports the following options:

| Option | Description |
|---|---|
`--authlevel` |
Set the authorization level for an HTTP trigger. Supported values are: `function` , `anonymous` , `admin` . Authorization isn't enforced when running locally. For more information, see
|
`--csx` |
Generates the same C# script (.csx) templates used by version 1.x and in the portal editor. |
, `--language` `-l` |
Reguired only in version 1.x. In all other versions, the language is defined by the `--worker-runtime` value passed to `func init` . |
, `--name` `-n` |
The function name. |
, `--template` `-t` |
Use the `func templates list` command to see the complete list of available templates for each supported language. |

To learn more, see [Create a function](functions-run-local#create-func).

`func pack`


Creates a deployment package that contains your project code in a runnable state. Use this method when you need to manually create a deployment package for your app on your local computer outside of the `func azure functionapp publish`

command. By default, `func pack`

builds your project when required.

```
func pack
```


Run `func pack`

in the directory that contains your `host.json`

project file, which is the root directory of your app. The generated output (.zip) file has the same name as the folder you're packaging. If a .zip file with that name already exists, it's first deleted and then replaced with an updated version.

By default, `func pack`

builds and packages the Functions project in the directory in which it runs. You can run `func pack`

to package a different directory by setting the path to the project root after the command, like `func pack ./myprojectroot`

. When the directory against which `func pack`

runs doesn't contain a `host.json`

file, an error is returned.

By default, `func pack`

builds all projects and installs dependencies for all languages. Use the `--no-build`

and `--skip-install`

options to modify this behavior.

Important

Python app packages built on a Windows computer often have issues being deployed to and running on Linux in Azure Functions. Consider using `--no-build`

with a remote build or `--build-native-deps`

when running `func pack`

for a Python app on Windows.

The `func pack`

action supports these options:

| Option | Description |
|---|---|
`--output` |
Sets a path to the location in which the deployment .zip package file is created. |
`--no-build` |
Project isn't built before packing. For C# apps, use only when you've already generated your binaries. For Node.js apps, both `npm install` and `npm run build` are skipped. You can use this option when requesting a remote build on the package contents. |
`--skip-install` |
Skips running `npm install` when packing Node.js-based function app. Use this option to avoid overwriting custom npm modules. |
`--build-native-deps` |
Installs Python dependencies locally by using an image that matches the environment used in Azure, which requires Docker tools. When enabled, Core Tools starts a Docker container, builds the app inside that container, and creates a .zip file with all dependencies restored in `.python_packages` . Use this option when running on Windows as a way to avoid potential library issues when deployed to Linux in Azure. |

`func run`


*Version 1.x only.*

Use this command to invoke a function directly. This command works like running a function by using the **Test** tab in the Azure portal. This command works only in version 1.x. For later versions, use `func start`

and [call the function endpoint directly](functions-run-local#run-a-local-function).

```
func run
```


The `func run`

command supports the following options:

| Option | Description |
|---|---|
`--content` |
Inline content passed to the function. |
`--debug` |
Attach a debugger to the host process before running the function. |
`--file` |
The file name to use as content. |
`--no-interactive` |
Doesn't prompt for input, which is useful for automation scenarios. |
`--timeout` |
Time to wait (in seconds) until the local Functions host is ready. |

For example, to call an HTTP-triggered function and pass content body, run the following command:

```
func run MyHttpTrigger --content '{\"name\": \"Azure\"}'
```


`func start`


Starts the local runtime host and loads the function project in the current folder.

The specific command depends on the [runtime version](functions-versions).

```
func start
```


`func start`

supports the following options:

| Option | Description |
|---|---|
`--cert` |
The path to a .pfx file that contains a private key. Only supported with `--useHttps` . |
`--cors` |
A comma-separated list of CORS origins, with no spaces. |
`--cors-credentials` |
Allow cross-origin authenticated requests using cookies and the Authentication header. |
`--dotnet-isolated-debug` |
When set to `true` , pauses the .NET worker process until a debugger is attached from the .NET isolated project being debugged. |
`--enable-json-output` |
Emits console logs as JSON, when possible. |
`--enableAuth` |
Enable full authentication handling pipeline, with authorization requirements. |
`--functions` |
A space-separated list of functions to load. |
`--language-worker` |
Arguments to configure the language worker. For example, you can enable debugging for language worker by providing
|

`--no-build`

`false`

.`--password`

`--cert`

.`--port`

`--timeout`

`--useHttps`

`https://localhost:{port}`

rather than to `http://localhost:{port}`

. By default, this option creates a trusted certificate on your computer.With the project running, you can [verify individual function endpoints](functions-run-local#run-a-local-function).

`func azure functionapp`

global options

All `func azure functionapp`

commands support these options:

| Option | Description |
|---|---|
`--slot` |
Target a specific named
|

`--access-token`

`--access-token-stdin `

[.](/en-us/cli/azure/account#az-account-get-access-token)`az account get-access-token`

`--management-url`

`https://management.azure.com`

. Use this option when your function app runs in a sovereign cloud.`--subscription`

`func azure functionapp fetch-app-settings`


Gets settings from a specific function app.

```
func azure functionapp fetch-app-settings <APP_NAME>
```


For more information, see [Download application settings](functions-run-local#download-application-settings).

The command downloads settings into the `local.settings.json`

file for the project. The command masks values on the screen for security. You can protect settings in the `local.settings.json`

file by [enabling local encryption](functions-run-local#encrypt-the-local-settings-file).

`func azure functionapp list-functions`


Returns a list of the functions in the specified function app.

```
func azure functionapp list-functions <APP_NAME>
```


| Option | Description |
|---|---|
`--show-keys` |
The function endpoint URLs that are returned include function-level access key values. |

`func azure functionapp logstream`


Connects the local command prompt to streaming logs for the function app in Azure.

```
func azure functionapp logstream <APP_NAME>
```


The default timeout for the connection is two hours. You can change the timeout by adding an app setting named [SCM_LOGSTREAM_TIMEOUT](functions-app-settings#scm_logstream_timeout), with a timeout value in seconds. This feature isn't yet supported for Linux in a [Flex Consumption](flex-consumption-plan) or [Consumption](consumption-plan) plan. For these apps, use the `--browser`

option to view logs in the portal.

The `deploy`

action supports the following options:

| Option | Description |
|---|---|
`--browser` |
Open Azure Application Insights Live Stream for the function app in the default browser. |

For more information, see [Enable streaming execution logs in Azure Functions](streaming-logs).

`func azure functionapp publish`


Deploys a Functions project to an existing function app resource in Azure.

```
func azure functionapp publish <APP_NAME>
```


For more information, see [Deploy project files](functions-run-local#project-file-deployment).

The following publish options apply, based on version:

| Option | Description |
|---|---|
`--additional-packages` |
List of packages to install when building native dependencies. For example: `python3-dev libevent-dev` . |
, `--build` `-b` |
Performs build action when deploying to a Linux function app. Accepts: `remote` and `local` . |
`--build-native-deps` |
Skips generating the `.wheels` folder when publishing Python function apps. |
`--csx` |
Publish a C# script (.csx) project. |
`--dotnet-cli-params` |
When publishing compiled C# (.csproj) functions, the core tools calls `dotnet build --output bin/publish` . Any parameters passed to this are appended to the command line. |
`--force` |
Ignore prepublishing verification in certain scenarios. |
`--list-ignored-files` |
Displays a list of files that are ignored during publishing, which is based on the `.funcignore` file. |
`--list-included-files` |
Displays a list of files that are published, which is based on the `.funcignore` file. |
`--no-build` |
Project isn't built during publishing. For Python, `pip install` isn't performed. |
`--nozip` |
Turns the default `Run-From-Package` mode off. |
`--overwrite-settings -y` |
Suppress the prompt to overwrite app settings when `--publish-local-settings -i` is used. |
`--publish-local-settings -i` |
Publish settings in local.settings.json to Azure, prompting to overwrite if the setting already exists. If you're using a
|

**,**`--publish-settings-only`

`-o`

`func azure storage fetch-connection-string`


Gets the connection string for the specified Azure Storage account.

```
func azure storage fetch-connection-string <STORAGE_ACCOUNT_NAME>
```


For more information, see [Download a storage connection string](functions-run-local#download-a-storage-connection-string).

`func azurecontainerapps deploy`


Deploys a containerized function app to an Azure Container Apps environment. Both the storage account used by the function app and the environment must already exist. For more information, see [Azure Container Apps hosting of Azure Functions](functions-container-apps-hosting).

```
func azurecontainerapps deploy --name <APP_NAME> --environment <ENVIRONMENT_NAME> --storage-account <STORAGE_CONNECTION> --resource-group <RESOURCE_GROUP> --image-name <IMAGE_NAME> --registry-server <REGISTRY_SERVER> --registry-username <USERNAME> --registry-password <PASSWORD>
```


The following deployment options apply:

| Option | Description |
|---|---|
`--environment` |
The name of an existing Container Apps environment. |
`--image-build` |
When set to `true` , skips the local Docker build. |
`--image-name` |
The image name of an existing container in a container registry. The image name includes the tag name. |
`--location ` |
Region for the deployment. Ideally, this region is the same region as the environment and storage account resources. |
`--name` |
The name used for the function app deployment in the Container Apps environment. This same name is also used when managing the function app in the portal. The name should be unique in the environment. |
`--registry` |
When set, a Docker build runs and the image is pushed to the registry set in `--registry` . You can't use `--registry` with `--image-name` . For Docker Hub, also use `--registry-username` . |
`--registry-password` |
The password or token used to retrieve the image from a private registry. |
`--registry-username` |
The username used to retrieve the image from a private registry. |
`--resource-group` |
The resource group in which to create the functions-related resources. |
`--storage-account` |
The connection string for the storage account to be used by the function app. |
`--worker-runtime` |
Sets the runtime language of the function app. This parameter is only used with `--image-name` and `--image-build` . Otherwise, the language is determined during the local build. Supported values are: `dotnet` , `dotnetIsolated` , `node` , `python` , `powershell` , and `custom` (for customer handlers). |

Important

Storage connection strings and other service credentials are important secrets. Make sure to securely store any script files that use `func azurecontainerapps deploy`

and don't store them in any publicly accessible source control.

`func deploy`


The `func deploy`

command is deprecated. Instead, use [ func kubernetes deploy](#func-kubernetes-deploy).

`func durable delete-task-hub`


Deletes all storage artifacts in the Durable Functions task hub.

```
func durable delete-task-hub
```


The `delete-task-hub`

action supports the following options:

| Option | Description |
|---|---|
`--connection-string-setting` |
Optional name of the setting containing the storage connection string to use. |
`--task-hub-name` |
Optional name of the Durable Task Hub to use. |

For more information, see the [Durable Functions documentation](durable/durable-functions-instance-management#delete-a-task-hub).

`func durable get-history`


Returns the history of the specified orchestration instance.

```
func durable get-history --id <INSTANCE_ID>
```


The `get-history`

action supports the following options:

| Option | Description |
|---|---|
`--id` |
Specifies the ID of an orchestration instance (required). |
`--connection-string-setting` |
Optional name of the setting containing the storage connection string to use. |
`--task-hub-name` |
Optional name of the Durable Task Hub to use. |

For more information, see the [Durable Functions documentation](durable/durable-functions-instance-management#azure-functions-core-tools-1).

`func durable get-instances`


Returns the status of all orchestration instances. Supports paging by using the `top`

parameter.

```
func durable get-instances
```


The `get-instances`

action supports the following options:

| Option | Description |
|---|---|
`--continuation-token` |
Optional token that indicates a specific page or section of the requests to return. |
`--connection-string-setting` |
Optional name of the app setting that contains the storage connection string to use. |
`--created-after` |
Optionally, get the instances created after this date and time (UTC). All ISO 8601 formatted datetimes are accepted. |
`--created-before` |
Optionally, get the instances created before a specific date and time (UTC). All ISO 8601 formatted datetimes are accepted. |
`--runtime-status` |
Optionally, get the instances whose status match a specific status, including `running` , `completed` , and `failed` . You can provide one or more space-separated statuses. |
`--top` |
Optionally limit the number of records returned in a given request. |
`--task-hub-name` |
Optional name of the Durable Functions task hub to use. |

For more information, see the [Durable Functions documentation](durable/durable-functions-instance-management#azure-functions-core-tools-2).

`func durable get-runtime-status`


Returns the status of the specified orchestration instance.

```
func durable get-runtime-status --id <INSTANCE_ID>
```


The `get-runtime-status`

action supports the following options:

| Option | Description |
|---|---|
`--connection-string-setting` |
Optional name of the setting containing the storage connection string to use. |
`--id` |
Specifies the ID of an orchestration instance (required). |
`--show-input` |
When set, the response contains the input of the function. |
`--show-output` |
When set, the response contains the execution history. |
`--task-hub-name` |
Optional name of the Durable Functions task hub to use. |

For more information, see the [Durable Functions documentation](durable/durable-functions-instance-management#azure-functions-core-tools-1).

`func durable purge-history`


Purge orchestration instance state, history, and blob storage for orchestrations older than the specified threshold.

```
func durable purge-history
```


The `purge-history`

action supports the following options:

| Option | Description |
|---|---|
`--connection-string-setting` |
Optional name of the setting containing the storage connection string to use. |
`--created-after` |
Optionally delete the history of instances created after this date/time (UTC). All ISO 8601 formatted datetime values are accepted. |
`--created-before` |
Optionally delete the history of instances created before this date/time (UTC). All ISO 8601 formatted datetime values are accepted. |
`--runtime-status` |
Optionally delete the history of instances whose status match a specific status, including `completed` , `terminated` , `canceled` , and `failed` . You can provide one or more space-separated statuses. If you don't include `--runtime-status` , instance history is deleted regardless of status. |
`--task-hub-name` |
Optional name of the Durable Functions task hub to use. |

To learn more, see the [Durable Functions documentation](durable/durable-functions-instance-management#azure-functions-core-tools-7).

`func durable raise-event`


Raises an event to the specified orchestration instance.

```
func durable raise-event --event-name <EVENT_NAME> --event-data <DATA>
```


The `raise-event`

action supports the following options:

| Option | Description |
|---|---|
`--connection-string-setting` |
Optional name of the setting containing the storage connection string to use. |
`--event-data` |
Data to pass to the event, either inline or from a JSON file (required). For files, prefix the path to the file with an ampersand (`@` ), such as `@path/to/file.json` . |
`--event-name` |
Name of the event to raise (required). |
`--id` |
Specifies the ID of an orchestration instance (required). |
`--task-hub-name` |
Optional name of the Durable Functions task hub to use. |

For more information, see the [Durable Functions documentation](durable/durable-functions-instance-management#azure-functions-core-tools-5).

`func durable rewind`


Rewinds the specified orchestration instance.

```
func durable rewind --id <INSTANCE_ID> --reason <REASON>
```


The `rewind`

action supports the following options:

| Option | Description |
|---|---|
`--connection-string-setting` |
Optional name of the setting containing the storage connection string to use. |
`--id` |
Specifies the ID of an orchestration instance (required). |
`--reason` |
Reason for rewinding the orchestration (required). |
`--task-hub-name` |
Optional name of the Durable Functions task hub to use. |

For more information, see the [Durable Functions documentation](durable/durable-functions-instance-management#azure-functions-core-tools-6).

`func durable start-new`


Starts a new instance of the specified orchestrator function.

```
func durable start-new --id <INSTANCE_ID> --function-name <FUNCTION_NAME> --input <INPUT>
```


The `start-new`

action supports the following options:

| Option | Description |
|---|---|
`--connection-string-setting` |
Optional name of the setting containing the storage connection string to use. |
`--function-name` |
Name of the orchestrator function to start (required). |
`--id` |
Specifies the ID of an orchestration instance (required). |
`--input` |
Input to the orchestrator function, either inline or from a JSON file (required). For files, prefix the path to the file with an ampersand (`@` ), such as `@path/to/file.json` . |
`--task-hub-name` |
Optional name of the Durable Functions task hub to use. |

For more information, see the [Durable Functions documentation](durable/durable-functions-instance-management#azure-functions-core-tools).

`func durable terminate`


Stops the specified orchestration instance.

```
func durable terminate --id <INSTANCE_ID> --reason <REASON>
```


The `terminate`

action supports the following options:

| Option | Description |
|---|---|
`--connection-string-setting` |
Optional name of the setting containing the storage connection string to use. |
`--id` |
Specifies the ID of an orchestration instance (required). |
`--reason` |
Reason for stopping the orchestration (required). |
`--task-hub-name` |
Optional name of the Durable Functions task hub to use. |

For more information, see the [Durable Functions documentation](durable/durable-functions-instance-management#azure-functions-core-tools-4).

`func extensions install`


Manually installs Functions extensions in a non-.NET project or in a C# script project.

```
func extensions install --package Microsoft.Azure.WebJobs.Extensions.<EXTENSION> --version <VERSION>
```


The `install`

action supports the following options:

| Option | Description |
|---|---|
`--configPath` |
Path of the directory containing extensions.csproj file. |
`--csx` |
Supports C# scripting (.csx) projects. |
`--force` |
Update the versions of existing extensions. |
`--output` |
Output path for the extensions. |
`--package` |
Identifier for a specific extension package. When not specified, all referenced extensions are installed, as with `func extensions sync` . |
`--source` |
NuGet feed source when not using NuGet.org. |
`--version` |
Extension package version. |

The following example installs version 5.0.1 of the Event Hubs extension in the local project:

```
func extensions install --package Microsoft.Azure.WebJobs.Extensions.EventHubs --version 5.0.1
```


The following considerations apply when using `func extensions install`

:

For compiled C# projects (both in-process and isolated worker process), instead use standard NuGet package installation methods, such as

`dotnet add package`

.To manually install extensions by using Core Tools, you must have the

[.NET SDK](https://dotnet.microsoft.com/download)installed.When possible, use

[extension bundles](extension-bundles). The following are some reasons why you might need to install extensions manually:- You need to access a specific version of an extension that's not available in a bundle.
- You need to access a custom extension that's not available in a bundle.
- You need to access a specific combination of extensions that's not available in a single bundle.

Before you can manually install extensions, you must first remove the

object from the host.json file that defines the bundle. No action is taken when an extension bundle is already set in your`extensionBundle`

[host.json file](functions-host-json#extensionbundle).The first time you explicitly install an extension, a .NET project file named extensions.csproj is added to the root of your app project. This file defines the set of NuGet packages required by your functions. While you can work with the

[NuGet package references](/en-us/nuget/consume-packages/package-references-in-project-files)in this file, Core Tools lets you install extensions without having to manually edit this C# project file.

`func extensions sync`


Installs all extensions you add to the function app.

The `sync`

action supports the following options:

| Option | Description |
|---|---|
`--configPath` |
Path of the directory containing extensions.csproj file. |
`--csx` |
Supports C# scripting (.csx) projects. |
`--output` |
Output path for the extensions. |

Regenerates a missing extensions.csproj file. If you define an extension bundle in your host.json file, no action is taken.

`func kubernetes deploy`


Deploys a Functions project as a custom Docker container to a Kubernetes cluster.

```
func kubernetes deploy
```


This command builds your project as a custom container and publishes it to a Kubernetes cluster. Custom containers must have a Dockerfile. To create an app with a Dockerfile, use the `--dockerfile`

option with the [ func init](#func-init) command.

The following Kubernetes deployment options are available:

| Option | Description |
|---|---|
`--dry-run` |
Optionally displays the deployment template, without execution. |
`--config-map-name` |
Optional name of an existing config map with
`--use-config-map` . The default behavior is to create settings based on the `Values` object in the
|

`--cooldown-period`

`--ignore-errors`

`--image-name`

`--keda-version`

`v1`

and `v2`

(default).`--keys-secret-name`

[access keys](function-keys-how-to).`--max-replicas`

`--min-replicas`

`--mount-funckeys-as-containervolume`

[access keys](function-keys-how-to)as a container volume.`--name`

`--namespace`

`--no-docker`

`--registry`

`--registry`

with `--image-name`

. For Docker, use your username.`--polling-interval`

`--pull-secret`

`--secret-name`

[function app settings](functions-how-to-use-azure-function-app-settings#settings)to use in the deployment. The default behavior is to create settings based on the`Values`

object in the [local.settings.json file](functions-develop-local#local-settings-file).`--show-service-fqdn`

`--service-type`

`ClusterIP`

, `NodePort`

, and `LoadBalancer`

(default).`--use-config-map`

`ConfigMap`

object (v1) instead of a `Secret`

object (v1) to configure [function app settings](functions-how-to-use-azure-function-app-settings#settings). The map name is set using`--config-map-name`

.Core Tools uses the local Docker CLI to build and publish the image. Make sure your Docker is already installed locally. Run the `docker login`

command to connect to your account.

Azure Functions supports hosting your containerized functions either in Azure Container Apps or in Azure Functions. Running your containers directly in a Kubernetes cluster or in Azure Kubernetes Service (AKS) isn't officially supported by Azure Functions. To learn more, see [Linux container support in Azure Functions](container-concepts).

`func kubernetes install`


Installs KEDA in a Kubernetes cluster.

```
func kubernetes install
```


Installs KEDA to the cluster defined in the kubectl config file.

The `install`

action supports the following options:

| Option | Description |
|---|---|
`--dry-run` |
Displays the deployment template, without execution. |
`--keda-version` |
Sets the version of KEDA to install. Valid options are: `v1` and `v2` (default). |
`--namespace` |
Supports installation to a specific Kubernetes namespace. When not set, the default namespace is used. |

For more information, see [Managing KEDA and functions in Kubernetes](functions-kubernetes-keda#managing-keda-and-functions-in-kubernetes).

`func kubernetes remove`


Removes KEDA from the Kubernetes cluster defined in the kubectl config file.

```
func kubernetes remove
```


Removes KEDA from the cluster defined in the kubectl config file.

The `remove`

action supports the following options:

| Option | Description |
|---|---|
`--namespace` |
Supports uninstall from a specific Kubernetes namespace. When not set, the default namespace is used. |

To learn more, see [Uninstalling KEDA from Kubernetes](functions-kubernetes-keda#uninstalling-keda-from-kubernetes).

`func settings add`


Adds a new setting to the `Values`

collection in the [local.settings.json file](functions-develop-local#local-settings-file).

```
func settings add <SETTING_NAME> <VALUE>
```


Replace `<SETTING_NAME>`

with the name of the app setting and `<VALUE>`

with the value of the setting.

The `add`

action supports the following option:

| Option | Description |
|---|---|
`--connectionString` |
Adds the name-value pair to the `ConnectionStrings` collection instead of the `Values` collection. Only use the `ConnectionStrings` collection when required by certain frameworks. To learn more, see
|

`func settings decrypt`


Decrypts previously encrypted values in the `Values`

collection in the [local.settings.json file](functions-develop-local#local-settings-file).

```
func settings decrypt
```


The command also decrypts connection string values in the `ConnectionStrings`

collection. In local.settings.json, the command sets `IsEncrypted`

to `false`

. Encrypt local settings to reduce the risk of leaking valuable information from local.settings.json. In Azure, application settings are always stored encrypted.

`func settings delete`


Removes an existing setting from the `Values`

collection in the [local.settings.json file](functions-develop-local#local-settings-file).

```
func settings delete <SETTING_NAME>
```


Replace `<SETTING_NAME>`

with the name of the app setting and `<VALUE>`

with the value of the setting.

The `delete`

action supports the following option:

| Option | Description |
|---|---|
`--connectionString` |
Removes the name-value pair from the `ConnectionStrings` collection instead of from the `Values` collection. |

`func settings encrypt`


Encrypts the values of individual items in the `Values`

collection in the [local.settings.json file](functions-develop-local#local-settings-file).

```
func settings encrypt
```


The command also encrypts connection string values in the `ConnectionStrings`

collection. In local.settings.json, the command sets `IsEncrypted`

to `true`

, which specifies that the local runtime decrypts settings before using them. Encrypt local settings to reduce the risk of leaking valuable information from local.settings.json. In Azure, application settings are always stored encrypted.

`func settings list`


Outputs a list of settings in the `Values`

collection in the [local.settings.json file](functions-develop-local#local-settings-file).

```
func settings list
```


Connection strings from the `ConnectionStrings`

collection are also output. By default, values are masked for security. Use the `--showValue`

option to display the actual value.

The `list`

action supports the following option:

| Option | Description |
|---|---|
`--showValue` |
Shows the actual unmasked values in the output. |

`func templates list`


Lists the available function (trigger) templates.

The `list`

action supports the following option:

| Option | Description |
|---|---|
`--language` |
Language for which to filter returned templates. Default is to return all languages. |
