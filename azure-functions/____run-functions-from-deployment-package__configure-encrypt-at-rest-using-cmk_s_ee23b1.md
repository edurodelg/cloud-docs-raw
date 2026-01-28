---
merged_at: 2026-01-28T07:43:39.524659
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/run-functions-from-deployment-package -->

# Run your functions from a package file in Azure

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure, you can run your functions directly from a deployment package file in your function app. The other option is to deploy your files in the `c:\home\site\wwwroot`

(Windows) or `/home/site/wwwroot`

(Linux) directory of your function app.

This article describes the benefits of running your functions from a package. It also shows how to enable this functionality in your function app.

## Benefits of running from a package file

There are several benefits to running functions from a package file:

- Reduces the risk of file copy locking issues.
- Can be deployed to a production app (with restart).
- Verifies the files that are running in your app.
- Improves the performance of
[Azure Resource Manager deployments](functions-infrastructure-as-code). - Reduces cold-start times, particularly for JavaScript functions with large npm package trees.

For more information, see [this announcement](https://github.com/Azure/app-service-announcements/issues/84).

## Enable functions to run from a package

Function apps on the [Flex Consumption](flex-consumption-plan) hosting plan run from a package by default. No special configuration needs to be done.

To enable your function app to run from a package on the [Consumption](consumption-plan), [Elastic Premium](functions-premium-plan), and [Dedicated (App Service)](dedicated-plan) hosting plans, add a `WEBSITE_RUN_FROM_PACKAGE`

app setting to your function app. The `WEBSITE_RUN_FROM_PACKAGE`

app setting can have one of the following values:

| Value | Description |
|---|---|
`1` |
Indicates that the function app runs from a local package file deployed in the `c:\home\data\SitePackages` (Windows) or `/home/data/SitePackages` (Linux) folder of your function app. |
`<URL>` |
Sets a URL that is the remote location of the specific package file you want to run. Required for functions apps running on Linux in a Consumption plan. |

The following table indicates the recommended `WEBSITE_RUN_FROM_PACKAGE`

values for deployment to a specific operating system and hosting plan:

| Hosting plan | Windows | Linux |
|---|---|---|
|

`1`

is highly recommended.`<URL>`

is supported.[Premium](functions-premium-plan)`1`

is recommended.`1`

is recommended.[Dedicated](dedicated-plan)`1`

is recommended.`1`

is recommended.## General considerations

- Do not add the
`WEBSITE_RUN_FROM_PACKAGE`

app setting to apps on the[Flex Consumption](flex-consumption-plan)plan. - The package file must be .zip formatted. Tar and gzip formats aren't supported.
[Zip deployment](#integration-with-zip-deployment)is recommended.- When deploying your function app to Windows, you should set
`WEBSITE_RUN_FROM_PACKAGE`

to`1`

and publish with zip deployment. - When you run from a package, the
`wwwroot`

folder is read-only and you receive an error if you write files to this directory. Files are also read-only in the Azure portal. - The maximum size for a deployment package file is 1 GB.
- The deployment uses temporary storage when unpacking your project files. This means that your function app must have enough available temporary storage space to hold the contents of your package. Keep in mind that the temporary storage limit for a Consumption plan is
[500 MB per plan](functions-scale#service-limits). To learn about how to troubleshoot issues with temporary storage, see[How to troubleshoot temporary storage on Azure App Service](/en-us/troubleshoot/azure/app-service/temporary-storage-for-azure-app-service).

- The deployment uses temporary storage when unpacking your project files. This means that your function app must have enough available temporary storage space to hold the contents of your package. Keep in mind that the temporary storage limit for a Consumption plan is
- You can't use the local cache when running from a deployment package.
- If your project needs to use remote build, don't use the
`WEBSITE_RUN_FROM_PACKAGE`

app setting. Instead, add the`SCM_DO_BUILD_DURING_DEPLOYMENT=true`

deployment customization app setting. For Linux, also add the`ENABLE_ORYX_BUILD=true`

setting. For more information, see[Remote build](functions-deployment-technologies#remote-build).

Note

The `WEBSITE_RUN_FROM_PACKAGE`

app setting does not work with MSDeploy as described in [MSDeploy VS. ZipDeploy](https://github.com/projectkudu/kudu/wiki/MSDeploy-VS.-ZipDeploy). You will receive an error during deployment, such as `ARM-MSDeploy Deploy Failed`

. To resolve this error, change `/MSDeploy`

to `/ZipDeploy`

.

### Add the WEBSITE_RUN_FROM_PACKAGE setting

There are several ways that you can add, update, and delete function app settings:

Changes to function app settings require your function app to be restarted.

### Creating the zip archive

The zip archive you deploy must contain all of the files needed to run your function app. You can manually create a zip archive from the contents of a Functions project folder using built-in .zip compression functionality or non-Microsoft tools.

The archive must include the [host.json](functions-host-json) file at the root of the extracted folder. The selected language stack for the function app creates other requirements:

Important

For languages that generate compiled output for deployment, make sure to compress the contents of the output folder you plan to publish and not the entire project folder. When Functions extracts the contents of the zip archive, the `host.json`

file must exist in the root of the package.

## Use WEBSITE_RUN_FROM_PACKAGE = 1

This section provides information about how to run your function app from a local package file.

### Considerations for deploying from an on-site package

- Using an on-site package is the recommended option for running from the deployment package, except when running on Linux hosted in a Consumption plan.
[Zip deployment](#integration-with-zip-deployment)is the recommended way to upload a deployment package to your site.- When not using zip deployment, make sure the
`c:\home\data\SitePackages`

(Windows) or`/home/data/SitePackages`

(Linux) folder has a file named`packagename.txt`

. This file contains only the name, without any whitespace, of the package file in this folder that's currently running.

### Integration with zip deployment

Zip deployment is a feature of Azure App Service that lets you deploy your function app project to the `wwwroot`

directory. The project is packaged as a .zip deployment file. The same APIs can be used to deploy your package to the `c:\home\data\SitePackages`

(Windows) or `/home/data/SitePackages`

(Linux) folder.

When you set the `WEBSITE_RUN_FROM_PACKAGE`

app setting value to `1`

, the zip deployment APIs copy your package to the `c:\home\data\SitePackages`

(Windows) or `/home/data/SitePackages`

(Linux) folder instead of extracting the files to `c:\home\site\wwwroot`

(Windows) or `/home/site/wwwroot`

(Linux). It also creates the `packagename.txt`

file. After your function app is automatically restarted, the package is mounted to `wwwroot`

as a read-only filesystem. For more information about zip deployment, see [Zip deployment for Azure Functions](deployment-zip-push).

Note

When a deployment occurs, a restart of the function app is triggered. Function executions currently running during the deploy are terminated. For information about how to write stateless and defensive functions, sett [Write functions to be stateless](performance-reliability#write-functions-to-be-stateless).

## Use WEBSITE_RUN_FROM_PACKAGE = URL

This section provides information about how to run your function app from a package deployed to a URL endpoint. This option is the only one supported for running from a Linux-hosted package with a Consumption plan. This option is not supported in the [Flex Consumption](flex-consumption-plan) plan.

### Considerations for deploying from a URL

- Do not set
`WEBSITE_RUN_FROM_PACKAGE = <URL>`

in apps on the[Flex Consumption](flex-consumption-plan)plan. This option is not supported. - Function apps running on Windows experience a slight increase in
[cold-start time](event-driven-scaling#cold-start)when the application package is deployed to a URL endpoint via`WEBSITE_RUN_FROM_PACKAGE = <URL>`

. - When you specify a URL, you must also
[manually sync triggers](functions-deployment-technologies#trigger-syncing)after you publish an updated package. - The Functions runtime must have permissions to access the package URL.
- Don't deploy your package to Azure Blob Storage as a public blob. Instead, use a private container with a
[shared access signature (SAS)](../storage/common/storage-sas-overview)or[use a managed identity](#fetch-a-package-from-azure-blob-storage-using-a-managed-identity)to enable the Functions runtime to access the package. - You must maintain any SAS URLs used for deployment. When an SAS expires, the package can no longer be deployed. In this case, you must generate a new SAS and update the setting in your function app. You can eliminate this management burden by
[using a managed identity](#fetch-a-package-from-azure-blob-storage-using-a-managed-identity). - When running on a Premium plan, make sure to
[eliminate cold starts](functions-premium-plan#eliminate-cold-starts). - When you're running on a Dedicated plan, ensure you enable
[Always On](dedicated-plan#always-on). - You can use
[Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer)to upload package files to blob containers in your storage account.

### Manually uploading a package to Blob Storage

To deploy a zipped package when using the URL option, you must create a .zip compressed deployment package and upload it to the destination. The following procedure deploys to a container in Blob Storage:

Create a .zip package for your project using the utility of your choice.

In the

[Azure portal](https://portal.azure.com), search for your storage account name or browse for it in the storage accounts list.In the storage account, select

**Containers**under**Data storage**.Select

**+ Container**to create a new Blob Storage container in your account.In the

**New container**page, provide a**Name**(for example,*deployments*), ensure the**Anonymous access level**is**Private**, and then select**Create**.Select the container you created, select

**Upload**, browse to the location of the .zip file you created with your project, and then select**Upload**.After the upload completes, choose your uploaded blob file, and copy the URL. If you aren't

[using a managed identity](#fetch-a-package-from-azure-blob-storage-using-a-managed-identity), you might need to generate a SAS URL.Search for your function app or browse for it in the

**Function App**page.In your function app, expand

**Settings**, and then select**Environment variables**.In the

**App settings**tab, select**+ Add**.Enter the value

`WEBSITE_RUN_FROM_PACKAGE`

for the**Name**, and paste the URL of your package in Blob Storage for the**Value**.Select

**Apply**, and then select**Apply**and**Confirm**to save the setting and restart the function app.

Now you can run your function in Azure to verify that deployment of the deployment package .zip file was successful.

### Fetch a package from Azure Blob Storage using a managed identity

You can configure Azure Blob Storage to [authorize requests with Microsoft Entra ID](/en-us/azure/storage/blobs/authorize-access-azure-active-directory?toc=%2fazure%2fstorage%2fblobs%2ftoc.json). This configuration means that instead of generating a SAS key with an expiration, you can instead rely on the application's [managed identity](/en-us/azure/app-service/overview-managed-identity). By default, the app's system-assigned identity is used. If you wish to specify a user-assigned identity, you can set the `WEBSITE_RUN_FROM_PACKAGE_BLOB_MI_RESOURCE_ID`

app setting to the resource ID of that identity. The setting can also accept `SystemAssigned`

as a value, which is equivalent to omitting the setting.

To enable the package to be fetched using the identity:

Ensure that the blob is

[configured for private access](/en-us/azure/storage/blobs/anonymous-read-access-configure#set-the-anonymous-access-level-for-a-container).Grant the identity the

[Storage Blob Data Reader](/en-us/azure/role-based-access-control/built-in-roles#storage-blob-data-reader)role with scope over the package blob. See[Assign an Azure role for access to blob data](/en-us/azure/storage/blobs/assign-azure-role-data-access)for details on creating the role assignment.Set the

`WEBSITE_RUN_FROM_PACKAGE`

application setting to the blob URL of the package. This URL is usually of the form`https://{storage-account-name}.blob.core.windows.net/{container-name}/{path-to-package}`

or similar.If you wish to specify a user-assigned identity, you can set the

`WEBSITE_RUN_FROM_PACKAGE_BLOB_MI_RESOURCE_ID`

app setting to the resource ID of that identity. The setting can also accept "SystemAssigned" as a value, although this is the same as omitting the setting altogether. A resource ID is a standard representation for a resource in Azure. For a user-assigned managed identity, that is going to be`/subscriptions/subid/resourcegroups/rg-name/providers/Microsoft.ManagedIdentity/userAssignedIdentities/identity-name`

. The resource ID of a user-assigned managed identity can be obtained in the**Settings**->**Properties**->**ID for the user assigned managed identity**.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/configure-encrypt-at-rest-using-cmk -->

# Encrypt your application data at rest using customer-managed keys

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Encrypting your function app's application data at rest requires an Azure Storage Account and an Azure Key Vault. These services are used when you run your app from a deployment package.

[Azure Storage provides encryption at rest](../storage/common/storage-service-encryption). You can use system-provided keys or your own, customer-managed keys. This is where your application data is stored when it's not running in a function app in Azure.[Running from a deployment package](run-functions-from-deployment-package)is a deployment feature of App Service. It allows you to deploy your site content from an Azure Storage Account using a Shared Access Signature (SAS) URL.[Key Vault references](../app-service/app-service-key-vault-references)are a security feature of App Service. It allows you to import secrets at runtime as application settings. Use this to encrypt the SAS URL of your Azure Storage Account.

## Set up encryption at rest

### Create an Azure Storage account

First, [create an Azure Storage account](../storage/common/storage-account-create) and [encrypt it with customer managed keys](../storage/common/customer-managed-keys-overview). Once the storage account is created, use the [Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer) to upload package files.

Next, use the Storage Explorer to [generate an SAS](../vs-azure-tools-storage-manage-with-storage-explorer?tabs=windows#generate-a-sas-in-storage-explorer).

Note

Save this SAS URL, this is used later to enable secure access of the deployment package at runtime.

### Configure running from a package from your storage account

Once you upload your file to Blob storage and have an SAS URL for the file, set the `WEBSITE_RUN_FROM_PACKAGE`

application setting to the SAS URL. The following example does it by using Azure CLI:

```
az webapp config appsettings set --name <app-name> --resource-group <resource-group-name> --settings WEBSITE_RUN_FROM_PACKAGE="<your-SAS-URL>"
```


Adding this application setting causes your function app to restart. After the app has restarted, browse to it and make sure that the app has started correctly using the deployment package. If the application didn't start correctly, see the [Run from package troubleshooting guide](run-functions-from-deployment-package#troubleshooting).

### Encrypt the application setting using Key Vault references

Now you can replace the value of the `WEBSITE_RUN_FROM_PACKAGE`

application setting with a Key Vault reference to the SAS-encoded URL. This keeps the SAS URL encrypted in Key Vault, which provides an extra layer of security.

Use the following

command to create a Key Vault instance.`az keyvault create`

`az keyvault create --name "Contoso-Vault" --resource-group <group-name> --location eastus`

Follow

[these instructions to grant your app access](../app-service/app-service-key-vault-references#grant-your-app-access-to-a-key-vault)to your key vault:Use the following

command to add your external URL as a secret in your key vault:`az keyvault secret set`

`az keyvault secret set --vault-name "Contoso-Vault" --name "external-url" --value "<SAS-URL>"`

Use the following

command to create the`az webapp config appsettings set`

`WEBSITE_RUN_FROM_PACKAGE`

application setting with the value as a Key Vault reference to the external URL:`az webapp config appsettings set --settings WEBSITE_RUN_FROM_PACKAGE="@Microsoft.KeyVault(SecretUri=https://Contoso-Vault.vault.azure.net/secrets/external-url/<secret-version>"`

The

`<secret-version>`

will be in the output of the previous`az keyvault secret set`

command.

Updating this application setting causes your function app to restart. After the app has restarted, browse to it make sure it has started correctly using the Key Vault reference.

## How to rotate the access token

It is best practice to periodically rotate the SAS key of your storage account. To ensure the function app does not inadvertently lose access, you must also update the SAS URL in Key Vault.

Rotate the SAS key by navigating to your storage account in the Azure portal. Under

**Settings**>**Access keys**, select the icon to rotate the SAS key.Copy the new SAS URL, and use the following command to set the updated SAS URL in your key vault:

`az keyvault secret set --vault-name "Contoso-Vault" --name "external-url" --value "<SAS-URL>"`

Update the key vault reference in your application setting to the new secret version:

`az webapp config appsettings set --settings WEBSITE_RUN_FROM_PACKAGE="@Microsoft.KeyVault(SecretUri=https://Contoso-Vault.vault.azure.net/secrets/external-url/<secret-version>"`

The

`<secret-version>`

will be in the output of the previous`az keyvault secret set`

command.

## How to revoke the function app's data access

There are two methods to revoke the function app's access to the storage account.

### Rotate the SAS key for the Azure Storage account

If the SAS key for the storage account is rotated, the function app will no longer have access to the storage account, but it will continue to run with the last downloaded version of the package file. Restart the function app to clear the last downloaded version.

### Remove the function app's access to Key Vault

You can revoke the function app's access to the site data by disabling the function app's access to Key Vault. To do this, remove the access policy for the function app's identity. This is the same identity you created earlier while configuring key vault references.

## Summary

Your application files are now encrypted at rest in your storage account. When your function app starts, it retrieves the SAS URL from your key vault. Finally, the function app loads the application files from the storage account.

If you need to revoke the function app's access to your storage account, you can either revoke access to the key vault or rotate the storage account keys, both of which invalidate the SAS URL.

## Frequently Asked Questions

### Is there any additional charge for running my function app from the deployment package?

Only the cost associated with the Azure Storage Account and any applicable egress charges.

### How does running from the deployment package affect my function app?

- Running your app from the deployment package makes
`wwwroot/`

read-only. Your app receives an error when it attempts to write to this directory. - TAR and GZIP formats are not supported.
- This feature is not compatible with local cache.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/self-hosted-mcp-servers -->

# Self-hosted remote MCP server on Azure Functions (public preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions provides two ways of hosting remote MCP servers:

- MCP servers created with the
[Functions MCP extension](functions-bindings-mcp) - MCP servers built with the
[official MCP SDKs](https://modelcontextprotocol.io/docs/sdk)

With the first approach, you can use the Azure Functions programming model with triggers and bindings to build the MCP server. Then, you can host the server remotely by deploying it to a Function app.

If you already have an MCP server created with the official MCP SDKs and just want to host it remotely, the second approach likely suits your needs. You don't need to make any code changes to the server to host it on Azure Functions. Instead, you can add the required Functions artifacts, and the server is ready to be deployed. As such, these servers are referred to as *self-hosted MCP servers*.


This article provides an overview of self-hosted MCP servers and links to relevant articles and samples.

## Custom handlers

Self-hosted MCP servers deploy to the Azure Functions platform as *custom handlers*. Custom handlers are lightweight web servers that receive events from the Functions host. They provide a way to run on the Functions platform applications built with frameworks different from the Functions programming model or in languages not supported out-of-the-box. For more information, see [Azure Functions custom handlers](functions-custom-handlers).

When you deploy an MCP SDK based server to Azure Functions, you must include a *host.json* in your project. The minimal *host.json* looks like this:

```
{
"version": "2.0",
"configurationProfile": "mcp-custom-handler",
"customHandler": {
"description": {
"defaultExecutablePath": "python",
"arguments": ["Path to main script file, e.g. hello_world.py"]
},
"port": "<MCP server port>"
}
}
```


```
{
"version": "2.0",
"configurationProfile": "mcp-custom-handler",
"customHandler": {
"description": {
"defaultExecutablePath": "npm",
"arguments": ["run", "start"]
},
"port": "<MCP server port>"
}
}
```


```
{
"version": "2.0",
"configurationProfile": "mcp-custom-handler",
"customHandler": {
"description": {
"defaultExecutablePath": "dotnet",
"arguments": ["Path to the compiled DLL, e.g. HelloWorld.dll"]
},
"port": "<MCP server port>"
}
}
```


Note

Because the payload deployed to Azure Functions is the content of the `bin/output`

directory, the path to the compiled DLL is relative to that directory, *not* to the project root.

Example not yet available.

Using a `configuration Profile`

value of `mcp-custom-handler`

automatically configures these Functions host settings, which are required for running your MCP server in Azure Functions:

`http.enableProxying`

to`true`

`http.routes`

to`[{ "route": "{*route}" }]`

`extensions.http.routePrefix`

to`""`


This example shows a host.json file with extra custom handler properties set equivalent to using the `mcp-custom-handler`

profile:

```
{
"version": "2.0",
"extensions": {
"http": {
"routePrefix": ""
}
},
"customHandler": {
"description": {
"defaultExecutablePath": "",
"arguments": [""]
},
"http": {
"enableProxying": true,
"defaultAuthorizationLevel": "anonymous",
"routes": [
{
"route": "{*route}",
// Default authorization level is `defaultAuthorizationLevel`
},
{
"route": "admin/{*route}",
"authorizationLevel": "admin"
}
]
}
}
}
```


This table explains the properties of `customHandler.http`

, along with default values:

| Property | What it does | Default value |
|---|---|---|
`enableProxying` |
Controls how the Azure Functions host handles HTTP requests to custom handlers. When `enableProxying` is set to `true` , the Functions host acts as a reverse proxy and forwards the entire HTTP request (including headers, body, query parameters) directly to the custom handler. This setting gives the custom handler full access to the original HTTP request details. When `enableProxying` is `false` , the Functions host processes the request first and transforms it into the Azure Functions request/response format before passing it to the custom handler. |
`false` |
`defaultAuthorizationLevel` |
Controls the authentication requirement for accessing custom handler endpoints. For example, `function` requires a function-specific API key to access. For more information, see
|
`function` |
`route` |
Specifies the URL path pattern that the custom handler responds to. `{*route}` matches any URL path (such as `/` , `/mcp` , `/api/tools` , or `/anything/nested/path` ) and forwards the request to the custom handler. |
`{*route}` |

## Built-in server authentication

OAuth-based authentication and authorization provided by the App Service platform implements the requirements of the [MCP authorization specification](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization), such as issuing 401 challenge and exposing the Protected Resource Metadata (PRM) document. When you enable built-in authentication, clients attempting to access the server are redirected to identity providers like Microsoft Entra ID for authentication before connecting.

For more information, see [Configure built-in server authorization (preview)](../app-service/configure-authentication-mcp) and [Hosting MCP servers on Azure Functions](functions-mcp-tutorial).

## Azure AI Foundry agent integrations

Agents in Azure AI Foundry can be [configured to use tools](functions-mcp-tutorial#configure-azure-ai-foundry-agent-to-use-your-tools) in MCP servers hosted in Azure Functions.

## Register your server in Azure API Center

When you register your MCP server in Azure API Center, you create a private organizational tool catalog. This approach is recommended for sharing MCP servers across your organization with consistent governance and discoverability. For more information, see [Register MCP servers hosted in Azure Functions in Azure API Center](register-mcp-server-api-center).

## Public preview support

The ability to host your own SDK-based MCP servers in Functions is currently in preview and supports these features:

**Stateless**servers that use the**streamable-http**transport. If you need your server to be stateful, consider using the Functions MCP extension.- Servers implemented with the Python, TypeScript, C#, or Java MCP SDKs.
- When running the project locally, you must use the Azure Functions Core Tools (
`func start`

command). You can't currently use`F5`

to start running with the debugger. - Servers must be hosted as
[Flex Consumption plan](flex-consumption-plan)apps.

## Samples

Not yet available.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-errors -->

# Azure Functions error handling and retries

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Handling errors in Azure Functions helps you avoid lost data, avoid missed events, and monitor the health of your application. It's also an important way to help you understand the retry behaviors of event-based triggers.

This article describes general strategies for error handling and the available retry strategies.

Important

The preview of retry policy support for certain triggers was removed in December 2022. Retry policies for supported triggers are now in general availability (GA). The [Retries](#retries) section of this article lists extensions that currently support retry policies.

## Handling errors

Errors that occur in an Azure function can come from:

- Use of built-in Azure Functions
[triggers and bindings](functions-triggers-bindings). - Calls to APIs of underlying Azure services.
- Calls to REST endpoints.
- Calls to client libraries, packages, or non-Microsoft APIs.

To avoid loss of data or missed messages, you should practice good error handling. This table describes some recommended error-handling practices and provides links to more information:

| Recommendation | Details |
|---|---|
| Enable Application Insights | Azure Functions integrates with Application Insights to collect error data, performance data, and runtime logs. Use Application Insights to discover and better understand errors that occur in your function executions. To learn more, see
|

[Binding error codes](#binding-error-codes)in this article. Depending on your specific retry strategy, you might also raise a new exception to run the function again.[Retries](#retries)in this article.[Designing Azure Functions for identical input](functions-idempotent).Tip

When you use output bindings, you can't handle errors that occur from accessing the remote service. Because of this behavior, you should validate all data passed to your output bindings to avoid raising any known exceptions. If you must be able to handle such exceptions in your function code, you should access the remote service by using the client SDK instead of relying on output bindings.

## Retries

Two kinds of retries are available for your functions:

- Built-in retry behaviors of individual trigger extensions
- Retry policies that the Azure Functions runtime provides

The following table indicates which triggers support retries and where the retry behavior is configured. It also links to more information about errors that come from the underlying services.

| Trigger/binding | Retry source | Configuration |
|---|---|---|
| Azure Cosmos DB |
|

[Binding extension](functions-bindings-storage-blob-trigger#poison-blobs)[host.json](functions-bindings-storage-queue#host-json)[Binding extension](../event-grid/delivery-and-retry)[Retry policies](#retry-policies)[Retry policies](#retry-policies)[Binding extension](functions-bindings-storage-queue-trigger#poison-messages)[host.json](functions-bindings-storage-queue#host-json)[Binding extension](functions-bindings-rabbitmq-trigger#dead-letter-queues)[Dead letter queue](https://www.rabbitmq.com/dlx.html)[Binding extension](functions-bindings-service-bus-trigger)[host.json](functions-bindings-service-bus#hostjson-settings)*[Retry policies](#retry-policies)* Requires version 5.x of the Azure Service Bus extension. In older extension versions, the [Service Bus dead letter queue](../service-bus-messaging/service-bus-dead-letter-queues#maximum-delivery-count) implements retry behaviors.

## Retry policies

With Azure Functions, you can define retry policies for specific trigger types. The runtime enforces these retry policies. The following trigger types currently support retry policies:

Retry support is the same for both v1 and v2 Python programming models.

Retry policies aren't supported in version 1.x of the Azure Functions runtime.

The retry policy tells the runtime to rerun a failed execution until either successful completion occurs or the maximum number of retries is reached.

A retry policy is evaluated when a function that a supported trigger type executes raises an uncaught exception. As a best practice, you should catch all exceptions in your code and raise new exceptions for any errors that you want to result in a retry.

Important

Event Hubs checkpoints aren't written until after the retry policy for the execution finishes. Because of this behavior, progress on the specific partition is paused until the current batch finishes processing. For more information, see [Reliable event processing with Azure Functions and Event Hubs](functions-reliable-event-processing).

Version 5.x of the Event Hubs extension supports extra retry capabilities for interactions between the Azure Functions host and the event hub. For more information, see `clientRetryOptions`

in the [Event Hubs host.json reference](functions-bindings-event-hubs#host-json).

### Retry strategies

You can configure two retry strategies that are supported by policy:

A specified amount of time is allowed to elapse between each retry.

When you use a Consumption plan, you're billed only for the time that your function code is running. You aren't billed for the wait time between executions in either of these retry strategies.

### Maximum retry counts

You can configure the maximum number of times that a function execution is retried before eventual failure. The current retry count is stored in the memory of the instance.

It's possible for an instance to have a failure between retry attempts. When an instance fails during a retry policy, the retry count is lost. When there are instance failures, the Event Hubs trigger can resume processing and retry the batch on a new instance, with the retry count reset to zero. The timer trigger doesn't resume on a new instance.

This behavior means that the maximum retry count is a best effort. In some rare cases, an execution could be retried more than the requested maximum number of times. For timer triggers, the retries can be less than the requested maximum number.

### Retry examples

Examples are provided for both fixed delay and exponential backoff strategies. To see examples for a specific strategy, you must first select that strategy on the previous tab.

Function-level retries are supported with the following NuGet packages:

[Microsoft.Azure.Functions.Worker.Sdk](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Sdk)version 1.9.0 and later[Microsoft.Azure.Functions.Worker.Extensions.EventHubs](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventHubs)version 5.2.0 and later[Microsoft.Azure.Functions.Worker.Extensions.Kafka](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Kafka)version 3.8.0 and later[Microsoft.Azure.Functions.Worker.Extensions.Timer](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Timer)version 4.2.0 and later

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


| Property | Description |
|---|---|
`MaxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`DelayInterval` |
The delay used between retries. Specify it as a string with the format `HH:mm:ss` . |

Here's an example of a retry policy defined in the `function.json`

file:

```
{
"disabled": false,
"bindings": [
{
....
}
],
"retry": {
"strategy": "fixedDelay",
"maxRetryCount": 4,
"delayInterval": "00:00:10"
}
}
```


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixedDelay` and `exponentialBackoff` . |
`maxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delayInterval` |
The delay used between retries when you're using a `fixedDelay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimumInterval` |
The minimum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximumInterval` |
The maximum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

The way that you define the retry policy for the trigger depends on your Node.js version:

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
const { app } = require('@azure/functions');
app.timer('timerTriggerWithRetry', {
schedule: '0 */5 * * * *',
retry: {
strategy: 'fixedDelay',
delayInterval: {
seconds: 10,
},
maxRetryCount: 4,
},
handler: (myTimer, context) => {
if (context.retryContext?.retryCount < 2) {
throw new Error('Retry!');
} else {
context.log('Timer function processed request.');
}
},
});
```


The way that you define the retry policy for the trigger depends on your Node.js version:

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
import { app, InvocationContext, Timer } from '@azure/functions';
export async function timerTriggerWithRetry(myTimer: Timer, context: InvocationContext): Promise<void> {
if (context.retryContext?.retryCount < 2) {
throw new Error('Retry!');
} else {
context.log('Timer function processed request.');
}
}
app.timer('timerTriggerWithRetry', {
schedule: '0 */5 * * * *',
retry: {
strategy: 'fixedDelay',
delayInterval: {
seconds: 10,
},
maxRetryCount: 4,
},
handler: timerTriggerWithRetry,
});
```


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixedDelay` and `exponentialBackoff` . |
`maxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delayInterval` |
The delay used between retries when you're using a `fixedDelay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimumInterval` |
The minimum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximumInterval` |
The maximum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
import logging
from azure.functions import AuthLevel, Context, FunctionApp, TimerRequest
app = FunctionApp(http_auth_level=AuthLevel.ANONYMOUS)
@app.timer_trigger(schedule="*/1 * * * * *", arg_name="mytimer",
run_on_startup=False,
use_monitor=False)
@app.retry(strategy="fixed_delay", max_retry_count="3",
delay_interval="00:00:01")
def mytimer(mytimer: TimerRequest, context: Context) -> None:
logging.info(f'Current retry count: {context.retry_context.retry_count}')
if context.retry_context.retry_count == \
context.retry_context.max_retry_count:
logging.info(
f"Max retries of {context.retry_context.max_retry_count} for "
f"function {context.function_name} has been reached")
else:
raise Exception("This is a retryable exception")
```


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixed_delay` and `exponential_backoff` . |
`max_retry_count` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delay_interval` |
The delay used between retries when you're using a `fixed_delay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimum_interval` |
The minimum retry delay when you're using an `exponential_backoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximum_interval` |
The maximum retry delay when you're using an `exponential_backoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

```
@FunctionName("TimerTriggerJava1")
@FixedDelayRetry(maxRetryCount = 4, delayInterval = "00:00:10")
public void run(
@TimerTrigger(name = "timerInfo", schedule = "0 */5 * * * *") String timerInfo,
final ExecutionContext context
) {
context.getLogger().info("Java Timer trigger function executed at: " + LocalDateTime.now());
}
```


## Binding error codes

When you're integrating with Azure services, errors might originate from the APIs of the underlying services. Information that relates to binding-specific errors is available in the "Exceptions and return codes" sections of the following articles:

[Azure Cosmos DB](/en-us/rest/api/cosmos-db/http-status-codes-for-cosmosdb)[Blob Storage](functions-bindings-storage-blob-output#exceptions-and-return-codes)[Event Grid](../event-grid/troubleshoot-errors)[Event Hubs](functions-bindings-event-hubs-output#exceptions-and-return-codes)[IoT Hub](functions-bindings-event-iot-output#exceptions-and-return-codes)[Notification Hubs](functions-bindings-notification-hubs#exceptions-and-return-codes)[Queue Storage](functions-bindings-storage-queue-output#exceptions-and-return-codes)[Service Bus](functions-bindings-service-bus-output#exceptions-and-return-codes)[Table Storage](functions-bindings-storage-table-output#exceptions-and-return-codes)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-error-pages -->

# Azure Functions error handling and retries

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Handling errors in Azure Functions helps you avoid lost data, avoid missed events, and monitor the health of your application. It's also an important way to help you understand the retry behaviors of event-based triggers.

This article describes general strategies for error handling and the available retry strategies.

Important

The preview of retry policy support for certain triggers was removed in December 2022. Retry policies for supported triggers are now in general availability (GA). The [Retries](#retries) section of this article lists extensions that currently support retry policies.

## Handling errors

Errors that occur in an Azure function can come from:

- Use of built-in Azure Functions
[triggers and bindings](functions-triggers-bindings). - Calls to APIs of underlying Azure services.
- Calls to REST endpoints.
- Calls to client libraries, packages, or non-Microsoft APIs.

To avoid loss of data or missed messages, you should practice good error handling. This table describes some recommended error-handling practices and provides links to more information:

| Recommendation | Details |
|---|---|
| Enable Application Insights | Azure Functions integrates with Application Insights to collect error data, performance data, and runtime logs. Use Application Insights to discover and better understand errors that occur in your function executions. To learn more, see
|

[Binding error codes](#binding-error-codes)in this article. Depending on your specific retry strategy, you might also raise a new exception to run the function again.[Retries](#retries)in this article.[Designing Azure Functions for identical input](functions-idempotent).Tip

When you use output bindings, you can't handle errors that occur from accessing the remote service. Because of this behavior, you should validate all data passed to your output bindings to avoid raising any known exceptions. If you must be able to handle such exceptions in your function code, you should access the remote service by using the client SDK instead of relying on output bindings.

## Retries

Two kinds of retries are available for your functions:

- Built-in retry behaviors of individual trigger extensions
- Retry policies that the Azure Functions runtime provides

The following table indicates which triggers support retries and where the retry behavior is configured. It also links to more information about errors that come from the underlying services.

| Trigger/binding | Retry source | Configuration |
|---|---|---|
| Azure Cosmos DB |
|

[Binding extension](functions-bindings-storage-blob-trigger#poison-blobs)[host.json](functions-bindings-storage-queue#host-json)[Binding extension](../event-grid/delivery-and-retry)[Retry policies](#retry-policies)[Retry policies](#retry-policies)[Binding extension](functions-bindings-storage-queue-trigger#poison-messages)[host.json](functions-bindings-storage-queue#host-json)[Binding extension](functions-bindings-rabbitmq-trigger#dead-letter-queues)[Dead letter queue](https://www.rabbitmq.com/dlx.html)[Binding extension](functions-bindings-service-bus-trigger)[host.json](functions-bindings-service-bus#hostjson-settings)*[Retry policies](#retry-policies)* Requires version 5.x of the Azure Service Bus extension. In older extension versions, the [Service Bus dead letter queue](../service-bus-messaging/service-bus-dead-letter-queues#maximum-delivery-count) implements retry behaviors.

## Retry policies

With Azure Functions, you can define retry policies for specific trigger types. The runtime enforces these retry policies. The following trigger types currently support retry policies:

Retry support is the same for both v1 and v2 Python programming models.

Retry policies aren't supported in version 1.x of the Azure Functions runtime.

The retry policy tells the runtime to rerun a failed execution until either successful completion occurs or the maximum number of retries is reached.

A retry policy is evaluated when a function that a supported trigger type executes raises an uncaught exception. As a best practice, you should catch all exceptions in your code and raise new exceptions for any errors that you want to result in a retry.

Important

Event Hubs checkpoints aren't written until after the retry policy for the execution finishes. Because of this behavior, progress on the specific partition is paused until the current batch finishes processing. For more information, see [Reliable event processing with Azure Functions and Event Hubs](functions-reliable-event-processing).

Version 5.x of the Event Hubs extension supports extra retry capabilities for interactions between the Azure Functions host and the event hub. For more information, see `clientRetryOptions`

in the [Event Hubs host.json reference](functions-bindings-event-hubs#host-json).

### Retry strategies

You can configure two retry strategies that are supported by policy:

A specified amount of time is allowed to elapse between each retry.

When you use a Consumption plan, you're billed only for the time that your function code is running. You aren't billed for the wait time between executions in either of these retry strategies.

### Maximum retry counts

You can configure the maximum number of times that a function execution is retried before eventual failure. The current retry count is stored in the memory of the instance.

It's possible for an instance to have a failure between retry attempts. When an instance fails during a retry policy, the retry count is lost. When there are instance failures, the Event Hubs trigger can resume processing and retry the batch on a new instance, with the retry count reset to zero. The timer trigger doesn't resume on a new instance.

This behavior means that the maximum retry count is a best effort. In some rare cases, an execution could be retried more than the requested maximum number of times. For timer triggers, the retries can be less than the requested maximum number.

### Retry examples

Examples are provided for both fixed delay and exponential backoff strategies. To see examples for a specific strategy, you must first select that strategy on the previous tab.

Function-level retries are supported with the following NuGet packages:

[Microsoft.Azure.Functions.Worker.Sdk](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Sdk)version 1.9.0 and later[Microsoft.Azure.Functions.Worker.Extensions.EventHubs](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventHubs)version 5.2.0 and later[Microsoft.Azure.Functions.Worker.Extensions.Kafka](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Kafka)version 3.8.0 and later[Microsoft.Azure.Functions.Worker.Extensions.Timer](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Timer)version 4.2.0 and later

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


| Property | Description |
|---|---|
`MaxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`DelayInterval` |
The delay used between retries. Specify it as a string with the format `HH:mm:ss` . |

Here's an example of a retry policy defined in the `function.json`

file:

```
{
"disabled": false,
"bindings": [
{
....
}
],
"retry": {
"strategy": "fixedDelay",
"maxRetryCount": 4,
"delayInterval": "00:00:10"
}
}
```


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixedDelay` and `exponentialBackoff` . |
`maxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delayInterval` |
The delay used between retries when you're using a `fixedDelay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimumInterval` |
The minimum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximumInterval` |
The maximum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

The way that you define the retry policy for the trigger depends on your Node.js version:

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
const { app } = require('@azure/functions');
app.timer('timerTriggerWithRetry', {
schedule: '0 */5 * * * *',
retry: {
strategy: 'fixedDelay',
delayInterval: {
seconds: 10,
},
maxRetryCount: 4,
},
handler: (myTimer, context) => {
if (context.retryContext?.retryCount < 2) {
throw new Error('Retry!');
} else {
context.log('Timer function processed request.');
}
},
});
```


The way that you define the retry policy for the trigger depends on your Node.js version:

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
import { app, InvocationContext, Timer } from '@azure/functions';
export async function timerTriggerWithRetry(myTimer: Timer, context: InvocationContext): Promise<void> {
if (context.retryContext?.retryCount < 2) {
throw new Error('Retry!');
} else {
context.log('Timer function processed request.');
}
}
app.timer('timerTriggerWithRetry', {
schedule: '0 */5 * * * *',
retry: {
strategy: 'fixedDelay',
delayInterval: {
seconds: 10,
},
maxRetryCount: 4,
},
handler: timerTriggerWithRetry,
});
```


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixedDelay` and `exponentialBackoff` . |
`maxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delayInterval` |
The delay used between retries when you're using a `fixedDelay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimumInterval` |
The minimum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximumInterval` |
The maximum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
import logging
from azure.functions import AuthLevel, Context, FunctionApp, TimerRequest
app = FunctionApp(http_auth_level=AuthLevel.ANONYMOUS)
@app.timer_trigger(schedule="*/1 * * * * *", arg_name="mytimer",
run_on_startup=False,
use_monitor=False)
@app.retry(strategy="fixed_delay", max_retry_count="3",
delay_interval="00:00:01")
def mytimer(mytimer: TimerRequest, context: Context) -> None:
logging.info(f'Current retry count: {context.retry_context.retry_count}')
if context.retry_context.retry_count == \
context.retry_context.max_retry_count:
logging.info(
f"Max retries of {context.retry_context.max_retry_count} for "
f"function {context.function_name} has been reached")
else:
raise Exception("This is a retryable exception")
```


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixed_delay` and `exponential_backoff` . |
`max_retry_count` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delay_interval` |
The delay used between retries when you're using a `fixed_delay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimum_interval` |
The minimum retry delay when you're using an `exponential_backoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximum_interval` |
The maximum retry delay when you're using an `exponential_backoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

```
@FunctionName("TimerTriggerJava1")
@FixedDelayRetry(maxRetryCount = 4, delayInterval = "00:00:10")
public void run(
@TimerTrigger(name = "timerInfo", schedule = "0 */5 * * * *") String timerInfo,
final ExecutionContext context
) {
context.getLogger().info("Java Timer trigger function executed at: " + LocalDateTime.now());
}
```


## Binding error codes

When you're integrating with Azure services, errors might originate from the APIs of the underlying services. Information that relates to binding-specific errors is available in the "Exceptions and return codes" sections of the following articles:

[Azure Cosmos DB](/en-us/rest/api/cosmos-db/http-status-codes-for-cosmosdb)[Blob Storage](functions-bindings-storage-blob-output#exceptions-and-return-codes)[Event Grid](../event-grid/troubleshoot-errors)[Event Hubs](functions-bindings-event-hubs-output#exceptions-and-return-codes)[IoT Hub](functions-bindings-event-iot-output#exceptions-and-return-codes)[Notification Hubs](functions-bindings-notification-hubs#exceptions-and-return-codes)[Queue Storage](functions-bindings-storage-queue-output#exceptions-and-return-codes)[Service Bus](functions-bindings-service-bus-output#exceptions-and-return-codes)[Table Storage](functions-bindings-storage-table-output#exceptions-and-return-codes)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-concurrency -->

# Concurrency in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure Functions, a single function app instance allows for multiple events to be processed concurrently. Because these run on the same compute instance, they share memory, CPU, and connection resources. In certain hosting plans, high demand on a specific instance causes the Functions host to automatically create new instances to handle the increased load. In these *dynamic scale* plans, there's a tradeoff between concurrency and scaling behaviors. To provide more control over how your app runs, Functions provides a way for you to manage the number of concurrent executions.

Functions provides two main ways of managing concurrency:

[Fixed per-instance concurrency](#fixed-per-instance-concurrency): You can configure host-level limits on concurrency that are specific to individual triggers. This model is the default concurrency behavior for Functions.[Dynamic concurrency](#dynamic-concurrency): For certain trigger types, the Functions host can automatically determine the best level of concurrency for that trigger in your function app. You must[opt in to this concurrency model](#dynamic-concurrency-configuration).

This article describes the concurrency behaviors of event-driven triggers in Functions and how these behaviors affect scaling in dynamic plans. It also compares the fixed per-instance and dynamic concurrency models.

## Scaling versus concurrency

For functions that use event-based triggers or respond to HTTP requests, you can quickly reach the limits of concurrent executions during periods of high demand. During such periods, you must be able to scale your function app by adding instances to avoid a backlog in processing incoming requests. The way that we scale your app depends on your hosting plan:

| Scale type | Hosting plans | Description |
|---|---|---|
| Dynamic (event-driven) scaling |
|

[Event-driven scaling in Azure Functions](event-driven-scaling).[Dedicated (App Service) plans](dedicated-plan)[set up an autoscale scheme](dedicated-plan#scaling).Before any scaling might occur, your function app attempts to handle increases in load by handling multiple invocations of the same type in a single instance. As a result, these concurrent executions on a given instance directly impact scale decisions. For instance, when an app in a dynamic scale plan hits a concurrency limit, it might need to scale to keep up with incoming demand.

The balance of scale versus concurrency you try to achieve in your app depends on where bottlenecks might occur: in processing (CPU-intensive process limitations) or in a downstream service (I/O-based limitations).

## Fixed per-instance concurrency

By default, most triggers support a fixed per-instance concurrency configuration model via [target-based scaling](functions-target-based-scaling). In this model, each trigger type has a per-instance concurrency limit.

You can override the concurrency default values for most triggers by setting a specific per-instance concurrency for that trigger type. For many triggers, you configure concurrency settings in the [host.json file](functions-host-json). For example, the [Azure Service Bus trigger](functions-bindings-service-bus-trigger) provides both a `MaxConcurrentCalls`

and a `MaxConcurrentSessions`

setting in *host.json*. These settings work together to control the maximum number of messages that each function app processes concurrently on each instance.

In certain target-based scaling scenarios, such as when you use an Apache Kafka or Azure Cosmos DB trigger, the concurrency configuration is in the function declaration, not in the *host.json* file. Other trigger types have built-in mechanisms for load balancing invocations across instances. For example, Azure Event Hubs and Azure Cosmos DB both use a partition-based scheme.

For trigger types that support concurrency configuration, the concurrency settings are applied to all running instances. This way, you can control the maximum concurrency for your functions on each instance. For example, when your function is CPU-intensive or resource-intensive, you might choose to limit concurrency to keep instances healthy. In this case, you can rely on scaling to handle increased loads. Similarly, when your function makes requests to a downstream service that's being throttled, you should also consider limiting concurrency to avoid overloading the downstream service.

## HTTP trigger concurrency

*Applies only to the Flex Consumption plan*

HTTP trigger concurrency is a special type of fixed per-instance concurrency. In HTTP trigger concurrency, the default concurrency also depends on the [instance size](flex-consumption-plan#instance-sizes).

The Flex Consumption plan scales all HTTP trigger functions together as a group. For more information, see [Per-function scaling](event-driven-scaling#per-function-scaling).

The following table indicates the default concurrency setting for HTTP triggers on a given instance, based on the configured instance memory size:

| Instance size (MB) | Default concurrency* |
|---|---|
| 512 | 4 |
| 2,048 | 16 |
| 4,096 | 32 |

*In Python apps, all instance sizes use an HTTP trigger concurrency level of one by default.

These default values should work well for most cases, and you can start with them. Consider that at a given number of HTTP requests, increasing the HTTP concurrency value reduces the number of instances required to handle HTTP requests. Likewise, decreasing the HTTP concurrency value requires more instances to handle the same load.

If you need to fine-tune the HTTP concurrency, you can do so by using the Azure CLI. For more information, see [Set HTTP concurrency limits](flex-consumption-how-to#set-http-concurrency-limits).

The default concurrency values in the preceding table apply only when you don't set your own HTTP concurrency setting. When you don't explicitly set an HTTP concurrency setting, the default concurrency increases as shown in the table when you change the instance size. After you specifically set an HTTP concurrency value, that value is maintained despite changes in the instance size.

## Determine optimal fixed per-instance concurrency

Fixed per-instance concurrency configurations give you control of certain trigger behaviors, such as throttling your functions. But it can be difficult to determine the optimal values for these settings. Generally, you have to arrive at acceptable values by an iterative process of load testing. Even after you determine a set of values that work for a particular load profile, the number of events that arrive from your connected services can change from day to day. This variability can cause your app to run with suboptimal values. For example, your function app might process demanding message payloads on the last day of the week, which requires you to throttle concurrency down. However, during the rest of the week, the message payloads might be lighter, which means you can use a higher concurrency level the rest of the week.

Ideally, the system should allow instances to process as much work as they can while keeping each instance healthy and latencies low. Dynamic concurrency is designed for that purpose.

## Dynamic concurrency

Functions provides a dynamic concurrency model that simplifies configuring concurrency for all function apps that run in the same plan.

Note

Dynamic concurrency is currently only supported for the Azure Blob Storage, Azure Queue Storage, and Service Bus triggers. Also, you must use the extension versions listed in [Extension support](#extension-support), later in this article.

### Benefits

Dynamic concurrency provides the following benefits:

**Simplified configuration**: You no longer have to manually determine per-trigger concurrency settings. The system learns the optimal values for your workload over time.**Dynamic adjustments**: Concurrency is adjusted up or down dynamically in real time, which allows the system to adapt to changing load patterns over time.**Instance health protection**: The runtime limits concurrency to levels that a function app instance can comfortably handle. These limits protect the app from overloading itself by taking on more work than it should.**Improved throughput**: Overall throughput is improved, because individual instances don't pull more work than they can quickly process. As a result, work is load-balanced more effectively across instances. For functions that can handle higher loads, higher throughput can be obtained by increasing concurrency to values above the default configuration.

### Dynamic concurrency configuration

You can turn on dynamic concurrency at the host level in the *host.json* file. When it's turned on, the concurrency levels of any binding extensions that support this feature are adjusted automatically as needed. In these cases, dynamic concurrency settings override any manually configured concurrency settings.

By default, dynamic concurrency is turned off. When you turn on dynamic concurrency, concurrency starts at a level of one for each function. The concurrency level is adjusted up to an optimal value, which the host determines.

You can turn on dynamic concurrency in your function app by adding the following settings to your *host.json* file:

```
{
"version": "2.0",
"concurrency": {
"dynamicConcurrencyEnabled": true,
"snapshotPersistenceEnabled": true
}
}
```


When `snapshotPersistenceEnabled`

is `true`

, which is the default value, the learned concurrency values are periodically persisted to storage. New instances start from those values instead of starting from a level of one and having to redo the learning.

### Concurrency manager

Behind the scenes, when dynamic concurrency is turned on, a concurrency manager process runs in the background. This manager constantly monitors instance health metrics, like CPU and thread utilization, and changes throttles as needed. When one or more throttles are turned on, function concurrency is adjusted down until the host is healthy again. When throttles are turned off, concurrency can increase. Various heuristics are used to intelligently adjust concurrency up or down as needed based on these throttles. Over time, concurrency for each function stabilizes to a particular level. Because it can take time to determine the optimal concurrency value, use dynamic concurrency only if a suboptimal value is acceptable for your solution initially or after a period of inactivity.

Concurrency levels are managed for each individual function. Specifically, the system balances between resource-intensive functions that require a low level of concurrency and more lightweight functions that can handle higher concurrency. The balance of concurrency for each function helps to maintain the overall health of the function app instance.

When dynamic concurrency is turned on, you find dynamic concurrency decisions in your logs. For example, log entries are added when various throttles are turned on, and whenever concurrency is adjusted up or down for each function. These logs are written under the **Host.Concurrency** log category in the **traces** table.

### Extension support

Dynamic concurrency is enabled for a function app at the host level, and any extensions that support dynamic concurrency run in that mode. Dynamic concurrency requires collaboration between the host and individual trigger extensions. Only the listed versions of the following extensions support dynamic concurrency.

| Extension | Version | Description |
|---|---|---|
Queue Storage |
|

`BatchSize`

and `NewBatchThreshold`

configuration options govern concurrency. When you use dynamic concurrency, those configuration values are ignored. Dynamic concurrency is integrated into the message loop, so the number of messages retrieved per iteration is dynamically adjusted. When throttles are turned on, the host is overloaded. Message processing is paused until the throttles are turned off. When the throttles are turned off, concurrency increases.**Blob Storage**[Version 5.x](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Storage)(Storage extension)**Service Bus**[Version 5.x](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ServiceBus)**Single dispatch topic/queue processing**: Each invocation of your function processes a single message. When you use a fixed per-instance configuration, the

`MaxConcurrentCalls`

configuration option governs concurrency. When you use dynamic concurrency, that configuration value is ignored, and concurrency is adjusted dynamically.**Session-based single dispatch topic/queue processing**: Each invocation of your function processes a single message. Depending on the number of active sessions for your topic or queue, each instance leases one or more sessions. Messages in each session are processed serially, to guarantee ordering in a session. When you don't use dynamic concurrency, the

`MaxConcurrentSessions`

setting governs concurrency. When dynamic concurrency is turned on, the `MaxConcurrentSessions`

value is ignored, and the number of sessions that each instance processes is dynamically adjusted.**Batch processing**: Each invocation of your function processes a batch of messages, governed by the

`MaxMessageCount`

setting. Because batch invocations are serial, concurrency for your batch-triggered function is always one, and dynamic concurrency doesn't apply.## Next steps

For more information, see the following resources:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-warmup -->

# Azure Functions warmup trigger

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to work with the warmup trigger in Azure Functions. A warmup trigger is invoked when an instance is added to scale a running function app. The warmup trigger lets you define a function that runs when a new instance of your function app is started. You can use a warmup trigger to preload custom dependencies so your functions are ready to start processing requests immediately. Some actions for a warmup trigger might include opening connections, loading dependencies, or running any other custom logic before your app begins receiving traffic.

The following considerations apply when using a warmup trigger:

- There can be only one warmup trigger function per function app, and it can't be invoked after the instance is already running.
- The name of the function that is the warmup trigger for your app should be
`warmup`

(case-insensitive). - The warmup trigger isn't available to apps running on the
[Consumption plan](consumption-plan). - The warmup trigger isn't supported on version 1.x of the Functions runtime.
- Support for the warmup trigger is provided by default in all development environments. You don't have to manually install the package or register the extension.
- The warmup trigger is only called during scale-out operations, not during restarts or other nonscaling startups. Make sure your logic can load all required dependencies without relying on the warmup trigger. Lazy loading is a good pattern to achieve this goal.
- Dependencies created by warmup trigger should be shared with other functions in your app. To learn more, see
[Static clients](manage-connections#static-clients). - If the
[built-in authentication](../app-service/overview-authentication-authorization)(also known as Easy Auth) is used,[HTTPS Only](../app-service/configure-ssl-bindings#enforce-https)should be enabled for the warmup trigger to get invoked.

## Example

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The following example shows a [C# function](dotnet-isolated-process-guide) that runs on each new instance when added to your app.

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.Logging;
namespace SampleApp
{
public static class Warmup
{
[Function(nameof(Warmup))]
public static void Run([WarmupTrigger] object warmupContext, FunctionContext context)
{
var logger = context.GetLogger(nameof(Warmup));
logger.LogInformation("Function App instance is now warm!");
}
}
}
```


The following example shows a warmup trigger that runs when each new instance is added to your app.

```
@FunctionName("Warmup")
public void warmup( @WarmupTrigger Object warmupContext, ExecutionContext context) {
context.getLogger().info("Function App instance is warm.");
}
```


The following example shows a [JavaScript function](functions-reference-node) with a warmup trigger that runs on each new instance when added to your app:

```
const { app } = require('@azure/functions');
app.warmup('warmupTrigger', {
handler: (warmupContext, context) => {
context.log('Function App instance is warm.');
},
});
```


The following example shows a [TypeScript function](functions-reference-node) with a warmup trigger that runs on each new instance when added to your app:

```
import { app, InvocationContext, WarmupContext } from '@azure/functions';
export async function warmupFunction(warmupContext: WarmupContext, context: InvocationContext): Promise<void> {
context.log('Function App instance is warm.');
}
app.warmup('warmup', {
handler: warmupFunction,
});
```


Here's the *function.json* file:

```
{
"bindings": [
{
"type": "warmupTrigger",
"direction": "in",
"name": "warmupContext"
}
]
}
```


PowerShell example code pending.

The following example shows a warmup trigger in a *function.json* file and a [Python function](functions-reference-python) that runs on each new instance when it'is added to your app.

Your function must be named `warmup`

(case-insensitive) and there can only be one warmup function per app.

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.warm_up_trigger('warmup')
def warmup(warmup) -> None:
logging.info('Function App instance is warm')
```


For more information, see [Configuration](#configuration).

## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the `WarmupTrigger`

attribute to define the function. C# script instead uses a [function.json configuration file](#configuration).

Use the `WarmupTrigger`

attribute to define the function. This attribute has no parameters.

## Annotations

Warmup triggers don't require annotations. Just use a name of `warmup`

(case-insensitive) for the `FunctionName`

annotation.

## Configuration

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Required - must be set to `warmupTrigger` . |
direction |
Required - must be set to `in` . |
name |
Required - the variable name used in function code. A `name` of `warmupContext` is recommended for the binding parameter. |

See the [Example section](#example) for complete examples.

## Usage

The following considerations apply to using a warmup function in C#:

- Your function must be named
`warmup`

(case-insensitive) using the`Function`

attribute. - A return value attribute isn't required.
- Use the
`Microsoft.Azure.Functions.Worker.Extensions.Warmup`

package - You can pass an object instance to the function.

Your function must be named `warmup`

(case-insensitive) using the `FunctionName`

annotation.

The function type in function.json must be set to `warmupTrigger`

.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache-trigger-redislist -->

# RedisListTrigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The `RedisListTrigger`

pops new elements from a list and surfaces those entries to the function.

For more information about Azure Cache for Redis triggers and bindings, [Redis Extension for Azure Functions](https://github.com/Azure/azure-functions-redis-extension/tree/main).

## Scope of availability for functions triggers

| Trigger Type | Azure Managed Redis | Azure Cache for Redis |
|---|---|---|
| Lists | Yes | Yes |

Important

When using Azure Managed Redis or the Enterprise tiers of Azure Cache for Redis, use port 10000 rather than port 6380 or 6379.

Important

Redis triggers aren't currently supported for functions running on a [Consumption plan](consumption-plan) or a [Flex Consumption plan](flex-consumption-plan).

Important

The Node.js v4 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Important

The Python v2 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v2 model works, refer to the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

## Example

Important

For .NET functions, using the *isolated worker* model is recommended over the *in-process* model. For a comparison of the *in-process* and *isolated worker* models, see differences between the *isolated worker* model and the *in-process* model for .NET on Azure Functions.

The following sample polls the key `listTest`

.:

```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.Functions.Worker.Extensions.Redis.Samples.RedisListTrigger
{
public class SimpleListTrigger
{
private readonly ILogger<SimpleListTrigger> logger;
public SimpleListTrigger(ILogger<SimpleListTrigger> logger)
{
this.logger = logger;
}
[Function(nameof(SimpleListTrigger))]
public void Run(
[RedisListTrigger(Common.connectionStringSetting, "listTest")] string entry)
{
logger.LogInformation(entry);
}
}
}
```


The following sample polls the key `listTest`

at a localhost Redis instance at `redisLocalhost`

:

```
package com.function.RedisListTrigger;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.redis.annotation.*;
public class SimpleListTrigger {
@FunctionName("SimpleListTrigger")
public void run(
@RedisListTrigger(
name = "req",
connection = "redisConnectionString",
key = "listTest",
pollingIntervalInMs = 1000,
maxBatchSize = 1)
String message,
final ExecutionContext context) {
context.getLogger().info(message);
}
}
```


This sample uses the same `index.js`

file, with binding data in the `function.json`

file.

Here's the `index.js`

file:

```
module.exports = async function (context, entry) {
context.log(entry);
}
```


From `function.json`

, here's the binding data:

```
{
"bindings": [
{
"type": "redisListTrigger",
"listPopFromBeginning": true,
"connection": "redisConnectionString",
"key": "listTest",
"pollingIntervalInMs": 1000,
"maxBatchSize": 16,
"name": "entry",
"direction": "in"
}
],
"scriptFile": "index.js"
}
```


This sample uses the same `run.ps1`

file, with binding data in the `function.json`

file.

Here's the `run.ps1`

file:

```
param($entry, $TriggerMetadata)
Write-Host $entry
```


From `function.json`

, here's the binding data:

```
{
"bindings": [
{
"type": "redisListTrigger",
"listPopFromBeginning": true,
"connection": "redisConnectionString",
"key": "listTest",
"pollingIntervalInMs": 1000,
"maxBatchSize": 16,
"name": "entry",
"direction": "in"
}
],
"scriptFile": "run.ps1"
}
```


This sample uses the same `__init__.py`

file, with binding data in the `function.json`

file.

The Python v1 programming model requires you to define bindings in a separate *function.json* file in the function folder. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-configuration#programming-model).

Here's the `__init__.py`

file:

```
import logging
def main(entry: str):
logging.info(entry)
```


From `function.json`

, here's the binding data:

```
{
"bindings": [
{
"type": "redisListTrigger",
"listPopFromBeginning": true,
"connection": "redisConnectionString",
"key": "listTest",
"pollingIntervalInMs": 1000,
"maxBatchSize": 16,
"name": "entry",
"direction": "in"
}
],
"scriptFile": "__init__.py"
}
```


## Attributes

| Parameter | Description | Required | Default |
|---|---|---|---|
`Connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`Key`

`INameResolver`

.`PollingIntervalInMs`

`1000`

`MessagesPerWorker`

`100`

`Count`

`COUNT`

argument in [and](https://redis.io/commands/lpop/)`LPOP`

[.](https://redis.io/commands/rpop/)`RPOP`

`10`

`ListPopFromBeginning`

[, or to pop entries from the end using](https://redis.io/commands/lpop/)`LPOP`

[.](https://redis.io/commands/rpop/)`RPOP`

`true`

## Annotations

| Parameter | Description | Required | Default |
|---|---|---|---|
`name` |
"entry" | ||
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`key`

`pollingIntervalInMs`

`1000`

`messagesPerWorker`

`100`

`count`

`10`

`listPopFromBeginning`

`true`

## Configuration

The following table explains the binding configuration properties that you set in the function.json file.

| function.json Property | Description | Optional | Default |
|---|---|---|---|
`type` |
Name of the trigger. | No | |
`listPopFromBeginning` |
Whether to delete the stream entries after the function has run. Set to `true` . |
Yes | `true` |
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`key`

`INameResolver`

.`pollingIntervalInMs`

`1000`

`messagesPerWorker`

`100`

`count`

`10`

`name`

`direction`

`in`

.See the Example section for complete examples.

## Usage

The `RedisListTrigger`

pops new elements from a list and surfaces those entries to the function. The trigger polls Redis at a configurable fixed interval, and uses [ LPOP](https://redis.io/commands/lpop/) and

[to pop entries from the lists.](https://redis.io/commands/rpop/)

`RPOP`

| Type | Description |
|---|---|
`byte[]` |
The message from the channel. |
`string` |
The message from the channel. |
`Custom` |
The trigger uses Json.NET serialization to map the message from the channel from a `string` into a custom type. |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-blob-input -->

# Azure Blob storage input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The input binding allows you to read blob storage data as input to an Azure Function.

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

[HTTP trigger: look up blob name from query string](#http-trigger-look-up-blob-name-from-query-string)[Queue trigger: receive blob name from queue message](#queue-trigger-receive-blob-name-from-queue-message)

#### HTTP trigger, look up blob name from query string

The following example shows a Java function that uses the `HttpTrigger`

annotation to receive a parameter containing the name of a file in a blob storage container. The `BlobInput`

annotation then reads the file and passes its contents to the function as a `byte[]`

.

```
@FunctionName("getBlobSizeHttp")
@StorageAccount("Storage_Account_Connection_String")
public HttpResponseMessage blobSize(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@BlobInput(
name = "file",
dataType = "binary",
path = "samples-workitems/{Query.file}")
byte[] content,
final ExecutionContext context) {
// build HTTP response with size of requested blob
return request.createResponseBuilder(HttpStatus.OK)
.body("The size of \"" + request.getQueryParameters().get("file") + "\" is: " + content.length + " bytes")
.build();
}
```


#### Queue trigger: receive blob name from queue message

The following example shows a Java function that uses the `QueueTrigger`

annotation to receive a message containing the name of a file in a blob storage container. The `BlobInput`

annotation then reads the file and passes its contents to the function as a `byte[]`

.

```
@FunctionName("getBlobSize")
@StorageAccount("Storage_Account_Connection_String")
public void blobSize(
@QueueTrigger(
name = "filename",
queueName = "myqueue-items-sample")
String filename,
@BlobInput(
name = "file",
dataType = "binary",
path = "samples-workitems/{queueTrigger}")
byte[] content,
final ExecutionContext context) {
context.getLogger().info("The size of \"" + filename + "\" is: " + content.length + " bytes");
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@BlobInput`

annotation on parameters whose value would come from a blob. This annotation can be used with native Java types, POJOs, or nullable values using `Optional<T>`

.

This example shows how to get the BlobClient from both a Storage Blob trigger and from the input binding on an HTTP trigger:

```
import "@azure/functions-extensions-blob"; // This is the mandatory first import for SDK binding
import { StorageBlobClient } from "@azure/functions-extensions-blob";
import { app, InvocationContext } from "@azure/functions";
export async function storageBlobTrigger(
blobStorageClient: StorageBlobClient, // SDK binding provides this client
context: InvocationContext
): Promise<void> {
context.log(`Blob trigger processing: ${context.triggerMetadata.name}`);
// Access to full SDK capabilities
const blobProperties = await blobStorageClient.blobClient.getProperties();
context.log(`Blob size: ${blobProperties.contentLength}`);
// Download blob content
const downloadResponse = await blobStorageClient.blobClient.download();
context.log(`Content: ${downloadResponse}`);
}
// Register the function
app.storageBlob("storageBlobTrigger", {
path: "snippets/{name}",
connection: "AzureWebJobsStorage",
sdkBinding: true, // Enable SDK binding
handler: storageBlobTrigger,
});
```


This example shows how to get the `ContainerClient`

from both a Storage Blob input binding using an HTTP trigger:

```
import "@azure/functions-extensions-blob"; // This is the mandatory first import for SDK binding
import { StorageBlobClient } from "@azure/functions-extensions-blob";
import {
app,
HttpRequest,
HttpResponseInit,
input,
InvocationContext,
} from "@azure/functions";
const blobInput = input.storageBlob({
path: "snippets",
connection: "AzureWebJobsStorage",
sdkBinding: true,
});
export async function listBlobs(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
// Get input binding for a specific container
const storageBlobClient = context.extraInputs.get(
blobInput
) as StorageBlobClient;
// List all blobs in the container
const blobs = [];
for await (const blob of storageBlobClient.containerClient.listBlobsFlat()) {
blobs.push(blob.name);
}
return { jsonBody: { blobs } };
}
app.http("listBlobs", {
methods: ["GET"],
authLevel: "function",
extraInputs: [blobInput],
handler: listBlobs,
});
```


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


The following example shows a blob input binding, defined in the *function.json* file, which makes the incoming blob data available to the [PowerShell](functions-reference-powershell) function.

Here's the json configuration:

```
{
"bindings": [
{
"name": "InputBlob",
"type": "blobTrigger",
"direction": "in",
"path": "source/{name}",
"connection": "AzureWebJobsStorage"
}
]
}
```


Here's the function code:

```
# Input bindings are passed in via param block.
param([byte[]] $InputBlob, $TriggerMetadata)
Write-Host "PowerShell Blob trigger: Name: $($TriggerMetadata.Name) Size: $($InputBlob.Length) bytes"
```


This example uses SDK types to directly access the underlying `BlobClient`

object provided by the Blob storage input binding:

```
import azure.functions as func
import azurefunctions.extensions.bindings.blob as blob
app = func.FunctionApp(http_auth_level=func.AuthLevel.FUNCTION)
@app.route(route="file")
@app.blob_input(
arg_name="client", path="PATH/TO/BLOB", connection="AzureWebJobsStorage"
)
def blob_input(req: func.HttpRequest, client: blob.BlobClient):
logging.info(
f"Python blob input function processed blob \n"
f"Properties: {client.get_blob_properties()}\n"
f"Blob content head: {client.download_blob().read(size=1)}"
)
return "ok"
```


For examples of using other SDK types, see the [ ContainerClient](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_containerclient/function_app.py) and

[samples. For a step-by-step tutorial on how to include SDK-type bindings in your function app, follow the](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_storagestreamdownloader/function_app.py)

`StorageStreamDownloader`

[Python SDK Bindings for Blob Sample](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-python).

To learn more, including what other SDK type bindings are supported, see [SDK type bindings](functions-reference-python#sdk-type-bindings).

The code creates a copy of a blob.

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="BlobOutput1")
@app.route(route="file")
@app.blob_input(arg_name="inputblob",
path="PATH/TO/BLOB",
connection="CONNECTION_SETTING")
@app.blob_output(arg_name="outputblob",
path="PATH/TO/NEW/BLOB",
connection="CONNECTION_SETTING")
def main(req: func.HttpRequest, inputblob: str, outputblob: func.Out[str]):
logging.info(f'Python Queue trigger function processed {len(inputblob)} bytes')
outputblob.set(inputblob)
return "ok"
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#blob-input).

Isolated worker process defines an input binding by using a `BlobInputAttribute`

attribute, which takes the following parameters:

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
`data_type` |
For dynamically typed languages, specifies the underlying data type. Possible values are `string` , `binary` , or `stream` . For more detail, refer to the
|

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

The `@BlobInput`

attribute gives you access to the blob that triggered the function. If you use a byte array with the attribute, set `dataType`

to `binary`

. Refer to the [input example](#example) for details.

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `input.storageBlob()`

method.

| Property | Description |
|---|---|
path |
The path to the blob. |
connection |
The name of an app setting or setting collection that specifies how to connect to Azure Blobs. See
|

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `blob` . |
direction |
Must be set to `in` . Exceptions are noted in the
|
name |
The name of the variable that represents the blob in function code. |
path |
The path to the blob. |
connection |
The name of an app setting or setting collection that specifies how to connect to Azure Blobs. See
|

**dataType**`string`

, `binary`

, or `stream`

. For more detail, refer to the [triggers and bindings concepts](functions-triggers-bindings?tabs=python#trigger-and-binding-definitions).See the [Example section](#example) for complete examples.

## Usage

The binding types supported by Blob input depend on the extension package version and the C# modality used in your function app.

When you want the function to process a single blob, the blob input binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The blob content as a string. Use when the blob content is simple text. |
`byte[]` |
The bytes of the blob content. |
| JSON serializable types | When a blob contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

[BlobClient](/en-us/dotnet/api/azure.storage.blobs.blobclient)1,[BlockBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blockblobclient)1,[PageBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.pageblobclient)1,[AppendBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.appendblobclient)1,[BlobBaseClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blobbaseclient)1When you want the function to process multiple blobs from a container, the blob input binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` or `List<T>` where `T` is one of the single blob input binding types |
An array or list of multiple blobs. Each entry represents one blob from the container. You can also bind to any interfaces implemented by these types, such as `IEnumerable<T>` . |
1 |

1 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs 6.0.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs/6.0.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

Binding to `string`

, or `Byte[]`

is only recommended when the blob size is small, since the entire blob contents are loaded into memory. For most blobs, use a `Stream`

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

The `@BlobInput`

attribute gives you access to the blob that triggered the function. If you use a byte array with the attribute, set `dataType`

to `binary`

. Refer to the [input example](#example) for details.

Access the blob data via a parameter that matches the name designated by binding's name parameter in the *function.json* file.

Access blob data via the parameter typed as [InputStream](/en-us/python/api/azure-functions/azure.functions.inputstream). Refer to the [input example](#example) for details.

Functions also supports Python SDK type bindings for Azure Blob storage, which lets you work with blob data using these underlying SDK types:

Note

Only synchronous SDK types are supported.

Important

SDK types support for Python is generally available and is only supported for the Python v2 programming model. For more information, see [SDK types in Python](functions-reference-python#sdk-type-bindings).

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/self-hosted-mcp-servers -->

# Self-hosted remote MCP server on Azure Functions (public preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions provides two ways of hosting remote MCP servers:

- MCP servers created with the
[Functions MCP extension](functions-bindings-mcp) - MCP servers built with the
[official MCP SDKs](https://modelcontextprotocol.io/docs/sdk)

With the first approach, you can use the Azure Functions programming model with triggers and bindings to build the MCP server. Then, you can host the server remotely by deploying it to a Function app.

If you already have an MCP server created with the official MCP SDKs and just want to host it remotely, the second approach likely suits your needs. You don't need to make any code changes to the server to host it on Azure Functions. Instead, you can add the required Functions artifacts, and the server is ready to be deployed. As such, these servers are referred to as *self-hosted MCP servers*.


This article provides an overview of self-hosted MCP servers and links to relevant articles and samples.

## Custom handlers

Self-hosted MCP servers deploy to the Azure Functions platform as *custom handlers*. Custom handlers are lightweight web servers that receive events from the Functions host. They provide a way to run on the Functions platform applications built with frameworks different from the Functions programming model or in languages not supported out-of-the-box. For more information, see [Azure Functions custom handlers](functions-custom-handlers).

When you deploy an MCP SDK based server to Azure Functions, you must include a *host.json* in your project. The minimal *host.json* looks like this:

```
{
"version": "2.0",
"configurationProfile": "mcp-custom-handler",
"customHandler": {
"description": {
"defaultExecutablePath": "python",
"arguments": ["Path to main script file, e.g. hello_world.py"]
},
"port": "<MCP server port>"
}
}
```


```
{
"version": "2.0",
"configurationProfile": "mcp-custom-handler",
"customHandler": {
"description": {
"defaultExecutablePath": "npm",
"arguments": ["run", "start"]
},
"port": "<MCP server port>"
}
}
```


```
{
"version": "2.0",
"configurationProfile": "mcp-custom-handler",
"customHandler": {
"description": {
"defaultExecutablePath": "dotnet",
"arguments": ["Path to the compiled DLL, e.g. HelloWorld.dll"]
},
"port": "<MCP server port>"
}
}
```


Note

Because the payload deployed to Azure Functions is the content of the `bin/output`

directory, the path to the compiled DLL is relative to that directory, *not* to the project root.

Example not yet available.

Using a `configuration Profile`

value of `mcp-custom-handler`

automatically configures these Functions host settings, which are required for running your MCP server in Azure Functions:

`http.enableProxying`

to`true`

`http.routes`

to`[{ "route": "{*route}" }]`

`extensions.http.routePrefix`

to`""`


This example shows a host.json file with extra custom handler properties set equivalent to using the `mcp-custom-handler`

profile:

```
{
"version": "2.0",
"extensions": {
"http": {
"routePrefix": ""
}
},
"customHandler": {
"description": {
"defaultExecutablePath": "",
"arguments": [""]
},
"http": {
"enableProxying": true,
"defaultAuthorizationLevel": "anonymous",
"routes": [
{
"route": "{*route}",
// Default authorization level is `defaultAuthorizationLevel`
},
{
"route": "admin/{*route}",
"authorizationLevel": "admin"
}
]
}
}
}
```


This table explains the properties of `customHandler.http`

, along with default values:

| Property | What it does | Default value |
|---|---|---|
`enableProxying` |
Controls how the Azure Functions host handles HTTP requests to custom handlers. When `enableProxying` is set to `true` , the Functions host acts as a reverse proxy and forwards the entire HTTP request (including headers, body, query parameters) directly to the custom handler. This setting gives the custom handler full access to the original HTTP request details. When `enableProxying` is `false` , the Functions host processes the request first and transforms it into the Azure Functions request/response format before passing it to the custom handler. |
`false` |
`defaultAuthorizationLevel` |
Controls the authentication requirement for accessing custom handler endpoints. For example, `function` requires a function-specific API key to access. For more information, see
|
`function` |
`route` |
Specifies the URL path pattern that the custom handler responds to. `{*route}` matches any URL path (such as `/` , `/mcp` , `/api/tools` , or `/anything/nested/path` ) and forwards the request to the custom handler. |
`{*route}` |

## Built-in server authentication

OAuth-based authentication and authorization provided by the App Service platform implements the requirements of the [MCP authorization specification](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization), such as issuing 401 challenge and exposing the Protected Resource Metadata (PRM) document. When you enable built-in authentication, clients attempting to access the server are redirected to identity providers like Microsoft Entra ID for authentication before connecting.

For more information, see [Configure built-in server authorization (preview)](../app-service/configure-authentication-mcp) and [Hosting MCP servers on Azure Functions](functions-mcp-tutorial).

## Azure AI Foundry agent integrations

Agents in Azure AI Foundry can be [configured to use tools](functions-mcp-tutorial#configure-azure-ai-foundry-agent-to-use-your-tools) in MCP servers hosted in Azure Functions.

## Register your server in Azure API Center

When you register your MCP server in Azure API Center, you create a private organizational tool catalog. This approach is recommended for sharing MCP servers across your organization with consistent governance and discoverability. For more information, see [Register MCP servers hosted in Azure Functions in Azure API Center](register-mcp-server-api-center).

## Public preview support

The ability to host your own SDK-based MCP servers in Functions is currently in preview and supports these features:

**Stateless**servers that use the**streamable-http**transport. If you need your server to be stateful, consider using the Functions MCP extension.- Servers implemented with the Python, TypeScript, C#, or Java MCP SDKs.
- When running the project locally, you must use the Azure Functions Core Tools (
`func start`

command). You can't currently use`F5`

to start running with the debugger. - Servers must be hosted as
[Flex Consumption plan](flex-consumption-plan)apps.

## Samples

Not yet available.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-warmup -->

# Azure Functions warmup trigger

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to work with the warmup trigger in Azure Functions. A warmup trigger is invoked when an instance is added to scale a running function app. The warmup trigger lets you define a function that runs when a new instance of your function app is started. You can use a warmup trigger to preload custom dependencies so your functions are ready to start processing requests immediately. Some actions for a warmup trigger might include opening connections, loading dependencies, or running any other custom logic before your app begins receiving traffic.

The following considerations apply when using a warmup trigger:

- There can be only one warmup trigger function per function app, and it can't be invoked after the instance is already running.
- The name of the function that is the warmup trigger for your app should be
`warmup`

(case-insensitive). - The warmup trigger isn't available to apps running on the
[Consumption plan](consumption-plan). - The warmup trigger isn't supported on version 1.x of the Functions runtime.
- Support for the warmup trigger is provided by default in all development environments. You don't have to manually install the package or register the extension.
- The warmup trigger is only called during scale-out operations, not during restarts or other nonscaling startups. Make sure your logic can load all required dependencies without relying on the warmup trigger. Lazy loading is a good pattern to achieve this goal.
- Dependencies created by warmup trigger should be shared with other functions in your app. To learn more, see
[Static clients](manage-connections#static-clients). - If the
[built-in authentication](../app-service/overview-authentication-authorization)(also known as Easy Auth) is used,[HTTPS Only](../app-service/configure-ssl-bindings#enforce-https)should be enabled for the warmup trigger to get invoked.

## Example

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The following example shows a [C# function](dotnet-isolated-process-guide) that runs on each new instance when added to your app.

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.Logging;
namespace SampleApp
{
public static class Warmup
{
[Function(nameof(Warmup))]
public static void Run([WarmupTrigger] object warmupContext, FunctionContext context)
{
var logger = context.GetLogger(nameof(Warmup));
logger.LogInformation("Function App instance is now warm!");
}
}
}
```


The following example shows a warmup trigger that runs when each new instance is added to your app.

```
@FunctionName("Warmup")
public void warmup( @WarmupTrigger Object warmupContext, ExecutionContext context) {
context.getLogger().info("Function App instance is warm.");
}
```


The following example shows a [JavaScript function](functions-reference-node) with a warmup trigger that runs on each new instance when added to your app:

```
const { app } = require('@azure/functions');
app.warmup('warmupTrigger', {
handler: (warmupContext, context) => {
context.log('Function App instance is warm.');
},
});
```


The following example shows a [TypeScript function](functions-reference-node) with a warmup trigger that runs on each new instance when added to your app:

```
import { app, InvocationContext, WarmupContext } from '@azure/functions';
export async function warmupFunction(warmupContext: WarmupContext, context: InvocationContext): Promise<void> {
context.log('Function App instance is warm.');
}
app.warmup('warmup', {
handler: warmupFunction,
});
```


Here's the *function.json* file:

```
{
"bindings": [
{
"type": "warmupTrigger",
"direction": "in",
"name": "warmupContext"
}
]
}
```


PowerShell example code pending.

The following example shows a warmup trigger in a *function.json* file and a [Python function](functions-reference-python) that runs on each new instance when it'is added to your app.

Your function must be named `warmup`

(case-insensitive) and there can only be one warmup function per app.

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.warm_up_trigger('warmup')
def warmup(warmup) -> None:
logging.info('Function App instance is warm')
```


For more information, see [Configuration](#configuration).

## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the `WarmupTrigger`

attribute to define the function. C# script instead uses a [function.json configuration file](#configuration).

Use the `WarmupTrigger`

attribute to define the function. This attribute has no parameters.

## Annotations

Warmup triggers don't require annotations. Just use a name of `warmup`

(case-insensitive) for the `FunctionName`

annotation.

## Configuration

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Required - must be set to `warmupTrigger` . |
direction |
Required - must be set to `in` . |
name |
Required - the variable name used in function code. A `name` of `warmupContext` is recommended for the binding parameter. |

See the [Example section](#example) for complete examples.

## Usage

The following considerations apply to using a warmup function in C#:

- Your function must be named
`warmup`

(case-insensitive) using the`Function`

attribute. - A return value attribute isn't required.
- Use the
`Microsoft.Azure.Functions.Worker.Extensions.Warmup`

package - You can pass an object instance to the function.

Your function must be named `warmup`

(case-insensitive) using the `FunctionName`

annotation.

The function type in function.json must be set to `warmupTrigger`

.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-signalr-service-output -->

# SignalR Service output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the *SignalR* output binding to send one or more messages using Azure SignalR Service. You can broadcast a message to:

- All connected clients
- Connected clients in a specified group
- Connected clients authenticated to a specific user

The output binding also allows you to manage groups, such as adding a client or user to a group, removing a client or user from a group.

For information on setup and configuration details, see the [overview](functions-bindings-signalr-service).

## Example

### Broadcast to all clients

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The following example shows a function that sends a message using the output binding to all connected clients. The *newMessage* is the name of the method to be invoked on each client.

```
[Function(nameof(BroadcastToAll))]
[SignalROutput(HubName = "chat", ConnectionStringSetting = "SignalRConnection")]
public static SignalRMessageAction BroadcastToAll([HttpTrigger(AuthorizationLevel.Anonymous, "post")] HttpRequestData req)
{
using var bodyReader = new StreamReader(req.Body);
return new SignalRMessageAction("newMessage")
{
// broadcast to all the connected clients without specifying any connection, user or group.
Arguments = new[] { bodyReader.ReadToEnd() },
};
}
```


Here's binding data in the *function.json* file:

Example function.json:

```
{
"type": "signalR",
"name": "signalROutput",
"hubName": "hubName1",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "out"
}
```


```
const { app, output } = require('@azure/functions');
const signalR = output.generic({
type: 'signalR',
name: 'signalR',
hubName: 'hub',
connectionStringSetting: 'AzureSignalRConnectionString',
});
// You can use any other trigger type instead.
app.http('broadcast', {
methods: ['GET'],
authLevel: 'anonymous',
extraOutputs: [signalR],
handler: (request, context) => {
context.extraOutputs.set(signalR, {
"target": "newMessage",
"arguments": [request.body]
});
}
});
```


Complete PowerShell examples are pending.

Here's the Python code:

```
def main(req: func.HttpRequest, signalROutput: func.Out[str]) -> func.HttpResponse:
message = req.get_json()
signalROutput.set(json.dumps({
'target': 'newMessage',
'arguments': [ message ]
}))
```


```
@FunctionName("sendMessage")
@SignalROutput(name = "$return", HubName = "hubName1")
public SignalRMessage sendMessage(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST },
authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Object> req) {
SignalRMessage message = new SignalRMessage();
message.target = "newMessage";
message.arguments.add(req.getBody());
return message;
}
```


### Send to a user

You can send a message only to connections that have been authenticated to a user by setting the *user ID* in the SignalR message.

```
[Function(nameof(SendToUser))]
[SignalROutput(HubName = "chat", ConnectionStringSetting = "SignalRConnection")]
public static SignalRMessageAction SendToUser([HttpTrigger(AuthorizationLevel.Anonymous, "post")] HttpRequestData req)
{
using var bodyReader = new StreamReader(req.Body);
return new SignalRMessageAction("newMessage")
{
Arguments = new[] { bodyReader.ReadToEnd() },
UserId = "userToSend",
};
}
```


Here's binding data in the *function.json* file:

Example function.json:

```
{
"type": "signalR",
"name": "signalROutput",
"hubName": "hubName1",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "out"
}
```


Complete PowerShell examples are pending.

Here's the Python code:

```
def main(req: func.HttpRequest, signalROutput: func.Out[str]) -> func.HttpResponse:
message = req.get_json()
signalROutput.set(json.dumps({
#message will only be sent to this user ID
'userId': 'userId1',
'target': 'newMessage',
'arguments': [ message ]
}))
```


```
@FunctionName("sendMessage")
@SignalROutput(name = "$return", HubName = "hubName1")
public SignalRMessage sendMessage(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST },
authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Object> req) {
SignalRMessage message = new SignalRMessage();
message.userId = "userId1";
message.target = "newMessage";
message.arguments.add(req.getBody());
return message;
}
```


```
const { app, output } = require('@azure/functions');
const signalR = output.generic({
type: 'signalR',
name: 'signalR',
hubName: 'hub',
connectionStringSetting: 'AzureSignalRConnectionString',
});
app.http('sendToUser', {
methods: ['GET'],
authLevel: 'anonymous',
extraOutputs: [signalR],
handler: (request, context) => {
context.extraOutputs.set(signalR, {
"target": "newMessage",
"arguments": [request.body],
"userId": "userId1",
});
}
});
```


### Send to a group

You can send a message only to connections that have been added to a group by setting the *group name* in the SignalR message.

```
[Function(nameof(SendToGroup))]
[SignalROutput(HubName = "chat", ConnectionStringSetting = "SignalRConnection")]
public static SignalRMessageAction SendToGroup([HttpTrigger(AuthorizationLevel.Anonymous, "post")] HttpRequestData req)
{
using var bodyReader = new StreamReader(req.Body);
return new SignalRMessageAction("newMessage")
{
Arguments = new[] { bodyReader.ReadToEnd() },
GroupName = "groupToSend"
};
}
```


Here's binding data in the *function.json* file:

Example function.json:

```
{
"type": "signalR",
"name": "signalROutput",
"hubName": "hubName1",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "out"
}
```


```
const { app, output } = require('@azure/functions');
const signalR = output.generic({
type: 'signalR',
name: 'signalR',
hubName: 'hub',
connectionStringSetting: 'AzureSignalRConnectionString',
});
app.http('sendToGroup', {
methods: ['GET'],
authLevel: 'anonymous',
extraOutputs: [signalR],
handler: (request, context) => {
context.extraOutputs.set(signalR, {
"target": "newMessage",
"arguments": [request.body],
"groupName": "myGroup",
});
}
});
```


Complete PowerShell examples are pending.

Here's the Python code:

```
def main(req: func.HttpRequest, signalROutput: func.Out[str]) -> func.HttpResponse:
message = req.get_json()
signalROutput.set(json.dumps({
#message will only be sent to this group
'groupName': 'myGroup',
'target': 'newMessage',
'arguments': [ message ]
}))
```


```
@FunctionName("sendMessage")
@SignalROutput(name = "$return", HubName = "hubName1")
public SignalRMessage sendMessage(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST },
authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Object> req) {
SignalRMessage message = new SignalRMessage();
message.groupName = "myGroup";
message.target = "newMessage";
message.arguments.add(req.getBody());
return message;
}
```


### Group management

SignalR Service allows users or connections to be added to groups. Messages can then be sent to a group. You can use the `SignalR`

output binding to manage groups.

Specify `SignalRGroupActionType`

to add or remove a member. The following example removes a user from a group.

```
[Function(nameof(RemoveFromGroup))]
[SignalROutput(HubName = "chat", ConnectionStringSetting = "SignalRConnection")]
public static SignalRGroupAction RemoveFromGroup([HttpTrigger(AuthorizationLevel.Anonymous, "post")] HttpRequestData req)
{
return new SignalRGroupAction(SignalRGroupActionType.Remove)
{
GroupName = "group1",
UserId = "user1"
};
}
```


Note

In order to get the `ClaimsPrincipal`

correctly bound, you must have configured the authentication settings in Azure Functions.

Here's binding data in the *function.json* file:

Example function.json:

```
{
"type": "signalR",
"name": "signalROutput",
"hubName": "hubName1",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "out"
}
```


```
const { app, output } = require('@azure/functions');
const signalR = output.generic({
type: 'signalR',
name: 'signalR',
hubName: 'hub',
connectionStringSetting: 'AzureSignalRConnectionString',
});
// The following function adds a user to a group
app.http('addUserToGroup', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [signalR],
handler: (request, context) => {
context.extraOutputs.set(signalR, {
"userId": req.query.userId,
"groupName": "myGroup",
"action": "add"
});
}
});
// The following function removes a user from a group
app.http('removeUserFromGroup', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [signalR],
handler: (request, context) => {
context.extraOutputs.set(signalR, {
"userId": req.query.userId,
"groupName": "myGroup",
"action": "remove"
});
}
});
```


Complete PowerShell examples are pending.

The following example adds a user to a group.

```
def main(req: func.HttpRequest, signalROutput: func.Out[str]) -> func.HttpResponse:
signalROutput.set(json.dumps({
'userId': 'userId1',
'groupName': 'myGroup',
'action': 'add'
}))
```


The following example removes a user from a group.

```
def main(req: func.HttpRequest, signalROutput: func.Out[str]) -> func.HttpResponse:
signalROutput.set(json.dumps({
'userId': 'userId1',
'groupName': 'myGroup',
'action': 'remove'
}))
```


The following example adds a user to a group.

```
@FunctionName("addToGroup")
@SignalROutput(name = "$return", HubName = "hubName1")
public SignalRGroupAction addToGroup(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST },
authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Object> req,
@BindingName("userId") String userId) {
SignalRGroupAction groupAction = new SignalRGroupAction();
groupAction.action = "add";
groupAction.userId = userId;
groupAction.groupName = "myGroup";
return action;
}
```


The following example removes a user from a group.

```
@FunctionName("removeFromGroup")
@SignalROutput(name = "$return", HubName = "hubName1")
public SignalRGroupAction removeFromGroup(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST },
authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Object> req,
@BindingName("userId") String userId) {
SignalRGroupAction groupAction = new SignalRGroupAction();
groupAction.action = "remove";
groupAction.userId = userId;
groupAction.groupName = "myGroup";
return action;
}
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attribute to define the function. C# script instead uses a [function.json configuration file](#configuration).

The following table explains the properties of the `SignalROutput`

attribute.

| Attribute property | Description |
|---|---|
HubName |
This value must be set to the name of the SignalR hub for which the connection information is generated. |
ConnectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |

## Annotations

The following table explains the supported settings for the `SignalROutput`

annotation.

| Setting | Description |
|---|---|
name |
Variable name used in function code for connection info object. |
hubName |
This value must be set to the name of the SignalR hub for which the connection information is generated. |
connectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `signalR` . |
direction |
Must be set to `out` . |
name |
Variable name used in function code for connection info object. |
hubName |
This value must be set to the name of the SignalR hub for which the connection information is generated. |
connectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

For optimal security, your function app should use managed identities when connecting to the Azure SignalR service instead of using a connection string, which contains a shared secret key. For more information, see [Authorize requests to Azure SignalR Service resources with Microsoft Entra managed identities](../azure-signalr/signalr-howto-authorize-managed-identity#azure-signalr-service-bindings-in-azure-functions).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-blob-input -->

# Azure Blob storage input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The input binding allows you to read blob storage data as input to an Azure Function.

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

[HTTP trigger: look up blob name from query string](#http-trigger-look-up-blob-name-from-query-string)[Queue trigger: receive blob name from queue message](#queue-trigger-receive-blob-name-from-queue-message)

#### HTTP trigger, look up blob name from query string

The following example shows a Java function that uses the `HttpTrigger`

annotation to receive a parameter containing the name of a file in a blob storage container. The `BlobInput`

annotation then reads the file and passes its contents to the function as a `byte[]`

.

```
@FunctionName("getBlobSizeHttp")
@StorageAccount("Storage_Account_Connection_String")
public HttpResponseMessage blobSize(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@BlobInput(
name = "file",
dataType = "binary",
path = "samples-workitems/{Query.file}")
byte[] content,
final ExecutionContext context) {
// build HTTP response with size of requested blob
return request.createResponseBuilder(HttpStatus.OK)
.body("The size of \"" + request.getQueryParameters().get("file") + "\" is: " + content.length + " bytes")
.build();
}
```


#### Queue trigger: receive blob name from queue message

The following example shows a Java function that uses the `QueueTrigger`

annotation to receive a message containing the name of a file in a blob storage container. The `BlobInput`

annotation then reads the file and passes its contents to the function as a `byte[]`

.

```
@FunctionName("getBlobSize")
@StorageAccount("Storage_Account_Connection_String")
public void blobSize(
@QueueTrigger(
name = "filename",
queueName = "myqueue-items-sample")
String filename,
@BlobInput(
name = "file",
dataType = "binary",
path = "samples-workitems/{queueTrigger}")
byte[] content,
final ExecutionContext context) {
context.getLogger().info("The size of \"" + filename + "\" is: " + content.length + " bytes");
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@BlobInput`

annotation on parameters whose value would come from a blob. This annotation can be used with native Java types, POJOs, or nullable values using `Optional<T>`

.

This example shows how to get the BlobClient from both a Storage Blob trigger and from the input binding on an HTTP trigger:

```
import "@azure/functions-extensions-blob"; // This is the mandatory first import for SDK binding
import { StorageBlobClient } from "@azure/functions-extensions-blob";
import { app, InvocationContext } from "@azure/functions";
export async function storageBlobTrigger(
blobStorageClient: StorageBlobClient, // SDK binding provides this client
context: InvocationContext
): Promise<void> {
context.log(`Blob trigger processing: ${context.triggerMetadata.name}`);
// Access to full SDK capabilities
const blobProperties = await blobStorageClient.blobClient.getProperties();
context.log(`Blob size: ${blobProperties.contentLength}`);
// Download blob content
const downloadResponse = await blobStorageClient.blobClient.download();
context.log(`Content: ${downloadResponse}`);
}
// Register the function
app.storageBlob("storageBlobTrigger", {
path: "snippets/{name}",
connection: "AzureWebJobsStorage",
sdkBinding: true, // Enable SDK binding
handler: storageBlobTrigger,
});
```


This example shows how to get the `ContainerClient`

from both a Storage Blob input binding using an HTTP trigger:

```
import "@azure/functions-extensions-blob"; // This is the mandatory first import for SDK binding
import { StorageBlobClient } from "@azure/functions-extensions-blob";
import {
app,
HttpRequest,
HttpResponseInit,
input,
InvocationContext,
} from "@azure/functions";
const blobInput = input.storageBlob({
path: "snippets",
connection: "AzureWebJobsStorage",
sdkBinding: true,
});
export async function listBlobs(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
// Get input binding for a specific container
const storageBlobClient = context.extraInputs.get(
blobInput
) as StorageBlobClient;
// List all blobs in the container
const blobs = [];
for await (const blob of storageBlobClient.containerClient.listBlobsFlat()) {
blobs.push(blob.name);
}
return { jsonBody: { blobs } };
}
app.http("listBlobs", {
methods: ["GET"],
authLevel: "function",
extraInputs: [blobInput],
handler: listBlobs,
});
```


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


The following example shows a blob input binding, defined in the *function.json* file, which makes the incoming blob data available to the [PowerShell](functions-reference-powershell) function.

Here's the json configuration:

```
{
"bindings": [
{
"name": "InputBlob",
"type": "blobTrigger",
"direction": "in",
"path": "source/{name}",
"connection": "AzureWebJobsStorage"
}
]
}
```


Here's the function code:

```
# Input bindings are passed in via param block.
param([byte[]] $InputBlob, $TriggerMetadata)
Write-Host "PowerShell Blob trigger: Name: $($TriggerMetadata.Name) Size: $($InputBlob.Length) bytes"
```


This example uses SDK types to directly access the underlying `BlobClient`

object provided by the Blob storage input binding:

```
import azure.functions as func
import azurefunctions.extensions.bindings.blob as blob
app = func.FunctionApp(http_auth_level=func.AuthLevel.FUNCTION)
@app.route(route="file")
@app.blob_input(
arg_name="client", path="PATH/TO/BLOB", connection="AzureWebJobsStorage"
)
def blob_input(req: func.HttpRequest, client: blob.BlobClient):
logging.info(
f"Python blob input function processed blob \n"
f"Properties: {client.get_blob_properties()}\n"
f"Blob content head: {client.download_blob().read(size=1)}"
)
return "ok"
```


For examples of using other SDK types, see the [ ContainerClient](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_containerclient/function_app.py) and

[samples. For a step-by-step tutorial on how to include SDK-type bindings in your function app, follow the](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_storagestreamdownloader/function_app.py)

`StorageStreamDownloader`

[Python SDK Bindings for Blob Sample](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-python).

To learn more, including what other SDK type bindings are supported, see [SDK type bindings](functions-reference-python#sdk-type-bindings).

The code creates a copy of a blob.

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="BlobOutput1")
@app.route(route="file")
@app.blob_input(arg_name="inputblob",
path="PATH/TO/BLOB",
connection="CONNECTION_SETTING")
@app.blob_output(arg_name="outputblob",
path="PATH/TO/NEW/BLOB",
connection="CONNECTION_SETTING")
def main(req: func.HttpRequest, inputblob: str, outputblob: func.Out[str]):
logging.info(f'Python Queue trigger function processed {len(inputblob)} bytes')
outputblob.set(inputblob)
return "ok"
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#blob-input).

Isolated worker process defines an input binding by using a `BlobInputAttribute`

attribute, which takes the following parameters:

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
`data_type` |
For dynamically typed languages, specifies the underlying data type. Possible values are `string` , `binary` , or `stream` . For more detail, refer to the
|

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

The `@BlobInput`

attribute gives you access to the blob that triggered the function. If you use a byte array with the attribute, set `dataType`

to `binary`

. Refer to the [input example](#example) for details.

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `input.storageBlob()`

method.

| Property | Description |
|---|---|
path |
The path to the blob. |
connection |
The name of an app setting or setting collection that specifies how to connect to Azure Blobs. See
|

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `blob` . |
direction |
Must be set to `in` . Exceptions are noted in the
|
name |
The name of the variable that represents the blob in function code. |
path |
The path to the blob. |
connection |
The name of an app setting or setting collection that specifies how to connect to Azure Blobs. See
|

**dataType**`string`

, `binary`

, or `stream`

. For more detail, refer to the [triggers and bindings concepts](functions-triggers-bindings?tabs=python#trigger-and-binding-definitions).See the [Example section](#example) for complete examples.

## Usage

The binding types supported by Blob input depend on the extension package version and the C# modality used in your function app.

When you want the function to process a single blob, the blob input binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The blob content as a string. Use when the blob content is simple text. |
`byte[]` |
The bytes of the blob content. |
| JSON serializable types | When a blob contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

[BlobClient](/en-us/dotnet/api/azure.storage.blobs.blobclient)1,[BlockBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blockblobclient)1,[PageBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.pageblobclient)1,[AppendBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.appendblobclient)1,[BlobBaseClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blobbaseclient)1When you want the function to process multiple blobs from a container, the blob input binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` or `List<T>` where `T` is one of the single blob input binding types |
An array or list of multiple blobs. Each entry represents one blob from the container. You can also bind to any interfaces implemented by these types, such as `IEnumerable<T>` . |
1 |

1 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs 6.0.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs/6.0.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

Binding to `string`

, or `Byte[]`

is only recommended when the blob size is small, since the entire blob contents are loaded into memory. For most blobs, use a `Stream`

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

The `@BlobInput`

attribute gives you access to the blob that triggered the function. If you use a byte array with the attribute, set `dataType`

to `binary`

. Refer to the [input example](#example) for details.

Access the blob data via a parameter that matches the name designated by binding's name parameter in the *function.json* file.

Access blob data via the parameter typed as [InputStream](/en-us/python/api/azure-functions/azure.functions.inputstream). Refer to the [input example](#example) for details.

Functions also supports Python SDK type bindings for Azure Blob storage, which lets you work with blob data using these underlying SDK types:

Note

Only synchronous SDK types are supported.

Important

SDK types support for Python is generally available and is only supported for the Python v2 programming model. For more information, see [SDK types in Python](functions-reference-python#sdk-type-bindings).

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache-trigger-redislist -->

# RedisListTrigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The `RedisListTrigger`

pops new elements from a list and surfaces those entries to the function.

For more information about Azure Cache for Redis triggers and bindings, [Redis Extension for Azure Functions](https://github.com/Azure/azure-functions-redis-extension/tree/main).

## Scope of availability for functions triggers

| Trigger Type | Azure Managed Redis | Azure Cache for Redis |
|---|---|---|
| Lists | Yes | Yes |

Important

When using Azure Managed Redis or the Enterprise tiers of Azure Cache for Redis, use port 10000 rather than port 6380 or 6379.

Important

Redis triggers aren't currently supported for functions running on a [Consumption plan](consumption-plan) or a [Flex Consumption plan](flex-consumption-plan).

Important

The Node.js v4 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Important

The Python v2 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v2 model works, refer to the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

## Example

Important

For .NET functions, using the *isolated worker* model is recommended over the *in-process* model. For a comparison of the *in-process* and *isolated worker* models, see differences between the *isolated worker* model and the *in-process* model for .NET on Azure Functions.

The following sample polls the key `listTest`

.:

```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.Functions.Worker.Extensions.Redis.Samples.RedisListTrigger
{
public class SimpleListTrigger
{
private readonly ILogger<SimpleListTrigger> logger;
public SimpleListTrigger(ILogger<SimpleListTrigger> logger)
{
this.logger = logger;
}
[Function(nameof(SimpleListTrigger))]
public void Run(
[RedisListTrigger(Common.connectionStringSetting, "listTest")] string entry)
{
logger.LogInformation(entry);
}
}
}
```


The following sample polls the key `listTest`

at a localhost Redis instance at `redisLocalhost`

:

```
package com.function.RedisListTrigger;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.redis.annotation.*;
public class SimpleListTrigger {
@FunctionName("SimpleListTrigger")
public void run(
@RedisListTrigger(
name = "req",
connection = "redisConnectionString",
key = "listTest",
pollingIntervalInMs = 1000,
maxBatchSize = 1)
String message,
final ExecutionContext context) {
context.getLogger().info(message);
}
}
```


This sample uses the same `index.js`

file, with binding data in the `function.json`

file.

Here's the `index.js`

file:

```
module.exports = async function (context, entry) {
context.log(entry);
}
```


From `function.json`

, here's the binding data:

```
{
"bindings": [
{
"type": "redisListTrigger",
"listPopFromBeginning": true,
"connection": "redisConnectionString",
"key": "listTest",
"pollingIntervalInMs": 1000,
"maxBatchSize": 16,
"name": "entry",
"direction": "in"
}
],
"scriptFile": "index.js"
}
```


This sample uses the same `run.ps1`

file, with binding data in the `function.json`

file.

Here's the `run.ps1`

file:

```
param($entry, $TriggerMetadata)
Write-Host $entry
```


From `function.json`

, here's the binding data:

```
{
"bindings": [
{
"type": "redisListTrigger",
"listPopFromBeginning": true,
"connection": "redisConnectionString",
"key": "listTest",
"pollingIntervalInMs": 1000,
"maxBatchSize": 16,
"name": "entry",
"direction": "in"
}
],
"scriptFile": "run.ps1"
}
```


This sample uses the same `__init__.py`

file, with binding data in the `function.json`

file.

The Python v1 programming model requires you to define bindings in a separate *function.json* file in the function folder. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-configuration#programming-model).

Here's the `__init__.py`

file:

```
import logging
def main(entry: str):
logging.info(entry)
```


From `function.json`

, here's the binding data:

```
{
"bindings": [
{
"type": "redisListTrigger",
"listPopFromBeginning": true,
"connection": "redisConnectionString",
"key": "listTest",
"pollingIntervalInMs": 1000,
"maxBatchSize": 16,
"name": "entry",
"direction": "in"
}
],
"scriptFile": "__init__.py"
}
```


## Attributes

| Parameter | Description | Required | Default |
|---|---|---|---|
`Connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`Key`

`INameResolver`

.`PollingIntervalInMs`

`1000`

`MessagesPerWorker`

`100`

`Count`

`COUNT`

argument in [and](https://redis.io/commands/lpop/)`LPOP`

[.](https://redis.io/commands/rpop/)`RPOP`

`10`

`ListPopFromBeginning`

[, or to pop entries from the end using](https://redis.io/commands/lpop/)`LPOP`

[.](https://redis.io/commands/rpop/)`RPOP`

`true`

## Annotations

| Parameter | Description | Required | Default |
|---|---|---|---|
`name` |
"entry" | ||
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`key`

`pollingIntervalInMs`

`1000`

`messagesPerWorker`

`100`

`count`

`10`

`listPopFromBeginning`

`true`

## Configuration

The following table explains the binding configuration properties that you set in the function.json file.

| function.json Property | Description | Optional | Default |
|---|---|---|---|
`type` |
Name of the trigger. | No | |
`listPopFromBeginning` |
Whether to delete the stream entries after the function has run. Set to `true` . |
Yes | `true` |
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`key`

`INameResolver`

.`pollingIntervalInMs`

`1000`

`messagesPerWorker`

`100`

`count`

`10`

`name`

`direction`

`in`

.See the Example section for complete examples.

## Usage

The `RedisListTrigger`

pops new elements from a list and surfaces those entries to the function. The trigger polls Redis at a configurable fixed interval, and uses [ LPOP](https://redis.io/commands/lpop/) and

[to pop entries from the lists.](https://redis.io/commands/rpop/)

`RPOP`

| Type | Description |
|---|---|
`byte[]` |
The message from the channel. |
`string` |
The message from the channel. |
`Custom` |
The trigger uses Json.NET serialization to map the message from the channel from a `string` into a custom type. |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-grid -->

# Azure Event Grid bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This reference shows how to connect to Azure Event Grid using Azure Functions triggers and bindings.

Event Grid is an Azure service that sends HTTP requests to notify you about events that happen in publishers. A *publisher* is the service or resource that originates the event. For example, an Azure blob storage account is a publisher, and [a blob upload or deletion is an event](../storage/blobs/storage-blob-event-overview). Some [Azure services have built-in support for publishing events to Event Grid](../event-grid/concepts#event-sources).

Event *handlers* receive and process events. Azure Functions is one of several [Azure services that have built-in support for handling Event Grid events](../event-grid/overview#event-handlers). Functions provides an Event Grid trigger, which invokes a function when an event is received from Event Grid. A similar output binding can be used to send events from your function to an [Event Grid custom topic](../event-grid/post-to-custom-topic).

You can also use an HTTP trigger to handle Event Grid Events. To learn more, see [Receive events to an HTTP endpoint](../event-grid/receive-events). We recommend using the Event Grid trigger over HTTP trigger.

| Action | Type |
|---|---|
| Run a function when an Event Grid event is dispatched |
|

[Output binding](functions-bindings-event-grid-output)[HTTP endpoint](../event-grid/receive-events)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

Add the extension to your project by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventGrid), version 3.x.

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

Considerations for the Event Grid extension:

- Event Grid extension versions earlier than 3.x don't support
[CloudEvents schema](../event-grid/cloudevents-schema#azure-functions). To consume this schema, instead use an HTTP trigger. - The Event Grid output binding is only available for Functions 2.x and higher.

## Binding types

The binding types supported for .NET depend on both the extension version and C# execution mode, which can be one of the following:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see binding type details for the mode and version.

The isolated worker process supports parameter types according to the tables below. Support for binding to `Stream`

, and to types from [Azure.Messaging](/en-us/dotnet/api/azure.messaging) is in preview.

**Event Grid trigger**

When you want the function to process a single event, the Event Grid trigger can bind to the following types:

| Type | Description |
|---|---|
| JSON serializable types | Functions tries to deserialize the JSON data of the event into a plain-old CLR object (POCO) type. |
`string` |
The event as a string. |
1 |

[CloudEvent](/en-us/dotnet/api/azure.messaging.cloudevent)1[EventGridEvent](/en-us/dotnet/api/azure.messaging.eventgrid.eventgridevent)1When you want the function to process a batch of events, the Event Grid trigger can bind to the following types:

| Type | Description |
|---|---|
`CloudEvent[]` 1,`EventGridEvent[]` 1,`string[]` ,`BinaryData[]` 1 |
An array of events from the batch. Each entry represents one event. |

1 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.EventGrid 3.3.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventGrid/3.3.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

**Event Grid output binding**

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

## host.json settings

The Event Grid trigger uses a webhook HTTP request, which can be configured using the same [ host.json settings as the HTTP Trigger](functions-bindings-http-webhook#hostjson-settings).

## Next steps

- If you have questions, submit an issue to the team
[here](https://github.com/Azure/azure-sdk-for-net/issues) [Event Grid trigger](functions-bindings-event-grid-trigger)[Event Grid output binding](functions-bindings-event-grid-output)[Run a function when an Event Grid event is dispatched](functions-bindings-event-grid-trigger)[Dispatch an Event Grid event](functions-bindings-event-grid-trigger)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-web-pubsub-input -->

# Azure Web PubSub input bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Our extension provides two input binding targeting different needs.

-
To let a client connect to Azure Web PubSub Service, it must know the service endpoint URL and a valid access token. The

`WebPubSubConnection`

input binding produces required information, so client doesn't need to handle this token generation itself. The token is time-limited and can authenticate a specific user to a connection. Therefore, don't cache the token or share it between clients. An HTTP trigger working with this input binding can be used for clients to retrieve the connection information. -
When using Static Web Apps,

`HttpTrigger`

is the only supported trigger. In Web PubSub scenarios, the`WebPubSubContext`

input binding helps users deserialize upstream HTTP requests from the service under Web PubSub protocols. So customers can get similar results comparing to`WebPubSubTrigger`

to easily handle in functions. When used with`HttpTrigger`

, customer requires to configure the HttpTrigger exposed url in event handler accordingly.

`WebPubSubConnection`


### Example

The following example shows an HTTP trigger function that acquires Web PubSub connection information using the input binding and returns it over HTTP. In following example, the `UserId`

is passed in through client request query part like `?userid={User-A}`

.

```
[Function("WebPubSubConnectionInputBinding")]
public static HttpResponseData Run([HttpTrigger(AuthorizationLevel.Anonymous)] HttpRequestData req,
[WebPubSubConnectionInput(Hub = "<hub>", , UserId = "{query.userid}", Connection = "<web_pubsub_connection_name>")] WebPubSubConnection connectionInfo)
{
var response = req.CreateResponse(HttpStatusCode.OK);
response.WriteAsJsonAsync(connectionInfo);
return response;
}
```


```
const { app, input } = require('@azure/functions');
const connection = input.generic({
type: 'webPubSubConnection',
name: 'connection',
userId: '{query.userId}',
hub: '<hub>'
});
app.http('negotiate', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraInputs: [connection],
handler: async (request, context) => {
return { body: JSON.stringify(context.extraInputs.get('connection')) };
},
});
```


Create a folder *negotiate* and update *negotiate/function.json* and copy following JSON codes.

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req"
},
{
"type": "http",
"direction": "out",
"name": "$return"
},
{
"type": "webPubSubConnection",
"name": "connection",
"userId": "{query.userid}",
"hub": "<hub>",
"direction": "in"
}
]
}
```


Define function in *negotiate/ init.py*.

```
import logging
import azure.functions as func
def main(req: func.HttpRequest, connection) -> func.HttpResponse:
return func.HttpResponse(connection)
```


Note

Complete samples for this language are pending

Note

The Web PubSub extensions for Java isn't supported yet.

### Get authenticated user ID

If the function is triggered by an authenticated client, you can add a user ID claim to the generated token. You can easily add authentication to a function app using App Service Authentication.

App Service Authentication sets HTTP headers named `x-ms-client-principal-id`

and `x-ms-client-principal-name`

that contain the authenticated user's client principal ID and name, respectively.

You can set the `UserId`

property of the binding to the value from either header using a binding expression: `{headers.x-ms-client-principal-id}`

or `{headers.x-ms-client-principal-name}`

.

```
[Function("WebPubSubConnectionInputBinding")]
public static HttpResponseData Run([HttpTrigger(AuthorizationLevel.Anonymous)] HttpRequestData req,
[WebPubSubConnectionInput(Hub = "<hub>", , UserId = "{headers.x-ms-client-principal-id}", Connection = "<web_pubsub_connection_name>")] WebPubSubConnection connectionInfo)
{
var response = req.CreateResponse(HttpStatusCode.OK);
response.WriteAsJsonAsync(connectionInfo);
return response;
}
```


```
const { app, input } = require('@azure/functions');
const connection = input.generic({
type: 'webPubSubConnection',
name: 'connection',
userId: '{headers.x-ms-client-principal-id}',
hub: '<hub>'
});
app.http('negotiate', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraInputs: [connection],
handler: async (request, context) => {
return { body: JSON.stringify(context.extraInputs.get('connection')) };
},
});
```


Create a folder *negotiate* and update *negotiate/function.json* and copy following JSON codes.

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req"
},
{
"type": "http",
"direction": "out",
"name": "$return"
},
{
"type": "webPubSubConnection",
"name": "connection",
"userId": "{headers.x-ms-client-principal-id}",
"hub": "<hub>",
"direction": "in"
}
]
}
```


Define function in *negotiate/ init.py*.

```
import logging
import azure.functions as func
def main(req: func.HttpRequest, connection) -> func.HttpResponse:
return func.HttpResponse(connection)
```


Note

Complete samples for this language are pending

Note

The Web PubSub extensions for Java isn't supported yet.

### Configuration

The following table explains the binding configuration properties that you set in the function.json file and the `WebPubSubConnection`

attribute.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Must be set to `webPubSubConnection` |
direction |
n/a | Must be set to `in` |
name |
n/a | Variable name used in function code for input connection binding object. |
hub |
Hub | Required - The value must be set to the name of the Web PubSub hub for the function to be triggered. We support set the value in attribute as higher priority, or it can be set in app settings as a global value. |
userId |
UserId | Optional - the value of the user identifier claim to be set in the access key token. |
clientProtocol |
ClientProtocol | Optional - The client protocol type. Valid values include `default` and `mqtt` . For MQTT clients, you must set it to `mqtt` . For other clients, you can omit the property or set it to `default` . |
connection |
Connection | Required - The name of the app setting that contains the Web PubSub Service connection string (defaults to "WebPubSubConnectionString"). |

### Usage

`WebPubSubConnection`

provides following properties.

| Binding Name | Binding Type | Description |
|---|---|---|
| BaseUri | Uri | Web PubSub client connection uri. |
| Uri | Uri | Absolute Uri of the Web PubSub connection, contains `AccessToken` generated base on the request. |
| AccessToken | string | Generated `AccessToken` based on request UserId and service information. |

`WebPubSubConnection`

provides following properties.

| Binding Name | Description |
|---|---|
| baseUrl | Web PubSub client connection uri. |
| url | Absolute Uri of the Web PubSub connection, contains `AccessToken` generated base on the request. |
| accessToken | Generated `AccessToken` based on request UserId and service information. |

Note

The Web PubSub extensions for Java isn't supported yet.

### More customization of generated token

Limited to the binding parameter types don't support a way to pass list nor array, the `WebPubSubConnection`

isn't fully supported with all the parameters server SDK has, especially `roles`

, and also includes `groups`

and `expiresAfter`

.

When customer needs to add roles or delay building the access token in the function, we suggest you to work with [server SDK for C#](/en-us/dotnet/api/overview/azure/messaging.webpubsub-readme).

```
[Function("WebPubSubConnectionCustomRoles")]
public static HttpResponseData Run([HttpTrigger(AuthorizationLevel.Anonymous)] HttpRequestData req)
{
var serviceClient = new WebPubSubServiceClient(new Uri(endpoint), "<hub>", "<web-pubsub-connection-string>");
var userId = req.Query["userid"].FirstOrDefault();
// your method to get custom roles.
var roles = GetRoles(userId);
var url = await serviceClient.GetClientAccessUriAsync(TimeSpan.FromMinutes(5), userId, roles);
var response = req.CreateResponse(HttpStatusCode.OK);
response.WriteString(url.ToString());
return response;
}
```


When customer needs to add roles or delay building the access token in the function, we suggest you working with [server SDK for JavaScript](/en-us/javascript/api/overview/azure/web-pubsub).

```
const { app } = require('@azure/functions');
const { WebPubSubServiceClient } = require('@azure/web-pubsub');
app.http('negotiate', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: async (request, context) => {
const serviceClient = new WebPubSubServiceClient(process.env.WebPubSubConnectionString, "<hub>");
let token = await serviceClient.getAuthenticationToken({ userId: req.query.userid, roles: ["webpubsub.joinLeaveGroup", "webpubsub.sendToGroup"] });
return { body: token.url };
},
});
```


Note

Complete samples for this language are pending

Note

The Web PubSub extensions for Java isn't supported yet.

`WebPubSubContext`


### Example

```
// validate method when upstream set as http://<func-host>/api/{event}
[Function("validate")]
public static HttpResponseData Validate(
[HttpTrigger(AuthorizationLevel.Anonymous, "options")] HttpRequestData req,
[WebPubSubContextInput] WebPubSubContext wpsReq)
{
return BuildHttpResponseData(req, wpsReq.Response);
}
// Respond AbuseProtection to put header correctly.
private static HttpResponseData BuildHttpResponseData(HttpRequestData request, SimpleResponse wpsResponse)
{
var response = request.CreateResponse();
response.StatusCode = (HttpStatusCode)wpsResponse.Status;
response.Body = response.Body;
foreach (var header in wpsResponse.Headers)
{
response.Headers.Add(header.Key, header.Value);
}
return response;
}
```


```
const { app, input } = require('@azure/functions');
const wpsContext = input.generic({
type: 'webPubSubContext',
name: 'wpsContext'
});
app.http('connect', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraInputs: [wpsContext],
handler: async (request, context) => {
var wpsRequest = context.extraInputs.get('wpsContext');
return { "userId": wpsRequest.request.connectionContext.userId };
}
});
```


Note

Complete samples for this language are pending

Note

The Web PubSub extensions for Java isn't supported yet.

### Configuration

The following table explains the binding configuration properties that you set in the functions.json file and the `WebPubSubContext`

attribute.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Must be set to `webPubSubContext` . |
direction |
n/a | Must be set to `in` . |
name |
n/a | Variable name used in function code for input Web PubSub request. |
connection |
Connection | Optional - the name of an app settings or setting collection that specifies the upstream Azure Web PubSub service. The value is used for
`null` means the validation isn't needed and always succeed. |

Important

For optimal security, your function app should use managed identities when connecting to the Web PubSub service instead of using a connection string, which contains a shared secret key. For more information, see [Authorize a managed identity request by using Microsoft Entra ID](../azure-web-pubsub/howto-authorize-from-managed-identity).

### Usage

`WebPubSubContext`

provides following properties.

| Binding Name | Binding Type | Description | Properties |
|---|---|---|---|
| request | `WebPubSubEventRequest` |
Request from client, see following table for details. | `WebPubSubConnectionContext` from request header and other properties deserialized from request body describe the request, for example, `Reason` for `DisconnectedEventRequest` . |
| response | `HttpResponseMessage` |
Extension builds response mainly for `AbuseProtection` and errors cases. |
- |
| errorMessage | string | Describe the error details when processing the upstream request. | - |
| hasError | bool | Flag to indicate whether it's a valid Web PubSub upstream request. | - |
| isPreflight | bool | Flag to indicate whether it's a preflight request of `AbuseProtection` . |
- |

For `WebPubSubEventRequest`

, it's deserialized to different classes that provide different information about the request scenario. For `PreflightRequest`

or not valid cases, user can check the flags `IsPreflight`

and `HasError`

to know. We suggest you to return system build response `WebPubSubContext.Response`

directly, or customer can log errors on demand. In different scenarios, customer can read the request properties as following.

| Derived Class | Description | Properties |
|---|---|---|
`PreflightRequest` |
Used in `AbuseProtection` when `IsPreflight` is true |
- |
`ConnectEventRequest` |
Used in system `Connect` event type |
Claims, Query, Subprotocols, ClientCertificates |
`ConnectedEventRequest` |
Used in system `Connected` event type |
- |
`UserEventRequest` |
Used in user event type | Data, DataType |
`DisconnectedEventRequest` |
Used in system `Disconnected` event type |
Reason |

Note

Though the

`WebPubSubContext`

is an input binding provides similar request deserialize way under`HttpTrigger`

comparing to`WebPubSubTrigger`

, there's limitations, i.e. connection state post merge isn't supported. The return response is still respected by the service side, but users require to build the response themselves. If users have needs to set the event response, you should return a`HttpResponseMessage`

contains`ConnectEventResponse`

or messages for user event asresponse bodyand put connection state with key`ce-connectionstate`

inresponse header.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-host-json -->

# host.json reference for Azure Functions 2.x and later

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The host.json metadata file contains configuration options that affect all functions in a function app instance. This article lists the settings that are available starting with version 2.x of the Azure Functions runtime.

Note

This article is for Azure Functions 2.x and later versions. For a reference of host.json in Functions 1.x, see [host.json reference for Azure Functions 1.x](functions-host-json-v1).

Other function app configuration options are managed depending on where the function app runs:

**Deployed to Azure**: in your[application settings](functions-app-settings)**On your local computer**: in the[local.settings.json](functions-develop-local#local-settings-file)file.

Configurations in host.json related to bindings are applied equally to each function in the function app.

You can also [override or apply settings per environment](#override-hostjson-values) using application settings.

## Sample host.json file

The following sample *host.json* file for version 2.x+ has all possible options specified (excluding any that are for internal use only).

```
{
"version": "2.0",
"aggregator": {
"batchSize": 1000,
"flushTimeout": "00:00:30"
},
"concurrency": {
"dynamicConcurrencyEnabled": true,
"snapshotPersistenceEnabled": true
},
"extensions": {
"blobs": {},
"cosmosDb": {},
"durableTask": {},
"eventHubs": {},
"http": {},
"queues": {},
"sendGrid": {},
"serviceBus": {}
},
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.0.0, 5.0.0)"
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
"logging": {
"fileLoggingMode": "debugOnly",
"logLevel": {
"Function.MyFunction": "Information",
"default": "None"
},
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"maxTelemetryItemsPerSecond" : 20,
"evaluationInterval": "01:00:00",
"initialSamplingPercentage": 100.0,
"samplingPercentageIncreaseTimeout" : "00:00:01",
"samplingPercentageDecreaseTimeout" : "00:00:01",
"minSamplingPercentage": 0.1,
"maxSamplingPercentage": 100.0,
"movingAverageRatio": 1.0,
"excludedTypes" : "Dependency;Event",
"includedTypes" : "PageView;Trace"
},
"dependencyTrackingOptions": {
"enableSqlCommandTextInstrumentation": true
},
"enableLiveMetrics": true,
"enableDependencyTracking": true,
"enablePerformanceCountersCollection": true,
"httpAutoCollectionOptions": {
"enableHttpTriggerExtendedInfoCollection": true,
"enableW3CDistributedTracing": true,
"enableResponseHeaderInjection": true
},
"snapshotConfiguration": {
"agentEndpoint": null,
"captureSnapshotMemoryWeight": 0.5,
"failedRequestLimit": 3,
"handleUntrackedExceptions": true,
"isEnabled": true,
"isEnabledInDeveloperMode": false,
"isEnabledWhenProfiling": true,
"isExceptionSnappointsEnabled": false,
"isLowPrioritySnapshotUploader": true,
"maximumCollectionPlanSize": 50,
"maximumSnapshotsRequired": 3,
"problemCounterResetInterval": "24:00:00",
"provideAnonymousTelemetry": true,
"reconnectInterval": "00:15:00",
"shadowCopyFolder": null,
"shareUploaderProcess": true,
"snapshotInLowPriorityThread": true,
"snapshotsPerDayLimit": 30,
"snapshotsPerTenMinutesLimit": 1,
"tempFolder": null,
"thresholdForSnapshotting": 1,
"uploaderProxy": null
}
}
},
"managedDependency": {
"enabled": true
},
"singleton": {
"lockPeriod": "00:00:15",
"listenerLockPeriod": "00:01:00",
"listenerLockRecoveryPollingInterval": "00:01:00",
"lockAcquisitionTimeout": "00:01:00",
"lockAcquisitionPollingInterval": "00:00:03"
},
"telemetryMode": "OpenTelemetry",
"watchDirectories": [ "Shared", "Test" ],
"watchFiles": [ "myFile.txt" ]
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

This setting is a child of [logging](#logging).

Controls options for Application Insights, including [sampling options](configure-monitoring#configure-sampling).

For the complete JSON structure, see the earlier [example host.json file](#sample-hostjson-file).

Note

Log sampling may cause some executions to not show up in the Application Insights monitor blade. To avoid log sampling, add `excludedTypes: "Request"`

to the `samplingSettings`

value.

| Property | Default | Description |
|---|---|---|
| samplingSettings | n/a | See
|

[applicationInsights.dependencyTrackingOptions](#applicationinsightsdependencytrackingoptions).[applicationInsights.samplingSettings.excludedTypes](#applicationinsightssamplingsettings), For more information, see see[Select and filter your metrics](/en-us/azure/azure-monitor/app/live-stream#select-and-filter-your-metrics).[applicationInsights.httpAutoCollectionOptions](#applicationinsightshttpautocollectionoptions).[applicationInsights.snapshotConfiguration](#applicationinsightssnapshotconfiguration).### applicationInsights.samplingSettings

For more information about these settings, see [Sampling in Application Insights](/en-us/azure/azure-monitor/app/sampling).

| Property | Default | Description |
|---|---|---|
| isEnabled | true | Enables or disables sampling. |
| maxTelemetryItemsPerSecond | 20 | The target number of telemetry items logged per second on each server host. If your app runs on many hosts, reduce this value to remain within your overall target rate of traffic. |
| evaluationInterval | 01:00:00 | The interval at which the current rate of telemetry is reevaluated. Evaluation is performed as a moving average. You might want to shorten this interval if your telemetry is liable to sudden bursts. |
| initialSamplingPercentage | 100.0 | The initial sampling percentage applied at the start of the sampling process to dynamically vary the percentage. Don't reduce value while you're debugging. |
| samplingPercentageIncreaseTimeout | 00:00:01 | When the sampling percentage value changes, this property determines how soon afterwards Application Insights is allowed to raise sampling percentage again to capture more data. |
| samplingPercentageDecreaseTimeout | 00:00:01 | When the sampling percentage value changes, this property determines how soon afterwards Application Insights is allowed to lower sampling percentage again to capture less data. |
| minSamplingPercentage | 0.1 | As sampling percentage varies, this property determines the minimum allowed sampling percentage. |
| maxSamplingPercentage | 100.0 | As sampling percentage varies, this property determines the maximum allowed sampling percentage. |
| movingAverageRatio | 1.0 | In the calculation of the moving average, the weight assigned to the most recent value. Use a value equal to or less than 1. Smaller values make the algorithm less reactive to sudden changes. |
| excludedTypes | null | A semi-colon delimited list of types that you don't want to be sampled. Recognized types are: `Dependency` , `Event` , `Exception` , `PageView` , `Request` , and `Trace` . All instances of the specified types are transmitted; the types that aren't specified are sampled. |
| includedTypes | null | A semi-colon delimited list of types that you want to be sampled; an empty list implies all types. Type listed in `excludedTypes` override types listed here. Recognized types are: `Dependency` , `Event` , `Exception` , `PageView` , `Request` , and `Trace` . Instances of the specified types are sampled; the types that aren't specified or implied are transmitted without sampling. |

### applicationInsights.httpAutoCollectionOptions

| Property | Default | Description |
|---|---|---|
| enableHttpTriggerExtendedInfoCollection | true | Enables or disables extended HTTP request information for HTTP triggers: incoming request correlation headers, multi-instrumentation keys support, HTTP method, path, and response. |
| enableW3CDistributedTracing | true | Enables or disables support of W3C distributed tracing protocol (and turns on legacy correlation schema). Enabled by default if `enableHttpTriggerExtendedInfoCollection` is true. If `enableHttpTriggerExtendedInfoCollection` is false, this flag applies to outgoing requests only, not incoming requests. |
| enableResponseHeaderInjection | true | Enables or disables injection of multi-component correlation headers into responses. Enabling injection allows Application Insights to construct an Application Map to when several instrumentation keys are used. Enabled by default if `enableHttpTriggerExtendedInfoCollection` is true. This setting doesn't apply if `enableHttpTriggerExtendedInfoCollection` is false. |

### applicationInsights.dependencyTrackingOptions

| Property | Default | Description |
|---|---|---|
| enableSqlCommandTextInstrumentation | false | Enables collection of the full text of SQL queries, which is disabled by default. For more information on collecting SQL query text, see
|

### applicationInsights.snapshotConfiguration

For more information on snapshots, see [Debug snapshots on exceptions in .NET apps](/en-us/azure/azure-monitor/app/snapshot-debugger) and [Troubleshoot problems enabling Application Insights Snapshot Debugger or viewing snapshots](/en-us/troubleshoot/azure/azure-monitor/app-insights/snapshot-debugger-troubleshoot).

| Property | Default | Description |
|---|---|---|
| agentEndpoint | null | The endpoint used to connect to the Application Insights Snapshot Debugger service. If null, a default endpoint is used. |
| captureSnapshotMemoryWeight | 0.5 | The weight given to the current process memory size when checking if there's enough memory to take a snapshot. The expected value is a greater than 0 proper fraction (0 < CaptureSnapshotMemoryWeight < 1). |
| failedRequestLimit | 3 | The limit on the number of failed requests to request snapshots before the telemetry processor is disabled. |
| handleUntrackedExceptions | true | Enables or disables tracking of exceptions that aren't tracked by Application Insights telemetry. |
| isEnabled | true | Enables or disables snapshot collection |
| isEnabledInDeveloperMode | false | Enables or disables snapshot collection is enabled in developer mode. |
| isEnabledWhenProfiling | true | Enables or disables snapshot creation even if the Application Insights Profiler is collecting a detailed profiling session. |
| isExceptionSnappointsEnabled | false | Enables or disables filtering of exceptions. |
| isLowPrioritySnapshotUploader | true | Determines whether to run the SnapshotUploader process at below normal priority. |
| maximumCollectionPlanSize | 50 | The maximum number of problems that we can track at any time in a range from one to 9999. |
| maximumSnapshotsRequired | 3 | The maximum number of snapshots collected for a single problem, in a range from one to 999. A problem may be thought of as an individual throw statement in your application. Once the number of snapshots collected for a problem reaches this value, no more snapshots will be collected for that problem until problem counters are reset (see `problemCounterResetInterval` ) and the `thresholdForSnapshotting` limit is reached again. |
| problemCounterResetInterval | 24:00:00 | How often to reset the problem counters in a range from one minute to seven days. When this interval is reached, all problem counts are reset to zero. Existing problems that have already reached the threshold for doing snapshots, but haven't yet generated the number of snapshots in `maximumSnapshotsRequired` , remain active. |
| provideAnonymousTelemetry | true | Determines whether to send anonymous usage and error telemetry to Microsoft. This telemetry may be used if you contact Microsoft to help troubleshoot problems with the Snapshot Debugger. It's also used to monitor usage patterns. |
| reconnectInterval | 00:15:00 | How often we reconnect to the Snapshot Debugger endpoint. Allowable range is one minute to one day. |
| shadowCopyFolder | null | Specifies the folder to use for shadow copying binaries. If not set, the folders specified by the following environment variables are tried in order: Fabric_Folder_App_Temp, LOCALAPPDATA, APPDATA, TEMP. |
| shareUploaderProcess | true | If true, only one instance of SnapshotUploader will collect and upload snapshots for multiple apps that share the InstrumentationKey. If set to false, the SnapshotUploader will be unique for each (ProcessName, InstrumentationKey) tuple. |
| snapshotInLowPriorityThread | true | Determines whether or not to process snapshots in a low IO priority thread. Creating a snapshot is a fast operation but, in order to upload a snapshot to the Snapshot Debugger service, it must first be written to disk as a minidump. That happens in the SnapshotUploader process. Setting this value to true uses low-priority IO to write the minidump, which won't compete with your application for resources. Setting this value to false speeds up minidump creation at the expense of slowing down your application. |
| snapshotsPerDayLimit | 30 | The maximum number of snapshots allowed in one day (24 hours). This limit is also enforced on the Application Insights service side. Uploads are rate limited to 50 per day per application (that is, per instrumentation key). This value helps prevent creating additional snapshots that will eventually be rejected during upload. A value of zero removes the limit entirely, which isn't recommended. |
| snapshotsPerTenMinutesLimit | 1 | The maximum number of snapshots allowed in 10 minutes. Although there's no upper bound on this value, exercise caution increasing it on production workloads because it could impact the performance of your application. Creating a snapshot is fast, but creating a minidump of the snapshot and uploading it to the Snapshot Debugger service is a much slower operation that will compete with your application for resources (both CPU and I/O). |
| tempFolder | null | Specifies the folder to write minidumps and uploader log files. If not set, then %TEMP%\Dumps is used. |
| thresholdForSnapshotting | 1 | How many times Application Insights needs to see an exception before it asks for snapshots. |
| uploaderProxy | null | Overrides the proxy server used in the Snapshot Uploader process. You may need to use this setting if your application connects to the internet via a proxy server. The Snapshot Collector runs within your application's process and will use the same proxy settings. However, the Snapshot Uploader runs as a separate process and you may need to configure the proxy server manually. If this value is null, then Snapshot Collector will attempt to autodetect the proxy's address by examining `System.Net.WebRequest.DefaultWebProxy` and passing on the value to the Snapshot Uploader. If this value isn't null, then autodetection isn't used and the proxy server specified here will be used in the Snapshot Uploader. |

## blobs

Configuration settings can be found in [Storage blob triggers and bindings](functions-bindings-storage-blob#hostjson-settings).

## console

This setting is a child of [logging](#logging). It controls the console logging when not in debugging mode.

```
{
"logging": {
...
"console": {
"isEnabled": false,
"DisableColors": true
},
...
}
}
```


| Property | Default | Description |
|---|---|---|
| DisableColors | false | Suppresses log formatting in the container logs on Linux. Set to true if you're seeing unwanted ANSI control characters in the container logs when running on Linux. |
| isEnabled | false | Enables or disables console logging. |

## Azure Cosmos DB

Configuration settings can be found in [Azure Cosmos DB triggers and bindings](functions-bindings-cosmosdb-v2#hostjson-settings).

## customHandler

Configuration settings for a custom handler. For more information, see [Azure Functions custom handlers](functions-custom-handlers#configuration).

```
"customHandler": {
"description": {
"defaultExecutablePath": "server",
"workingDirectory": "handler",
"arguments": [ "--port", "%FUNCTIONS_CUSTOMHANDLER_PORT%" ]
},
"enableForwardingHttpRequest": false
}
```


| Property | Default | Description |
|---|---|---|
| defaultExecutablePath | n/a | The executable to start as the custom handler process. It's a required setting when using custom handlers and its value is relative to the function app root. |
| workingDirectory | function app root |
The working directory in which to start the custom handler process. It's an optional setting and its value is relative to the function app root. |
| arguments | n/a | An array of command line arguments to pass to the custom handler process. |
| enableForwardingHttpRequest | false | If set, all functions that consist of only an HTTP trigger and HTTP output is forwarded the original HTTP request instead of the custom handler
|

## durableTask

Configuration setting can be found in [bindings for Durable Functions](durable/durable-functions-bindings#host-json).

## concurrency

Enables dynamic concurrency for specific bindings in your function app. For more information, see [Dynamic concurrency](functions-concurrency#dynamic-concurrency).

```
{
"concurrency": {
"dynamicConcurrencyEnabled": true,
"snapshotPersistenceEnabled": true
}
}
```


| Property | Default | Description |
|---|---|---|
| dynamicConcurrencyEnabled | false | Enables dynamic concurrency behaviors for all triggers supported by this feature, which is off by default. |
| snapshotPersistenceEnabled | true | Learned concurrency values are periodically persisted to storage so new instances start from those values instead of starting from 1 and having to redo the learning. |

## eventHub

Configuration settings can be found in [Event Hub triggers and bindings](functions-bindings-event-hubs#host-json).

## extensions

Property that returns an object that contains all of the binding-specific settings, such as [http](#http) and [eventHub](#eventhub).

## extensionBundle

Extension bundles let you add a compatible set of Functions binding extensions to your function app. To learn more, see [Extension bundles for local development](extension-bundles).

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

The following properties are available in `extensionBundle`

:

| Property | Description |
|---|---|
`id` |
The namespace for Azure Functions extension bundles. |
`version` |
The version range of the bundle to install. The Azure Functions runtime always chooses the maximum permissible version that the version range or interval defines. For example, a `version` value range of `[4.0.0, 5.0.0)` allows all bundle versions from 4.0.0 up to (but not including) 5.0.0. For more information, see the
|

Tip

You might also see the version range defined in your *host.json* as `[4.*, 5.0.0)`

, which is interpreted the same as `[4.0.0, 5.0.0)`

.

## functions

A list of functions that the job host runs. An empty array means run all functions. Intended for use only when [running locally](functions-run-local). In function apps in Azure, you should instead follow the steps in [How to disable functions in Azure Functions](disable-function) to disable specific functions rather than using this setting.

```
{
"functions": [ "QueueProcessor", "GitHubWebHook" ]
}
```


## functionTimeout

Indicates the timeout duration for all function executions. It follows the [timespan string format](/en-us/dotnet/fundamentals/runtime-libraries/system-timespan-parse). A value of `-1`

indicates unbounded execution, but keeping a fixed upper bound is recommended.

```
{
"functionTimeout": "00:05:00"
}
```


The format of the timespan string needs to follow the syntax `[d.]hh:mm:ss`

and the valid values are:

- d = days (optional)
- hh = hours (0–23)
- mm = minutes (0–59)
- ss = seconds (0–59)

Tip

When you need to set a 24-hour timeout, you must define it as one day (`"1.00:00:00"`

) instead of 24 hours (`"24:00:00"`

). You might also use `"23:59:59"`

.

For more information on the default and maximum values for specific plans, see [Function app timeout duration](functions-scale#timeout).

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
| healthCheckWindow | 2 minutes | A sliding time window used in conjunction with the `healthCheckThreshold` setting. |
| healthCheckThreshold | 6 | Maximum number of times the health check can fail before a host recycle is initiated. |
| counterThreshold | 0.80 | The threshold at which a performance counter will be considered unhealthy. |

## http

Configuration settings can be found in [http triggers and bindings](functions-bindings-http-webhook#hostjson-settings).

## logging

Controls the logging behaviors of the function app, including Application Insights.

```
"logging": {
"fileLoggingMode": "debugOnly",
"logLevel": {
"Function.MyFunction": "Information",
"default": "None"
},
"console": {
...
},
"applicationInsights": {
...
}
}
```


| Property | Default | Description |
|---|---|---|
| fileLoggingMode | debugOnly | Determines the file logging behavior when running in Azure. Options are `never` , `always` , and `debugOnly` . This setting isn't used when running locally. When possible, you should use Application Insights when debugging your functions in Azure. Using `always` negatively impacts your app's cold start behavior and data throughput. The default `debugOnly` setting generates log files when you're debugging using the Azure portal. |
| logLevel | n/a | Object that defines the log category filtering for functions in the app. This setting lets you filter logging for specific functions. For more information, see
|

[console](#console)logging setting.[applicationInsights](#applicationinsights)setting.## managedDependency

Managed dependency is a feature that is currently only supported with PowerShell based functions. It enables dependencies to be automatically managed by the service. When the `enabled`

property is set to `true`

, the `requirements.psd1`

file is processed. Dependencies are updated when any minor versions are released. For more information, see [Managed dependency](functions-reference-powershell#dependency-management) in the PowerShell article.

```
{
"managedDependency": {
"enabled": true
}
}
```


## queues

Configuration settings can be found in [Storage queue triggers and bindings](functions-bindings-storage-queue#host-json).

## sendGrid

Configuration setting can be found in [SendGrid triggers and bindings](functions-bindings-sendgrid#host-json).

## serviceBus

Configuration setting can be found in [Service Bus triggers and bindings](functions-bindings-service-bus).

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
| lockAcquisitionTimeout | 00:01:00 | The maximum amount of time the runtime will try to acquire a lock. |
| lockAcquisitionPollingInterval | n/a | The interval between lock acquisition attempts. |

## telemetryMode

*This feature is currently in preview.*

Used to enable output of logs and traces in an OpenTelemetry output format to one or more endpoints that support OpenTelemetry. When this setting is set to `OpenTelemetry`

, OpenTelemetry output is used. By default without this setting, all logs, traces, and events are sent to Application Insights using the standard outputs. For more information, see [Use OpenTelemetry with Azure Functions](opentelemetry-howto).

## version

This value indicates the schema version of host.json. The version string `"version": "2.0"`

is required for a function app that targets the v2 runtime, or a later version. There are no host.json schema changes between v2 and v3.

## watchDirectories

A set of [shared code directories](functions-reference-csharp#watched-directories) that should be monitored for changes. Ensures that when code in these directories is changed, the changes are picked up by your functions.

```
{
"watchDirectories": [ "Shared" ]
}
```


## watchFiles

An array of one or more names of files that are monitored for changes that require your app to restart. This guarantees that when code in these files is changed, the updates are picked up by your functions.

```
{
"watchFiles": [ "myFile.txt" ]
}
```


## Override host.json values

There may be instances where you wish to configure or modify specific settings in a host.json file for a specific environment, without changing the host.json file itself. You can override specific host.json values by creating an equivalent value as an application setting. When the runtime finds an application setting in the format `AzureFunctionsJobHost__path__to__setting`

, it overrides the equivalent host.json setting located at `path.to.setting`

in the JSON. When expressed as an application setting, the dot (`.`

) used to indicate JSON hierarchy is replaced by a double underscore (`__`

).

For example, say that you wanted to disable Application Insight sampling when running locally. If you changed the local host.json file to disable Application Insights, this change might get pushed to your production app during deployment. The safer way to do this is to instead create an application setting as `"AzureFunctionsJobHost__logging__applicationInsights__samplingSettings__isEnabled":"false"`

in the `local.settings.json`

file. You can see this in the following `local.settings.json`

file, which doesn't get published:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "{storage-account-connection-string}",
"FUNCTIONS_WORKER_RUNTIME": "{language-runtime}",
"AzureFunctionsJobHost__logging__applicationInsights__samplingSettings__isEnabled":"false"
}
}
```


Overriding host.json settings using environment variables follows the ASP.NET Core naming conventions. When the element structure includes an array, the numeric array index should be treated as an additional element name in this path. For more information, see [Naming of environment variables](/en-us/aspnet/core/fundamentals/configuration/#naming-of-environment-variables).
