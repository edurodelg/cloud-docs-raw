---
merged_at: 2026-01-25T15:41:11.643327
merged_files: 2
---

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
