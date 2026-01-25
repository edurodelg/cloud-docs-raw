---
merged_at: 2026-01-25T15:41:11.650784
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-deploy-container-apps__python-scale-performance-reference_analyze-tel_f0a70c.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-deploy-container-apps.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-deploy-container-apps -->

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

<!-- DOCUMENTO FUSIONADO: _python-scale-performance-reference_analyze-telemetry-data.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: python-scale-performance-reference.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/python-scale-performance-reference -->

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

<!-- DOCUMENTO FUSIONADO: analyze-telemetry-data.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/analyze-telemetry-data -->

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

<!-- DOCUMENTO FUSIONADO: _functions-add-output-binding-storage-queue-cli_functions-add-output-binding-sto_a92a2e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-add-output-binding-storage-queue-cli.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-add-output-binding-storage-queue-cli -->

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

<!-- DOCUMENTO FUSIONADO: functions-add-output-binding-storage-queue-java.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-add-output-binding-storage-queue-java -->

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
