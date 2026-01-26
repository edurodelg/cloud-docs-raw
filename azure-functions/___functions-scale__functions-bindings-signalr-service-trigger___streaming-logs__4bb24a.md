---
merged_at: 2026-01-26T21:02:36.337567
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-scale__functions-bindings-signalr-service-trigger___streaming-logs_fu_fd3a92.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-scale.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-scale -->

# Azure Functions hosting options

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create a function app in Azure, you must choose a hosting option for your app. Azure provides you with these hosting options for your function code:

| Hosting option | Service | Availability | Container support |
|---|---|---|---|
|
Azure Functions | Generally available (GA) | None |
|
Azure Functions | GA | Linux |
|
Azure Functions | GA | Linux |
|
Azure Container Apps | GA | Linux |
|
Azure Functions | Windows - GA Linux - Retired |
None |

Important

After 30 September 2028, the option to host your function app on Linux in a Consumption plan is retired. To avoid disruptions, migrate your existing Consumption plan apps that run on Linux to the [Flex Consumption plan](flex-consumption-plan) before that date. Apps running on Windows in a Consumption plan aren't affected by this change.
For more information, see the [Linux Consumption plan retirement notice](https://go.microsoft.com/fwlink/?linkid=2335809).

The Azure App Service infrastructure on both Linux and Windows virtual machines facilitates the Azure Functions hosting options. The hosting option you choose dictates the following behaviors:

- How your function app is scaled.
- The resources available to each function app instance.
- Support for advanced functionality, such as Azure Virtual Network connectivity.
- Support for Linux containers.

The plan you choose also impacts the costs for running your function code. For more information, see [Billing](#billing).

This article provides a detailed comparison between the various hosting options. To learn more about running and managing your function code in Linux containers, see [Linux container support in Azure Functions](container-concepts).

## Overview of plans

The following table summarizes the benefits of the various options for Azure functions hosting.

| Option | Benefits |
|---|---|
|
Experience fast horizontal scaling, with flexible compute options, virtual network integration, and serverless pay-as-you-go billing. In the Flex Consumption plan, function instances dynamically scale out (up to 1,000) based on configured per-instance concurrency, incoming events, and per-function workloads for optimal efficiency. Consider the Flex Consumption plan when: ✔ You need a serverless host for your function code, paying only for on-demand executions. ✔ You require virtual network connectivity for secure access to Azure resources. ✔ Your workloads are variable and can go from no activity to demanding rapid, event-driven scaling. ✔ You want to customize compute with memory sizes (512 MB, 2,048 MB, or 4,096 MB) and reduce cold starts via one or more pre-provisioned (always-ready) instances. |
|
Automatically scales based on demand using prewarmed workers, which run applications with no delay after being idle, runs on more powerful instances, and connects to virtual networks. Consider the Azure Functions Premium plan in the following situations: ✔ Your function apps run continuously, or nearly continuously. ✔ You want more control of your instances and want to deploy multiple function apps on the same plan with event-driven scaling. ✔ You have a high number of small executions and a high execution bill, but low GB seconds in the Consumption plan. ✔ You need more CPU or memory options than are provided by consumption plans. ✔ Your code needs to run longer than the maximum execution time allowed on the Consumption plan. ✔ You require virtual network connectivity for secure access to Azure resources. ✔ You want to provide a custom Linux image in which to run your functions. |
|
Run your functions within an App Service plan at regular
Best for long-running scenarios where
✔ You have existing and underutilized virtual machines that are already running other App Service instances. ✔ You must have fully predictable billing, or you need to manually scale instances. ✔ You want to run multiple web apps and function apps on the same plan ✔ You need access to larger compute size choices. ✔ Full compute isolation and secure network access provided by an App Service Environment (ASE). ✔ Very high memory usage and high scale (ASE). |

[Container Apps](../container-apps/functions-overview)Use the Azure Functions programming model to build event-driven, serverless, cloud native function apps. Run your functions alongside other microservices, APIs, websites, and workflows as container-hosted programs. Consider hosting your functions on Container Apps in the following situations:

✔ You want control of the container image and want to package custom libraries with your function code to support line-of-business apps.

✔ You need to migrate code execution from on-premises or legacy apps to cloud native microservices running in containers.

✔ When you want to avoid the overhead and complexity of managing Kubernetes clusters and dedicated compute.

✔ Your functions need high-end processing power provided by dedicated GPU compute resources.

[Consumption plan](consumption-plan)On the Consumption plan, function instances are dynamically added and removed based on the number of incoming events.

Consider the Consumption plan when:

✔ You have a dependency on Windows. For example, using the v1 runtime, the full .NET Framework, or Windows-specific features like certain PowerShell modules.

✔ You want a serverless billing model and pay only when your functions are running.

The remaining tables in this article compare hosting options based on various features and behaviors.

## Operating system support

This table shows operating system support for the hosting options.

| Hosting | Linux1 deployment |
Windows2 deployment |
|---|---|---|
|
✅ Code-only ❌ Container (not supported) |
❌ Not supported |
|
✅ Code-only ✅ Container |
✅ Code-only |
|
✅ Code-only ✅ Container |
✅ Code-only |
|
✅ Container-only | ❌ Not supported |
3 |
✅ Code-only (Retired) ❌ Container (not supported) |
✅ Code-only |

- Linux is the only supported operating system for the
[Python runtime stack](functions-reference-python). - Windows deployments are code-only. Azure Functions doesn't currently support Windows containers.
- The ability to run your app on Linux in a Consumption plan will be retired on 30 September 2028. For more information, see
[Consumption plan](consumption-plan).

## Function app timeout duration

The `functionTimeout`

property in the [host.json](functions-host-json#functiontimeout) project file sets the timeout duration for functions in a function app. This property applies specifically to function executions. After the trigger starts function execution, the function needs to return or respond within the timeout duration. When an execution exceeds this duration, a timeout error occurs and the language worker process restarts. For C# apps running in-process, the host process itself restarts. To avoid timeouts and subsequent process restarts, it's important to [write robust functions](functions-best-practices#write-robust-functions). For more information, see [Improve Azure Functions performance and reliability](performance-reliability#make-sure-background-tasks-complete).

The following table shows the default and maximum values (in minutes) for specific plans:

| Plan | Default | Maximum1 |
|---|---|---|
|
30 | Unbounded2 |
|
304 |
Unbounded2 |
|
304 |
Unbounded3 |
|
30 | Unbounded5 |
|
5 | 10 |

- Regardless of the function app timeout setting, 230 seconds is the maximum amount of time that an HTTP triggered function can take to respond to a request. This limit exists because of the
[default idle timeout of Azure Load Balancer](../app-service/faq-availability-performance-application-issues#why-does-my-request-time-out-after-230-seconds). For longer processing times, consider using the[Durable Functions async pattern](durable/durable-functions-overview#async-http)or[defer the actual work and return an immediate response](performance-reliability#avoid-long-running-functions). - There's no maximum execution timeout duration enforced. However, the grace period given to a function execution is 60 minutes
[during scale in](event-driven-scaling#scale-in-behaviors)for the Flex Consumption and Premium plans, and a grace period of 10 minutes is given during platform updates. - Requires the App Service plan be set to
[Always On](/en-us/azure/azure-functions/dedicated-plan#always-on). A grace period of 10 minutes is given during platform updates. - The default timeout for version 1.x of the Functions host runtime is
*unbounded*. - When the
[minimum number of replicas](../container-apps/scale-app#scale-definition)is set to zero, the default timeout depends on the specific triggers used in the app.

These values assume that the Azure Functions host process starts and runs correctly. There's a maximum timeout of 60 seconds for the language-specific worker process to also start. The worker process startup timeout isn't currently configurable.

## Language support

For details on current native language stack support in Functions, see [Supported languages in Azure Functions](supported-languages).

## Scale

The following table compares the scaling behaviors of the various hosting plans.

Maximum instances are given on a per-function app (Consumption) or per-plan (Premium/Dedicated) basis, unless otherwise indicated.

| Plan | Scale out | Max # instances |
|---|---|---|
|
Fast event-driven scaling decisions are calculated on a per-function basis, called
|

1[Premium plan](functions-premium-plan)[Event driven](event-driven-scaling). Scale out automatically, even during periods of high load. Azure Functions infrastructure scales CPU and memory resources by adding more instances of the Functions host, based on the number of events that its functions are triggered on.**Windows:**1006**Linux:**20-1002,6[Dedicated plan](dedicated-plan)3100 (ASE)

[Container Apps](../container-apps/functions-overview)[Event driven](event-driven-scaling). Scale out automatically, even during periods of high load. Azure Functions infrastructure scales CPU and memory resources by adding more instances of the Functions host, based on the number of events that its functions are triggered on.4[Consumption plan](consumption-plan)[Event driven](event-driven-scaling). Automatic scale based on the source of events. Functions infrastructure scales resources by adding more instances of the function host, based on the number of incoming trigger events.**Windows:**200**Linux:**1005- Flex Consumption plan has a regional subscription quota that limits the total memory usage of all instances across a given region. For more information, see
[Regional subscription memory quotas](flex-consumption-plan#regional-subscription-memory-quotas). Flex Consumption plans currently only support Linux. - In some regions, Linux apps on a Premium plan can scale to 100 instances. For more information, see the
[Premium plan article](functions-premium-plan#region-max-scale-out). - For specific limits for the various App Service plan options, see the
[App Service plan limits](../azure-resource-manager/management/azure-subscription-service-limits#azure-app-service-limits). - On Container Apps, the default is 10 instances, but you can set the
[maximum number of replicas](../container-apps/scale-app#scale-definition), which has an overall maximum of 1000. This setting is honored as long as there's enough cores quota available. For more information, see[Quotas for Azure Container Apps](/en-us/azure/container-apps/quotas). When you create your function app from the Azure portal, you're limited to 300 instances. - During scale-out, there's currently a limit of 500 instances per subscription per hour for Linux apps on a Consumption plan.
- For private endpoint restricted http triggers, scaling out is limited to at most 20 instances.

## Cold start behavior

| Plan | Details |
|---|---|
|
Improved cold start even when scaled to zero. Supports
|

[Premium plan](functions-premium-plan)[always ready instances](functions-premium-plan#always-ready-instances)to avoid cold starts by letting you maintain one or more*perpetually warm*instances.[Dedicated plan](dedicated-plan)[Container Apps](../container-apps/functions-overview)[minimum number of replicas](../container-apps/scale-app#scale-definition):• When set to zero: apps can scale to zero when idle and some requests might have more latencies at startup.

• When set to one or more: the host process runs continuously, which means that cold start isn't an issue.

[Consumption plan](consumption-plan)## Service limits

| Resource |
|
|---|

[Premium plan](functions-premium-plan)

[Dedicated plan](dedicated-plan)/

[ASE](../app-service/environment/overview)

[Container Apps](../container-apps/functions-overview)

[Consumption plan](consumption-plan)

[time-out duration](/en-us/azure/azure-functions/functions-scale#timeout)(min)116[time-out duration](/en-us/azure/azure-functions/functions-scale#timeout)(min)99217[App Service limits](/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#azure-app-service-limits)333[ACU](/en-us/azure/virtual-machines/acu)per instance10[varies](/en-us/azure/container-apps/billing)14[varies](/en-us/azure/container-apps/billing)1511181344[App Service plans](/en-us/azure/app-service/overview-hosting-plans)[region](https://azure.microsoft.com/global-infrastructure/regions/)[Deployment slots](/en-us/azure/azure-functions/functions-deployment-slots)per app121157116,788[TSL/SSL support](/en-us/azure/app-service/configure-ssl-bindings)Notes on service limits:

- By default, the time-out for the Functions 1.x runtime in an App Service plan is unbounded.
- Requires the App Service plan be set to
[Always On](/en-us/azure/azure-functions/dedicated-plan#always-on). Pay at standard[rates](https://azure.microsoft.com/pricing/details/app-service/). A grace period of 10 minutes is given for HTTP triggered functions during platform updates but not for other triggers. - These limits are
[set in the host](https://github.com/Azure/azure-functions-host/blob/dev/src/WebJobs.Script.WebHost/web.config). - The actual number of function apps that you can host depends on the activity of the apps, the size of the machine instances, and the corresponding resource utilization.
- The storage limit is the total content size in temporary storage across all apps in the same App Service plan. For Consumption plans on Linux, the storage is currently 1.5 GB.
- Consumption plan uses an Azure Files share for persisted storage. When you provide your own Azure Files share, the specific share size limits depend on the storage account you set for
[WEBSITE_CONTENTAZUREFILECONNECTIONSTRING](/en-us/azure/azure-functions/functions-app-settings#website_contentazurefileconnectionstring). - On Linux, you must
[explicitly mount your own Azure Files share](/en-us/azure/azure-functions/storage-considerations#mount-file-shares). - When your function app is hosted in a
[Consumption plan](/en-us/azure/azure-functions/consumption-plan), only the CNAME option is supported. For function apps in a[Premium plan](/en-us/azure/azure-functions/functions-premium-plan)or an[App Service plan](/en-us/azure/azure-functions/dedicated-plan), you can map a custom domain using either a CNAME or an A record. - There's no maximum execution time-out duration enforced. However, the grace period given to a function execution is 60 minutes
[during scale in](event-driven-scaling#scale-in-behaviors)and 10 minutes during platform updates. - Workers are roles that host customer apps. Workers are available in three fixed sizes: One vCPU/3.5 GB RAM; Two vCPU/7 GB RAM; Four vCPU/14 GB RAM.
- See
[App Service limits](/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#app-service-limits)for details. - Including the production slot.
- There's currently a limit of 5,000 function apps in a given subscription.
- Flex Consumption plan instance sizes are currently defined as 512 MB, 2,048 MB, or 4,096 MB. For more information, see
[Instance memory](/en-us/azure/azure-functions/flex-consumption-plan#instance-sizes). - For details, see
[Scale](functions-scale#scale)in the Hosting comparison article. - When the
[minimum number of replicas](/en-us/azure/container-apps/scale-app#scale-definition)is set to zero, the default time-out depends on the specific triggers used in the app. - When the
[minimum number of replicas](../container-apps/scale-app#scale-definition)is set to one or more.

## Networking features

| Feature |
|
|---|

[Consumption plan](consumption-plan)

[Premium plan](functions-premium-plan)

[Dedicated plan](dedicated-plan)/

[ASE](../app-service/environment/intro)

[Container Apps](../container-apps/functions-overview)

1

[Inbound IP restrictions](functions-networking-options#inbound-networking-features)[Inbound Private Endpoints](functions-networking-options#inbound-networking-features)[Virtual network integration](functions-networking-options#virtual-network-integration)23[Outbound IP restrictions](functions-networking-options#outbound-ip-restrictions)- For more information, see
[Networking in Azure Container Apps environment](../container-apps/networking). - There are special considerations when working with
[virtual network triggers](functions-networking-options#virtual-network-triggers-non-http). - Only the Dedicated/ASE plan supports gateway-required virtual network integration.

## Billing

| Plan | Details |
|---|---|
|
Billing is based on number of executions, the memory of instances when they're actively executing functions, plus the cost of any
|

[Premium plan](functions-premium-plan)[Dedicated plan](dedicated-plan)For an ASE, there's a flat monthly rate that pays for the infrastructure and doesn't change with the size of the environment. There's also a cost per App Service plan vCPU. All apps hosted in an ASE are in the Isolated pricing model. For more information, see the

[ASE overview article](../app-service/environment/overview#pricing).[Container Apps](../container-apps/functions-overview)[Billing in Azure Container Apps](../container-apps/billing).[Consumption plan](consumption-plan)For a direct cost comparison between dynamic hosting plans (Consumption, Flex Consumption, and Premium), see the [Azure Functions pricing page](https://azure.microsoft.com/pricing/details/functions/). For pricing of the various Dedicated plan options, see the [App Service pricing page](https://azure.microsoft.com/pricing/details/app-service). For pricing Container Apps hosting, see [Azure Container Apps pricing](https://azure.microsoft.com/pricing/details/container-apps/).

## Limitations for creating new function apps in an existing resource group

In some cases, when trying to create a new hosting plan for your function app in an existing resource group you might receive one of the following errors:

- The pricing tier isn't allowed in this resource group
- <SKU_name> workers aren't available in resource group <resource_group_name>

These errors can occur when the following conditions are met:

- You create a function app in an existing resource group that has yet to contain another function app or web app. For example, Linux Consumption apps aren't supported in the same resource group as Linux Dedicated or Linux Premium plans.
- Your new function app is created in the same region as the previous app.
- The previous app is in some way incompatible with your new app. This incompatibility can occur between versions, operating systems, or is due to other platform-level features, such as availability zone support.

Function app and web app plans are mapped to different pools of resources when they're created. Different plans require a different set of infrastructure capabilities. When you create an app in a resource group, that resource group is mapped and assigned to a specific pool of resources. If you try to create another plan in that resource group and the mapped pool doesn't have the required resources, the previously mentioned errors occur.

If this situation happens, create your function app and hosting plan in a new resource group instead.


---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-signalr-service-trigger___streaming-logs_functions-idempoten_d87a34.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-signalr-service-trigger.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-signalr-service-trigger -->

# SignalR Service trigger binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the *SignalR* trigger binding to respond to messages sent from Azure SignalR Service. When function is triggered, messages passed to the function is parsed as a json object.

In SignalR Service serverless mode, SignalR Service uses the [Upstream](../azure-signalr/concept-upstream) feature to send messages from client to Function App. And Function App uses SignalR Service trigger binding to handle these messages. The general architecture is shown below:


For information on setup and configuration details, see the [overview](functions-bindings-signalr-service).

## Example

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The following sample shows a C# function that receives a message event from clients and logs the message content.

```
[Function(nameof(OnClientMessage))]
public static void OnClientMessage(
[SignalRTrigger("Hub", "messages", "sendMessage", "content", ConnectionStringSetting = "SignalRConnection")]
SignalRInvocationContext invocationContext, string content, FunctionContext functionContext)
{
var logger = functionContext.GetLogger(nameof(OnClientMessage));
logger.LogInformation("Connection {connectionId} sent a message. Message content: {content}", invocationContext.ConnectionId, content);
}
```


Important

Class based model of SignalR Service bindings in C# isolated worker doesn't optimize how you write SignalR triggers due to the limitation of C# worker model. For more information about class based model, see [Class based model](../azure-signalr/signalr-concept-serverless-development-config#class-based-model).

SignalR trigger isn't currently supported for Java.

Here's binding data in the *function.json* file:

```
{
"type": "signalRTrigger",
"name": "invocation",
"hubName": "hubName1",
"category": "messages",
"event": "SendMessage",
"parameterNames": [
"message"
],
"direction": "in"
}
```


```
app.generic("function1",
{
trigger: { "type": "signalRTrigger", "name": "invocation", "direction": "in", "hubName": "hubName1", "event": "SendMessage", "category": "messages" },
handler: (triggerInput, context) => {
context.log(`Receive ${triggerInput.Arguments[0]} from ${triggerInput.ConnectionId}.`)
}
})
```


Complete PowerShell examples are pending.

Here's the Python code:

```
import logging
import json
import azure.functions as func
def main(invocation) -> None:
invocation_json = json.loads(invocation)
logging.info("Receive {0} from {1}".format(invocation_json['Arguments'][0], invocation_json['ConnectionId']))
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the `SignalRTrigger`

attribute to define the function. C# script instead uses a [function.json configuration file](#configuration).

The following table explains the properties of the `SignalRTrigger`

attribute.

| Attribute property | Description |
|---|---|
HubName |
This value must be set to the name of the SignalR hub for the function to be triggered. |
Category |
This value must be set as the category of messages for the function to be triggered. The category can be one of the following values:
|
Event |
This value must be set as the event of messages for the function to be triggered. For messages category, event is the target in
connections category, only connected and disconnected is used. |
ParameterNames |
(Optional) A list of names that binds to the parameters. |
ConnectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |

## Annotations

There isn't currently a supported Java annotation for a SignalR trigger.

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `SignalRTrigger` . |
direction |
Must be set to `in` . |
name |
Variable name used in function code for trigger invocation context object. |
hubName |
This value must be set to the name of the SignalR hub for the function to be triggered. |
category |
This value must be set as the category of messages for the function to be triggered. The category can be one of the following values:
|
event |
This value must be set as the event of messages for the function to be triggered. For messages category, event is the target in
connections category, only connected and disconnected is used. |
parameterNames |
(Optional) A list of names that binds to the parameters. |
connectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |

See the [Example section](#example) for complete examples.

## Usage

### Managed identity-based connections

For optimal security, your function app should use managed identities when connecting to the Azure SignalR service instead of using a connection string, which contains a shared secret key. For more information, see [Authorize requests to Azure SignalR Service resources with Microsoft Entra managed identities](../azure-signalr/signalr-howto-authorize-managed-identity#azure-signalr-service-bindings-in-azure-functions).

### Payloads

The trigger input type is declared as either `InvocationContext`

or a custom type. If you choose `InvocationContext`

, you get full access to the request content. For a custom type, the runtime tries to parse the JSON request body to set the object properties.

### InvocationContext

`InvocationContext`

contains all the content in the message sent from a SignalR service, which includes the following properties:

| Property | Description |
|---|---|
| Arguments | Available for messages category. Contains arguments in
|
| Error | Available for disconnected event. It can be Empty if the connection closed with no error, or it contains the error messages. |
| Hub | The hub name that the message belongs to. |
| Category | The category of the message. |
| Event | The event of the message. |
| ConnectionId | The connection ID of the client that sends the message. |
| UserId | The user identity of the client that sends the message. |
| Headers | The headers of the request. |
| Query | The query of the request when clients connect to the service. |
| Claims | The claims of the client. |

### Using `ParameterNames`


The property `ParameterNames`

in `SignalRTrigger`

lets you bind arguments of invocation messages to the parameters of functions. You can use the name you defined as part of [binding expressions](functions-bindings-expressions-patterns) in other binding or as parameters in your code. That gives you a more convenient way to access arguments of `InvocationContext`

.

Say you have a JavaScript SignalR client trying to invoke method `broadcast`

in Azure Function with two arguments `message1`

, `message2`

.

```
await connection.invoke("broadcast", message1, message2);
```


After you set `parameterNames`

, the names you defined correspond to the arguments sent on the client side.

```
[SignalRTrigger(parameterNames: new string[] {"arg1, arg2"})]
```


Then, the `arg1`

contains the content of `message1`

, and `arg2`

contains the content of `message2`

.

`ParameterNames`

considerations

For the parameter binding, the order matters. If you're using `ParameterNames`

, the order in `ParameterNames`

matches the order of the arguments you invoke in the client. If you're using attribute `[SignalRParameter]`

in C#, the order of arguments in Azure Function methods matches the order of arguments in clients.

`ParameterNames`

and attribute `[SignalRParameter]`

**cannot** be used at the same time, or you'll get an exception.

### SignalR Service integration

SignalR Service needs a URL to access Function App when you're using SignalR Service trigger binding. The URL should be configured in **Upstream Settings** on the SignalR Service side.


When using SignalR Service trigger, the URL can be simple and formatted as follows:

```
<Function_App_URL>/runtime/webhooks/signalr?code=<API_KEY>
```


The `Function_App_URL`

can be found on Function App's Overview page and the `API_KEY`

is generated by Azure Function. You can get the `API_KEY`

from `signalr_extension`

in the **App keys** blade of Function App.

If you want to use more than one Function App together with one SignalR Service, upstream can also support complex routing rules. Find more details at [Upstream settings](../azure-signalr/concept-upstream).

### Step-by-step sample

You can follow the sample in GitHub to deploy a chat room on Function App with SignalR Service trigger binding and upstream feature: [Bidirectional chat room sample](https://github.com/aspnet/AzureSignalR-samples/tree/master/samples/BidirectionChat)


---

<!-- DOCUMENTO FUSIONADO: __streaming-logs_functions-idempotent_functions-create-maven-eclipse.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _streaming-logs_functions-idempotent.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: streaming-logs.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/streaming-logs -->

# Enable streaming execution logs in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

While developing an application, you often want to see what's being written to the logs in near real time when running in Azure.

There are two ways to view the stream of log files that your function executions generate.

When your function app is [connected to Application Insights](configure-monitoring#enable-application-insights-integration), you can use [Live Metrics Stream](/en-us/azure/azure-monitor/app/live-stream) to view log data and other metrics in near real-time in the Azure portal. Live Metrics stream is *the recommended way to view streaming logs* it supports all plan types and is the method to use when monitoring functions running on multiple-instances. It also uses [sampled data](configure-monitoring#configure-sampling), so it can protect you from producing too much data during times of peak loads.

Important

By default, the Live Metrics stream includes logs from all apps connected to a given Application Insights instance. When you have more than one app sending log data, you should [filter your log stream data](/en-us/azure/azure-monitor/app/live-stream#filter-by-server-instance).

Log streams can be viewed both in the portal and in most local development environments. The way that you enable and view streaming logs depends on your log streaming method, either Live Metrics or built-in.

To view the Live Metrics Stream for your app, select the

**Overview**tab of your function app.When you have Application Insights enabled, you see an

**Application Insights**link under**Configured features**. This link takes you to the Application Insights page for your app.In Application Insights, select

**Live Metrics Stream**.[Sampled log entries](configure-monitoring#configure-sampling)are displayed under**Sample Telemetry**.


---

<!-- DOCUMENTO FUSIONADO: functions-idempotent.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-idempotent -->

# Designing Azure Functions for identical input

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The reality of event-driven and message-based architecture dictates the need to accept identical requests while preserving data integrity and system stability.

To illustrate, consider an elevator call button. As you press the button, it lights up and an elevator is sent to your floor. A few moments later, someone else joins you in the lobby. This person smiles at you and presses the illuminated button a second time. You smile back and chuckle to yourself as you're reminded that the command to call an elevator is idempotent.

Pressing an elevator call button a second, third, or fourth time has no bearing on the final result. When you press the button, regardless of the number of times, the elevator is sent to your floor. Idempotent systems, like the elevator, result in the same outcome no matter how many times identical commands are issued.

When it comes to building applications, consider the following scenarios:

- What happens if your inventory control application tries to delete the same product more than once?
- How does your human resource application behave if there is more than one request to create an employee record for the same person?
- Where does the money go if your banking app gets 100 requests to make the same withdrawal?

There are many contexts where requests to a function may receive identical commands. Some situations include:

- Retry policies sending the same request many times.
- Cached commands replayed to the application.
- Application errors sending multiple identical requests.

To protect data integrity and system health, an idempotent application contains logic that may contain the following behaviors:

- Verifying of the existence of data before trying to execute a delete.
- Checking to see if data already exists before trying to execute a create action.
- Reconciling logic that creates eventual consistency in data.
- Concurrency controls.
- Duplication detection.
- Data freshness validation.
- Guard logic to verify input data.

Ultimately idempotency is achieved by ensuring a given action is possible and is only executed once.


---

<!-- DOCUMENTO FUSIONADO: functions-create-maven-eclipse.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-maven-eclipse -->

# Create your first function with Java and Eclipse

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to create a [serverless](https://azure.microsoft.com/solutions/serverless/) function project with the Eclipse IDE and Apache Maven, test and debug it, then deploy it to Azure Functions.

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Set up your development environment

To develop a functions app with Java and Eclipse, you must have the following installed:

[Java Developer Kit](/en-us/java/openjdk/download#openjdk-17), version 8, 11, 17 or 21. (Java 21 is currently supported only on Linux)[Apache Maven](https://maven.apache.org), version 3.0 or above.[Eclipse](https://www.eclipse.org/downloads/packages/), with Java and Maven support.[Azure CLI](/en-us/cli/azure)

Important

The JAVA_HOME environment variable must be set to the install location of the JDK to complete this quickstart.

It's highly recommended to also install [Azure Functions Core Tools, version 2](functions-run-local#v2), which provide a local environment for running and debugging Azure Functions.

## Create a Functions project

- In Eclipse, select the
**File**menu, then select**New -> Maven Project**. - Accept the defaults in the
**New Maven Project**dialogue and select**Next**. - Find and select the
[azure-functions-archetype](https://mvnrepository.com/artifact/com.microsoft.azure/azure-functions-archetype)and click**Next**. - Be sure to fill in values for all of the fields including
`resourceGroup`

,`appName`

, and`appRegion`

(please use a different appName other than**fabrikam-function-20170920120101928**), and eventually**Finish**.

Maven creates the project files in a new folder with a name of *artifactId*. The generated code in the project is a simple [HTTP triggered](functions-bindings-http-webhook) function that echoes the body of the triggering HTTP request.

## Run functions locally in the IDE

Note

[Azure Functions Core Tools, version 2](functions-run-local#v2) must be installed to run and debug functions locally.

- Right-click on the generated project, then choose
**Run As**and**Maven build**. - In the
**Edit Configuration**dialog, Enter`package`

in the**Goals**, then select**Run**. This will build and package the function code. - Once the build is complete, create another Run configuration as above, using
`azure-functions:run`

as the goal and name. Select**Run**to run the function in the IDE.

Terminate the runtime in the console window when you're done testing your function. Only one function host can be active and running locally at a time.

### Debug the function in Eclipse

In your **Run As** configuration set up in the previous step, change `azure-functions:run`

to `azure-functions:run -DenableDebug`

and run the updated configuration to start the function app in debug mode.

Select the **Run** menu and open **Debug Configurations**. Choose **Remote Java Application** and create a new one. Give your configuration a name and fill in the settings. The port should be consistent with the debug port opened by function host, which by default is `5005`

. After setup, click on `Debug`

to start debugging.

Set breakpoints and inspect objects in your function using the IDE. When finished, stop the debugger and the running function host. Only one function host can be active and running locally at a time.

## Deploy the function to Azure

The deploy process to Azure Functions uses account credentials from the Azure CLI. [Log in with the Azure CLI](/en-us/cli/azure/authenticate-azure-cli) before continuing using your computer's command prompt.

```
az login
```


Deploy your code into a new Function app using the `azure-functions:deploy`

Maven goal in a new **Run As** configuration.

When the deploy is complete, you see the URL you can use to access your Azure function app:

```
[INFO] Successfully deployed Function App with package.
[INFO] Deleting deployment package from Azure Storage...
[INFO] Successfully deleted deployment package fabrikam-function-20170920120101928.20170920143621915.zip
[INFO] Successfully deployed Function App at https://fabrikam-function-20170920120101928.azurewebsites.net
[INFO] ------------------------------------------------------------------------
```


## Next steps

- Review the
[Java Functions developer guide](functions-reference-java)for more information on developing Java functions. - Add additional functions with different triggers to your project using the
`azure-functions:add`

Maven target.


---

<!-- DOCUMENTO FUSIONADO: _functions-identity-based-connections-tutorial_recover-python-functions.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-identity-based-connections-tutorial.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-identity-based-connections-tutorial -->

# Tutorial: Create a function app that connects to Azure services using identities instead of secrets

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This tutorial shows you how to configure a function app using Microsoft Entra identities instead of secrets or connection strings, where possible. Using identities helps you avoid accidentally leaking sensitive secrets and can provide better visibility into how data is accessed. To learn more about identity-based connections, see [configure an identity-based connection](functions-reference#configure-an-identity-based-connection).

While the procedures shown work generally for all languages, this tutorial currently supports C# class library functions on Windows specifically.

In this tutorial, you learn how to:

- Create a function app in Azure using an ARM template
- Enable both system-assigned and user-assigned managed identities on the function app
- Create role assignments that give permissions to other resources
- Move secrets that can't be replaced with identities into Azure Key Vault
- Configure an app to connect to the default host storage using its managed identity

After you complete this tutorial, you should complete the follow-on tutorial that shows how to [use identity-based connections instead of secrets with triggers and bindings](functions-identity-based-connections-tutorial-2).

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Why use identity?

Managing secrets and credentials is a common challenge for teams of all sizes. Secrets need to be secured against theft or accidental disclosure, and they might need to be periodically rotated. Many Azure services allow you to instead use an identity in [Microsoft Entra ID](../active-directory/fundamentals/active-directory-whatis) to authenticate clients and check against permissions, which can be modified and revoked quickly. Doing so allows for greater control over application security with less operational overhead. An identity could be a human user, such as the developer of an application, or a running application in Azure with a [managed identity](../active-directory/managed-identities-azure-resources/overview).

Because some services don't support Microsoft Entra authentication, your applications might still require secrets in certain cases. However, these secrets can be stored in [Azure Key Vault](/en-us/azure/key-vault/general/overview), which helps simplify the management lifecycle for your secrets. Access to a key vault is also controlled with identities.

By understanding how to use identities instead of secrets when you can, and to use Key Vault when you can't, you reduce risk, decrease operational overhead, and generally improve the security posture for your applications.

## Create a function app that uses Key Vault for necessary secrets

Azure Files is an example of a service that doesn't yet support Microsoft Entra authentication for Server Message Block (SMB) file shares. Azure Files is the default file system for Windows deployments on Premium and Consumption plans. While we could [remove Azure Files entirely](storage-considerations#create-an-app-without-azure-files), doing so introduces limitations you might not want. Instead, you move the Azure Files connection string into Azure Key Vault. That way it's centrally managed, with access controlled by the identity.

### Create an Azure Key Vault

First you need a key vault to store secrets in. You configure it to use [Azure role-based access control (RBAC)](../role-based-access-control/overview) for determining who can read secrets from the vault.

In the

[Azure portal](https://portal.azure.com), choose**Create a resource (+)**.On the

**Create a resource**page, select**Security**>**Key Vault**.On the

**Basics**page, use the following table to configure the key vault.Option Suggested value Description **Subscription**Your subscription Subscription under which this new function app is created. [Resource Group](../azure-resource-manager/management/overview)myResourceGroup Name for the new resource group where you create your function app. **Key vault name**Globally unique name Name that identifies your new key vault. The vault name must only contain alphanumeric characters and dashes and can't start with a number. **Pricing Tier**Standard Options for billing. Standard is sufficient for this tutorial. **Region**Preferred region Choose a [region](https://azure.microsoft.com/regions/)near you or near other services that your functions access.Use the default selections for the "Recovery options" sections.

Make a note of the name you used, for use later.

Select

**Next: Access Policy**to navigate to the**Access Policy**tab.Under

**Permission model**, choose**Azure role-based access control**Select

**Review + create**. Review the configuration, and then select**Create**.

### Set up an identity and permissions for the app

In order to use Azure Key Vault, your app needs to have an identity that can be granted permission to read secrets. This app uses a user-assigned identity so that the permissions can be set up before the app is even created. For more information about managed identities for Azure Functions, see [How to use managed identities in Azure Functions](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json).

In the

[Azure portal](https://portal.azure.com), choose**Create a resource (+)**.On the

**Create a resource**page, select**Identity**>**User Assigned Managed Identity**.On the

**Basics**page, use the following table to configure the identity.Option Suggested value Description **Subscription**Your subscription Subscription under which this new function app is created. [Resource Group](../azure-resource-manager/management/overview)myResourceGroup Name for the new resource group where you create your function app. **Region**Preferred region Choose a [region](https://azure.microsoft.com/regions/)near you or near other services that your functions access.**Name**Globally unique name Name that identifies your new user-assigned identity. Select

**Review + create**. Review the configuration, and then select**Create**.When the identity is created, navigate to it in the portal. Select

**Properties**, and make note of the**Resource ID**for use later.Select

**Azure Role Assignments**, and select**Add role assignment (Preview)**.In the

**Add role assignment (Preview)**page, use options as shown in the following table.Option Suggested value Description **Scope**Key Vault Scope is a set of resources that the role assignment applies to. Scope has levels that are inherited at lower levels. For example, if you select a subscription scope, the role assignment applies to all resource groups and resources in the subscription. **Subscription**Your subscription Subscription under which this new function app is created. **Resource**Your key vault The key vault you created earlier. **Role**Key Vault Secrets User A role is a collection of permissions that are being granted. Key Vault Secrets User gives permission for the identity to read secret values from the vault. Select

**Save**. It might take a minute or two for the role to show up when you refresh the role assignments list for the identity.

The identity is now able to read secrets stored in the key vault. Later in the tutorial, you add additional role assignments for different purposes.

### Generate a template for creating a function app

Because the portal experience for creating a function app doesn't interact with Azure Key Vault, you need to generate and edit an Azure Resource Manager template. You can then use this template to create your function app referencing the Azure Files connection string from your key vault.

Important

Don't create the function app until after you edit the ARM template. The Azure Files configuration needs to be set up at app creation time.

In the

[Azure portal](https://portal.azure.com), choose**Create a resource (+)**.On the

**Create a resource**page, select**Compute**>**Function App**.On the

**Basics**page, use the following table to configure the function app.Option Suggested value Description **Subscription**Your subscription Subscription under which this new function app is created. [Resource Group](../azure-resource-manager/management/overview)myResourceGroup Name for the new resource group where you create your function app. **Function App name**Globally unique name Name that identifies your new function app. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

.**Publish**Code Choose to publish code files or a Docker container. **Runtime stack**.NET This tutorial uses .NET. **Region**Preferred region Choose a [region](https://azure.microsoft.com/regions/)near you or near other services that your functions access.Select

**Review + create**. Your app uses the default values on the**Hosting**and**Monitoring**page. Review the default options, which are included in the ARM template that you generate.Instead of creating your function app here, choose

**Download a template for automation**, which is to the right of the**Next**button.In the template page, select

**Deploy**, then in the Custom deployment page, select**Edit template**.

### Edit the template

You now edit the template to store the Azure Files connection string in Key Vault and allow your function app to reference it. Make sure that you have the following values from the earlier sections before proceeding:

- The resource ID of the user-assigned identity
- The name of your key vault

Note

If you were to create a full template for automation, you would want to include definitions for the identity and role assignment resources, with the appropriate `dependsOn`

clauses. This would replace the earlier steps which used the portal. Consult the [Azure Resource Manager guidance](../azure-resource-manager/templates/syntax) and the documentation for each service.

In the editor, find where the

`resources`

array begins. Before the function app definition, add the following section, which puts the Azure Files connection string into Key Vault. Substitute "VAULT_NAME" with the name of your key vault.`{ "type": "Microsoft.KeyVault/vaults/secrets", "apiVersion": "2016-10-01", "name": "VAULT_NAME/azurefilesconnectionstring", "properties": { "value": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName')), '2019-06-01').keys[0].value,';EndpointSuffix=','core.windows.net')]" }, "dependsOn": [ "[concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName'))]" ] },`

In the definition for the function app resource (which has

`type`

set to`Microsoft.Web/sites`

), add`Microsoft.KeyVault/vaults/VAULT_NAME/secrets/azurefilesconnectionstring`

to the`dependsOn`

array. Again, substitute "VAULT_NAME" with the name of your key vault. Doing so prevents your app from being created before the secret is defined. The`dependsOn`

array should look like the following example:`{ "type": "Microsoft.Web/sites", "apiVersion": "2018-11-01", "name": "[parameters('name')]", "location": "[parameters('location')]", "tags": null, "dependsOn": [ "microsoft.insights/components/idcxntut", "Microsoft.KeyVault/vaults/VAULT_NAME/secrets/azurefilesconnectionstring", "[concat('Microsoft.Web/serverfarms/', parameters('hostingPlanName'))]", "[concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName'))]" ], // ... }`

Add the

`identity`

block from the following example into the definition for your function app resource. Substitute "IDENTITY_RESOURCE_ID" for the resource ID of your user-assigned identity.`{ "apiVersion": "2018-11-01", "name": "[parameters('name')]", "type": "Microsoft.Web/sites", "kind": "functionapp", "location": "[parameters('location')]", "identity": { "type": "SystemAssigned,UserAssigned", "userAssignedIdentities": { "IDENTITY_RESOURCE_ID": {} } }, "tags": null, // ... }`

This

`identity`

block also sets up a system-assigned identity, which you use later in this tutorial.Add the

`keyVaultReferenceIdentity`

property to the`properties`

object for the function app, as in the following example. Substitute "IDENTITY_RESOURCE_ID" for the resource ID of your user-assigned identity.`{ // ... "properties": { "name": "[parameters('name')]", "keyVaultReferenceIdentity": "IDENTITY_RESOURCE_ID", // ... } }`

You need this configuration because an app could have multiple user-assigned identities configured. Whenever you want to use a user-assigned identity, you must specify it with an ID. System-assigned identities don't need to be specified this way, because an app can only ever have one. Many features that use managed identity assume they should use the system-assigned one by default.

Find the JSON objects that define the

`WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

application setting, which should look like the following example:`{ "name": "WEBSITE_CONTENTAZUREFILECONNECTIONSTRING", "value": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName')), '2019-06-01').keys[0].value,';EndpointSuffix=','core.windows.net')]" },`

Replace the

`value`

field with a reference to the secret as shown in the following example. Substitute "VAULT_NAME" with the name of your key vault.`{ "name": "WEBSITE_CONTENTAZUREFILECONNECTIONSTRING", "value": "[concat('@Microsoft.KeyVault(SecretUri=', reference(resourceId('Microsoft.KeyVault/vaults/secrets', 'VAULT_NAME', 'azurefilesconnectionstring')).secretUri, ')')]" },`

Select

**Save**to save the updated ARM template.

### Deploy the modified template

Make sure that your create options, including

**Resource Group**, are still correct and select**Review + create**.After your template validates, make a note of your

**Storage Account Name**, since you'll use this account later. Finally, select**Create**to create your Azure resources and deploy your code to the function app.After deployment completes, select

**Go to resource group**and then select the new function app.

Congratulations! You've successfully created your function app to reference the Azure Files connection string from Azure Key Vault.

Whenever your app would need to add a reference to a secret, you would just need to define a new application setting pointing to the value stored in Key Vault. For more information, see [Key Vault references for Azure Functions](../app-service/app-service-key-vault-references?toc=/azure/azure-functions/toc.json).

Tip

The [Application Insights connection string](/en-us/azure/azure-monitor/app/sdk-connection-string) and its included instrumentation key are not considered secrets and can be retrieved from App Insights using [Reader](../role-based-access-control/built-in-roles#reader) permissions. You do not need to move them into an Azure Key Vault instance, although you certainly can. If you choose to use Key Vault, your function app must have a managed identity that can be used to securely retrieve the secret [using a Key Vault reference in the app settings](../app-service/app-service-key-vault-references).

## Use managed identity for AzureWebJobsStorage

Next, you use the system-assigned identity you configured in the previous steps for the `AzureWebJobsStorage`

connection. `AzureWebJobsStorage`

is used by the Functions runtime and by several triggers and bindings to coordinate between multiple running instances. It's required for your function app to operate, and like Azure Files, is configured with a connection string by default when you create a new function app.

### Grant the system-assigned identity access to the storage account

Similar to the steps you previously followed with the user-assigned identity and your key vault, you now create a role assignment granting the system-assigned identity access to your storage account.

In the

[Azure portal](https://portal.azure.com), navigate to the storage account that was created with your function app earlier.Select

**Access Control (IAM)**. This page is where you can view and configure who has access to the resource.Select

**Add**and select**add role assignment**.Search for

**Storage Blob Data Owner**, select it, and select**Next**On the

**Members**tab, under**Assign access to**, choose**Managed Identity**Select

**Select members**to open the**Select managed identities**panel.Confirm that the

**Subscription**is the one in which you created the resources earlier.In the

**Managed identity**selector, choose**Function App**from the**System-assigned managed identity**category. The**Function App**label might have a number in parentheses next to it, indicating the number of apps in the subscription with system-assigned identities.Your app should appear in a list below the input fields. If you don't see it, you can use the

**Select**box to filter the results with your app's name.Select your application. It should move down into the

**Selected members**section. Choose**Select**.On the

**Add role assignment**screen, select**Review + assign**. Review the configuration, and then select**Review + assign**.

Tip

If you intend to use the function app for a blob-triggered function, you will need to repeat these steps for the **Storage Account Contributor** and **Storage Queue Data Contributor** roles over the account used by AzureWebJobsStorage. To learn more, see [Blob trigger identity-based connections](functions-bindings-storage-blob-trigger#identity-based-connections).

### Edit the AzureWebJobsStorage configuration

Next you update your function app to use its system-assigned identity when it uses the blob service for host storage.

Important

The `AzureWebJobsStorage`

configuration is used by some triggers and bindings, and those extensions must be able to use identity-based connections, too. Apps that use blob triggers or event hub triggers may need to update those extensions. Because no functions have been defined for this app, there isn't a concern yet. To learn more about this requirement, see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity).

Similarly, `AzureWebJobsStorage`

is used for deployment artifacts when using server-side build in Linux Consumption. When you enable identity-based connections for `AzureWebJobsStorage`

in Linux Consumption, you will need to deploy via [an external deployment package](run-functions-from-deployment-package).

In the

[Azure portal](https://portal.azure.com), navigate to your function app.In your function app, expand

**Settings**, and then select**Environment variables**.In the

**App settings**tab, select the**AzureWebJobsStorage**app setting, and edit it according to the following table:Option Suggested value Description **Name**AzureWebJobsStorage__accountName Change the name from **AzureWebJobsStorage**to the exact name`AzureWebJobsStorage__accountName`

. This setting instructs the host to use the identity instead of searching for a stored secret. The new setting uses a double underscore (`__`

), which is a special character in application settings.**Value**Your account name Update the name from the connection string to just your **StorageAccountName**.This configuration tells the system to use an identity to connect to the resource.

Select

**Apply**, and then select**Apply**and**Confirm**to save your changes and restart the app function.

You've now removed the storage connection string requirement for AzureWebJobsStorage by configuring your app to instead connect to blobs using managed identities.

Note

The `__accountName`

syntax is unique to the AzureWebJobsStorage connection and cannot be used for other storage connections. To learn to define other connections, check the reference for each trigger and binding your app uses.

## Next steps

This tutorial showed how to create a function app without storing secrets in its configuration.

Advance to the next tutorial to learn how to use identities in trigger and binding connections.


---

<!-- DOCUMENTO FUSIONADO: recover-python-functions.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/recover-python-functions -->

# Troubleshoot Python errors in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides information to help you troubleshoot errors with your Python functions in Azure Functions. This article supports both the v1 and v2 programming models. Choose the model you want to use from the selector at the top of the article.

Note

The Python v2 programming model is only supported in the 4.x functions runtime. For more information, see [Azure Functions runtime versions overview](functions-versions).

Here are the troubleshooting sections for common issues in Python functions:

Specifically with the v2 model, here are some known issues and their workarounds:

General troubleshooting guides for Python Functions include:

## Troubleshoot: ModuleNotFoundError

This section helps you troubleshoot module-related errors in your Python function app. These errors typically result in the following Azure Functions error message:

Exception: ModuleNotFoundError: No module named 'module_name'.


This error occurs when a Python function app fails to load a Python module. The root cause for this error is one of the following issues:

[The package can't be found](#the-package-cant-be-found)[The package isn't resolved with proper Linux wheel](#the-package-isnt-resolved-with-the-proper-linux-wheel)[The package is incompatible with the Python interpreter version](#the-package-is-incompatible-with-the-python-interpreter-version)[The package conflicts with other packages](#the-package-conflicts-with-other-packages)[The package supports only Windows and macOS platforms](#the-package-supports-only-windows-and-macos-platforms)

### View project files

To identify the actual cause of your issue, you need to get the Python project files that run on your function app. If you don't have the project files on your local computer, you can get them in one of the following ways:

- If the function app has a
`WEBSITE_RUN_FROM_PACKAGE`

app setting and its value is a URL, download the file by copying and pasting the URL into your browser. - If the function app has
`WEBSITE_RUN_FROM_PACKAGE`

set to`1`

, go to`https://<app-name>.scm.azurewebsites.net/api/vfs/data/SitePackages`

and download the file from the latest`href`

URL. - If the function app doesn't have either of the preceding app settings, go to
`https://<app-name>.scm.azurewebsites.net/api/settings`

and find the URL under`SCM_RUN_FROM_PACKAGE`

. Download the file by copying and pasting the URL into your browser. - If suggestions resolve the issue, go to
`https://<app-name>.scm.azurewebsites.net/DebugConsole`

and view the content under`/home/site/wwwroot`

.

The rest of this article helps you troubleshoot potential causes of this error by inspecting your function app's content, identifying the root cause, and resolving the specific issue.

### Diagnose ModuleNotFoundError

This section details potential root causes of module-related errors. After you figure out which is the likely root cause, you can go to the related mitigation.

#### The package can't be found

Go to `.python_packages/lib/python3.6/site-packages/<package-name>`

or `.python_packages/lib/site-packages/<package-name>`

. If the file path doesn't exist, this missing path is likely the root cause.

Using third-party or outdated tools during deployment might cause this issue.

To mitigate this issue, see [Enable remote build](#enable-remote-build) or [Build native dependencies](#build-native-dependencies).

#### The package isn't resolved with the proper Linux wheel

Go to `.python_packages/lib/python3.6/site-packages/<package-name>-<version>-dist-info`

or `.python_packages/lib/site-packages/<package-name>-<version>-dist-info`

. Use your favorite text editor to open the *wheel* file and check the **Tag:** section. The issue might be that the tag value doesn't contain **linux**.

Python functions run only on Linux in Azure. The Functions runtime v2.x runs on Debian Stretch, and the v3.x runtime runs on Debian Buster. The artifact is expected to contain the correct Linux binaries. When you use the `--build local`

flag in Core Tools, third-party, or outdated tools, it might cause older binaries to be used.

To mitigate the issue, see [Enable remote build](#enable-remote-build) or [Build native dependencies](#build-native-dependencies).

#### The package is incompatible with the Python interpreter version

Go to `.python_packages/lib/python3.6/site-packages/<package-name>-<version>-dist-info`

or `.python_packages/lib/site-packages/<package-name>-<version>-dist-info`

. In your text editor, open the *METADATA* file and check the **Classifiers:** section. If the section doesn't contain `Python :: 3`

, `Python :: 3.6`

, `Python :: 3.7`

, `Python :: 3.8`

, or `Python :: 3.9`

, the package version is either too old or, more likely, it's already out of maintenance.

You can check the Python version of your function app from the [Azure portal](https://portal.azure.com). Navigate to your function app's **Overview** resource page to find the runtime version. The runtime version supports Python versions as described in the [Azure Functions runtime versions overview](functions-versions).

To mitigate the issue, see [Update your package to the latest version](#update-your-package-to-the-latest-version) or [Replace the package with equivalents](#replace-the-package-with-equivalents).

#### The package conflicts with other packages

If you've verified that the package is resolved correctly with the proper Linux wheels, there might be a conflict with other packages. In certain packages, the PyPi documentation might clarify the incompatible modules. For example, in [ azure 4.0.0](https://pypi.org/project/azure/4.0.0/), you find the following statement:

This package isn't compatible with azure-storage. If you installed azure-storage, or if you installed azure 1.x/2.x and didn’t uninstall azure-storage, you must uninstall azure-storage first.


You can find the documentation for your package version in `https://pypi.org/project/<package-name>/<package-version>`

.

To mitigate the issue, see [Update your package to the latest version](#update-your-package-to-the-latest-version) or [Replace the package with equivalents](#replace-the-package-with-equivalents).

#### The package supports only Windows and macOS platforms

Open the `requirements.txt`

with a text editor and check the package in `https://pypi.org/project/<package-name>`

. Some packages run only on Windows and macOS platforms. For example, pywin32 runs on Windows only.

The `Module Not Found`

error might not occur when you're using Windows or macOS for local development. However, the package fails to import on Azure Functions, which uses Linux at runtime. This issue is likely to be caused by using `pip freeze`

to export the virtual environment into *requirements.txt* from your Windows or macOS machine during project initialization.

To mitigate the issue, see [Replace the package with equivalents](#replace-the-package-with-equivalents) or [Handcraft requirements.txt](#handcraft-requirementstxt).

### Mitigate ModuleNotFoundError

The following are potential mitigations for module-related issues. Use the [previously mentioned diagnoses](#diagnose-modulenotfounderror) to determine which of these mitigations to try.

#### Enable remote build

Make sure that remote build is enabled. The way that you make sure depends on your deployment method.

Make sure that the latest version of the [Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions) is installed. Verify that the *.vscode/settings.json* file exists and it contains the setting `"azureFunctions.scmDoBuildDuringDeployment": true`

. If it doesn't, create the file with the `azureFunctions.scmDoBuildDuringDeployment`

setting enabled, and then redeploy the project.

#### Build native dependencies

Make sure that the latest versions of both Docker and [Azure Functions Core Tools](https://github.com/Azure/azure-functions-core-tools/releases) are installed. Go to your local function project folder, and use `func azure functionapp publish <app-name> --build-native-deps`

for deployment.

#### Update your package to the latest version

In the latest package version of `https://pypi.org/project/<package-name>`

, check the **Classifiers:** section. The package should be `OS Independent`

, or compatible with `POSIX`

or `POSIX :: Linux`

in **Operating System**. Also, the programming language should contain: `Python :: 3`

, `Python :: 3.6`

, `Python :: 3.7`

, `Python :: 3.8`

, or `Python :: 3.9`

.

If these package items are correct, you can update the package to the latest version by changing the line `<package-name>~=<latest-version>`

in *requirements.txt*.

#### Handcraft requirements.txt

Some developers use `pip freeze > requirements.txt`

to generate the list of Python packages for their developing environments. Although this convenience should work in most cases, there can be issues in cross-platform deployment scenarios, such as developing functions locally on Windows or macOS, but publishing to a function app, which runs on Linux. In this scenario, `pip freeze`

can introduce unexpected operating system-specific dependencies or dependencies for your local development environment. These dependencies can break the Python function app when it's running on Linux.

The best practice is to check the import statement from each *.py* file in your project source code and then check in only the modules in the *requirements.txt* file. This practice guarantees that the resolution of packages can be handled properly on different operating systems.

#### Replace the package with equivalents

First, take a look into the latest version of the package in `https://pypi.org/project/<package-name>`

. This package usually has its own GitHub page. Go to the **Issues** section on GitHub and search to see whether your issue has been fixed. If it has been fixed, update the package to the latest version.

Sometimes, the package might have been integrated into [Python Standard Library](https://docs.python.org/3/library/) (such as `pathlib`

). If so, because we provide a certain Python distribution in Azure Functions (Python 3.6, Python 3.7, Python 3.8, and Python 3.9), the package in your *requirements.txt* file should be removed.

However, if you're finding that the issue hasn't been fixed, and you're on a deadline, we encourage you to do some research to find a similar package for your project. Usually, the Python community provides you with a wide variety of similar libraries that you can use.

#### Disable dependency isolation flag

Set the application setting [PYTHON_ISOLATE_WORKER_DEPENDENCIES](functions-app-settings#python_isolate_worker_dependencies) to a value of `0`

.

## Troubleshoot: cannot import 'cygrpc'

This section helps you troubleshoot 'cygrpc'-related errors in your Python function app. These errors typically result in the following Azure Functions error message:

Cannot import name 'cygrpc' from 'grpc._cython'


This error occurs when a Python function app fails to start with a proper Python interpreter. The root cause for this error is one of the following issues:

[The Python interpreter mismatches OS architecture](#the-python-interpreter-mismatches-os-architecture)[The Python interpreter isn't supported by Azure Functions Python Worker](#the-python-interpreter-isnt-supported-by-azure-functions-python-worker)

### Diagnose the 'cygrpc' reference error

There are several possible causes for errors that reference `cygrpc`

, which are detailed in this section.

#### The Python interpreter mismatches OS architecture

This mismatch is most likely caused by a 32-bit Python interpreter being installed on your 64-bit operating system.

If you're running on an x64 operating system, ensure that your Python version 3.6, 3.7, 3.8, or 3.9 interpreter is also on a 64-bit version.

You can check your Python interpreter bitness by running the following commands:

On Windows in PowerShell, run `py -c 'import platform; print(platform.architecture()[0])'`

.

On a Unix-like shell, run `python3 -c 'import platform; print(platform.architecture()[0])'`

.

If there's a mismatch between Python interpreter bitness and the operating system architecture, download a proper Python interpreter from [Python Software Foundation](https://www.python.org/downloads).

#### The Python interpreter isn't supported by Azure Functions Python Worker

The Azure Functions Python Worker supports only [specific Python versions](functions-versions?pivots=programming-language-python#languages).

Check to see whether your Python interpreter matches your expected version by `py --version`

in Windows or `python3 --version`

in Unix-like systems. Ensure that the return result is one of the [supported Python versions](functions-versions?pivots=programming-language-python#languages).

If your Python interpreter version doesn't meet the requirements for Azure Functions, instead download a Python interpreter version that is supported by Functions from the [Python Software Foundation](https://www.python.org/downloads).

## Troubleshoot: python exited with code 137

Code 137 errors are typically caused by out-of-memory issues in your Python function app. As a result, you get the following Azure Functions error message:

Microsoft.Azure.WebJobs.Script.Workers.WorkerProcessExitException : python exited with code 137


This error occurs when a Python function app is forced to terminate by the operating system with a `SIGKILL`

signal. This signal usually indicates an out-of-memory error in your Python process. The Azure Functions platform has a [service limitation](functions-scale#service-limits) that terminates any function apps that exceed this limit.

To analyze the memory bottleneck in your function app, see [Profile Python function app in local development environment](python-memory-profiler-reference#memory-profiling-process).

## Troubleshoot: python exited with code 139

This section helps you troubleshoot segmentation fault errors in your Python function app. These errors typically result in the following Azure Functions error message:

Microsoft.Azure.WebJobs.Script.Workers.WorkerProcessExitException : python exited with code 139


This error occurs when a Python function app is forced to terminate by the operating system with a `SIGSEGV`

signal. This signal indicates violation of the memory segmentation, which can result from an unexpected reading from or writing into a restricted memory region. In the following sections, we provide a list of common root causes.

### A regression from third-party packages

In your function app's *requirements.txt* file, an unpinned package gets upgraded to the latest version during each deployment to Azure. Package updates can potentially introduce regressions that affect your app. To recover from such issues, comment out the import statements, disable the package references, or pin the package to a previous version in *requirements.txt*.

### Unpickling from a malformed .pkl file

If your function app is using the Python pickle library to load a Python object from a *.pkl* file, it's possible that the file contains a malformed bytes string or an invalid address reference. To recover from this issue, try commenting out the `pickle.load()`

function.

### Pyodbc connection collision

If your function app is using the popular ODBC database driver [pyodbc](https://github.com/mkleehammer/pyodbc), it's possible that multiple connections are open within a single function app. To avoid this issue, use the singleton pattern, and ensure that only one pyodbc connection is used across the function app.

## Sync triggers failed

The error `Sync triggers failed`

can be caused by several issues. One potential cause is a conflict between customer-defined dependencies and Python built-in modules when your functions run in an App Service plan. For more information, see [Package management](functions-reference-python#package-management).

## Troubleshoot: could not load file or assembly

You can see this error when you're running locally using the v2 programming model. This error is caused by a known issue to be resolved in an upcoming release.

This is an example message for this error:

DurableTask.Netherite.AzureFunctions: Could not load file or assembly 'Microsoft.Azure.WebJobs.Extensions.DurableTask, Version=2.0.0.0, Culture=neutral, PublicKeyToken=014045d636e89289'.


The system cannot find the file specified.

The error occurs because of an issue with how the extension bundle was cached. To troubleshoot the issue, run this command with `--verbose`

to see more details:

```
func host start --verbose
```


It's likely you're seeing this caching issue when you see an extension loading log like `Loading startup extension <>`

that isn't followed by `Loaded extension <>`

.

To resolve this issue:

Find the

`.azure-functions-core-tools`

path by running:`func GetExtensionBundlePath`

Delete the

`.azure-functions-core-tools`

directory.`rm -r <insert path>/.azure-functions-core-tools`


The cache directory is recreated when you run Core Tools again.

## Troubleshoot: unable to resolve the Azure Storage connection

You might see this error in your local output as the following message:

Microsoft.Azure.WebJobs.Extensions.DurableTask: Unable to resolve the Azure Storage connection named 'Storage'.


Value cannot be null. (Parameter 'provider')

This error is a result of how extensions are loaded from the bundle locally. To resolve this error, take one of the following actions:

Use a storage emulator such as

[Azurite](../storage/common/storage-use-azurite). This option is a good one when you aren't planning to use a storage account in your function application.Create a storage account and add a connection string to the

`AzureWebJobsStorage`

environment variable in the*localsettings.json*file. Use this option when you're using a storage account trigger or binding with your application, or if you have an existing storage account. To get started, see[Create a storage account](../storage/common/storage-account-create).

## Functions not found after deployment

There are several common build issues that can cause Python functions to not be found by the host after an apparently successful deployment:

The agent pool must be running on Ubuntu to guarantee that packages are restored correctly from the build step. Make sure your deployment template requires an Ubuntu environment for build and deployment.

When the function app isn't at the root of the source repo, make sure that the

`pip install`

step references the correct location in which to create the`.python_packages`

folder. Keep in mind that this location is case sensitive, such as in this command example:`pip install --target="./FunctionApp1/.python_packages/lib/site-packages" -r ./FunctionApp1/requirements.txt`

The template must generate a deployment package that can be loaded into

`/home/site/wwwroot`

. In Azure Pipelines, this is done by the`ArchiveFiles`

task.

## Development issues in the Azure portal

When using the [Azure portal](https://portal.azure.com/), take into account these known issues and their workarounds:

- There are general limitations for writing your function code in the portal. For more information, see
[Development limitations in the Azure portal](functions-how-to-use-azure-function-app-settings#development-limitations-in-the-azure-portal).

- To delete a function from a function app in the portal, remove the function code from the file itself. The
**Delete**button doesn't work to remove the function when using the Python v2 programming model.

- When creating a function in the portal, you might be admonished to use a different tool for development. There are several scenarios where you can't edit your code in the portal, including when a syntax error has been detected. In these scenarios, use
[Visual Studio Code](functions-develop-vs-code?pivots=programming-language-python)or[Azure Functions Core Tools](functions-run-local?pivots=programming-language-python)to develop and publish your function code.

## Next steps

If you're unable to resolve your issue, contact the Azure Functions team:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/function-keys-how-to -->

# Work with access keys in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions lets you use secret keys to make it more difficult to access your function endpoints. This article describes the kinds of access keys that Functions supports, and how to work with access keys.

While access keys provide some mitigation against unwanted access, you should consider other options to secure HTTP endpoints in production. For example, it's not a good practice to distribute shared secrets in a public app. If your function is being called from a public client, you should consider implementing these or other security mechanisms:

[Enable App Service Authentication/Authorization](security-concepts#enable-app-service-authenticationauthorization)[Use Azure API Management (APIM) to authenticate requests](security-concepts#use-azure-api-management-apim-to-authenticate-requests)[Deploy your function app to a virtual network](security-concepts#deploy-your-function-app-to-a-virtual-network)[Deploy your function app in isolation](security-concepts#deploy-your-function-app-in-isolation)

Access keys provide the basis for HTTP authorization in HTTP triggered functions. For more information, see [Authorization level](functions-bindings-http-webhook-trigger#http-auth).

## Understand keys

The scope of an access key and the actions it supports depend on the type of access key.

| Key type | Key name | HTTP auth level | Description |
|---|---|---|---|
Function |
`default` or user defined |
`function` |
Allows access only to a specific function endpoint. |
Host |
`default` or user defined |
`function` |
Allows access to all function endpoints in a function app. |
Master |
`_master` |
`admin` |
Special host key that also provides administrative access to the runtime REST APIs in a function app. Because the master key grants elevated permissions in your function app, you shouldn't share this key with third parties or distribute it in native client applications. |
System |
Depends on the extension | n/a | Specific extensions might require a system-managed key to access webhook endpoints. System keys are designed for extension-specific function endpoints that get called by internal components. For example, the
Only specific extensions can create system keys. You can't explicitly set their values. Like other keys, you can generate a new value for the key from the portal or by using the key APIs. |

Each key is named for reference. There's a default key (named `default`

) at the function and host level. Function keys take precedence over host keys. When two keys are defined with the same name, the function key is always used.

The following table compares the uses for various kinds of access keys:

| Action | Scope | Key type |
|---|---|---|
| Execute a function | Specific function | Function |
| Execute a function | Any function | Function or host |
Call an `admin` endpoint |
Function app | Master-only |
| Call Durable Task extension APIs | Function app* |
System |
| Call an extension-specific Webhook (internal) | Function app* |
system |

*Scope determined by the extension.

## Key requirements

In Functions, access keys are randomly generated 32-byte arrays that are encoded as URL-safe base-64 strings. While you can generate your own access keys and use them with Functions, we strongly recommend that you instead allow Functions to generate all of your access keys for you.

Functions-generated access keys include special signature and checksum values that indicate the type of access key and that Azure Functions generated it. Having these extra components in the key itself makes it much easier to determine the source of these kinds of secrets located during security scanning and other automated processes.

To allow Functions to generate your keys for you, don't supply the key `value`

to any of the APIs that you can use to generate keys.

## Manage key storage

Keys are stored as part of your function app in Azure and are encrypted at rest. By default, keys are stored in a Blob storage container in the account provided by the `AzureWebJobsStorage`

setting. You can use the [ AzureWebJobsSecretStorageType](functions-app-settings#azurewebjobssecretstoragetype) setting to override this default behavior and instead store keys in one of these alternate locations:

| Location | Value | Description |
|---|---|---|
| A second storage account | `blob` |
Stores keys in Blob storage in a storage account that's different than the one used by the Functions runtime. The specific account and container used are defined by a shared access signature (SAS) URL set in the
`AzureWebJobsSecretStorageSas` |

`AzureWebJobsSecretStorageSas`

setting when the SAS URL changes.[Azure Key Vault](/en-us/azure/key-vault/general/overview)`keyvault`

[is used to store keys.](functions-app-settings#azurewebjobssecretstoragekeyvaulturi)`AzureWebJobsSecretStorageKeyVaultUri`

`files`

`kubernetes`

[AzureWebJobsKubernetesSecretName](functions-app-settings#azurewebjobskubernetessecretname)is used to store keys. Supported only when your function app is deployed to Kubernetes. The[Azure Functions Core Tools](functions-run-local)generates the values automatically when you use it to deploy your app to a Kubernetes cluster.[Immutable secrets](https://kubernetes.io/docs/concepts/configuration/secret/#secret-immutable)aren't supported.`ContainerApps`

When you use Key Vault for key storage, the app settings you need depend on the managed identity type, either system-assigned or user-assigned.

| Setting name | System-assigned | User-assigned | App registration |
|---|---|---|---|
|

[AzureWebJobsSecretStorageKeyVaultClientId](functions-app-settings#azurewebjobssecretstoragekeyvaultclientid)[AzureWebJobsSecretStorageKeyVaultClientSecret](functions-app-settings#azurewebjobssecretstoragekeyvaultclientsecret)[AzureWebJobsSecretStorageKeyVaultTenantId](functions-app-settings#azurewebjobssecretstoragekeyvaulttenantid)Important

Secrets aren't scoped to individual function apps through the `AzureWebJobsSecretStorageKeyVaultUri`

setting. If multiple function apps are configured to use the same Key Vault they share the same secrets, potentially leading to key collisions or overwrites. To avoid unintended behavior, we recommend that you use a separate Key Vault instance for each function app.

## Use access keys

HTTP triggered functions can generally be called by using a URL that includes the function name. When the authorization level of a given function is set as a value other than `anonymous`

, you must also provide an access key in your request. The access key can either be provided in the URL using the `?code=`

query string or in the request header (`x-functions-key`

). For more information, see [Access key authorization](functions-bindings-http-webhook-trigger#api-key-authorization).

To access the runtime REST APIs (under `/admin/`

), you must provide the master key (`_master`

) in the `x-functions-key`

request header. You can [remove the admin endpoints](security-concepts#disable-administrative-endpoints) using the `functionsRuntimeAdminIsolationEnabled`

site property.

## Get your function access keys

You can get function and host keys programmatically by using these Azure Resource Manager APIs:

To learn how to call Azure Resource Manager APIs, see the [Azure REST API reference](/en-us/rest/api/azure/).

You can use these methods to get access keys without having to use the REST APIs.

Sign in to the Azure portal, then search for and select

**Function App**.Select the function app you want to work with.

In the left menu, expand

**Functions**, and then select**App keys**.The

**App keys**page appears.  the host keys are displayed, which can be used to access any function in the app. The system key is also displayed, which gives anyone administrator-level access to all function app APIs.

You can also practice least privilege by using the key for a specific function. You can get function-specific keys from the **Function keys** tab of a specific HTTP-triggered function.

Tip

You can also obtain access keys for your functions by using the Azure Functions Core Tools command `func azure functionapp list-functions`

with the `--show-keys`

option. For more information, see the [Azure Functions Core Tools reference](functions-core-tools-reference#func-azure-functionapp-list-functions).

## Renew or create access keys

When you renew or create your access key values, you must manually redistribute the updated key values to all clients that call your function.

You can renew function and host keys programmatically or create new ones by using these Azure Resource Manager APIs:

[Create Or Update Function Secret](/en-us/rest/api/appservice/webapps/createorupdatefunctionsecret)[Create Or Update Function Secret Slot](/en-us/rest/api/appservice/webapps/createorupdatefunctionsecretslot)[Create Or Update Host Secret](/en-us/rest/api/appservice/webapps/createorupdatehostsecret)[Create Or Update Host Secret Slot](/en-us/rest/api/appservice/webapps/createorupdatehostsecretslot)

To learn how to call Azure Resource Manager APIs, see the [Azure REST API reference](/en-us/rest/api/azure/).

You can use these methods to get access keys without having to manually create calls to the REST APIs.

Sign in to the Azure portal, then search for and select

**Function App**.Select the function app you want to work with.

In the left menu, expand

**Functions**, and then select**App keys**.The

**App keys**page appears.  the host keys are displayed, which can be used to access any function in the app. The system key is also displayed, which gives anyone administrator-level access to all function app APIs.Select

**Renew key value**next to the key you want to renew, then select**Renew and save**.

You can also renew a function key in the **Function keys** tab of a specific HTTP-triggered function.

## Delete access keys

You can delete function and host keys programmatically by using these Azure Resource Manager APIs:

To learn how to call Azure Resource Manager APIs, see the [Azure REST API reference](/en-us/rest/api/azure/).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-kafka -->

# Apache Kafka bindings for Azure Functions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Kafka extension for Azure Functions enables you to write values to [Apache Kafka](https://kafka.apache.org/) topics by using an output binding. You can also use a trigger to invoke your functions in response to messages in Kafka topics.

Important

Kafka bindings are available for Functions on the [Flex Consumption plan](flex-consumption-plan), [Elastic Premium Plan](functions-premium-plan), and [Dedicated (App Service) plan](dedicated-plan). They are only supported on version 4.x of the Functions runtime.

| Action | Type |
|---|---|
| Run a function based on a new Kafka event. |
|

[Output binding](functions-bindings-kafka-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions run in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

Add the extension to your project by installing this [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Kafka).

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

## Enable runtime scaling

To allow your functions to scale properly on the Premium plan when using Kafka triggers and bindings, you need to enable runtime scale monitoring.

In the Azure portal, in your function app, select

**Configuration**.On the

**Function runtime settings**tab, for**Runtime Scale Monitoring**, select**On**.

## host.json settings

This section describes the configuration settings available for this binding in versions 3.x and higher. Settings in the host.json file apply to all functions in a function app instance. For more information about function app configuration settings in versions 3.x and later versions, see the [host.json reference for Azure Functions](functions-host-json).

```
{
"version": "2.0",
"extensions": {
"kafka": {
"maxBatchSize": 64,
"SubscriberIntervalInSeconds": 1,
"ExecutorChannelCapacity": 1,
"ChannelFullRetryIntervalInMs": 50
}
}
}
```


| Property | Default | Type | Description |
|---|---|---|---|
| ChannelFullRetryIntervalInMs | 50 | Trigger | Defines the subscriber retry interval, in milliseconds, used when attempting to add items to an at-capacity channel. |
| ExecutorChannelCapacity | 1 | Both | Defines the channel message capacity. Once capacity is reached, the Kafka subscriber pauses until the function catches up. |
| MaxBatchSize | 64 | Trigger | Maximum batch size when calling a Kafka triggered function. |
| SubscriberIntervalInSeconds | 1 | Trigger | Defines the minimum frequency incoming messages are executed, per function in seconds. Only when the message volume is less than `MaxBatchSize` / `SubscriberIntervalInSeconds` |

The following properties, which are inherited from the [Apache Kafka C/C++ client library](https://github.com/edenhill/librdkafka/blob/master/CONFIGURATION.md), are also supported in the `kafka`

section of host.json, for either triggers or both output bindings and triggers:

| Property | Applies to | librdkafka equivalent |
|---|---|---|
| AutoCommitIntervalMs | Trigger | `auto.commit.interval.ms` |
| AutoOffsetReset | Trigger | `auto.offset.reset` |
| FetchMaxBytes | Trigger | `fetch.max.bytes` |
| LibkafkaDebug | Both | `debug` |
| MaxPartitionFetchBytes | Trigger | `max.partition.fetch.bytes` |
| MaxPollIntervalMs | Trigger | `max.poll.interval.ms` |
| MetadataMaxAgeMs | Both | `metadata.max.age.ms` |
| QueuedMinMessages | Trigger | `queued.min.messages` |
| QueuedMaxMessagesKbytes | Trigger | `queued.max.messages.kbytes` |
| ReconnectBackoffMs | Trigger | `reconnect.backoff.max.ms` |
| ReconnectBackoffMaxMs | Trigger | `reconnect.backoff.max.ms` |
| SessionTimeoutMs | Trigger | `session.timeout.ms` |
| SocketKeepaliveEnable | Both | `socket.keepalive.enable` |
| StatisticsIntervalMs | Trigger | `statistics.interval.ms` |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-networking-faq -->

# Frequently asked questions about networking in Azure Functions

This article lists frequently asked questions about networking in Azure Functions. For a more comprehensive overview, see [Functions networking options](functions-networking-options).

## How do I set a static IP in Functions?

Deploying a function in an App Service Environment is the primary way to have static inbound and outbound IP addresses for your functions. For details on using an App Service Environment, start with the article [Create and use an internal load balancer with an App Service Environment](../app-service/environment/create-ilb-ase).

You can also use a virtual network NAT gateway to route outbound traffic through a public IP address that you control. To learn more, see [Tutorial: Control Azure Functions outbound IP with an Azure virtual network NAT gateway](functions-how-to-use-nat-gateway).

## How do I restrict internet access to my function?

You can restrict internet access in a couple of ways:

[Private endpoints](functions-networking-options#private-endpoints): Restrict inbound traffic to your function app by private link over your virtual network, effectively blocking inbound traffic from the public internet.[IP restrictions](../app-service/app-service-ip-restrictions): Restrict inbound traffic to your function app by IP range.- Under IP restrictions, you are also able to configure
[Service Endpoints](../virtual-network/virtual-network-service-endpoints-overview), which restrict your Function to only accept inbound traffic from a particular virtual network.

- Under IP restrictions, you are also able to configure
- Removal of all HTTP triggers. For some applications, it's enough to simply avoid HTTP triggers and use any other event source to trigger your function.

Keep in mind that the Azure portal editor requires direct access to your running function. Any code changes through the Azure portal will require the device you're using to browse the portal to have its IP added to the approved list. But you can still use anything under the platform features tab with network restrictions in place.

## How do I restrict my function app to a virtual network?

You are able to restrict **inbound** traffic for a function app to a virtual network using [Service Endpoints](functions-networking-options#use-service-endpoints). This configuration still allows the function app to make outbound calls to the internet.

To completely restrict a function such that all traffic flows through a virtual network, you can use a [private endpoints](functions-networking-options#private-endpoints) with outbound virtual network integration or an App Service Environment. To learn more, see [Integrate Azure Functions with an Azure virtual network by using private endpoints](functions-create-vnet).

## How can I access resources in a virtual network from a function app?

You can access resources in a virtual network from a running function by using virtual network integration. For more information, see [Virtual network integration](functions-networking-options#virtual-network-integration).

## How do I access resources protected by service endpoints?

By using virtual network integration you can access service-endpoint-secured resources from a running function. For more information, see [virtual network integration](functions-networking-options#virtual-network-integration).

## How can I trigger a function from a resource in a virtual network?

You are able to allow HTTP triggers to be called from a virtual network using [Service Endpoints](functions-networking-options#use-service-endpoints) or [Private Endpoint connections](functions-networking-options#private-endpoints).

You can also trigger a function from all other resources in a virtual network by deploying your function app to a Premium plan, App Service plan, or App Service Environment. See [non-HTTP virtual network triggers](functions-networking-options#virtual-network-triggers-non-http)
for more information

## How can I deploy my function app in a virtual network?

Deploying to an App Service Environment is the only way to create a function app that's wholly inside a virtual network. For details on using an internal load balancer with an App Service Environment, start with the article [Create and use an internal load balancer with an App Service Environment](../app-service/environment/create-ilb-ase).

For scenarios where you need only one-way access to virtual network resources, or less comprehensive network isolation, see the [Functions networking overview](functions-networking-options).

## Next steps

To learn more about networking and functions:

[Follow the tutorial about getting started with virtual network integration](functions-create-vnet)[Learn more about the networking options in Azure Functions](functions-networking-options)[Learn more about virtual network integration with App Service and Functions](../app-service/overview-vnet-integration)[Learn more about virtual networks in Azure](../virtual-network/virtual-networks-overview)[Enable more networking features and control with App Service Environments](../app-service/environment/intro)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-first-function-resource-manager -->

# Quickstart: Create and deploy Azure Functions resources from an ARM template

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you use an Azure Resource Manager template (ARM template) to create a function app in a Flex Consumption plan in Azure, along with its required Azure resources. The function app provides a serverless execution context for your function code executions. The app uses Microsoft Entra ID with managed identities to connect to other Azure resources.

Completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

An [Azure Resource Manager template](/en-us/azure/azure-resource-manager/templates/overview) is a JavaScript Object Notation (JSON) file that defines the infrastructure and configuration for your project. The template uses declarative syntax. You describe your intended deployment without writing the sequence of programming commands to create the deployment.

If your environment meets the prerequisites and you're familiar with using ARM templates, select the **Deploy to Azure** button. The template opens in the Azure portal.

After you create the function app, you can deploy your Azure Functions project code to that app. A final code deployment step is outside the scope of this quickstart article.

## Prerequisites

### Azure account

Before you begin, you must have an Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Review the template

The template used in this quickstart is from [Azure Quickstart Templates](/en-us/samples/azure/azure-quickstart-templates/function-app-flex-managed-identities/).

```
{
"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"metadata": {
"_generator": {
"name": "bicep",
"version": "0.33.93.31351",
"templateHash": "7223343042960867068"
}
},
"parameters": {
"location": {
"type": "string",
"defaultValue": "[resourceGroup().location]",
"minLength": 1,
"metadata": {
"description": "Primary region for all Azure resources."
}
},
"functionAppRuntime": {
"type": "string",
"defaultValue": "dotnet-isolated",
"allowedValues": [
"dotnet-isolated",
"python",
"java",
"node",
"powerShell"
],
"metadata": {
"description": "Language runtime used by the function app."
}
},
"functionAppRuntimeVersion": {
"type": "string",
"defaultValue": "8.0",
"allowedValues": [
"3.10",
"3.11",
"7.4",
"8.0",
"9.0",
"10",
"11",
"17",
"20"
],
"metadata": {
"description": "Target language version used by the function app."
}
},
"maximumInstanceCount": {
"type": "int",
"defaultValue": 100,
"minValue": 40,
"maxValue": 1000,
"metadata": {
"description": "The maximum scale-out instance count limit for the app."
}
},
"instanceMemoryMB": {
"type": "int",
"defaultValue": 2048,
"allowedValues": [
2048,
4096
],
"metadata": {
"description": "The memory size of instances used by the app."
}
},
"resourceToken": {
"type": "string",
"defaultValue": "[toLower(uniqueString(subscription().id, parameters('location')))]",
"minLength": 3,
"metadata": {
"description": "A unique token used for resource name generation."
}
},
"appName": {
"type": "string",
"defaultValue": "[format('func-{0}', parameters('resourceToken'))]",
"metadata": {
"description": "A globally unigue name for your deployed function app."
}
}
},
"variables": {
"deploymentStorageContainerName": "[format('app-package-{0}-{1}', take(parameters('appName'), 32), take(parameters('resourceToken'), 7))]",
"storageAccountAllowSharedKeyAccess": false,
"storageBlobDataOwnerRoleId": "b7e6dc6d-f1e8-4753-8033-0f276bb0955b",
"storageBlobDataContributorRoleId": "ba92f5b4-2d11-453d-a403-e96b0029c9fe",
"storageQueueDataContributorId": "974c5e8b-45b9-4653-ba55-5f855dd0fb88",
"storageTableDataContributorId": "0a9a7e1f-b9d0-4cc4-a60d-0319b160aaa3",
"monitoringMetricsPublisherId": "3913510d-42f4-4e42-8a64-420c390055eb"
},
"resources": [
{
"type": "Microsoft.Storage/storageAccounts/blobServices/containers",
"apiVersion": "2023-05-01",
"name": "[format('{0}/{1}/{2}', format('st{0}', parameters('resourceToken')), 'default', variables('deploymentStorageContainerName'))]",
"properties": {
"publicAccess": "None"
},
"dependsOn": [
"[resourceId('Microsoft.Storage/storageAccounts/blobServices', format('st{0}', parameters('resourceToken')), 'default')]"
]
},
{
"type": "Microsoft.Storage/storageAccounts/blobServices",
"apiVersion": "2023-05-01",
"name": "[format('{0}/{1}', format('st{0}', parameters('resourceToken')), 'default')]",
"properties": {
"deleteRetentionPolicy": {}
},
"dependsOn": [
"[resourceId('Microsoft.Storage/storageAccounts', format('st{0}', parameters('resourceToken')))]"
]
},
{
"type": "Microsoft.Web/sites/config",
"apiVersion": "2024-04-01",
"name": "[format('{0}/{1}', parameters('appName'), 'appsettings')]",
"properties": {
"AzureWebJobsStorage__accountName": "[format('st{0}', parameters('resourceToken'))]",
"AzureWebJobsStorage__credential": "managedidentity",
"AzureWebJobsStorage__clientId": "[reference(resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', format('uai-data-owner-{0}', parameters('resourceToken'))), '2023-01-31').clientId]",
"APPLICATIONINSIGHTS_INSTRUMENTATIONKEY": "[reference(resourceId('Microsoft.Insights/components', format('appi-{0}', parameters('resourceToken'))), '2020-02-02').InstrumentationKey]",
"APPLICATIONINSIGHTS_AUTHENTICATION_STRING": "[format('ClientId={0};Authorization=AAD', reference(resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', format('uai-data-owner-{0}', parameters('resourceToken'))), '2023-01-31').clientId)]"
},
"dependsOn": [
"[resourceId('Microsoft.Insights/components', format('appi-{0}', parameters('resourceToken')))]",
"[resourceId('Microsoft.Web/sites', parameters('appName'))]",
"[resourceId('Microsoft.Storage/storageAccounts', format('st{0}', parameters('resourceToken')))]",
"[resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', format('uai-data-owner-{0}', parameters('resourceToken')))]"
]
},
{
"type": "Microsoft.OperationalInsights/workspaces",
"apiVersion": "2023-09-01",
"name": "[format('log-{0}', parameters('resourceToken'))]",
"location": "[parameters('location')]",
"properties": {
"retentionInDays": 30,
"features": {
"searchVersion": 1
},
"sku": {
"name": "PerGB2018"
}
}
},
{
"type": "Microsoft.Insights/components",
"apiVersion": "2020-02-02",
"name": "[format('appi-{0}', parameters('resourceToken'))]",
"location": "[parameters('location')]",
"kind": "web",
"properties": {
"Application_Type": "web",
"WorkspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', format('log-{0}', parameters('resourceToken')))]",
"DisableLocalAuth": true
},
"dependsOn": [
"[resourceId('Microsoft.OperationalInsights/workspaces', format('log-{0}', parameters('resourceToken')))]"
]
},
{
"type": "Microsoft.Storage/storageAccounts",
"apiVersion": "2023-05-01",
"name": "[format('st{0}', parameters('resourceToken'))]",
"location": "[parameters('location')]",
"kind": "StorageV2",
"sku": {
"name": "Standard_LRS"
},
"properties": {
"accessTier": "Hot",
"allowBlobPublicAccess": false,
"allowSharedKeyAccess": "[variables('storageAccountAllowSharedKeyAccess')]",
"dnsEndpointType": "Standard",
"minimumTlsVersion": "TLS1_2",
"networkAcls": {
"bypass": "AzureServices",
"defaultAction": "Allow"
},
"publicNetworkAccess": "Enabled"
}
},
{
"type": "Microsoft.ManagedIdentity/userAssignedIdentities",
"apiVersion": "2023-01-31",
"name": "[format('uai-data-owner-{0}', parameters('resourceToken'))]",
"location": "[parameters('location')]"
},
{
"type": "Microsoft.Authorization/roleAssignments",
"apiVersion": "2022-04-01",
"scope": "[format('Microsoft.Storage/storageAccounts/{0}', format('st{0}', parameters('resourceToken')))]",
"name": "[guid(subscription().id, resourceId('Microsoft.Storage/storageAccounts', format('st{0}', parameters('resourceToken'))), resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', format('uai-data-owner-{0}', parameters('resourceToken'))), 'Storage Blob Data Owner')]",
"properties": {
"roleDefinitionId": "[subscriptionResourceId('Microsoft.Authorization/roleDefinitions', variables('storageBlobDataOwnerRoleId'))]",
"principalId": "[reference(resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', format('uai-data-owner-{0}', parameters('resourceToken'))), '2023-01-31').principalId]",
"principalType": "ServicePrincipal"
},
"dependsOn": [
"[resourceId('Microsoft.Storage/storageAccounts', format('st{0}', parameters('resourceToken')))]",
"[resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', format('uai-data-owner-{0}', parameters('resourceToken')))]"
]
},
{
"type": "Microsoft.Authorization/roleAssignments",
"apiVersion": "2022-04-01",
"scope": "[format('Microsoft.Storage/storageAccounts/{0}', format('st{0}', parameters('resourceToken')))]",
"name": "[guid(subscription().id, resourceId('Microsoft.Storage/storageAccounts', format('st{0}', parameters('resourceToken'))), resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', format('uai-data-owner-{0}', parameters('resourceToken'))), 'Storage Blob Data Contributor')]",
"properties": {
"roleDefinitionId": "[subscriptionResourceId('Microsoft.Authorization/roleDefinitions', variables('storageBlobDataContributorRoleId'))]",
"principalId": "[reference(resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', format('uai-data-owner-{0}', parameters('resourceToken'))), '2023-01-31').principalId]",
"principalType": "ServicePrincipal"
},
"dependsOn": [
"[resourceId('Microsoft.Storage/storageAccounts', format('st{0}', parameters('resourceToken')))]",
"[resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', format('uai-data-owner-{0}', parameters('resourceToken')))]"
]
},
{
"type": "Microsoft.Authorization/roleAssignments",
"apiVersion": "2022-04-01",
"scope": "[format('Microsoft.Storage/storageAccounts/{0}', format('st{0}', parameters('resourceToken')))]",
"name": "[guid(subscription().id, resourceId('Microsoft.Storage/storageAccounts', format('st{0}', parameters('resourceToken'))), resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', format('uai-data-owner-{0}', parameters('resourceToken'))), 'Storage Queue Data Contributor')]",
"properties": {
"roleDefinitionId": "[subscriptionResourceId('Microsoft.Authorization/roleDefinitions', variables('storageQueueDataContributorId'))]",
"principalId": "[reference(resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', format('uai-data-owner-{0}', parameters('resourceToken'))), '2023-01-31').principalId]",
"principalType": "ServicePrincipal"
},
"dependsOn": [
"[resourceId('Microsoft.Storage/storageAccounts', format('st{0}', parameters('resourceToken')))]",
"[resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', format('uai-data-owner-{0}', parameters('resourceToken')))]"
]
},
{
"type": "Microsoft.Authorization/roleAssignments",
"apiVersion": "2022-04-01",
"scope": "[format('Microsoft.Storage/storageAccounts/{0}', format('st{0}', parameters('resourceToken')))]",
"name": "[guid(subscription().id, resourceId('Microsoft.Storage/storageAccounts', format('st{0}', parameters('resourceToken'))), resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', format('uai-data-owner-{0}', parameters('resourceToken'))), 'Storage Table Data Contributor')]",
"properties": {
"roleDefinitionId": "[subscriptionResourceId('Microsoft.Authorization/roleDefinitions', variables('storageTableDataContributorId'))]",
"principalId": "[reference(resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', format('uai-data-owner-{0}', parameters('resourceToken'))), '2023-01-31').principalId]",
"principalType": "ServicePrincipal"
},
"dependsOn": [
"[resourceId('Microsoft.Storage/storageAccounts', format('st{0}', parameters('resourceToken')))]",
"[resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', format('uai-data-owner-{0}', parameters('resourceToken')))]"
]
},
{
"type": "Microsoft.Authorization/roleAssignments",
"apiVersion": "2022-04-01",
"scope": "[format('Microsoft.Insights/components/{0}', format('appi-{0}', parameters('resourceToken')))]",
"name": "[guid(subscription().id, resourceId('Microsoft.Insights/components', format('appi-{0}', parameters('resourceToken'))), resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', format('uai-data-owner-{0}', parameters('resourceToken'))), 'Monitoring Metrics Publisher')]",
"properties": {
"roleDefinitionId": "[subscriptionResourceId('Microsoft.Authorization/roleDefinitions', variables('monitoringMetricsPublisherId'))]",
"principalId": "[reference(resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', format('uai-data-owner-{0}', parameters('resourceToken'))), '2023-01-31').principalId]",
"principalType": "ServicePrincipal"
},
"dependsOn": [
"[resourceId('Microsoft.Insights/components', format('appi-{0}', parameters('resourceToken')))]",
"[resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', format('uai-data-owner-{0}', parameters('resourceToken')))]"
]
},
{
"type": "Microsoft.Web/serverfarms",
"apiVersion": "2024-04-01",
"name": "[format('plan-{0}', parameters('resourceToken'))]",
"location": "[parameters('location')]",
"kind": "functionapp",
"sku": {
"tier": "FlexConsumption",
"name": "FC1"
},
"properties": {
"reserved": true
}
},
{
"type": "Microsoft.Web/sites",
"apiVersion": "2024-04-01",
"name": "[parameters('appName')]",
"location": "[parameters('location')]",
"kind": "functionapp,linux",
"identity": {
"type": "UserAssigned",
"userAssignedIdentities": {
"[format('{0}', resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', format('uai-data-owner-{0}', parameters('resourceToken'))))]": {}
}
},
"properties": {
"serverFarmId": "[resourceId('Microsoft.Web/serverfarms', format('plan-{0}', parameters('resourceToken')))]",
"httpsOnly": true,
"siteConfig": {
"minTlsVersion": "1.2"
},
"functionAppConfig": {
"deployment": {
"storage": {
"type": "blobContainer",
"value": "[format('{0}{1}', reference(resourceId('Microsoft.Storage/storageAccounts', format('st{0}', parameters('resourceToken'))), '2023-05-01').primaryEndpoints.blob, variables('deploymentStorageContainerName'))]",
"authentication": {
"type": "UserAssignedIdentity",
"userAssignedIdentityResourceId": "[resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', format('uai-data-owner-{0}', parameters('resourceToken')))]"
}
}
},
"scaleAndConcurrency": {
"maximumInstanceCount": "[parameters('maximumInstanceCount')]",
"instanceMemoryMB": "[parameters('instanceMemoryMB')]"
},
"runtime": {
"name": "[parameters('functionAppRuntime')]",
"version": "[parameters('functionAppRuntimeVersion')]"
}
}
},
"dependsOn": [
"[resourceId('Microsoft.Web/serverfarms', format('plan-{0}', parameters('resourceToken')))]",
"[resourceId('Microsoft.Storage/storageAccounts', format('st{0}', parameters('resourceToken')))]",
"[resourceId('Microsoft.ManagedIdentity/userAssignedIdentities', format('uai-data-owner-{0}', parameters('resourceToken')))]"
]
}
]
}
```


This template creates these Azure resources needed by a function app that securely connects to Azure services:

: creates your function app.**Microsoft.Web/sites**: creates a serverless Flex Consumption hosting plan for your app.**Microsoft.Web/serverfarms**: creates an Azure Storage account, which is required by Functions.**Microsoft.Storage/storageAccounts**: creates an Application Insights instance for monitoring your app.**Microsoft.Insights/components**: creates a workspace required by Application Insights.**Microsoft.OperationalInsights/workspaces**: creates a user-assigned managed identity that's used by the app to authenticate with other Azure services using Microsoft Entra.**Microsoft.ManagedIdentity/userAssignedIdentities**: creates role assignments to the user-assigned managed identity, which provide the app with least-privilege access when connecting to other Azure services.**Microsoft.Authorization/roleAssignments**

Deployment considerations:

- The storage account is used to store important app data, including the application code deployment package. This deployment creates a storage account that is accessed using Microsoft Entra ID authentication and managed identities. Identity access is granted on a least-permissions basis.
- The Bicep file defaults to creating a C# app that uses .NET 8 in an isolated process. For other languages, use the
`functionAppRuntime`

and`functionAppRuntimeVersion`

parameters to specify the specific language and version on which to run your app. Make sure to select your programming language at the[top](#top)of the article.

## Deploy the template

These scripts are designed for and tested in [Azure Cloud Shell](../cloud-shell/overview). Choose **Try It** to open a Cloud Shell instance right in your browser. When prompted, enter the name of a region that [supports the Flex Consumption plan](flex-consumption-how-to#view-currently-supported-regions), such as `eastus`

or `northeurope`

.

```
read -p "Enter a supported Azure region: " location &&
resourceGroupName=exampleRG &&
templateUri="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/quickstarts/microsoft.web/function-app-flex-managed-identities/azuredeploy.json" &&
az group create --name $resourceGroupName --location "$location" &&
az deployment group create --resource-group $resourceGroupName --template-uri $templateUri --parameters functionAppRuntime=dotnet-isolated functionAppRuntimeVersion=8.0 &&
echo "Press [ENTER] to continue ..." &&
read
```


```
read -p "Enter a supported Azure region: " location &&
resourceGroupName=exampleRG &&
templateUri="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/quickstarts/microsoft.web/function-app-flex-managed-identities/azuredeploy.json" &&
az group create --name $resourceGroupName --location "$location" &&
az deployment group create --resource-group $resourceGroupName --template-uri $templateUri --parameters functionAppRuntime=java functionAppRuntimeVersion=17 &&
echo "Press [ENTER] to continue ..." &&
read
```


```
read -p "Enter a supported Azure region: " location &&
resourceGroupName=exampleRG &&
templateUri="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/quickstarts/microsoft.web/function-app-flex-managed-identities/azuredeploy.json" &&
az group create --name $resourceGroupName --location "$location" &&
az deployment group create --resource-group $resourceGroupName --template-uri $templateUri --parameters functionAppRuntime=node functionAppRuntimeVersion=20 &&
echo "Press [ENTER] to continue ..." &&
read
```


```
read -p "Enter a supported Azure region: " location &&
resourceGroupName=exampleRG &&
templateUri="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/quickstarts/microsoft.web/function-app-flex-managed-identities/azuredeploy.json" &&
az group create --name $resourceGroupName --location "$location" &&
az deployment group create --resource-group $resourceGroupName --template-uri $templateUri --parameters functionAppRuntime=python functionAppRuntimeVersion=3.11 &&
echo "Press [ENTER] to continue ..." &&
read
```


```
read -p "Enter a supported Azure region: " location &&
resourceGroupName=exampleRG &&
templateUri="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/quickstarts/microsoft.web/function-app-flex-managed-identities/azuredeploy.json" &&
az group create --name $resourceGroupName --location "$location" &&
az deployment group create --resource-group $resourceGroupName --template-uri $templateUri --parameters functionAppRuntime=powerShell functionAppRuntimeVersion=7.4 &&
echo "Press [ENTER] to continue ..." &&
read
```


When the deployment finishes, you should see a message indicating the deployment succeeded.

## Visit function app welcome page

Use the output from the previous validation step to retrieve the unique name created for your function app.

Open a browser and enter the following URL:

**<https://<appName.azurewebsites.net>**. Make sure to replace**<\appName>**with the unique name created for your function app.When you visit the URL, you should see a page like this:


## Clean up resources

Now that you have deployed a function app and related resources to Azure, can continue to the next step of publishing project code to your app. Otherwise, use these commands to delete the resources, when you no longer need them.

```
az group delete --name exampleRG
```


You can also remove resources by using the [Azure portal](https://portal.azure.com).

## Next steps

You can now deploy a code project to the function app resources you created in Azure.

You can create, verify, and deploy a code project to your new function app from these local environments:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-http-webhook-trigger -->

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
