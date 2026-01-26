---
merged_at: 2026-01-26T23:29:57.717466
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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
<!-- Source: N/A -->

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
<!-- Source: N/A -->

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
