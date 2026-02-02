---
merged_at: 2026-02-02T16:24:03.463588
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/recover-python-functions -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/configure-networking-how-to -->

# How to use a secured storage account with Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions requires an Azure Storage account when you create a function app instance. This default storage account is used by the Functions runtime to maintain the health of your function app. For more information, see [Storage considerations for Azure Functions](storage-considerations). This article shows you how to use a secured storage account as the default storage account. For an in-depth tutorial on how to create your function app with inbound and outbound access restrictions, see the [Integrate with a virtual network](functions-create-vnet) tutorial. To learn more about Azure Functions and networking, see [Azure Functions networking options](functions-networking-options).

## Restrict your storage account to a virtual network

When you create a function app, you either create a new storage account or link to an existing one. Keep these considerations in mind when working with secured storage account.

- To create a function app that uses an existing secured storage account as the default storage account, you must create your app either in the
[Azure portal](https://portal.azure.com)or by using[ARM template](functions-infrastructure-as-code?tabs=json&pivots=premium-plan#secured-deployments)or[Bicep](functions-infrastructure-as-code?tabs=bicep&pivots=premium-plan#secured-deployments)deployments. - When using a secured storage account with a dynamic scale plan, you should host your functions in the
[Flex Consumption plan](flex-consumption-plan). This plan supports both secured storage accounts and managed identity-based connections to storage, which is the most secure connection option. - All tiers of both the
[Dedicated (App Service) plan](dedicated-plan)and the[Elastic Premium plan](functions-premium-plan)also support secure storage accounts. However, there are trade-offs when using managed identities to connect from a Premium plan app. For more information, see[Create an app without Azure Files](storage-considerations#create-an-app-without-azure-files). - The
[Consumption plan](consumption-plan)doesn't support virtual networks, so you can't connect to a secured storage account when running in the Consumption plan. To take advantage of serverless function hosting, you should instead recreate your app to run in Flex Consumption plan. - This article currently shows you how to create a function app in a Premium plan that connects to a secured storage account using the storage account connection string. To provide the best protection of storage account credentials, you should instead use managed identities when connecting to a storage account. Instead follow the
[Quickstart: Create and deploy functions to Azure Functions using the Azure Developer CLI](create-first-function-azure-developer-cli)to create a function app in the Flex Consumption plan that connects to a new secured storage account using managed identities. - For a list of all restrictions on storage accounts, see
[Storage account requirements](storage-considerations#storage-account-requirements).

## Secure storage during function app creation

You can create a function app, along with a new storage account that is secured behind a virtual network. The following sections show you how to create these resources by using either the Azure portal or by using deployment templates.

Complete the steps in [Create a function app in a Premium plan](functions-create-vnet#create-a-function-app-in-a-premium-plan). This section of the virtual networking tutorial shows you how to create a function app that connects to storage over private endpoints.

Note

When you create your function app in the Azure portal, you can also choose an existing secured storage account in the **Storage** tab. However, you must configure the appropriate networking on the function app so that it can connect through the virtual network used to secure the storage account. If you don't have permissions to configure networking or you haven't fully prepared your network, select **Configure networking after creation** in the **Networking** tab. You can configure networking for your new function app in the portal under **Settings** > **Networking**.

## Secure storage for an existing function app

When you have an existing function app, you can directly configure networking on the storage account being used by the app. However, this process results in your function app being down while you configure networking and while your function app restarts.

To minimize downtime, you can instead swap-out an existing storage account for a new, secured storage account.

### 1. Enable virtual network integration

As a prerequisite, you need to enable virtual network integration for your function app:

Choose a function app with a storage account that doesn't have service endpoints or private endpoints enabled.

[Enable virtual network integration](functions-networking-options#enable-virtual-network-integration)for your function app.

### 2. Create a secured storage account

Set up a secured storage account for your function app:

[Create a second storage account](../storage/common/storage-account-create). This storage account is the secured storage account for your function app to use instead of its original unsecured storage account. You can also use an existing storage account not already being used by Functions.Save the connection string for this storage account to use later.

[Create a file share](../storage/files/storage-how-to-create-file-share#create-a-file-share)in the new storage account. For your convenience, you can use the same file share name from your original storage account. Otherwise, if you use a new file share name, you must update your app setting.Secure the new storage account in one of the following ways:

[Create a private endpoint](../storage/common/storage-private-endpoints#creating-a-private-endpoint). As you set up your private endpoint connection, create private endpoints for the`file`

,`blob`

and`table`

subresources. For Durable Functions, you must also make`queue`

subresources accessible through private endpoints. If you're using a custom or on-premises Domain Name System (DNS) server,[configure your DNS server](../storage/common/storage-private-endpoints#dns-changes-for-private-endpoints)to resolve to the new private endpoints.[Restrict traffic to specific subnets](../storage/common/storage-network-security#grant-access-from-a-virtual-network). Ensure your function app is network integrated with an allowed subnet and that the subnet has only one of these service endpoints defined:`Microsoft.Storage`

: use when your app is in the same region as your virtual network.`Microsoft.Storage.Global`

: use when your app is in a different region than your virtual network.


Copy the file and blob content from the current storage account used by the function app to the newly secured storage account and file share.

[AzCopy](../storage/common/storage-use-azcopy-blobs-copy)and[Azure Storage Explorer](https://techcommunity.microsoft.com/t5/azure-developer-community-blog/azure-tips-and-tricks-how-to-move-azure-storage-blobs-between/ba-p/3545304)are common methods. If you use Azure Storage Explorer, you might need to allow your client IP address access to your storage account's firewall.

Now you're ready to configure your function app to communicate with the newly secured storage account.

### 3. Enable application and configuration routing

Note

These configuration steps are required only for the [Elastic Premium](functions-premium-plan) and [Dedicated (App Service)](dedicated-plan) hosting plans.
The [Flex Consumption plan](flex-consumption-plan) doesn't require site settings to configure networking.

You're now ready to route your function app's traffic to go through the virtual network:

Enable

[application routing](../app-service/overview-vnet-integration#application-routing)to route your app's traffic to the virtual network:In your function app, expand

**Settings**, and then select**Networking**. In the**Networking**page, under**Outbound traffic configuration**, select the subnet associated with your virtual network integration.In the new page, under

**Application routing**, select**Outbound internet traffic**.

If your app uses an Azure Files share, enable

[content share routing](../app-service/overview-vnet-integration#content-share)by selecting**Content storage**under**Configuration routing**. This allows your app to communicate with Azure Files using the virtual network.

Note

You must take special care when routing to the content share in a storage account shared by multiple function apps in the same plan. For more information, see [Consistent routing through virtual networks](storage-considerations#consistent-routing-through-virtual-networks) in the Storage considerations article.

### 4. Update application settings

Finally, you need to update your application settings to point to the new secure storage account:

In your function app, expand

**Settings**, and then select**Environment variables**.In the

**App settings**tab, update the following settings by selecting each setting, editing it, and then selecting**Apply**:Setting name Value Comment `AzureWebJobsStorage`

Storage connection string Use the connection string for your new secured storage account, which you saved earlier. `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

Storage connection string Use the connection string for your new secured storage account, which you saved earlier. Only relevant if your app is using Azure Files. `WEBSITE_CONTENTSHARE`

File share Use the name of the file share created in the secured storage account where the project deployment files reside. Only relevant if your app is using Azure Files. Select

**Apply**, and then**Confirm**to save the new application settings in the function app. This causes the function app to restart.

After the function app finishes restarting, it connects to the secured storage account.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-scenarios -->

# Azure Functions scenarios

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Often, you build systems that react to a series of critical events. Whether you're building a web API, responding to database changes, or processing event streams or messages, you can use Azure Functions to implement these systems.

In many cases, a function [integrates with an array of cloud services](functions-triggers-bindings) to provide feature-rich implementations. The following list shows common (but by no means exhaustive) scenarios for Azure Functions.

Select your development language at the top of the article.

## Process file uploads

You can use functions in several ways to process files into or out of a blob storage container. To learn more about options for triggering on a blob container, see [Working with blobs](storage-considerations#working-with-blobs) in the best practices documentation.

For example, in a retail solution, a partner system can submit product catalog information as files into blob storage. You can use a blob triggered function to validate, transform, and process the files into the main system as you upload them.

The following tutorials use a Blob trigger (Event Grid based) to process files in a blob container:

For example, use the blob trigger with an event subscription on blob containers:

```
[FunctionName("ProcessCatalogData")]
public static async Task Run([BlobTrigger("catalog-uploads/{name}", Source = BlobTriggerSource.EventGrid, Connection = "<NAMED_STORAGE_CONNECTION>")] Stream myCatalogData, string name, ILogger log)
{
log.LogInformation($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myCatalogData.Length} Bytes");
using (var reader = new StreamReader(myCatalogData))
{
var catalogEntry = await reader.ReadLineAsync();
while(catalogEntry !=null)
{
// Process the catalog entry
// ...
catalogEntry = await reader.ReadLineAsync();
}
}
}
```


[Quickstart: Respond to blob storage events by using Azure Functions](scenario-blob-storage-events)[Sample: Blob trigger with the Event Grid source type quickstart sample)](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-eventgrid-blob)[Tutorial (events): Trigger Azure Functions on blob containers using an event subscription](functions-event-grid-blob-trigger)[Tutorial (polling): Upload and analyze a file with Azure Functions and Blob Storage](../storage/blobs/blob-upload-function-trigger)

[Quickstart: Respond to blob storage events by using Azure Functions](scenario-blob-storage-events)[Sample: Blob trigger with the Event Grid source type quickstart sample)](https://github.com/Azure-Samples/functions-quickstart-javascript-azd-eventgrid-blob)[Tutorial (events): Trigger Azure Functions on blob containers using an event subscription](functions-event-grid-blob-trigger?pivots=programming-language-javascript)[Tutorial (polling): Upload and analyze a file with Azure Functions and Blob Storage](../storage/blobs/blob-upload-function-trigger-javascript)

## Real-time stream and event processing

Cloud applications, IoT devices, and networking devices generate and collect a large amount of telemetry. Azure Functions can process that data in near real-time as the hot path, then store it in [Azure Cosmos DB](/en-us/azure/cosmos-db/introduction) for use in an analytics dashboard.

Your functions can also use low-latency event triggers, like Event Grid, and real-time outputs like SignalR to process data in near-real-time.

For example, you can use the event hubs trigger to read from an event hub and the output binding to write to an event hub after debatching and transforming the events:

```
[FunctionName("ProcessorFunction")]
public static async Task Run(
[EventHubTrigger(
"%Input_EH_Name%",
Connection = "InputEventHubConnectionSetting",
ConsumerGroup = "%Input_EH_ConsumerGroup%")] EventData[] inputMessages,
[EventHub(
"%Output_EH_Name%",
Connection = "OutputEventHubConnectionSetting")] IAsyncCollector<SensorDataRecord> outputMessages,
PartitionContext partitionContext,
ILogger log)
{
var debatcher = new Debatcher(log);
var debatchedMessages = await debatcher.Debatch(inputMessages, partitionContext.PartitionId);
var xformer = new Transformer(log);
await xformer.Transform(debatchedMessages, partitionContext.PartitionId, outputMessages);
}
```


[Streaming at scale with Azure Event Hubs, Functions and Azure SQL](https://github.com/Azure-Samples/streaming-at-scale/tree/main/eventhubs-functions-azuresql)[Streaming at scale with Azure Event Hubs, Functions and Cosmos DB](https://github.com/Azure-Samples/streaming-at-scale/tree/main/eventhubs-functions-cosmosdb)[Streaming at scale with Azure Event Hubs with Kafka producer, Functions with Kafka trigger and Cosmos DB](https://github.com/Azure-Samples/streaming-at-scale/tree/main/eventhubskafka-functions-cosmosdb)[Streaming at scale with Azure IoT Hub, Functions and Azure SQL](https://github.com/Azure-Samples/streaming-at-scale/tree/main/iothub-functions-azuresql)[Azure Event Hubs trigger for Azure Functions](functions-bindings-event-hubs-trigger?pivots=programming-language-csharp)[Apache Kafka trigger for Azure Functions](functions-bindings-kafka-trigger?pivots=programming-language-csharp)

## Machine learning and AI

Azure Functions provides serverless compute resources that integrate with AI and Azure services to streamline building cloud-hosted intelligent applications. You can use the Functions programming model to create and host remote Model Content Protocol (MCP) servers and implement various AI tools. For more information, see [Tools and MCP servers](functions-create-ai-enabled-apps#tools-and-mcp-servers).

The [Azure OpenAI binding extension](functions-bindings-openai) lets you integrate AI features and behaviors of the [Azure OpenAI service](/en-us/azure/ai-services/openai/overview), such as retrieval-augmented generation (RAG), into your function code executions. For more information, see [Retrieval-augmented generation](functions-create-ai-enabled-apps#retrieval-augmented-generation).

A function might also call a TensorFlow model or Azure AI services to process and classify a stream of images.

For more information, see [Use AI tools and models in Azure Functions](functions-create-ai-enabled-apps).

## Run scheduled tasks

Functions enables you to run your code based on a [cron schedule](functions-bindings-timer#usage) that you define.

See [Create a function in the Azure portal that runs on a schedule](functions-create-scheduled-function).

For example, you might analyze a financial services customer database for duplicate entries every 15 minutes to avoid multiple communications going out to the same customer.

For examples, see these code snippets:

```
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */15 * * * *")]TimerInfo myTimer, ILogger log)
{
if (myTimer.IsPastDue)
{
log.LogInformation("Timer is running late!");
}
log.LogInformation($"C# Timer trigger function executed at: {DateTime.Now}");
// Perform the database deduplication
}
```


## Build a scalable web API

An HTTP triggered function defines an HTTP endpoint. These endpoints run function code that can connect to other services directly or by using binding extensions. You can compose the endpoints into a web-based API.

You can also use an HTTP triggered function endpoint as a webhook integration, such as GitHub webhooks. In this way, you can create functions that process data from GitHub events. For more information, see [Monitor GitHub events by using a webhook with Azure Functions](/en-us/training/modules/monitor-github-events-with-a-function-triggered-by-a-webhook/).

For examples, see these code snippets:

```
[FunctionName("InsertName")]
public static async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Function, "post")] HttpRequest req,
[CosmosDB(
databaseName: "my-database",
collectionName: "my-container",
ConnectionStringSetting = "CosmosDbConnectionString")]IAsyncCollector<dynamic> documentsOut,
ILogger log)
{
string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
dynamic data = JsonConvert.DeserializeObject(requestBody);
string name = data?.name;
if (name == null)
{
return new BadRequestObjectResult("Please pass a name in the request body json");
}
// Add a JSON document to the output container.
await documentsOut.AddAsync(new
{
// create a random ID
id = System.Guid.NewGuid().ToString(),
name = name
});
return new OkResult();
}
```


[Quickstart: Azure Functions HTTP trigger](create-first-function-azure-developer-cli?pivots=programming-language-csharp)[Article: Create serverless APIs in Visual Studio using Azure Functions and API Management integration](openapi-apim-integrate-visual-studio)[Training: Expose multiple function apps as a consistent API by using Azure API Management](/en-us/training/modules/build-serverless-api-with-functions-api-management/)[Sample: Web application with a C# API and Azure SQL DB on Static Web Apps and Functions](/en-us/samples/azure-samples/todo-csharp-sql-swa-func/todo-csharp-sql-swa-func/)

## Build a serverless workflow

Functions often serve as the compute component in a serverless workflow topology, such as a Logic Apps workflow. You can also create long-running orchestrations by using the Durable Functions extension. For more information, see [Durable Functions overview](durable/durable-functions-overview).

## Respond to database changes

Some processes need to log, audit, or perform other operations when stored data changes. Functions triggers provide a good way to get notified of data changes to initial such an operation.

Consider these examples:

## Create reliable message systems

You can use Functions with Azure messaging services to create advanced event-driven messaging solutions.

For example, you can use triggers on Azure Storage queues as a way to chain together a series of function executions. Or use service bus queues and triggers for an online ordering system.

These articles show how to write output to a storage queue:

These articles show how to trigger from an Azure Service Bus queue or topic.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-deployment-technologies -->

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

A **Flex Consumption Deployment** diagnostic tool is available in the Azure portal. Open your Flex Consumption app, select **Diagnose and solve problems**, and search for `Flex Consumption Deployment`

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
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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
<!-- Source: N/A -->

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

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-host-json-v1 -->

# host.json reference for Azure Functions 1.x

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The *host.json* metadata file contains configuration options that affect all functions in a function app instance. This article lists the settings that are available for the version 1.x runtime. The JSON schema is at [http://json.schemastore.org/host](http://json.schemastore.org/host).

Note

This article is for Azure Functions 1.x. For a reference of host.json in Functions 2.x and later, see [host.json reference for Azure Functions 2.x](functions-host-json).

Other function app configuration options are managed in your [app settings](functions-app-settings).

Some host.json settings are only used when running locally in the [local.settings.json](functions-develop-local#local-settings-file) file.

## Sample host.json file

The following sample *host.json* files have all possible options specified.

```
{
"aggregator": {
"batchSize": 1000,
"flushTimeout": "00:00:30"
},
"applicationInsights": {
"sampling": {
"isEnabled": true,
"maxTelemetryItemsPerSecond" : 5
}
},
"documentDB": {
"connectionMode": "Gateway",
"protocol": "Https",
"leaseOptions": {
"leasePrefix": "prefix"
}
},
"eventHub": {
"maxBatchSize": 64,
"prefetchCount": 256,
"batchCheckpointFrequency": 1
},
"functions": [ "QueueProcessor", "GitHubWebHook" ],
"functionTimeout": "00:05:00",
"healthMonitor": {
"enabled": true,
"healthCheckInterval": "00:00:10",
"healthCheckWindow": "00:02:00",
"healthCheckThreshold": 6,
"counterThreshold": 0.80
},
"http": {
"routePrefix": "api",
"maxOutstandingRequests": 20,
"maxConcurrentRequests": 10,
"dynamicThrottlesEnabled": false
},
"id": "9f4ea53c5136457d883d685e57164f08",
"logger": {
"categoryFilter": {
"defaultLevel": "Information",
"categoryLevels": {
"Host": "Error",
"Function": "Error",
"Host.Aggregator": "Information"
}
}
},
"queues": {
"maxPollingInterval": 2000,
"visibilityTimeout" : "00:00:30",
"batchSize": 16,
"maxDequeueCount": 5,
"newBatchThreshold": 8
},
"sendGrid": {
"from": "Contoso Group <admin@contoso.com>"
},
"serviceBus": {
"maxConcurrentCalls": 16,
"prefetchCount": 100,
"autoRenewTimeout": "00:05:00",
"autoComplete": true
},
"singleton": {
"lockPeriod": "00:00:15",
"listenerLockPeriod": "00:01:00",
"listenerLockRecoveryPollingInterval": "00:01:00",
"lockAcquisitionTimeout": "00:01:00",
"lockAcquisitionPollingInterval": "00:00:03"
},
"tracing": {
"consoleLevel": "verbose",
"fileLoggingMode": "debugOnly"
},
"watchDirectories": [ "Shared" ],
}
```


The following sections of this article explain each top-level property. All are optional unless otherwise indicated.

## aggregator

Specifies how many function invocations are aggregated when [calculating metrics for Application Insights](configure-monitoring#configure-the-aggregator).

```
{
"aggregator": {
"batchSize": 1000,
"flushTimeout": "00:00:30"
}
}
```


| Property | Default | Description |
|---|---|---|
| batchSize | 1000 | Maximum number of requests to aggregate. |
| flushTimeout | 00:00:30 | Maximum time period to aggregate. |

Function invocations are aggregated when the first of the two limits are reached.

## applicationInsights

Controls the [sampling feature in Application Insights](configure-monitoring#configure-sampling).

```
{
"applicationInsights": {
"sampling": {
"isEnabled": true,
"maxTelemetryItemsPerSecond" : 5
}
}
}
```


| Property | Default | Description |
|---|---|---|
| isEnabled | true | Enables or disables sampling. |
| maxTelemetryItemsPerSecond | 5 | The threshold at which sampling begins. |

## DocumentDB

Configuration settings for the [Azure Cosmos DB trigger and bindings](functions-bindings-cosmosdb).

```
{
"documentDB": {
"connectionMode": "Gateway",
"protocol": "Https",
"leaseOptions": {
"leasePrefix": "prefix1"
}
}
}
```


| Property | Default | Description |
|---|---|---|
| GatewayMode | Gateway | The connection mode used by the function when connecting to the Azure Cosmos DB service. Options are `Direct` and `Gateway` |
| Protocol | Https | The connection protocol used by the function when connection to the Azure Cosmos DB service. Read
|

## durableTask

Configuration settings for [Durable Functions](durable/durable-functions-overview).

Note

All major versions of Durable Functions are supported on all versions of the Azure Functions runtime. However, the schema of the *host.json* configuration differs slightly depending on the version of the Azure Functions runtime and the version of the Durable Functions extension that you use.

The following code provides two examples of `durableTask`

settings in *host.json*: one for Durable Functions 2.x and one for Durable Functions 1.x. You can use both examples with Azure Functions 2.0 and 3.0. With Azure Functions 1.0, the available settings are the same, but the `durableTask`

section of *host.json* is located in the root of the *host.json* configuration instead of being a field under `extensions`

.

```
{
"extensions": {
"durableTask": {
"hubName": "MyTaskHub",
"defaultVersion": "1.0",
"versionMatchStrategy": "CurrentOrOlder",
"versionFailureStrategy": "Reject",
"storageProvider": {
"connectionStringName": "AzureWebJobsStorage",
"controlQueueBatchSize": 32,
"controlQueueBufferThreshold": 256,
"controlQueueVisibilityTimeout": "00:05:00",
"FetchLargeMessagesAutomatically": true,
"maxQueuePollingInterval": "00:00:30",
"partitionCount": 4,
"trackingStoreConnectionStringName": "TrackingStorage",
"trackingStoreNamePrefix": "DurableTask",
"useLegacyPartitionManagement": false,
"useTablePartitionManagement": true,
"workItemQueueVisibilityTimeout": "00:05:00",
"QueueClientMessageEncoding": "UTF8"
},
"tracing": {
"traceInputsAndOutputs": false,
"traceReplayEvents": false,
},
"httpSettings":{
"defaultAsyncRequestSleepTimeMilliseconds": 30000,
"useForwardedHost": false,
},
"notifications": {
"eventGrid": {
"topicEndpoint": "https://topic_name.westus2-1.eventgrid.azure.net/api/events",
"keySettingName": "EventGridKey",
"publishRetryCount": 3,
"publishRetryInterval": "00:00:30",
"publishEventTypes": [
"Started",
"Completed",
"Failed",
"Terminated"
]
}
},
"maxConcurrentActivityFunctions": 10,
"maxConcurrentOrchestratorFunctions": 10,
"maxConcurrentEntityFunctions": 10,
"extendedSessionsEnabled": false,
"extendedSessionIdleTimeoutInSeconds": 30,
"useAppLease": true,
"useGracefulShutdown": false,
"maxEntityOperationBatchSize": 50,
"maxOrchestrationActions": 100000,
"storeInputsInOrchestrationHistory": false
}
}
}
```


| Property | Default value | Description |
|---|---|---|
| hubName | TestHubName (DurableFunctionsHub in v1.x) | The name of the hub that stores the current state of a function app. Task hub names must start with a letter and consist of only letters and numbers. If you don't specify a name, the default value is used. Alternate task hub names can be used to isolate multiple Durable Functions applications from each other, even if they use the same storage back end. For more information, see
|

[orchestration versioning](durable/durable-functions-orchestration-versioning)feature to enable scenarios like zero-downtime deployments with breaking changes. You can use any string value for the version.`None`

, `Strict`

, and `CurrentOrOlder`

. For detailed explanations, see [Orchestration versioning](durable/durable-functions-orchestration-versioning).`defaultVersion`

value. Valid values are `Reject`

and `Fail`

. For detailed explanations, see [Orchestration versioning](durable/durable-functions-orchestration-versioning).**Consumption plan for Python**: 32**Consumption plan for other languages**: 128**Dedicated or Premium plan**: 256*hh:mm:ss*format.*hh:mm:ss*format.`true`

, large messages that exceed the queue size limit are retrieved. When this setting is `false`

, a blob URL that points to each large message is retrieved.**Consumption plan**: 10**Dedicated or Premium plan**: 10 times the number of processors on the current machine**Consumption plan**: 5**Dedicated or Premium plan**: 10 times the number of processors on the current machine**Consumption plan**: 5**Dedicated or Premium plan**: 10 times the number of processors on the current machine[durable task scheduler](durable/durable-task-scheduler/durable-task-scheduler). Otherwise, the maximum number of concurrent entity executions is limited to the`maxConcurrentOrchestratorFunctions`

value.*hh:mm:ss*format. Higher values can result in higher message processing latencies. Lower values can result in higher storage costs because of increased storage transactions.connectionStringName (v2.x)

azureStorageConnectionStringName (v1.x)

trackingStoreConnectionStringName

`connectionStringName`

value (v2.x) or `azureStorageConnectionStringName`

value (v1.x) connection is used.`trackingStoreConnectionStringName`

is specified. If you don't specify a prefix, the default value of `DurableTask`

is used. If `trackingStoreConnectionStringName`

isn't specified, the History and Instances tables use the `hubName`

value as their prefix, and the `trackingStoreNamePrefix`

setting is ignored.`true`

, the entire contents of function inputs and outputs are logged.`EventGridTopicEndpoint`

URL.*hh:mm:ss*format.`Started`

, `Completed`

, `Failed`

, and `Terminated`

.`extendedSessionsEnabled`

setting is `true`

.[Disaster recovery and geo-distribution in Durable Functions](durable/durable-functions-disaster-recovery-geo-distribution). This setting is available starting in v2.3.0.`false`

, an algorithm is used that reduces the possibility of duplicate function execution when scaling out. This setting is available starting in v2.3.0. **Setting this value to**.`true`

isn't recommendedIn v2.x: false

`true`

, an algorithm is used that's designed to reduce costs for Azure Storage v2 accounts. This setting is available starting in WebJobs.Extensions.DurableTask v2.10.0. Using this setting with a managed identity requires WebJobs.Extensions.DurableTask v3.x or later, or Worker.Extensions.DurableTask v1.2.x or later.**Consumption plan**: 50**Dedicated or Premium plan**: 5,000[batch](durable/durable-functions-perf-and-scale#entity-operation-batching). If this value is 1, batching is disabled, and a separate function invocation processes each operation message. This setting is available starting in v2.6.1.`true`

, the Durable Task Framework saves activity inputs in the History table, and activity function inputs appear in orchestration history query results.`DurableTaskClient`

uses the gRPC client to manage orchestration instances. This setting applies to Durable Functions .NET isolated worker and Java apps.*hh:mm:ss*format for the HTTP client used by the gRPC client in Durable Functions. The client is currently supported for .NET isolated worker apps (.NET 6 and later versions) and for Java apps.Many of these settings are for optimizing performance. For more information, see [Performance and scale](durable/durable-functions-perf-and-scale).

## eventHub

Configuration settings for [Event Hub triggers and bindings](functions-bindings-event-hubs?tabs=functionsv1#hostjson-settings).

## functions

A list of functions that the job host runs. An empty array means run all functions. Intended for use only when [running locally](functions-run-local). In function apps in Azure, you should instead follow the steps in [How to disable functions in Azure Functions](disable-function) to disable specific functions rather than using this setting.

```
{
"functions": [ "QueueProcessor", "GitHubWebHook" ]
}
```


## functionTimeout

Indicates the timeout duration for all functions. In a serverless Consumption plan, the valid range is from 1 second to 10 minutes, and the default value is 5 minutes. In an App Service plan, there is no overall limit and the default is *null*, which indicates no timeout.

```
{
"functionTimeout": "00:05:00"
}
```


## healthMonitor

Configuration settings for [Host health monitor](https://github.com/Azure/azure-webjobs-sdk-script/wiki/Host-Health-Monitor).

```
{
"healthMonitor": {
"enabled": true,
"healthCheckInterval": "00:00:10",
"healthCheckWindow": "00:02:00",
"healthCheckThreshold": 6,
"counterThreshold": 0.80
}
}
```


| Property | Default | Description |
|---|---|---|
| enabled | true | Specifies whether the feature is enabled. |
| healthCheckInterval | 10 seconds | The time interval between the periodic background health checks. |
| healthCheckWindow | 2 minutes | A sliding time window used with the `healthCheckThreshold` setting. |
| healthCheckThreshold | 6 | Maximum number of times the health check can fail before a host recycle is initiated. |
| counterThreshold | 0.80 | The threshold at which a performance counter will be considered unhealthy. |

## http

Configuration settings for [http triggers and bindings](functions-bindings-http-webhook).

```
{
"http": {
"routePrefix": "api",
"maxOutstandingRequests": 200,
"maxConcurrentRequests": 100,
"dynamicThrottlesEnabled": true
}
}
```


| Property | Default | Description |
|---|---|---|
| dynamicThrottlesEnabled | false | When enabled, this setting causes the request processing pipeline to periodically check system performance counters like connections/threads/processes/memory/cpu/etc. and if any of those counters are over a built-in high threshold (80%), requests are rejected with a 429 "Too Busy" response until the counter(s) return to normal levels. |
| maxConcurrentRequests | unbounded (`-1` ) |
The maximum number of HTTP functions that will be executed in parallel. This allows you to control concurrency, which can help manage resource utilization. For example, you might have an HTTP function that uses a lot of system resources (memory/cpu/sockets) such that it causes issues when concurrency is too high. Or you might have a function that makes outbound requests to a third party service, and those calls need to be rate limited. In these cases, applying a throttle here can help. |
| maxOutstandingRequests | unbounded (`-1` ) |
The maximum number of outstanding requests that are held at any given time. This limit includes requests that are queued but have not started executing, and any in progress executions. Any incoming requests over this limit are rejected with a 429 "Too Busy" response. That allows callers to employ time-based retry strategies, and also helps you to control maximum request latencies. This only controls queuing that occurs within the script host execution path. Other queues such as the ASP.NET request queue will still be in effect and unaffected by this setting. |
| routePrefix | api | The route prefix that applies to all routes. Use an empty string to remove the default prefix. |

## id

The unique ID for a job host. Can be a lower case GUID with dashes removed. Required when running locally. When running in Azure, we recommend that you not set an ID value. An ID is generated automatically in Azure when `id`

is omitted.

If you share a Storage account across multiple function apps, make sure that each function app has a different `id`

. You can omit the `id`

property or manually set each function app's `id`

to a different value. The timer trigger uses a storage lock to ensure that there will be only one timer instance when a function app scales out to multiple instances. If two function apps share the same `id`

and each uses a timer trigger, only one timer runs.

```
{
"id": "9f4ea53c5136457d883d685e57164f08"
}
```


## logger

Controls filtering for logs written by an [ILogger](functions-dotnet-class-library#ilogger) object or by [context.log](functions-reference-node#contextlog-method).

```
{
"logger": {
"categoryFilter": {
"defaultLevel": "Information",
"categoryLevels": {
"Host": "Error",
"Function": "Error",
"Host.Aggregator": "Information"
}
}
}
}
```


| Property | Default | Description |
|---|---|---|
| categoryFilter | n/a | Specifies filtering by category |
| defaultLevel | Information | For any categories not specified in the `categoryLevels` array, send logs at this level and above to Application Insights. |
| categoryLevels | n/a | An array of categories that specifies the minimum log level to send to Application Insights for each category. The category specified here controls all categories that begin with the same value, and longer values take precedence. In the preceding sample host.json file, all categories that begin with "Host.Aggregator" log at `Information` level. All other categories that begin with "Host", such as "Host.Executor", log at `Error` level. |

## queues

Configuration settings for [Storage queue triggers and bindings](functions-bindings-storage-queue).

```
{
"queues": {
"maxPollingInterval": 2000,
"visibilityTimeout" : "00:00:30",
"batchSize": 16,
"maxDequeueCount": 5,
"newBatchThreshold": 8
}
}
```


| Property | Default | Description |
|---|---|---|
| maxPollingInterval | 60000 | The maximum interval in milliseconds between queue polls. |
| visibilityTimeout | 0 | The time interval between retries when processing of a message fails. |
| batchSize | 16 | The number of queue messages that the Functions runtime retrieves simultaneously and processes in parallel. When the number being processed gets down to the `newBatchThreshold` , the runtime gets another batch and starts processing those messages. So the maximum number of concurrent messages being processed per function is `batchSize` plus `newBatchThreshold` . This limit applies separately to each queue-triggered function. If you want to avoid parallel execution for messages received on one queue, you can set `batchSize` to 1. However, this setting eliminates concurrency only so long as your function app runs on a single virtual machine (VM). If the function app scales out to multiple VMs, each VM could run one instance of each queue-triggered function.The maximum `batchSize` is 32. |
| maxDequeueCount | 5 | The number of times to try processing a message before moving it to the poison queue. |
| newBatchThreshold | batchSize/2 | Whenever the number of messages being processed concurrently gets down to this number, the runtime retrieves another batch. |

## SendGrid

Configuration setting for the [SendGrind output binding](functions-bindings-sendgrid)

```
{
"sendGrid": {
"from": "Contoso Group <admin@contoso.com>"
}
}
```


| Property | Default | Description |
|---|---|---|
| from | n/a | The sender's email address across all functions. |

## serviceBus

Configuration setting for [Service Bus triggers and bindings](functions-bindings-service-bus).

```
{
"serviceBus": {
"maxConcurrentCalls": 16,
"prefetchCount": 100,
"autoRenewTimeout": "00:05:00",
"autoComplete": true
}
}
```


| Property | Default | Description |
|---|---|---|
| maxConcurrentCalls | 16 | The maximum number of concurrent calls to the callback that the message pump should initiate. By default, the Functions runtime processes multiple messages concurrently. To direct the runtime to process only a single queue or topic message at a time, set `maxConcurrentCalls` to 1. |
| prefetchCount | n/a | The default PrefetchCount that will be used by the underlying ServiceBusReceiver. |
| autoRenewTimeout | 00:05:00 | The maximum duration within which the message lock will be renewed automatically. |
| autoComplete | true | When true, the trigger completes the message processing automatically on successful execution of the operation. When false, it is the responsibility of the function to complete the message before returning. |

## singleton

Configuration settings for Singleton lock behavior. For more information, see [GitHub issue about singleton support](https://github.com/Azure/azure-webjobs-sdk-script/issues/912).

```
{
"singleton": {
"lockPeriod": "00:00:15",
"listenerLockPeriod": "00:01:00",
"listenerLockRecoveryPollingInterval": "00:01:00",
"lockAcquisitionTimeout": "00:01:00",
"lockAcquisitionPollingInterval": "00:00:03"
}
}
```


| Property | Default | Description |
|---|---|---|
| lockPeriod | 00:00:15 | The period that function level locks are taken for. The locks auto-renew. |
| listenerLockPeriod | 00:01:00 | The period that listener locks are taken for. |
| listenerLockRecoveryPollingInterval | 00:01:00 | The time interval used for listener lock recovery if a listener lock couldn't be acquired on startup. |
| lockAcquisitionTimeout | 00:01:00 | The maximum amount of time the runtime tries to acquire a lock. |
| lockAcquisitionPollingInterval | n/a | The interval between lock acquisition attempts. |

## tracing

*Version 1.x*

Configuration settings for logs that you create by using a `TraceWriter`

object. To learn more, see [C# Logging].

```
{
"tracing": {
"consoleLevel": "verbose",
"fileLoggingMode": "debugOnly"
}
}
```


| Property | Default | Description |
|---|---|---|
| consoleLevel | info | The tracing level for console logging. Options are: `off` , `error` , `warning` , `info` , and `verbose` . |
| fileLoggingMode | debugOnly | The tracing level for file logging. Options are `never` , `always` , `debugOnly` . |

## watchDirectories

A set of [shared code directories](functions-reference-csharp#watched-directories) that should be monitored for changes. Ensures that when code in these directories is changed, the changes are picked up by your functions.

```
{
"watchDirectories": [ "Shared" ]
}
```

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-expressions-patterns -->

# Azure Functions binding expressions and patterns

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

One of the most powerful features of [triggers and bindings](functions-triggers-bindings) in Azure Functions is *binding expressions*. In the `function.json`

file and in function parameters and code, you can use expressions that resolve to values from various sources.

Most expressions are wrapped in curly braces. For example, in a queue trigger function, `{queueTrigger}`

resolves to the queue message text. If the `path`

property for a blob output binding is `container/{queueTrigger}`

and a queue message `HelloWorld`

triggers the function, a blob named `HelloWorld`

is created.

App settings

It's a best practice to manage secrets and connection strings by using app settings rather than configuration files. This practice limits access to these secrets and makes it safe to store files such as `function.json`

in public source-control repositories.

App settings are also useful whenever you want to change a configuration based on the environment. For example, in a test environment, you might want to monitor a different container for queue storage or blob storage.

Binding expressions for app settings are identified differently from other binding expressions: they're wrapped in percent signs rather than curly braces. For example, if the path for a blob output binding is `%Environment%/newblob.txt`

and the `Environment`

app setting value is `Development`

, a blob is created in the `Development`

container.

When a function is running locally, values for app settings come from the `local.settings.json`

file.

Note

The `connection`

property of triggers and bindings is a special case and automatically resolves values as app settings, without percent signs.

The following example is an Azure Queue Storage trigger that uses an app setting `%input_queue_name%`

to define the queue to trigger on:

```
{
"bindings": [
{
"name": "order",
"type": "queueTrigger",
"direction": "in",
"queueName": "%input_queue_name%",
"connection": "MY_STORAGE_ACCT_APP_SETTING"
}
]
}
```


You can use the same approach in class libraries:

```
[FunctionName("QueueTrigger")]
public static void Run(
[QueueTrigger("%input_queue_name%")]string myQueueItem,
ILogger log)
{
log.LogInformation($"C# Queue trigger function processed: {myQueueItem}");
}
```


## Trigger file name

The `path`

value for a blob trigger can be a pattern that lets you refer to the name of the triggering blob in other bindings and function code. The pattern can also include filtering criteria that specify which blobs can trigger a function invocation.

For example, in the following binding for a blob trigger, the `path`

pattern is `sample-images/{filename}`

. This pattern creates a binding expression named `filename`

.

```
{
"bindings": [
{
"name": "image",
"type": "blobTrigger",
"path": "sample-images/{filename}",
"direction": "in",
"connection": "MyStorageConnection"
},
...
```


You can then use the expression `filename`

in an output binding to specify the name of the blob that you're creating:

```
...
{
"name": "imageSmall",
"type": "blob",
"path": "sample-images-sm/{filename}",
"direction": "out",
"connection": "MyStorageConnection"
}
],
}
```


Function code has access to this same value by using `filename`

as a parameter name:

```
// C# example of binding to {filename}
public static void Run(Stream image, string filename, Stream imageSmall, ILogger log)
{
log.LogInformation($"Blob trigger processing: {filename}");
// ...
}
```


The same ability to use binding expressions and patterns applies to attributes in class libraries. In the following example, the attribute constructor parameters are the same `path`

values as the preceding `function.json`

examples:

```
[FunctionName("ResizeImage")]
public static void Run(
[BlobTrigger("sample-images/{filename}")] Stream image,
[Blob("sample-images-sm/{filename}", FileAccess.Write)] Stream imageSmall,
string filename,
ILogger log)
{
log.LogInformation($"Blob trigger processing: {filename}");
// ...
}
```


You can also create expressions for parts of the file name. In the following example, the function is triggered only on file names that match a pattern: `anyname-anyfile.csv`

.

```
{
"name": "myBlob",
"type": "blobTrigger",
"direction": "in",
"path": "testContainerName/{date}-{filetype}.csv",
"connection": "OrderStorageConnection"
}
```


For more information on how to use expressions and patterns in the blob path string, see the [reference for Azure Blob Storage bindings](functions-bindings-storage-blob).

## Trigger metadata

In addition to the data payload that a trigger provides (such as the content of the queue message that triggered a function), many triggers provide other metadata values. You can use these values as input parameters in C# and F# or as properties on the `context.bindings`

object in JavaScript.

For example, an Azure Queue Storage trigger supports the following properties:

`QueueTrigger`

(triggering message content if the string is valid)`DequeueCount`

`ExpirationTime`

`Id`

`InsertionTime`

`NextVisibleTime`

`PopReceipt`


These metadata values are accessible in the `function.json`

file properties. For example, suppose you use a queue trigger and the queue message contains the name of a blob that you want to read. In the `function.json`

file, you can use the `queueTrigger`

metadata property in the blob `path`

property, as shown in the following example:

```
{
"bindings": [
{
"name": "myQueueItem",
"type": "queueTrigger",
"queueName": "myqueue-items",
"connection": "MyStorageConnection",
},
{
"name": "myInputBlob",
"type": "blob",
"path": "samples-workitems/{queueTrigger}",
"direction": "in",
"connection": "MyStorageConnection"
}
]
}
```


You can find details of metadata properties for each trigger in the corresponding reference article. For an example, see the [metadata for an Azure Queue Storage trigger](functions-bindings-storage-queue-trigger#message-metadata). Documentation is also available on the **Integrate** tab of the portal, in the **Documentation** section below the binding configuration area.

## JSON payloads

In some scenarios, you can refer to the trigger payload's properties in the configuration for other bindings in the same function and in function code. This approach requires that the trigger payload is JSON and is smaller than a threshold specific to each trigger. Typically, the payload size needs to be less than 100 MB, but you should check the reference content for each trigger.

Using trigger payload properties might affect the performance of your application. It also forces the trigger parameter type to be a simple type (like a string) or a custom object type that represents JSON data. You can't use it with streams, clients, or other SDK types.

The following example shows the `function.json`

file for a webhook function that receives a blob name in JSON: `{"BlobName":"HelloWorld.txt"}`

. A blob input binding reads the blob, and the HTTP output binding returns the blob contents in the HTTP response. Notice that the blob input binding gets the blob name by referring directly to the `BlobName`

property (`"path": "strings/{BlobName}"`

).

```
{
"bindings": [
{
"name": "info",
"type": "httpTrigger",
"direction": "in",
"webHookType": "genericJson"
},
{
"name": "blobContents",
"type": "blob",
"direction": "in",
"path": "strings/{BlobName}",
"connection": "AzureWebJobsStorage"
},
{
"name": "res",
"type": "http",
"direction": "out"
}
]
}
```


For this approach to work in C# and F#, you need a class that defines the fields to be deserialized, as in the following example:

```
using System.Net;
using Microsoft.Extensions.Logging;
public class BlobInfo
{
public string BlobName { get; set; }
}
public static HttpResponseMessage Run(HttpRequestMessage req, BlobInfo info, string blobContents, ILogger log)
{
if (blobContents == null) {
return req.CreateResponse(HttpStatusCode.NotFound);
}
log.LogInformation($"Processing: {info.BlobName}");
return req.CreateResponse(HttpStatusCode.OK, new {
data = $"{blobContents}"
});
}
```


In JavaScript, JSON deserialization is automatically performed:

```
module.exports = async function (context, info) {
if ('BlobName' in info) {
context.res = {
body: { 'data': context.bindings.blobContents }
}
}
else {
context.res = {
status: 404
};
}
}
```


### Dot notation

If some of the properties in your JSON payload are objects with properties, you can refer to them directly by using dot (`.`

) notation. This notation doesn't work for [Azure Cosmos DB](functions-bindings-cosmosdb-v2) or [Azure Table Storage](functions-bindings-storage-table-output) bindings.

For example, suppose your JSON looks like this example:

```
{
"BlobName": {
"FileName":"HelloWorld",
"Extension":"txt"
}
}
```


You can refer directly to `FileName`

as `BlobName.FileName`

. With this JSON format, here's what the `path`

property in the preceding example would look like:

```
"path": "strings/{BlobName.FileName}.{BlobName.Extension}",
```


In C#, you would need two classes:

```
public class BlobInfo
{
public BlobName BlobName { get; set; }
}
public class BlobName
{
public string FileName { get; set; }
public string Extension { get; set; }
}
```


## New GUIDs

The `{rand-guid}`

binding expression creates a GUID. The following blob path in a `function.json`

file creates a blob with a name like *50710cb5-84b9-4d87-9d83-a03d6976a682.txt*:

```
{
"type": "blob",
"name": "blobOutput",
"direction": "out",
"path": "my-output-container/{rand-guid}.txt"
}
```


## Current date and time

The binding expression `DateTime`

resolves to `DateTime.UtcNow`

. The following blob path in a `function.json`

file creates a blob with a name like *2018-02-16T17-59-55Z.txt*:

```
{
"type": "blob",
"name": "blobOutput",
"direction": "out",
"path": "my-output-container/{DateTime}.txt"
}
```


## Binding at runtime

In C# and other .NET languages, you can use an imperative binding pattern, as opposed to the declarative bindings in `function.json`

and attributes. Imperative binding is useful when binding parameters need to be computed at runtime rather than design time. To learn more, see the [C# developer reference](functions-dotnet-class-library#binding-at-runtime) or the [C# script developer reference](functions-reference-csharp#binding-at-runtime).

---
<!-- Source: N/A -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache -->

# Overview of Azure functions for Azure Redis

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to use either Azure Managed Redis or Azure Cache for Redis with Azure Functions to create optimized serverless and event-driven architectures.

Azure Functions provides an event-driven programming model where triggers and bindings are key features. With Azure Functions, you can easily build event-driven serverless applications. Azure Redis services (Azure Managed Redis and Azure Cache for Redis) provide a set of building blocks and best practices for building distributed applications, including microservices, state management, pub/sub messaging, and more.

Azure Redis can be used as a trigger for Azure Functions, allowing you to initiate a serverless workflow. This functionality can be highly useful in data architectures like a write-behind cache, or any event-based architectures.

You can integrate Azure Redis and Azure Functions to build functions that react to events from Azure Redis or external systems.

| Action | Direction |
|---|---|
|

[Trigger on Redis lists](functions-bindings-cache-trigger-redislist)[Trigger on Redis streams](functions-bindings-cache-trigger-redisstream)[Read a cached value](functions-bindings-cache-input)[Write a values to cache](functions-bindings-cache-output)## Scope of availability for functions triggers and bindings

| Tier | Azure Cache for Redis (Basic, Standard, Premium, Enterprise, Enterprise Flash) | Azure Managed Redis (Memory Optimized, Basic, Compute Optimized, Flash Optimized) |
|---|---|---|
| Pub/Sub | Yes | Yes |
| Lists | Yes | Yes |
| Streams | Yes | Yes |
| Bindings | Yes | Yes |

Important

Redis triggers are currently only supported for functions running in either a [Elastic Premium plan](functions-premium-plan) or a dedicated [App Service plan](dedicated-plan).

## Install extension

Functions run in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

Add the extension to your project by installing [this NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Redis).

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Redis
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

## Update packages

Add the [Azure Functions Java Redis Annotations package](https://mvnrepository.com/artifact/com.microsoft.azure.functions/azure-functions-java-library-redis) to your project by updating the `pom.xml`

file to add this dependency:

```
<dependency>
<groupId>com.microsoft.azure.functions</groupId>
<artifactId>azure-functions-java-library-redis</artifactId>
<version>1.0.0</version>
</dependency>
```


## Redis connection string

Azure Redis triggers and bindings have a required property that indicates the application setting or collection name that contains cache connection information. The Redis trigger or binding looks for an environmental variable holding the connection string with the name passed to the `Connection`

parameter.

In local development, the `Connection`

can be defined using the [local.settings.json](/en-us/azure/azure-functions/functions-develop-local#local-settings-file) file. When deployed to Azure, [application settings](/en-us/azure/azure-functions/functions-how-to-use-azure-function-app-settings) can be used.

When connecting to a cache instance with an Azure function, you can use one of these kinds of connections in your deployments:

A user-assigned managed identity must be associated with your function app, and that identity must also be granted explicit permissions in your cache service. For more information, see [Use Microsoft Entra ID for cache authentication](/en-us/azure/azure-cache-for-redis/cache-azure-active-directory-for-authentication).

These examples show the key name and value of app settings required to connect to each cache service based on the kind of client authentication, assuming that the `Connection`

property in the binding is set to `Redis`

.

```
"Redis__redisHostName": "<cacheName>.<region>.redis.azure.net",
"Redis__principalId": "<principalId>",
"Redis__clientId": "<clientId>"
```

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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
<!-- Source: N/A -->

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

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-host-json-v1 -->

# host.json reference for Azure Functions 1.x

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The *host.json* metadata file contains configuration options that affect all functions in a function app instance. This article lists the settings that are available for the version 1.x runtime. The JSON schema is at [http://json.schemastore.org/host](http://json.schemastore.org/host).

Note

This article is for Azure Functions 1.x. For a reference of host.json in Functions 2.x and later, see [host.json reference for Azure Functions 2.x](functions-host-json).

Other function app configuration options are managed in your [app settings](functions-app-settings).

Some host.json settings are only used when running locally in the [local.settings.json](functions-develop-local#local-settings-file) file.

## Sample host.json file

The following sample *host.json* files have all possible options specified.

```
{
"aggregator": {
"batchSize": 1000,
"flushTimeout": "00:00:30"
},
"applicationInsights": {
"sampling": {
"isEnabled": true,
"maxTelemetryItemsPerSecond" : 5
}
},
"documentDB": {
"connectionMode": "Gateway",
"protocol": "Https",
"leaseOptions": {
"leasePrefix": "prefix"
}
},
"eventHub": {
"maxBatchSize": 64,
"prefetchCount": 256,
"batchCheckpointFrequency": 1
},
"functions": [ "QueueProcessor", "GitHubWebHook" ],
"functionTimeout": "00:05:00",
"healthMonitor": {
"enabled": true,
"healthCheckInterval": "00:00:10",
"healthCheckWindow": "00:02:00",
"healthCheckThreshold": 6,
"counterThreshold": 0.80
},
"http": {
"routePrefix": "api",
"maxOutstandingRequests": 20,
"maxConcurrentRequests": 10,
"dynamicThrottlesEnabled": false
},
"id": "9f4ea53c5136457d883d685e57164f08",
"logger": {
"categoryFilter": {
"defaultLevel": "Information",
"categoryLevels": {
"Host": "Error",
"Function": "Error",
"Host.Aggregator": "Information"
}
}
},
"queues": {
"maxPollingInterval": 2000,
"visibilityTimeout" : "00:00:30",
"batchSize": 16,
"maxDequeueCount": 5,
"newBatchThreshold": 8
},
"sendGrid": {
"from": "Contoso Group <admin@contoso.com>"
},
"serviceBus": {
"maxConcurrentCalls": 16,
"prefetchCount": 100,
"autoRenewTimeout": "00:05:00",
"autoComplete": true
},
"singleton": {
"lockPeriod": "00:00:15",
"listenerLockPeriod": "00:01:00",
"listenerLockRecoveryPollingInterval": "00:01:00",
"lockAcquisitionTimeout": "00:01:00",
"lockAcquisitionPollingInterval": "00:00:03"
},
"tracing": {
"consoleLevel": "verbose",
"fileLoggingMode": "debugOnly"
},
"watchDirectories": [ "Shared" ],
}
```


The following sections of this article explain each top-level property. All are optional unless otherwise indicated.

## aggregator

Specifies how many function invocations are aggregated when [calculating metrics for Application Insights](configure-monitoring#configure-the-aggregator).

```
{
"aggregator": {
"batchSize": 1000,
"flushTimeout": "00:00:30"
}
}
```


| Property | Default | Description |
|---|---|---|
| batchSize | 1000 | Maximum number of requests to aggregate. |
| flushTimeout | 00:00:30 | Maximum time period to aggregate. |

Function invocations are aggregated when the first of the two limits are reached.

## applicationInsights

Controls the [sampling feature in Application Insights](configure-monitoring#configure-sampling).

```
{
"applicationInsights": {
"sampling": {
"isEnabled": true,
"maxTelemetryItemsPerSecond" : 5
}
}
}
```


| Property | Default | Description |
|---|---|---|
| isEnabled | true | Enables or disables sampling. |
| maxTelemetryItemsPerSecond | 5 | The threshold at which sampling begins. |

## DocumentDB

Configuration settings for the [Azure Cosmos DB trigger and bindings](functions-bindings-cosmosdb).

```
{
"documentDB": {
"connectionMode": "Gateway",
"protocol": "Https",
"leaseOptions": {
"leasePrefix": "prefix1"
}
}
}
```


| Property | Default | Description |
|---|---|---|
| GatewayMode | Gateway | The connection mode used by the function when connecting to the Azure Cosmos DB service. Options are `Direct` and `Gateway` |
| Protocol | Https | The connection protocol used by the function when connection to the Azure Cosmos DB service. Read
|

## durableTask

Configuration settings for [Durable Functions](durable/durable-functions-overview).

Note

All major versions of Durable Functions are supported on all versions of the Azure Functions runtime. However, the schema of the *host.json* configuration differs slightly depending on the version of the Azure Functions runtime and the version of the Durable Functions extension that you use.

The following code provides two examples of `durableTask`

settings in *host.json*: one for Durable Functions 2.x and one for Durable Functions 1.x. You can use both examples with Azure Functions 2.0 and 3.0. With Azure Functions 1.0, the available settings are the same, but the `durableTask`

section of *host.json* is located in the root of the *host.json* configuration instead of being a field under `extensions`

.

```
{
"extensions": {
"durableTask": {
"hubName": "MyTaskHub",
"defaultVersion": "1.0",
"versionMatchStrategy": "CurrentOrOlder",
"versionFailureStrategy": "Reject",
"storageProvider": {
"connectionStringName": "AzureWebJobsStorage",
"controlQueueBatchSize": 32,
"controlQueueBufferThreshold": 256,
"controlQueueVisibilityTimeout": "00:05:00",
"FetchLargeMessagesAutomatically": true,
"maxQueuePollingInterval": "00:00:30",
"partitionCount": 4,
"trackingStoreConnectionStringName": "TrackingStorage",
"trackingStoreNamePrefix": "DurableTask",
"useLegacyPartitionManagement": false,
"useTablePartitionManagement": true,
"workItemQueueVisibilityTimeout": "00:05:00",
"QueueClientMessageEncoding": "UTF8"
},
"tracing": {
"traceInputsAndOutputs": false,
"traceReplayEvents": false,
},
"httpSettings":{
"defaultAsyncRequestSleepTimeMilliseconds": 30000,
"useForwardedHost": false,
},
"notifications": {
"eventGrid": {
"topicEndpoint": "https://topic_name.westus2-1.eventgrid.azure.net/api/events",
"keySettingName": "EventGridKey",
"publishRetryCount": 3,
"publishRetryInterval": "00:00:30",
"publishEventTypes": [
"Started",
"Completed",
"Failed",
"Terminated"
]
}
},
"maxConcurrentActivityFunctions": 10,
"maxConcurrentOrchestratorFunctions": 10,
"maxConcurrentEntityFunctions": 10,
"extendedSessionsEnabled": false,
"extendedSessionIdleTimeoutInSeconds": 30,
"useAppLease": true,
"useGracefulShutdown": false,
"maxEntityOperationBatchSize": 50,
"maxOrchestrationActions": 100000,
"storeInputsInOrchestrationHistory": false
}
}
}
```


| Property | Default value | Description |
|---|---|---|
| hubName | TestHubName (DurableFunctionsHub in v1.x) | The name of the hub that stores the current state of a function app. Task hub names must start with a letter and consist of only letters and numbers. If you don't specify a name, the default value is used. Alternate task hub names can be used to isolate multiple Durable Functions applications from each other, even if they use the same storage back end. For more information, see
|

[orchestration versioning](durable/durable-functions-orchestration-versioning)feature to enable scenarios like zero-downtime deployments with breaking changes. You can use any string value for the version.`None`

, `Strict`

, and `CurrentOrOlder`

. For detailed explanations, see [Orchestration versioning](durable/durable-functions-orchestration-versioning).`defaultVersion`

value. Valid values are `Reject`

and `Fail`

. For detailed explanations, see [Orchestration versioning](durable/durable-functions-orchestration-versioning).**Consumption plan for Python**: 32**Consumption plan for other languages**: 128**Dedicated or Premium plan**: 256*hh:mm:ss*format.*hh:mm:ss*format.`true`

, large messages that exceed the queue size limit are retrieved. When this setting is `false`

, a blob URL that points to each large message is retrieved.**Consumption plan**: 10**Dedicated or Premium plan**: 10 times the number of processors on the current machine**Consumption plan**: 5**Dedicated or Premium plan**: 10 times the number of processors on the current machine**Consumption plan**: 5**Dedicated or Premium plan**: 10 times the number of processors on the current machine[durable task scheduler](durable/durable-task-scheduler/durable-task-scheduler). Otherwise, the maximum number of concurrent entity executions is limited to the`maxConcurrentOrchestratorFunctions`

value.*hh:mm:ss*format. Higher values can result in higher message processing latencies. Lower values can result in higher storage costs because of increased storage transactions.connectionStringName (v2.x)

azureStorageConnectionStringName (v1.x)

trackingStoreConnectionStringName

`connectionStringName`

value (v2.x) or `azureStorageConnectionStringName`

value (v1.x) connection is used.`trackingStoreConnectionStringName`

is specified. If you don't specify a prefix, the default value of `DurableTask`

is used. If `trackingStoreConnectionStringName`

isn't specified, the History and Instances tables use the `hubName`

value as their prefix, and the `trackingStoreNamePrefix`

setting is ignored.`true`

, the entire contents of function inputs and outputs are logged.`EventGridTopicEndpoint`

URL.*hh:mm:ss*format.`Started`

, `Completed`

, `Failed`

, and `Terminated`

.`extendedSessionsEnabled`

setting is `true`

.[Disaster recovery and geo-distribution in Durable Functions](durable/durable-functions-disaster-recovery-geo-distribution). This setting is available starting in v2.3.0.`false`

, an algorithm is used that reduces the possibility of duplicate function execution when scaling out. This setting is available starting in v2.3.0. **Setting this value to**.`true`

isn't recommendedIn v2.x: false

`true`

, an algorithm is used that's designed to reduce costs for Azure Storage v2 accounts. This setting is available starting in WebJobs.Extensions.DurableTask v2.10.0. Using this setting with a managed identity requires WebJobs.Extensions.DurableTask v3.x or later, or Worker.Extensions.DurableTask v1.2.x or later.**Consumption plan**: 50**Dedicated or Premium plan**: 5,000[batch](durable/durable-functions-perf-and-scale#entity-operation-batching). If this value is 1, batching is disabled, and a separate function invocation processes each operation message. This setting is available starting in v2.6.1.`true`

, the Durable Task Framework saves activity inputs in the History table, and activity function inputs appear in orchestration history query results.`DurableTaskClient`

uses the gRPC client to manage orchestration instances. This setting applies to Durable Functions .NET isolated worker and Java apps.*hh:mm:ss*format for the HTTP client used by the gRPC client in Durable Functions. The client is currently supported for .NET isolated worker apps (.NET 6 and later versions) and for Java apps.Many of these settings are for optimizing performance. For more information, see [Performance and scale](durable/durable-functions-perf-and-scale).

## eventHub

Configuration settings for [Event Hub triggers and bindings](functions-bindings-event-hubs?tabs=functionsv1#hostjson-settings).

## functions

A list of functions that the job host runs. An empty array means run all functions. Intended for use only when [running locally](functions-run-local). In function apps in Azure, you should instead follow the steps in [How to disable functions in Azure Functions](disable-function) to disable specific functions rather than using this setting.

```
{
"functions": [ "QueueProcessor", "GitHubWebHook" ]
}
```


## functionTimeout

Indicates the timeout duration for all functions. In a serverless Consumption plan, the valid range is from 1 second to 10 minutes, and the default value is 5 minutes. In an App Service plan, there is no overall limit and the default is *null*, which indicates no timeout.

```
{
"functionTimeout": "00:05:00"
}
```


## healthMonitor

Configuration settings for [Host health monitor](https://github.com/Azure/azure-webjobs-sdk-script/wiki/Host-Health-Monitor).

```
{
"healthMonitor": {
"enabled": true,
"healthCheckInterval": "00:00:10",
"healthCheckWindow": "00:02:00",
"healthCheckThreshold": 6,
"counterThreshold": 0.80
}
}
```


| Property | Default | Description |
|---|---|---|
| enabled | true | Specifies whether the feature is enabled. |
| healthCheckInterval | 10 seconds | The time interval between the periodic background health checks. |
| healthCheckWindow | 2 minutes | A sliding time window used with the `healthCheckThreshold` setting. |
| healthCheckThreshold | 6 | Maximum number of times the health check can fail before a host recycle is initiated. |
| counterThreshold | 0.80 | The threshold at which a performance counter will be considered unhealthy. |

## http

Configuration settings for [http triggers and bindings](functions-bindings-http-webhook).

```
{
"http": {
"routePrefix": "api",
"maxOutstandingRequests": 200,
"maxConcurrentRequests": 100,
"dynamicThrottlesEnabled": true
}
}
```


| Property | Default | Description |
|---|---|---|
| dynamicThrottlesEnabled | false | When enabled, this setting causes the request processing pipeline to periodically check system performance counters like connections/threads/processes/memory/cpu/etc. and if any of those counters are over a built-in high threshold (80%), requests are rejected with a 429 "Too Busy" response until the counter(s) return to normal levels. |
| maxConcurrentRequests | unbounded (`-1` ) |
The maximum number of HTTP functions that will be executed in parallel. This allows you to control concurrency, which can help manage resource utilization. For example, you might have an HTTP function that uses a lot of system resources (memory/cpu/sockets) such that it causes issues when concurrency is too high. Or you might have a function that makes outbound requests to a third party service, and those calls need to be rate limited. In these cases, applying a throttle here can help. |
| maxOutstandingRequests | unbounded (`-1` ) |
The maximum number of outstanding requests that are held at any given time. This limit includes requests that are queued but have not started executing, and any in progress executions. Any incoming requests over this limit are rejected with a 429 "Too Busy" response. That allows callers to employ time-based retry strategies, and also helps you to control maximum request latencies. This only controls queuing that occurs within the script host execution path. Other queues such as the ASP.NET request queue will still be in effect and unaffected by this setting. |
| routePrefix | api | The route prefix that applies to all routes. Use an empty string to remove the default prefix. |

## id

The unique ID for a job host. Can be a lower case GUID with dashes removed. Required when running locally. When running in Azure, we recommend that you not set an ID value. An ID is generated automatically in Azure when `id`

is omitted.

If you share a Storage account across multiple function apps, make sure that each function app has a different `id`

. You can omit the `id`

property or manually set each function app's `id`

to a different value. The timer trigger uses a storage lock to ensure that there will be only one timer instance when a function app scales out to multiple instances. If two function apps share the same `id`

and each uses a timer trigger, only one timer runs.

```
{
"id": "9f4ea53c5136457d883d685e57164f08"
}
```


## logger

Controls filtering for logs written by an [ILogger](functions-dotnet-class-library#ilogger) object or by [context.log](functions-reference-node#contextlog-method).

```
{
"logger": {
"categoryFilter": {
"defaultLevel": "Information",
"categoryLevels": {
"Host": "Error",
"Function": "Error",
"Host.Aggregator": "Information"
}
}
}
}
```


| Property | Default | Description |
|---|---|---|
| categoryFilter | n/a | Specifies filtering by category |
| defaultLevel | Information | For any categories not specified in the `categoryLevels` array, send logs at this level and above to Application Insights. |
| categoryLevels | n/a | An array of categories that specifies the minimum log level to send to Application Insights for each category. The category specified here controls all categories that begin with the same value, and longer values take precedence. In the preceding sample host.json file, all categories that begin with "Host.Aggregator" log at `Information` level. All other categories that begin with "Host", such as "Host.Executor", log at `Error` level. |

## queues

Configuration settings for [Storage queue triggers and bindings](functions-bindings-storage-queue).

```
{
"queues": {
"maxPollingInterval": 2000,
"visibilityTimeout" : "00:00:30",
"batchSize": 16,
"maxDequeueCount": 5,
"newBatchThreshold": 8
}
}
```


| Property | Default | Description |
|---|---|---|
| maxPollingInterval | 60000 | The maximum interval in milliseconds between queue polls. |
| visibilityTimeout | 0 | The time interval between retries when processing of a message fails. |
| batchSize | 16 | The number of queue messages that the Functions runtime retrieves simultaneously and processes in parallel. When the number being processed gets down to the `newBatchThreshold` , the runtime gets another batch and starts processing those messages. So the maximum number of concurrent messages being processed per function is `batchSize` plus `newBatchThreshold` . This limit applies separately to each queue-triggered function. If you want to avoid parallel execution for messages received on one queue, you can set `batchSize` to 1. However, this setting eliminates concurrency only so long as your function app runs on a single virtual machine (VM). If the function app scales out to multiple VMs, each VM could run one instance of each queue-triggered function.The maximum `batchSize` is 32. |
| maxDequeueCount | 5 | The number of times to try processing a message before moving it to the poison queue. |
| newBatchThreshold | batchSize/2 | Whenever the number of messages being processed concurrently gets down to this number, the runtime retrieves another batch. |

## SendGrid

Configuration setting for the [SendGrind output binding](functions-bindings-sendgrid)

```
{
"sendGrid": {
"from": "Contoso Group <admin@contoso.com>"
}
}
```


| Property | Default | Description |
|---|---|---|
| from | n/a | The sender's email address across all functions. |

## serviceBus

Configuration setting for [Service Bus triggers and bindings](functions-bindings-service-bus).

```
{
"serviceBus": {
"maxConcurrentCalls": 16,
"prefetchCount": 100,
"autoRenewTimeout": "00:05:00",
"autoComplete": true
}
}
```


| Property | Default | Description |
|---|---|---|
| maxConcurrentCalls | 16 | The maximum number of concurrent calls to the callback that the message pump should initiate. By default, the Functions runtime processes multiple messages concurrently. To direct the runtime to process only a single queue or topic message at a time, set `maxConcurrentCalls` to 1. |
| prefetchCount | n/a | The default PrefetchCount that will be used by the underlying ServiceBusReceiver. |
| autoRenewTimeout | 00:05:00 | The maximum duration within which the message lock will be renewed automatically. |
| autoComplete | true | When true, the trigger completes the message processing automatically on successful execution of the operation. When false, it is the responsibility of the function to complete the message before returning. |

## singleton

Configuration settings for Singleton lock behavior. For more information, see [GitHub issue about singleton support](https://github.com/Azure/azure-webjobs-sdk-script/issues/912).

```
{
"singleton": {
"lockPeriod": "00:00:15",
"listenerLockPeriod": "00:01:00",
"listenerLockRecoveryPollingInterval": "00:01:00",
"lockAcquisitionTimeout": "00:01:00",
"lockAcquisitionPollingInterval": "00:00:03"
}
}
```


| Property | Default | Description |
|---|---|---|
| lockPeriod | 00:00:15 | The period that function level locks are taken for. The locks auto-renew. |
| listenerLockPeriod | 00:01:00 | The period that listener locks are taken for. |
| listenerLockRecoveryPollingInterval | 00:01:00 | The time interval used for listener lock recovery if a listener lock couldn't be acquired on startup. |
| lockAcquisitionTimeout | 00:01:00 | The maximum amount of time the runtime tries to acquire a lock. |
| lockAcquisitionPollingInterval | n/a | The interval between lock acquisition attempts. |

## tracing

*Version 1.x*

Configuration settings for logs that you create by using a `TraceWriter`

object. To learn more, see [C# Logging].

```
{
"tracing": {
"consoleLevel": "verbose",
"fileLoggingMode": "debugOnly"
}
}
```


| Property | Default | Description |
|---|---|---|
| consoleLevel | info | The tracing level for console logging. Options are: `off` , `error` , `warning` , `info` , and `verbose` . |
| fileLoggingMode | debugOnly | The tracing level for file logging. Options are `never` , `always` , `debugOnly` . |

## watchDirectories

A set of [shared code directories](functions-reference-csharp#watched-directories) that should be monitored for changes. Ensures that when code in these directories is changed, the changes are picked up by your functions.

```
{
"watchDirectories": [ "Shared" ]
}
```

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-host-json-v1 -->

# host.json reference for Azure Functions 1.x

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The *host.json* metadata file contains configuration options that affect all functions in a function app instance. This article lists the settings that are available for the version 1.x runtime. The JSON schema is at [http://json.schemastore.org/host](http://json.schemastore.org/host).

Note

This article is for Azure Functions 1.x. For a reference of host.json in Functions 2.x and later, see [host.json reference for Azure Functions 2.x](functions-host-json).

Other function app configuration options are managed in your [app settings](functions-app-settings).

Some host.json settings are only used when running locally in the [local.settings.json](functions-develop-local#local-settings-file) file.

## Sample host.json file

The following sample *host.json* files have all possible options specified.

```
{
"aggregator": {
"batchSize": 1000,
"flushTimeout": "00:00:30"
},
"applicationInsights": {
"sampling": {
"isEnabled": true,
"maxTelemetryItemsPerSecond" : 5
}
},
"documentDB": {
"connectionMode": "Gateway",
"protocol": "Https",
"leaseOptions": {
"leasePrefix": "prefix"
}
},
"eventHub": {
"maxBatchSize": 64,
"prefetchCount": 256,
"batchCheckpointFrequency": 1
},
"functions": [ "QueueProcessor", "GitHubWebHook" ],
"functionTimeout": "00:05:00",
"healthMonitor": {
"enabled": true,
"healthCheckInterval": "00:00:10",
"healthCheckWindow": "00:02:00",
"healthCheckThreshold": 6,
"counterThreshold": 0.80
},
"http": {
"routePrefix": "api",
"maxOutstandingRequests": 20,
"maxConcurrentRequests": 10,
"dynamicThrottlesEnabled": false
},
"id": "9f4ea53c5136457d883d685e57164f08",
"logger": {
"categoryFilter": {
"defaultLevel": "Information",
"categoryLevels": {
"Host": "Error",
"Function": "Error",
"Host.Aggregator": "Information"
}
}
},
"queues": {
"maxPollingInterval": 2000,
"visibilityTimeout" : "00:00:30",
"batchSize": 16,
"maxDequeueCount": 5,
"newBatchThreshold": 8
},
"sendGrid": {
"from": "Contoso Group <admin@contoso.com>"
},
"serviceBus": {
"maxConcurrentCalls": 16,
"prefetchCount": 100,
"autoRenewTimeout": "00:05:00",
"autoComplete": true
},
"singleton": {
"lockPeriod": "00:00:15",
"listenerLockPeriod": "00:01:00",
"listenerLockRecoveryPollingInterval": "00:01:00",
"lockAcquisitionTimeout": "00:01:00",
"lockAcquisitionPollingInterval": "00:00:03"
},
"tracing": {
"consoleLevel": "verbose",
"fileLoggingMode": "debugOnly"
},
"watchDirectories": [ "Shared" ],
}
```


The following sections of this article explain each top-level property. All are optional unless otherwise indicated.

## aggregator

Specifies how many function invocations are aggregated when [calculating metrics for Application Insights](configure-monitoring#configure-the-aggregator).

```
{
"aggregator": {
"batchSize": 1000,
"flushTimeout": "00:00:30"
}
}
```


| Property | Default | Description |
|---|---|---|
| batchSize | 1000 | Maximum number of requests to aggregate. |
| flushTimeout | 00:00:30 | Maximum time period to aggregate. |

Function invocations are aggregated when the first of the two limits are reached.

## applicationInsights

Controls the [sampling feature in Application Insights](configure-monitoring#configure-sampling).

```
{
"applicationInsights": {
"sampling": {
"isEnabled": true,
"maxTelemetryItemsPerSecond" : 5
}
}
}
```


| Property | Default | Description |
|---|---|---|
| isEnabled | true | Enables or disables sampling. |
| maxTelemetryItemsPerSecond | 5 | The threshold at which sampling begins. |

## DocumentDB

Configuration settings for the [Azure Cosmos DB trigger and bindings](functions-bindings-cosmosdb).

```
{
"documentDB": {
"connectionMode": "Gateway",
"protocol": "Https",
"leaseOptions": {
"leasePrefix": "prefix1"
}
}
}
```


| Property | Default | Description |
|---|---|---|
| GatewayMode | Gateway | The connection mode used by the function when connecting to the Azure Cosmos DB service. Options are `Direct` and `Gateway` |
| Protocol | Https | The connection protocol used by the function when connection to the Azure Cosmos DB service. Read
|

## durableTask

Configuration settings for [Durable Functions](durable/durable-functions-overview).

Note

All major versions of Durable Functions are supported on all versions of the Azure Functions runtime. However, the schema of the *host.json* configuration differs slightly depending on the version of the Azure Functions runtime and the version of the Durable Functions extension that you use.

The following code provides two examples of `durableTask`

settings in *host.json*: one for Durable Functions 2.x and one for Durable Functions 1.x. You can use both examples with Azure Functions 2.0 and 3.0. With Azure Functions 1.0, the available settings are the same, but the `durableTask`

section of *host.json* is located in the root of the *host.json* configuration instead of being a field under `extensions`

.

```
{
"extensions": {
"durableTask": {
"hubName": "MyTaskHub",
"defaultVersion": "1.0",
"versionMatchStrategy": "CurrentOrOlder",
"versionFailureStrategy": "Reject",
"storageProvider": {
"connectionStringName": "AzureWebJobsStorage",
"controlQueueBatchSize": 32,
"controlQueueBufferThreshold": 256,
"controlQueueVisibilityTimeout": "00:05:00",
"FetchLargeMessagesAutomatically": true,
"maxQueuePollingInterval": "00:00:30",
"partitionCount": 4,
"trackingStoreConnectionStringName": "TrackingStorage",
"trackingStoreNamePrefix": "DurableTask",
"useLegacyPartitionManagement": false,
"useTablePartitionManagement": true,
"workItemQueueVisibilityTimeout": "00:05:00",
"QueueClientMessageEncoding": "UTF8"
},
"tracing": {
"traceInputsAndOutputs": false,
"traceReplayEvents": false,
},
"httpSettings":{
"defaultAsyncRequestSleepTimeMilliseconds": 30000,
"useForwardedHost": false,
},
"notifications": {
"eventGrid": {
"topicEndpoint": "https://topic_name.westus2-1.eventgrid.azure.net/api/events",
"keySettingName": "EventGridKey",
"publishRetryCount": 3,
"publishRetryInterval": "00:00:30",
"publishEventTypes": [
"Started",
"Completed",
"Failed",
"Terminated"
]
}
},
"maxConcurrentActivityFunctions": 10,
"maxConcurrentOrchestratorFunctions": 10,
"maxConcurrentEntityFunctions": 10,
"extendedSessionsEnabled": false,
"extendedSessionIdleTimeoutInSeconds": 30,
"useAppLease": true,
"useGracefulShutdown": false,
"maxEntityOperationBatchSize": 50,
"maxOrchestrationActions": 100000,
"storeInputsInOrchestrationHistory": false
}
}
}
```


| Property | Default value | Description |
|---|---|---|
| hubName | TestHubName (DurableFunctionsHub in v1.x) | The name of the hub that stores the current state of a function app. Task hub names must start with a letter and consist of only letters and numbers. If you don't specify a name, the default value is used. Alternate task hub names can be used to isolate multiple Durable Functions applications from each other, even if they use the same storage back end. For more information, see
|

[orchestration versioning](durable/durable-functions-orchestration-versioning)feature to enable scenarios like zero-downtime deployments with breaking changes. You can use any string value for the version.`None`

, `Strict`

, and `CurrentOrOlder`

. For detailed explanations, see [Orchestration versioning](durable/durable-functions-orchestration-versioning).`defaultVersion`

value. Valid values are `Reject`

and `Fail`

. For detailed explanations, see [Orchestration versioning](durable/durable-functions-orchestration-versioning).**Consumption plan for Python**: 32**Consumption plan for other languages**: 128**Dedicated or Premium plan**: 256*hh:mm:ss*format.*hh:mm:ss*format.`true`

, large messages that exceed the queue size limit are retrieved. When this setting is `false`

, a blob URL that points to each large message is retrieved.**Consumption plan**: 10**Dedicated or Premium plan**: 10 times the number of processors on the current machine**Consumption plan**: 5**Dedicated or Premium plan**: 10 times the number of processors on the current machine**Consumption plan**: 5**Dedicated or Premium plan**: 10 times the number of processors on the current machine[durable task scheduler](durable/durable-task-scheduler/durable-task-scheduler). Otherwise, the maximum number of concurrent entity executions is limited to the`maxConcurrentOrchestratorFunctions`

value.*hh:mm:ss*format. Higher values can result in higher message processing latencies. Lower values can result in higher storage costs because of increased storage transactions.connectionStringName (v2.x)

azureStorageConnectionStringName (v1.x)

trackingStoreConnectionStringName

`connectionStringName`

value (v2.x) or `azureStorageConnectionStringName`

value (v1.x) connection is used.`trackingStoreConnectionStringName`

is specified. If you don't specify a prefix, the default value of `DurableTask`

is used. If `trackingStoreConnectionStringName`

isn't specified, the History and Instances tables use the `hubName`

value as their prefix, and the `trackingStoreNamePrefix`

setting is ignored.`true`

, the entire contents of function inputs and outputs are logged.`EventGridTopicEndpoint`

URL.*hh:mm:ss*format.`Started`

, `Completed`

, `Failed`

, and `Terminated`

.`extendedSessionsEnabled`

setting is `true`

.[Disaster recovery and geo-distribution in Durable Functions](durable/durable-functions-disaster-recovery-geo-distribution). This setting is available starting in v2.3.0.`false`

, an algorithm is used that reduces the possibility of duplicate function execution when scaling out. This setting is available starting in v2.3.0. **Setting this value to**.`true`

isn't recommendedIn v2.x: false

`true`

, an algorithm is used that's designed to reduce costs for Azure Storage v2 accounts. This setting is available starting in WebJobs.Extensions.DurableTask v2.10.0. Using this setting with a managed identity requires WebJobs.Extensions.DurableTask v3.x or later, or Worker.Extensions.DurableTask v1.2.x or later.**Consumption plan**: 50**Dedicated or Premium plan**: 5,000[batch](durable/durable-functions-perf-and-scale#entity-operation-batching). If this value is 1, batching is disabled, and a separate function invocation processes each operation message. This setting is available starting in v2.6.1.`true`

, the Durable Task Framework saves activity inputs in the History table, and activity function inputs appear in orchestration history query results.`DurableTaskClient`

uses the gRPC client to manage orchestration instances. This setting applies to Durable Functions .NET isolated worker and Java apps.*hh:mm:ss*format for the HTTP client used by the gRPC client in Durable Functions. The client is currently supported for .NET isolated worker apps (.NET 6 and later versions) and for Java apps.Many of these settings are for optimizing performance. For more information, see [Performance and scale](durable/durable-functions-perf-and-scale).

## eventHub

Configuration settings for [Event Hub triggers and bindings](functions-bindings-event-hubs?tabs=functionsv1#hostjson-settings).

## functions

A list of functions that the job host runs. An empty array means run all functions. Intended for use only when [running locally](functions-run-local). In function apps in Azure, you should instead follow the steps in [How to disable functions in Azure Functions](disable-function) to disable specific functions rather than using this setting.

```
{
"functions": [ "QueueProcessor", "GitHubWebHook" ]
}
```


## functionTimeout

Indicates the timeout duration for all functions. In a serverless Consumption plan, the valid range is from 1 second to 10 minutes, and the default value is 5 minutes. In an App Service plan, there is no overall limit and the default is *null*, which indicates no timeout.

```
{
"functionTimeout": "00:05:00"
}
```


## healthMonitor

Configuration settings for [Host health monitor](https://github.com/Azure/azure-webjobs-sdk-script/wiki/Host-Health-Monitor).

```
{
"healthMonitor": {
"enabled": true,
"healthCheckInterval": "00:00:10",
"healthCheckWindow": "00:02:00",
"healthCheckThreshold": 6,
"counterThreshold": 0.80
}
}
```


| Property | Default | Description |
|---|---|---|
| enabled | true | Specifies whether the feature is enabled. |
| healthCheckInterval | 10 seconds | The time interval between the periodic background health checks. |
| healthCheckWindow | 2 minutes | A sliding time window used with the `healthCheckThreshold` setting. |
| healthCheckThreshold | 6 | Maximum number of times the health check can fail before a host recycle is initiated. |
| counterThreshold | 0.80 | The threshold at which a performance counter will be considered unhealthy. |

## http

Configuration settings for [http triggers and bindings](functions-bindings-http-webhook).

```
{
"http": {
"routePrefix": "api",
"maxOutstandingRequests": 200,
"maxConcurrentRequests": 100,
"dynamicThrottlesEnabled": true
}
}
```


| Property | Default | Description |
|---|---|---|
| dynamicThrottlesEnabled | false | When enabled, this setting causes the request processing pipeline to periodically check system performance counters like connections/threads/processes/memory/cpu/etc. and if any of those counters are over a built-in high threshold (80%), requests are rejected with a 429 "Too Busy" response until the counter(s) return to normal levels. |
| maxConcurrentRequests | unbounded (`-1` ) |
The maximum number of HTTP functions that will be executed in parallel. This allows you to control concurrency, which can help manage resource utilization. For example, you might have an HTTP function that uses a lot of system resources (memory/cpu/sockets) such that it causes issues when concurrency is too high. Or you might have a function that makes outbound requests to a third party service, and those calls need to be rate limited. In these cases, applying a throttle here can help. |
| maxOutstandingRequests | unbounded (`-1` ) |
The maximum number of outstanding requests that are held at any given time. This limit includes requests that are queued but have not started executing, and any in progress executions. Any incoming requests over this limit are rejected with a 429 "Too Busy" response. That allows callers to employ time-based retry strategies, and also helps you to control maximum request latencies. This only controls queuing that occurs within the script host execution path. Other queues such as the ASP.NET request queue will still be in effect and unaffected by this setting. |
| routePrefix | api | The route prefix that applies to all routes. Use an empty string to remove the default prefix. |

## id

The unique ID for a job host. Can be a lower case GUID with dashes removed. Required when running locally. When running in Azure, we recommend that you not set an ID value. An ID is generated automatically in Azure when `id`

is omitted.

If you share a Storage account across multiple function apps, make sure that each function app has a different `id`

. You can omit the `id`

property or manually set each function app's `id`

to a different value. The timer trigger uses a storage lock to ensure that there will be only one timer instance when a function app scales out to multiple instances. If two function apps share the same `id`

and each uses a timer trigger, only one timer runs.

```
{
"id": "9f4ea53c5136457d883d685e57164f08"
}
```


## logger

Controls filtering for logs written by an [ILogger](functions-dotnet-class-library#ilogger) object or by [context.log](functions-reference-node#contextlog-method).

```
{
"logger": {
"categoryFilter": {
"defaultLevel": "Information",
"categoryLevels": {
"Host": "Error",
"Function": "Error",
"Host.Aggregator": "Information"
}
}
}
}
```


| Property | Default | Description |
|---|---|---|
| categoryFilter | n/a | Specifies filtering by category |
| defaultLevel | Information | For any categories not specified in the `categoryLevels` array, send logs at this level and above to Application Insights. |
| categoryLevels | n/a | An array of categories that specifies the minimum log level to send to Application Insights for each category. The category specified here controls all categories that begin with the same value, and longer values take precedence. In the preceding sample host.json file, all categories that begin with "Host.Aggregator" log at `Information` level. All other categories that begin with "Host", such as "Host.Executor", log at `Error` level. |

## queues

Configuration settings for [Storage queue triggers and bindings](functions-bindings-storage-queue).

```
{
"queues": {
"maxPollingInterval": 2000,
"visibilityTimeout" : "00:00:30",
"batchSize": 16,
"maxDequeueCount": 5,
"newBatchThreshold": 8
}
}
```


| Property | Default | Description |
|---|---|---|
| maxPollingInterval | 60000 | The maximum interval in milliseconds between queue polls. |
| visibilityTimeout | 0 | The time interval between retries when processing of a message fails. |
| batchSize | 16 | The number of queue messages that the Functions runtime retrieves simultaneously and processes in parallel. When the number being processed gets down to the `newBatchThreshold` , the runtime gets another batch and starts processing those messages. So the maximum number of concurrent messages being processed per function is `batchSize` plus `newBatchThreshold` . This limit applies separately to each queue-triggered function. If you want to avoid parallel execution for messages received on one queue, you can set `batchSize` to 1. However, this setting eliminates concurrency only so long as your function app runs on a single virtual machine (VM). If the function app scales out to multiple VMs, each VM could run one instance of each queue-triggered function.The maximum `batchSize` is 32. |
| maxDequeueCount | 5 | The number of times to try processing a message before moving it to the poison queue. |
| newBatchThreshold | batchSize/2 | Whenever the number of messages being processed concurrently gets down to this number, the runtime retrieves another batch. |

## SendGrid

Configuration setting for the [SendGrind output binding](functions-bindings-sendgrid)

```
{
"sendGrid": {
"from": "Contoso Group <admin@contoso.com>"
}
}
```


| Property | Default | Description |
|---|---|---|
| from | n/a | The sender's email address across all functions. |

## serviceBus

Configuration setting for [Service Bus triggers and bindings](functions-bindings-service-bus).

```
{
"serviceBus": {
"maxConcurrentCalls": 16,
"prefetchCount": 100,
"autoRenewTimeout": "00:05:00",
"autoComplete": true
}
}
```


| Property | Default | Description |
|---|---|---|
| maxConcurrentCalls | 16 | The maximum number of concurrent calls to the callback that the message pump should initiate. By default, the Functions runtime processes multiple messages concurrently. To direct the runtime to process only a single queue or topic message at a time, set `maxConcurrentCalls` to 1. |
| prefetchCount | n/a | The default PrefetchCount that will be used by the underlying ServiceBusReceiver. |
| autoRenewTimeout | 00:05:00 | The maximum duration within which the message lock will be renewed automatically. |
| autoComplete | true | When true, the trigger completes the message processing automatically on successful execution of the operation. When false, it is the responsibility of the function to complete the message before returning. |

## singleton

Configuration settings for Singleton lock behavior. For more information, see [GitHub issue about singleton support](https://github.com/Azure/azure-webjobs-sdk-script/issues/912).

```
{
"singleton": {
"lockPeriod": "00:00:15",
"listenerLockPeriod": "00:01:00",
"listenerLockRecoveryPollingInterval": "00:01:00",
"lockAcquisitionTimeout": "00:01:00",
"lockAcquisitionPollingInterval": "00:00:03"
}
}
```


| Property | Default | Description |
|---|---|---|
| lockPeriod | 00:00:15 | The period that function level locks are taken for. The locks auto-renew. |
| listenerLockPeriod | 00:01:00 | The period that listener locks are taken for. |
| listenerLockRecoveryPollingInterval | 00:01:00 | The time interval used for listener lock recovery if a listener lock couldn't be acquired on startup. |
| lockAcquisitionTimeout | 00:01:00 | The maximum amount of time the runtime tries to acquire a lock. |
| lockAcquisitionPollingInterval | n/a | The interval between lock acquisition attempts. |

## tracing

*Version 1.x*

Configuration settings for logs that you create by using a `TraceWriter`

object. To learn more, see [C# Logging].

```
{
"tracing": {
"consoleLevel": "verbose",
"fileLoggingMode": "debugOnly"
}
}
```


| Property | Default | Description |
|---|---|---|
| consoleLevel | info | The tracing level for console logging. Options are: `off` , `error` , `warning` , `info` , and `verbose` . |
| fileLoggingMode | debugOnly | The tracing level for file logging. Options are `never` , `always` , `debugOnly` . |

## watchDirectories

A set of [shared code directories](functions-reference-csharp#watched-directories) that should be monitored for changes. Ensures that when code in these directories is changed, the changes are picked up by your functions.

```
{
"watchDirectories": [ "Shared" ]
}
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-grid-output -->

# Azure Event Grid output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the Event Grid output binding to write events to a custom topic. You must have a valid [access key for the custom topic](../event-grid/security-authenticate-publishing-clients). The Event Grid output binding doesn't support shared access signature (SAS) tokens.

For information on setup and configuration details, see [How to work with Event Grid triggers and bindings in Azure Functions](event-grid-how-tos).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

Important

The Event Grid output binding is only available for Functions 2.x and higher.

## Example

The type of the output parameter used with an Event Grid output binding depends on the Functions runtime version, the binding extension version, and the modality of the C# function. The C# function can be created using one of the following C# modes:

[In-process class library](functions-dotnet-class-library): compiled C# function that runs in the same process as the Functions runtime.[Isolated worker process class library](dotnet-isolated-process-guide): compiled C# function that runs in a worker process isolated from the runtime.

The following example shows how the custom type is used in both the trigger and an Event Grid output binding:

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.Logging;
namespace SampleApp
{
public static class EventGridFunction
{
[Function(nameof(EventGridFunction))]
[EventGridOutput(TopicEndpointUri = "MyEventGridTopicUriSetting", TopicKeySetting = "MyEventGridTopicKeySetting")]
public static MyEventType Run([EventGridTrigger] MyEventType input, FunctionContext context)
{
var logger = context.GetLogger(nameof(EventGridFunction));
logger.LogInformation(input.Data?.ToString());
var outputEvent = new MyEventType()
{
Id = "unique-id",
Subject = "abc-subject",
Data = new Dictionary<string, object>
{
{ "myKey", "myValue" }
}
};
return outputEvent;
}
}
public class MyEventType
{
public string? Id { get; set; }
public string? Topic { get; set; }
public string? Subject { get; set; }
public string? EventType { get; set; }
public DateTime EventTime { get; set; }
public IDictionary<string, object>? Data { get; set; }
}
}
```


The following example shows a Java function that writes a message to an Event Grid custom topic. The function uses the binding's `setValue`

method to output a string.

```
public class Function {
@FunctionName("EventGridTriggerTest")
public void run(@EventGridTrigger(name = "event") String content,
@EventGridOutput(name = "outputEvent", topicEndpointUri = "MyEventGridTopicUriSetting", topicKeySetting = "MyEventGridTopicKeySetting") OutputBinding<String> outputEvent,
final ExecutionContext context) {
context.getLogger().info("Java EventGrid trigger processed a request." + content);
final String eventGridOutputDocument = "{\"id\": \"1807\", \"eventType\": \"recordInserted\", \"subject\": \"myapp/cars/java\", \"eventTime\":\"2017-08-10T21:03:07+00:00\", \"data\": {\"make\": \"Ducati\",\"model\": \"Monster\"}, \"dataVersion\": \"1.0\"}";
outputEvent.setValue(eventGridOutputDocument);
}
}
```


You can also use a POJO class to send Event Grid messages.

```
public class Function {
@FunctionName("EventGridTriggerTest")
public void run(@EventGridTrigger(name = "event") String content,
@EventGridOutput(name = "outputEvent", topicEndpointUri = "MyEventGridTopicUriSetting", topicKeySetting = "MyEventGridTopicKeySetting") OutputBinding<EventGridEvent> outputEvent,
final ExecutionContext context) {
context.getLogger().info("Java EventGrid trigger processed a request." + content);
final EventGridEvent eventGridOutputDocument = new EventGridEvent();
eventGridOutputDocument.setId("1807");
eventGridOutputDocument.setEventType("recordInserted");
eventGridOutputDocument.setEventTime("2017-08-10T21:03:07+00:00");
eventGridOutputDocument.setDataVersion("1.0");
eventGridOutputDocument.setSubject("myapp/cars/java");
eventGridOutputDocument.setData("{\"make\": \"Ducati\",\"model\":\"monster\"");
outputEvent.setValue(eventGridOutputDocument);
}
}
class EventGridEvent {
private String id;
private String eventType;
private String subject;
private String eventTime;
private String dataVersion;
private String data;
public String getId() {
return id;
}
public String getData() {
return data;
}
public void setData(String data) {
this.data = data;
}
public String getDataVersion() {
return dataVersion;
}
public void setDataVersion(String dataVersion) {
this.dataVersion = dataVersion;
}
public String getEventTime() {
return eventTime;
}
public void setEventTime(String eventTime) {
this.eventTime = eventTime;
}
public String getSubject() {
return subject;
}
public void setSubject(String subject) {
this.subject = subject;
}
public String getEventType() {
return eventType;
}
public void setEventType(String eventType) {
this.eventType = eventType;
}
public void setId(String id) {
this.id = id;
}
}
```


The following example shows a timer triggered [TypeScript function](functions-reference-node?tabs=typescript) that outputs a single event:

```
import { app, EventGridPartialEvent, InvocationContext, output, Timer } from '@azure/functions';
export async function timerTrigger1(myTimer: Timer, context: InvocationContext): Promise<EventGridPartialEvent> {
const timeStamp = new Date().toISOString();
return {
id: 'message-id',
subject: 'subject-name',
dataVersion: '1.0',
eventType: 'event-type',
data: {
name: 'John Henry',
},
eventTime: timeStamp,
};
}
app.timer('timerTrigger1', {
schedule: '0 */5 * * * *',
return: output.eventGrid({
topicEndpointUri: 'MyEventGridTopicUriSetting',
topicKeySetting: 'MyEventGridTopicKeySetting',
}),
handler: timerTrigger1,
});
```


To output multiple events, return an array instead of a single object. For example:

```
const timeStamp = new Date().toISOString();
return [
{
id: 'message-id',
subject: 'subject-name',
dataVersion: '1.0',
eventType: 'event-type',
data: {
name: 'John Henry',
},
eventTime: timeStamp,
},
{
id: 'message-id-2',
subject: 'subject-name',
dataVersion: '1.0',
eventType: 'event-type',
data: {
name: 'John Doe',
},
eventTime: timeStamp,
},
];
```


The following example shows a timer triggered [JavaScript function](functions-reference-node) that outputs a single event:

```
const { app, output } = require('@azure/functions');
const eventGridOutput = output.eventGrid({
topicEndpointUri: 'MyEventGridTopicUriSetting',
topicKeySetting: 'MyEventGridTopicKeySetting',
});
app.timer('timerTrigger1', {
schedule: '0 */5 * * * *',
return: eventGridOutput,
handler: (myTimer, context) => {
const timeStamp = new Date().toISOString();
return {
id: 'message-id',
subject: 'subject-name',
dataVersion: '1.0',
eventType: 'event-type',
data: {
name: 'John Henry',
},
eventTime: timeStamp,
};
},
});
```


To output multiple events, return an array instead of a single object. For example:

```
const timeStamp = new Date().toISOString();
return [
{
id: 'message-id',
subject: 'subject-name',
dataVersion: '1.0',
eventType: 'event-type',
data: {
name: 'John Henry',
},
eventTime: timeStamp,
},
{
id: 'message-id-2',
subject: 'subject-name',
dataVersion: '1.0',
eventType: 'event-type',
data: {
name: 'John Doe',
},
eventTime: timeStamp,
},
];
```


The following example demonstrates how to configure a function to output an Event Grid event message. The section where `type`

is set to `eventGrid`

configures the values needed to establish an Event Grid output binding.

```
{
"bindings": [
{
"type": "eventGrid",
"name": "outputEvent",
"topicEndpointUri": "MyEventGridTopicUriSetting",
"topicKeySetting": "MyEventGridTopicKeySetting",
"direction": "out"
},
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
}
]
}
```


In your function, use the `Push-OutputBinding`

to send an event to a custom topic through the Event Grid output binding.

```
using namespace System.Net
# Input bindings are passed in via param block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell HTTP trigger function processed a request."
# Interact with query parameters or the body of the request.
$message = $Request.Query.Message
Push-OutputBinding -Name outputEvent -Value @{
id = "1"
eventType = "testEvent"
subject = "testapp/testPublish"
eventTime = "2020-08-27T21:03:07+00:00"
data = @{
Message = $message
}
dataVersion = "1.0"
}
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = 200
Body = "OK"
})
```


The following example shows a trigger binding and a Python function that uses the binding. It then sends in an event to the custom topic, as specified by the `topicEndpointUri`

. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

Here's the function in the function_app.py file:

```
import logging
import azure.functions as func
import datetime
app = func.FunctionApp()
@app.function_name(name="eventgrid_output")
@app.event_grid_trigger(arg_name="eventGridEvent")
@app.event_grid_output(
arg_name="outputEvent",
topic_endpoint_uri="MyEventGridTopicUriSetting",
topic_key_setting="MyEventGridTopicKeySetting")
def eventgrid_output(eventGridEvent: func.EventGridEvent,
outputEvent: func.Out[func.EventGridOutputEvent]) -> None:
logging.log("eventGridEvent: ", eventGridEvent)
outputEvent.set(
func.EventGridOutputEvent(
id="test-id",
data={"tag1": "value1", "tag2": "value2"},
subject="test-subject",
event_type="test-event-1",
event_time=datetime.datetime.utcnow(),
data_version="1.0"))
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attribute to configure the binding. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#event-grid-output).

The attribute's constructor takes the name of an application setting that contains the name of the custom topic, and the name of an application setting that contains the topic key.

The following table explains the parameters for the `EventGridOutputAttribute`

.

| Parameter | Description |
|---|---|
TopicEndpointUri |
The name of an app setting that contains the URI for the custom topic, such as `MyTopicEndpointUri` . |
TopicKeySetting |
The name of an app setting that contains an access key for the custom topic. |
connection* |
The value of the common prefix for the setting that contains the topic endpoint URI. For more information about the naming format of this application setting, see
|

## Annotations

For Java classes, use the [EventGridAttribute](https://github.com/Azure/azure-functions-java-library/blob/dev/src/main/java/com/microsoft/azure/functions/annotation/EventGridOutput.java) attribute.

The attribute's constructor takes the name of an app setting that contains the name of the custom topic, and the name of an app setting that contains the topic key. For more information about these settings, see [Output - configuration](#configuration). Here's an `EventGridOutput`

attribute example:

```
public class Function {
@FunctionName("EventGridTriggerTest")
public void run(@EventGridTrigger(name = "event") String content,
@EventGridOutput(name = "outputEvent", topicEndpointUri = "MyEventGridTopicUriSetting", topicKeySetting = "MyEventGridTopicKeySetting") OutputBinding<String> outputEvent, final ExecutionContext context) {
...
}
}
```


## Configuration

The following table explains the properties that you can set on the `options`

object passed to the `output.eventGrid()`

method.

| Property | Description |
|---|---|
topicEndpointUri |
The name of an app setting that contains the URI for the custom topic, such as `MyTopicEndpointUri` . |
topicKeySetting |
The name of an app setting that contains an access key for the custom topic. |
connection* |
The value of the common prefix for the setting that contains the topic endpoint URI. When setting the `connection` property, the `topicEndpointUri` and `topicKeySetting` properties shouldn't be set. For more information about the naming format of this application setting, see
|

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `eventGrid` . |
direction |
Must be set to `out` . This parameter is set automatically when you create the binding in the Azure portal. |
name |
The variable name used in function code that represents the event. |
topicEndpointUri |
The name of an app setting that contains the URI for the custom topic, such as `MyTopicEndpointUri` . |
topicKeySetting |
The name of an app setting that contains an access key for the custom topic. |
connection* |
The value of the common prefix for the setting that contains the topic endpoint URI. For more information about the naming format of this application setting, see
|

*Support for identity-based connections requires version 3.3.x or higher of the extension.

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

Important

Make sure that you set the value of `TopicEndpointUri`

to the name of an app setting that contains the URI of the custom topic. Don't specify the URI of the custom topic directly in this property. The same applies when using `Connection`

.

See the [Example section](#example) for complete examples.

## Usage

The parameter type supported by the Event Grid output binding depends on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to write a single event, the Event Grid output binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The event as a string. |
`byte[]` |
The bytes of the event message. |
| JSON serializable types | An object representing a JSON event. Functions tries to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write multiple events, the Event Grid output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single event types |
An array containing multiple events. Each entry represents one event. |

For other output scenarios, create and use an [EventGridPublisherClient](/en-us/dotnet/api/azure.messaging.eventgrid.eventgridpublisherclient) with other types from [Azure.Messaging.EventGrid](/en-us/dotnet/api/azure.messaging.eventgrid) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

Send individual messages by calling a method parameter such as `out EventGridOutput paramName`

, and write multiple messages with `ICollector<EventGridOutput>`

.

Access the output event by using the `Push-OutputBinding`

cmdlet to send an event to the Event Grid output binding.

There are two options for outputting an Event Grid message from a function:

**Return value**: Set the`name`

property in*function.json*to`$return`

. With this configuration, the function's return value is persisted as an Event Grid message.**Imperative**: Pass a value to the[set](/en-us/python/api/azure-functions/azure.functions.out#set-val--t-----none)method of the parameter declared as an[Out](/en-us/python/api/azure-functions/azure.functions.out)type. The value passed to`set`

is persisted as an Event Grid message.

The output function parameter must be defined as `func.Out[str]`

, `func.Out[bytes]`

, `func.Out[func.EventGridOutputEvent]`

, or `func.Out[List[func.EventGridOutputEvent]]`

. Refer to the [output example](#example) for details.

## Connections

There are two ways of authenticating to an Event Grid topic when using the Event Grid output binding:

| Authentication method | Description |
|---|---|
| Using a topic key | Set the `TopicEndpointUri` and `TopicKeySetting` properties, as described in
|
| Using an identity | Set the `Connection` property to the name of a shared prefix for multiple application settings, together defining
|

### Use a topic key

Use the following steps to configure a topic key:

Follow the steps in

[Get access keys](../event-grid/get-access-keys)to obtain the topic key for your Event Grid topic.In your application settings, create a setting that defines the topic key value. Use the name of this setting for the

`TopicKeySetting`

property of the binding.In your application settings, create a setting that defines the topic endpoint. Use the name of this setting for the

`TopicEndpointUri`

property of the binding.

### Identity-based authentication

When using version 3.3.x or higher of the extension, you can connect to an Event Grid topic using an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis) to avoid having to obtain and work with topic keys.

You need to create an application setting that returns the topic endpoint URI. The name of the setting should combine a *unique common prefix* (for example, `myawesometopic`

) with the value `__topicEndpointUri`

. Then, you must use that common prefix (in this case, `myawesometopic`

) when you define the `Connection`

property in the binding.

In this mode, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Topic Endpoint URI | `<CONNECTION_NAME_PREFIX>__topicEndpointUri` |
The topic endpoint. | `https://<topic-name>.centralus-1.eventgrid.azure.net/api/events` |

More properties can be used to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

Note

When using [Azure App Configuration](../azure-app-configuration/quickstart-azure-functions-csharp) or [Key Vault](/en-us/azure/key-vault/general/overview) to provide settings for managed identity-based connections, setting names should use a valid key separator such as `:`

or `/`

in place of the `__`

to ensure names are resolved correctly.

For example, `<CONNECTION_NAME_PREFIX>:topicEndpointUri`

.

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

You must create a role assignment that provides access to your Event Grid topic at runtime. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) are not sufficient. The following table shows built-in roles that are recommended when using the Event Hubs extension in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles |
|---|---|
| Output binding |
|

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/scenario-scheduled-tasks -->

# Quickstart: Run scheduled tasks using Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you use the Azure Developer CLI (`azd`

) to create a Timer trigger function to run a scheduled task in Azure Functions. After verifying the code locally, you deploy it to a new serverless function app you create running in a Flex Consumption plan in Azure Functions.

The project source uses `azd`

to create the function app and related resources and to deploy your code to Azure. This deployment follows current best practices for secure and scalable Azure Functions deployments.

By default, the Flex Consumption plan follows a *pay-for-what-you-use* billing model, which means you can complete this article and only incur a small cost of a few USD cents or less in your Azure account.

Important

While [running scheduled tasks](functions-bindings-timer) is supported for all languages, this quickstart scenario currently only has examples for C#, Python, and TypeScript. To complete this quickstart, select one of these supported languages at the top of the article.

## Prerequisites

[Node.js 22](https://nodejs.org/)or above

[Python 3.11](https://www.python.org/)or above

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Initialize the project

Use the `azd init`

command to create a local Azure Functions code project from a template.

In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-dotnet-azd-timer -e scheduled-dotnet`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-timer)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name is also used in the name of the resource group you create in Azure.Run this command to navigate to the app folder:

`cd src`

Create a file named

*local.settings.json*in the`src`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "dotnet-isolated", "TIMER_SCHEDULE": "*/30 * * * * *" } }`

This file is required when running locally.


In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-typescript-azd-timer -e scheduled-ts`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-timer)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name is also used in the name of the resource group you create in Azure.Create a file named

*local.settings.json*in the`src`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "node", "TIMER_SCHEDULE": "*/30 * * * * *" } }`

This file is required when running locally.


In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-python-azd-timer -e scheduled-py`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-python-azd-timer)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name is also used in the name of the resource group you create in Azure.Create a file named

*local.settings.json*in the`src`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "python", "TIMER_SCHEDULE": "*/30 * * * * *" } }`

This file is required when running locally.


## Create and activate a virtual environment

In the root folder, run these commands to create and activate a virtual environment named `.venv`

:

```
python3 -m venv .venv
source .venv/bin/activate
```


If Python doesn't install the venv package on your Linux distribution, run the following command:

```
sudo apt-get install python3-venv
```


## Run in your local environment

Run this command from your app folder in a terminal or command prompt:

`func start`


Run this command from your app folder in a terminal or command prompt:

`npm install npm start`


When the Functions host starts in your local project folder, it writes information about your Timer triggered function to the terminal output. You should see your Timer triggered function execute based on the schedule defined in your code.

The default schedule is

`*/30 * * * * *`

, which runs every 30 seconds.When you're done, press Ctrl+C in the terminal window to stop the

`func.exe`

host process.

- Run
`deactivate`

to shut down the virtual environment.

## Review the code (optional)

You can review the code that defines the Timer trigger function:

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.Timer;
using Microsoft.Extensions.Logging;
namespace Company.Function
{
public class timerFunction
{
private readonly ILogger _logger;
public timerFunction(ILoggerFactory loggerFactory)
{
_logger = loggerFactory.CreateLogger<timerFunction>();
}
[Function("timerFunction")]
public void Run(
[TimerTrigger("%TIMER_SCHEDULE%", RunOnStartup = true)] TimerInfo myTimer,
FunctionContext context
)
{
_logger.LogInformation($"C# Timer trigger function executed at: {DateTime.Now}");
if (myTimer.IsPastDue)
{
_logger.LogWarning("The timer is running late!");
}
}
}
}
```


You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-timer).

```
import { app, InvocationContext, Timer } from '@azure/functions';
export async function timerFunction(myTimer: Timer, context: InvocationContext): Promise<void> {
context.log(`TypeScript Timer trigger function executed at: ${new Date().toISOString()}`);
if (myTimer.isPastDue) {
context.warn("The timer is running late!");
}
}
app.timer('timerFunction', {
schedule: '%TIMER_SCHEDULE%',
runOnStartup: true,
handler: timerFunction
});
```


You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-timer).

```
import datetime
import logging
import azure.functions as func
# Create the function app instance
app = func.FunctionApp()
@app.timer_trigger(schedule="%TIMER_SCHEDULE%",
arg_name="mytimer",
run_on_startup=True,
use_monitor=False)
def timer_function(mytimer: func.TimerRequest) -> None:
utc_timestamp = datetime.datetime.now(datetime.timezone.utc).isoformat()
logging.info(f'Python timer trigger function executed at: {utc_timestamp}')
if mytimer.past_due:
logging.warning('The timer is running late!')
```


You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-python-azd-timer).

After you verify your function locally, it's time to publish it to Azure.

## Deploy to Azure

This project is configured to use the `azd up`

command to deploy your code to a new function app in a Flex Consumption plan in Azure.

Tip

This project includes a set of Bicep files that `azd`

uses to create a secure deployment to a Flex consumption plan that follows best practices.

Run this command to have

`azd`

create the required Azure resources in Azure and deploy your code project to the new function app:`azd up`

The root folder contains the

`azure.yaml`

definition file required by`azd`

.If you're not already signed in, you're asked to authenticate with your Azure account.

When prompted, provide these required deployment parameters:

Parameter Description *Azure subscription*Subscription in which your resources are created. *Azure location*Azure region in which to create the resource group that contains the new Azure resources. Only regions that currently support the Flex Consumption plan are shown. The

`azd up`

command uses your response to these prompts with the Bicep configuration files to complete these deployment tasks:Create and configure these required Azure resources (equivalent to

`azd provision`

):- Flex Consumption plan and function app
- Azure Storage (required) and Application Insights (recommended)
- Access policies and roles for your account
- Service-to-service connections using managed identities (instead of stored connection strings)
- Virtual network to securely run both the function app and the other Azure resources

Package and deploy your code to the deployment container (equivalent to

`azd deploy`

). The app is then started and runs in the deployed package.

After the command completes successfully, you see links to the resources you created.


## Verify deployment

After deployment completes, your Timer trigger function automatically starts running in Azure based on its schedule.

In the

[Azure portal](https://portal.azure.com), go to your new function app.Select

**Log stream**from the left menu to monitor your function executions in real-time.You should see log entries that show your Timer trigger function executing according to its schedule.


## Redeploy your code

Run the `azd up`

command as many times as you need to both provision your Azure resources and deploy code updates to your function app.

Note

Deployed code files are always overwritten by the latest deployment package.

Your initial responses to `azd`

prompts and any environment variables generated by `azd`

are stored locally in your named environment. Use the `azd env get-values`

command to review all of the variables in your environment that were used when creating Azure resources.

## Clean up resources

When you're done working with your function app and related resources, use this command to delete the function app and its related resources from Azure and avoid incurring any further costs:

```
azd down --no-prompt
```


Note

The `--no-prompt`

option instructs `azd`

to delete your resource group without a confirmation from you.

This command doesn't affect your local code project.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-node-upgrade-v4 -->

# Migrate to version 4 of the Node.js programming model for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article discusses the differences between version 3 and version 4 of the Node.js programming model and how to upgrade an existing v3 app. If you want to create a new v4 app instead of upgrading an existing v3 app, see the tutorial for either [Visual Studio Code (VS Code)](how-to-create-function-azure-cli?pivots=programming-language-javascript) or [Azure Functions Core Tools](how-to-create-function-vs-code?pivot=programming-language-javascript). This article uses "tip" alerts to highlight the most important concrete actions that you should take to upgrade your app.
Version 4 is designed to provide Node.js developers with the following benefits:

- Provide a familiar and intuitive experience to Node.js developers.
- Make the file structure flexible with support for full customization.
- Switch to a code-centric approach for defining function configuration.

## Considerations

- The Node.js programming model shouldn't be confused with the Azure Functions runtime:
**Programming model**: Defines how you author your code and is specific to JavaScript and TypeScript.**Runtime**: Defines underlying behavior of Azure Functions and is shared across all languages.

- The version of the programming model is strictly tied to the version of the
npm package. It's versioned independently of the`@azure/functions`

[runtime](functions-versions). Both the runtime and the programming model use the number 4 as their latest major version, but that's a coincidence. - You can't mix the v3 and v4 programming models in the same function app. As soon as you register one v4 function in your app, any v3 functions registered in
*function.json*files are ignored.

## Requirements

Version 4 of the Node.js programming model requires the following minimum versions:

npm package v4.0.0`@azure/functions`

[Node.js](https://nodejs.org/en/about/previous-releases)v18+[Azure Functions Runtime](functions-versions)v4.25+[Azure Functions Core Tools](functions-run-local)v4.0.5382+ (if running locally)

npm package v4.0.0`@azure/functions`

[Node.js](https://nodejs.org/en/about/previous-releases)v18+[TypeScript](https://www.typescriptlang.org/)v4+[Azure Functions Runtime](functions-versions)v4.25+[Azure Functions Core Tools](functions-run-local)v4.0.5382+ (if running locally)

## Include the npm package

In v4, the [ @azure/functions](https://www.npmjs.com/package/@azure/functions) npm package contains the primary source code that backs the Node.js programming model. In previous versions, that code shipped directly in Azure and the npm package had only the TypeScript types. You now need to include this package for both TypeScript and JavaScript apps. You

*can*include the package for existing v3 apps, but it isn't required.

Tip

Make sure the `@azure/functions`

package is listed in the `dependencies`

section (not `devDependencies`

) of your *package.json* file. You can install v4 by using the following command:

```
npm install @azure/functions
```


## Set your app entry point

In v4 of the programming model, you can structure your code however you want. The only files that you need at the root of your app are *host.json* and *package.json*.

Otherwise, you define the file structure by setting the `main`

field in your *package.json* file. You can set the `main`

field to a single file or multiple files by using a [glob pattern](https://wikipedia.org/wiki/Glob_(programming)). The following table shows example values for the `main`

field:

| Example | Description |
|---|---|
`src/index.js` |
Register functions from a single root file. |
`src/functions/*.js` |
Register each function from its own file. |
`src/{index.js,functions/*.js}` |
A combination where you register each function from its own file, but you still have a root file for general app-level code. |

| Example | Description |
|---|---|
`dist/src/index.js` |
Register functions from a single root file. |
`dist/src/functions/*.js` |
Register each function from its own file. |
`dist/src/{index.js,functions/*.js}` |
A combination where you register each function from its own file, but you still have a root file for general app-level code. |

Tip

Make sure you define a `main`

field in your *package.json* file.

## Switch the order of arguments

The trigger input, instead of the invocation context, is now the first argument to your function handler. The invocation context, now the second argument, is simplified in v4 and isn't as required as the trigger input. You can leave it off if you aren't using it.

Tip

Switch the order of your arguments. For example, if you're using an HTTP trigger, switch `(context, request)`

to either `(request, context)`

or just `(request)`

if you aren't using the context.

## Define your function in code

You no longer have to create and maintain those separate *function.json* configuration files. You can now fully define your functions directly in your TypeScript or JavaScript files. In addition, many properties now have defaults so that you don't have to specify them every time.

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


Tip

Move the configuration from your *function.json* file to your code. The type of the trigger corresponds to a method on the `app`

object in the new model. For example, if you use an `httpTrigger`

type in *function.json*, call `app.http()`

in your code to register the function. If you use `timerTrigger`

, call `app.timer()`

.

## Review your usage of context

In v4, the `context`

object is simplified to reduce duplication and to make writing unit tests easier. For example, we streamlined the primary input and output so that they're accessed only as the argument and return value of your function handler.

You can't access the primary input and output on the `context`

object anymore, but you must still access *secondary* inputs and outputs on the `context`

object. For more information about secondary inputs and outputs, see the [Node.js developer guide](functions-reference-node#extra-inputs-and-outputs).

### Get the primary input as an argument

The primary input is also called the *trigger* and is the only required input or output. You must have one (and only one) trigger.

Version 4 supports only one way of getting the trigger input, as the first argument:

```
async function httpTrigger1(request, context) {
const onlyOption = request;
```


```
async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
const onlyOption = request;
```


Tip

Make sure you aren't using `context.req`

or `context.bindings`

to get the input.

### Set the primary output as your return value

Version 4 supports only one way of setting the primary output, through the return value:

```
return {
body: `Hello, ${name}!`
};
```


```
async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
// ...
return {
body: `Hello, ${name}!`
};
}
```


Tip

Make sure you always return the output in your function handler, instead of setting it with the `context`

object.

### Context logging

In v4, logging methods were moved to the root `context`

object as shown in the following example. For more information about logging, see the [Node.js developer guide](functions-reference-node#logging).

```
context.log('This is an info log');
context.error('This is an error');
context.warn('This is an error');
```


### Create a test context

Version 3 doesn't support creating an invocation context outside the Azure Functions runtime, so authoring unit tests can be difficult. Version 4 allows you to create an instance of the invocation context, although the information during tests isn't detailed unless you add it yourself.

```
const testInvocationContext = new InvocationContext({
functionName: 'testFunctionName',
invocationId: 'testInvocationId'
});
```


## Review your usage of HTTP types

The HTTP request and response types are now a subset of the [fetch standard](https://developer.mozilla.org/docs/Web/API/fetch). They're no longer unique to Azure Functions.

The types use the [ undici](https://undici.nodejs.org/) package in Node.js. This package follows the fetch standard and is

[currently being integrated](https://github.com/nodejs/undici/issues/1737)into Node.js core.

### HttpRequest

*Body*. You can access the body by using a method specific to the type that you want to receive:`const body = await request.text(); const body = await request.json(); const body = await request.formData(); const body = await request.arrayBuffer(); const body = await request.blob();`

*Header*:`const header = request.headers.get('content-type');`

*Query parameter*:`const name = request.query.get('name');`


### HttpResponse

*Status*:`return { status: 200 };`

*Body*:Use the

`body`

property to return most types like a`string`

or`Buffer`

:`return { body: "Hello, world!" };`

Use the

`jsonBody`

property for the easiest way to return a JSON response:`return { jsonBody: { hello: "world" } };`

*Header*. You can set the header in two ways, depending on whether you're using the`HttpResponse`

class or the`HttpResponseInit`

interface:`const response = new HttpResponse(); response.headers.set('content-type', 'application/json'); return response;`

`return { headers: { 'content-type': 'application/json' } };`


Tip

Update any logic by using the HTTP request or response types to match the new methods.

Tip

Update any logic by using the HTTP request or response types to match the new methods. You should get TypeScript build errors to help you identify if you're using old methods.

## Troubleshoot

See the [Node.js Troubleshoot guide](functions-node-troubleshoot).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/monitor-functions-reference -->

# Azure Functions monitoring data reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article contains all the monitoring reference information for this service.

See [Monitor Azure Functions](monitor-functions) for details on the data you can collect for Azure Functions and how to use it.

See [Monitor executions in Azure Functions](functions-monitoring) for details on using Application Insights to collect and analyze log data from individual functions in your function app.

## Metrics

This section lists all the automatically collected platform metrics for this service. These metrics are also part of the global list of [all platform metrics supported in Azure Monitor](/en-us/azure/azure-monitor/reference/supported-metrics/metrics-index#supported-metrics-per-resource-type).

For information on metric retention, see [Azure Monitor Metrics overview](/en-us/azure/azure-monitor/essentials/data-platform-metrics#retention-of-metrics).

Hosting plans that allow your apps to scale dynamically support extra Functions-specific metrics:

These metrics are used to estimate the costs associated with *on demand* and *always ready* meters used for billing in a [Flex Consumption plan](flex-consumption-plan):

| Metric | Description | Meter calculation |
|---|---|---|
On Demand Function Execution Count |
Total number of function executions in on demand instances. | `OnDemandFunctionExecutionCount` relates to the On Demand Total Executions meter. |
Always Ready Function Execution Count |
Total number of function executions in always ready instances. | `AlwaysReadyFunctionExecutionCount` relates to the Always Ready Total Executions meter. |
On Demand Function Execution Units |
Total MB-milliseconds from on demand instances while actively executing functions. | `OnDemandFunctionExecutionUnits / 1,024,000` is the On Demand Execution Time meter, in GB-seconds. |
Always Ready Function Execution Units |
Total MB-milliseconds from always ready instances while actively executing functions. | `AlwaysReadyFunctionExecutionUnits / 1,024,000` is the Always Ready Execution Time meter, in GB-seconds. |
Always Ready Units |
The total MB-milliseconds of always ready instances assigned to the app, whether or not functions are actively executing. | `AlwaysReadyUnits / 1,024,000` is the Always Ready Baseline meter, in GB-seconds. |

In this table, all execution units are calculated by multiplying the fixed instance memory size, such as 512 MB or 2,048 MB, by total execution times, in milliseconds.

These metrics are used to monitor the performance and scaling behavior of your function app in a Flex Consumption plan:

| Metric | Description |
|---|---|
Automatic Scaling Instance Count |
The number of instances on which this app is running. Note that this is emitted every 30 seconds, and given Flex Consumption scales out and in fast, the number will be an aggregate of all new instances the app used in this time period. Make sure to change the aggregation to the minimum possible in the graph and the aggregation to "count". |
Memory working set |
The current amount of memory used by the app, in MB. Can be further filtered for each instance of the app. |
Average memory working set |
The average amount of memory used by the app, in megabytes (MB). Can be further filtered for each instance of the app. |
CPU Percentage |
The average percentage of CPU being used. Can be further filtered for each instance of the app. This is currently rolling out and might not be available for apps in all regions yet. |

These performance metrics help you understand resource utilization and scaling patterns in your Flex Consumption function app. The instance count metric is particularly useful for monitoring the dynamic scaling behavior, while memory and CPU metrics provide insights into resource consumption patterns.

### Supported metrics for Microsoft.Web/sites

The following table lists the metrics available for the Microsoft.Web/sites resource type. Most of these metrics apply to both function app and web apps, which both run on App Service.

Note

These metrics aren't available when your function app runs on Linux in a [Consumption plan](consumption-plan).

- All columns might not be present in every table.
- Some columns might be beyond the viewing area of the page. Select
**Expand table**to view all available columns.

**Table headings**

**Category**- The metrics group or classification.**Metric**- The metric display name as it appears in the Azure portal.**Name in REST API**- The metric name as referred to in the[REST API](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough).**Unit**- Unit of measure.**Aggregation**- The default[aggregation](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained)type. Valid values: Average (Avg), Minimum (Min), Maximum (Max), Total (Sum), Count.**Dimensions**-[Dimensions](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#dimensions-splitting-and-filtering)available for the metric.**Time Grains**-[Intervals](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#granularity)at which the metric is sampled. For example,`PT1M`

indicates that the metric is sampled every minute,`PT30M`

every 30 minutes,`PT1H`

every hour, and so on.**DS Export**- Whether the metric is exportable to Azure Monitor Logs via diagnostic settings. For information on exporting metrics, see[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings?tabs=portal).

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Always Ready Function Execution CountAlways Ready Function Execution Count. For Flex Consumption FunctionApps only. |
`AlwaysReadyFunctionExecutionCount` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Always Ready Function Execution UnitsAlways Ready Function Execution Units. For Flex Consumption FunctionApps only. |
`AlwaysReadyFunctionExecutionUnits` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Always Ready UnitsAlways Ready Units. For Flex Consumption FunctionApps only. |
`AlwaysReadyUnits` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
ConnectionsThe number of bound sockets existing in the sandbox (w3wp.exe and its child processes). A bound socket is created by calling bind()/connect() APIs and remains until said socket is closed with CloseHandle()/closesocket(). For WebApps and FunctionApps. |
`AppConnections` |
Count | Average, Count, Maximum, Minimum | `Instance` |
PT1M | Yes |
Average memory working setThe average amount of memory used by the app, in megabytes (MiB). For WebApps and FunctionApps. |
`AverageMemoryWorkingSet` |
Bytes | Average | `Instance` |
PT1M | Yes |
Average Response Time (deprecated)The average time taken for the app to serve requests, in seconds. For WebApps and FunctionApps. |
`AverageResponseTime` |
Seconds | Average | `Instance` |
PT1M | Yes |
Data InThe amount of incoming bandwidth consumed by the app, in MiB. For WebApps and FunctionApps. |
`BytesReceived` |
Bytes | Total (Sum) | `Instance` |
PT1M | Yes |
Data OutThe amount of outgoing bandwidth consumed by the app, in MiB. For WebApps and FunctionApps. |
`BytesSent` |
Bytes | Total (Sum) | `Instance` |
PT1M | Yes |
Percentage CPUThe average percentage of CPU being used. For Flex Consumption function apps only. |
`CpuPercentage` |
Percent | Average | `Instance` |
PT1M | Yes |
CPU TimeThe amount of CPU consumed by the app, in seconds. For more information about this metric. Please see
|
`CpuTime` |
Seconds | Count, Total (Sum), Minimum, Maximum | `Instance` |
PT1M | Yes |
Current AssembliesThe current number of Assemblies loaded across all AppDomains in this application. For WebApps and FunctionApps. |
`CurrentAssemblies` |
Count | Average | `Instance` |
PT1M | Yes |
File System UsagePercentage of filesystem quota consumed by the app. For WebApps and FunctionApps. |
`FileSystemUsage` |
Bytes | Average | <none> | PT6H, PT12H, P1D | Yes |
Function Execution CountFunction Execution Count. For FunctionApps only. |
`FunctionExecutionCount` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Function Execution UnitsFunction Execution Units. For FunctionApps only. |
`FunctionExecutionUnits` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Gen 0 Garbage CollectionsThe number of times the generation 0 objects are garbage collected since the start of the app process. Higher generation GCs include all lower generation GCs. For WebApps and FunctionApps. |
`Gen0Collections` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Gen 1 Garbage CollectionsThe number of times the generation 1 objects are garbage collected since the start of the app process. Higher generation GCs include all lower generation GCs. For WebApps and FunctionApps. |
`Gen1Collections` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Gen 2 Garbage CollectionsThe number of times the generation 2 objects are garbage collected since the start of the app process. For WebApps and FunctionApps. |
`Gen2Collections` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Handle CountThe total number of handles currently open by the app process. For WebApps and FunctionApps. |
`Handles` |
Count | Average | `Instance` |
PT1M | Yes |
Health check statusHealth check status. For WebApps and FunctionApps. |
`HealthCheckStatus` |
Count | Average | `Instance` |
PT5M, PT1H, P1D | Yes |
Http 101The count of requests resulting in an HTTP status code 101. For WebApps and FunctionApps. |
`Http101` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http 2xxThe count of requests resulting in an HTTP status code >= 200 but < 300. For WebApps and FunctionApps. |
`Http2xx` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http 3xxThe count of requests resulting in an HTTP status code >= 300 but < 400. For WebApps and FunctionApps. |
`Http3xx` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http 401The count of requests resulting in HTTP 401 status code. For WebApps and FunctionApps. |
`Http401` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http 403The count of requests resulting in HTTP 403 status code. For WebApps and FunctionApps. |
`Http403` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http 404The count of requests resulting in HTTP 404 status code. For WebApps and FunctionApps. |
`Http404` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http 406The count of requests resulting in HTTP 406 status code. For WebApps and FunctionApps. |
`Http406` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http 4xxThe count of requests resulting in an HTTP status code >= 400 but < 500. For WebApps and FunctionApps. |
`Http4xx` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http Server ErrorsThe count of requests resulting in an HTTP status code >= 500 but < 600. For WebApps and FunctionApps. |
`Http5xx` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Response TimeThe time taken for the app to serve requests, in seconds. For WebApps and FunctionApps. |
`HttpResponseTime` |
Seconds | Average | `Instance` |
PT1M | Yes |
Automatic Scaling Instance CountThe number of instances on which this app is running. |
`InstanceCount` |
Count | Average | <none> | PT1M | Yes |
IO Other Bytes Per SecondThe rate at which the app process is issuing bytes to I/O operations that don't involve data, such as control operations. For WebApps and FunctionApps. |
`IoOtherBytesPerSecond` |
BytesPerSecond | Total (Sum) | `Instance` |
PT1M | Yes |
IO Other Operations Per SecondThe rate at which the app process is issuing I/O operations that aren't read or write operations. For WebApps and FunctionApps. |
`IoOtherOperationsPerSecond` |
BytesPerSecond | Total (Sum) | `Instance` |
PT1M | Yes |
IO Read Bytes Per SecondThe rate at which the app process is reading bytes from I/O operations. For WebApps and FunctionApps. |
`IoReadBytesPerSecond` |
BytesPerSecond | Total (Sum) | `Instance` |
PT1M | Yes |
IO Read Operations Per SecondThe rate at which the app process is issuing read I/O operations. For WebApps and FunctionApps. |
`IoReadOperationsPerSecond` |
BytesPerSecond | Total (Sum) | `Instance` |
PT1M | Yes |
IO Write Bytes Per SecondThe rate at which the app process is writing bytes to I/O operations. For WebApps and FunctionApps. |
`IoWriteBytesPerSecond` |
BytesPerSecond | Total (Sum) | `Instance` |
PT1M | Yes |
IO Write Operations Per SecondThe rate at which the app process is issuing write I/O operations. For WebApps and FunctionApps. |
`IoWriteOperationsPerSecond` |
BytesPerSecond | Total (Sum) | `Instance` |
PT1M | Yes |
Memory working setThe current amount of memory used by the app, in MiB. For WebApps and FunctionApps. |
`MemoryWorkingSet` |
Bytes | Average | `Instance` |
PT1M | Yes |
On Demand Function Execution CountOn Demand Function Execution Count. For Flex Consumption FunctionApps only. |
`OnDemandFunctionExecutionCount` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
On Demand Function Execution UnitsOn Demand Function Execution Units. For Flex Consumption FunctionApps only. |
`OnDemandFunctionExecutionUnits` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Private BytesPrivate Bytes is the current size, in bytes, of memory that the app process has allocated that can't be shared with other processes. For WebApps and FunctionApps. |
`PrivateBytes` |
Bytes | Average | `Instance` |
PT1M | Yes |
RequestsThe total number of requests regardless of their resulting HTTP status code. For WebApps and FunctionApps. |
`Requests` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Requests In Application QueueThe number of requests in the application request queue. For WebApps and FunctionApps. |
`RequestsInApplicationQueue` |
Count | Average | `Instance` |
PT1M | Yes |
Thread CountThe number of threads currently active in the app process. For WebApps and FunctionApps. |
`Threads` |
Count | Average | `Instance` |
PT1M | Yes |
Total App DomainsThe current number of AppDomains loaded in this application. For WebApps and FunctionApps. |
`TotalAppDomains` |
Count | Average | `Instance` |
PT1M | Yes |
Total App Domains UnloadedThe total number of AppDomains unloaded since the start of the application. For WebApps and FunctionApps. |
`TotalAppDomainsUnloaded` |
Count | Average | `Instance` |
PT1M | Yes |
Workflow Action Completed CountWorkflow Action Completed Count. For LogicApps only. |
`WorkflowActionsCompleted` |
Count | Total (Sum) | `workflowName` , `status` |
PT1M | Yes |
Workflow Actions Failure RateWorkflow Actions Failure Rate. For LogicApps only. |
`WorkflowActionsFailureRate` |
Percent | Total (Sum) | `workflowName` |
PT1M | Yes |
Logic App Job Pull Rate Per SecondLogic Job Pull Rate per second. For LogicApps only. |
`WorkflowAppJobPullRate` |
CountPerSecond | Total (Sum) | `accountName` |
PT1M | Yes |
Workflow Job Execution DelayWorkflow Job Execution Delay. For LogicApps only. |
`WorkflowJobExecutionDelay` |
Seconds | Average | `workflowName` |
PT1M | Yes |
Workflow Job Execution DurationWorkflow Job Execution Duration. For LogicApps only. |
`WorkflowJobExecutionDuration` |
Seconds | Average | `workflowName` |
PT1M | Yes |
Workflow Runs Completed CountWorkflow Runs Completed Count. For LogicApps only. |
`WorkflowRunsCompleted` |
Count | Total (Sum) | `workflowName` , `status` |
PT1M | Yes |
Workflow Runs dispatched CountWorkflow Runs Dispatched Count. For LogicApps only. |
`WorkflowRunsDispatched` |
Count | Total (Sum) | `workflowName` |
PT1M | Yes |
Workflow Runs Failure RateWorkflow Runs Failure Rate. For LogicApps only. |
`WorkflowRunsFailureRate` |
Percent | Total (Sum) | `workflowName` |
PT1M | Yes |
Workflow Runs Started CountWorkflow Runs Started Count. For LogicApps only. |
`WorkflowRunsStarted` |
Count | Total (Sum) | `workflowName` |
PT1M | Yes |
Workflow Triggers Completed CountWorkflow Triggers Completed Count. For LogicApps only. |
`WorkflowTriggersCompleted` |
Count | Total (Sum) | `workflowName` , `status` |
PT1M | Yes |
Workflow Triggers Failure RateWorkflow Triggers Failure Rate. For LogicApps only. |
`WorkflowTriggersFailureRate` |
Percent | Total (Sum) | `workflowName` |
PT1M | Yes |

## Metric dimensions

For information about what metric dimensions are, see [Multi-dimensional metrics](/en-us/azure/azure-monitor/platform/data-platform-metrics#multi-dimensional-metrics).

This service doesn't have any metrics that contain dimensions.

## Resource logs

This section lists the types of resource logs you can collect for this service. The section pulls from the list of [all resource logs category types supported in Azure Monitor](/en-us/azure/azure-monitor/platform/resource-logs-schema).

### Supported resource logs for Microsoft.Web/sites

| Category | Category display name | Log table |
|
|---|

[Supports ingestion-time transformation](/en-us/azure/azure-monitor/essentials/data-collection-transformations)

`AppServiceAntivirusScanAuditLogs`

[AppServiceAntivirusScanAuditLogs](/en-us/azure/azure-monitor/reference/tables/appserviceantivirusscanauditlogs)Report on any discovered virus or infected files that have been uploaded to their site.

`AppServiceAppLogs`

[AppServiceAppLogs](/en-us/azure/azure-monitor/reference/tables/appserviceapplogs)Logs generated through your application.

[Queries](/en-us/azure/azure-monitor/reference/queries/appserviceapplogs)`AppServiceAuditLogs`

[AppServiceAuditLogs](/en-us/azure/azure-monitor/reference/tables/appserviceauditlogs)Logs generated when publishing users successfully log on via one of the App Service publishing protocols.

[Queries](/en-us/azure/azure-monitor/reference/queries/appserviceauditlogs)`AppServiceAuthenticationLogs`

[AppServiceAuthenticationLogs](/en-us/azure/azure-monitor/reference/tables/appserviceauthenticationlogs)Logs generated through App Service Authentication for your application.

[Queries](/en-us/azure/azure-monitor/reference/queries/appserviceauthenticationlogs)`AppServiceConsoleLogs`

[AppServiceConsoleLogs](/en-us/azure/azure-monitor/reference/tables/appserviceconsolelogs)Console logs generated from application or container.

[Queries](/en-us/azure/azure-monitor/reference/queries/appserviceconsolelogs)`AppServiceFileAuditLogs`

[AppServiceFileAuditLogs](/en-us/azure/azure-monitor/reference/tables/appservicefileauditlogs)Logs generated when app service content is modified.

[Queries](/en-us/azure/azure-monitor/reference/queries/appservicefileauditlogs)`AppServiceHTTPLogs`

[AppServiceHTTPLogs](/en-us/azure/azure-monitor/reference/tables/appservicehttplogs)Incoming HTTP requests on App Service. Use these logs to monitor application health, performance and usage patterns.

[Queries](/en-us/azure/azure-monitor/reference/queries/appservicehttplogs)`AppServiceIPSecAuditLogs`

[AppServiceIPSecAuditLogs](/en-us/azure/azure-monitor/reference/tables/appserviceipsecauditlogs)Logs generated through your application and pushed to Azure Monitoring.

`AppServicePlatformLogs`

[AppServicePlatformLogs](/en-us/azure/azure-monitor/reference/tables/appserviceplatformlogs)Logs generated through AppService platform for your application.

`FunctionAppLogs`

[FunctionAppLogs](/en-us/azure/azure-monitor/reference/tables/functionapplogs)Log generated by Function Apps. It includes logs emitted by the Functions host and logs emitted by customer code. Use these logs to monitor application health, performance, and behavior.

[Queries](/en-us/azure/azure-monitor/reference/queries/functionapplogs)`WorkflowRuntime`

[LogicAppWorkflowRuntime](/en-us/azure/azure-monitor/reference/tables/logicappworkflowruntime)Logs generated during Logic Apps workflow runtime.

[Queries](/en-us/azure/azure-monitor/reference/queries/logicappworkflowruntime)The log specific to Azure Functions is **FunctionAppLogs**.

For more information, see the [App Service monitoring data reference](/en-us/azure/app-service/monitor-app-service-reference#metrics).

## Azure Monitor Logs tables

This section lists the Azure Monitor Logs tables relevant to this service, which are available for query by Log Analytics using Kusto queries. The tables contain resource log data and possibly more depending on what is collected and routed to them.

### App Services

Microsoft.Web/sites

## Activity log

The linked table lists the operations that can be recorded in the activity log for this service. These operations are a subset of [all the possible resource provider operations in the activity log](/en-us/azure/role-based-access-control/resource-provider-operations).

For more information on the schema of activity log entries, see [Activity Log schema](/en-us/azure/azure-monitor/essentials/activity-log-schema).

The following table lists operations related to Azure Functions that might be created in the activity log.

| Operation | Description |
|---|---|
| Microsoft.web/sites/functions/listkeys/action | Return the
|

[host keys for the function app](function-keys-how-to).[Sync triggers](functions-deployment-technologies#trigger-syncing)operation.You may also find logged operations that relate to the underlying App Service behaviors. For a more complete list, see [Microsoft.Web resource provider operations](/en-us/azure/role-based-access-control/resource-provider-operations#microsoftweb).

## Related content

- See
[Monitor Azure Functions](monitor-functions)for a description of monitoring Azure Functions. - See
[Monitor Azure resources with Azure Monitor](/en-us/azure/azure-monitor/essentials/monitor-azure-resource)for details on monitoring Azure resources.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-expressions-patterns -->

# Azure Functions binding expressions and patterns

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

One of the most powerful features of [triggers and bindings](functions-triggers-bindings) in Azure Functions is *binding expressions*. In the `function.json`

file and in function parameters and code, you can use expressions that resolve to values from various sources.

Most expressions are wrapped in curly braces. For example, in a queue trigger function, `{queueTrigger}`

resolves to the queue message text. If the `path`

property for a blob output binding is `container/{queueTrigger}`

and a queue message `HelloWorld`

triggers the function, a blob named `HelloWorld`

is created.

App settings

It's a best practice to manage secrets and connection strings by using app settings rather than configuration files. This practice limits access to these secrets and makes it safe to store files such as `function.json`

in public source-control repositories.

App settings are also useful whenever you want to change a configuration based on the environment. For example, in a test environment, you might want to monitor a different container for queue storage or blob storage.

Binding expressions for app settings are identified differently from other binding expressions: they're wrapped in percent signs rather than curly braces. For example, if the path for a blob output binding is `%Environment%/newblob.txt`

and the `Environment`

app setting value is `Development`

, a blob is created in the `Development`

container.

When a function is running locally, values for app settings come from the `local.settings.json`

file.

Note

The `connection`

property of triggers and bindings is a special case and automatically resolves values as app settings, without percent signs.

The following example is an Azure Queue Storage trigger that uses an app setting `%input_queue_name%`

to define the queue to trigger on:

```
{
"bindings": [
{
"name": "order",
"type": "queueTrigger",
"direction": "in",
"queueName": "%input_queue_name%",
"connection": "MY_STORAGE_ACCT_APP_SETTING"
}
]
}
```


You can use the same approach in class libraries:

```
[FunctionName("QueueTrigger")]
public static void Run(
[QueueTrigger("%input_queue_name%")]string myQueueItem,
ILogger log)
{
log.LogInformation($"C# Queue trigger function processed: {myQueueItem}");
}
```


## Trigger file name

The `path`

value for a blob trigger can be a pattern that lets you refer to the name of the triggering blob in other bindings and function code. The pattern can also include filtering criteria that specify which blobs can trigger a function invocation.

For example, in the following binding for a blob trigger, the `path`

pattern is `sample-images/{filename}`

. This pattern creates a binding expression named `filename`

.

```
{
"bindings": [
{
"name": "image",
"type": "blobTrigger",
"path": "sample-images/{filename}",
"direction": "in",
"connection": "MyStorageConnection"
},
...
```


You can then use the expression `filename`

in an output binding to specify the name of the blob that you're creating:

```
...
{
"name": "imageSmall",
"type": "blob",
"path": "sample-images-sm/{filename}",
"direction": "out",
"connection": "MyStorageConnection"
}
],
}
```


Function code has access to this same value by using `filename`

as a parameter name:

```
// C# example of binding to {filename}
public static void Run(Stream image, string filename, Stream imageSmall, ILogger log)
{
log.LogInformation($"Blob trigger processing: {filename}");
// ...
}
```


The same ability to use binding expressions and patterns applies to attributes in class libraries. In the following example, the attribute constructor parameters are the same `path`

values as the preceding `function.json`

examples:

```
[FunctionName("ResizeImage")]
public static void Run(
[BlobTrigger("sample-images/{filename}")] Stream image,
[Blob("sample-images-sm/{filename}", FileAccess.Write)] Stream imageSmall,
string filename,
ILogger log)
{
log.LogInformation($"Blob trigger processing: {filename}");
// ...
}
```


You can also create expressions for parts of the file name. In the following example, the function is triggered only on file names that match a pattern: `anyname-anyfile.csv`

.

```
{
"name": "myBlob",
"type": "blobTrigger",
"direction": "in",
"path": "testContainerName/{date}-{filetype}.csv",
"connection": "OrderStorageConnection"
}
```


For more information on how to use expressions and patterns in the blob path string, see the [reference for Azure Blob Storage bindings](functions-bindings-storage-blob).

## Trigger metadata

In addition to the data payload that a trigger provides (such as the content of the queue message that triggered a function), many triggers provide other metadata values. You can use these values as input parameters in C# and F# or as properties on the `context.bindings`

object in JavaScript.

For example, an Azure Queue Storage trigger supports the following properties:

`QueueTrigger`

(triggering message content if the string is valid)`DequeueCount`

`ExpirationTime`

`Id`

`InsertionTime`

`NextVisibleTime`

`PopReceipt`


These metadata values are accessible in the `function.json`

file properties. For example, suppose you use a queue trigger and the queue message contains the name of a blob that you want to read. In the `function.json`

file, you can use the `queueTrigger`

metadata property in the blob `path`

property, as shown in the following example:

```
{
"bindings": [
{
"name": "myQueueItem",
"type": "queueTrigger",
"queueName": "myqueue-items",
"connection": "MyStorageConnection",
},
{
"name": "myInputBlob",
"type": "blob",
"path": "samples-workitems/{queueTrigger}",
"direction": "in",
"connection": "MyStorageConnection"
}
]
}
```


You can find details of metadata properties for each trigger in the corresponding reference article. For an example, see the [metadata for an Azure Queue Storage trigger](functions-bindings-storage-queue-trigger#message-metadata). Documentation is also available on the **Integrate** tab of the portal, in the **Documentation** section below the binding configuration area.

## JSON payloads

In some scenarios, you can refer to the trigger payload's properties in the configuration for other bindings in the same function and in function code. This approach requires that the trigger payload is JSON and is smaller than a threshold specific to each trigger. Typically, the payload size needs to be less than 100 MB, but you should check the reference content for each trigger.

Using trigger payload properties might affect the performance of your application. It also forces the trigger parameter type to be a simple type (like a string) or a custom object type that represents JSON data. You can't use it with streams, clients, or other SDK types.

The following example shows the `function.json`

file for a webhook function that receives a blob name in JSON: `{"BlobName":"HelloWorld.txt"}`

. A blob input binding reads the blob, and the HTTP output binding returns the blob contents in the HTTP response. Notice that the blob input binding gets the blob name by referring directly to the `BlobName`

property (`"path": "strings/{BlobName}"`

).

```
{
"bindings": [
{
"name": "info",
"type": "httpTrigger",
"direction": "in",
"webHookType": "genericJson"
},
{
"name": "blobContents",
"type": "blob",
"direction": "in",
"path": "strings/{BlobName}",
"connection": "AzureWebJobsStorage"
},
{
"name": "res",
"type": "http",
"direction": "out"
}
]
}
```


For this approach to work in C# and F#, you need a class that defines the fields to be deserialized, as in the following example:

```
using System.Net;
using Microsoft.Extensions.Logging;
public class BlobInfo
{
public string BlobName { get; set; }
}
public static HttpResponseMessage Run(HttpRequestMessage req, BlobInfo info, string blobContents, ILogger log)
{
if (blobContents == null) {
return req.CreateResponse(HttpStatusCode.NotFound);
}
log.LogInformation($"Processing: {info.BlobName}");
return req.CreateResponse(HttpStatusCode.OK, new {
data = $"{blobContents}"
});
}
```


In JavaScript, JSON deserialization is automatically performed:

```
module.exports = async function (context, info) {
if ('BlobName' in info) {
context.res = {
body: { 'data': context.bindings.blobContents }
}
}
else {
context.res = {
status: 404
};
}
}
```


### Dot notation

If some of the properties in your JSON payload are objects with properties, you can refer to them directly by using dot (`.`

) notation. This notation doesn't work for [Azure Cosmos DB](functions-bindings-cosmosdb-v2) or [Azure Table Storage](functions-bindings-storage-table-output) bindings.

For example, suppose your JSON looks like this example:

```
{
"BlobName": {
"FileName":"HelloWorld",
"Extension":"txt"
}
}
```


You can refer directly to `FileName`

as `BlobName.FileName`

. With this JSON format, here's what the `path`

property in the preceding example would look like:

```
"path": "strings/{BlobName.FileName}.{BlobName.Extension}",
```


In C#, you would need two classes:

```
public class BlobInfo
{
public BlobName BlobName { get; set; }
}
public class BlobName
{
public string FileName { get; set; }
public string Extension { get; set; }
}
```


## New GUIDs

The `{rand-guid}`

binding expression creates a GUID. The following blob path in a `function.json`

file creates a blob with a name like *50710cb5-84b9-4d87-9d83-a03d6976a682.txt*:

```
{
"type": "blob",
"name": "blobOutput",
"direction": "out",
"path": "my-output-container/{rand-guid}.txt"
}
```


## Current date and time

The binding expression `DateTime`

resolves to `DateTime.UtcNow`

. The following blob path in a `function.json`

file creates a blob with a name like *2018-02-16T17-59-55Z.txt*:

```
{
"type": "blob",
"name": "blobOutput",
"direction": "out",
"path": "my-output-container/{DateTime}.txt"
}
```


## Binding at runtime

In C# and other .NET languages, you can use an imperative binding pattern, as opposed to the declarative bindings in `function.json`

and attributes. Imperative binding is useful when binding parameters need to be computed at runtime rather than design time. To learn more, see the [C# developer reference](functions-dotnet-class-library#binding-at-runtime) or the [C# script developer reference](functions-reference-csharp#binding-at-runtime).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/scenario-scheduled-tasks -->

# Quickstart: Run scheduled tasks using Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you use the Azure Developer CLI (`azd`

) to create a Timer trigger function to run a scheduled task in Azure Functions. After verifying the code locally, you deploy it to a new serverless function app you create running in a Flex Consumption plan in Azure Functions.

The project source uses `azd`

to create the function app and related resources and to deploy your code to Azure. This deployment follows current best practices for secure and scalable Azure Functions deployments.

By default, the Flex Consumption plan follows a *pay-for-what-you-use* billing model, which means you can complete this article and only incur a small cost of a few USD cents or less in your Azure account.

Important

While [running scheduled tasks](functions-bindings-timer) is supported for all languages, this quickstart scenario currently only has examples for C#, Python, and TypeScript. To complete this quickstart, select one of these supported languages at the top of the article.

## Prerequisites

[Node.js 22](https://nodejs.org/)or above

[Python 3.11](https://www.python.org/)or above

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Initialize the project

Use the `azd init`

command to create a local Azure Functions code project from a template.

In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-dotnet-azd-timer -e scheduled-dotnet`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-timer)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name is also used in the name of the resource group you create in Azure.Run this command to navigate to the app folder:

`cd src`

Create a file named

*local.settings.json*in the`src`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "dotnet-isolated", "TIMER_SCHEDULE": "*/30 * * * * *" } }`

This file is required when running locally.


In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-typescript-azd-timer -e scheduled-ts`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-timer)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name is also used in the name of the resource group you create in Azure.Create a file named

*local.settings.json*in the`src`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "node", "TIMER_SCHEDULE": "*/30 * * * * *" } }`

This file is required when running locally.


In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-python-azd-timer -e scheduled-py`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-python-azd-timer)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name is also used in the name of the resource group you create in Azure.Create a file named

*local.settings.json*in the`src`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "python", "TIMER_SCHEDULE": "*/30 * * * * *" } }`

This file is required when running locally.


## Create and activate a virtual environment

In the root folder, run these commands to create and activate a virtual environment named `.venv`

:

```
python3 -m venv .venv
source .venv/bin/activate
```


If Python doesn't install the venv package on your Linux distribution, run the following command:

```
sudo apt-get install python3-venv
```


## Run in your local environment

Run this command from your app folder in a terminal or command prompt:

`func start`


Run this command from your app folder in a terminal or command prompt:

`npm install npm start`


When the Functions host starts in your local project folder, it writes information about your Timer triggered function to the terminal output. You should see your Timer triggered function execute based on the schedule defined in your code.

The default schedule is

`*/30 * * * * *`

, which runs every 30 seconds.When you're done, press Ctrl+C in the terminal window to stop the

`func.exe`

host process.

- Run
`deactivate`

to shut down the virtual environment.

## Review the code (optional)

You can review the code that defines the Timer trigger function:

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.Timer;
using Microsoft.Extensions.Logging;
namespace Company.Function
{
public class timerFunction
{
private readonly ILogger _logger;
public timerFunction(ILoggerFactory loggerFactory)
{
_logger = loggerFactory.CreateLogger<timerFunction>();
}
[Function("timerFunction")]
public void Run(
[TimerTrigger("%TIMER_SCHEDULE%", RunOnStartup = true)] TimerInfo myTimer,
FunctionContext context
)
{
_logger.LogInformation($"C# Timer trigger function executed at: {DateTime.Now}");
if (myTimer.IsPastDue)
{
_logger.LogWarning("The timer is running late!");
}
}
}
}
```


You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-timer).

```
import { app, InvocationContext, Timer } from '@azure/functions';
export async function timerFunction(myTimer: Timer, context: InvocationContext): Promise<void> {
context.log(`TypeScript Timer trigger function executed at: ${new Date().toISOString()}`);
if (myTimer.isPastDue) {
context.warn("The timer is running late!");
}
}
app.timer('timerFunction', {
schedule: '%TIMER_SCHEDULE%',
runOnStartup: true,
handler: timerFunction
});
```


You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-timer).

```
import datetime
import logging
import azure.functions as func
# Create the function app instance
app = func.FunctionApp()
@app.timer_trigger(schedule="%TIMER_SCHEDULE%",
arg_name="mytimer",
run_on_startup=True,
use_monitor=False)
def timer_function(mytimer: func.TimerRequest) -> None:
utc_timestamp = datetime.datetime.now(datetime.timezone.utc).isoformat()
logging.info(f'Python timer trigger function executed at: {utc_timestamp}')
if mytimer.past_due:
logging.warning('The timer is running late!')
```


You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-python-azd-timer).

After you verify your function locally, it's time to publish it to Azure.

## Deploy to Azure

This project is configured to use the `azd up`

command to deploy your code to a new function app in a Flex Consumption plan in Azure.

Tip

This project includes a set of Bicep files that `azd`

uses to create a secure deployment to a Flex consumption plan that follows best practices.

Run this command to have

`azd`

create the required Azure resources in Azure and deploy your code project to the new function app:`azd up`

The root folder contains the

`azure.yaml`

definition file required by`azd`

.If you're not already signed in, you're asked to authenticate with your Azure account.

When prompted, provide these required deployment parameters:

Parameter Description *Azure subscription*Subscription in which your resources are created. *Azure location*Azure region in which to create the resource group that contains the new Azure resources. Only regions that currently support the Flex Consumption plan are shown. The

`azd up`

command uses your response to these prompts with the Bicep configuration files to complete these deployment tasks:Create and configure these required Azure resources (equivalent to

`azd provision`

):- Flex Consumption plan and function app
- Azure Storage (required) and Application Insights (recommended)
- Access policies and roles for your account
- Service-to-service connections using managed identities (instead of stored connection strings)
- Virtual network to securely run both the function app and the other Azure resources

Package and deploy your code to the deployment container (equivalent to

`azd deploy`

). The app is then started and runs in the deployed package.

After the command completes successfully, you see links to the resources you created.


## Verify deployment

After deployment completes, your Timer trigger function automatically starts running in Azure based on its schedule.

In the

[Azure portal](https://portal.azure.com), go to your new function app.Select

**Log stream**from the left menu to monitor your function executions in real-time.You should see log entries that show your Timer trigger function executing according to its schedule.


## Redeploy your code

Run the `azd up`

command as many times as you need to both provision your Azure resources and deploy code updates to your function app.

Note

Deployed code files are always overwritten by the latest deployment package.

Your initial responses to `azd`

prompts and any environment variables generated by `azd`

are stored locally in your named environment. Use the `azd env get-values`

command to review all of the variables in your environment that were used when creating Azure resources.

## Clean up resources

When you're done working with your function app and related resources, use this command to delete the function app and its related resources from Azure and avoid incurring any further costs:

```
azd down --no-prompt
```


Note

The `--no-prompt`

option instructs `azd`

to delete your resource group without a confirmation from you.

This command doesn't affect your local code project.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-grid-output -->

# Azure Event Grid output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the Event Grid output binding to write events to a custom topic. You must have a valid [access key for the custom topic](../event-grid/security-authenticate-publishing-clients). The Event Grid output binding doesn't support shared access signature (SAS) tokens.

For information on setup and configuration details, see [How to work with Event Grid triggers and bindings in Azure Functions](event-grid-how-tos).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

Important

The Event Grid output binding is only available for Functions 2.x and higher.

## Example

The type of the output parameter used with an Event Grid output binding depends on the Functions runtime version, the binding extension version, and the modality of the C# function. The C# function can be created using one of the following C# modes:

[In-process class library](functions-dotnet-class-library): compiled C# function that runs in the same process as the Functions runtime.[Isolated worker process class library](dotnet-isolated-process-guide): compiled C# function that runs in a worker process isolated from the runtime.

The following example shows how the custom type is used in both the trigger and an Event Grid output binding:

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.Logging;
namespace SampleApp
{
public static class EventGridFunction
{
[Function(nameof(EventGridFunction))]
[EventGridOutput(TopicEndpointUri = "MyEventGridTopicUriSetting", TopicKeySetting = "MyEventGridTopicKeySetting")]
public static MyEventType Run([EventGridTrigger] MyEventType input, FunctionContext context)
{
var logger = context.GetLogger(nameof(EventGridFunction));
logger.LogInformation(input.Data?.ToString());
var outputEvent = new MyEventType()
{
Id = "unique-id",
Subject = "abc-subject",
Data = new Dictionary<string, object>
{
{ "myKey", "myValue" }
}
};
return outputEvent;
}
}
public class MyEventType
{
public string? Id { get; set; }
public string? Topic { get; set; }
public string? Subject { get; set; }
public string? EventType { get; set; }
public DateTime EventTime { get; set; }
public IDictionary<string, object>? Data { get; set; }
}
}
```


The following example shows a Java function that writes a message to an Event Grid custom topic. The function uses the binding's `setValue`

method to output a string.

```
public class Function {
@FunctionName("EventGridTriggerTest")
public void run(@EventGridTrigger(name = "event") String content,
@EventGridOutput(name = "outputEvent", topicEndpointUri = "MyEventGridTopicUriSetting", topicKeySetting = "MyEventGridTopicKeySetting") OutputBinding<String> outputEvent,
final ExecutionContext context) {
context.getLogger().info("Java EventGrid trigger processed a request." + content);
final String eventGridOutputDocument = "{\"id\": \"1807\", \"eventType\": \"recordInserted\", \"subject\": \"myapp/cars/java\", \"eventTime\":\"2017-08-10T21:03:07+00:00\", \"data\": {\"make\": \"Ducati\",\"model\": \"Monster\"}, \"dataVersion\": \"1.0\"}";
outputEvent.setValue(eventGridOutputDocument);
}
}
```


You can also use a POJO class to send Event Grid messages.

```
public class Function {
@FunctionName("EventGridTriggerTest")
public void run(@EventGridTrigger(name = "event") String content,
@EventGridOutput(name = "outputEvent", topicEndpointUri = "MyEventGridTopicUriSetting", topicKeySetting = "MyEventGridTopicKeySetting") OutputBinding<EventGridEvent> outputEvent,
final ExecutionContext context) {
context.getLogger().info("Java EventGrid trigger processed a request." + content);
final EventGridEvent eventGridOutputDocument = new EventGridEvent();
eventGridOutputDocument.setId("1807");
eventGridOutputDocument.setEventType("recordInserted");
eventGridOutputDocument.setEventTime("2017-08-10T21:03:07+00:00");
eventGridOutputDocument.setDataVersion("1.0");
eventGridOutputDocument.setSubject("myapp/cars/java");
eventGridOutputDocument.setData("{\"make\": \"Ducati\",\"model\":\"monster\"");
outputEvent.setValue(eventGridOutputDocument);
}
}
class EventGridEvent {
private String id;
private String eventType;
private String subject;
private String eventTime;
private String dataVersion;
private String data;
public String getId() {
return id;
}
public String getData() {
return data;
}
public void setData(String data) {
this.data = data;
}
public String getDataVersion() {
return dataVersion;
}
public void setDataVersion(String dataVersion) {
this.dataVersion = dataVersion;
}
public String getEventTime() {
return eventTime;
}
public void setEventTime(String eventTime) {
this.eventTime = eventTime;
}
public String getSubject() {
return subject;
}
public void setSubject(String subject) {
this.subject = subject;
}
public String getEventType() {
return eventType;
}
public void setEventType(String eventType) {
this.eventType = eventType;
}
public void setId(String id) {
this.id = id;
}
}
```


The following example shows a timer triggered [TypeScript function](functions-reference-node?tabs=typescript) that outputs a single event:

```
import { app, EventGridPartialEvent, InvocationContext, output, Timer } from '@azure/functions';
export async function timerTrigger1(myTimer: Timer, context: InvocationContext): Promise<EventGridPartialEvent> {
const timeStamp = new Date().toISOString();
return {
id: 'message-id',
subject: 'subject-name',
dataVersion: '1.0',
eventType: 'event-type',
data: {
name: 'John Henry',
},
eventTime: timeStamp,
};
}
app.timer('timerTrigger1', {
schedule: '0 */5 * * * *',
return: output.eventGrid({
topicEndpointUri: 'MyEventGridTopicUriSetting',
topicKeySetting: 'MyEventGridTopicKeySetting',
}),
handler: timerTrigger1,
});
```


To output multiple events, return an array instead of a single object. For example:

```
const timeStamp = new Date().toISOString();
return [
{
id: 'message-id',
subject: 'subject-name',
dataVersion: '1.0',
eventType: 'event-type',
data: {
name: 'John Henry',
},
eventTime: timeStamp,
},
{
id: 'message-id-2',
subject: 'subject-name',
dataVersion: '1.0',
eventType: 'event-type',
data: {
name: 'John Doe',
},
eventTime: timeStamp,
},
];
```


The following example shows a timer triggered [JavaScript function](functions-reference-node) that outputs a single event:

```
const { app, output } = require('@azure/functions');
const eventGridOutput = output.eventGrid({
topicEndpointUri: 'MyEventGridTopicUriSetting',
topicKeySetting: 'MyEventGridTopicKeySetting',
});
app.timer('timerTrigger1', {
schedule: '0 */5 * * * *',
return: eventGridOutput,
handler: (myTimer, context) => {
const timeStamp = new Date().toISOString();
return {
id: 'message-id',
subject: 'subject-name',
dataVersion: '1.0',
eventType: 'event-type',
data: {
name: 'John Henry',
},
eventTime: timeStamp,
};
},
});
```


To output multiple events, return an array instead of a single object. For example:

```
const timeStamp = new Date().toISOString();
return [
{
id: 'message-id',
subject: 'subject-name',
dataVersion: '1.0',
eventType: 'event-type',
data: {
name: 'John Henry',
},
eventTime: timeStamp,
},
{
id: 'message-id-2',
subject: 'subject-name',
dataVersion: '1.0',
eventType: 'event-type',
data: {
name: 'John Doe',
},
eventTime: timeStamp,
},
];
```


The following example demonstrates how to configure a function to output an Event Grid event message. The section where `type`

is set to `eventGrid`

configures the values needed to establish an Event Grid output binding.

```
{
"bindings": [
{
"type": "eventGrid",
"name": "outputEvent",
"topicEndpointUri": "MyEventGridTopicUriSetting",
"topicKeySetting": "MyEventGridTopicKeySetting",
"direction": "out"
},
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
}
]
}
```


In your function, use the `Push-OutputBinding`

to send an event to a custom topic through the Event Grid output binding.

```
using namespace System.Net
# Input bindings are passed in via param block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell HTTP trigger function processed a request."
# Interact with query parameters or the body of the request.
$message = $Request.Query.Message
Push-OutputBinding -Name outputEvent -Value @{
id = "1"
eventType = "testEvent"
subject = "testapp/testPublish"
eventTime = "2020-08-27T21:03:07+00:00"
data = @{
Message = $message
}
dataVersion = "1.0"
}
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = 200
Body = "OK"
})
```


The following example shows a trigger binding and a Python function that uses the binding. It then sends in an event to the custom topic, as specified by the `topicEndpointUri`

. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

Here's the function in the function_app.py file:

```
import logging
import azure.functions as func
import datetime
app = func.FunctionApp()
@app.function_name(name="eventgrid_output")
@app.event_grid_trigger(arg_name="eventGridEvent")
@app.event_grid_output(
arg_name="outputEvent",
topic_endpoint_uri="MyEventGridTopicUriSetting",
topic_key_setting="MyEventGridTopicKeySetting")
def eventgrid_output(eventGridEvent: func.EventGridEvent,
outputEvent: func.Out[func.EventGridOutputEvent]) -> None:
logging.log("eventGridEvent: ", eventGridEvent)
outputEvent.set(
func.EventGridOutputEvent(
id="test-id",
data={"tag1": "value1", "tag2": "value2"},
subject="test-subject",
event_type="test-event-1",
event_time=datetime.datetime.utcnow(),
data_version="1.0"))
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attribute to configure the binding. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#event-grid-output).

The attribute's constructor takes the name of an application setting that contains the name of the custom topic, and the name of an application setting that contains the topic key.

The following table explains the parameters for the `EventGridOutputAttribute`

.

| Parameter | Description |
|---|---|
TopicEndpointUri |
The name of an app setting that contains the URI for the custom topic, such as `MyTopicEndpointUri` . |
TopicKeySetting |
The name of an app setting that contains an access key for the custom topic. |
connection* |
The value of the common prefix for the setting that contains the topic endpoint URI. For more information about the naming format of this application setting, see
|

## Annotations

For Java classes, use the [EventGridAttribute](https://github.com/Azure/azure-functions-java-library/blob/dev/src/main/java/com/microsoft/azure/functions/annotation/EventGridOutput.java) attribute.

The attribute's constructor takes the name of an app setting that contains the name of the custom topic, and the name of an app setting that contains the topic key. For more information about these settings, see [Output - configuration](#configuration). Here's an `EventGridOutput`

attribute example:

```
public class Function {
@FunctionName("EventGridTriggerTest")
public void run(@EventGridTrigger(name = "event") String content,
@EventGridOutput(name = "outputEvent", topicEndpointUri = "MyEventGridTopicUriSetting", topicKeySetting = "MyEventGridTopicKeySetting") OutputBinding<String> outputEvent, final ExecutionContext context) {
...
}
}
```


## Configuration

The following table explains the properties that you can set on the `options`

object passed to the `output.eventGrid()`

method.

| Property | Description |
|---|---|
topicEndpointUri |
The name of an app setting that contains the URI for the custom topic, such as `MyTopicEndpointUri` . |
topicKeySetting |
The name of an app setting that contains an access key for the custom topic. |
connection* |
The value of the common prefix for the setting that contains the topic endpoint URI. When setting the `connection` property, the `topicEndpointUri` and `topicKeySetting` properties shouldn't be set. For more information about the naming format of this application setting, see
|

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `eventGrid` . |
direction |
Must be set to `out` . This parameter is set automatically when you create the binding in the Azure portal. |
name |
The variable name used in function code that represents the event. |
topicEndpointUri |
The name of an app setting that contains the URI for the custom topic, such as `MyTopicEndpointUri` . |
topicKeySetting |
The name of an app setting that contains an access key for the custom topic. |
connection* |
The value of the common prefix for the setting that contains the topic endpoint URI. For more information about the naming format of this application setting, see
|

*Support for identity-based connections requires version 3.3.x or higher of the extension.

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

Important

Make sure that you set the value of `TopicEndpointUri`

to the name of an app setting that contains the URI of the custom topic. Don't specify the URI of the custom topic directly in this property. The same applies when using `Connection`

.

See the [Example section](#example) for complete examples.

## Usage

The parameter type supported by the Event Grid output binding depends on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to write a single event, the Event Grid output binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The event as a string. |
`byte[]` |
The bytes of the event message. |
| JSON serializable types | An object representing a JSON event. Functions tries to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write multiple events, the Event Grid output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single event types |
An array containing multiple events. Each entry represents one event. |

For other output scenarios, create and use an [EventGridPublisherClient](/en-us/dotnet/api/azure.messaging.eventgrid.eventgridpublisherclient) with other types from [Azure.Messaging.EventGrid](/en-us/dotnet/api/azure.messaging.eventgrid) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

Send individual messages by calling a method parameter such as `out EventGridOutput paramName`

, and write multiple messages with `ICollector<EventGridOutput>`

.

Access the output event by using the `Push-OutputBinding`

cmdlet to send an event to the Event Grid output binding.

There are two options for outputting an Event Grid message from a function:

**Return value**: Set the`name`

property in*function.json*to`$return`

. With this configuration, the function's return value is persisted as an Event Grid message.**Imperative**: Pass a value to the[set](/en-us/python/api/azure-functions/azure.functions.out#set-val--t-----none)method of the parameter declared as an[Out](/en-us/python/api/azure-functions/azure.functions.out)type. The value passed to`set`

is persisted as an Event Grid message.

The output function parameter must be defined as `func.Out[str]`

, `func.Out[bytes]`

, `func.Out[func.EventGridOutputEvent]`

, or `func.Out[List[func.EventGridOutputEvent]]`

. Refer to the [output example](#example) for details.

## Connections

There are two ways of authenticating to an Event Grid topic when using the Event Grid output binding:

| Authentication method | Description |
|---|---|
| Using a topic key | Set the `TopicEndpointUri` and `TopicKeySetting` properties, as described in
|
| Using an identity | Set the `Connection` property to the name of a shared prefix for multiple application settings, together defining
|

### Use a topic key

Use the following steps to configure a topic key:

Follow the steps in

[Get access keys](../event-grid/get-access-keys)to obtain the topic key for your Event Grid topic.In your application settings, create a setting that defines the topic key value. Use the name of this setting for the

`TopicKeySetting`

property of the binding.In your application settings, create a setting that defines the topic endpoint. Use the name of this setting for the

`TopicEndpointUri`

property of the binding.

### Identity-based authentication

When using version 3.3.x or higher of the extension, you can connect to an Event Grid topic using an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis) to avoid having to obtain and work with topic keys.

You need to create an application setting that returns the topic endpoint URI. The name of the setting should combine a *unique common prefix* (for example, `myawesometopic`

) with the value `__topicEndpointUri`

. Then, you must use that common prefix (in this case, `myawesometopic`

) when you define the `Connection`

property in the binding.

In this mode, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Topic Endpoint URI | `<CONNECTION_NAME_PREFIX>__topicEndpointUri` |
The topic endpoint. | `https://<topic-name>.centralus-1.eventgrid.azure.net/api/events` |

More properties can be used to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

Note

When using [Azure App Configuration](../azure-app-configuration/quickstart-azure-functions-csharp) or [Key Vault](/en-us/azure/key-vault/general/overview) to provide settings for managed identity-based connections, setting names should use a valid key separator such as `:`

or `/`

in place of the `__`

to ensure names are resolved correctly.

For example, `<CONNECTION_NAME_PREFIX>:topicEndpointUri`

.

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

You must create a role assignment that provides access to your Event Grid topic at runtime. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) are not sufficient. The following table shows built-in roles that are recommended when using the Event Hubs extension in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles |
|---|---|
| Output binding |
|

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/monitor-functions-reference -->

# Azure Functions monitoring data reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article contains all the monitoring reference information for this service.

See [Monitor Azure Functions](monitor-functions) for details on the data you can collect for Azure Functions and how to use it.

See [Monitor executions in Azure Functions](functions-monitoring) for details on using Application Insights to collect and analyze log data from individual functions in your function app.

## Metrics

This section lists all the automatically collected platform metrics for this service. These metrics are also part of the global list of [all platform metrics supported in Azure Monitor](/en-us/azure/azure-monitor/reference/supported-metrics/metrics-index#supported-metrics-per-resource-type).

For information on metric retention, see [Azure Monitor Metrics overview](/en-us/azure/azure-monitor/essentials/data-platform-metrics#retention-of-metrics).

Hosting plans that allow your apps to scale dynamically support extra Functions-specific metrics:

These metrics are used to estimate the costs associated with *on demand* and *always ready* meters used for billing in a [Flex Consumption plan](flex-consumption-plan):

| Metric | Description | Meter calculation |
|---|---|---|
On Demand Function Execution Count |
Total number of function executions in on demand instances. | `OnDemandFunctionExecutionCount` relates to the On Demand Total Executions meter. |
Always Ready Function Execution Count |
Total number of function executions in always ready instances. | `AlwaysReadyFunctionExecutionCount` relates to the Always Ready Total Executions meter. |
On Demand Function Execution Units |
Total MB-milliseconds from on demand instances while actively executing functions. | `OnDemandFunctionExecutionUnits / 1,024,000` is the On Demand Execution Time meter, in GB-seconds. |
Always Ready Function Execution Units |
Total MB-milliseconds from always ready instances while actively executing functions. | `AlwaysReadyFunctionExecutionUnits / 1,024,000` is the Always Ready Execution Time meter, in GB-seconds. |
Always Ready Units |
The total MB-milliseconds of always ready instances assigned to the app, whether or not functions are actively executing. | `AlwaysReadyUnits / 1,024,000` is the Always Ready Baseline meter, in GB-seconds. |

In this table, all execution units are calculated by multiplying the fixed instance memory size, such as 512 MB or 2,048 MB, by total execution times, in milliseconds.

These metrics are used to monitor the performance and scaling behavior of your function app in a Flex Consumption plan:

| Metric | Description |
|---|---|
Automatic Scaling Instance Count |
The number of instances on which this app is running. Note that this is emitted every 30 seconds, and given Flex Consumption scales out and in fast, the number will be an aggregate of all new instances the app used in this time period. Make sure to change the aggregation to the minimum possible in the graph and the aggregation to "count". |
Memory working set |
The current amount of memory used by the app, in MB. Can be further filtered for each instance of the app. |
Average memory working set |
The average amount of memory used by the app, in megabytes (MB). Can be further filtered for each instance of the app. |
CPU Percentage |
The average percentage of CPU being used. Can be further filtered for each instance of the app. This is currently rolling out and might not be available for apps in all regions yet. |

These performance metrics help you understand resource utilization and scaling patterns in your Flex Consumption function app. The instance count metric is particularly useful for monitoring the dynamic scaling behavior, while memory and CPU metrics provide insights into resource consumption patterns.

### Supported metrics for Microsoft.Web/sites

The following table lists the metrics available for the Microsoft.Web/sites resource type. Most of these metrics apply to both function app and web apps, which both run on App Service.

Note

These metrics aren't available when your function app runs on Linux in a [Consumption plan](consumption-plan).

- All columns might not be present in every table.
- Some columns might be beyond the viewing area of the page. Select
**Expand table**to view all available columns.

**Table headings**

**Category**- The metrics group or classification.**Metric**- The metric display name as it appears in the Azure portal.**Name in REST API**- The metric name as referred to in the[REST API](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough).**Unit**- Unit of measure.**Aggregation**- The default[aggregation](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained)type. Valid values: Average (Avg), Minimum (Min), Maximum (Max), Total (Sum), Count.**Dimensions**-[Dimensions](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#dimensions-splitting-and-filtering)available for the metric.**Time Grains**-[Intervals](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#granularity)at which the metric is sampled. For example,`PT1M`

indicates that the metric is sampled every minute,`PT30M`

every 30 minutes,`PT1H`

every hour, and so on.**DS Export**- Whether the metric is exportable to Azure Monitor Logs via diagnostic settings. For information on exporting metrics, see[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings?tabs=portal).

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Always Ready Function Execution CountAlways Ready Function Execution Count. For Flex Consumption FunctionApps only. |
`AlwaysReadyFunctionExecutionCount` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Always Ready Function Execution UnitsAlways Ready Function Execution Units. For Flex Consumption FunctionApps only. |
`AlwaysReadyFunctionExecutionUnits` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Always Ready UnitsAlways Ready Units. For Flex Consumption FunctionApps only. |
`AlwaysReadyUnits` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
ConnectionsThe number of bound sockets existing in the sandbox (w3wp.exe and its child processes). A bound socket is created by calling bind()/connect() APIs and remains until said socket is closed with CloseHandle()/closesocket(). For WebApps and FunctionApps. |
`AppConnections` |
Count | Average, Count, Maximum, Minimum | `Instance` |
PT1M | Yes |
Average memory working setThe average amount of memory used by the app, in megabytes (MiB). For WebApps and FunctionApps. |
`AverageMemoryWorkingSet` |
Bytes | Average | `Instance` |
PT1M | Yes |
Average Response Time (deprecated)The average time taken for the app to serve requests, in seconds. For WebApps and FunctionApps. |
`AverageResponseTime` |
Seconds | Average | `Instance` |
PT1M | Yes |
Data InThe amount of incoming bandwidth consumed by the app, in MiB. For WebApps and FunctionApps. |
`BytesReceived` |
Bytes | Total (Sum) | `Instance` |
PT1M | Yes |
Data OutThe amount of outgoing bandwidth consumed by the app, in MiB. For WebApps and FunctionApps. |
`BytesSent` |
Bytes | Total (Sum) | `Instance` |
PT1M | Yes |
Percentage CPUThe average percentage of CPU being used. For Flex Consumption function apps only. |
`CpuPercentage` |
Percent | Average | `Instance` |
PT1M | Yes |
CPU TimeThe amount of CPU consumed by the app, in seconds. For more information about this metric. Please see
|
`CpuTime` |
Seconds | Count, Total (Sum), Minimum, Maximum | `Instance` |
PT1M | Yes |
Current AssembliesThe current number of Assemblies loaded across all AppDomains in this application. For WebApps and FunctionApps. |
`CurrentAssemblies` |
Count | Average | `Instance` |
PT1M | Yes |
File System UsagePercentage of filesystem quota consumed by the app. For WebApps and FunctionApps. |
`FileSystemUsage` |
Bytes | Average | <none> | PT6H, PT12H, P1D | Yes |
Function Execution CountFunction Execution Count. For FunctionApps only. |
`FunctionExecutionCount` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Function Execution UnitsFunction Execution Units. For FunctionApps only. |
`FunctionExecutionUnits` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Gen 0 Garbage CollectionsThe number of times the generation 0 objects are garbage collected since the start of the app process. Higher generation GCs include all lower generation GCs. For WebApps and FunctionApps. |
`Gen0Collections` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Gen 1 Garbage CollectionsThe number of times the generation 1 objects are garbage collected since the start of the app process. Higher generation GCs include all lower generation GCs. For WebApps and FunctionApps. |
`Gen1Collections` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Gen 2 Garbage CollectionsThe number of times the generation 2 objects are garbage collected since the start of the app process. For WebApps and FunctionApps. |
`Gen2Collections` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Handle CountThe total number of handles currently open by the app process. For WebApps and FunctionApps. |
`Handles` |
Count | Average | `Instance` |
PT1M | Yes |
Health check statusHealth check status. For WebApps and FunctionApps. |
`HealthCheckStatus` |
Count | Average | `Instance` |
PT5M, PT1H, P1D | Yes |
Http 101The count of requests resulting in an HTTP status code 101. For WebApps and FunctionApps. |
`Http101` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http 2xxThe count of requests resulting in an HTTP status code >= 200 but < 300. For WebApps and FunctionApps. |
`Http2xx` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http 3xxThe count of requests resulting in an HTTP status code >= 300 but < 400. For WebApps and FunctionApps. |
`Http3xx` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http 401The count of requests resulting in HTTP 401 status code. For WebApps and FunctionApps. |
`Http401` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http 403The count of requests resulting in HTTP 403 status code. For WebApps and FunctionApps. |
`Http403` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http 404The count of requests resulting in HTTP 404 status code. For WebApps and FunctionApps. |
`Http404` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http 406The count of requests resulting in HTTP 406 status code. For WebApps and FunctionApps. |
`Http406` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http 4xxThe count of requests resulting in an HTTP status code >= 400 but < 500. For WebApps and FunctionApps. |
`Http4xx` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Http Server ErrorsThe count of requests resulting in an HTTP status code >= 500 but < 600. For WebApps and FunctionApps. |
`Http5xx` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Response TimeThe time taken for the app to serve requests, in seconds. For WebApps and FunctionApps. |
`HttpResponseTime` |
Seconds | Average | `Instance` |
PT1M | Yes |
Automatic Scaling Instance CountThe number of instances on which this app is running. |
`InstanceCount` |
Count | Average | <none> | PT1M | Yes |
IO Other Bytes Per SecondThe rate at which the app process is issuing bytes to I/O operations that don't involve data, such as control operations. For WebApps and FunctionApps. |
`IoOtherBytesPerSecond` |
BytesPerSecond | Total (Sum) | `Instance` |
PT1M | Yes |
IO Other Operations Per SecondThe rate at which the app process is issuing I/O operations that aren't read or write operations. For WebApps and FunctionApps. |
`IoOtherOperationsPerSecond` |
BytesPerSecond | Total (Sum) | `Instance` |
PT1M | Yes |
IO Read Bytes Per SecondThe rate at which the app process is reading bytes from I/O operations. For WebApps and FunctionApps. |
`IoReadBytesPerSecond` |
BytesPerSecond | Total (Sum) | `Instance` |
PT1M | Yes |
IO Read Operations Per SecondThe rate at which the app process is issuing read I/O operations. For WebApps and FunctionApps. |
`IoReadOperationsPerSecond` |
BytesPerSecond | Total (Sum) | `Instance` |
PT1M | Yes |
IO Write Bytes Per SecondThe rate at which the app process is writing bytes to I/O operations. For WebApps and FunctionApps. |
`IoWriteBytesPerSecond` |
BytesPerSecond | Total (Sum) | `Instance` |
PT1M | Yes |
IO Write Operations Per SecondThe rate at which the app process is issuing write I/O operations. For WebApps and FunctionApps. |
`IoWriteOperationsPerSecond` |
BytesPerSecond | Total (Sum) | `Instance` |
PT1M | Yes |
Memory working setThe current amount of memory used by the app, in MiB. For WebApps and FunctionApps. |
`MemoryWorkingSet` |
Bytes | Average | `Instance` |
PT1M | Yes |
On Demand Function Execution CountOn Demand Function Execution Count. For Flex Consumption FunctionApps only. |
`OnDemandFunctionExecutionCount` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
On Demand Function Execution UnitsOn Demand Function Execution Units. For Flex Consumption FunctionApps only. |
`OnDemandFunctionExecutionUnits` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Private BytesPrivate Bytes is the current size, in bytes, of memory that the app process has allocated that can't be shared with other processes. For WebApps and FunctionApps. |
`PrivateBytes` |
Bytes | Average | `Instance` |
PT1M | Yes |
RequestsThe total number of requests regardless of their resulting HTTP status code. For WebApps and FunctionApps. |
`Requests` |
Count | Total (Sum) | `Instance` |
PT1M | Yes |
Requests In Application QueueThe number of requests in the application request queue. For WebApps and FunctionApps. |
`RequestsInApplicationQueue` |
Count | Average | `Instance` |
PT1M | Yes |
Thread CountThe number of threads currently active in the app process. For WebApps and FunctionApps. |
`Threads` |
Count | Average | `Instance` |
PT1M | Yes |
Total App DomainsThe current number of AppDomains loaded in this application. For WebApps and FunctionApps. |
`TotalAppDomains` |
Count | Average | `Instance` |
PT1M | Yes |
Total App Domains UnloadedThe total number of AppDomains unloaded since the start of the application. For WebApps and FunctionApps. |
`TotalAppDomainsUnloaded` |
Count | Average | `Instance` |
PT1M | Yes |
Workflow Action Completed CountWorkflow Action Completed Count. For LogicApps only. |
`WorkflowActionsCompleted` |
Count | Total (Sum) | `workflowName` , `status` |
PT1M | Yes |
Workflow Actions Failure RateWorkflow Actions Failure Rate. For LogicApps only. |
`WorkflowActionsFailureRate` |
Percent | Total (Sum) | `workflowName` |
PT1M | Yes |
Logic App Job Pull Rate Per SecondLogic Job Pull Rate per second. For LogicApps only. |
`WorkflowAppJobPullRate` |
CountPerSecond | Total (Sum) | `accountName` |
PT1M | Yes |
Workflow Job Execution DelayWorkflow Job Execution Delay. For LogicApps only. |
`WorkflowJobExecutionDelay` |
Seconds | Average | `workflowName` |
PT1M | Yes |
Workflow Job Execution DurationWorkflow Job Execution Duration. For LogicApps only. |
`WorkflowJobExecutionDuration` |
Seconds | Average | `workflowName` |
PT1M | Yes |
Workflow Runs Completed CountWorkflow Runs Completed Count. For LogicApps only. |
`WorkflowRunsCompleted` |
Count | Total (Sum) | `workflowName` , `status` |
PT1M | Yes |
Workflow Runs dispatched CountWorkflow Runs Dispatched Count. For LogicApps only. |
`WorkflowRunsDispatched` |
Count | Total (Sum) | `workflowName` |
PT1M | Yes |
Workflow Runs Failure RateWorkflow Runs Failure Rate. For LogicApps only. |
`WorkflowRunsFailureRate` |
Percent | Total (Sum) | `workflowName` |
PT1M | Yes |
Workflow Runs Started CountWorkflow Runs Started Count. For LogicApps only. |
`WorkflowRunsStarted` |
Count | Total (Sum) | `workflowName` |
PT1M | Yes |
Workflow Triggers Completed CountWorkflow Triggers Completed Count. For LogicApps only. |
`WorkflowTriggersCompleted` |
Count | Total (Sum) | `workflowName` , `status` |
PT1M | Yes |
Workflow Triggers Failure RateWorkflow Triggers Failure Rate. For LogicApps only. |
`WorkflowTriggersFailureRate` |
Percent | Total (Sum) | `workflowName` |
PT1M | Yes |

## Metric dimensions

For information about what metric dimensions are, see [Multi-dimensional metrics](/en-us/azure/azure-monitor/platform/data-platform-metrics#multi-dimensional-metrics).

This service doesn't have any metrics that contain dimensions.

## Resource logs

This section lists the types of resource logs you can collect for this service. The section pulls from the list of [all resource logs category types supported in Azure Monitor](/en-us/azure/azure-monitor/platform/resource-logs-schema).

### Supported resource logs for Microsoft.Web/sites

| Category | Category display name | Log table |
|
|---|

[Supports ingestion-time transformation](/en-us/azure/azure-monitor/essentials/data-collection-transformations)

`AppServiceAntivirusScanAuditLogs`

[AppServiceAntivirusScanAuditLogs](/en-us/azure/azure-monitor/reference/tables/appserviceantivirusscanauditlogs)Report on any discovered virus or infected files that have been uploaded to their site.

`AppServiceAppLogs`

[AppServiceAppLogs](/en-us/azure/azure-monitor/reference/tables/appserviceapplogs)Logs generated through your application.

[Queries](/en-us/azure/azure-monitor/reference/queries/appserviceapplogs)`AppServiceAuditLogs`

[AppServiceAuditLogs](/en-us/azure/azure-monitor/reference/tables/appserviceauditlogs)Logs generated when publishing users successfully log on via one of the App Service publishing protocols.

[Queries](/en-us/azure/azure-monitor/reference/queries/appserviceauditlogs)`AppServiceAuthenticationLogs`

[AppServiceAuthenticationLogs](/en-us/azure/azure-monitor/reference/tables/appserviceauthenticationlogs)Logs generated through App Service Authentication for your application.

[Queries](/en-us/azure/azure-monitor/reference/queries/appserviceauthenticationlogs)`AppServiceConsoleLogs`

[AppServiceConsoleLogs](/en-us/azure/azure-monitor/reference/tables/appserviceconsolelogs)Console logs generated from application or container.

[Queries](/en-us/azure/azure-monitor/reference/queries/appserviceconsolelogs)`AppServiceFileAuditLogs`

[AppServiceFileAuditLogs](/en-us/azure/azure-monitor/reference/tables/appservicefileauditlogs)Logs generated when app service content is modified.

[Queries](/en-us/azure/azure-monitor/reference/queries/appservicefileauditlogs)`AppServiceHTTPLogs`

[AppServiceHTTPLogs](/en-us/azure/azure-monitor/reference/tables/appservicehttplogs)Incoming HTTP requests on App Service. Use these logs to monitor application health, performance and usage patterns.

[Queries](/en-us/azure/azure-monitor/reference/queries/appservicehttplogs)`AppServiceIPSecAuditLogs`

[AppServiceIPSecAuditLogs](/en-us/azure/azure-monitor/reference/tables/appserviceipsecauditlogs)Logs generated through your application and pushed to Azure Monitoring.

`AppServicePlatformLogs`

[AppServicePlatformLogs](/en-us/azure/azure-monitor/reference/tables/appserviceplatformlogs)Logs generated through AppService platform for your application.

`FunctionAppLogs`

[FunctionAppLogs](/en-us/azure/azure-monitor/reference/tables/functionapplogs)Log generated by Function Apps. It includes logs emitted by the Functions host and logs emitted by customer code. Use these logs to monitor application health, performance, and behavior.

[Queries](/en-us/azure/azure-monitor/reference/queries/functionapplogs)`WorkflowRuntime`

[LogicAppWorkflowRuntime](/en-us/azure/azure-monitor/reference/tables/logicappworkflowruntime)Logs generated during Logic Apps workflow runtime.

[Queries](/en-us/azure/azure-monitor/reference/queries/logicappworkflowruntime)The log specific to Azure Functions is **FunctionAppLogs**.

For more information, see the [App Service monitoring data reference](/en-us/azure/app-service/monitor-app-service-reference#metrics).

## Azure Monitor Logs tables

This section lists the Azure Monitor Logs tables relevant to this service, which are available for query by Log Analytics using Kusto queries. The tables contain resource log data and possibly more depending on what is collected and routed to them.

### App Services

Microsoft.Web/sites

## Activity log

The linked table lists the operations that can be recorded in the activity log for this service. These operations are a subset of [all the possible resource provider operations in the activity log](/en-us/azure/role-based-access-control/resource-provider-operations).

For more information on the schema of activity log entries, see [Activity Log schema](/en-us/azure/azure-monitor/essentials/activity-log-schema).

The following table lists operations related to Azure Functions that might be created in the activity log.

| Operation | Description |
|---|---|
| Microsoft.web/sites/functions/listkeys/action | Return the
|

[host keys for the function app](function-keys-how-to).[Sync triggers](functions-deployment-technologies#trigger-syncing)operation.You may also find logged operations that relate to the underlying App Service behaviors. For a more complete list, see [Microsoft.Web resource provider operations](/en-us/azure/role-based-access-control/resource-provider-operations#microsoftweb).

## Related content

- See
[Monitor Azure Functions](monitor-functions)for a description of monitoring Azure Functions. - See
[Monitor Azure resources with Azure Monitor](/en-us/azure/azure-monitor/essentials/monitor-azure-resource)for details on monitoring Azure resources.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-timer -->

# Timer trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to work with timer triggers in Azure Functions. A timer trigger lets you run a function on a schedule.

This is reference information for Azure Functions developers. If you're new to Azure Functions, start with the following resources:

C# developer references:


For information on how to manually run a timer-triggered function, see [Manually run a non HTTP-triggered function](functions-manually-run-non-http).

Support for this binding is automatically provided in all development environments. You don't have to manually install the package or register the extension.

Source code for the timer extension package is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/) GitHub repository.

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

## Example

This example shows a C# function that executes each time the minutes have a value divisible by five. For example, when the function starts at 18:55:00, the next execution is at 19:00:00. A `TimerInfo`

object is passed to the function.

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

```
[Function(nameof(TimerFunction))]
[FixedDelayRetry(5, "00:00:10")]
public static void Run([TimerTrigger("0 */5 * * * *")] TimerInfo timerInfo,
FunctionContext context)
{
var logger = context.GetLogger(nameof(TimerFunction));
logger.LogInformation($"Function Ran. Next timer schedule = {timerInfo.ScheduleStatus?.Next}");
}
```


The following example function triggers and executes every five minutes. The `@TimerTrigger`

annotation on the function defines the schedule using the same string format as [CRON expressions](https://en.wikipedia.org/wiki/Cron#CRON_expression).

```
@FunctionName("keepAlive")
public void keepAlive(
@TimerTrigger(name = "keepAliveTrigger", schedule = "0 */5 * * * *") String timerInfo,
ExecutionContext context
) {
// timeInfo is a JSON string, you can deserialize it to an object using your favorite JSON library
context.getLogger().info("Timer is triggered: " + timerInfo);
}
```


The following example shows a timer trigger binding and function code that uses the binding, where an instance representing the timer is passed to the function. The function writes a log indicating whether this function invocation is due to a missed schedule occurrence. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

```
import datetime
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="mytimer")
@app.timer_trigger(schedule="0 */5 * * * *",
arg_name="mytimer",
run_on_startup=False)
def test_function(mytimer: func.TimerRequest) -> None:
utc_timestamp = datetime.datetime.utcnow().replace(
tzinfo=datetime.timezone.utc).isoformat()
if mytimer.past_due:
logging.info('The timer is past due!')
logging.info('Python timer trigger function ran at %s', utc_timestamp)
```


The following example shows a timer trigger [TypeScript function](functions-reference-node?tabs=typescript).

```
import { app, InvocationContext, Timer } from '@azure/functions';
export async function timerTrigger1(myTimer: Timer, context: InvocationContext): Promise<void> {
context.log('Timer function processed request.');
}
app.timer('timerTrigger1', {
schedule: '0 */5 * * * *',
handler: timerTrigger1,
});
```


The following example shows a timer trigger [JavaScript function](functions-reference-node).

Here's the binding data in the *function.json* file:

```
{
"schedule": "0 */5 * * * *",
"name": "myTimer",
"type": "timerTrigger",
"direction": "in"
}
```


The following is the timer function code in the run.ps1 file:

```
# Input bindings are passed in via param block.
param($myTimer)
# Get the current universal time in the default string format.
$currentUTCtime = (Get-Date).ToUniversalTime()
# The 'IsPastDue' property is 'true' when the current function invocation is later than scheduled.
if ($myTimer.IsPastDue) {
Write-Host "PowerShell timer is running late!"
}
# Write an information log with the current time.
Write-Host "PowerShell timer trigger function ran! TIME: $currentUTCtime"
```


## Attributes

[In-process](functions-dotnet-class-library) C# library uses [TimerTriggerAttribute](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs) from [Microsoft.Azure.WebJobs.Extensions](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions) whereas [isolated worker process](dotnet-isolated-process-guide) C# library uses [TimerTriggerAttribute](https://github.com/Azure/azure-functions-dotnet-worker/blob/main/extensions/Worker.Extensions.Timer/src/TimerTriggerAttribute.cs) from [Microsoft.Azure.Functions.Worker.Extensions.Timer](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Timer) to define the function. C# script instead uses a [function.json configuration file](#configuration).

| Attribute property | Description |
|---|---|
Schedule |
A
`TimeSpan` can be used only for a function app that runs on an App Service Plan. You can put the schedule expression in an app setting and set this property to the app setting name wrapped in % signs, as `%ScheduleAppSetting%` . |

**RunOnStartup**`true`

, the function is invoked when the runtime starts. For example, the runtime starts when the function app wakes up after going idle due to inactivity. when the function app restarts due to function changes, and when the function app scales out. *Use with caution.***RunOnStartup**should rarely if ever be set to`true`

, especially in production.**UseMonitor**`true`

or `false`

to indicate whether the schedule should be monitored. Schedule monitoring persists schedule occurrences to aid in ensuring the schedule is maintained correctly even when function app instances restart. If not set explicitly, the default is `true`

for schedules that have a recurrence interval greater than or equal to 1 minute. For schedules that trigger more than once per minute, the default is `false`

.## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, the following properties on the `schedule`

:

| Property | Description |
|---|---|
`arg_name` |
The name of the variable that represents the timer object in function code. |
`schedule` |
A
`TimeSpan` can be used only for a function app that runs on an App Service Plan. You can put the schedule expression in an app setting and set this property to the app setting name wrapped in % signs, as in this example: "%ScheduleAppSetting%". |

`run_on_startup`

`true`

, the function is invoked when the runtime starts. For example, the runtime starts when the function app wakes up after going idle due to inactivity. when the function app restarts due to function changes, and when the function app scales out. *Use with caution.***runOnStartup**should rarely if ever be set to`true`

, especially in production.`use_monitor`

`true`

or `false`

to indicate whether the schedule should be monitored. Schedule monitoring persists schedule occurrences to aid in ensuring the schedule is maintained correctly even when function app instances restart. If not set explicitly, the default is `true`

for schedules that have a recurrence interval greater than or equal to 1 minute. For schedules that trigger more than once per minute, the default is `false`

.For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

The `@TimerTrigger`

annotation on the function defines the `schedule`

using the same string format as [CRON expressions](https://en.wikipedia.org/wiki/Cron#CRON_expression). The annotation supports the following settings:

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `app.timer()`

method.

| Property | Description |
|---|---|
schedule |
A
`TimeSpan` can be used only for a function app that runs on an App Service Plan. You can put the schedule expression in an app setting and set this property to the app setting name wrapped in % signs, as in this example: "%ScheduleAppSetting%". |

**runOnStartup**`true`

, the function is invoked when the runtime starts. For example, the runtime starts when the function app wakes up after going idle due to inactivity. when the function app restarts due to function changes, and when the function app scales out. *Use with caution.***runOnStartup**should rarely if ever be set to`true`

, especially in production.**useMonitor**`true`

or `false`

to indicate whether the schedule should be monitored. Schedule monitoring persists schedule occurrences to aid in ensuring the schedule is maintained correctly even when function app instances restart. If not set explicitly, the default is `true`

for schedules that have a recurrence interval greater than or equal to 1 minute. For schedules that trigger more than once per minute, the default is `false`

.The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to "timerTrigger". This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to "in". This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that represents the timer object in function code. |
schedule |
A
`TimeSpan` can be used only for a function app that runs on an App Service Plan. You can put the schedule expression in an app setting and set this property to the app setting name wrapped in % signs, as in this example: "%ScheduleAppSetting%". |

**runOnStartup**`true`

, the function is invoked when the runtime starts. For example, the runtime starts when the function app wakes up after going idle due to inactivity. when the function app restarts due to function changes, and when the function app scales out. *Use with caution.***runOnStartup**should rarely if ever be set to`true`

, especially in production.**useMonitor**`true`

or `false`

to indicate whether the schedule should be monitored. Schedule monitoring persists schedule occurrences to aid in ensuring the schedule is maintained correctly even when function app instances restart. If not set explicitly, the default is `true`

for schedules that have a recurrence interval greater than or equal to 1 minute. For schedules that trigger more than once per minute, the default is `false`

.When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

Caution

Don't set **runOnStartup** to `true`

in production. Using this setting makes code execute at highly unpredictable times. In certain production settings, these extra executions can result in significantly higher costs for apps hosted in a Consumption plan. For example, with **runOnStartup** enabled the trigger is invoked whenever your function app is scaled. Make sure you fully understand the production behavior of your functions before enabling **runOnStartup** in production.

See the [Example section](#example) for complete examples.

## Usage

When a timer trigger function is invoked, a timer object is passed into the function. The following JSON is an example representation of the timer object.

```
{
"Schedule":{
"AdjustForDST": true
},
"ScheduleStatus": {
"Last":"2016-10-04T10:15:00+00:00",
"LastUpdated":"2016-10-04T10:16:00+00:00",
"Next":"2016-10-04T10:20:00+00:00"
},
"IsPastDue":false
}
```


```
{
"schedule":{
"adjustForDST": true
},
"scheduleStatus": {
"last":"2016-10-04T10:15:00+00:00",
"lastUpdated":"2016-10-04T10:16:00+00:00",
"next":"2016-10-04T10:20:00+00:00"
},
"isPastDue":false
}
```


The `isPastDue`

property is `true`

when the current function invocation is later than scheduled. For example, a function app restart might cause an invocation to be missed.

### NCRONTAB expressions

Azure Functions uses the [NCronTab](https://github.com/atifaziz/NCrontab) library to interpret NCRONTAB expressions. An NCRONTAB expression is similar to a CRON expression except that it includes an additional sixth field at the beginning to use for time precision in seconds:

`{second} {minute} {hour} {day} {month} {day-of-week}`


Each field can have one of the following types of values:

| Type | Example | When triggered |
|---|---|---|
| A specific value | `0 5 * * * *` |
Once every hour of the day at minute 5 of each hour |
All values (`*` ) |
`0 * 5 * * *` |
At every minute in the hour, during hour 5 |
A range (`-` operator) |
`5-7 * * * * *` |
Three times a minute - at seconds 5 through 7 during every minute of every hour of each day |
A set of values (`,` operator) |
`5,8,10 * * * * *` |
Three times a minute - at seconds 5, 8, and 10 during every minute of every hour of each day |
An interval value (`/` operator) |
`0 */5 * * * *` |
12 times an hour - at second 0 of every 5th minute of every hour of each day |

To specify months or days you can use numeric values, names, or abbreviations of names:

- For days, the numeric values are 0 to 6, where 0 starts with Sunday.
- Names are in English. For example:
`Monday`

,`January`

. - Names are case-insensitive.
- Names can be abbreviated. We recommend using three letters for abbreviations. For example:
`Mon`

,`Jan`

.

#### NCRONTAB examples

Here are some examples of NCRONTAB expressions you can use for the timer trigger in Azure Functions.

| Example | When triggered |
|---|---|
`0 */5 * * * *` |
once every five minutes |
`0 0 * * * *` |
once at the top of every hour |
`0 0 */2 * * *` |
once every two hours |
`0 0 9-17 * * *` |
once every hour from 9 AM to 5 PM |
`0 30 9 * * *` |
at 9:30 AM every day |
`0 30 9 * * 1-5` |
at 9:30 AM every weekday |
`0 30 9 * Jan Mon` |
at 9:30 AM every Monday in January |

Note

NCRONTAB expression supports both **five field** and **six field** format. The sixth field position is a value for seconds which is placed at the beginning of the expression.
If the CRON expression is invalid the Azure Portal Function Test will display a 404 error, if Application Insights is connected more details are logged there.

#### NCRONTAB time zones

The numbers in an NCRONTAB expression refer to a time and date, not a time span. For example, a 5 in the `hour`

field refers to 5:00 AM, not every 5 hours.

The default time zone used with the CRON expressions is Coordinated Universal Time (UTC). To have your CRON expression based on another time zone, create an app setting for your function app named `WEBSITE_TIME_ZONE`

.

The value of this setting depends on the operating system and plan on which your function app runs.

| Operating system | Plan | Value |
|---|---|---|
Windows |
All | Set the value to the name of the desired time zone as given by the second line from each pair given by the Windows command `tzutil.exe /L` |
Linux |
Premium Dedicated |
Set the value to the name of the desired time zone as shown in the
|

Note

`WEBSITE_TIME_ZONE`

and `TZ`

aren't currently supported when running on Linux in a [Flex Consumption](flex-consumption-plan) or [Consumption](consumption-plan) plan. In this case, the setting `WEBSITE_TIME_ZONE`

or `TZ`

can create SSL-related issues and cause metrics to stop working for your app.

For example, Eastern Time in the US (represented by `Eastern Standard Time`

(Windows) or `America/New_York`

(Linux)) currently uses UTC-05:00 during standard time and UTC-04:00 during daylight time. To have a timer trigger fire at 10:00 AM Eastern Time every day, create an app setting for your function app named `WEBSITE_TIME_ZONE`

, set the value to `Eastern Standard Time`

(Windows) or `America/New_York`

(Linux), and then use the following NCRONTAB expression:

```
"0 0 10 * * *"
```


When you use `WEBSITE_TIME_ZONE`

, the time is adjusted for time changes in the specific timezone, including daylight saving time and changes in standard time.

### TimeSpan

A `TimeSpan`

can be used only for a function app that runs on an App Service Plan.

Unlike an NCRONTAB expression, a `TimeSpan`

value specifies the time interval between each function invocation. When a function completes after running longer than the specified interval, the timer immediately invokes the function again.

Expressed as a string, the `TimeSpan`

format is `hh:mm:ss`

when `hh`

is less than 24. When the first two digits are 24 or greater, the format is `dd:hh:mm`

. Here are some examples:

| Example | When triggered |
|---|---|
| "01:00:00" | every hour |
| "00:01:00" | every minute |
| "25:00:00:00" | every 25 days |
| "1.00:00:00" | every day |

### Scale-out

If a function app scales out to multiple instances, only a single instance of a timer-triggered function is run across all instances. It will not trigger again if there is an outstanding invocation still running.

### Function apps sharing Storage

If you are sharing storage accounts across function apps that are not deployed to app service, you might need to explicitly assign host ID to each app.

| Functions version | Setting |
|---|---|
| 2.x (and higher) | `AzureFunctionsWebHost__hostid` environment variable |
| 1.x | `id` in host.json |

You can omit the identifying value or manually set each function app's identifying configuration to a different value.

The timer trigger uses a storage lock to ensure that there is only one timer instance when a function app scales out to multiple instances. If two function apps share the same identifying configuration and each uses a timer trigger, only one timer runs.

### Retry behavior

Unlike the queue trigger, the timer trigger doesn't retry after a function fails. When a function fails, it isn't called again until the next time on the schedule.

### Manually invoke a timer trigger

The timer trigger for Azure Functions provides an HTTP webhook that can be invoked to manually trigger the function. This can be extremely useful in the following scenarios.

- Integration testing
- Slot swaps as part of a smoke test or warmup activity
- Initial deployment of a function to immediately populate a cache or lookup table in a database

Please refer to [manually run a non HTTP-triggered function](functions-manually-run-non-http) for details on how to manually invoke a timer triggered function.

### Troubleshooting

For information about what to do when the timer trigger doesn't work as expected, see [Investigating and reporting issues with timer triggered functions not firing](https://github.com/Azure/azure-functions-host/wiki/Investigating-and-reporting-issues-with-timer-triggered-functions-not-firing).

## Connections

Timer triggers have an implicit dependency on blob storage, except when run locally through the Azure Functions Core Tools. The system uses blob storage to coordinate across multiple instances [when the app scales out](#scale-out). It accesses blob storage using the host storage (`AzureWebJobsStorage`

) connection. If you configure the host storage to use an [identity-based connection](functions-reference#connecting-to-host-storage-with-an-identity), the identity should have the [Storage Blob Data Owner](../role-based-access-control/built-in-roles#storage-blob-data-owner) role, which is the default requirement for host storage.
