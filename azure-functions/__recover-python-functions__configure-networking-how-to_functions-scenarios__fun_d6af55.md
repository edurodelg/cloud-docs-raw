---
merged_at: 2026-01-26T23:29:57.711780
merged_files: 2
---


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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr-trigger -->

# Dapr Input Bindings trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions can be triggered on a Dapr input binding using the following Dapr events.

For information on setup and configuration details of the Dapr extension, see the [Dapr extension overview](functions-bindings-dapr).

## Example

A C# function can be created using one of the following C# modes:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).```
[FunctionName("ConsumeMessageFromKafka")]
public static void Run(
// Note: the value of BindingName must match the binding name in components/kafka-bindings.yaml
[DaprBindingTrigger(BindingName = "%KafkaBindingName%")] JObject triggerData,
ILogger log)
{
log.LogInformation("Hello from Kafka!");
log.LogInformation($"Trigger data: {triggerData}");
}
```


Here's the Java code for the Dapr Input Binding trigger:

```
@FunctionName("ConsumeMessageFromKafka")
public String run(
@DaprBindingTrigger(
bindingName = "%KafkaBindingName%")
)
```


Use the `app`

object to register the `daprBindingTrigger`

:

```
const { app, trigger } = require('@azure/functions');
app.generic('ConsumeMessageFromKafka', {
trigger: trigger.generic({
type: 'daprBindingTrigger',
bindingName: "%KafkaBindingName%",
name: "triggerData"
}),
handler: async (request, context) => {
context.log("Node function processed a ConsumeMessageFromKafka request from the Dapr Runtime.");
context.log(context.triggerMetadata.triggerData)
}
});
```


The following example shows Dapr triggers in a *function.json* file and PowerShell code that uses those bindings.

Here's the *function.json* file for `daprBindingTrigger`

:

```
{
"bindings": [
{
"type": "daprBindingTrigger",
"bindingName": "%KafkaBindingName%",
"name": "triggerData",
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
$triggerData
)
Write-Host "PowerShell function processed a ConsumeMessageFromKafka request from the Dapr Runtime."
$jsonString = $triggerData | ConvertTo-Json
Write-Host "Trigger data: $jsonString"
```


The following example shows a Dapr Input Binding trigger, which uses the [v2 Python programming model](functions-reference-python). To use the `daprBinding`

in your Python function app code:

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="ConsumeMessageFromKafka")
@app.dapr_binding_trigger(arg_name="triggerData", binding_name="%KafkaBindingName%")
def main(triggerData: str) -> None:
logging.info('Python function processed a ConsumeMessageFromKafka request from the Dapr Runtime.')
logging.info('Trigger data: ' + triggerData)
```


## Attributes

In the [in-process model](functions-dotnet-class-library), use the `DaprBindingTrigger`

to trigger a Dapr input binding, which supports the following properties.

| Parameter | Description |
|---|---|
BindingName |
The name of the Dapr trigger. If not specified, the name of the function is used as the trigger name. |

## Annotations

The `DaprBindingTrigger`

annotation allows you to create a function that gets triggered by the binding component you created.

| Element | Description |
|---|---|
bindingName |
The name of the Dapr binding. |

## Configuration

The following table explains the binding configuration properties that you set in the code.

| Property | Description |
|---|---|
bindingName |
The name of the binding. |

The following table explains the binding configuration properties that you set in the function.json file.

| function.json property | Description |
|---|---|
bindingName |
The name of the binding. |

See the [Example section](#example) for complete examples.

## Usage

To use the Dapr Input Binding trigger, start by setting up a Dapr input binding component. You can learn more about which component to use and how to set it up in the official Dapr documentation.

To use the `daprBindingTrigger`

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
