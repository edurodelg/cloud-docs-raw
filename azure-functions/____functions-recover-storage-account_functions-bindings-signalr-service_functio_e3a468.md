---
merged_at: 2026-01-26T21:02:36.329153
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-recover-storage-account -->

# Troubleshoot error: "Azure Functions Runtime is unreachable"

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article helps you troubleshoot the following error string that appears in the Azure portal:

"Error: Azure Functions Runtime is unreachable. Click here for details on storage configuration."


This issue occurs when the Functions runtime can't start. The most common reason for this is that the function app lost access to its storage account. For more information, see [Storage account requirements](storage-considerations#storage-account-requirements).

The rest of this article helps you troubleshoot specific causes of this error, including how to identify and resolve each case.

## Storage account was deleted

Every function app requires a storage account that is used by the Functions host to operate. If that default host storage account is deleted, your function app won't run.

Start by looking up your storage account name in your application settings. Either `AzureWebJobsStorage`

or `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

contains the name of your storage account as part of a connection string. For more information, see [App settings reference for Azure Functions](functions-app-settings#azurewebjobsstorage).

Search for your storage account in the Azure portal to see whether it still exists. If it has been deleted, re-create the storage account and replace your storage connection strings. Your function code is lost, and you need to redeploy it.

## Storage account application settings were deleted

In the preceding step, if you can't find a storage account connection string, it was likely deleted or overwritten. Deleting application settings most commonly happens when you're using deployment slots or Azure Resource Manager scripts to set application settings.

### Required application settings

- Required:
- Required for Elastic Premium and Consumption plan functions:

For more information, see [App settings reference for Azure Functions](functions-app-settings).

### Guidance

- Don't check
**slot setting**for any of these settings. If you swap deployment slots, the function app breaks. - Don't modify these settings as part of automated deployments.
- These settings must be provided and valid at creation time. An automated deployment that doesn't contain these settings results in a function app that doesn't run, even if the settings are added later.

## Storage account credentials are invalid

The previously discussed storage account connection strings must be updated if you regenerate storage keys. For more information about storage key management, see [Create an Azure Storage account](../storage/common/storage-account-create).

## Storage account is inaccessible

Your function app must be able to access the storage account. Common issues that block a function app's access to a storage account are:

The function app is deployed to your App Service Environment (ASE) without the correct network rules to allow traffic to and from the storage account.

The storage account firewall is enabled and not configured to allow traffic to and from functions. For more information, see

[Configure Azure Storage firewalls and virtual networks](../storage/common/storage-network-security?toc=/azure/storage/files/toc.json).Verify that the

`allowSharedKeyAccess`

setting is set to`true`

, which is its default value. For more information, see[Prevent Shared Key authorization for an Azure Storage account](../storage/common/shared-key-authorization-prevent?tabs=portal#verify-that-shared-key-access-is-not-allowed).

## Daily execution quota is full

If you have a daily execution quota configured, your function app is temporarily disabled, which causes many of the portal controls to become unavailable.

To verify the quota in the [Azure portal](https://portal.azure.com), select **Platform Features** > **Function App Settings** in your function app. If you're over the **Daily Usage Quota** that you set, the following message is displayed:

"The Function App has reached daily usage quota and has been stopped until the next 24 hours time frame."


To resolve this issue, remove or increase the daily quota, and then restart your app. Otherwise, the execution of your app is blocked until the next day.

## App is behind a firewall

Your function app might be unreachable for either of the following reasons:

Your function app is hosted in an

[internally load balanced App Service Environment](../app-service/environment/create-ilb-ase)and it's configured to block inbound internet traffic.Your function app has

[inbound IP restrictions](functions-networking-options#inbound-networking-features)that are configured to block internet access.

The Azure portal makes calls directly to the running app to fetch the list of functions, and it makes HTTP calls to the Kudu endpoint. Platform-level settings under the **Platform Features** tab are still available.

To verify your ASE configuration:

- Go to the network security group (NSG) of the subnet where the ASE resides.
- Validate the inbound rules to allow traffic that's coming from the public IP of the computer where you're accessing the application.

You can also use the portal from a computer that's connected to the virtual network that's running your app or to a virtual machine that's running in your virtual network.

For more information about inbound rule configuration, see [Networking considerations for an App Service Environment](../app-service/environment/network-info#network-security-groups).

## Container errors on Linux

For function apps that run on Linux in a container, the `Azure Functions runtime is unreachable`

error can occur as a result of problems with the container. Use the following procedure to review the container logs for errors:

Navigate to the Kudu endpoint for the function app, which is located at

`https://<FUNCTION_APP>.scm.azurewebsites.net`

, where`<FUNCTION_APP>`

is the name of your app.Download the Docker logs .zip file and review the contents on your local computer.

Check for any logged errors that indicate that the container is unable to start successfully.


## Container image unavailable

Errors can occur when the container image being referenced is unavailable or fails to start correctly. Check for any logged errors that indicate that the container is unable to start successfully.

You need to correct any errors that prevent the container from starting for the function app run correctly.

When the container image can't be found, you see a `manifest unknown`

error in the Docker logs. In this case, you can use the Azure CLI commands documented at [How to target Azure Functions runtime versions](set-runtime-version?tabs=azurecli#manual-version-updates-on-linux) to change the container image being referenced. If you've deployed a [custom container image](functions-how-to-custom-container), you need to fix the image and redeploy the updated version to the referenced registry.

## App container has conflicting ports

Your function app might be in an unresponsive state due to conflicting port assignment upon startup. This situation can happen in the following cases:

- Your container has separate services running where one or more services are tying to bind to the same port as the function app.
- You added an Azure Hybrid Connection that shares the same port value as the function app.

By default, the container in which your function app runs uses port `:80`

. When other services in the same container are also trying to using port `:80`

, the function app can fail to start. If your logs show port conflicts, change the default ports.

## Host ID collision

Starting with version 3.x of the Functions runtime, [host ID collision](storage-considerations#host-id-considerations) are detected and logged as a warning. In version 4.x, an error is logged and the host is stopped. If the runtime can't start for your function app, [review the logs](analyze-telemetry-data). If there's a warning or an error about host ID collisions, follow the mitigation steps in [Host ID considerations](storage-considerations#host-id-considerations).

## Read-only app settings

Changing any *read-only* [App Service application settings](../app-service/reference-app-settings#app-environment) can put your function app into an unreachable state.

## ASP.NET authentication overrides

*Applies only to C# apps running in-process with the Functions host.*

Configuring ASP.NET authentication in a Functions startup class can override services that are required for the Azure portal to communicate with the host. This includes, but isn't limited to, any calls to `AddAuthentication()`

. If the host's authentication services are overridden and the portal can't communicate with the host, it considers the app unreachable. This issue might result in errors such as: `No authentication handler is registered for the scheme 'ArmToken'.`


## Next steps

Learn about monitoring your function apps:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-signalr-service -->

# SignalR Service bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This set of articles explains how to authenticate and send real-time messages to clients connected to [Azure SignalR Service](https://azure.microsoft.com/services/signalr-service/) by using SignalR Service bindings in Azure Functions. Azure Functions runtime version 2.x and higher supports input and output bindings for SignalR Service.

| Action | Type |
|---|---|
| Handle messages from SignalR Service |
|

[Input binding](functions-bindings-signalr-service-input)[Output binding](functions-bindings-signalr-service-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

Add the extension to your project by installing this [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.SignalRService/).

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

## Add dependency

To use the SignalR Service annotations in Java functions, you need to add a dependency to the *azure-functions-java-library-signalr* artifact (version 1.0 or higher) to your *pom.xml* file.

```
<dependency>
<groupId>com.microsoft.azure.functions</groupId>
<artifactId>azure-functions-java-library-signalr</artifactId>
<version>1.0.0</version>
</dependency>
```


## Connections

You can use [connection string](#connection-string) or [Microsoft Entra identity](#identity-based-connections) to connect to Azure SignalR Service.

### Connection string

For instructions on how to retrieve the connection string for your Azure SignalR Service, see [Connection strings in Azure SignalR Service](../azure-signalr/concept-connection-string#how-to-get-connection-strings)

This connection string should be stored in an application setting with a name `AzureSignalRConnectionString`

. You can customize the application setting name with the `connectionStringSetting`

property of the binding configuration.

### Identity-based connections

If you're using version 1.7.0 or higher, instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis).

First of all, you should make sure your Microsoft Entra identity has role [SignalR Service Owner](../role-based-access-control/built-in-roles#signalr-service-owner).

Then you would define settings with a common prefix `AzureSignalRConnectionString`

. You can customize prefix name with the `connectionStringSetting`

property of the binding configuration.

In this mode, the settings include following items:

| Property | Environment variable template | Description | Required | Example value |
|---|---|---|---|---|
| Service URI | `AzureSignalRConnectionString__serviceUri` |
The URI of your service endpoint. When you only configure "Service URI", the extensions would attempt to use
|

`AzureSignalRConnectionString__credential`

`managedidentity`

if your deployed Azure Function intends to use managed identity authentication. This value is only valid when a managed identity is available in the hosting environment.`AzureSignalRConnectionString__clientId`

`credential`

is set to `managedidentity`

, this property can be set to specify the user-assigned identity to be used when obtaining a token. The property accepts a client ID corresponding to a user-assigned identity assigned to the application. It's invalid to specify both a Resource ID and a client ID. If not specified, the system-assigned identity is used. This property is used differently in [local development scenarios](functions-reference#local-development-with-identity-based-connections), when`credential`

shouldn't be set.`AzureSignalRConnectionString__managedIdentityResourceId`

`credential`

is set to `managedidentity`

, this property can be set to specify the resource Identifier to be used when obtaining a token. The property accepts a resource identifier corresponding to the resource ID of the user-defined managed identity. It's invalid to specify both a resource ID and a client ID. If neither are specified, the system-assigned identity is used. This property is used differently in [local development scenarios](functions-reference#local-development-with-identity-based-connections), when`credential`

shouldn't be set.Note

When using `local.settings.json`

file at local, [Azure App Configuration](../azure-app-configuration/quickstart-azure-functions-csharp), or [Key Vault](/en-us/azure/key-vault/general/overview) to provide settings for identity-based connections, replace `__`

with `:`

in the setting name to ensure names are resolved correctly.

For example, `AzureSignalRConnectionString:serviceUri`

.

#### Multiple endpoints setting

You can also configure multiple endpoints and specify identity settings per endpoint.

In this case, prefix your settings with `Azure__SignalR__Endpoints__{endpointName}`

. The `{endpointName}`

is an arbitrary name assigned by you to associate a group of settings to a service endpoint. The prefix `Azure__SignalR__Endpoints__{endpointName}`

can't be customized by `connectionStringSetting`

property.

| Property | Environment variable template | Description | Required | Example value |
|---|---|---|---|---|
| Service URI | `Azure__SignalR__Endpoints__{endpointName}__serviceUri` |
The URI your service endpoint. When you only configure "Service URI", the extensions would attempt to use
|

`Azure__SignalR__Endpoints__{endpointName}__type`

`Primary`

. Valid values are `Primary`

and `Secondary`

, case-insensitive.`Secondary`

`Azure__SignalR__Endpoints__{endpointName}__credential`

`managedidentity`

if your deployed Azure Function intends to use managed identity authentication. This value is only valid when a managed identity is available in the hosting environment.`Azure__SignalR__Endpoints__{endpointName}__clientId`

`credential`

is set to `managedidentity`

, this property can be set to specify the user-assigned identity to be used when obtaining a token. The property accepts a client ID corresponding to a user-assigned identity assigned to the application. It's invalid to specify both a Resource ID and a client ID. If not specified, the system-assigned identity is used. This property is used differently in [local development scenarios](functions-reference#local-development-with-identity-based-connections), when`credential`

shouldn't be set.`Azure__SignalR__Endpoints__{endpointName}__managedIdentityResourceId`

`credential`

is set to `managedidentity`

, this property can be set to specify the resource Identifier to be used when obtaining a token. The property accepts a resource identifier corresponding to the resource ID of the user-defined managed identity. It's invalid to specify both a resource ID and a client ID. If neither are specified, the system-assigned identity is used. This property is used differently in [local development scenarios](functions-reference#local-development-with-identity-based-connections), when`credential`

shouldn't be set.For more information about multiple endpoints, see [Scale SignalR Service with multiple instances](../azure-signalr/signalr-howto-scale-multi-instances?pivots=serverless-mode#for-signalr-functions-extensions)

For optimal security, your function app should use managed identities when connecting to the Azure SignalR service instead of using a connection string, which contains a shared secret key. For more information, see [Authorize requests to Azure SignalR Service resources with Microsoft Entra managed identities](../azure-signalr/signalr-howto-authorize-managed-identity#azure-signalr-service-bindings-in-azure-functions).

## Next steps

For details on how to configure and use SignalR Service and Azure Functions together, refer to [Azure Functions development and configuration with Azure SignalR Service](../azure-signalr/signalr-concept-serverless-development-config).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-develop-local -->

# Code and test Azure Functions locally

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Whenever possible, you should create and validate your Azure Functions code project in a local development environment. Azure Functions Core Tools provides a local runtime version of Azure Functions that integrates with popular development tools for an integrated development, debugging, and deployments. Your local functions can even connect to live Azure services.

This article provides some shared guidance for local development, such as working with the [local.settings.json file](#local-settings-file). It also links to development environment-specific guidance.

Tip

You can find detailed information about how to develop functions locally in the linked IDE-specific guidance articles.

## Local development environments

The way in which you develop functions on your local computer depends on your [language](supported-languages) and tooling preferences. Make sure to choose your preferred language at the [top of the article](#top).

Tip

All local development relies on Azure Functions Core Tools to provide the Functions runtime for debugging in a local environment.

You can use these development environments to code functions locally in your preferred language:

| Environment | Description |
|---|---|
|

**Azure development**workload of[Visual Studio](https://www.visualstudio.com/vs/). Lets you compile and deploy your C# function code to Azure as a .NET class library. Includes the Core Tools for local testing. To learn more, see[Create your first C# function in Azure using Visual Studio](functions-create-your-first-function-visual-studio)[Visual Studio Code](functions-develop-vs-code)[Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)adds Functions support to Visual Studio Code. Requires the Core Tools. Supports development on Linux, macOS, and Windows. To learn more, see[Create your first function using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-csharp).[Command prompt or terminal](functions-run-local)[Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools)provides the core runtime and templates for creating functions, which enable local development. Supports development on Linux, macOS, and Windows. To learn more, see[Create a C# function in Azure from the command line](how-to-create-function-azure-cli?pivots=programming-language-csharp).| Environment | Description |
|---|---|
|

[Create your first function with Java and Maven](how-to-create-function-azure-cli?pivots=programming-language-java).[Visual Studio Code](functions-develop-vs-code)[Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)adds Functions support to Visual Studio Code. Requires the Core Tools. Supports development on Linux, macOS, and Windows. To learn more, see[Create your first function using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-java).[IntelliJ IDEA](functions-create-maven-intellij)[Create your first Java function in Azure using IntelliJ](functions-create-maven-intellij).[Eclipse](functions-create-maven-eclipse)[Create your first Java function in Azure using Ecplise](functions-create-maven-eclipse).| Environment | Description |
|---|---|
|

[Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)adds Functions support to Visual Studio Code. Requires the Core Tools. Supports development on Linux, macOS, and Windows. To learn more, see[Create your first function using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-javascript).[Command prompt or terminal](functions-run-local)[Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools)provides the core runtime and templates for creating functions, which enable local development. Supports development on Linux, macOS, and Windows. To learn more, see[Create a Node.js function in Azure from the command line](how-to-create-function-azure-cli?pivots=programming-language-javascript).| Environment | Description |
|---|---|
|

[Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)adds Functions support to Visual Studio Code. Requires the Core Tools. Supports development on Linux, macOS, and Windows. To learn more, see[Create your first function using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-powershell).[Command prompt or terminal](functions-run-local)[Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools)provides the core runtime and templates for creating functions, which enable local development. Supports development on Linux, macOS, and Windows. To learn more, see[Create a PowerShell function in Azure from the command line](how-to-create-function-azure-cli?pivots=programming-language-powershell).| Environment | Description |
|---|---|
|

[Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)adds Functions support to Visual Studio Code. Requires the Core Tools. Supports development on Linux, macOS, and Windows. To learn more, see[Create your first function using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-python).[Command prompt or terminal](functions-run-local)[Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools)provides the core runtime and templates for creating functions, which enable local development. Supports development on Linux, macOS, and Windows. To learn more, see[Create a Python function in Azure from the command line](how-to-create-function-azure-cli?pivots=programming-language-python).Each of these local development environments lets you create function app projects and use predefined function templates to create new functions. Each uses the Core Tools so that you can test and debug your functions against the real Functions runtime on your own machine just as you would any other app. You can also publish your function app project from any of these environments to Azure.

## Local project files

A Functions project directory contains the following files in the project root folder, regardless of language:

| File name | Description |
|---|---|
| host.json | To learn more, see the
|

[local settings file](#local-settings-file).[local settings file](#local-settings-file).Other files in the project depend on your language and specific functions. For more information, see the developer guide for your language.

### Local settings file

The `local.settings.json`

file stores app settings and settings used by local development tools. Settings in the `local.settings.json`

file are used only when you're running your project locally. When you publish your project to Azure, be sure to also add any required settings to the app settings for the function app.

Important

Because the `local.settings.json`

file might contain secrets, such as connection strings, you should use caution committing to source control. Tools that support Functions provide ways to synchronize settings in the `local.settings.json`

file with the [app settings](functions-how-to-use-azure-function-app-settings#settings) in the function app to which your project is deployed.

The `local.settings.json`

file has this structure:

```
{
"IsEncrypted": false,
"Values": {
"FUNCTIONS_WORKER_RUNTIME": "<language worker>",
"AzureWebJobsStorage": "<connection-string>",
"MyBindingConnection": "<binding-connection-string>",
"AzureWebJobs.HttpExample.Disabled": "true"
},
"Host": {
"LocalHttpPort": 7071,
"CORS": "*",
"CORSCredentials": false
},
"ConnectionStrings": {
"SQLConnectionString": "<sqlclient-connection-string>"
}
}
```


These settings are supported when you run projects locally:

| Setting | Description |
|---|---|
`IsEncrypted` |
When this setting is set to `true` , all values are encrypted with a local machine key. Used with `func settings` commands. Default value is `false` . You might want to encrypt the local.settings.json file on your local computer when it contains secrets, such as service connection strings. The host automatically decrypts settings when it runs. Use the `func settings decrypt` command before trying to read locally encrypted settings. |
`Values` |
Collection of application settings used when a project is running locally. These key-value (string-string) pairs correspond to application settings in your function app in Azure, like
`AzureWebJobsStorage` |

`Connection`

for the [Blob storage trigger](functions-bindings-storage-blob-trigger#configuration). For these properties, you need an application setting defined in the

`Values`

array. See the subsequent table for a list of commonly used settings. Values must be strings and not JSON objects or arrays. Setting names can't include a double underline (

`__`

) and shouldn't include a colon (`:`

). Double underline characters are reserved by the runtime, and the colon is reserved to support [dependency injection](functions-dotnet-dependency-injection#working-with-options-and-settings).

`Host`

`LocalHttpPort`

`func host start`

and `func run`

). The `--port`

command-line option takes precedence over this setting. For example, when running in Visual Studio IDE, you may change the port number by navigating to the "Project Properties -> Debug" window and explicitly specifying the port number in a `host start --port <your-port-number>`

command that can be supplied in the "Application Arguments" field.`CORS`

[cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing). Origins are supplied as a comma-separated list with no spaces. The wildcard value (*) is supported, which allows requests from any origin.`CORSCredentials`

`true`

, allows `withCredentials`

requests.`ConnectionStrings`

`ConnectionStrings`

section of a configuration file, like [Entity Framework](/en-us/ef/ef6/). Connection strings in this object are added to the environment with the provider type of[System.Data.SqlClient](/en-us/dotnet/api/system.data.sqlclient). Items in this collection aren't published to Azure with other app settings. You must explicitly add these values to the`Connection strings`

collection of your function app settings. If you're creating a [in your function code, you should store the connection string value with your other connections in](/en-us/dotnet/api/system.data.sqlclient.sqlconnection)`SqlConnection`

**Application Settings**in the portal.The following application settings can be included in the ** Values** array when running locally:

| Setting | Values | Description |
|---|---|---|
`AzureWebJobsStorage` |
Storage account connection string, or`UseDevelopmentStorage=true` |
Contains the connection string for an Azure storage account. Required when using triggers other than HTTP. For more information, see the
`AzureWebJobsStorage` |

When you have the

[Azurite Emulator](../storage/common/storage-use-azurite)installed locally and you set

[to](functions-app-settings#azurewebjobsstorage)

`AzureWebJobsStorage`

`UseDevelopmentStorage=true`

, Core Tools uses the emulator. For more information, see [Local storage emulator](#local-storage-emulator).

`AzureWebJobs.<FUNCTION_NAME>.Disabled`

`true`

|`false`

`"AzureWebJobs.<FUNCTION_NAME>.Disabled": "true"`

to the collection, where `<FUNCTION_NAME>`

is the name of the function. To learn more, see [How to disable functions in Azure Functions](disable-function#disable-functions-locally).`FUNCTIONS_WORKER_RUNTIME`

`dotnet`

`dotnet-isolated`

`node`

`java`

`powershell`

`python`

[reference.](functions-app-settings#functions_worker_runtime)`FUNCTIONS_WORKER_RUNTIME`

`FUNCTIONS_WORKER_RUNTIME_VERSION`

`~7`

`powerShellVersion`

site configuration setting, when it runs in Azure, which can be [set in the portal](functions-reference-powershell#changing-the-powershell-version).To learn how to use values from the `values`

array as environment variables in your function code, see [Environment variables](functions-reference-node#environment-variables) in the developer guide.

To learn how to use values from the `values`

array as environment variables in your function code, see [Environment variables](functions-reference-java#environment-variables) in the developer guide.

To learn how to use values from the `values`

array as environment variables in your function code, see [Environment variables](functions-reference-powershell#environment-variables) in the developer guide.

To learn how to use values from the `values`

array as environment variables in your function code, see [Environment variables](functions-reference-python#environment-variables) in the developer guide.

## Synchronize settings

When you develop your functions locally, any local settings required by your app must also be present in app settings of the function app to which your code is deployed. You might also need to download current settings from the function app to your local project. While you can [manually configure app settings in the Azure portal](functions-how-to-use-azure-function-app-settings?tabs=portal#settings), the following tools also let you synchronize app settings with local settings in your project:

## Triggers and bindings

When you develop your functions locally, you need to take trigger and binding behaviors into consideration. For HTTP triggers, you can call the HTTP endpoint on the local computer, using `http://localhost/`

. For non-HTTP triggered functions, there are several options to run locally:

- The easiest way to test bindings during local development is to use connection strings that target live Azure services. You can target live services by adding the appropriate connection string settings in the
`Values`

array in the local.settings.json file. When you do this, local executions during testing might affect your production services. Instead, consider setting-up separate services to use during development and testing, and then switch to different services during production. - For storage-based triggers, you can use a
[local storage emulator](#local-storage-emulator). - You can manually run non-HTTP trigger functions by using special administrator endpoints. For more information, see
[Manually run a non-HTTP-triggered function](functions-manually-run-non-http).

During local testing, you must be running the host provided by Core Tools (func.exe) locally. For more information, see [Azure Functions Core Tools](functions-run-local).

## HTTP test tools

During development, it's easy to call any of your function endpoints from a web browser when they support the HTTP GET method. However, for other HTTP methods that support payloads, such as POST or PUT, you need to use an HTTP test tool to create and send these HTTP requests to your function endpoints.

Caution

For scenarios where your requests must include sensitive data, make sure to use a tool that protects your data and reduces the risk of exposing any sensitive data to the public. Sensitive data you should protect might include: credentials, secrets, access tokens, API keys, geolocation data, even personal data.

You can keep your data secure by choosing an HTTP test tool that works either offline or locally, doesn't sync your data to the cloud, and doesn't require that you sign in to an online account. Some tools can also protect your data from accidental exposure by implementing specific security features.

Avoid using tools that centrally store your HTTP request history (including sensitive information), don't follow best security practices, or don't respect data privacy concerns.

Consider using one of these tools for securely sending HTTP requests to your function endpoints:

[Visual Studio Code](https://code.visualstudio.com/download)with an[extension from Visual Studio Marketplace](https://marketplace.visualstudio.com/vscode), such as[REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)[PowerShell Invoke-RestMethod](/en-us/powershell/module/microsoft.powershell.utility/invoke-restmethod)[Microsoft Edge - Network Console tool](/en-us/microsoft-edge/devtools-guide-chromium/network-console/network-console-tool)[Bruno](https://www.usebruno.com/)[curl](https://curl.se/)

## Local storage emulator

During local development, you can use the local [Azurite emulator](../storage/common/storage-use-azurite) when testing functions with Azure Storage bindings (Queue Storage, Blob Storage, and Table Storage), without having to connect to remote storage services. Azurite integrates with Visual Studio Code and Visual Studio, and you can also run it from the command prompt using npm. For more information, see [Use the Azurite emulator for local Azure Storage development](../storage/common/storage-use-azurite).

The following setting in the `Values`

collection of the local.settings.json file tells the local Functions host to use Azurite for the default `AzureWebJobsStorage`

connection:

```
"AzureWebJobsStorage": "UseDevelopmentStorage=true"
```


With this setting value, any Azure Storage trigger or binding that uses `AzureWebJobsStorage`

as its connection connects to Azurite when running locally. Keep these considerations in mind when using storage emulation during local execution:

- You must have Azurite installed and running.
- You should test with an actual storage connection to Azure services before publishing to Azure.
- When you publish your project, don't publish the
`AzureWebJobsStorage`

setting as`UseDevelopmentStorage=true`

. In Azure, the`AzureWebJobsStorage`

setting must always be the connection string of the storage account used by your function app. For more information, see.`AzureWebJobsStorage`


## Related articles

- To learn more about local development of functions using Visual Studio, see
[Develop Azure Functions using Visual Studio](functions-develop-vs).

- To learn more about local development of functions using Visual Studio Code on a Mac, Linux, or Windows computer, see
[Develop Azure Functions by using Visual Studio Code](functions-develop-vs-code). - To learn more about developing functions from the command prompt or terminal, see
[Work with Azure Functions Core Tools](functions-run-local).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-mysql -->

# Overview of Azure Database for MySQL bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This set of articles explains how to work with [Azure Database for MySQL](/en-us/azure/mysql/index) bindings in Azure Functions. Azure Functions supports input bindings, output bindings and trigger bindings in general availability for Azure Database for MySQL

| Action | Type |
|---|---|
| Read data from a database |
|

[Output binding](functions-bindings-azure-mysql-output)[Trigger binding](functions-bindings-azure-mysql-trigger)## Install the extension

The extension NuGet package that you install depends on the C# mode you're using in your function app:

Functions run in an isolated C# worker process. To learn more, see [Guide for running C# Azure functions in an isolated worker process](dotnet-isolated-process-guide).

Add the extension to your project by installing [this NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.MySql/1.0.129/).

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.MySql --version 1.0.129
```


## Install the bundle

The extension for Azure Database for MySQL bindings is part of the v4 [extension bundle](extension-bundles). This bundle is specified in your host.json project file.

### Bundle v4.x

You can use the extension bundle by adding or replacing the following code in your host.json file:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
}
}
```


## Install the bundle

The extension for Azure Database for MySQL bindings is part of the v4 [extension bundle](extension-bundles). This bundle is specified in your host.json project file.

### Bundle v4.x

You can use the extension bundle by adding or replacing the following code in your host.json file:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
}
}
```


## Install the bundle

The extension for Azure Database for MySQL bindings is part of the v4 [extension bundle](extension-bundles). This bundle is specified in your host.json project file.

### Bundle v4.x

You can use the extension bundle by adding or replacing the following code in your host.json file:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
}
}
```


## Update packages

You can use the extension bundle with an update to the pom.xml file in your Java Azure Functions project, as shown in the following snippet:

```
<dependency>
<groupId>com.microsoft.azure.functions</groupId>
<artifactId>azure-functions-java-library-mysql</artifactId>
<version>1.0.2</version>
</dependency>
```


## MySQL connection string

Azure Database for MySQL bindings for Azure Functions have a required property for the connection string. These bindings pass the connection string to the MySql.Data.MySqlClient library and provide support as defined in the [MySqlClient ConnectionString documentation](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html). Notable keywords include:

`server`

: The host on which the server instance is running. The value can be a host name, IPv4 address, or IPv6 address.`uid`

: The MySQL user account to provide for the authentication process.`pwd`

: The password to use for the authentication process.`database`

: The default database for the connection. If no database is specified, the connection has no default database.

## Considerations

- Azure Database for MySQL bindings support version 4.x and later of the Azure Functions runtime.
- You can find source code for the Azure Database for MySQL bindings in
[this GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/src). - These bindings require connectivity to Azure Database for MySQL.
- Output bindings against tables with columns of spatial data types
`GEOMETRY`

,`POINT`

, and`POLYGON`

aren't supported. Data upserts fail.

## Samples

In addition to the samples for C#, Java, JavaScript, PowerShell, and Python available in the [GitHub repository for Azure Database for MySQL bindings](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples), more are available in [Azure Samples](https://github.com/Azure-Samples).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-http-webhook -->

# Azure Functions HTTP triggers and bindings overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions may be invoked via HTTP requests to build serverless APIs and respond to [webhooks](https://en.wikipedia.org/wiki/Webhook).

| Action | Type |
|---|---|
| Run a function from an HTTP request |
|

[Output binding](functions-bindings-http-webhook-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

Add the extension to your project by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Http), version 3.x.

Note

An additional extension package is needed for [ASP.NET Core integration in .NET Isolated](dotnet-isolated-process-guide#aspnet-core-integration)

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

Note

For a reference of host.json in Functions 1.x, see [host.json reference for Azure Functions 1.x](functions-host-json-v1#http).

```
{
"extensions": {
"http": {
"routePrefix": "api",
"maxOutstandingRequests": 200,
"maxConcurrentRequests": 100,
"dynamicThrottlesEnabled": true,
"hsts": {
"isEnabled": true,
"maxAge": "10"
},
"customHeaders": {
"X-Content-Type-Options": "nosniff"
}
}
}
}
```


| Property | Default | Description | ||||||||||
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| customHeaders | none | Allows you to set custom headers in the HTTP response. The previous example adds the `X-Content-Type-Options` header to the response to avoid content type sniffing. This custom header applies to all HTTP triggered functions in the function app. |
||||||||||
| dynamicThrottlesEnabled | true* |
When enabled, this setting causes the request processing pipeline to periodically check system performance counters like `connections/threads/processes/memory/cpu/etc` and if any of those counters are over a built-in high threshold (80%), requests will be rejected with a `429 "Too Busy"` response until the counter(s) return to normal levels.*The default in a Consumption plan is `true` . The default in the Premium and Dedicated plans is `false` . |
||||||||||
| hsts | not enabled | When `isEnabled` is set to `true` , the
`HstsOptions` class |

| Property | Description |
|---|---|
| excludedHosts | A string array of host names for which the HSTS header isn't added. |
| includeSubDomains | Boolean value that indicates whether the includeSubDomain parameter of the Strict-Transport-Security header is enabled. |
| maxAge | String that defines the max-age parameter of the Strict-Transport-Security header. |
| preload | Boolean that indicates whether the preload parameter of the Strict-Transport-Security header is enabled. |

**The default for a Consumption plan is 100. The default for the Premium and Dedicated plans is unbounded (`-1`

).**The default for a Consumption plan is 200. The default for the Premium and Dedicated plans is unbounded (`-1`

).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-sendgrid -->

# Azure Functions SendGrid bindings

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to send email by using [SendGrid](https://sendgrid.com/docs/User_Guide/index.html) bindings in Azure Functions. Azure Functions supports an output binding for SendGrid.

This is reference information for Azure Functions developers. If you're new to Azure Functions, start with the following resources:

C# developer references:


## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

Add the extension to your project by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.SendGrid), version 3.x.

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

## Example

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

We don't currently have an example for using the SendGrid binding in a function app running in an isolated worker process.

The following example shows a SendGrid output binding in a *function.json* file and a [JavaScript function](functions-reference-node) that uses the binding.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"name": "$return",
"type": "sendGrid",
"direction": "out",
"apiKey" : "MySendGridKey",
"to": "{ToEmail}",
"from": "{FromEmail}",
"subject": "SendGrid output bindings"
}
]
}
```


The [configuration](#configuration) section explains these properties.

Here's the JavaScript code:

```
module.exports = function (context, input) {
var message = {
"personalizations": [ { "to": [ { "email": "sample@sample.com" } ] } ],
from: { email: "sender@contoso.com" },
subject: "Azure news",
content: [{
type: 'text/plain',
value: input
}]
};
return message;
};
```


Complete PowerShell examples aren't currently available for SendGrid bindings.

The following example shows an HTTP-triggered function that sends an email using the SendGrid binding. You can provide default values in the binding configuration. For instance, the *from* email address is configured in *function.json*.

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"type": "httpTrigger",
"authLevel": "function",
"direction": "in",
"name": "req",
"methods": ["get", "post"]
},
{
"type": "http",
"direction": "out",
"name": "$return"
},
{
"type": "sendGrid",
"name": "sendGridMessage",
"direction": "out",
"apiKey": "SendGrid_API_Key",
"from": "sender@contoso.com"
}
]
}
```


The following function shows how you can provide custom values for optional properties.

```
import logging
import json
import azure.functions as func
def main(req: func.HttpRequest, sendGridMessage: func.Out[str]) -> func.HttpResponse:
value = "Sent from Azure Functions"
message = {
"personalizations": [ {
"to": [{
"email": "user@contoso.com"
}]}],
"subject": "Azure Functions email with SendGrid",
"content": [{
"type": "text/plain",
"value": value }]}
sendGridMessage.set(json.dumps(message))
return func.HttpResponse(f"Sent")
```


The following example uses the `@SendGridOutput`

annotation from the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime) to send an email using the SendGrid output binding.

```
package com.function;
import java.util.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.*;
public class HttpTriggerSendGrid {
@FunctionName("HttpTriggerSendGrid")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = { HttpMethod.GET, HttpMethod.POST },
authLevel = AuthorizationLevel.FUNCTION)
HttpRequestMessage<Optional<String>> request,
@SendGridOutput(
name = "message",
dataType = "String",
apiKey = "SendGrid_API_Key",
to = "user@contoso.com",
from = "sender@contoso.com",
subject = "Azure Functions email with SendGrid",
text = "Sent from Azure Functions")
OutputBinding<String> message,
final ExecutionContext context) {
final String toAddress = "user@contoso.com";
final String value = "Sent from Azure Functions";
StringBuilder builder = new StringBuilder()
.append("{")
.append("\"personalizations\": [{ \"to\": [{ \"email\": \"%s\"}]}],")
.append("\"content\": [{\"type\": \"text/plain\", \"value\": \"%s\"}]")
.append("}");
final String body = String.format(builder.toString(), toAddress, value);
message.setValue(body);
return request.createResponseBuilder(HttpStatus.OK).body("Sent").build();
}
}
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the output binding. C# script instead uses a function.json configuration file.

In [isolated worker process](dotnet-isolated-process-guide) function apps, the `SendGridOutputAttribute`

supports the following parameters:

| Attribute/annotation property | Description |
|---|---|
ApiKey |
The name of an app setting that contains your API key. If not set, the default app setting name is `AzureWebJobsSendGridApiKey` . |
To |
(Optional) The recipient's email address. |
From |
(Optional) The sender's email address. |
Subject |
(Optional) The subject of the email. |
Text |
(Optional) The email content. |

## Annotations

The [SendGridOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.sendgridoutput) annotation allows you to declaratively configure the SendGrid binding by providing the following configuration values.

## Configuration

The following table lists the binding configuration properties available in the *function.json* file and the `SendGrid`

attribute/annotation.

function.json property |
Description |
|---|---|
type |
Must be set to `sendGrid` . |
direction |
Must be set to `out` . |
name |
The variable name used in function code for the request or request body. This value is `$return` when there's only one return value. |
apiKey |
The name of an app setting that contains your API key. If not set, the default app setting name is AzureWebJobsSendGridApiKey. |
to |
(Optional) The recipient's email address. |
from |
(Optional) The sender's email address. |
subject |
(Optional) The subject of the email. |
text |
(Optional) The email content. |

Optional properties may have default values defined in the binding and either added or overridden programmatically.

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## host.json settings

This section describes the configuration settings available for this binding in version 2.x and later. Settings in the host.json file apply to all functions in a function app instance. For more information about function app configuration settings, see [host.json reference for Azure Functions](functions-host-json).

Note

For a reference of host.json in Functions 1.x, see [host.json reference for Azure Functions 1.x](functions-host-json-v1).

```
{
"version": "2.0",
"extensions": {
"sendGrid": {
"from": "Azure Functions <samples@functions.com>"
}
}
}
```


| Property | Default | Description |
|---|---|---|
from |
n/a | The sender's email address across all functions. |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-deploy-container -->

# Create your first containerized Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you create a function app running in a Linux container and deploy it to Azure Functions.

Deploying your function code to Azure Functions in a container requires [Premium plan](functions-premium-plan) or [Dedicated (App Service) plan](dedicated-plan) hosting. Completing this article incurs costs of a few US dollars in your Azure account, which you can minimize by [cleaning-up resources](#clean-up-resources) when you're done.

Tip

When you need to run your event-driven functions in Azure in the same environment as other microservices, APIs, websites, workflows, or any container hosted programs, consider instead hosting your containerized function apps in Azure Container Apps. Functions provides integrated support for developing, deploying, and managing containerized function apps on Container Apps. For more information, see [Azure Container Apps hosting of Azure Functions](../container-apps/functions-overview).

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
[Storage account](../storage/common/storage-account-create), which is used to maintain state and other information about your functions. - A function app, which provides the environment for executing your function code. A function app maps to your local function project and lets you group functions as a logical unit for easier management, deployment, and sharing of resources.

Important

This article currently shows how to connect to both the Azure Storage account and your container registry by using connection strings and other shared secret credentials. For the best security, you should instead use only a managed identity-based connection to both your storage account and to Azure Container Registry using Microsoft Entra authentication. For more information, see the [Functions developer guide](functions-reference#connections).

Use the following commands to create these items. Both Azure CLI and PowerShell are supported. To create your Azure resources using Azure PowerShell, you also need the [Az PowerShell module](/en-us/powershell/azure/install-az-ps), version 5.9.0 or later.

If you haven't done already, sign in to Azure.

`az login`

The

command signs you into your Azure account.`az login`

Create a resource group named

`AzureFunctionsContainers-rg`

in your chosen region.`az group create --name AzureFunctionsContainers-rg --location <REGION>`

The

command creates a resource group. In the above command, replace`az group create`

`<REGION>`

with a region near you, using an available region code returned from the[az account list-locations](/en-us/cli/azure/account#az-account-list-locations)command.Create a general-purpose storage account in your resource group and region.

`az storage account create --name <STORAGE_NAME> --location <REGION> --resource-group AzureFunctionsContainers-rg --sku Standard_LRS`

The

command creates the storage account.`az storage account create`

In the previous example, replace

`<STORAGE_NAME>`

with a name that is appropriate to you and unique in Azure Storage. Storage names must contain 3 to 24 characters numbers and lowercase letters only.`Standard_LRS`

specifies a general-purpose account[supported by Functions](storage-considerations#storage-account-requirements).Use the command to create a Premium plan for Azure Functions named

`myPremiumPlan`

in the**Elastic Premium 1**pricing tier (`--sku EP1`

), in your`<REGION>`

, and in a Linux container (`--is-linux`

).`az functionapp plan create --resource-group AzureFunctionsContainers-rg --name myPremiumPlan --location <REGION> --number-of-workers 1 --sku EP1 --is-linux`

We use the Premium plan here, which can scale as needed. For more information about hosting, see

[Azure Functions hosting plans comparison](functions-scale). For more information on how to calculate costs, see the[Functions pricing page](https://azure.microsoft.com/pricing/details/functions/).The command also creates an associated Azure Application Insights instance in the same resource group, with which you can monitor your function app and view logs. For more information, see

[Monitor Azure Functions](functions-monitoring). The instance incurs no costs until you activate it.

## Create and configure a function app on Azure with the image

A function app on Azure manages the execution of your functions in your Azure Functions hosting plan. In this section, you use the Azure resources from the previous section to create a function app from an image in a container registry and configure it with a connection string to Azure Storage.

Create a function app using the following command, depending on your container registry:

`az functionapp create --name <APP_NAME> --storage-account <STORAGE_NAME> --resource-group AzureFunctionsContainers-rg --plan myPremiumPlan --image <LOGIN_SERVER>/azurefunctionsimage:v1.0.0 --registry-username <USERNAME> --registry-password <SECURE_PASSWORD>`

In this example, replace

`<STORAGE_NAME>`

with the name you used in the previous section for the storage account. Also, replace`<APP_NAME>`

with a globally unique name appropriate to you and`<DOCKER_ID>`

or`<LOGIN_SERVER>`

with your Docker Hub account ID or Container Registry server, respectively. When you're deploying from a custom container registry, the image name indicates the URL of the registry.When you first create the function app, it pulls the initial image from your Docker Hub. You can also

[Enable continuous deployment](functions-how-to-custom-container#enable-continuous-deployment-to-azure)to Azure from your container registry.Tip

You can use the

in the`DisableColor`

setting*host.json*file to prevent ANSI control characters from being written to the container logs.Use the following command to get the connection string for the storage account you created:

`az storage account show-connection-string --resource-group AzureFunctionsContainers-rg --name <STORAGE_NAME> --query connectionString --output tsv`

The connection string for the storage account is returned by using the

command.`az storage account show-connection-string`

Important

This article currently shows how to connect to the default storage account by using a connection string. For the best security, you should instead create a managed identity-based connection to Azure Storage using Microsoft Entra authentication. For more information, see the

[Functions developer guide](functions-reference#connections).Replace

`<STORAGE_NAME>`

with the name of the storage account you created earlier.Use the following command to add the setting to the function app:

`az functionapp config appsettings set --name <APP_NAME> --resource-group AzureFunctionsContainers-rg --settings AzureWebJobsStorage=<CONNECTION_STRING>`

The

command creates the setting.`az functionapp config appsettings set`

In this command, replace

`<APP_NAME>`

with the name of your function app and`<CONNECTION_STRING>`

with the connection string from the previous step. The connection should be a long encoded string that begins with`DefaultEndpointProtocol=`

.The function can now use this connection string to access the storage account.


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

## Clean up resources

If you want to continue working with Azure Function using the resources you created in this article, you can leave all those resources in place. Because you created a Premium Plan for Azure Functions, you'll incur one or two USD per day in ongoing costs.

To avoid ongoing costs, delete the `AzureFunctionsContainers-rg`

resource group to clean up all the resources in that group:

```
az group delete --name AzureFunctionsContainers-rg
```

---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _scenario-custom-remote-mcp-server_functions-versions.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: scenario-custom-remote-mcp-server.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/scenario-custom-remote-mcp-server -->

# Quickstart: Build a custom remote MCP server using Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you create a custom remote Model Context Protocol (MCP) server from a template project using the Azure Developer CLI (`azd`

). The MCP server uses the Azure Functions MCP server extension to provide tools for AI models, agents, and assistants. After running the project locally and verifying your code using GitHub Copilot, you deploy it to a new serverless function app in Azure Functions that follows current best practices for secure and scalable deployments.

Tip

Functions also enables you to deploy an existing MCP server code project to a Flex Consumption plan app without having to make changes to your code project. For more information, see [Quickstart: Host existing MCP servers on Azure Functions](scenario-host-mcp-server-sdks).

Because the new app runs on the Flex Consumption plan, which follows a *pay-for-what-you-use* billing model, completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

Important

While [creating custom MCP servers](functions-bindings-mcp) is supported for all Functions languages, this quickstart scenario currently only has examples for C#, Python, and TypeScript. To complete this quickstart, select one of these supported languages at the top of the article.

This article supports version 4 of the Node.js programming model for Azure Functions.

This article supports version 2 of the Python programming model for Azure Functions.

## Prerequisites

[Java 17 Developer Kit](/en-us/azure/developer/java/fundamentals/java-support-on-azure)- If you use another
[supported version of Java](supported-languages?pivots=programming-language-java#languages-by-runtime-version), you must update the project's pom.xml file. - Set the
`JAVA_HOME`

environment variable to the install location of the correct version of the Java Development Kit (JDK).

- If you use another
[Apache Maven 3.8.x](https://maven.apache.org)

[Visual Studio Code](https://code.visualstudio.com/)with these extensions:[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions). This extension requires[Azure Functions Core Tools](functions-run-local)and attempts to install it when not available.

[Azure CLI](/en-us/cli/azure/install-azure-cli). You can also run Azure CLI commands in[Azure Cloud Shell](../cloud-shell/overview).An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Initialize the project

Use the `azd init`

command to create a local Azure Functions code project from a template.

- In Visual Studio Code, open a folder or workspace where you want to create your project.

In the Terminal, run this

`azd init`

command:`azd init --template remote-mcp-functions-dotnet -e mcpserver-dotnet`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/remote-mcp-functions-dotnet)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also used in the name of the resource group you create in Azure.

In your local terminal or command prompt, run this

`azd init`

command:`azd init --template remote-mcp-functions-java -e mcpserver-java`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/remote-mcp-functions-java)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also used in names of the resources you create in Azure.

In your local terminal or command prompt, run this

`azd init`

command:`azd init --template remote-mcp-functions-typescript -e mcpserver-ts`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/remote-mcp-functions-typescript)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also used in names of the resources you create in Azure.

In your local terminal or command prompt, run this

`azd init`

command:`azd init --template remote-mcp-functions-python -e mcpserver-python`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/remote-mcp-functions-python)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also used in names of the resources you create in Azure.

## Start the storage emulator

Use the Azurite emulator to simulate an Azure Storage account connection when running your code project locally.

If you haven't already,

[install Azurite](/en-us/azure/storage/common/storage-use-azurite#install-azurite).Press

`F1`. In the command palette, search for and run the command`Azurite: Start`

to start the local storage emulator.

## Run your MCP server locally

Visual Studio Code integrates with [Azure Functions Core tools](functions-run-local) to let you run this project on your local development computer by using the Azurite emulator.

To start the function locally, press

`F5`or the**Run and Debug**icon in the left-hand side Activity bar. The**Terminal**panel displays the output from Core Tools. Your app starts in the**Terminal**panel, and you can see the name of the functions that are running locally.Make a note of the local MCP server endpoint (like

`http://localhost:7071/runtime/webhooks/mcp`

), which you use to configure GitHub Copilot in Visual Studio Code.

## Verify using GitHub Copilot

To verify your code, add the running project as an MCP server for GitHub Copilot in Visual Studio Code:

Press

`F1`. In the command palette, search for and run**MCP: Add Server**.Choose

**HTTP (Server-Sent Events)**for the transport type.Enter the URL of the MCP endpoint you copied in the previous step.

Use the generated

**Server ID**and select**Workspace**to save the MCP server connection to your Workspace settings.Open the command palette and run

**MCP: List Servers**and verify that the server you added is listed and running.In Copilot chat, select

**Agent**mode and run this prompt:`Say Hello`

When prompted to run the tool, select

**Allow in this Workspace**so you don't have to keep granting permission. The prompt runs and returns a`Hello World`

response and function execution information is written to the logs.Now, select some code in one of your project files and run this prompt:

`Save this snippet as snippet1`

Copilot stores the snippet and responds to your request with information about how to retrieve the snippet by using the

`getSnippets`

tool. Again, you can review the function execution in the logs and verify that the`saveSnippets`

function ran.In Copilot chat, run this prompt:

`Retrieve snippet1 and apply to NewFile`

Copilot retrieves the snippets, adds it to a file called

`NewFile`

, and does whatever else it thinks is needed to make the code snippet work in your project. The Functions logs show that the`getSnippets`

endpoint was called.When you're done testing, press Ctrl+C to stop the Functions host.


## Review the code (optional)

You can review the code that defines the MCP server tools:

The function code for the MCP server tools is defined in the `src`

folder. The `McpToolTrigger`

attribute exposes the functions as MCP Server tools:

```
[Function(nameof(SayHello))]
public string SayHello(
[McpToolTrigger(HelloToolName, HelloToolDescription)] ToolInvocationContext context
)
{
logger.LogInformation("C# MCP tool trigger function processed a request.");
return "Hello I am MCP Tool!";
}
```


```
[Function(nameof(GetSnippet))]
public object GetSnippet(
[McpToolTrigger(GetSnippetToolName, GetSnippetToolDescription)]
ToolInvocationContext context,
[BlobInput(BlobPath)] string snippetContent
)
{
return snippetContent;
}
[Function(nameof(SaveSnippet))]
[BlobOutput(BlobPath)]
public string SaveSnippet(
[McpToolTrigger(SaveSnippetToolName, SaveSnippetToolDescription)]
ToolInvocationContext context,
[McpToolProperty(SnippetNamePropertyName, SnippetNamePropertyDescription, true)]
string name,
[McpToolProperty(SnippetPropertyName, SnippetPropertyDescription, true)]
string snippet
)
{
return snippet;
}
}
```


You can view the complete project template in the [Azure Functions .NET MCP Server](https://github.com/Azure-Samples/remote-mcp-functions-dotnet) GitHub repository.

The function code for the MCP server tools is defined in the `src/main/java/com/function/`

folder. The `@McpToolTrigger`

annotation exposes the functions as MCP Server tools:

```
description = "The messages to be logged.",
isRequired = true,
isArray = true)
String messages,
final ExecutionContext functionExecutionContext
) {
functionExecutionContext.getLogger().info("Hello, World!");
functionExecutionContext.getLogger().info("Tool Name: " + mcpToolInvocationContext.getName());
functionExecutionContext.getLogger().info("Transport Type: " + mcpToolInvocationContext.getTransportType());
// Handle different transport types
if (mcpToolInvocationContext.isHttpStreamable()) {
functionExecutionContext.getLogger().info("Session ID: " + mcpToolInvocationContext.getSessionid());
} else if (mcpToolInvocationContext.isHttpSse()) {
if (mcpToolInvocationContext.getClientinfo() != null) {
functionExecutionContext.getLogger().info("Client: " +
mcpToolInvocationContext.getClientinfo().get("name").getAsString() + " v" +
```


```
// Write the snippet content to the output blob
outputBlob.setValue(snippet);
return "Successfully saved snippet '" + snippetName + "' with " + snippet.length() + " characters.";
}
/**
* Azure Function that handles retrieving a text snippet from Azure Blob Storage.
* <p>
* The function is triggered by an MCP Tool Trigger. The snippet name is provided
* as an MCP tool property, and the snippet content is read from the blob at the
* path derived from the snippet name.
*
* @param mcpToolInvocationContext The JSON input from the MCP tool trigger.
* @param snippetName The name of the snippet to retrieve, provided as an MCP tool property.
* @param inputBlob The Azure Blob input binding that fetches the snippet content.
* @param functionExecutionContext The execution context for logging.
*/
@FunctionName("GetSnippets")
@StorageAccount("AzureWebJobsStorage")
public String getSnippet(
@McpToolTrigger(
name = "getSnippets",
description = "Gets a text snippet from your snippets collection.")
String mcpToolInvocationContext,
@McpToolProperty(
name = SNIPPET_NAME_PROPERTY_NAME,
propertyType = "string",
description = "The name of the snippet.",
isRequired = true)
String snippetName,
@BlobInput(name = "inputBlob", path = BLOB_PATH)
String inputBlob,
final ExecutionContext functionExecutionContext
) {
// Log the entire incoming JSON for debugging
functionExecutionContext.getLogger().info(mcpToolInvocationContext);
// Log the snippet name and the fetched snippet content from the blob
```


You can view the complete project template in the [Azure Functions Java MCP Server](https://github.com/Azure-Samples/remote-mcp-functions-java) GitHub repository.

The function code for the MCP server tools is defined in the `src/function_app.py`

file. The MCP function annotations expose these functions as MCP Server tools:

```
tool_properties_save_snippets_json = json.dumps([prop.to_dict() for prop in tool_properties_save_snippets_object])
tool_properties_get_snippets_json = json.dumps([prop.to_dict() for prop in tool_properties_get_snippets_object])
@app.generic_trigger(
arg_name="context",
type="mcpToolTrigger",
toolName="hello_mcp",
description="Hello world.",
toolProperties="[]",
)
def hello_mcp(context) -> None:
"""
```


```
@app.generic_trigger(
arg_name="context",
type="mcpToolTrigger",
toolName="save_snippet",
description="Save a snippet with a name.",
toolProperties=tool_properties_save_snippets_json,
)
@app.generic_output_binding(arg_name="file", type="blob", connection="AzureWebJobsStorage", path=_BLOB_PATH)
def save_snippet(file: func.Out[str], context) -> str:
content = json.loads(context)
snippet_name_from_args = content["arguments"][_SNIPPET_NAME_PROPERTY_NAME]
snippet_content_from_args = content["arguments"][_SNIPPET_PROPERTY_NAME]
if not snippet_name_from_args:
return "No snippet name provided"
if not snippet_content_from_args:
return "No snippet content provided"
file.set(snippet_content_from_args)
logging.info(f"Saved snippet: {snippet_content_from_args}")
return f"Snippet '{snippet_content_from_args}' saved successfully"
```


You can view the complete project template in the [Azure Functions Python MCP Server](https://github.com/Azure-Samples/remote-mcp-functions-python) GitHub repository.

The function code for the MCP server tools is defined in the `src`

folder. The MCP function registration exposes these functions as MCP Server tools:

```
export async function mcpToolHello(_toolArguments:unknown, context: InvocationContext): Promise<string> {
console.log(_toolArguments);
// Get name from the tool arguments
const mcptoolargs = context.triggerMetadata.mcptoolargs as {
name?: string;
};
const name = mcptoolargs?.name;
console.info(`Hello ${name}, I am MCP Tool!`);
return `Hello ${name || 'World'}, I am MCP Tool!`;
}
// Register the hello tool
app.mcpTool('hello', {
toolName: 'hello',
description: 'Simple hello world MCP Tool that responses with a hello message.',
toolProperties:{
name: arg.string().describe('Required property to identify the caller.').optional()
},
handler: mcpToolHello
});
```


```
// SaveSnippet function - saves a snippet with a name
export async function saveSnippet(
_toolArguments: unknown,
context: InvocationContext
): Promise<string> {
console.info("Saving snippet");
// Get snippet name and content from the tool arguments
const mcptoolargs = context.triggerMetadata.mcptoolargs as {
snippetname?: string;
snippet?: string;
};
const snippetName = mcptoolargs?.snippetname;
const snippet = mcptoolargs?.snippet;
if (!snippetName) {
return "No snippet name provided";
}
if (!snippet) {
return "No snippet content provided";
}
// Save the snippet to blob storage using the output binding
context.extraOutputs.set(blobOutputBinding, snippet);
console.info(`Saved snippet: ${snippetName}`);
return snippet;
}
```


You can view the complete project template in the [Azure Functions TypeScript MCP Server](https://github.com/Azure-Samples/remote-mcp-functions-typescript) GitHub repository.

After verifying the MCP server tools locally, you can publish the project to Azure.

## Deploy to Azure

This project is configured to use the `azd up`

command to deploy this project to a new function app in a Flex Consumption plan in Azure. The project includes a set of Bicep files that `azd`

uses to create a secure deployment to a Flex consumption plan that follows best practices.

In Visual Studio Code, press

`F1`to open the command palette. Search for and run the command`Azure Developer CLI (azd): Package, Provison and Deploy (up)`

. Then, sign in by using your Azure account.If you're not already signed in, authenticate with your Azure account.

When prompted, provide these required deployment parameters:

Parameter Description *Azure subscription*Subscription in which your resources are created. *Azure location*Azure region in which to create the resource group that contains the new Azure resources. Only regions that currently support the Flex Consumption plan are shown. After the command completes successfully, you see links to the resources you created.


## Connect to your remote MCP server

Your MCP server is now running in Azure. When you access the tools, you need to include a system key in your request. This key provides a degree of access control for clients accessing your remote MCP server. After you get this key, you can connect GitHub Copilot to your remote server.

Run this script that uses

`azd`

and the Azure CLI to print out both the MCP server URL and the system key (`mcp_extension`

) required to access the tools:`eval $(azd env get-values --output dotenv) MCP_EXTENSION_KEY=$(az functionapp keys list --resource-group $AZURE_RESOURCE_GROUP \ --name $AZURE_FUNCTION_NAME --query "systemKeys.mcp_extension" -o tsv) printf "MCP Server URL: %s\n" "https://$SERVICE_API_NAME.azurewebsites.net/runtime/webhooks/mcp" printf "MCP Server key: %s\n" "$MCP_EXTENSION_KEY"`

In Visual Studio Code, press

`F1`to open the command palette, search for and run the command`MCP: Open Workspace Folder MCP Configuraton`

, which opens the`mcp.json`

configuration file.In the

`mcp.json`

configuration, find the named MCP server you added earlier, change the`url`

value to your remote MCP server URL, and add a`headers.x-functions-key`

element, which contains your copied MCP server access key, as in this example:`{ "servers": { "remote-mcp-function": { "type": "http", "url": "https://contoso.azurewebsites.net/runtime/webhooks/mcp", "headers": { "x-functions-key": "A1bC2dE3fH4iJ5kL6mN7oP8qR9sT0u..." } } } }`

Select the

**Start**button above your server name in the open`mcp.json`

to restart the remote MCP server, this time using your deployed app.

## Verify your deployment

You can now have GitHub Copilot use your remote MCP tools just as you did locally, but now the code runs securely in Azure. Replay the same commands you used earlier to ensure everything works correctly.

## Clean up resources

When you're done working with your MCP server and related resources, use this command to delete the function app and its related resources from Azure to avoid incurring further costs:

```
azd down --no-prompt
```


Note

The `--no-prompt`

option instructs `azd`

to delete your resource group without confirmation from you. This command doesn't affect your local code project.


---

<!-- DOCUMENTO FUSIONADO: functions-versions.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-versions -->

# Azure Functions runtime versions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Azure Functions currently supports two versions of the runtime host. The following table details the currently supported runtime versions, their support level, and when they should be used:]

| Version | Support level | Description |
|---|---|---|
| 4.x | GA | Check out Recommended runtime version for functions in all languages.
|
| 1.x | GA (
|

**Support will end for version 1.x on September 14, 2026.**We highly recommend you[migrate your apps to version 4.x](migrate-version-1-version-4?pivots=programming-language-csharp), which supports .NET Framework 4.8, .NET 8, .NET 9, and .NET 10 Preview.Important

As of December 13, 2022, function apps running on versions 2.x and 3.x of the Azure Functions runtime reached the end of extended support. For more information, see [Retired versions](#retired-versions).

This article details some of the differences between supported versions, how you can create each version, and how to change the version on which your functions run.

## Levels of support

There are two levels of support:

**Generally available (GA)**- Fully supported and approved for production use.**Preview**- Not yet supported, but expected to reach GA status in the future.

## Languages

All functions in a function app must share the same language. You choose the language of functions in your function app when you create the app. The language of your function app is maintained in the [FUNCTIONS_WORKER_RUNTIME](functions-app-settings#functions_worker_runtime) setting, and can't be changed when there are existing functions.

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

For information about the language versions of previously supported versions of the Functions runtime, see [Retired runtime versions](language-support-policy#language-support-related-resources).

## Run on a specific version

The version of the Functions runtime used by published apps in Azure is dictated by the [ FUNCTIONS_EXTENSION_VERSION](functions-app-settings#functions_extension_version) application setting. In some cases and for certain languages, other settings can apply.

By default, function apps created in the Azure portal, by the Azure CLI, or from Visual Studio tools are set to version 4.x. You can modify this version if needed. You can only downgrade the runtime version to 1.x after you create your function app but before you add any functions. Updating to a later major version is allowed even with apps that have existing functions.

### Migrating existing function apps

When your app has existing functions, you must take precautions before moving to a later major runtime version. The following articles detail breaking changes between major versions, including language-specific breaking changes. They also provide you with step-by-step instructions for a successful migration of your existing function app.

### Changing the version of apps in Azure

The following major runtime version values are used:

| Value | Runtime target |
|---|---|
`~4` |
4.x |
`~1` |
1.x |

Important

Don't arbitrarily change this app setting, because other app setting changes and changes to your function code might be required. For existing function apps, follow the [migration instructions](#migrating-existing-function-apps).

### Pinning to a specific minor version

To resolve issues that your function app could have when running on the latest major version, you must temporarily pin your app to a specific minor version. Pinning gives you time to get your app running correctly on the latest major version. The way that you pin to a minor version differs between Windows and Linux. To learn more, see [How to target Azure Functions runtime versions](set-runtime-version).

Older minor versions are periodically removed from Functions. For the latest news about Azure Functions releases, including the removal of specific older minor versions, monitor [Azure App Service announcements](https://github.com/Azure/app-service-announcements/issues).

## Minimum extension versions

There's technically not a correlation between binding extension versions and the Functions runtime version. However, starting with version 4.x the Functions runtime enforces a minimum version for all trigger and binding extensions.

If you receive a warning about a package not meeting a minimum required version, you should update that NuGet package to the minimum version as you normally would. The minimum version requirements for extensions used in Functions v4.x can be found in [the linked configuration file](https://github.com/Azure/azure-functions-host/blob/dev/src/WebJobs.Script/extensionrequirements.json).

For C# script, update the extension bundle reference in the *host.json* as follows:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.0.0, 5.0.0)"
}
}
```


There's technically not a correlation between extension bundle versions and the Functions runtime version. However, starting with version 4.x the Functions runtime enforces a minimum version for extension bundles.

If you receive a warning about your extension bundle version not meeting a minimum required version, update your existing extension bundle reference in the *host.json* as follows:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.0.0, 5.0.0)"
}
}
```


To learn more about extension bundles, see [Extension bundles](extension-bundles).

## Retired versions

Important

[Support will end for version 1.x of the Azure Functions runtime on September 14, 2026](https://aka.ms/azure-functions-retirements/hostv1). We highly recommend that you [migrate your apps to version 4.x](migrate-version-1-version-4) for full support.

These versions of the Functions runtime reached the end of extended support on December 13, 2022.

| Version | Current support level | Previous support level |
|---|---|---|
| 3.x | Out of support | GA |
| 2.x | Out of support | GA |

As soon as possible, you should migrate your apps to version 4.x to obtain full support. For a complete set of language-specific migration instructions, see [Migrate apps to Azure Functions version 4.x](migrate-version-3-version-4).

Apps using versions 2.x and 3.x can still be created and deployed from your CI/CD DevOps pipeline, and all existing apps continue to run without breaking changes. However, your apps aren't eligible for new features, security patches, and performance optimizations. You can only get related service support after you upgrade your apps to version 4.x.

Versions 2.x and 3.x are no longer supported due to the end of support for .NET Core 3.1, which was a core dependency. This requirement affects all [languages supported by Azure Functions](supported-languages).

## Locally developed application versions

You can make the following updates to function apps to locally change the targeted versions.

### Visual Studio runtime versions

In Visual Studio, you select the runtime version when you create a project. Azure Functions tools for Visual Studio supports the two major runtime versions. The correct version is used when debugging and publishing based on project settings. The version settings are defined in the *.csproj* file in the following properties:

```
<TargetFramework>net8.0</TargetFramework>
<AzureFunctionsVersion>v4</AzureFunctionsVersion>
```


If you're using the [isolated worker model](dotnet-isolated-process-guide), you can choose, `net9.0`

, `net8.0`

, or `net48`

as the target framework. You can also choose to use [preview support](dotnet-isolated-process-guide#preview-net-versions) for `net10.0`

. If you're using the [in-process model](functions-dotnet-class-library), you can choose `net8.0`

or `net6.0`

, and you must include the `Microsoft.NET.Sdk.Functions`

extension set to at least `4.4.0`

. .NET 10 is not supported by the in-process model; if you are on the in-process model and wish to use .NET 10, [migrate your app to the isolated worker model](migrate-dotnet-to-isolated-model).

.NET 6 was previously supported on the isolated worker model and the in-process model, but it reached the end of official support on [November 12, 2024](https://dotnet.microsoft.com/platform/support/policy/dotnet-core#lifecycle).
.NET 7 was previously supported on the isolated worker model but reached the end of official support on [May 14, 2024](https://dotnet.microsoft.com/platform/support/policy/dotnet-core#lifecycle).

### Visual Studio Code and Azure Functions Core Tools

[Azure Functions Core Tools](functions-run-local) is used for command-line development and also by the [Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions) for Visual Studio Code. For more information, see [Install the Azure Functions Core Tools](functions-run-local#install-the-azure-functions-core-tools).

For Visual Studio Code development, you might also need to update the user setting for the `azureFunctions.projectRuntime`

to match the version of the tools installed. This setting also updates the templates and languages used during function app creation.

## Bindings

Starting with version 2.x, the runtime uses a new [binding extensibility model](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) that offers these advantages:

Support for non-Microsoft binding extensions.

Decoupling of runtime and bindings. This change allows binding extensions to be versioned and released independently. You can, for example, opt to upgrade to a version of an extension that relies on a newer version of an underlying SDK.

A lighter execution environment, where only the bindings in use are known and loaded by the runtime.


Except for HTTP and timer triggers, all bindings must be explicitly added to the function app project, or registered in the portal. For more information, see [Azure Functions binding expression patterns](functions-bindings-expressions-patterns).

This table shows the bindings that are supported in the major versions of the Azure Functions runtime:

| Type | 4.x1 |
1.x2 |
Trigger | Input | Output |
|---|---|---|---|---|---|
|

[Azure Cosmos DB](functions-bindings-cosmosdb-v2)[Azure Data Explorer](functions-bindings-azure-data-explorer)[Azure SQL](functions-bindings-azure-sql)[Dapr](functions-bindings-dapr)4[Event Grid](functions-bindings-event-grid)[Event Hubs](functions-bindings-event-hubs)[HTTP and webhooks](functions-bindings-http-webhook)[IoT Hub](functions-bindings-event-iot)[Kafka](functions-bindings-kafka)3[Mobile Apps](functions-bindings-mobile-apps)[Model Context Protocol](functions-bindings-mcp)[Notification Hubs](functions-bindings-notification-hubs)[Queue Storage](functions-bindings-storage-queue)[Redis](functions-bindings-cache)[RabbitMQ](functions-bindings-rabbitmq)3[SendGrid](functions-bindings-sendgrid)[Service Bus](functions-bindings-service-bus)[Azure SignalR Service](functions-bindings-signalr-service)[Table Storage](functions-bindings-storage-table)[Timer](functions-bindings-timer)[Twilio](functions-bindings-twilio)- Register all bindings except HTTP and timer. See
[Register Azure Functions binding extensions](functions-bindings-register). This step isn't required when using version 1.x of the Functions runtime. [Support ends for version 1.x of the Azure Functions runtime on September 14, 2026](https://aka.ms/azure-functions-retirements/hostv1).[Migrate your apps to version 4.x](migrate-version-1-version-4)for full support.- Triggers aren't supported in the Consumption plan. This binding type requires
[runtime-driven triggers](functions-networking-options#elastic-premium-plan-with-virtual-network-triggers). - This binding type is supported in Kubernetes, Azure IoT Edge, and other self-hosted modes only.

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

## Related content

For more information, see the following resources:


---

<!-- DOCUMENTO FUSIONADO: __python-memory-profiler-reference__dedicated-plan_functions-bindings-azure-data_243f17.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _python-memory-profiler-reference__dedicated-plan_functions-bindings-azure-data-_7022ea.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: python-memory-profiler-reference.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/python-memory-profiler-reference -->

# Profile Python apps memory usage in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

During development or after deploying your local Python function app project to Azure, it's a good practice to analyze for potential memory bottlenecks in your functions. Such bottlenecks can decrease the performance of your functions and lead to errors. The following instructions show you how to use the [memory-profiler](https://pypi.org/project/memory-profiler) Python package, which provides line-by-line memory consumption analysis of your functions as they execute.

Note

Memory profiling is intended only for memory footprint analysis in development environments. Please do not apply the memory profiler on production function apps.

## Prerequisites

Before you start developing a Python function app, you must meet these requirements:

[Python 3.7 or above](https://www.python.org/downloads). To check the full list of supported Python versions in Azure Functions, see the[Python developer guide](functions-reference-python#supported-python-versions).The

[Azure Functions Core Tools](functions-run-local#v2), version 4.x or greater. Check your version with`func --version`

. To learn about updating, see[Azure Functions Core Tools on GitHub](https://github.com/Azure/azure-functions-core-tools).[Visual Studio Code](https://code.visualstudio.com/)installed on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).An active Azure subscription.


If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Memory profiling process

In your requirements.txt, add

`memory-profiler`

to ensure the package is bundled with your deployment. If you're developing on your local machine, you may want to[activate a Python virtual environment](how-to-create-function-azure-cli?pivots=programming-language-python#create-venv)and do a package resolution by`pip install -r requirements.txt`

.In your function script (for example,

*__init__.py*for the Python v1 programming model and*function_app.py*for the v2 model), add the following lines above the`main()`

function. These lines ensure the root logger reports the child logger names, so that the memory profiling logs are distinguishable by the prefix`memory_profiler_logs`

.`import logging import memory_profiler root_logger = logging.getLogger() root_logger.handlers[0].setFormatter(logging.Formatter("%(name)s: %(message)s")) profiler_logstream = memory_profiler.LogFile('memory_profiler_logs', True)`

Apply the following decorator above any functions that need memory profiling. The decorator doesn't work directly on the trigger entrypoint

`main()`

method. You need to create subfunctions and decorate them. Also, due to a memory-profiler known issue, when applying to an async coroutine, the coroutine return value is always`None`

.`@memory_profiler.profile(stream=profiler_logstream)`

Test the memory profiler on your local machine by using Azure Functions Core Tools command

`func host start`

. When you invoke the functions, they should generate a memory usage report. The report contains file name, line of code, memory usage, memory increment, and the line content in it.To check the memory profiling logs on an existing function app instance in Azure, you can query the memory profiling logs for recent invocations with

[Kusto](/en-us/azure/azure-monitor/logs/log-query-overview)queries in Application Insights, Logs.`traces | where timestamp > ago(1d) | where message startswith_cs "memory_profiler_logs:" | parse message with "memory_profiler_logs: " LineNumber " " TotalMem_MiB " " IncreMem_MiB " " Occurrences " " Contents | union ( traces | where timestamp > ago(1d) | where message startswith_cs "memory_profiler_logs: Filename: " | parse message with "memory_profiler_logs: Filename: " FileName | project timestamp, FileName, itemId ) | project timestamp, LineNumber=iff(FileName != "", FileName, LineNumber), TotalMem_MiB, IncreMem_MiB, Occurrences, Contents, RequestId=itemId | order by timestamp asc`


## Example

Here's an example of performing memory profiling on an asynchronous and a synchronous HTTP trigger, named "HttpTriggerAsync" and "HttpTriggerSync" respectively. We'll build a Python function app that simply sends out GET requests to the Microsoft's home page.

### Create a Python function app

A Python function app should follow Azure Functions specified [folder structure](functions-reference-python#folder-structure). To scaffold the project, we recommend using the Azure Functions Core Tools by running the following commands:

```
func init PythonMemoryProfilingDemo --python
cd PythonMemoryProfilingDemo
func new -l python -t HttpTrigger -n HttpTriggerAsync -a anonymous
func new -l python -t HttpTrigger -n HttpTriggerSync -a anonymous
```


### Update file contents

The *requirements.txt* defines the packages that are used in our project. Besides the Azure Functions SDK and memory-profiler, we introduce `aiohttp`

for asynchronous HTTP requests and `requests`

for synchronous HTTP calls.

```
# requirements.txt
azure-functions
memory-profiler
aiohttp
requests
```


Create the asynchronous HTTP trigger.

Replace the code in the asynchronous HTTP trigger *HttpTriggerAsync/__init__.py* with the following code, which configures the memory profiler, root logger format, and logger streaming binding.

```
# HttpTriggerAsync/__init__.py
import azure.functions as func
import aiohttp
import logging
import memory_profiler
# Update root logger's format to include the logger name. Ensure logs generated
# from memory profiler can be filtered by "memory_profiler_logs" prefix.
root_logger = logging.getLogger()
root_logger.handlers[0].setFormatter(logging.Formatter("%(name)s: %(message)s"))
profiler_logstream = memory_profiler.LogFile('memory_profiler_logs', True)
async def main(req: func.HttpRequest) -> func.HttpResponse:
await get_microsoft_page_async('https://microsoft.com')
return func.HttpResponse(
f"Microsoft page loaded.",
status_code=200
)
@memory_profiler.profile(stream=profiler_logstream)
async def get_microsoft_page_async(url: str):
async with aiohttp.ClientSession() as client:
async with client.get(url) as response:
await response.text()
# @memory_profiler.profile does not support return for coroutines.
# All returns become None in the parent functions.
# GitHub Issue: https://github.com/pythonprofilers/memory_profiler/issues/289
```


Create the synchronous HTTP trigger.

Replace the code in the asynchronous HTTP trigger *HttpTriggerSync/__init__.py* with the following code.

```
# HttpTriggerSync/__init__.py
import azure.functions as func
import requests
import logging
import memory_profiler
# Update root logger's format to include the logger name. Ensure logs generated
# from memory profiler can be filtered by "memory_profiler_logs" prefix.
root_logger = logging.getLogger()
root_logger.handlers[0].setFormatter(logging.Formatter("%(name)s: %(message)s"))
profiler_logstream = memory_profiler.LogFile('memory_profiler_logs', True)
def main(req: func.HttpRequest) -> func.HttpResponse:
content = profile_get_request('https://microsoft.com')
return func.HttpResponse(
f"Microsoft page response size: {len(content)}",
status_code=200
)
@memory_profiler.profile(stream=profiler_logstream)
def profile_get_request(url: str):
response = requests.get(url)
return response.content
```


### Profile Python function app in local development environment

After you make the above changes, there are a few more steps to initialize a Python virtual environment for Azure Functions runtime.

Open a Windows PowerShell or any Linux shell as you prefer.

Create a Python virtual environment by

`py -m venv .venv`

in Windows, or`python3 -m venv .venv`

in Linux.Activate the Python virtual environment with

`.venv\Scripts\Activate.ps1`

in Windows PowerShell or`source .venv/bin/activate`

in Linux shell.Restore the Python dependencies with

`pip install -r requirements.txt`

Start the Azure Functions runtime locally with Azure Functions Core Tools

`func host start`

Send a GET request to

`https://localhost:7071/api/HttpTriggerAsync`

or`https://localhost:7071/api/HttpTriggerSync`

.It should show a memory profiling report similar to the following section in Azure Functions Core Tools.

`Filename: <ProjectRoot>\HttpTriggerAsync\__init__.py Line # Mem usage Increment Occurrences Line Contents ============================================================ 19 45.1 MiB 45.1 MiB 1 @memory_profiler.profile 20 async def get_microsoft_page_async(url: str): 21 45.1 MiB 0.0 MiB 1 async with aiohttp.ClientSession() as client: 22 46.6 MiB 1.5 MiB 10 async with client.get(url) as response: 23 47.6 MiB 1.0 MiB 4 await response.text()`


## Next steps

For more information about Azure Functions Python development, see the following resources:


---

<!-- DOCUMENTO FUSIONADO: _dedicated-plan_functions-bindings-azure-data-explorer.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: dedicated-plan.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/dedicated-plan -->

# Dedicated hosting plans for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article is about hosting your function app with dedicated resources in an App Service plan, including in an App Service Environment (ASE). For other hosting options, see the [hosting plan article](functions-scale).

An App Service plan defines a set of dedicated compute resources for an app to run. These dedicated compute resources are analogous to the [ server farm](https://wikipedia.org/wiki/Server_farm) in conventional hosting. One or more function apps can be configured to run on the same computing resources (App Service plan) as other App Service apps, such as web apps. The dedicated App Service plans supported for function app hosting include Basic, Standard, Premium, and Isolated SKUs. For details about how the App Service plan works, see the

[Azure App Service plans in-depth overview](../app-service/overview-hosting-plans).

Important

Free and Shared tier App Service plans aren't supported by Azure Functions. For a lower-cost option hosting your function executions, you should instead consider the [Consumption plan](consumption-plan) or the [Flex Consumption plan](flex-consumption-plan), where you are billed based on function executions.

Consider a dedicated App Service plan in the following situations:

- You have existing, underutilized VMs that are already running other App Service instances.
- You want to provide a custom image on which to run your functions.

## Billing

You pay for function apps in an App Service Plan as you would for other App Service resources. This differs from Azure Functions [Consumption plan](consumption-plan) or [Premium plan](functions-premium-plan) hosting, which have consumption-based cost components. You are billed only for the plan, regardless of how many function apps or web apps run in the plan. To learn more, see the [App Service pricing page](https://azure.microsoft.com/pricing/details/app-service/windows/).

## Always On

When you run your app on an App Service plan, you should enable the **Always on** setting so that your function app runs correctly. On an App Service plan, the Functions runtime goes idle after a few minutes of inactivity. The **Always on** setting is available only on an App Service plan. In other plans, the platform activates function apps automatically. If you choose not to enable **Always on**, you can reactivate an idled app in these ways:

- Send a request to an HTTP trigger endpoint or any other endpoint on the app. Even a failed request should wake up your app.
- Access your app in the
[Azure portal](https://portal.azure.com).

Even with **Always on** enabled, the execution timeout for individual functions is controlled by the `functionTimeout`

setting in the [host.json](functions-host-json#functiontimeout) project file.

## Scaling

Using an App Service plan, you can manually scale out by adding more VM instances. You can also enable autoscale, though autoscale will be slower than the elastic scale of the Premium plan. For more information, see [Scale instance count manually or automatically](/en-us/azure/azure-monitor/autoscale/autoscale-get-started?toc=%2fazure%2fapp-service%2ftoc.json). You can also scale up by choosing a different App Service plan. For more information, see [Scale up an app in Azure](../app-service/manage-scale-up).

Note

When running JavaScript (Node.js) functions on an App Service plan, you should choose a plan that has fewer vCPUs. For more information, see [Choose single-core App Service plans](functions-reference-node#choose-single-vcpu-app-service-plans).

## App Service Environments

Running in an App Service Environment (ASE) lets you fully isolate your functions and take advantage of higher numbers of instances than an App Service Plan. To get started, see [Introduction to the App Service Environments](../app-service/environment/overview).

If you just want to run your function app in a virtual network, you can do this using the [Premium plan](functions-premium-plan). To learn more, see [Establish Azure Functions private site access](functions-create-private-site-access).


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-azure-data-explorer.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-data-explorer -->

# Azure Data Explorer bindings for Azure Functions overview (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This set of articles explains how to work with [Azure Data Explorer](/en-us/azure/data-explorer/index) bindings in Azure Functions. Azure Functions supports input bindings and output bindings for Azure Data Explorer clusters.

| Action | Type |
|---|---|
| Read data from a database |
|

[Output binding](functions-bindings-azure-data-explorer-output)## Install the extension

The extension NuGet package you install depends on the C# mode you're using in your function app.

Functions run in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

Add the extension to your project by installing [this NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Kusto/).

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Kusto --prerelease
```


## Install the bundle

Azure Data Explorer bindings extension is part of a preview [extension bundle](extension-bundles), which is specified in your *host.json* project file.

You can add the preview extension bundle by adding or replacing the following code in your *host.json* file:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle.Preview",
"version": "[4.*, 5.0.0)"
}
}
```


## Functions runtime

Note

Python language support for the Azure Data Explorer bindings extension is available starting with v4.6.0 or later of the [Functions runtime](set-runtime-version#manual-version-updates-on-linux). You might need to update your installation of Azure Functions [Core Tools](functions-run-local) for local development.

## Install the bundle

The Azure Data Explorer bindings extension is part of a preview [extension bundle](extension-bundles), which is specified in your *host.json* project file.

You can add the preview extension bundle by adding or replacing the following code in your *host.json* file:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle.Preview",
"version": "[4.*, 5.0.0)"
}
}
```


## Install the bundle

Azure Data Explorer bindings extension is part of a preview [extension bundle](extension-bundles), which is specified in your *host.json* project file.

You can add the preview extension bundle by adding or replacing the following code in your *host.json* file:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle.Preview",
"version": "[4.*, 5.0.0)"
}
}
```


## Update packages

Add the Java library for Azure Data Explorer bindings to your Functions project with an update to the `pom.xml`

file in your Python Azure Functions project, as follows:

```
<dependency>
<groupId>com.microsoft.azure.functions</groupId>
<artifactId>azure-functions-java-library-kusto</artifactId>
<version>1.0.4-Preview</version>
</dependency>
```


## Kusto connection string

Azure Data Explorer bindings for Azure Functions have a required property for the connection string on all bindings. The connection string is documented at [Kusto connection strings](/en-us/azure/data-explorer/kusto/api/connection-strings/kusto).

## Considerations

- Azure Data Explorer binding supports version 4.x and later of the Functions runtime.
- Source code for the Azure Data Explorer bindings is in
[this GitHub repository](https://github.com/Azure/Webjobs.Extensions.Kusto). - For enhanced security, your function app should use managed identities when connecting to Azure Data Explorer instead of using connection strings that contain keys. For more information, see
[Kusto connection strings](/en-us/azure/data-explorer/kusto/api/connection-strings/kusto). For managed identity-based connections, you must set the`managedServiceIdentity`

property in the binding definition. - This binding requires connectivity to Azure Data Explorer. For input bindings, users require
**Viewer**permissions. For output bindings, users require**Ingestor**permissions. For more information about permissions, see[Role-based access control](/en-us/azure/data-explorer/kusto/management/access-control/role-based-access-control).


---

<!-- DOCUMENTO FUSIONADO: functions-develop-local.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-develop-local -->

# Code and test Azure Functions locally

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Whenever possible, you should create and validate your Azure Functions code project in a local development environment. Azure Functions Core Tools provides a local runtime version of Azure Functions that integrates with popular development tools for an integrated development, debugging, and deployments. Your local functions can even connect to live Azure services.

This article provides some shared guidance for local development, such as working with the [local.settings.json file](#local-settings-file). It also links to development environment-specific guidance.

Tip

You can find detailed information about how to develop functions locally in the linked IDE-specific guidance articles.

## Local development environments

The way in which you develop functions on your local computer depends on your [language](supported-languages) and tooling preferences. Make sure to choose your preferred language at the [top of the article](#top).

Tip

All local development relies on Azure Functions Core Tools to provide the Functions runtime for debugging in a local environment.

You can use these development environments to code functions locally in your preferred language:

| Environment | Description |
|---|---|
|

**Azure development**workload of[Visual Studio](https://www.visualstudio.com/vs/). Lets you compile and deploy your C# function code to Azure as a .NET class library. Includes the Core Tools for local testing. To learn more, see[Create your first C# function in Azure using Visual Studio](functions-create-your-first-function-visual-studio)[Visual Studio Code](functions-develop-vs-code)[Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)adds Functions support to Visual Studio Code. Requires the Core Tools. Supports development on Linux, macOS, and Windows. To learn more, see[Create your first function using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-csharp).[Command prompt or terminal](functions-run-local)[Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools)provides the core runtime and templates for creating functions, which enable local development. Supports development on Linux, macOS, and Windows. To learn more, see[Create a C# function in Azure from the command line](how-to-create-function-azure-cli?pivots=programming-language-csharp).| Environment | Description |
|---|---|
|

[Create your first function with Java and Maven](how-to-create-function-azure-cli?pivots=programming-language-java).[Visual Studio Code](functions-develop-vs-code)[Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)adds Functions support to Visual Studio Code. Requires the Core Tools. Supports development on Linux, macOS, and Windows. To learn more, see[Create your first function using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-java).[IntelliJ IDEA](functions-create-maven-intellij)[Create your first Java function in Azure using IntelliJ](functions-create-maven-intellij).[Eclipse](functions-create-maven-eclipse)[Create your first Java function in Azure using Ecplise](functions-create-maven-eclipse).| Environment | Description |
|---|---|
|

[Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)adds Functions support to Visual Studio Code. Requires the Core Tools. Supports development on Linux, macOS, and Windows. To learn more, see[Create your first function using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-javascript).[Command prompt or terminal](functions-run-local)[Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools)provides the core runtime and templates for creating functions, which enable local development. Supports development on Linux, macOS, and Windows. To learn more, see[Create a Node.js function in Azure from the command line](how-to-create-function-azure-cli?pivots=programming-language-javascript).| Environment | Description |
|---|---|
|

[Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)adds Functions support to Visual Studio Code. Requires the Core Tools. Supports development on Linux, macOS, and Windows. To learn more, see[Create your first function using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-powershell).[Command prompt or terminal](functions-run-local)[Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools)provides the core runtime and templates for creating functions, which enable local development. Supports development on Linux, macOS, and Windows. To learn more, see[Create a PowerShell function in Azure from the command line](how-to-create-function-azure-cli?pivots=programming-language-powershell).| Environment | Description |
|---|---|
|

[Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)adds Functions support to Visual Studio Code. Requires the Core Tools. Supports development on Linux, macOS, and Windows. To learn more, see[Create your first function using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-python).[Command prompt or terminal](functions-run-local)[Azure Functions Core Tools](https://www.npmjs.com/package/azure-functions-core-tools)provides the core runtime and templates for creating functions, which enable local development. Supports development on Linux, macOS, and Windows. To learn more, see[Create a Python function in Azure from the command line](how-to-create-function-azure-cli?pivots=programming-language-python).Each of these local development environments lets you create function app projects and use predefined function templates to create new functions. Each uses the Core Tools so that you can test and debug your functions against the real Functions runtime on your own machine just as you would any other app. You can also publish your function app project from any of these environments to Azure.

## Local project files

A Functions project directory contains the following files in the project root folder, regardless of language:

| File name | Description |
|---|---|
| host.json | To learn more, see the
|

[local settings file](#local-settings-file).[local settings file](#local-settings-file).Other files in the project depend on your language and specific functions. For more information, see the developer guide for your language.

### Local settings file

The `local.settings.json`

file stores app settings and settings used by local development tools. Settings in the `local.settings.json`

file are used only when you're running your project locally. When you publish your project to Azure, be sure to also add any required settings to the app settings for the function app.

Important

Because the `local.settings.json`

file might contain secrets, such as connection strings, you should use caution committing to source control. Tools that support Functions provide ways to synchronize settings in the `local.settings.json`

file with the [app settings](functions-how-to-use-azure-function-app-settings#settings) in the function app to which your project is deployed.

The `local.settings.json`

file has this structure:

```
{
"IsEncrypted": false,
"Values": {
"FUNCTIONS_WORKER_RUNTIME": "<language worker>",
"AzureWebJobsStorage": "<connection-string>",
"MyBindingConnection": "<binding-connection-string>",
"AzureWebJobs.HttpExample.Disabled": "true"
},
"Host": {
"LocalHttpPort": 7071,
"CORS": "*",
"CORSCredentials": false
},
"ConnectionStrings": {
"SQLConnectionString": "<sqlclient-connection-string>"
}
}
```


These settings are supported when you run projects locally:

| Setting | Description |
|---|---|
`IsEncrypted` |
When this setting is set to `true` , all values are encrypted with a local machine key. Used with `func settings` commands. Default value is `false` . You might want to encrypt the local.settings.json file on your local computer when it contains secrets, such as service connection strings. The host automatically decrypts settings when it runs. Use the `func settings decrypt` command before trying to read locally encrypted settings. |
`Values` |
Collection of application settings used when a project is running locally. These key-value (string-string) pairs correspond to application settings in your function app in Azure, like
`AzureWebJobsStorage` |

`Connection`

for the [Blob storage trigger](functions-bindings-storage-blob-trigger#configuration). For these properties, you need an application setting defined in the

`Values`

array. See the subsequent table for a list of commonly used settings. Values must be strings and not JSON objects or arrays. Setting names can't include a double underline (

`__`

) and shouldn't include a colon (`:`

). Double underline characters are reserved by the runtime, and the colon is reserved to support [dependency injection](functions-dotnet-dependency-injection#working-with-options-and-settings).

`Host`

`LocalHttpPort`

`func host start`

and `func run`

). The `--port`

command-line option takes precedence over this setting. For example, when running in Visual Studio IDE, you may change the port number by navigating to the "Project Properties -> Debug" window and explicitly specifying the port number in a `host start --port <your-port-number>`

command that can be supplied in the "Application Arguments" field.`CORS`

[cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing). Origins are supplied as a comma-separated list with no spaces. The wildcard value (*) is supported, which allows requests from any origin.`CORSCredentials`

`true`

, allows `withCredentials`

requests.`ConnectionStrings`

`ConnectionStrings`

section of a configuration file, like [Entity Framework](/en-us/ef/ef6/). Connection strings in this object are added to the environment with the provider type of[System.Data.SqlClient](/en-us/dotnet/api/system.data.sqlclient). Items in this collection aren't published to Azure with other app settings. You must explicitly add these values to the`Connection strings`

collection of your function app settings. If you're creating a [in your function code, you should store the connection string value with your other connections in](/en-us/dotnet/api/system.data.sqlclient.sqlconnection)`SqlConnection`

**Application Settings**in the portal.The following application settings can be included in the ** Values** array when running locally:

| Setting | Values | Description |
|---|---|---|
`AzureWebJobsStorage` |
Storage account connection string, or`UseDevelopmentStorage=true` |
Contains the connection string for an Azure storage account. Required when using triggers other than HTTP. For more information, see the
`AzureWebJobsStorage` |

When you have the

[Azurite Emulator](../storage/common/storage-use-azurite)installed locally and you set

[to](functions-app-settings#azurewebjobsstorage)

`AzureWebJobsStorage`

`UseDevelopmentStorage=true`

, Core Tools uses the emulator. For more information, see [Local storage emulator](#local-storage-emulator).

`AzureWebJobs.<FUNCTION_NAME>.Disabled`

`true`

|`false`

`"AzureWebJobs.<FUNCTION_NAME>.Disabled": "true"`

to the collection, where `<FUNCTION_NAME>`

is the name of the function. To learn more, see [How to disable functions in Azure Functions](disable-function#disable-functions-locally).`FUNCTIONS_WORKER_RUNTIME`

`dotnet`

`dotnet-isolated`

`node`

`java`

`powershell`

`python`

[reference.](functions-app-settings#functions_worker_runtime)`FUNCTIONS_WORKER_RUNTIME`

`FUNCTIONS_WORKER_RUNTIME_VERSION`

`~7`

`powerShellVersion`

site configuration setting, when it runs in Azure, which can be [set in the portal](functions-reference-powershell#changing-the-powershell-version).To learn how to use values from the `values`

array as environment variables in your function code, see [Environment variables](functions-reference-node#environment-variables) in the developer guide.

To learn how to use values from the `values`

array as environment variables in your function code, see [Environment variables](functions-reference-java#environment-variables) in the developer guide.

To learn how to use values from the `values`

array as environment variables in your function code, see [Environment variables](functions-reference-powershell#environment-variables) in the developer guide.

To learn how to use values from the `values`

array as environment variables in your function code, see [Environment variables](functions-reference-python#environment-variables) in the developer guide.

## Synchronize settings

When you develop your functions locally, any local settings required by your app must also be present in app settings of the function app to which your code is deployed. You might also need to download current settings from the function app to your local project. While you can [manually configure app settings in the Azure portal](functions-how-to-use-azure-function-app-settings?tabs=portal#settings), the following tools also let you synchronize app settings with local settings in your project:

## Triggers and bindings

When you develop your functions locally, you need to take trigger and binding behaviors into consideration. For HTTP triggers, you can call the HTTP endpoint on the local computer, using `http://localhost/`

. For non-HTTP triggered functions, there are several options to run locally:

- The easiest way to test bindings during local development is to use connection strings that target live Azure services. You can target live services by adding the appropriate connection string settings in the
`Values`

array in the local.settings.json file. When you do this, local executions during testing might affect your production services. Instead, consider setting-up separate services to use during development and testing, and then switch to different services during production. - For storage-based triggers, you can use a
[local storage emulator](#local-storage-emulator). - You can manually run non-HTTP trigger functions by using special administrator endpoints. For more information, see
[Manually run a non-HTTP-triggered function](functions-manually-run-non-http).

During local testing, you must be running the host provided by Core Tools (func.exe) locally. For more information, see [Azure Functions Core Tools](functions-run-local).

## HTTP test tools

During development, it's easy to call any of your function endpoints from a web browser when they support the HTTP GET method. However, for other HTTP methods that support payloads, such as POST or PUT, you need to use an HTTP test tool to create and send these HTTP requests to your function endpoints.

Caution

For scenarios where your requests must include sensitive data, make sure to use a tool that protects your data and reduces the risk of exposing any sensitive data to the public. Sensitive data you should protect might include: credentials, secrets, access tokens, API keys, geolocation data, even personal data.

You can keep your data secure by choosing an HTTP test tool that works either offline or locally, doesn't sync your data to the cloud, and doesn't require that you sign in to an online account. Some tools can also protect your data from accidental exposure by implementing specific security features.

Avoid using tools that centrally store your HTTP request history (including sensitive information), don't follow best security practices, or don't respect data privacy concerns.

Consider using one of these tools for securely sending HTTP requests to your function endpoints:

[Visual Studio Code](https://code.visualstudio.com/download)with an[extension from Visual Studio Marketplace](https://marketplace.visualstudio.com/vscode), such as[REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)[PowerShell Invoke-RestMethod](/en-us/powershell/module/microsoft.powershell.utility/invoke-restmethod)[Microsoft Edge - Network Console tool](/en-us/microsoft-edge/devtools-guide-chromium/network-console/network-console-tool)[Bruno](https://www.usebruno.com/)[curl](https://curl.se/)

## Local storage emulator

During local development, you can use the local [Azurite emulator](../storage/common/storage-use-azurite) when testing functions with Azure Storage bindings (Queue Storage, Blob Storage, and Table Storage), without having to connect to remote storage services. Azurite integrates with Visual Studio Code and Visual Studio, and you can also run it from the command prompt using npm. For more information, see [Use the Azurite emulator for local Azure Storage development](../storage/common/storage-use-azurite).

The following setting in the `Values`

collection of the local.settings.json file tells the local Functions host to use Azurite for the default `AzureWebJobsStorage`

connection:

```
"AzureWebJobsStorage": "UseDevelopmentStorage=true"
```


With this setting value, any Azure Storage trigger or binding that uses `AzureWebJobsStorage`

as its connection connects to Azurite when running locally. Keep these considerations in mind when using storage emulation during local execution:

- You must have Azurite installed and running.
- You should test with an actual storage connection to Azure services before publishing to Azure.
- When you publish your project, don't publish the
`AzureWebJobsStorage`

setting as`UseDevelopmentStorage=true`

. In Azure, the`AzureWebJobsStorage`

setting must always be the connection string of the storage account used by your function app. For more information, see.`AzureWebJobsStorage`


## Related articles

- To learn more about local development of functions using Visual Studio, see
[Develop Azure Functions using Visual Studio](functions-develop-vs).

- To learn more about local development of functions using Visual Studio Code on a Mac, Linux, or Windows computer, see
[Develop Azure Functions by using Visual Studio Code](functions-develop-vs-code). - To learn more about developing functions from the command prompt or terminal, see
[Work with Azure Functions Core Tools](functions-run-local).
