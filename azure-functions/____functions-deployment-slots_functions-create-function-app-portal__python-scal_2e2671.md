---
merged_at: 2026-01-26T21:02:36.345765
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-deployment-slots -->

# Azure Functions deployment slots

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions deployment slots allow your function app to run different instances called *slots*. Slots are different environments exposed by using a publicly available endpoint. One app instance is always mapped to the production slot, and you can swap instances assigned to a slot on demand.

The number of available slots depends on your specific hosting option:

| Hosting option | Slots (including production) |
|---|---|
|

[Flex Consumption plan](flex-consumption-plan)[Premium plan](functions-premium-plan)[Dedicated (App Service) plan](dedicated-plan)[1-20](../azure-resource-manager/management/azure-subscription-service-limits#azure-app-service-limits)[Container Apps](../container-apps/functions-overview)[Revisions](../container-apps/revisions)The following descriptions reflect how functions are affected by swapping slots:

- Traffic redirection is seamless; no requests are dropped because of a swap. This seamless behavior occurs because the next function trigger is routed to the swapped slot.
- Currently executing function are terminated during the swap. To learn how to write stateless and defensive functions, see
[Improve the performance and reliability of Azure Functions](performance-reliability#write-functions-to-be-stateless).

## Why use slots?

There are many advantages to using deployment slots, including:

**Different environments for different purposes**: Using different slots gives you the opportunity to differentiate app instances before swapping to production or a staging slot.**Prewarming**: Deploying to a slot instead of directly to production allows the app to warm up before going live. Additionally, using slots reduces latency for HTTP-triggered workloads. Instances are warmed up before deployment, which reduces the cold start for newly deployed functions.**Easy fallbacks**: After a swap with production, the slot with a previously staged app now has the previous production app. If the changes swapped into the production slot aren't as you expect, you can immediately reverse the swap to get your "last known good instance" back.**Minimize restarts**: Changing app settings in a production slot requires a restart of the running app. You can instead change settings in a staging slot and swap the settings change into production with a prewarmed instance. Slots are the recommended way to migrate between Functions runtime versions while maintaining the highest availability. To learn more, see[Minimum downtime update](migrate-version-3-version-4#minimum-downtime-update).

## Swap operations

During a swap, one slot is considered the source and the other is the target. The source slot has the instance of the application that is applied to the target slot. The following steps ensure the target slot doesn't experience downtime during a swap:

**Apply settings:**Settings from the target slot are applied to all instances of the source slot. For example, the production settings are applied to the staging instance. The applied settings include the following categories:[Slot-specific](#manage-settings)app settings and connection strings (if applicable)[Continuous deployment](../app-service/deploy-continuous-deployment)settings (if enabled)[App Service authentication](../app-service/overview-authentication-authorization)settings (if enabled)

**Wait for restarts and availability:**The swap waits for every instance in the source slot to complete its restart and to be available for requests. If any instance fails to restart, the swap operation reverts all changes to the source slot and stops the operation.**Update routing:**If all instances on the source slot are warmed up successfully, the two slots complete the swap by switching routing rules. After this step, the target slot (for example, the production slot) has the app that was previously warmed up in the source slot.**Repeat operation:**Now that the source slot has the preswap app previously in the target slot, complete the same operation by applying all settings and restarting the instances for the source slot.

Keep in mind the following points:

At any point of the swap operation, initialization of the swapped apps happens on the source slot. The target slot remains online while the source slot is prepared, whether the swap succeeds or fails.

To swap a staging slot with the production slot, make sure that the production slot is

*always*the target slot. This way, the swap operation doesn't affect your production app.Settings related to event sources and bindings must be configured as

[deployment slot settings](#manage-settings)*before you start a swap*. Marking them as "sticky" ahead of time ensures events and outputs are directed to the proper instance.When you create a new staging slot, all existing settings from the production slot are created in the new slot, regardless of the

*stickiness*of the setting.

## Manage settings

Some configuration settings are slot-specific. The following lists detail which settings change when you swap slots, and which remain the same.

**Slot-specific settings**:

- Publishing endpoints
- Custom domain names
- Nonpublic certificates and TLS/SSL settings
- Scale settings
- IP restrictions
- Always On
- Diagnostic settings
- Cross-origin resource sharing (CORS)
- Private endpoints

**Non slot-specific settings**:

- General settings, such as framework version, 32/64-bit, web sockets
- App settings (can be configured to stick to a slot)
- Connection strings (can be configured to stick to a slot)
- Handler mappings
- Public certificates
- Hybrid connections *
- Virtual network integration *
- Service endpoints *
- Azure Content Delivery Network *

Features marked with an asterisk (*) don't get swapped, by design.

Note

Certain app settings that apply to unswapped settings are also not swapped. For example, since diagnostic settings aren't swapped, related app settings like `WEBSITE_HTTPLOGGING_RETENTION_DAYS`

and `DIAGNOSTICS_AZUREBLOBRETENTIONDAYS`

are also not swapped, even if they don't show up as slot settings.

### Create a deployment setting

You can mark settings as a deployment setting, which makes it *sticky*. A sticky setting doesn't swap with the app instance.

If you create a deployment setting in one slot, make sure to create the same setting with a unique value in any other slot that is involved in a swap. This way, while a setting's value doesn't change, the setting names remain consistent among slots. This name consistency ensures your code doesn't try to access a setting that is defined in one slot but not another.

Use the following steps to create a deployment setting:

Navigate to

**Deployment slots**in the function app, and then select the slot name.Select

**Configuration**, and then select the setting name you want to stick with the current slot.Select

**Deployment slot setting**, and then select**OK**.Once setting section disappears, select

**Save**to keep the changes

## Deployment

Slots are empty when you create a slot. You can use any of the [supported deployment technologies](functions-deployment-technologies) to deploy your application to a slot.

## Scaling

All slots scale to the same number of workers as the production slot.

- For Consumption plans, the slot scales as the function app scales.
- For App Service plans, the app scales to a fixed number of workers. Slots run on the same number of workers as the app plan.

## View slots

You can view information about existing slots using either the [Azure CLI](/en-us/cli/azure) or through the [Azure portal](https://portal.azure.com).

Use these steps to create a new slot in the portal:

Navigate to your function app.

Select

**Deployment slots**and the existing slots are shown.

## Add a slot

You can add a slot using either the [Azure CLI](/en-us/cli/azure) or through the [Azure portal](https://portal.azure.com).

Use these steps to create a slot in the portal:

Navigate to your function app.

Select

**Deployment slots**, and then select**+ Add Slot**.Type the name of the slot and select

**Add**.

You can also create a slot by using ARM templates or Bicep files. For an example of how to create a function app in a Consumption plan with a deployment slot, see this [Azure Resource Manager quickstart](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.web/function-app-create-dynamic-slot).

## Access slot resources

You access resources (HTTP triggers and administrator endpoints) in a staging slot in the same way as the production slot. However, instead of the function app host name you use the slot-specific host name in the request URL, along with any slot-specific keys. Because staging slots are live apps, you must [secure your functions](security-concepts) in a staging slot as you would in the production slot.

## Swap slots

You can swap slots in an out of production using either the [Azure CLI](/en-us/cli/azure) or through the [Azure portal](https://portal.azure.com).

Use these steps to swap a staging slot into production:

Navigate to the function app.

Select

**Deployment slots**, and then select**Swap**.Verify the configuration settings for your swap and select

**Swap**.

The swap operation can take a few seconds.

## Roll back a swap

If a swap results in an error or you simply want to "undo" a swap, you can roll back to the initial state. To return to the preswapped state, do another swap to reverse the swap.

## Remove a slot

You can remove a slot using either the [Azure CLI](/en-us/cli/azure) or through the [Azure portal](https://portal.azure.com).

Use these steps to remove a slot from your app in the portal:

Navigate to

**Deployment slots**in the function app, and then select the slot name.Select

**Delete**.Type the name of the deployment slot you want to delete, and then select

**Delete**.Close the confirmation pane.


## Change App Service plan

With a function app that is running under an App Service plan, you can change the underlying App Service plan for a slot.

Note

You can't change a slot's App Service plan under the Consumption plan.

Use the following steps to change a slot's App Service plan:

Navigate to

**Deployment slots**in the function app, and then select the slot name.Under

**App Service plan**, select**Change App Service plan**.Select the plan you want to upgrade to, or create a new plan.

Select

**OK**.

## Considerations

Azure Functions deployment slots have the following considerations:

- The number of slots available to an app depends on the plan. The Consumption plan is only allowed one deployment slot. More slots are available for apps running under other plans. For details, see
[Service limits](functions-scale#service-limits). - Swapping a slot resets keys for apps that have an
`AzureWebJobsSecretStorageType`

app setting equal to`files`

. - When slots are enabled, your function app is set to read-only mode in the portal.
- Slot swaps might fail when your function app is using a
[secured storage account](configure-networking-how-to)as its default storage account (set in`AzureWebJobsStorage`

). For more information, see thereference.`WEBSITE_OVERRIDE_STICKY_DIAGNOSTICS_SETTINGS`

- Use function app names shorter than 32 characters. Names longer than 32 characters are at risk of causing
[host ID collisions](storage-considerations#host-id-considerations).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-function-app-portal -->

# Create a function app in the Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use the Azure portal to create a function app that's hosted in Azure Functions. These hosting plan options, which support dynamic, event-driven scaling, are featured:

| Hosting option | Description |
|---|---|
|

[Premium plan](functions-premium-plan)[Consumption plan](consumption-plan)The Flex Consumption plan is the recommended plan for hosting serverless compute resources in Azure.

Choose your preferred hosting plan at the [top](#top) of the article. For more information about all supported hosting options, see [Azure Functions hosting options](functions-scale).

## Prerequisites

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Sign in to Azure

Sign in to the [Azure portal](https://portal.azure.com) with your Azure account.

## Create a function app

You must have a function app to host the execution of your functions. A function app lets you group functions as a logical unit for easier management, deployment, scaling, and sharing of resources.

Use these steps to create your function app and related Azure resources in the Azure portal.

In the

[Azure portal](https://portal.azure.com), from the menu or the**Home**page, select**Create a resource**.Select

**Get started**and then**Create**under**Function App**.Under

**Select a hosting option**, choose**Flex Consumption**>**Select**.On the

**Basics**page, use the function app settings as specified in the following table:Setting Suggested value Description **Subscription**Your subscription The subscription in which you create your new function app. [Resource Group](../azure-resource-manager/management/overview)*myResourceGroup*Name for the new resource group in which you create your function app. **Function App name**Globally unique name Name that identifies your new function app. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

.**Region**Preferred region Select a [region](https://azure.microsoft.com/regions/)that's near you or near other services that your functions can access. Unsupported regions aren't displayed. For more information, see[View currently supported regions](flex-consumption-how-to#view-currently-supported-regions).**Runtime stack**Preferred language Choose one of the supported language runtime stacks. In-portal editing using Visual Studio Code for the Web is currently only available for Node.js, PowerShell, and Python apps. C# class library and Java functions must be [developed locally](functions-develop-local#local-development-environments).**Version**Language version Choose a supported version of your language runtime stack. **Instance size**Default Determines the amount of instance memory allocated for each instance of your app. For more information, see [Instance sizes](flex-consumption-plan#instance-sizes).On the

**Storage**page, accept the default behavior of creating a new[default host storage account](storage-considerations)or choose to use an existing storage account.

On the

**Monitoring**page, make sure that**Enable Application Insights**is selected. Accept the default to create a new Application Insights instance, or else choose to use an existing instance. When you create an Application Insights instance, you're also asked to select a Log Analytics**Workspace**.On the

**Authentication**page, change the**Authentication type**to**Managed identity**for all resources. With this option, a user-assigned managed identity is also created that your app uses to access these Azure resources using Microsoft Entra ID authentication. Managed identities with Microsoft Entra ID provides the highest level of security for connecting to Azure resources.Accept the default options in the remaining tabs and then select

**Review + create**to review the app configuration you chose.When you're satisfied, select

**Create**to provision and deploy the function app and related resources.Select the

**Notifications**icon in the upper-right corner of the portal and watch for the**Deployment succeeded**message.Select

**Go to resource**to view your new function app. You can also select**Pin to dashboard**. Pinning makes it easier to return to this function app resource from your dashboard.

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

From the Azure portal menu or the

**Home**page, select**Create a resource**.In the

**New**page, select**Compute**>**Function App**.Under

**Select a hosting option**, select**Functions Premium**>**Select**to create your app in a[Premium plan](functions-premium-plan). In this[serverless](https://azure.microsoft.com/overview/serverless-computing/)hosting option, you pay only for the time your functions run. To learn more about different hosting plans, see[Overview of plans](functions-scale#overview-of-plans).On the

**Basics**page, use the function app settings as specified in the following table:Setting Suggested value Description **Subscription**Your subscription The subscription under which this new function app is created. [Resource Group](../azure-resource-manager/management/overview)*myResourceGroup*Name for the new resource group in which to create your function app. **Function App name**Globally unique name Name that identifies your new function app. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

. To guarantee a unique app name, you can optionally enable**Secure unique default hostname**, which is currently in preview.**Do you want to deploy code or container image?**Code Option to publish code files or a Docker container. **Operating system**Preferred OS Choose either Linux or Windows. **Runtime stack**Preferred language Choose a runtime that supports your favorite function programming language. **Version**Supported language version Choose a supported version of your function programming language. **Region**Preferred region Choose a [region](https://azure.microsoft.com/regions/)near you or near other services your functions access.Under

**Environment details**for either**Windows Plan**or**Linux Plan**, select**Create new**,**Name**your App Service plan, and select a**Pricing plan**. The default pricing plan is**EP1**, where EP stands for*elastic premium*. To learn more, see the[list of Premium SKUs](functions-premium-plan#available-instance-skus). When running JavaScript functions on a Premium plan, you should choose an instance that has fewer vCPUs. For more information, see[Choose single-core Premium plans](functions-reference-node#considerations-for-javascript-functions).Unless you want to enable

, keep the default value of**Zone Redundancy****Disabled**.Select

**Next: Storage**. On the**Storage**page, create the default host[storage account](../storage/common/storage-account-create)required by your function app. Storage account names must be between 3 and 24 characters in length and only can contain numbers and lowercase letters. You can also use an existing account, which must meet the[storage account requirements](storage-considerations#storage-account-requirements).Unless you're enabling virtual network integration, select

**Next: Monitoring**to skip the**Networking**tab. On the**Monitoring**page, enter the following settings:Setting Suggested value Description Enable Application Insights Yes Enables built-in Application Insight integration for monitoring your functions code. [Application Insights](functions-monitoring)Default Creates an Application Insights resource of the same *App name*in the nearest supported region. By expanding this setting, you can change the**New resource name**or choose a different**Location**in an[Azure geography](https://azure.microsoft.com/global-infrastructure/geographies/)to store your data.Select

**Review + create**to accept the defaults for the remaining pages and review the app configuration selections.On the

**Review + create**page, review your settings, and then select**Create**to provision and deploy the function app.Select the

**Notifications**icon in the upper-right corner of the portal and watch for the**Deployment succeeded**message.Select

**Go to resource**to view your new function app. You can also select**Pin to dashboard**. Pinning makes it easier to return to this function app resource from your dashboard.

## Next steps

You can now deploy a code project to the function app resources you created in Azure.

You can create, verify, and deploy a code project to your new function app from these local environments:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/python-scale-performance-reference -->

# Improve throughput performance of Python apps in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When developing for Azure Functions using Python, you need to understand how your functions perform and how that performance affects the way your function app gets scaled. The need is more important when designing highly performant apps. The main factors to consider when designing, writing, and configuring your functions apps are horizontal scaling and throughput performance configurations.

## Horizontal scaling

By default, Azure Functions automatically monitors the load on your application and creates more host instances for Python as needed. Azure Functions uses built-in thresholds for different trigger types to decide when to add instances, such as the age of messages and queue size for QueueTrigger. These thresholds aren't user configurable. For more information, see [Event-driven scaling in Azure Functions](event-driven-scaling).

## Improving throughput performance

The default configurations are suitable for most of Azure Functions applications. However, you can improve the performance of your applications' throughput by employing configurations based on your workload profile. The first step is to understand the type of workload that you're running.

| Workload type | Function app characteristics | Examples |
|---|---|---|
I/O-bound |
• App needs to handle many concurrent invocations. • App processes a large number of I/O events, such as network calls and disk read/writes. |
• Web APIs |
CPU-bound |
• App does long-running computations, such as image resizing. • App does data transformation. |
• Data processing • Machine learning inference |

As real world function workloads are usually a mix of I/O and CPU bound, you should profile the app under realistic production loads.

### Performance-specific configurations

After you understand the workload profile of your function app, the following are configurations that you can use to improve the throughput performance of your functions.

[Async](#async)[Multiple language worker](#use-multiple-language-worker-processes)[Max workers within a language worker process](#set-up-max-workers-within-a-language-worker-process)[Event loop](#managing-event-loop)[Vertical Scaling](#vertical-scaling)

#### Async

Because [Python is a single-threaded runtime](https://wiki.python.org/moin/GlobalInterpreterLock), a host instance for Python can process only one function invocation at a time by default. For applications that process a large number of I/O events and/or is I/O bound, you can improve performance significantly by running functions asynchronously.

To run a function asynchronously, use the `async def`

statement, which runs the function with [asyncio](https://docs.python.org/3/library/asyncio.html) directly:

```
async def main():
await some_nonblocking_socket_io_op()
```


Here's an example of a function with HTTP trigger that uses [aiohttp](https://pypi.org/project/aiohttp/) http client:

```
import aiohttp
import azure.functions as func
async def main(req: func.HttpRequest) -> func.HttpResponse:
async with aiohttp.ClientSession() as client:
async with client.get("PUT_YOUR_URL_HERE") as response:
return func.HttpResponse(await response.text())
return func.HttpResponse(body='NotFound', status_code=404)
```


A function without the `async`

keyword is run automatically in a ThreadPoolExecutor thread pool:

```
# Runs in a ThreadPoolExecutor threadpool. Number of threads is defined by PYTHON_THREADPOOL_THREAD_COUNT.
# The example is intended to show how default synchronous functions are handled.
def main():
some_blocking_socket_io()
```


In order to achieve the full benefit of running functions asynchronously, the I/O operation/library that is used in your code needs to have async implemented as well. Using synchronous I/O operations in functions that are defined as asynchronous **may hurt** the overall performance. If the libraries you're using don't have async version implemented, you may still benefit from running your code asynchronously by [managing event loop](#managing-event-loop) in your app.

Here are a few examples of client libraries that have implemented async patterns:

[aiohttp](https://pypi.org/project/aiohttp/)- Http client/server for asyncio[Streams API](https://docs.python.org/3/library/asyncio-stream.html)- High-level async/await-ready primitives to work with network connection[Janus Queue](https://pypi.org/project/janus/)- Thread-safe asyncio-aware queue for Python[pyzmq](https://pypi.org/project/pyzmq/)- Python bindings for ZeroMQ

##### Understanding async in Python worker

When you define `async`

in front of a function signature, Python marks the function as a coroutine. When you call the coroutine, it can be scheduled as a task into an event loop. When you call `await`

in an async function, it registers a continuation into the event loop, which allows the event loop to process the next task during the wait time.

In our Python Worker, the worker shares the event loop with the customer's `async`

function and it's capable for handling multiple requests concurrently. We strongly encourage our customers to make use of asyncio compatible libraries, such as [aiohttp](https://pypi.org/project/aiohttp/) and [pyzmq](https://pypi.org/project/pyzmq/). Following these recommendations increases your function's throughput compared to those libraries when implemented synchronously.

Note

If your function is declared as `async`

without any `await`

inside its implementation, the performance of your function will be severely impacted since the event loop will be blocked which prohibits the Python worker from handling concurrent requests.

#### Use multiple language worker processes

By default, every Functions host instance has a single language worker process. You can increase the number of worker processes per host (up to 10) by using the [ FUNCTIONS_WORKER_PROCESS_COUNT](functions-app-settings#functions_worker_process_count) application setting. Azure Functions then tries to evenly distribute simultaneous function invocations across these workers.

For CPU bound apps, you should set the number of language workers to be the same as or higher than the number of cores that are available per function app. To learn more, see [Available instance SKUs](functions-premium-plan#available-instance-skus).

I/O-bound apps may also benefit from increasing the number of worker processes beyond the number of cores available. Keep in mind that setting the number of workers too high can affect overall performance due to the increased number of required context switches.

The `FUNCTIONS_WORKER_PROCESS_COUNT`

applies to each host that Azure Functions creates when scaling out your application to meet demand.

#### Set up max workers within a language worker process

As mentioned in the async [section](#understanding-async-in-python-worker), the Python language worker treats functions and [coroutines](https://docs.python.org/3/library/asyncio-task.html#coroutines) differently. A coroutine is run within the same event loop that the language worker runs on. On the other hand, a function invocation is run within a [ThreadPoolExecutor](https://docs.python.org/3/library/concurrent.futures.html#threadpoolexecutor), which is maintained by the language worker as a thread.

You can set the value of maximum workers allowed for running sync functions using the [PYTHON_THREADPOOL_THREAD_COUNT](functions-app-settings#python_threadpool_thread_count) application setting. This value sets the `max_worker`

argument of the ThreadPoolExecutor object, which lets Python use a pool of at most `max_worker`

threads to execute calls asynchronously. The `PYTHON_THREADPOOL_THREAD_COUNT`

applies to each worker that Functions host creates, and Python decides when to create a new thread or reuse the existing idle thread. For older Python versions(that is, `3.8`

, `3.7`

, and `3.6`

), `max_worker`

value is set to 1. For Python version `3.9`

, `max_worker`

is set to `None`

.

For CPU-bound apps, you should keep the setting to a low number, starting from 1 and increasing as you experiment with your workload. This suggestion is to reduce the time spent on context switches and allowing CPU-bound tasks to finish.

For I/O-bound apps, you should see substantial gains by increasing the number of threads working on each invocation. The recommendation is to start with the Python default (the number of cores) + 4 and then tweak based on the throughput values you're seeing.

For mixed workloads apps, you should balance both `FUNCTIONS_WORKER_PROCESS_COUNT`

and `PYTHON_THREADPOOL_THREAD_COUNT`

configurations to maximize the throughput. To understand what your function apps spend the most time on, we recommend profiling them and setting the values according to their behaviors. To learn about these application settings, see [Use multiple worker processes](#use-multiple-language-worker-processes).

Note

Although these recommendations apply to both HTTP and non-HTTP triggered functions, you might need to adjust other trigger specific configurations for non-HTTP triggered functions to get the expected performance from your function apps. For more information about this, please refer to this [Best practices for reliable Azure Functions](functions-best-practices).

#### Managing event loop

You should use asyncio compatible third-party libraries. If none of the third-party libraries meet your needs, you can also manage the event loops in Azure Functions. Managing event loops give you more flexibility in compute resource management, and it also makes it possible to wrap synchronous I/O libraries into coroutines.

There are many useful Python official documents discussing the [Coroutines and Tasks](https://docs.python.org/3/library/asyncio-task.html) and [Event Loop](https://docs.python.org/3.8/library/asyncio-eventloop.html) by using the built-in **asyncio** library.

Take the following [requests](https://github.com/psf/requests) library as an example, this code snippet uses the **asyncio** library to wrap the `requests.get()`

method into a coroutine, running multiple web requests to SAMPLE_URL concurrently.

```
import asyncio
import json
import logging
import azure.functions as func
from time import time
from requests import get, Response
async def invoke_get_request(eventloop: asyncio.AbstractEventLoop) -> Response:
# Wrap requests.get function into a coroutine
single_result = await eventloop.run_in_executor(
None, # using the default executor
get, # each task call invoke_get_request
'SAMPLE_URL' # the url to be passed into the requests.get function
)
return single_result
async def main(req: func.HttpRequest) -> func.HttpResponse:
logging.info('Python HTTP trigger function processed a request.')
eventloop = asyncio.get_event_loop()
# Create 10 tasks for requests.get synchronous call
tasks = [
asyncio.create_task(
invoke_get_request(eventloop)
) for _ in range(10)
]
done_tasks, _ = await asyncio.wait(tasks)
status_codes = [d.result().status_code for d in done_tasks]
return func.HttpResponse(body=json.dumps(status_codes),
mimetype='application/json')
```


#### Vertical scaling

You might be able to get more processing units, especially in CPU-bound operation, by upgrading to premium plan with higher specifications. With higher processing units, you can adjust the number of worker processes count according to the number of cores available and achieve higher degree of parallelism.

## Next steps

For more information about Azure Functions Python development, see the following resources:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/analyze-telemetry-data -->

# Analyze Azure Functions telemetry in Application Insights

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions integrates with Application Insights to better enable you to monitor your function apps. Application Insights collects telemetry data generated by your function app, including information your app writes to logs. Application Insights integration is typically enabled when your function app is created. If your function app doesn't have the instrumentation key set, you must first [enable Application Insights integration](configure-monitoring#enable-application-insights-integration).

By default, the data collected from your function app is stored in Application Insights. In the [Azure portal](https://portal.azure.com), Application Insights provides an extensive set of visualizations of your telemetry data. You can drill into error logs and query events and metrics. This article provides basic examples of how to view and query your collected data. To learn more about exploring your function app data in Application Insights, see [What is Application Insights?](/en-us/azure/azure-monitor/app/app-insights-overview).

To be able to view Application Insights data from a function app, you must have at least Contributor role permissions on the function app. You also need to have the [Monitoring Reader permission](/en-us/azure/azure-monitor/roles-permissions-security#monitoring-reader) on the Application Insights instance. You have these permissions by default for any function app and Application Insights instance that you create.

To learn more about data retention and potential storage costs, see [Data collection, retention, and storage in Application Insights](/en-us/previous-versions/azure/azure-monitor/app/data-retention-privacy).

## Viewing telemetry in Monitor tab

With [Application Insights integration enabled](configure-monitoring#enable-application-insights-integration), you can view telemetry data in the **Monitor** tab.

In the function app page, select a function that has run at least once after Application Insights was configured. Then, select

**Monitor**from the left pane. Select**Refresh**periodically, until the list of function invocations appears.Note

It can take up to five minutes for the list to appear while the telemetry client batches data for transmission to the server. The delay doesn't apply to the

[Live Metrics Stream](/en-us/azure/azure-monitor/app/live-stream). That service connects to the Functions host when you load the page, so logs are streamed directly to the page.To see the logs for a particular function invocation, select the

**Date (UTC)**column link for that invocation. The logging output for that invocation appears in a new page.Choose

**Run in Application Insights**to view the source of the query that retrieves the Azure Monitor log data in Azure Log. If this is your first time using Azure Log Analytics in your subscription, you're asked to enable it.After you enable Log Analytics, the following query is displayed. You can see that the query results are limited to the last 30 days (

`where timestamp > ago(30d)`

), and the results show no more than 20 rows (`take 20`

). In contrast, the invocation details list for your function is for the last 30 days with no limit.

For more information, see [Query telemetry data](#query-telemetry-data) later in this article.

## View telemetry in Application Insights

To open Application Insights from a function app in the [Azure portal](https://portal.azure.com):

Browse to your function app in the portal.

Select

**Application Insights**under**Settings**in the left page.If this is your first time using Application Insights with your subscription, you'll be prompted to enable it. To do this, select

**Turn on Application Insights**, and then select**Apply**on the next page.

For information about how to use Application Insights, see the [Application Insights documentation](/en-us/azure/azure-monitor/app/app-insights-overview). This section shows some examples of how to view data in Application Insights. If you're already familiar with Application Insights, you can go directly to [the sections about how to configure and customize the telemetry data](configure-monitoring#configure-log-levels).

The following areas of Application Insights can be helpful when evaluating the behavior, performance, and errors in your functions:

| Investigate | Description |
|---|---|
|
Create charts and alerts based on function failures and server exceptions. The Operation Name is the function name. Failures in dependencies aren't shown unless you implement custom telemetry for dependencies. |
|
Analyze performance issues by viewing resource utilization and throughput per Cloud role instances. This performance data can be useful for debugging scenarios where functions are bogging down your underlying resources. |
|
Create charts and alerts that are based on metrics. Metrics include the number of function invocations, execution time, and success rates. |
|
View metrics data as it's created in near real time. |

## Query telemetry data

[Application Insights Analytics](/en-us/azure/azure-monitor/logs/log-query-overview) gives you access to all telemetry data in the form of tables in a database. Analytics provides a query language for extracting, manipulating, and visualizing the data.

Choose **Logs** to explore or query for logged events.

Here's a query example that shows the distribution of requests per worker over the last 30 minutes.

```
requests
| where timestamp > ago(30m)
| summarize count() by cloud_RoleInstance, bin(timestamp, 1m)
| render timechart
```


The tables that are available are shown in the **Schema** tab on the left. You can find data generated by function invocations in the following tables:

| Table | Description |
|---|---|
traces |
Logs created by the runtime, scale controller, and traces from your function code. For Flex Consumption plan hosting, `traces` also includes logs created during code deployment. |
requests |
One request for each function invocation. |
exceptions |
Any exceptions thrown by the runtime. |
customMetrics |
The count of successful and failing invocations, success rate, and duration. |
customEvents |
Events tracked by the runtime, for example: HTTP requests that trigger a function. |
performanceCounters |
Information about the performance of the servers that the functions are running on. |

The other tables are for availability tests, and client and browser telemetry. You can implement custom telemetry to add data to them.

Within each table, some of the Functions-specific data is in a `customDimensions`

field. For example, the following query retrieves all traces that have log level `Error`

.

```
traces
| where customDimensions.LogLevel == "Error"
```


The runtime provides the `customDimensions.LogLevel`

and `customDimensions.Category`

fields. You can provide additional fields in logs that you write in your function code. For an example in C#, see [Structured logging](functions-dotnet-class-library#structured-logging) in the .NET class library developer guide.

## Query function invocations

Every function invocation is assigned a unique ID. `InvocationId`

is included in the custom dimension and can be used to correlate all the logs from a particular function execution.

```
traces
| project customDimensions["InvocationId"], message
```


## Telemetry correlation

Logs from different functions can be correlated using `operation_Id`

. Use the following query to return all the logs for a specific logical operation.

```
traces
| where operation_Id == '45fa5c4f8097239efe14a2388f8b4e29'
| project timestamp, customDimensions["InvocationId"], message
| order by timestamp
```


## Sampling percentage

Sampling configuration can be used to reduce the volume of telemetry. Use the following query to determine if sampling is operational or not. If you see that `RetainedPercentage`

for any type is less than 100, then that type of telemetry is being sampled.

```
union requests,dependencies,pageViews,browserTimings,exceptions,traces
| where timestamp > ago(1d)
| summarize RetainedPercentage = 100/avg(itemCount) by bin(timestamp, 1h), itemType
```


## Query scale controller logs

*This feature is in preview.*

After enabling both [scale controller logging](configure-monitoring#configure-scale-controller-logs) and [Application Insights integration](configure-monitoring#enable-application-insights-integration), you can use the Application Insights log search to query for the emitted scale controller logs. Scale controller logs are saved in the `traces`

collection under the **ScaleControllerLogs** category.

The following query can be used to search for all scale controller logs for the current function app within the specified time period:

```
traces
| extend CustomDimensions = todynamic(tostring(customDimensions))
| where CustomDimensions.Category == "ScaleControllerLogs"
```


The following query expands on the previous query to show how to get only logs indicating a change in scale:

```
traces
| extend CustomDimensions = todynamic(tostring(customDimensions))
| where CustomDimensions.Category == "ScaleControllerLogs"
| where message == "Instance count changed"
| extend Reason = CustomDimensions.Reason
| extend PreviousInstanceCount = CustomDimensions.PreviousInstanceCount
| extend NewInstanceCount = CustomDimensions.CurrentInstanceCount
```


## Query Flex Consumption code deployment logs

The following query can be used to search for all code deployment logs for the current function app within the specified time period:

```
traces
| extend deploymentId = customDimensions.deploymentId
| where deploymentId != ''
| project timestamp, deploymentId, message, severityLevel, customDimensions, appName
```


## Consumption plan-specific metrics

When running in a [Consumption plan](consumption-plan), the execution *cost* of a single function execution is measured in *GB-seconds*. Execution cost is calculated by combining its memory usage with its execution time. To learn more, see [Estimating Consumption plan costs](functions-consumption-costs).

The following telemetry queries are specific to metrics that impact the cost of running functions in the Consumption plan.

#### Determine memory usage

Under **Monitoring**, select **Logs (Analytics)**, then copy the following telemetry query and paste it into the query window and select **Run**. This query returns the total memory usage at each sampled time.

```
performanceCounters
| where name == "Private Bytes"
| project timestamp, name, value
```


The results look like the following example:

| timestamp [UTC] | name | value |
|---|---|---|
| 9/12/2019, 1:05:14.947 AM | Private Bytes | 209,932,288 |
| 9/12/2019, 1:06:14.994 AM | Private Bytes | 212,189,184 |
| 9/12/2019, 1:06:30.010 AM | Private Bytes | 231,714,816 |
| 9/12/2019, 1:07:15.040 AM | Private Bytes | 210,591,744 |
| 9/12/2019, 1:12:16.285 AM | Private Bytes | 216,285,184 |
| 9/12/2019, 1:12:31.376 AM | Private Bytes | 235,806,720 |

#### Determine duration

Azure Monitor tracks metrics at the resource level, which for Functions is the function app. Application Insights integration emits metrics on a per-function basis. Here's an example analytics query to get the average duration of a function:

```
customMetrics
| where name contains "Duration"
| extend averageDuration = valueSum / valueCount
| summarize averageDurationMilliseconds=avg(averageDuration) by name
```


| name | averageDurationMilliseconds |
|---|---|
| QueueTrigger AvgDurationMs | 16.087 |
| QueueTrigger MaxDurationMs | 90.249 |
| QueueTrigger MinDurationMs | 8.522 |

## Next steps

Learn more about monitoring Azure Functions:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-deploy-container-apps -->

# Create your first containerized functions on Azure Container Apps

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you create a function app running in a Linux container and deploy it to an Azure Container Apps environment from a container registry. By deploying to Container Apps, you're able to integrate your function apps into cloud-native microservices. For more information, see [Azure Container Apps hosting of Azure Functions](functions-container-apps-hosting).

Important

A new hosting method for running Azure Functions directly in Azure Container Apps is now available. See [Native Azure Functions Support in Azure Container Apps](https://techcommunity.microsoft.com/blog/appsonazureblog/announcing-native-azure-functions-support-in-azure-container-apps/4414039). This integration allows you to use the full features and capabilities of Azure Container Apps. You also benefit from the functions programming model and simplicity of autoscaling provided by Azure Functions.

We recommend this approach for most new workloads. For more information, see [Azure Functions on Azure Container Apps](../container-apps/functions-overview).

This article shows you how to create functions running in a Linux container and deploy the container to a Container Apps environment.

Completing this quickstart incurs a small cost of a few USD cents or less in your Azure account, which you can minimize by [cleaning-up resources](#clean-up-resources) when you're done.

## Choose your development language

First, you use Azure Functions tools to create your project code as a function app in a Docker container using a language-specific Linux base image. Make sure to select your language of choice at the top of the article.

Core Tools automatically generates a Dockerfile for your project that uses the most up-to-date version of the correct base image for your functions language. You should regularly update your container from the latest base image and redeploy from the updated version of your container. For more information, see [Creating containerized function apps](functions-how-to-custom-container#creating-containerized-function-apps).

## Prerequisites

Before you begin, you must have the following requirements in place:

Install the

[.NET 8.0 SDK](https://dotnet.microsoft.com/download).Install

[Azure Functions Core Tools](functions-run-local#v2)version 4.0.5198, or a later version.

- Install
[Azure Functions Core Tools](functions-run-local#v2)version 4.x.

- Install a version of
[Node.js](https://nodejs.org/)that is[supported by Azure Functions](functions-reference-node#supported-versions).

- Install a version of Python that is
[supported by Azure Functions](functions-reference-python#supported-python-versions).

- Install the
[.NET 6 SDK](https://dotnet.microsoft.com/download).

Install a version of the

[Java Developer Kit](/en-us/azure/developer/java/fundamentals/java-jdk-long-term-support)that is[supported by Azure Functions](functions-reference-java#supported-versions).Install

[Apache Maven](https://maven.apache.org)version 3.0 or above.

[Azure CLI](/en-us/cli/azure/install-azure-cli)version 2.4 or a later version.

If you don't have an [Azure subscription](../guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing), create an [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

To publish the containerized function app image you create to a container registry, you need a Docker ID and [Docker](https://docs.docker.com/install/) running on your local computer. If you don't have a Docker ID, you can [create a Docker account](https://hub.docker.com/signup).

You also need to complete the [Create a container registry](/en-us/azure/container-registry/container-registry-get-started-portal#create-a-container-registry) section of the Container Registry quickstart to create a registry instance. Make a note of your fully qualified login server name.

## Create and activate a virtual environment

In a suitable folder, run the following commands to create and activate a virtual environment named `.venv`

. Make sure to use one of the [Python versions](functions-reference-python#supported-python-versions) supported by Azure Functions.

```
python -m venv .venv
```


```
source .venv/bin/activate
```


If Python didn't install the venv package on your Linux distribution, run the following command:

```
sudo apt-get install python3-venv
```


You run all subsequent commands in this activated virtual environment.

## Create and test the local functions project

In a terminal or command prompt, run the following command for your chosen language to create a function app project in the current folder:

```
func init --worker-runtime dotnet-isolated --docker
```


```
func init --worker-runtime node --language javascript --docker
```


```
func init --worker-runtime powershell --docker
```


```
func init --worker-runtime python --docker
```


```
func init --worker-runtime node --language typescript --docker
```


In an empty folder, run the following command to generate the Functions project from a [Maven archetype](https://maven.apache.org/guides/introduction/introduction-to-archetypes.html):

```
mvn archetype:generate -DarchetypeGroupId=com.microsoft.azure -DarchetypeArtifactId=azure-functions-archetype -DjavaVersion=8 -Ddocker
```


The `-DjavaVersion`

parameter tells the Functions runtime which version of Java to use. Use `-DjavaVersion=11`

if you want your functions to run on Java 11. When you don't specify `-DjavaVersion`

, Maven defaults to Java 8. For more information, see [Java versions](functions-reference-java#java-versions).

Important

The `JAVA_HOME`

environment variable must be set to the install location of the correct version of the JDK to complete this article.

Maven asks you for values needed to finish generating the project on deployment. Follow the prompts and provide the following information:

| Prompt | Value | Description |
|---|---|---|
groupId |
`com.fabrikam` |
A value that uniquely identifies your project across all projects, following the
|

**artifactId**`fabrikam-functions`

**version**`1.0-SNAPSHOT`

**package**`com.fabrikam.functions`

Type `Y`

or press Enter to confirm.

Maven creates the project files in a new folder named *artifactId*, which in this example is `fabrikam-functions`

.

The `--docker`

option generates a *Dockerfile* for the project, which defines a suitable container for use with Azure Functions and the selected runtime.

Navigate into the project folder:

```
cd fabrikam-functions
```


Use the following command to add a function to your project, where the `--name`

argument is the unique name of your function and the `--template`

argument specifies the function's trigger. `func new`

creates a C# code file in your project.

```
func new --name HttpExample --template "HTTP trigger"
```


Use the following command to add a function to your project, where the `--name`

argument is the unique name of your function and the `--template`

argument specifies the function's trigger. `func new`

creates a subfolder matching the function name that contains a configuration file named *function.json*.

```
func new --name HttpExample --template "HTTP trigger"
```


To test the function locally, start the local Azure Functions runtime host in the root of the project folder.

```
func start
```


```
func start
```


```
npm install
npm start
```


```
mvn clean package
mvn azure-functions:run
```


After you see the `HttpExample`

endpoint written to the output, navigate to that endpoint. You should see a welcome message in the response output.

After you see the `HttpExample`

endpoint written to the output, navigate to `http://localhost:7071/api/HttpExample?name=Functions`

. The browser must display a "hello" message that echoes back `Functions`

, the value supplied to the `name`

query parameter.

Press **Ctrl**+**C** (**Command**+**C** on macOS) to stop the host.

## Build the container image and verify locally

(Optional) Examine the *Dockerfile* in the root of the project folder. The *Dockerfile* describes the required environment to run the function app on Linux. The complete list of supported base images for Azure Functions can be found in the [Azure Functions base image page](https://hub.docker.com/_/microsoft-azure-functions-base).

In the root project folder, run the [docker build](https://docs.docker.com/engine/reference/commandline/build/) command, provide a name as `azurefunctionsimage`

, and tag as `v1.0.0`

. Replace `<DOCKER_ID>`

with your Docker Hub account ID. This command builds the Docker image for the container.

```
docker build --tag <DOCKER_ID>/azurefunctionsimage:v1.0.0 .
```


When the command completes, you can run the new container locally.

To verify the build, run the image in a local container using the [docker run](https://docs.docker.com/engine/reference/commandline/run/) command, replace `<DOCKER_ID>`

again with your Docker Hub account ID, and add the ports argument as `-p 8080:80`

:

```
docker run -p 8080:80 -it <DOCKER_ID>/azurefunctionsimage:v1.0.0
```


After the image starts in the local container, browse to `http://localhost:8080/api/HttpExample`

, which must display the same greeting message as before. Because the HTTP triggered function you created uses anonymous authorization, you can call the function running in the container without having to obtain an access key. For more information, see [authorization keys](functions-bindings-http-webhook-trigger#authorization-keys).

After the image starts in the local container, browse to `http://localhost:8080/api/HttpExample?name=Functions`

, which must display the same "hello" message as before. Because the HTTP triggered function you created uses anonymous authorization, you can call the function running in the container without having to obtain an access key. For more information, see [authorization keys](functions-bindings-http-webhook-trigger#authorization-keys).

After verifying the function app in the container, press **Ctrl**+**C** (**Command**+**C** on macOS) to stop execution.

## Publish the container image to a registry

To make your container image available for deployment to a hosting environment, you must push it to a container registry. As a security best practice, you should use an Azure Container Registry instance and enforce managed identity-based connections. Docker Hub requires you to authenticate using shared secrets, which make your deployments more vulnerable.

Azure Container Registry is a private registry service for building, storing, and managing container images and related artifacts. You should use a private registry service for publishing your containers to Azure services.

Use this command to sign in to your registry instance using your current Azure credentials:

`az acr login --name <REGISTRY_NAME>`

In the previous command, replace

`<REGISTRY_NAME>`

with the name of your Container Registry instance.Use this command to tag your image with the fully qualified name of your registry login server:

`docker tag <DOCKER_ID>/azurefunctionsimage:v1.0.0 <LOGIN_SERVER>/azurefunctionsimage:v1.0.0`

Replace

`<LOGIN_SERVER>`

with the fully qualified name of your registry login server and`<DOCKER_ID>`

with your Docker ID.Use this command to push the container to your registry instance:

`docker push <LOGIN_SERVER>/azurefunctionsimage:v1.0.0`


## Create supporting Azure resources for your function

Before you can deploy your container to Azure, you need to create three resources:

- A
[resource group](../azure-resource-manager/management/overview), which is a logical container for related resources. - A
[Storage account](../storage/common/storage-account-create), which is used to maintain state and other information about your functions. - An Azure Container Apps environment with a Log Analytics workspace.
- A user-assigned managed identity, which enables your function app to securely connect to Azure resources without using shared secrets. Connections to both the Azure Storage account and to the Azure Container Registry instance are instead made using Microsoft Entra authentication with the identity, which is recommended for this scenario.

Note

Docker Hub doesn't support managed identities.

Use these commands to create your required Azure resources:

If necessary, sign in to Azure:

The

command signs you into your Azure account. Use`az login`

`az account set`

when you have more than one subscription associated with your account.Run the following command to update the Azure CLI to the latest version:

`az upgrade`

If your version of Azure CLI isn't the latest version, an installation begins. The manner of upgrade depends on your operating system. You can proceed after the upgrade is complete.

Run the following commands that upgrade the Azure Container Apps extension and register namespaces required by Container Apps:

`az extension add --name containerapp --upgrade -y az provider register --namespace Microsoft.Web az provider register --namespace Microsoft.App az provider register --namespace Microsoft.OperationalInsights`

Create a resource group named

`AzureFunctionsContainers-rg`

.`az group create --name AzureFunctionsContainers-rg --location eastus`

This

command creates a resource group in the East US region. If you instead want to use a region near you, using an available region code returned from the`az group create`

[az account list-locations](/en-us/cli/azure/account#az-account-list-locations)command. You must modify subsequent commands to use your custom region instead of`eastus`

.Create Azure Container App environment with workload profiles enabled.

`az containerapp env create --name MyContainerappEnvironment --enable-workload-profiles --resource-group AzureFunctionsContainers-rg --location eastus`

This command can take a few minutes to complete.

Create a general-purpose storage account in your resource group and region, without shared key access.

`az storage account create --name <STORAGE_NAME> --location eastus --resource-group AzureFunctionsContainers-rg --sku Standard_LRS --allow-blob-public-access false --allow-shared-key-access false`

The

command creates the storage account that can only be accessed by using Microsoft Entra-authenticated identities that have been granted permissions to specific resources.`az storage account create`

In the previous example, replace

`<STORAGE_NAME>`

with a name that is appropriate to you and unique in Azure Storage. Storage names must contain 3 to 24 characters numbers and lowercase letters only.`Standard_LRS`

specifies a general-purpose account[supported by Functions](storage-considerations#storage-account-requirements).Create a managed identity and use the returned

`principalId`

to grant it both access to your storage account and pull permissions in your registry instance.`principalId=$(az identity create --name <USER_IDENTITY_NAME> --resource-group AzureFunctionsContainers-rg --location eastus --query principalId -o tsv) acrId=$(az acr show --name <REGISTRY_NAME> --query id --output tsv) az role assignment create --assignee-object-id $principalId --assignee-principal-type ServicePrincipal --role acrpull --scope $acrId storageId=$(az storage account show --resource-group AzureFunctionsContainers-rg --name <STORAGE_NAME> --query 'id' -o tsv) az role assignment create --assignee-object-id $principalId --assignee-principal-type ServicePrincipal --role "Storage Blob Data Owner" --scope $storageId`

The

command creates a user-assigned managed identity and the`az identity create`

commands adds your identity to the required roles. Replace`az role assignment create`

`<REGISTRY_NAME>`

,`<USER_IDENTITY_NAME>`

, and`<STORAGE_NAME>`

with the name your existing container registry, the name for your managed identity, and the storage account name, respectively. The managed identity can now be used by an app to access both the storage account and Azure Container Registry without using shared secrets.

## Create and configure a function app on Azure with the image

A function app on Azure manages the execution of your functions in your Azure Container Apps environment. In this section, you use the Azure resources from the previous section to create a function app from an image in a container registry in a Container Apps environment. You also configure the new environment with a connection string to the required Azure Storage account.

Use the [ az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create) command to create a function app in the new managed environment backed by Azure Container Apps. In

[, the](/en-us/cli/azure/functionapp#az-functionapp-create)

`az functionapp create`

`--environment`

parameter specifies the Container Apps environment.Tip

To make sure that your function app uses a managed identity-based connection to your registry instance, don't set the `--image`

parameter in `az functionapp create`

. When you set `--image`

to the fully qualified name of your image in the repository, shared secret credentials are obtained from your registry and stored in app settings.

First you must get the fully qualified ID value of your user-assigned managed identity with pull access to the registry, and then use the [ az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create) command to create a function app using the default image and with this identity assigned to it.

```
UAMI_RESOURCE_ID=$(az identity show --name $uami_name --resource-group $group --query id -o tsv)
az functionapp create --name <APP_NAME> --storage-account <STORAGE_NAME> --environment MyContainerappEnvironment --workload-profile-name "Consumption" --resource-group AzureFunctionsContainers-rg --functions-version 4 --assign-identity $UAMI_RESOURCE_ID
```


In [ az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create), the

`--assign-identity`

assigns your managed identity to the new app. Because you didn't set the `--image`

parameter in `az functionapp create`

, the application is created using a placeholder image.In this example, replace `<APP_NAME>`

, `<STORAGE_NAME>`

, and `<USER_IDENTITY_NAME>`

with a name for your new function app as well as the name of your storage account and the identity.

Finally, you must update the [ linuxFxVersion](functions-app-settings#linuxfxversion) site setting to the fully qualified name of your image in the repository. You must also update the

[and](functions-app-settings#acrusemanagedidentitycreds)

`acrUseManagedIdentityCreds`

[site settings so that managed identities are used when obtaining the image from the registry.](functions-app-settings#acrusermanagedidentityid)

`acrUserManagedIdentityID`

```
UAMI_RESOURCE_ID=$(az identity show --name <USER_IDENTITY_NAME> --resource-group AzureFunctionsContainers-rg --query id -o tsv)
az resource patch --resource-group AzureFunctionsContainers-rg --name <APP_NAME> --resource-type "Microsoft.Web/sites" --properties "{ \"siteConfig\": { \"linuxFxVersion\": \"DOCKER|<REGISTRY_NAME>.azurecr.io/azurefunctionsimage:v1.0.0\", \"acrUseManagedIdentityCreds\": true, \"acrUserManagedIdentityID\":\"$UAMI_RESOURCE_ID\", \"appSettings\": [{\"name\": \"DOCKER_REGISTRY_SERVER_URL\", \"value\": \"<REGISTRY_NAME>.azurecr.io\"}]}}"
```


In addition to the required site settings, the [ az resource patch](/en-us/cli/azure/resource#az-resource-patch) command also updates the

[app setting to the URL of your registry server.](functions-app-settings#docker_registry_server_url)

`DOCKER_REGISTRY_SERVER_URL`

In this example, replace `<APP_NAME>`

, `<REGISTRY_NAME>`

, and `<USER_IDENTITY_NAME>`

with the names of your function app, container registry, and identity, respectively.

Specifying `--workload-profile-name "Consumption"`

creates your app in an environment using the default `Consumption`

workload profile, which costs the same as running in a Container Apps Consumption plan. When you first create the function app, it pulls the initial image from your registry.

## Update application settings

To enable the Functions host to connect to the default storage account using shared secrets, you must replace the `AzureWebJobsStorage`

connection string setting with an equivalent setting that uses the user-assigned managed identity to connect to the storage account.

Remove the existing

`AzureWebJobsStorage`

connection string setting:`az functionapp config appsettings delete --name <APP_NAME> --resource-group AzureFunctionsContainers-rg --setting-names AzureWebJobsStorage`

The

[az functionapp config appsettings delete](/en-us/cli/azure/functionapp/config/appsettings#az-functionapp-config-appsettings-delete)command removes this setting from your app. Replace`<APP_NAME>`

with the name of your function app.Add equivalent settings, with an

`AzureWebJobsStorage__`

prefix, that define a user-assigned managed identity connection to the default storage account:`clientId=$(az identity show --name <USER_IDENTITY_NAME> --resource-group AzureFunctionsContainers-rg --query 'clientId' -o tsv) az functionapp config appsettings set --name <APP_NAME> --resource-group AzureFunctionsContainers-rg --settings AzureWebJobsStorage__accountName=<STORAGE_NAME> AzureWebJobsStorage__credential=managedidentity AzureWebJobsStorage__clientId=$clientId`

In this example, replace

`<APP_NAME>`

,`<USER_IDENTITY_NAME>`

,`<STORAGE_NAME>`

with your function app name, the name of your identity, and the storage account name, respectively.

At this point, your functions are running in a Container Apps environment, with the required application settings already added. When needed, you can add other settings in your functions app in the standard way for Functions. For more information, see [Use application settings](functions-how-to-use-azure-function-app-settings#settings).

Tip

When you make subsequent changes to your function code, you need to rebuild the container, republish the image to the registry, and update the function app with the new image version. For more information, see [Update an image in the registry](functions-how-to-custom-container#update-an-image-in-the-registry)

## Verify your functions on Azure

With the image deployed to your function app in Azure, you can now invoke the function through HTTP requests.

Run the following

command to get the URL of your new function:`az functionapp function show`

`az functionapp function show --resource-group AzureFunctionsContainers-rg --name <APP_NAME> --function-name HttpExample --query invokeUrlTemplate`

Replace

`<APP_NAME>`

with the name of your function app.

- Use the URL you just obtained to call the
`HttpExample`

function endpoint, appending the query string`?name=Functions`

.

- Use the URL you just obtained to call the
`HttpExample`

function endpoint.

When you navigate to this URL, the browser must display similar output as when you ran the function locally.

The request URL should look something like this:

`https://myacafunctionapp.kindtree-796af82b.eastus.azurecontainerapps.io/api/httpexample?name=functions`


`https://myacafunctionapp.kindtree-796af82b.eastus.azurecontainerapps.io/api/httpexample`


## Clean up resources

If you want to continue working with Azure Function using the resources you created in this article, you can leave all those resources in place.

When you're done working with this function app deployment, delete the `AzureFunctionsContainers-rg`

resource group to clean up all the resources in that group:

```
az group delete --name AzureFunctionsContainers-rg
```

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/event-driven-scaling -->

# Event-driven scaling in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In the Consumption, Flex Consumption, and Premium plans, Azure Functions scales resources by adding more instances based on the number of events that trigger a function.

The way in which your function app scales depends on the hosting plan:

**Consumption plan:**Each instance of the Functions host in the Consumption plan is limited, typically to 1.5 GB of memory and one CPU. An instance of the host supports the entire function app. As such, all functions within a function app that share resources in an instance are scaled at the same time. When function apps share the same Consumption plan, they're still scaled independently.**Flex Consumption plan:**The plan uses a deterministic per-function scaling strategy. Each function is scaled independently, except for HTTP, Blob, and Durable Functions triggered functions which scale in their own groups. For more information, see[Per-function scaling](#per-function-scaling). These instances are then scaled based on the concurrency of your requests.**Premium plan:**The specific size of the Premium plan determines the available memory and CPU for all apps in that plan on that instance. The plan scales out its instances based on the scaling needs of the apps in the plan, and the apps scale within the plan as needed.

Function code files are stored on Azure Files shares on the function's main storage account. When you delete the main storage account of the function app, the function code files are deleted and can't be recovered.

## Runtime scaling

Azure Functions uses a component called the *scale controller* to monitor the rate of events and determine whether to scale out or scale in. The scale controller uses heuristics for each trigger type. For example, when you're using an Azure Queue storage trigger, it uses [target-based scaling](functions-target-based-scaling).

The unit of scale for Azure Functions is the function app. When the function app is scaled out, more resources are allocated to run multiple instances of the Azure Functions host. Conversely, as compute demand is reduced, the scale controller removes function host instances. The number of instances is eventually "scaled in" when no functions are running within a function app.


## Cold Start

Should your function app become idle for a few minutes, the platform might decide to scale the number of instances on which your app runs down to zero. The next request has the added latency of scaling from zero to one. This latency is referred to as a *cold start*. The number of dependencies required by your function app can affect the cold start time. Cold start is more of an issue for synchronous operations, such as HTTP triggers that must return a response. If cold starts are impacting your functions, consider using a plan other than the Consumption. The other plans offer these strategies to mitigate or eliminate cold starts:

[Premium plan](functions-premium-plan#eliminate-cold-starts): supports both prewarmed instances and always ready instances, with a minimum of one instance.[Flex Consumption plan](flex-consumption-plan#always-ready-instances): supports an optional number of always ready instances, which can be defined on a per instance scaling basis.[Dedicated plan](dedicated-plan#always-on): the plan itself doesn't scale dynamically, but you can run your app continuously when the**Always on**setting is enabled.

## Understanding scaling behaviors

Scaling can vary based on several factors, and apps scale differently based on the triggers and language selected. There are a few intricacies of scaling behaviors to be aware of:

**Maximum instances:**A single function app only scales out to a[maximum allowed by the plan](functions-scale#scale). However, a single instance[can process more than one message or request at a time](functions-concurrency#concurrency-in-azure-functions). You can[specify a lower maximum](#limit-scale-out)to throttle scale as required.**New instance rate:**For HTTP triggers, new instances are allocated, at most, once per second. For non-HTTP triggers, new instances are allocated, at most, once every 30 seconds. Scaling is faster when running in a[Premium plan](functions-premium-plan).**Target-based scaling:**Target-based scaling provides a fast and intuitive scaling model for customers. Currently, this scaling method is supported for Service Bus queues and topics, Storage queues, Event Hubs, Apache Kafka, and Azure Cosmos DB extensions. Make sure to review[target-based scaling](functions-target-based-scaling)to understand their scaling behavior.**Per-function scaling:**With some notable exceptions, functions running in the Flex Consumption plan scale on independent instances. The exceptions include HTTP triggers and Blob storage (Event Grid) triggers. Each of these trigger types scale together as a group on the same instances. Likewise, the triggers of all Durable Functions also share instances and scale together. For more information, see[per-function scaling](#per-function-scaling).**Maximum monitored triggers:**Currently, the scale controller can only monitor up to 100 triggers to making scaling decisions. When your app has more than 100 event-based triggers, scale decisions are made based on only the first 100 triggers that execute. For more information, see[Best practices and patterns for scalable apps](#best-practices-and-patterns-for-scalable-apps).

## Limit scale-out

You might decide to restrict the maximum number of instances an app can use for scale-out. This limitation is most common for cases where a downstream component like a database has limited throughput. For the maximum scale limits when running the various hosting plans, see [Scale limits](functions-scale#scale).

### Flex Consumption plan

By default, apps running in a Flex Consumption plan have limit of `100`

overall instances. Currently the lowest maximum instance count value is `40`

, and the highest supported maximum instance count value is `1000`

. When you use the [ az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create) command to create a function app in the Flex Consumption plan, use the

`--maximum-instance-count`

parameter to set this maximum instance count for of your app.While you can change the maximum instance count of Flex Consumption apps up to 1000, the quota limit for your apps is reached before reaching that number. Review [Regional subscription memory quotas](flex-consumption-plan#regional-subscription-memory-quotas) for more details.

This example creates an app with a maximum instance count of `200`

:

```
az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage <STORAGE_ACCOUNT_NAME> --runtime <LANGUAGE_RUNTIME> --runtime-version <RUNTIME_VERSION> --flexconsumption-location <REGION> --maximum-instance-count 200
```


This example uses the [ az functionapp scale config set](/en-us/cli/azure/functionapp/scale/config#az-functionapp-scale-config-set) command to change the maximum instance count for an existing app to

`150`

:```
az functionapp scale config set --resource-group <RESOURCE_GROUP> --name <APP_NAME> --maximum-instance-count 150
```


### Consumption/Premium plans

In a Consumption or Elastic Premium plan, you can specify a lower maximum limit for your app by modifying the value of the `functionAppScaleLimit`

site configuration setting. The `functionAppScaleLimit`

can be set to `0`

or `null`

for unrestricted, or a valid value between `1`

and the app maximum.

```
az resource update --resource-type Microsoft.Web/sites -g <RESOURCE_GROUP> -n <FUNCTION_APP-NAME>/config/web --set properties.functionAppScaleLimit=<SCALE_LIMIT>
```


## Scale-in behaviors

Event-driven scaling automatically reduces capacity when demand for your functions is reduced. It makes this reduction by draining instances of their current function executions and then removes those instances. This behavior is logged as drain mode. The grace period for functions that are currently executing can extend up to 10 minutes for Consumption plan apps and up to 60 minutes for Flex Consumption and Premium plan apps. Event-driven scaling and this behavior don't apply to Dedicated plan apps.

The following considerations apply for scale-in behaviors:

- For apps running on Windows in a Consumption plan, only apps created after May 2021 have drain mode behaviors enabled by default.
- To enable graceful shutdown for functions using the Service Bus trigger, use version 4.2.0 or a later version of the
[Service Bus Extension](functions-bindings-service-bus).

## Per-function scaling

*Applies only to the Flex Consumption plan*.

The [Flex Consumption plan](flex-consumption-plan) is unique in that it implements a *per-function scaling* behavior. In per-function scaling, except for HTTP triggers, Blob (Event Grid) triggers, and Durable Functions, all other function trigger types in your app scale on independent instances. HTTP triggers in your app all scale together as a group on the same instances, as do all Blob (Event Grid), and all Durable Functions triggers, which have their own shared instances.

Consider a function app hosted by a Flex Consumption plan that has the following functions:

| function1 | function2 | function3 | function4 | function5 | function6 | function7 |
|---|---|---|---|---|---|---|
| HTTP trigger | HTTP trigger | Orchestration trigger (Durable) | Activity trigger (Durable) | Service Bus trigger | Service Bus trigger | Event Hubs trigger |

In this example:

- The two HTTP triggered functions (
`function1`

and`function2`

) both run together on their own instances and scale together according to[HTTP concurrency settings](flex-consumption-how-to#set-http-concurrency-limits). - The two Durable functions (
`function3`

and`function4`

) both run together on their own instances and scale together based on[configured concurrency throttles](durable/durable-functions-perf-and-scale#concurrency-throttles). - The Service bus triggered function
`function5`

runs in its own and is scaled independently according to the[target-based scaling rules for Service Bus queues and topics](functions-target-based-scaling#service-bus-queues-and-topics). - The Service bus triggered function
`function6`

runs in its own and is scaled independently according to the[target-based scaling rules for Service Bus queues and topics](functions-target-based-scaling#service-bus-queues-and-topics). - The Event Hubs trigger (
`function7`

) runs in its own instances and is scaled independently according to the[target-based scaling rules for Event Hubs](functions-target-based-scaling#event-hubs).

## Best practices and patterns for scalable apps

There are many aspects of a function app that impacts how it scales, including host configuration, runtime footprint, and resource efficiency. For more information, see the [scalability section of the performance considerations article](performance-reliability#scalability-best-practices). You should also be aware of how connections behave as your function app scales. For more information, see [How to manage connections in Azure Functions](manage-connections).

If your app has more than 100 functions that use event-based triggers, consider breaking the app into one or more apps, where each app has less than 100 event-based functions.

For more information on scaling in Python and Node.js, see the **Scaling and performance** section of the [Azure Functions Python developer guide](functions-reference-python) and the **Scaling and concurrency** section of the [Azure Functions Node.js developer guide](functions-reference-node).

## Next steps

To learn more, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr-input-state -->

# Dapr State input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Dapr state input binding allows you to read Dapr state during a function execution.

For information on setup and configuration details of the Dapr extension, see the [Dapr extension overview](functions-bindings-dapr).

## Example

A C# function can be created using one of the following C# modes:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).```
[FunctionName("StateInputBinding")]
public static IActionResult Run(
[HttpTrigger(AuthorizationLevel.Function, "get", Route = "state/{key}")] HttpRequest req,
[DaprState("statestore", Key = "{key}")] string state,
ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
return new OkObjectResult(state);
}
```


The following example creates a `"RetrieveOrder"`

function using the `DaprStateInput`

binding with the [ DaprServiceInvocationTrigger](functions-bindings-dapr-trigger-svc-invoke):

```
@FunctionName("RetrieveOrder")
public String run(
@DaprServiceInvocationTrigger(
methodName = "RetrieveOrder")
String payload,
@DaprStateInput(
stateStore = "%StateStoreName%",
key = "order")
String product,
final ExecutionContext context)
```


In the following example, the Dapr invoke input binding is added as an `extraInput`

and paired with an HTTP trigger, which is registered by the `app`

object:

```
const { app, trigger } = require('@azure/functions');
app.generic('StateInputBinding', {
trigger: trigger.generic({
type: 'httpTrigger',
authLevel: 'anonymous',
methods: ['GET'],
route: "state/{key}",
name: "req"
}),
extraInputs: [daprStateInput],
handler: async (request, context) => {
context.log("Node HTTP trigger function processed a request.");
const daprStateInputValue = context.extraInputs.get(daprStateInput);
// print the fetched state value
context.log(daprStateInputValue);
return daprStateInputValue;
}
});
```


The following examples show Dapr triggers in a *function.json* file and PowerShell code that uses those bindings.

Here's the *function.json* file for `daprState`

:

```
{
"bindings":
{
"type": "daprState",
"direction": "in",
"key": "order",
"stateStore": "%StateStoreName%",
"name": "order"
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
$payload, $order
)
# C# function processed a CreateNewOrder request from the Dapr Runtime.
Write-Host "PowerShell function processed a RetrieveOrder request from the Dapr Runtime."
# Convert the object to a JSON-formatted string with ConvertTo-Json
$jsonString = $order | ConvertTo-Json
Write-Host "$jsonString"
```


The following example shows a Dapr State input binding, which uses the [v2 Python programming model](functions-reference-python). To use the `daprState`

binding alongside the `daprServiceInvocationTrigger`

in your Python function app code:

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="RetrieveOrder")
@app.dapr_service_invocation_trigger(arg_name="payload", method_name="RetrieveOrder")
@app.dapr_state_input(arg_name="data", state_store="statestore", key="order")
def main(payload, data: str) :
# Function should be invoked with this command: dapr invoke --app-id functionapp --method RetrieveOrder --data '{}'
logging.info('Python function processed a RetrieveOrder request from the Dapr Runtime.')
logging.info(data)
```


## Attributes

In the [in-process model](functions-dotnet-class-library), use the `DaprState`

to read Dapr state into your function, which supports these parameters:

| Parameter | Description |
|---|---|
StateStore |
The name of the state store to retrieve state. |
Key |
The name of the key to retrieve from the specified state store. |

## Annotations

The `DaprStateInput`

annotation allows you to read Dapr state into your function.

| Element | Description |
|---|---|
stateStore |
The name of the Dapr state store. |
key |
The state store key value. |

## Configuration

The following table explains the binding configuration properties that you set in the code.

| Property | Description |
|---|---|
stateStore |
The name of the state store. |
key |
The name of the key to retrieve from the specified state store. |

The following table explains the binding configuration properties that you set in the function.json file.

| function.json property | Description |
|---|---|
key |
The name of the key to retrieve from the specified state store. |
stateStore |
The name of the state store. |

See the [Example section](#example) for complete examples.

## Usage

To use the Dapr state input binding, start by setting up a Dapr state store component. You can learn more about which component to use and how to set it up in the official Dapr documentation.

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-proxies -->

# Azure Functions proxies (legacy)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions is an essential compute service that you use to build serverless REST-based APIs. HTTP triggers expose REST endpoints that can be called by your clients, like browsers, mobile apps, and other backend services. With [native support for routes](functions-bindings-http-webhook-trigger#customize-the-http-endpoint), a single HTTP triggered function can expose a highly functional REST API. Functions also provides its own basic key-based authorization scheme to help limit access only to specific clients. For more information, see [Azure Functions HTTP trigger](functions-bindings-http-webhook-trigger)

In some scenarios, you may need your API to support a more complex set of REST behaviors. For example, you may need to combine multiple HTTP function endpoints into a single API. You might also want to pass requests through to one or more backend REST-based services. Finally, your APIs might require a higher-degree of security that lets you monetize its use.

To build more complex and robust APIs based on your functions, you should instead use the comprehensive API services provided by [Azure API Management](../api-management/api-management-key-concepts).
API Management uses a policy-based model to let you control routing, security, and OpenAPI integration. It also supports advanced policies like rate limiting monetization.

Important

Azure Functions proxies is a legacy feature for [versions 1.x through 3.x](functions-versions) of the Azure Functions runtime. Proxies can be re-enabled temporarily in version 4.x for you to successfully upgrade your function apps to the latest runtime version. As soon as possible, you should switch to integrating your function apps with Azure API Management. API Management lets you take advantage of a more complete set of features for defining, securing, managing, and monetizing your Functions-based APIs. For more information, see [API Management integration](functions-proxies#api-management-integration).

To learn how to temporarily re-enable proxies support in Functions version 4.x, see [Re-enable proxies in Functions v4.x](legacy-proxies#re-enable-proxies-in-functions-v4x).

## Moving from Functions Proxies to API Management

When moving from Functions Proxies to using API Management, you must integrate your function app with an API Management instance, and then configure the API Management instance to behave like the previous proxy. The following section provides links to the relevant articles that help you succeed in using API Management with Azure Functions.

If you have challenges moving from proxies or if Azure API Management doesn't address your specific scenarios, post a request in the [API Management feedback forum](https://feedback.azure.com/d365community/forum/e808a70c-ff24-ec11-b6e6-000d3a4f0858).

## API Management integration

API Management lets you import an existing function app. After import, each HTTP triggered function endpoint becomes an API that you can modify and manage. After import, you can also use API Management to generate an OpenAPI definition file for your APIs. During import, any endpoints with an `admin`

[authorization level](functions-bindings-http-webhook-trigger#http-auth) are ignored. For more information about using API Management with Functions, see the following articles:

| Article | Description |
|---|---|
|

[Create serverless APIs in Visual Studio using Azure Functions and API Management integration](openapi-apim-integrate-visual-studio)[OpenAPI extension](https://github.com/Azure/azure-functions-openapi-extension). The OpenAPI extension lets you define your .NET APIs by applying attributes directly to your C# code.[Quickstart: Create a new Azure API Management service instance by using the Azure portal](../api-management/get-started-create-service-instance)[Import an Azure function app as an API in Azure API Management](../api-management/import-function-app-as-api)After you have your function app endpoints exposed by using API Management, the following articles provide general information about how to manage your Functions-based APIs in the API Management instance.

| Article | Description |
|---|---|
|

[Policies in Azure API Management](../api-management/api-management-howto-policies)[API Management policy reference](../api-management/api-management-policies)[API Management policy samples](https://github.com/Azure/api-management-policy-snippets)## Legacy Functions Proxies

The legacy [Functions Proxies feature](legacy-proxies) also provides a set of basic API functionality for version 3.x and older version of the Functions runtime.

Important

Azure Functions proxies is a legacy feature for [versions 1.x through 3.x](functions-versions) of the Azure Functions runtime. Proxies can be re-enabled temporarily in version 4.x for you to successfully upgrade your function apps to the latest runtime version. As soon as possible, you should switch to integrating your function apps with Azure API Management. API Management lets you take advantage of a more complete set of features for defining, securing, managing, and monetizing your Functions-based APIs. For more information, see [API Management integration](functions-proxies#api-management-integration).

To learn how to temporarily re-enable proxies support in Functions version 4.x, see [Re-enable proxies in Functions v4.x](legacy-proxies#re-enable-proxies-in-functions-v4x).

Some basic hints for how to perform equivalent tasks using API Management have been added to the [Functions Proxies article](legacy-proxies). We don't currently have documentation or tools to help you migrate an existing Functions Proxies implementation to API Management.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-serverless-api -->

# Azure Functions proxies (legacy)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions is an essential compute service that you use to build serverless REST-based APIs. HTTP triggers expose REST endpoints that can be called by your clients, like browsers, mobile apps, and other backend services. With [native support for routes](functions-bindings-http-webhook-trigger#customize-the-http-endpoint), a single HTTP triggered function can expose a highly functional REST API. Functions also provides its own basic key-based authorization scheme to help limit access only to specific clients. For more information, see [Azure Functions HTTP trigger](functions-bindings-http-webhook-trigger)

In some scenarios, you may need your API to support a more complex set of REST behaviors. For example, you may need to combine multiple HTTP function endpoints into a single API. You might also want to pass requests through to one or more backend REST-based services. Finally, your APIs might require a higher-degree of security that lets you monetize its use.

To build more complex and robust APIs based on your functions, you should instead use the comprehensive API services provided by [Azure API Management](../api-management/api-management-key-concepts).
API Management uses a policy-based model to let you control routing, security, and OpenAPI integration. It also supports advanced policies like rate limiting monetization.

Important

Azure Functions proxies is a legacy feature for [versions 1.x through 3.x](functions-versions) of the Azure Functions runtime. Proxies can be re-enabled temporarily in version 4.x for you to successfully upgrade your function apps to the latest runtime version. As soon as possible, you should switch to integrating your function apps with Azure API Management. API Management lets you take advantage of a more complete set of features for defining, securing, managing, and monetizing your Functions-based APIs. For more information, see [API Management integration](functions-proxies#api-management-integration).

To learn how to temporarily re-enable proxies support in Functions version 4.x, see [Re-enable proxies in Functions v4.x](legacy-proxies#re-enable-proxies-in-functions-v4x).

## Moving from Functions Proxies to API Management

When moving from Functions Proxies to using API Management, you must integrate your function app with an API Management instance, and then configure the API Management instance to behave like the previous proxy. The following section provides links to the relevant articles that help you succeed in using API Management with Azure Functions.

If you have challenges moving from proxies or if Azure API Management doesn't address your specific scenarios, post a request in the [API Management feedback forum](https://feedback.azure.com/d365community/forum/e808a70c-ff24-ec11-b6e6-000d3a4f0858).

## API Management integration

API Management lets you import an existing function app. After import, each HTTP triggered function endpoint becomes an API that you can modify and manage. After import, you can also use API Management to generate an OpenAPI definition file for your APIs. During import, any endpoints with an `admin`

[authorization level](functions-bindings-http-webhook-trigger#http-auth) are ignored. For more information about using API Management with Functions, see the following articles:

| Article | Description |
|---|---|
|

[Create serverless APIs in Visual Studio using Azure Functions and API Management integration](openapi-apim-integrate-visual-studio)[OpenAPI extension](https://github.com/Azure/azure-functions-openapi-extension). The OpenAPI extension lets you define your .NET APIs by applying attributes directly to your C# code.[Quickstart: Create a new Azure API Management service instance by using the Azure portal](../api-management/get-started-create-service-instance)[Import an Azure function app as an API in Azure API Management](../api-management/import-function-app-as-api)After you have your function app endpoints exposed by using API Management, the following articles provide general information about how to manage your Functions-based APIs in the API Management instance.

| Article | Description |
|---|---|
|

[Policies in Azure API Management](../api-management/api-management-howto-policies)[API Management policy reference](../api-management/api-management-policies)[API Management policy samples](https://github.com/Azure/api-management-policy-snippets)## Legacy Functions Proxies

The legacy [Functions Proxies feature](legacy-proxies) also provides a set of basic API functionality for version 3.x and older version of the Functions runtime.

Important

Azure Functions proxies is a legacy feature for [versions 1.x through 3.x](functions-versions) of the Azure Functions runtime. Proxies can be re-enabled temporarily in version 4.x for you to successfully upgrade your function apps to the latest runtime version. As soon as possible, you should switch to integrating your function apps with Azure API Management. API Management lets you take advantage of a more complete set of features for defining, securing, managing, and monetizing your Functions-based APIs. For more information, see [API Management integration](functions-proxies#api-management-integration).

To learn how to temporarily re-enable proxies support in Functions version 4.x, see [Re-enable proxies in Functions v4.x](legacy-proxies#re-enable-proxies-in-functions-v4x).

Some basic hints for how to perform equivalent tasks using API Management have been added to the [Functions Proxies article](legacy-proxies). We don't currently have documentation or tools to help you migrate an existing Functions Proxies implementation to API Management.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/ -->

# Azure Functions documentation

Azure Functions is a managed platform-as-a-service (PaaS) provider that provides event-driven and scheduled compute resources for Azure cloud services. You can focus on the code that matters most to you and Functions handles the rest. Functions can provide scalable and serverless hosting for your code projects written in the most productive language for you. You can use Functions to build web APIs, respond to database changes, process IoT streams, manage message queues, and more.

## About Azure Functions

### Overview

### Concept

## Create your first function

### Get started

### Quickstart

## Languages

### Concept

### How-To Guide

## AI integration

### Concept

### Tutorial

### Reference

## Develop functions

### Concept

-
[Azure Functions developer guide](functions-reference) -
[Azure Functions triggers and bindings concepts](functions-triggers-bindings) -
[Code and test Azure Functions locally](functions-develop-local)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-cli-samples -->

# Azure CLI Samples

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

These end-to-end Azure CLI scripts are provided to help you learn how to provision and managing the Azure resources required by Azure Functions. You must use the [Azure Functions Core Tools](functions-run-local) to create actual Azure Functions code projects from the command line on your local computer and deploy code to these Azure resources. For a complete end-to-end example of developing and deploying from the command line using both Core Tools and the Azure CLI, see one of these language-specific command line quickstarts:

The following table includes links to bash scripts that you can use to create and manage the Azure resources required by Azure Functions using the Azure CLI.

| Create app | Description |
|---|---|
|

[Create a serverless Python function app](scripts/functions-cli-create-serverless-python)[Create a function app in a scalable Premium plan](scripts/functions-cli-create-premium-plan)[Create a function app in a dedicated (App Service) plan](scripts/functions-cli-create-app-service-plan)| Integrate | Description |
|---|---|
|

[Create a function app and connect to an Azure Cosmos DB](scripts/functions-cli-create-function-app-connect-to-cosmos-db)[Create a Python function app and mount an Azure Files share](scripts/functions-cli-mount-files-storage-linux)| Continuous deployment | Description |
|---|---|
|

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/consumption-plan -->

# Azure Functions Consumption plan hosting

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you're using the Consumption plan, instances of the Azure Functions host are dynamically added and removed based on the number of incoming events.

Important

After 30 September 2028, the option to host your function app on Linux in a Consumption plan is retired. To avoid disruptions, migrate your existing Consumption plan apps that run on Linux to the [Flex Consumption plan](flex-consumption-plan) before that date. Apps running on Windows in a Consumption plan aren't affected by this change.
For more information, see the [Linux Consumption plan retirement notice](https://go.microsoft.com/fwlink/?linkid=2335809).

The Consumption plan scales automatically, even during periods of high load. When running functions in a Consumption plan, you're charged for compute resources only when your functions are running. On a Consumption plan, a function execution times out after a configurable period of time.

Tip

The Flex Consumption plan is now the recommended serverless hosting plan for Azure Functions. It offers faster scaling, reduced cold starts, private networking, and more control over performance and cost. For more information, see [Flex Consumption plan](flex-consumption-plan).

## Billing

Billing is based on number of executions, execution time, and memory used. Usage is aggregated across all functions within a function app. For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).

To learn more about how to estimate costs when running in a Consumption plan, see [Understanding Consumption plan costs](functions-consumption-costs).

## Create a Consumption plan function app

When you create a function app in the Azure portal, the Consumption plan is the default. When using APIs to create your function app, you don't have to first create an App Service plan as you do with Premium and Dedicated plans.

In Consumption plan hosting, each function app typically runs in its own plan. In the Azure portal or in code, you might also see the Consumption plan referred to as `Dynamic`

or `Y1`

.

Use the following links to learn how to create a serverless function app in a Consumption plan, either programmatically or in the Azure portal:

You can also create function apps in a Consumption plan when you publish a Functions project from [Visual Studio Code](how-to-create-function-vs-code#create-the-function-app-in-azure) or [Visual Studio](functions-create-your-first-function-visual-studio#publish-the-project-to-azure).

## Multiple apps in the same plan

The general recommendation is for each function app to have its own Consumption plan. However, if needed, function apps in the same region can be assigned to the same Consumption plan. Keep in mind that there's a [limit to the number of function apps that can run in a Consumption plan](functions-scale#service-limits). Function apps in the same plan still scale independently of each other.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr-trigger-topic -->

# Dapr Topic trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions can be triggered on a Dapr topic subscription using the following Dapr events.

For information on setup and configuration details of the Dapr extension, see the [Dapr extension overview](functions-bindings-dapr).

## Example

A C# function can be created using one of the following C# modes:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).```
[FunctionName("TransferEventBetweenTopics")]
public static void Run(
[DaprTopicTrigger("%PubSubName%", Topic = "A")] CloudEvent subEvent,
[DaprPublish(PubSubName = "%PubSubName%", Topic = "B")] out DaprPubSubEvent pubEvent,
ILogger log)
{
log.LogInformation("C# function processed a TransferEventBetweenTopics request from the Dapr Runtime.");
pubEvent = new DaprPubSubEvent("Transfer from Topic A: " + subEvent.Data);
}
```


Here's the Java code for subscribing to a topic using the Dapr Topic trigger:

```
@FunctionName("PrintTopicMessage")
public String run(
@DaprTopicTrigger(
pubSubName = "%PubSubName%",
topic = "B")
String payload,
final ExecutionContext context) throws JsonProcessingException {
Logger logger = context.getLogger();
logger.info("Java function processed a PrintTopicMessage request from the Dapr Runtime.");
```


Use the `app`

object to register the `daprTopicTrigger`

:

```
const { app, trigger } = require('@azure/functions');
app.generic('TransferEventBetweenTopics', {
trigger: trigger.generic({
type: 'daprTopicTrigger',
name: "subEvent",
pubsubname: "%PubSubName%",
topic: "A"
}),
return: daprPublishOutput,
handler: async (request, context) => {
context.log("Node function processed a TransferEventBetweenTopics request from the Dapr Runtime.");
context.log(context.triggerMetadata.subEvent.data);
return { payload: context.triggerMetadata.subEvent.data };
}
});
```


The following examples show Dapr triggers in a *function.json* file and PowerShell code that uses those bindings.

Here's the *function.json* file for `daprTopicTrigger`

:

```
{
"bindings": [
{
"type": "daprTopicTrigger",
"pubsubname": "%PubSubName%",
"topic": "B",
"name": "subEvent",
"direction": "in"
}
]
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
$subEvent
)
Write-Host "PowerShell function processed a PrintTopicMessage request from the Dapr Runtime."
# Convert the object to a JSON-formatted string with ConvertTo-Json
$jsonString = $subEvent["data"] | ConvertTo-Json -Compress
Write-Host "Topic B received a message: $jsonString"
```


The following example shows a Dapr Topic trigger, which uses the [v2 Python programming model](functions-reference-python). To use the `daprTopicTrigger`

in your Python function app code:

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="PrintTopicMessage")
@app.dapr_topic_trigger(arg_name="subEvent", pub_sub_name="%PubSubName%", topic="B", route="B")
def main(subEvent) -> None:
logging.info('Python function processed a PrintTopicMessage request from the Dapr Runtime.')
subEvent_json = json.loads(subEvent)
logging.info("Topic B received a message: " + subEvent_json["data"])
```


## Attributes

In the [in-process model](functions-dotnet-class-library), use the `DaprTopicTrigger`

to trigger a Dapr pub/sub binding, which supports the following properties.

| Parameter | Description |
|---|---|
PubSubName |
The name of the Dapr pub/sub. |
Topic |
The name of the Dapr topic. |

## Annotations

The `DaprTopicTrigger`

annotation allows you to create a function that runs when a topic is received.

| Element | Description |
|---|---|
pubSubName |
The name of the Dapr pub/sub. |
topic |
The name of the Dapr topic. |

## Configuration

The following table explains the binding configuration properties that you set in the code.

| Property | Description |
|---|---|
pubsubname |
The name of the Dapr pub/sub component type. |
topic |
Name of the topic. |

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
pubsubname |
The name of the Dapr pub/sub component type. |
topic |
Name of the topic. |

The following table explains the binding configuration properties for `@dapp.dapr_topic_trigger`

that you set in your Python code.

| Property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
pub_sub_name |
The name of the Dapr subscription component type. | ✔️ | ❌ |
topic |
The subscription topic. | ✔️ | ❌ |

See the [Example section](#example) for complete examples.

## Usage

To use a Dapr Topic trigger, start by setting up a Dapr pub/sub component. You can learn more about which component to use and how to set it up in the official Dapr documentation.

To use the `daprTopicTrigger`

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-web-pubsub-output -->

# Azure Web PubSub output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the *Web PubSub* output binding to invoke Azure Web PubSub service to do something. You can send a message to:

- All connected clients
- Connected clients authenticated to a specific user
- Connected clients joined in a specific group
- A specific client connection

The output binding also allows you to manage clients and groups, and grant/revoke permissions targeting specific connectionId with group.

- Add connection to group
- Add user to group
- Remove connection from a group
- Remove user from a group
- Remove user from all groups
- Close all client connections
- Close a specific client connection
- Close connections in a group
- Grant permission of a connection
- Revoke permission of a connection

For information on setup and configuration details, see the [overview](functions-bindings-web-pubsub).

## Example

```
[Function("WebPubSubOutputBinding")]
[WebPubSubOutput(Hub = "<hub>", Connection = "<web_pubsub_connection_name>")]
public static WebPubSubAction Run([HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequestData req)
{
return new SendToAllAction
{
Data = BinaryData.FromString("Hello Web PubSub!"),
DataType = WebPubSubDataType.Text
};
}
```


```
const { app, output } = require('@azure/functions');
const wpsMsg = output.generic({
type: 'webPubSub',
name: 'actions',
hub: '<hub>',
});
app.http('message', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraOutputs: [wpsMsg],
handler: async (request, context) => {
context.extraOutputs.set(wpsMsg, [{
"actionName": "sendToAll",
"data": `Hello world`,
"dataType": `text`
}]);
}
});
```


Note

Complete samples for this language are pending

Note

The Web PubSub extensions for Java is not supported yet.

### WebPubSubAction

`WebPubSubAction`

is the base abstract type of output bindings. The derived types represent the action server want service to invoke.

In C# language, we provide a few static methods under `WebPubSubAction`

to help discover available actions. For example, user can create the `SendToAllAction`

by call `WebPubSubAction.CreateSendToAllAction()`

.

| Derived Class | Properties |
|---|---|
`SendToAllAction` |
Data, DataType, Excluded |
`SendToGroupAction` |
Group, Data, DataType, Excluded |
`SendToUserAction` |
UserId, Data, DataType |
`SendToConnectionAction` |
ConnectionId, Data, DataType |
`AddUserToGroupAction` |
UserId, Group |
`RemoveUserFromGroupAction` |
UserId, Group |
`RemoveUserFromAllGroupsAction` |
UserId |
`AddConnectionToGroupAction` |
ConnectionId, Group |
`RemoveConnectionFromGroupAction` |
ConnectionId, Group |
`CloseAllConnectionsAction` |
Excluded, Reason |
`CloseClientConnectionAction` |
ConnectionId, Reason |
`CloseGroupConnectionsAction` |
Group, Excluded, Reason |
`GrantPermissionAction` |
ConnectionId, Permission, TargetName |
`RevokePermissionAction` |
ConnectionId, Permission, TargetName |

** actionName** is the key parameter to resolve the type. Available actions are listed as follows.

| ActionName | Properties |
|---|---|
`sendToAll` |
Data, DataType, Excluded |
`sendToGroup` |
Group, Data, DataType, Excluded |
`sendToUser` |
UserId, Data, DataType |
`sendToConnection` |
ConnectionId, Data, DataType |
`addUserToGroup` |
UserId, Group |
`removeUserFromGroup` |
UserId, Group |
`removeUserFromAllGroups` |
UserId |
`addConnectionToGroup` |
ConnectionId, Group |
`removeConnectionFromGroup` |
ConnectionId, Group |
`closeAllConnections` |
Excluded, Reason |
`closeClientConnection` |
ConnectionId, Reason |
`closeGroupConnections` |
Group, Excluded, Reason |
`grantPermission` |
ConnectionId, Permission, TargetName |
`revokePermission` |
ConnectionId, Permission, TargetName |

Important

The message data property in the sent message related actions must be `string`

if data type is set to `json`

or `text`

to avoid data conversion ambiguity. Please use `JSON.stringify()`

to convert the json object in need. This is applied to any place using message property, for example, `UserEventResponse.Data`

working with `WebPubSubTrigger`

.

When data type is set to `binary`

, it's allowed to leverage binding naturally supported `dataType`

as `binary`

configured in the `function.json`

, see [Trigger and binding definitions](functions-triggers-bindings?tabs=csharp#trigger-and-binding-definitions) for details.

### Configuration

The following table explains the binding configuration properties that you set in the function.json file and the `WebPubSub`

attribute.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Must be set to `webPubSub` |
direction |
n/a | Must be set to `out` |
name |
n/a | Variable name used in function code for output binding object. |
hub |
Hub | The value must be set to the name of the Web PubSub hub for the function to be triggered. We support set the value in attribute as higher priority, or it can be set in app settings as a global value. |
connection |
Connection | The name of the app setting that contains the Web PubSub Service connection string (defaults to "WebPubSubConnectionString"). |

Important

For optimal security, your function app should use managed identities when connecting to the Web PubSub service instead of using a connection string, which contains a shared secret key. For more information, see [Authorize a managed identity request by using Microsoft Entra ID](../azure-web-pubsub/howto-authorize-from-managed-identity).

## Troubleshooting

### Setting up console logging

You can also easily [enable console logging](https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/core/Azure.Core/samples/Diagnostics.md#logging) if you want to dig deeper into the requests you're making against the service.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-add-output-binding-storage-queue-cli -->

# Connect Azure Functions to Azure Storage using command line tools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you integrate an Azure Storage queue with the function and storage account you created in the previous quickstart article. You achieve this integration by using an *output binding* that writes data from an HTTP request to a message in the queue. Completing this article incurs no extra costs beyond the few USD cents of the previous quickstart. To learn more about bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings).

## Configure your local environment

Before you begin, you must complete the article, [Quickstart: Create an Azure Functions project from the command line](how-to-create-function-azure-cli?pivots=programming-language-csharp). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

Before you begin, you must complete the article, [Quickstart: Create an Azure Functions project from the command line](how-to-create-function-azure-cli?pivots=programming-language-javascript). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

Before you begin, you must complete the article, [Quickstart: Create an Azure Functions project from the command line](how-to-create-function-azure-cli?pivots=programming-language-java). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

Before you begin, you must complete the article, [Quickstart: Create an Azure Functions project from the command line](how-to-create-function-azure-cli?pivots=programming-language-typescript). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

Before you begin, you must complete the article, [Quickstart: Create an Azure Functions project from the command line](how-to-create-function-azure-cli?pivots=programming-language-python). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

Before you begin, you must complete the article, [Quickstart: Create an Azure Functions project from the command line](how-to-create-function-azure-cli?pivots=programming-language-powershell). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

### Retrieve the Azure Storage connection string

Important

This article currently shows how to connect to your Azure Storage account by using the connection string, which contains a shared secret key. Using a connection string makes it easier for you to verify data updates in the storage account. For the best security, you should instead use managed identities when connecting to your storage account. For more information, see [Connections](functions-reference#connections) in the Developer Guide.

Earlier, you created an Azure Storage account for function app's use. The connection string for this account is stored securely in app settings in Azure. By downloading the setting into the *local.settings.json* file, you can use the connection to write to a Storage queue in the same account when running the function locally.

From the root of the project, run the following command, replacing

`<APP_NAME>`

with the name of your function app from the previous step. This command overwrites any existing values in the file.`func azure functionapp fetch-app-settings <APP_NAME>`

Open

*local.settings.json*file and locate the value named`AzureWebJobsStorage`

, which is the Storage account connection string. You use the name`AzureWebJobsStorage`

and the connection string in other sections of this article.

Important

Because the *local.settings.json* file contains secrets downloaded from Azure, always exclude this file from source control. The *.gitignore* file created with a local functions project excludes the file by default.

## Register binding extensions

Except for HTTP and timer triggers, bindings are implemented as extension packages. Run the following [dotnet add package](/en-us/dotnet/core/tools/dotnet-add-package) command in the Terminal window to add the Storage extension package to your project.

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues --prerelease
```


Now, you can add the storage output binding to your project.

## Add an output binding definition to the function

Although a function can have only one trigger, it can have multiple input and output bindings, which lets you connect to other Azure services and resources without writing custom integration code.

When using the [Node.js v4 programming model](functions-reference-node), binding attributes are defined directly in the *./src/functions/HttpExample.js* file. From the previous quickstart, your file already contains an HTTP binding defined by the `app.http`

method.

```
const { app } = require('@azure/functions');
app.http('httpTrigger', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: async (request, context) => {
try {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text());
context.log(`Name: ${name}`);
if (!name) {
return { status: 404, body: 'Not Found' };
}
return { body: `Hello, ${name}!` };
} catch (error) {
context.log(`Error: ${error}`);
return { status: 500, body: 'Internal Server Error' };
}
},
});
```


When using the [Node.js v4 programming model](functions-reference-node), binding attributes are defined directly in the *./src/functions/HttpExample.js* file. From the previous quickstart, your file already contains an HTTP binding defined by the `app.http`

method.

```
import {
app,
HttpRequest,
HttpResponseInit,
InvocationContext,
} from '@azure/functions';
export async function httpTrigger1(
request: HttpRequest,
context: InvocationContext,
): Promise<HttpResponseInit> {
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


You declare these bindings in the *function.json* file in your function folder. From the previous quickstart, your *function.json* file in the *HttpExample* folder contains two bindings in the `bindings`

collection:

When using the [Python v2 programming model](functions-reference-python?pivots=python-mode-decorators), binding attributes are defined directly in the *function_app.py* file as decorators. From the previous quickstart, your *function_app.py* file already contains one decorator-based binding:

```
import azure.functions as func
import logging
app = func.FunctionApp()
@app.function_name(name="HttpTrigger1")
@app.route(route="hello", auth_level=func.AuthLevel.ANONYMOUS)
```


The `route`

decorator adds HttpTrigger and HttpOutput binding to the function, which enables your function be triggered when http requests hit the specified route.

To write to an Azure Storage queue from this function, add the `queue_output`

decorator to your function code:

```
@app.queue_output(arg_name="msg", queue_name="outqueue", connection="AzureWebJobsStorage")
```


In the decorator, `arg_name`

identifies the binding parameter referenced in your code, `queue_name`

is name of the queue that the binding writes to, and `connection`

is the name of an application setting that contains the connection string for the Storage account. In quickstarts you use the same storage account as the function app, which is in the `AzureWebJobsStorage`

setting (from *local.settings.json* file). When the `queue_name`

doesn't exist, the binding creates it on first use.

```
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
```


To write to an Azure Storage queue:

Add an

`extraOutputs`

property to the binding configuration`{ methods: ['GET', 'POST'], extraOutputs: [sendToQueue], // add output binding to HTTP trigger authLevel: 'anonymous', handler: () => {} }`

Add a

`output.storageQueue`

function above the`app.http`

call`const sendToQueue: StorageQueueOutput = output.storageQueue({ queueName: 'outqueue', connection: 'AzureWebJobsStorage', });`


The second binding in the collection is named `res`

. This `http`

binding is an output binding (`out`

) that is used to write the HTTP response.

To write to an Azure Storage queue from this function, add an `out`

binding of type `queue`

with the name `msg`

, as shown in the code below:

```
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
},
{
"type": "queue",
"direction": "out",
"name": "msg",
"queueName": "outqueue",
"connection": "AzureWebJobsStorage"
}
]
}
```


For a `queue`

type, you must specify the name of the queue in `queueName`

and provide the *name* of the Azure Storage connection (from *local.settings.json* file) in `connection`

.

In a C# project, the bindings are defined as binding attributes on the function method. Specific definitions depend on whether your app runs in-process (C# class library) or in an isolated worker process.

Open the *HttpExample.cs* project file and add the following `MultiResponse`

class:

```
public class MultiResponse
{
[QueueOutput("outqueue",Connection = "AzureWebJobsStorage")]
public string[] Messages { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
```


The `MultiResponse`

class allows you to write to a storage queue named `outqueue`

and an HTTP success message. Multiple messages could be sent to the queue because the `QueueOutput`

attribute is applied to a string array.

The `Connection`

property sets the connection string for the storage account. In this case, you could omit `Connection`

because you're already using the default storage account.

In a Java project, the bindings are defined as binding annotations on the function method. The *function.json* file is then autogenerated based on these annotations.

Browse to the location of your function code under *src/main/java*, open the *Function.java* project file, and add the following parameter to the `run`

method definition:

```
@QueueOutput(name = "msg", queueName = "outqueue", connection = "AzureWebJobsStorage") OutputBinding<String> msg
```


The `msg`

parameter is an [ OutputBinding<T>](/en-us/java/api/com.microsoft.azure.functions.outputbinding) type, which represents a collection of strings. These strings are written as messages to an output binding when the function completes. In this case, the output is a storage queue named

`outqueue`

. The connection string for the Storage account is set by the `connection`

method. You pass the application setting that contains the Storage account connection string, rather than passing the connection string itself.The `run`

method definition must now look like the following example:

```
@FunctionName("HttpTrigger-Java")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.FUNCTION)
HttpRequestMessage<Optional<String>> request,
@QueueOutput(name = "msg", queueName = "outqueue", connection = "AzureWebJobsStorage")
OutputBinding<String> msg, final ExecutionContext context) {
...
}
```


For more information on the details of bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings) and [queue output configuration](functions-bindings-storage-queue-output#configuration).

## Add code to use the output binding

With the queue binding defined, you can now update your function to receive the `msg`

output parameter and write messages to the queue.

Update *HttpExample\function_app.py* to match the following code, add the `msg`

parameter to the function definition and `msg.set(name)`

under the `if name:`

statement:

```
import azure.functions as func
import logging
app = func.FunctionApp(http_auth_level=func.AuthLevel.ANONYMOUS)
@app.route(route="HttpExample")
@app.queue_output(arg_name="msg", queue_name="outqueue", connection="AzureWebJobsStorage")
def HttpExample(req: func.HttpRequest, msg: func.Out [func.QueueMessage]) -> func.HttpResponse:
logging.info('Python HTTP trigger function processed a request.')
name = req.params.get('name')
if not name:
try:
req_body = req.get_json()
except ValueError:
pass
else:
name = req_body.get('name')
if name:
msg.set(name)
return func.HttpResponse(f"Hello, {name}. This HTTP triggered function executed successfully.")
else:
return func.HttpResponse(
"This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response.",
status_code=200
)
```


The `msg`

parameter is an instance of the [ azure.functions.Out class](/en-us/python/api/azure-functions/azure.functions.out). The

`set`

method writes a string message to the queue. In this case, it's the `name`

passed to the function in the URL query string.Add code that uses the output binding object on `context.extraOutputs`

to create a queue message. Add this code before the return statement.

```
context.extraOutputs.set(sendToQueue, [msg]);
```


At this point, your function could look as follows:

```
const { app, output } = require('@azure/functions');
const sendToQueue = output.storageQueue({
queueName: 'outqueue',
connection: 'AzureWebJobsStorage',
});
app.http('HttpExample', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraOutputs: [sendToQueue],
handler: async (request, context) => {
try {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text());
context.log(`Name: ${name}`);
if (name) {
const msg = `Name passed to the function ${name}`;
context.extraOutputs.set(sendToQueue, [msg]);
return { body: msg };
} else {
context.log('Missing required data');
return { status: 404, body: 'Missing required data' };
}
} catch (error) {
context.log(`Error: ${error}`);
return { status: 500, body: 'Internal Server Error' };
}
},
});
```


Add code that uses the output binding object on `context.extraOutputs`

to create a queue message. Add this code before the return statement.

```
context.extraOutputs.set(sendToQueue, [msg]);
```


At this point, your function could look as follows:

```
import {
app,
output,
HttpRequest,
HttpResponseInit,
InvocationContext,
StorageQueueOutput,
} from '@azure/functions';
const sendToQueue: StorageQueueOutput = output.storageQueue({
queueName: 'outqueue',
connection: 'AzureWebJobsStorage',
});
export async function HttpExample(
request: HttpRequest,
context: InvocationContext,
): Promise<HttpResponseInit> {
try {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text());
context.log(`Name: ${name}`);
if (name) {
const msg = `Name passed to the function ${name}`;
context.extraOutputs.set(sendToQueue, [msg]);
return { body: msg };
} else {
context.log('Missing required data');
return { status: 404, body: 'Missing required data' };
}
} catch (error) {
context.log(`Error: ${error}`);
return { status: 500, body: 'Internal Server Error' };
}
}
app.http('HttpExample', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: HttpExample,
});
```


Add code that uses the `Push-OutputBinding`

cmdlet to write text to the queue using the `msg`

output binding. Add this code before you set the OK status in the `if`

statement.

```
$outputMsg = $name
Push-OutputBinding -name msg -Value $outputMsg
```


At this point, your function must look as follows:

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
if ($name) {
# Write the $name value to the queue,
# which is the name passed to the function.
$outputMsg = $name
Push-OutputBinding -name msg -Value $outputMsg
$status = [HttpStatusCode]::OK
$body = "Hello $name"
}
else {
$status = [HttpStatusCode]::BadRequest
$body = "Please pass a name on the query string or in the request body."
}
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = $status
Body = $body
})
```


Replace the existing `HttpExample`

class with the following code:

```
[Function("HttpExample")]
public static MultiResponse Run([HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequestData req,
FunctionContext executionContext)
{
var logger = executionContext.GetLogger("HttpExample");
logger.LogInformation("C# HTTP trigger function processed a request.");
var message = "Welcome to Azure Functions!";
var response = req.CreateResponse(HttpStatusCode.OK);
response.Headers.Add("Content-Type", "text/plain; charset=utf-8");
response.WriteString(message);
// Return a response to both HTTP trigger and storage output binding.
return new MultiResponse()
{
// Write a single message.
Messages = new string[] { message },
HttpResponse = response
};
}
}
```


Now, you can use the new `msg`

parameter to write to the output binding from your function code. Add the following line of code before the success response to add the value of `name`

to the `msg`

output binding.

```
msg.setValue(name);
```


When you use an output binding, you don't have to use the Azure Storage SDK code for authentication, getting a queue reference, or writing data. The Functions runtime and queue output binding do those tasks for you.

Your `run`

method must now look like the following example:

```
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@QueueOutput(name = "msg", queueName = "outqueue",
connection = "AzureWebJobsStorage") OutputBinding<String> msg,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
// Parse query parameter
String query = request.getQueryParameters().get("name");
String name = request.getBody().orElse(query);
if (name == null) {
return request.createResponseBuilder(HttpStatus.BAD_REQUEST)
.body("Please pass a name on the query string or in the request body").build();
} else {
// Write the name to the message queue.
msg.setValue(name);
return request.createResponseBuilder(HttpStatus.OK).body("Hello, " + name).build();
}
}
```


## Update the tests

Because the archetype also creates a set of tests, you need to update these tests to handle the new `msg`

parameter in the `run`

method signature.

Browse to the location of your test code under *src/test/java*, open the *Function.java* project file, and replace the line of code under `//Invoke`

with the following code:

```
@SuppressWarnings("unchecked")
final OutputBinding<String> msg = (OutputBinding<String>)mock(OutputBinding.class);
final HttpResponseMessage ret = new Function().run(req, msg, context);
```


Observe that you *don't* need to write any code for authentication, getting a queue reference, or writing data. All these integration tasks are conveniently handled in the Azure Functions runtime and queue output binding.

## Run the function locally

Run your function by starting the local Azure Functions runtime host from the

*LocalFunctionProj*folder.`func start`

Toward the end of the output, the following lines must appear:

Note

If HttpExample doesn't appear as shown above, you likely started the host from outside the root folder of the project. In that case, use

**Ctrl**+**C**to stop the host, go to the project's root folder, and run the previous command again.Copy the URL of your HTTP function from this output to a browser and append the query string

`?name=<YOUR_NAME>`

, making the full URL like`http://localhost:7071/api/HttpExample?name=Functions`

. The browser should display a response message that echoes back your query string value. The terminal in which you started your project also shows log output as you make requests.When you're done, press

`Ctrl + C`and type`y`

to stop the functions host.

## View the message in the Azure Storage queue

You can view the queue in the [Azure portal](../storage/queues/storage-quickstart-queues-portal) or in the [Microsoft Azure Storage Explorer](https://storageexplorer.com/). You can also view the queue in the Azure CLI, as described in the following steps:

Open the function project's

*local.setting.json*file and copy the connection string value. In a terminal or command window, run the following command to create an environment variable named`AZURE_STORAGE_CONNECTION_STRING`

, and paste your specific connection string in place of`<MY_CONNECTION_STRING>`

. (This environment variable means you don't need to supply the connection string to each subsequent command using the`--connection-string`

argument.)`export AZURE_STORAGE_CONNECTION_STRING="<MY_CONNECTION_STRING>"`

(Optional) Use the

command to view the Storage queues in your account. The output from this command must include a queue named`az storage queue list`

`outqueue`

, which was created when the function wrote its first message to that queue.`az storage queue list --output tsv`

Use the

command to read the message from this queue, which should be the value you supplied when testing the function earlier. The command reads and removes the first message from the queue.`az storage message get`

`echo `echo $(az storage message get --queue-name outqueue -o tsv --query '[].{Message:content}') | base64 --decode``

Because the message body is stored

[base64 encoded](functions-bindings-storage-queue-trigger#encoding), the message must be decoded before it's displayed. After you execute`az storage message get`

, the message is removed from the queue. If there was only one message in`outqueue`

, you won't retrieve a message when you run this command a second time and instead get an error.

## Redeploy the project to Azure

After you verify locally that the function wrote a message to the Azure Storage queue, you can redeploy your project to update the endpoint running on Azure.

In the *LocalFunctionsProj* folder, use the [ func azure functionapp publish](functions-run-local#project-file-deployment) command to redeploy the project, replacing

`<APP_NAME>`

with the name of your app.```
func azure functionapp publish <APP_NAME>
```


In the local project folder, use the following Maven command to republish your project:

```
mvn azure-functions:deploy
```


## Verify in Azure

As in the previous quickstart, use a browser or CURL to test the redeployed function.

Examine the Storage queue again, as described in the previous section, to verify that it contains the new message written to the queue.


## Clean up resources

After you finish, use the following command to delete the resource group and all its contained resources to avoid incurring further costs.

```
az group delete --name AzureFunctionsQuickstart-rg
```


## Next steps

You've updated your HTTP triggered function to write data to a Storage queue. Now you can learn more about developing Functions from the command line using Core Tools and Azure CLI:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-add-output-binding-storage-queue-java -->

# Connect Azure Functions to Azure Storage using command line tools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you integrate an Azure Storage queue with the function and storage account you created in the previous quickstart article. You achieve this integration by using an *output binding* that writes data from an HTTP request to a message in the queue. Completing this article incurs no extra costs beyond the few USD cents of the previous quickstart. To learn more about bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings).

## Configure your local environment

Before you begin, you must complete the article, [Quickstart: Create an Azure Functions project from the command line](how-to-create-function-azure-cli?pivots=programming-language-csharp). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

Before you begin, you must complete the article, [Quickstart: Create an Azure Functions project from the command line](how-to-create-function-azure-cli?pivots=programming-language-javascript). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

Before you begin, you must complete the article, [Quickstart: Create an Azure Functions project from the command line](how-to-create-function-azure-cli?pivots=programming-language-java). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

Before you begin, you must complete the article, [Quickstart: Create an Azure Functions project from the command line](how-to-create-function-azure-cli?pivots=programming-language-typescript). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

Before you begin, you must complete the article, [Quickstart: Create an Azure Functions project from the command line](how-to-create-function-azure-cli?pivots=programming-language-python). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

Before you begin, you must complete the article, [Quickstart: Create an Azure Functions project from the command line](how-to-create-function-azure-cli?pivots=programming-language-powershell). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

### Retrieve the Azure Storage connection string

Important

This article currently shows how to connect to your Azure Storage account by using the connection string, which contains a shared secret key. Using a connection string makes it easier for you to verify data updates in the storage account. For the best security, you should instead use managed identities when connecting to your storage account. For more information, see [Connections](functions-reference#connections) in the Developer Guide.

Earlier, you created an Azure Storage account for function app's use. The connection string for this account is stored securely in app settings in Azure. By downloading the setting into the *local.settings.json* file, you can use the connection to write to a Storage queue in the same account when running the function locally.

From the root of the project, run the following command, replacing

`<APP_NAME>`

with the name of your function app from the previous step. This command overwrites any existing values in the file.`func azure functionapp fetch-app-settings <APP_NAME>`

Open

*local.settings.json*file and locate the value named`AzureWebJobsStorage`

, which is the Storage account connection string. You use the name`AzureWebJobsStorage`

and the connection string in other sections of this article.

Important

Because the *local.settings.json* file contains secrets downloaded from Azure, always exclude this file from source control. The *.gitignore* file created with a local functions project excludes the file by default.

## Register binding extensions

Except for HTTP and timer triggers, bindings are implemented as extension packages. Run the following [dotnet add package](/en-us/dotnet/core/tools/dotnet-add-package) command in the Terminal window to add the Storage extension package to your project.

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues --prerelease
```


Now, you can add the storage output binding to your project.

## Add an output binding definition to the function

Although a function can have only one trigger, it can have multiple input and output bindings, which lets you connect to other Azure services and resources without writing custom integration code.

When using the [Node.js v4 programming model](functions-reference-node), binding attributes are defined directly in the *./src/functions/HttpExample.js* file. From the previous quickstart, your file already contains an HTTP binding defined by the `app.http`

method.

```
const { app } = require('@azure/functions');
app.http('httpTrigger', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: async (request, context) => {
try {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text());
context.log(`Name: ${name}`);
if (!name) {
return { status: 404, body: 'Not Found' };
}
return { body: `Hello, ${name}!` };
} catch (error) {
context.log(`Error: ${error}`);
return { status: 500, body: 'Internal Server Error' };
}
},
});
```


When using the [Node.js v4 programming model](functions-reference-node), binding attributes are defined directly in the *./src/functions/HttpExample.js* file. From the previous quickstart, your file already contains an HTTP binding defined by the `app.http`

method.

```
import {
app,
HttpRequest,
HttpResponseInit,
InvocationContext,
} from '@azure/functions';
export async function httpTrigger1(
request: HttpRequest,
context: InvocationContext,
): Promise<HttpResponseInit> {
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


You declare these bindings in the *function.json* file in your function folder. From the previous quickstart, your *function.json* file in the *HttpExample* folder contains two bindings in the `bindings`

collection:

When using the [Python v2 programming model](functions-reference-python?pivots=python-mode-decorators), binding attributes are defined directly in the *function_app.py* file as decorators. From the previous quickstart, your *function_app.py* file already contains one decorator-based binding:

```
import azure.functions as func
import logging
app = func.FunctionApp()
@app.function_name(name="HttpTrigger1")
@app.route(route="hello", auth_level=func.AuthLevel.ANONYMOUS)
```


The `route`

decorator adds HttpTrigger and HttpOutput binding to the function, which enables your function be triggered when http requests hit the specified route.

To write to an Azure Storage queue from this function, add the `queue_output`

decorator to your function code:

```
@app.queue_output(arg_name="msg", queue_name="outqueue", connection="AzureWebJobsStorage")
```


In the decorator, `arg_name`

identifies the binding parameter referenced in your code, `queue_name`

is name of the queue that the binding writes to, and `connection`

is the name of an application setting that contains the connection string for the Storage account. In quickstarts you use the same storage account as the function app, which is in the `AzureWebJobsStorage`

setting (from *local.settings.json* file). When the `queue_name`

doesn't exist, the binding creates it on first use.

```
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
```


To write to an Azure Storage queue:

Add an

`extraOutputs`

property to the binding configuration`{ methods: ['GET', 'POST'], extraOutputs: [sendToQueue], // add output binding to HTTP trigger authLevel: 'anonymous', handler: () => {} }`

Add a

`output.storageQueue`

function above the`app.http`

call`const sendToQueue: StorageQueueOutput = output.storageQueue({ queueName: 'outqueue', connection: 'AzureWebJobsStorage', });`


The second binding in the collection is named `res`

. This `http`

binding is an output binding (`out`

) that is used to write the HTTP response.

To write to an Azure Storage queue from this function, add an `out`

binding of type `queue`

with the name `msg`

, as shown in the code below:

```
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
},
{
"type": "queue",
"direction": "out",
"name": "msg",
"queueName": "outqueue",
"connection": "AzureWebJobsStorage"
}
]
}
```


For a `queue`

type, you must specify the name of the queue in `queueName`

and provide the *name* of the Azure Storage connection (from *local.settings.json* file) in `connection`

.

In a C# project, the bindings are defined as binding attributes on the function method. Specific definitions depend on whether your app runs in-process (C# class library) or in an isolated worker process.

Open the *HttpExample.cs* project file and add the following `MultiResponse`

class:

```
public class MultiResponse
{
[QueueOutput("outqueue",Connection = "AzureWebJobsStorage")]
public string[] Messages { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
```


The `MultiResponse`

class allows you to write to a storage queue named `outqueue`

and an HTTP success message. Multiple messages could be sent to the queue because the `QueueOutput`

attribute is applied to a string array.

The `Connection`

property sets the connection string for the storage account. In this case, you could omit `Connection`

because you're already using the default storage account.

In a Java project, the bindings are defined as binding annotations on the function method. The *function.json* file is then autogenerated based on these annotations.

Browse to the location of your function code under *src/main/java*, open the *Function.java* project file, and add the following parameter to the `run`

method definition:

```
@QueueOutput(name = "msg", queueName = "outqueue", connection = "AzureWebJobsStorage") OutputBinding<String> msg
```


The `msg`

parameter is an [ OutputBinding<T>](/en-us/java/api/com.microsoft.azure.functions.outputbinding) type, which represents a collection of strings. These strings are written as messages to an output binding when the function completes. In this case, the output is a storage queue named

`outqueue`

. The connection string for the Storage account is set by the `connection`

method. You pass the application setting that contains the Storage account connection string, rather than passing the connection string itself.The `run`

method definition must now look like the following example:

```
@FunctionName("HttpTrigger-Java")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.FUNCTION)
HttpRequestMessage<Optional<String>> request,
@QueueOutput(name = "msg", queueName = "outqueue", connection = "AzureWebJobsStorage")
OutputBinding<String> msg, final ExecutionContext context) {
...
}
```


For more information on the details of bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings) and [queue output configuration](functions-bindings-storage-queue-output#configuration).

## Add code to use the output binding

With the queue binding defined, you can now update your function to receive the `msg`

output parameter and write messages to the queue.

Update *HttpExample\function_app.py* to match the following code, add the `msg`

parameter to the function definition and `msg.set(name)`

under the `if name:`

statement:

```
import azure.functions as func
import logging
app = func.FunctionApp(http_auth_level=func.AuthLevel.ANONYMOUS)
@app.route(route="HttpExample")
@app.queue_output(arg_name="msg", queue_name="outqueue", connection="AzureWebJobsStorage")
def HttpExample(req: func.HttpRequest, msg: func.Out [func.QueueMessage]) -> func.HttpResponse:
logging.info('Python HTTP trigger function processed a request.')
name = req.params.get('name')
if not name:
try:
req_body = req.get_json()
except ValueError:
pass
else:
name = req_body.get('name')
if name:
msg.set(name)
return func.HttpResponse(f"Hello, {name}. This HTTP triggered function executed successfully.")
else:
return func.HttpResponse(
"This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response.",
status_code=200
)
```


The `msg`

parameter is an instance of the [ azure.functions.Out class](/en-us/python/api/azure-functions/azure.functions.out). The

`set`

method writes a string message to the queue. In this case, it's the `name`

passed to the function in the URL query string.Add code that uses the output binding object on `context.extraOutputs`

to create a queue message. Add this code before the return statement.

```
context.extraOutputs.set(sendToQueue, [msg]);
```


At this point, your function could look as follows:

```
const { app, output } = require('@azure/functions');
const sendToQueue = output.storageQueue({
queueName: 'outqueue',
connection: 'AzureWebJobsStorage',
});
app.http('HttpExample', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraOutputs: [sendToQueue],
handler: async (request, context) => {
try {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text());
context.log(`Name: ${name}`);
if (name) {
const msg = `Name passed to the function ${name}`;
context.extraOutputs.set(sendToQueue, [msg]);
return { body: msg };
} else {
context.log('Missing required data');
return { status: 404, body: 'Missing required data' };
}
} catch (error) {
context.log(`Error: ${error}`);
return { status: 500, body: 'Internal Server Error' };
}
},
});
```


Add code that uses the output binding object on `context.extraOutputs`

to create a queue message. Add this code before the return statement.

```
context.extraOutputs.set(sendToQueue, [msg]);
```


At this point, your function could look as follows:

```
import {
app,
output,
HttpRequest,
HttpResponseInit,
InvocationContext,
StorageQueueOutput,
} from '@azure/functions';
const sendToQueue: StorageQueueOutput = output.storageQueue({
queueName: 'outqueue',
connection: 'AzureWebJobsStorage',
});
export async function HttpExample(
request: HttpRequest,
context: InvocationContext,
): Promise<HttpResponseInit> {
try {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text());
context.log(`Name: ${name}`);
if (name) {
const msg = `Name passed to the function ${name}`;
context.extraOutputs.set(sendToQueue, [msg]);
return { body: msg };
} else {
context.log('Missing required data');
return { status: 404, body: 'Missing required data' };
}
} catch (error) {
context.log(`Error: ${error}`);
return { status: 500, body: 'Internal Server Error' };
}
}
app.http('HttpExample', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: HttpExample,
});
```


Add code that uses the `Push-OutputBinding`

cmdlet to write text to the queue using the `msg`

output binding. Add this code before you set the OK status in the `if`

statement.

```
$outputMsg = $name
Push-OutputBinding -name msg -Value $outputMsg
```


At this point, your function must look as follows:

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
if ($name) {
# Write the $name value to the queue,
# which is the name passed to the function.
$outputMsg = $name
Push-OutputBinding -name msg -Value $outputMsg
$status = [HttpStatusCode]::OK
$body = "Hello $name"
}
else {
$status = [HttpStatusCode]::BadRequest
$body = "Please pass a name on the query string or in the request body."
}
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = $status
Body = $body
})
```


Replace the existing `HttpExample`

class with the following code:

```
[Function("HttpExample")]
public static MultiResponse Run([HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequestData req,
FunctionContext executionContext)
{
var logger = executionContext.GetLogger("HttpExample");
logger.LogInformation("C# HTTP trigger function processed a request.");
var message = "Welcome to Azure Functions!";
var response = req.CreateResponse(HttpStatusCode.OK);
response.Headers.Add("Content-Type", "text/plain; charset=utf-8");
response.WriteString(message);
// Return a response to both HTTP trigger and storage output binding.
return new MultiResponse()
{
// Write a single message.
Messages = new string[] { message },
HttpResponse = response
};
}
}
```


Now, you can use the new `msg`

parameter to write to the output binding from your function code. Add the following line of code before the success response to add the value of `name`

to the `msg`

output binding.

```
msg.setValue(name);
```


When you use an output binding, you don't have to use the Azure Storage SDK code for authentication, getting a queue reference, or writing data. The Functions runtime and queue output binding do those tasks for you.

Your `run`

method must now look like the following example:

```
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@QueueOutput(name = "msg", queueName = "outqueue",
connection = "AzureWebJobsStorage") OutputBinding<String> msg,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
// Parse query parameter
String query = request.getQueryParameters().get("name");
String name = request.getBody().orElse(query);
if (name == null) {
return request.createResponseBuilder(HttpStatus.BAD_REQUEST)
.body("Please pass a name on the query string or in the request body").build();
} else {
// Write the name to the message queue.
msg.setValue(name);
return request.createResponseBuilder(HttpStatus.OK).body("Hello, " + name).build();
}
}
```


## Update the tests

Because the archetype also creates a set of tests, you need to update these tests to handle the new `msg`

parameter in the `run`

method signature.

Browse to the location of your test code under *src/test/java*, open the *Function.java* project file, and replace the line of code under `//Invoke`

with the following code:

```
@SuppressWarnings("unchecked")
final OutputBinding<String> msg = (OutputBinding<String>)mock(OutputBinding.class);
final HttpResponseMessage ret = new Function().run(req, msg, context);
```


Observe that you *don't* need to write any code for authentication, getting a queue reference, or writing data. All these integration tasks are conveniently handled in the Azure Functions runtime and queue output binding.

## Run the function locally

Run your function by starting the local Azure Functions runtime host from the

*LocalFunctionProj*folder.`func start`

Toward the end of the output, the following lines must appear:

Note

If HttpExample doesn't appear as shown above, you likely started the host from outside the root folder of the project. In that case, use

**Ctrl**+**C**to stop the host, go to the project's root folder, and run the previous command again.Copy the URL of your HTTP function from this output to a browser and append the query string

`?name=<YOUR_NAME>`

, making the full URL like`http://localhost:7071/api/HttpExample?name=Functions`

. The browser should display a response message that echoes back your query string value. The terminal in which you started your project also shows log output as you make requests.When you're done, press

`Ctrl + C`and type`y`

to stop the functions host.

## View the message in the Azure Storage queue

You can view the queue in the [Azure portal](../storage/queues/storage-quickstart-queues-portal) or in the [Microsoft Azure Storage Explorer](https://storageexplorer.com/). You can also view the queue in the Azure CLI, as described in the following steps:

Open the function project's

*local.setting.json*file and copy the connection string value. In a terminal or command window, run the following command to create an environment variable named`AZURE_STORAGE_CONNECTION_STRING`

, and paste your specific connection string in place of`<MY_CONNECTION_STRING>`

. (This environment variable means you don't need to supply the connection string to each subsequent command using the`--connection-string`

argument.)`export AZURE_STORAGE_CONNECTION_STRING="<MY_CONNECTION_STRING>"`

(Optional) Use the

command to view the Storage queues in your account. The output from this command must include a queue named`az storage queue list`

`outqueue`

, which was created when the function wrote its first message to that queue.`az storage queue list --output tsv`

Use the

command to read the message from this queue, which should be the value you supplied when testing the function earlier. The command reads and removes the first message from the queue.`az storage message get`

`echo `echo $(az storage message get --queue-name outqueue -o tsv --query '[].{Message:content}') | base64 --decode``

Because the message body is stored

[base64 encoded](functions-bindings-storage-queue-trigger#encoding), the message must be decoded before it's displayed. After you execute`az storage message get`

, the message is removed from the queue. If there was only one message in`outqueue`

, you won't retrieve a message when you run this command a second time and instead get an error.

## Redeploy the project to Azure

After you verify locally that the function wrote a message to the Azure Storage queue, you can redeploy your project to update the endpoint running on Azure.

In the *LocalFunctionsProj* folder, use the [ func azure functionapp publish](functions-run-local#project-file-deployment) command to redeploy the project, replacing

`<APP_NAME>`

with the name of your app.```
func azure functionapp publish <APP_NAME>
```


In the local project folder, use the following Maven command to republish your project:

```
mvn azure-functions:deploy
```


## Verify in Azure

As in the previous quickstart, use a browser or CURL to test the redeployed function.

Examine the Storage queue again, as described in the previous section, to verify that it contains the new message written to the queue.


## Clean up resources

After you finish, use the following command to delete the resource group and all its contained resources to avoid incurring further costs.

```
az group delete --name AzureFunctionsQuickstart-rg
```


## Next steps

You've updated your HTTP triggered function to write data to a Storage queue. Now you can learn more about developing Functions from the command line using Core Tools and Azure CLI:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-blob-output -->

# Azure Blob storage output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The output binding allows you to modify and delete blob storage data in an Azure Function.

For information on setup and configuration details, see the [overview](functions-bindings-storage-blob).

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

The following example is a [C# function](dotnet-isolated-process-guide) that runs in an isolated worker process and uses a blob trigger with both blob input and blob output blob bindings. The function is triggered by the creation of a blob in the *test-samples-trigger* container. It reads a text file from the *test-samples-input* container and creates a new text file in an output container based on the name of the triggered file.

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.Logging;
namespace SampleApp
{
public static class BlobFunction
{
[Function(nameof(BlobFunction))]
[BlobOutput("test-samples-output/{name}-output.txt")]
public static string Run(
[BlobTrigger("test-samples-trigger/{name}")] string myTriggerItem,
[BlobInput("test-samples-input/sample1.txt")] string myBlob,
FunctionContext context)
{
var logger = context.GetLogger("BlobFunction");
logger.LogInformation("Triggered Item = {myTriggerItem}", myTriggerItem);
logger.LogInformation("Input Item = {myBlob}", myBlob);
// Blob Output
return "blob-output content";
}
}
}
```


This section contains the following examples:

#### HTTP trigger, using OutputBinding (Java)

The following example shows a Java function that uses the `HttpTrigger`

annotation to receive a parameter containing the name of a file in a blob storage container. The `BlobInput`

annotation then reads the file and passes its contents to the function as a `byte[]`

. The `BlobOutput`

annotation binds to `OutputBinding outputItem`

, which is then used by the function to write the contents of the input blob to the configured storage container.

```
@FunctionName("copyBlobHttp")
@StorageAccount("Storage_Account_Connection_String")
public HttpResponseMessage copyBlobHttp(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@BlobInput(
name = "file",
dataType = "binary",
path = "samples-workitems/{Query.file}")
byte[] content,
@BlobOutput(
name = "target",
path = "myblob/{Query.file}-CopyViaHttp")
OutputBinding<String> outputItem,
final ExecutionContext context) {
// Save blob to outputItem
outputItem.setValue(new String(content, StandardCharsets.UTF_8));
// build HTTP response with size of requested blob
return request.createResponseBuilder(HttpStatus.OK)
.body("The size of \"" + request.getQueryParameters().get("file") + "\" is: " + content.length + " bytes")
.build();
}
```


#### Queue trigger, using function return value (Java)

The following example shows a Java function that uses the `QueueTrigger`

annotation to receive a message containing the name of a file in a blob storage container. The `BlobInput`

annotation then reads the file and passes its contents to the function as a `byte[]`

. The `BlobOutput`

annotation binds to the function return value, which is then used by the runtime to write the contents of the input blob to the configured storage container.

```
@FunctionName("copyBlobQueueTrigger")
@StorageAccount("Storage_Account_Connection_String")
@BlobOutput(
name = "target",
path = "myblob/{queueTrigger}-Copy")
public String copyBlobQueue(
@QueueTrigger(
name = "filename",
dataType = "string",
queueName = "myqueue-items")
String filename,
@BlobInput(
name = "file",
path = "samples-workitems/{queueTrigger}")
String content,
final ExecutionContext context) {
context.getLogger().info("The content of \"" + filename + "\" is: " + content);
return content;
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@BlobOutput`

annotation on function parameters whose value would be written to an object in blob storage. The parameter type should be `OutputBinding<T>`

, where `T`

is any native Java type or a POJO.

The following example shows a queue triggered [TypeScript function](functions-reference-node?tabs=typescript) that makes a copy of a blob. The function is triggered by a queue message that contains the name of the blob to copy. The new blob is named *{originalblobname}-Copy*.

```
import { app, input, InvocationContext, output } from '@azure/functions';
const blobInput = input.storageBlob({
path: 'samples-workitems/{queueTrigger}',
connection: 'MyStorageConnectionAppSetting',
});
const blobOutput = output.storageBlob({
path: 'samples-workitems/{queueTrigger}-Copy',
connection: 'MyStorageConnectionAppSetting',
});
export async function storageQueueTrigger1(queueItem: unknown, context: InvocationContext): Promise<unknown> {
return context.extraInputs.get(blobInput);
}
app.storageQueue('storageQueueTrigger1', {
queueName: 'myqueue-items',
connection: 'MyStorageConnectionAppSetting',
extraInputs: [blobInput],
return: blobOutput,
handler: storageQueueTrigger1,
});
```


The following example shows a queue triggered [JavaScript function](functions-reference-node) that makes a copy of a blob. The function is triggered by a queue message that contains the name of the blob to copy. The new blob is named *{originalblobname}-Copy*.

```
const { app, input, output } = require('@azure/functions');
const blobInput = input.storageBlob({
path: 'samples-workitems/{queueTrigger}',
connection: 'MyStorageConnectionAppSetting',
});
const blobOutput = output.storageBlob({
path: 'samples-workitems/{queueTrigger}-Copy',
connection: 'MyStorageConnectionAppSetting',
});
app.storageQueue('storageQueueTrigger1', {
queueName: 'myqueue-items',
connection: 'MyStorageConnectionAppSetting',
extraInputs: [blobInput],
return: blobOutput,
handler: (queueItem, context) => {
return context.extraInputs.get(blobInput);
},
});
```


The following example demonstrates how to create a copy of an incoming blob as the output from a [PowerShell function](functions-reference-powershell).

In the function's configuration file (*function.json*), the `trigger`

metadata property is used to specify the output blob name in the `path`

properties.

Note

To avoid infinite loops, make sure your input and output paths are different.

```
{
"bindings": [
{
"name": "myInputBlob",
"path": "data/{trigger}",
"connection": "MyStorageConnectionAppSetting",
"direction": "in",
"type": "blobTrigger"
},
{
"name": "myOutputBlob",
"type": "blob",
"path": "data/copy/{trigger}",
"connection": "MyStorageConnectionAppSetting",
"direction": "out"
}
],
"disabled": false
}
```


Here's the PowerShell code:

```
# Input bindings are passed in via param block.
param([byte[]] $myInputBlob, $TriggerMetadata)
Write-Host "PowerShell Blob trigger function Processed blob Name: $($TriggerMetadata.Name)"
Push-OutputBinding -Name myOutputBlob -Value $myInputBlob
```


The following example shows blob input and output bindings. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

The code creates a copy of a blob.

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="BlobOutput1")
@app.route(route="file")
@app.blob_input(arg_name="inputblob",
path="sample-workitems/test.txt",
connection="<BLOB_CONNECTION_SETTING>")
@app.blob_output(arg_name="outputblob",
path="newblob/test.txt",
connection="<BLOB_CONNECTION_SETTING>")
def main(req: func.HttpRequest, inputblob: str, outputblob: func.Out[str]):
logging.info(f'Python Queue trigger function processed {len(inputblob)} bytes')
outputblob.set(inputblob)
return "ok"
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attribute to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#blob-output).

The `BlobOutputAttribute`

constructor takes the following parameters:

| Parameter | Description |
|---|---|
BlobPath |
The path to the blob. |
Connection |
The name of an app setting or setting collection that specifies how to connect to Azure Blobs. See
|

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using decorators, the following properties on the `blob_input`

and `blob_output`

decorators define the Blob Storage triggers:

| Property | Description |
|---|---|
`arg_name` |
The name of the variable that represents the blob in function code. |
`path` |
The path to the blob For the `blob_input` decorator, it's the blob read. For the `blob_output` decorator, it's the output or copy of the input blob. |
`connection` |
The storage account connection string. |
`dataType` |
For dynamically typed languages, specifies the underlying data type. Possible values are `string` , `binary` , or `stream` . For more detail, refer to the
|

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

The `@BlobOutput`

attribute gives you access to the blob that triggered the function. If you use a byte array with the attribute, set `dataType`

to `binary`

. Refer to the [output example](#example) for details.

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `output.storageBlob()`

method.

| Property | Description |
|---|---|
path |
The path to the blob container. |
connection |
The name of an app setting or setting collection that specifies how to connect to Azure Blobs. See
|

The following table explains the binding configuration properties that you set in the *function.json* file.

| Property | Description |
|---|---|
type |
Must be set to `blob` . |
direction |
Must be set to `out` for an output binding. Exceptions are noted in the
|
name |
The name of the variable that represents the blob in function code. Set to `$return` to reference the function return value. |
path |
The path to the blob container. |
connection |
The name of an app setting or setting collection that specifies how to connect to Azure Blobs. See
|

See the [Example section](#example) for complete examples.

## Usage

The binding types supported by blob output depend on the extension package version and the C# modality used in your function app.

When you want the function to write to a single blob, the blob output binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The blob content as a string. Use when the blob content is simple text. |
`byte[]` |
The bytes of the blob content. |
| JSON serializable types | An object representing the content of a JSON blob. Functions attempts to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write to multiple blobs, the blob output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single blob output binding types |
An array containing content for multiple blobs. Each entry represents the content of one blob. |

For other output scenarios, create and use a [BlobClient](/en-us/dotnet/api/azure.storage.blobs.blobclient) or [BlobContainerClient](/en-us/dotnet/api/azure.storage.blobs.blobcontainerclient) with other types from [Azure.Storage.Blobs](/en-us/dotnet/api/azure.storage.blobs) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

Binding to `string`

, or `Byte[]`

is only recommended when the blob size is small. This is recommended because the entire blob contents are loaded into memory. For most blobs, use a `Stream`

or `BlobClient`

type. For more information, see [Concurrency and memory usage](functions-bindings-storage-blob-trigger#memory-usage-and-concurrency).

If you get an error message when trying to bind to one of the Storage SDK types, make sure that you have a reference to [the correct Storage SDK version](functions-bindings-storage-blob#tabpanel_2_functionsv1_in-process).

You can also use the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) to specify the storage account to use. You can do this when you need to use a different storage account than other functions in the library. The constructor takes the name of an app setting that contains a storage connection string. The attribute can be applied at the parameter, method, or class level. The following example shows class level and method level:

```
[StorageAccount("ClassLevelStorageAppSetting")]
public static class AzureFunctions
{
[FunctionName("BlobTrigger")]
[StorageAccount("FunctionLevelStorageAppSetting")]
public static void Run( //...
{
....
}
```


The storage account to use is determined in the following order:

- The
`BlobTrigger`

attribute's`Connection`

property. - The
`StorageAccount`

attribute applied to the same parameter as the`BlobTrigger`

attribute. - The
`StorageAccount`

attribute applied to the function. - The
`StorageAccount`

attribute applied to the class. - The default storage account for the function app, which is defined in the
`AzureWebJobsStorage`

application setting.

The `@BlobOutput`

attribute gives you access to the blob that triggered the function. If you use a byte array with the attribute, set `dataType`

to `binary`

. Refer to the [output example](#example) for details.

Access the blob data via a parameter that matches the name designated by binding's name parameter in the *function.json* file.

You can declare function parameters as the following types to write out to blob storage:

- Strings as
`func.Out[str]`

- Streams as
`func.Out[func.InputStream]`


Refer to the [output example](#example) for details.

## Connections

The `connection`

property is a reference to environment configuration that specifies how the app should connect to Azure Blobs. It may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections).

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

To obtain a connection string, follow the steps shown at [Manage storage account access keys](../storage/common/storage-account-keys-manage). The connection string must be for a general-purpose storage account, not a [Blob storage account](../storage/common/storage-account-overview#types-of-storage-accounts).

This connection string should be stored in an application setting with a name matching the value specified by the `connection`

property of the binding configuration.

If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name here. For example, if you set `connection`

to "MyStorage", the Functions runtime looks for an app setting that is named "AzureWebJobsMyStorage". If you leave `connection`

empty, the Functions runtime uses the default Storage connection string in the app setting that is named `AzureWebJobsStorage`

.

### Identity-based connections

If you're using [version 5.x or higher of the extension](functions-bindings-storage-blob#install-extension) ([bundle 3.x or higher](functions-bindings-storage-blob?tabs=extensionv3#install-bundle) for non-.NET language stacks), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). To use an identity, you define settings under a common prefix that maps to the `connection`

property in the trigger and binding configuration.

If you're setting `connection`

to "AzureWebJobsStorage", see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity). For all other connections, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Blob Service URI | `<CONNECTION_NAME_PREFIX>__serviceUri` 1 |
The data plane URI of the blob service to which you're connecting, using the HTTPS scheme. | https://<storage_account_name>.blob.core.windows.net |

1 `<CONNECTION_NAME_PREFIX>__blobServiceUri`

can be used as an alias. If the connection configuration will be used by a blob trigger, `blobServiceUri`

must also be accompanied by `queueServiceUri`

. See below.

The `serviceUri`

form can't be used when the overall connection configuration is to be used across blobs, queues, and/or tables. The URI can only designate the blob service. As an alternative, you can provide a URI specifically for each service, allowing a single connection to be used. If both versions are provided, the multi-service form is used. To configure the connection for multiple services, instead of `<CONNECTION_NAME_PREFIX>__serviceUri`

, set:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Blob Service URI | `<CONNECTION_NAME_PREFIX>__blobServiceUri` |
The data plane URI of the blob service to which you're connecting, using the HTTPS scheme. | https://<storage_account_name>.blob.core.windows.net |
Queue Service URI (required for blob triggers2) |
`<CONNECTION_NAME_PREFIX>__queueServiceUri` |
The data plane URI of a queue service, using the HTTPS scheme. This value is only needed for blob triggers. | https://<storage_account_name>.queue.core.windows.net |

2 The blob trigger handles failure across multiple retries by writing [poison blobs](functions-bindings-storage-blob-trigger#poison-blobs) to a queue. In the `serviceUri`

form, the `AzureWebJobsStorage`

connection is used. However, when specifying `blobServiceUri`

, a queue service URI must also be provided with `queueServiceUri`

. It's recommended that you use the service from the same storage account as the blob service. You also need to make sure the trigger can read and write messages in the configured queue service by assigning a role like [Storage Queue Data Contributor](../role-based-access-control/built-in-roles#storage-queue-data-contributor).

Other properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

You need to create a role assignment that provides access to your blob container at runtime. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) aren't sufficient. The following table shows built-in roles that are recommended when using the Blob Storage extension in normal operation. Your application may require further permissions based on the code you write.

| Binding type | Example built-in roles |
|---|---|
| Trigger |
and
1Extra permissions must also be granted to the AzureWebJobsStorage connection. 2 |

[Storage Blob Data Reader](../role-based-access-control/built-in-roles#storage-blob-data-reader)[Storage Blob Data Owner](../role-based-access-control/built-in-roles#storage-blob-data-owner)1 The blob trigger handles failure across multiple retries by writing [poison blobs](functions-bindings-storage-blob-trigger#poison-blobs) to a queue on the storage account specified by the connection.

2 The AzureWebJobsStorage connection is used internally for blobs and queues that enable the trigger. If it's configured to use an identity-based connection, it needs extra permissions beyond the default requirement. The required permissions are covered by the [Storage Blob Data Owner](../role-based-access-control/built-in-roles#storage-blob-data-owner), [Storage Queue Data Contributor](../role-based-access-control/built-in-roles#storage-queue-data-contributor), and [Storage Account Contributor](../role-based-access-control/built-in-roles#storage-account-contributor) roles. To learn more, see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity).

## Exceptions and return codes

| Binding | Reference |
|---|---|
| Blob |
|
