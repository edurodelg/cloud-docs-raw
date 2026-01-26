---
merged_at: 2026-01-26T23:29:57.720517
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/scenario-database-changes-azure-cosmosdb -->

# Quickstart: Respond to database changes in Azure Cosmos DB using Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this Quickstart, you use Visual Studio Code to build an app that responds to database changes in a No SQL database in Azure Cosmos DB. After testing the code locally, you deploy it to a new serverless function app you create running in a Flex Consumption plan in Azure Functions.

The project source uses the Azure Developer CLI (azd) extension with Visual Studio Code to simplify initializing and verifying your project code locally, as well as and deploying your code to Azure. This deployment follows current best practices for secure and scalable Azure Functions deployments.

Important

While responding to [changes in an Azure Cosmos DB No SQL database](functions-bindings-cosmosdb-v2-trigger) is supported for all languages, this quickstart scenario currently only has examples for C#, Python, and TypeScript. To complete this quickstart, select one of these supported languages at the top of the article.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code. This extension requires[Azure Functions Core Tools](functions-run-local). When this tool isn't available locally, the extension tries to install it by using a package-based installer. You can also install or update the Core Tools package by running`Azure Functions: Install or Update Azure Functions Core Tools`

from the command palette. If you don't have npm or Homebrew installed on your local computer, you must instead[manually install or update Core Tools](functions-run-local#install-the-azure-functions-core-tools).

[C# extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)for Visual Studio Code.

[Node.js 18.x](https://nodejs.org/en/about/previous-releases)or above. Use the`node --version`

command to check your version.

Python versions that are

[supported by Azure Functions](supported-languages#languages-by-runtime-version). For more information, see[How to install Python](https://wiki.python.org/moin/BeginnersGuide/Download).The

[Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)for Visual Studio Code.

- The
[Azure Developer CLI extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.azure-dev)for Visual Studio Code.

## Initialize the project

You can use the `azd init`

command from the command palette to create a local Azure Functions code project from a template.

In Visual Studio Code, open a folder or workspace in which you want to create your project.

Press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Initialize App (init)`

, and then choose**Select a template**.There might be a slight delay while

`azd`

initializes the current folder or workspace.

When prompted, choose

**Select a template**, then search for and select`Azure Functions with Cosmos DB Bindings (.NET)`

.When prompted, enter a unique environment name, such as

`cosmosdbchanges-dotnet`

.This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-cosmosdb)and initializes the project in the current folder or workspace. In`azd`

, the environment is used to maintain a unique deployment context for your app, and you can define more than one. It's also part of the name of the resource group you create in Azure.

When prompted, choose

**Select a template**, then search for and select`Azure Functions TypeScript CosmosDB trigger`

.When prompted, enter a unique environment name, such as

`cosmosdbchanges-ts`

.This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-cosmosdb)and initializes the project in the current folder or workspace. In`azd`

, the environment is used to maintain a unique deployment context for your app, and you can define more than one. It's also part of the name of the resource group you create in Azure.

When prompted, choose

**Select a template**, then search for and select`Azure Functions Python with CosmosDB triggers and bindings...`

.When prompted, enter a unique environment name, such as

`cosmosdbchanges-py`

.This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-python-azd-cosmosdb)and initializes the project in the current folder or workspace. In`azd`

, the environment is used to maintain a unique deployment context for your app, and you can define more than one. It's also part of the name of the resource group you create in Azure.

Run this command, depending on your local operating system, to grant configuration scripts the required permissions:

Run this command with sufficient privileges:

`chmod +x ./infra/scripts/*.sh`


Before you can run your app locally, you must create the resources in Azure. This project doesn't use local emulation for Azure Cosmos DB.

## Create Azure resources

This project is configured to use the `azd provision`

command to create a function app in a Flex Consumption plan, along with other required Azure resources that follows current best practices.

In Visual Studio Code, press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Sign In with Azure Developer CLI`

, and then sign in using your Azure account.Press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Provision Azure resources (provision)`

to create the required Azure resources:When prompted in the Terminal window, provide these required deployment parameters:

Prompt Description Select an Azure Subscription to use Choose the subscription in which you want your resources to be created. *location*deployment parameterAzure region in which to create the resource group that contains the new Azure resources. Only regions that currently support the Flex Consumption plan are shown. *vnetEnabled*deployment parameterWhile the template supports creating resources inside a virtual network, to simplify deployment and testing, choose `False`

.The

`azd provision`

command uses your response to these prompts with the Bicep configuration files to create and configure these required Azure resources, following the latest best practices:- Flex Consumption plan and function app
- Azure Cosmos DB account
- Azure Storage (required) and Application Insights (recommended)
- Access policies and roles for your account
- Service-to-service connections using managed identities (instead of stored connection strings)

Post-provision hooks also generate the

*local.settings.json*file required when running locally. This file also contains the settings required to connect to your Azure Cosmos DB database in Azure.Tip

Should any steps fail during provisioning, you can rerun the

`azd provision`

command again after resolving any issues.After the command completes successfully, you can run your project code locally and trigger on the Azure Cosmos DB database in Azure.


## Run the function locally

Visual Studio Code integrates with [Azure Functions Core tools](functions-run-local) to let you run this project on your local development computer before you publish to your new function app in Azure.

Press

`F1`and in the command palette search for and run the command`Azurite: Start`

.To start the function locally, press

`F5`or the**Run and Debug**icon in the left-hand side Activity bar. The**Terminal**panel displays the output from Core Tools. Your app starts in the**Terminal**panel, and you can see the name of the function that's running locally.If you have trouble running on Windows, make sure that the default terminal for Visual Studio Code isn't set to

**WSL Bash**.With Core Tools still running in

**Terminal**, press`F1`and in the command palette search for and run the command`NoSQL: Create Item...`

and select both the`document-db`

database and the`documents`

container.Replace the contents of the

*New Item.json*file with this JSON data and select**Save**:`{ "id": "doc1", "title": "Sample document", "content": "This is a sample document for testing my Azure Cosmos DB trigger in Azure Functions." }`

After you select

**Save**, you see the execution of the function in the terminal and the local document is updated to include metadata added by the service.When you're done, press Ctrl+C in the terminal window to stop the

`func.exe`

host process.

## Review the code (optional)

The function is triggered based on the change feed in an Azure Cosmos DB NoSQL database. These environment variables configure how the trigger monitors the change feed:

`COSMOS_CONNECTION__accountEndpoint`

: The Cosmos DB account endpoint`COSMOS_DATABASE_NAME`

: The name of the database to monitor`COSMOS_CONTAINER_NAME`

: The name of the container to monitor

These environment variables are created for you both in Azure (function app settings) and locally (local.settings.json) during the `azd provision`

operation.

You can review the code that defines the Azure Cosmos DB trigger in the [CosmosTrigger.cs project file](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-cosmosdb/blob/main/CosmosTrigger.cs).

You can review the code that defines the Azure Cosmos DB trigger in the [cosmos_trigger.ts project file](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-cosmosdb/blob/main/src/functions/cosmos_trigger.ts).

You can review the code that defines the Azure Cosmos DB trigger in the [function_app.py project file](https://github.com/Azure-Samples/functions-quickstart-python-azd-cosmosdb/blob/main/function_app.py).

After you review and verify your function code locally, it's time to publish the project to Azure.

## Deploy to Azure

You can run the `azd deploy`

command from Visual Studio Code to deploy the project code to your already provisioned resources in Azure.

Press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Deploy to Azure (deploy)`

.The

`azd deploy`

command packages and deploys your code to the deployment container. The app is then started and runs in the deployed package.After the command completes successfully, your app is running in Azure.


## Invoke the function on Azure

In Visual Studio Code, press

`F1`and in the command palette search for and run the command`Azure: Open in portal`

, select`Function app`

, and choose your new app. Sign in with your Azure account, if necessary.This command opens your new function app in the Azure portal.

In the

**Overview**tab on the main page, select your function app name and then the**Logs**tab.Use the

`NoSQL: Create Item`

command in Visual Studio Code to again add a document to the container as before.Verify again that the function gets triggered by an update in the monitored container.


## Redeploy your code

You can run the `azd deploy`

command as many times as you need to deploy code updates to your function app.

Note

Deployed code files are always overwritten by the latest deployment package.

Your initial responses to `azd`

prompts and any environment variables generated by `azd`

are stored locally in your named environment. Use the `azd env get-values`

command to review all of the variables in your environment that were used when creating Azure resources.

## Clean up resources

When you're done working with your function app and related resources, you can use this command to delete the function app and its related resources from Azure and avoid incurring any further costs:

```
azd down --no-prompt
```


Note

The `--no-prompt`

option instructs `azd`

to delete your resource group without a confirmation from you.

This command doesn't affect your local code project.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-signalr-service-input -->

# SignalR Service input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Before a client can connect to Azure SignalR Service, it must retrieve the service endpoint URL and a valid access token. The *SignalRConnectionInfo* input binding produces the SignalR Service endpoint URL and a valid token that are used to connect to the service. The token is time-limited and can be used to authenticate a specific user to a connection. Therefore, you shouldn't cache the token or share it between clients. Usually you use *SignalRConnectionInfo* with HTTP trigger for clients to retrieve the connection information.

For more information on how to use this binding to create a "negotiate" function that is compatible with a SignalR client SDK, see [Azure Functions development and configuration with Azure SignalR Service](../azure-signalr/signalr-concept-serverless-development-config).

When not explicitly declared, assume that examples are using the default connection setting value of `AzureSignalRConnectionString`

. For information on setup and configuration details, see the [overview](functions-bindings-signalr-service).

## Example

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The following example shows a [C# function](dotnet-isolated-process-guide) that acquires SignalR connection information using the input binding and returns it over HTTP.

```
[Function(nameof(Negotiate))]
public static string Negotiate([HttpTrigger(AuthorizationLevel.Anonymous)] HttpRequestData req,
[SignalRConnectionInfoInput(HubName = "serverless")] string connectionInfo)
{
// The serialization of the connection info object is done by the framework. It should be camel case. The SignalR client respects the camel case response only.
return connectionInfo;
}
```


The following example shows a SignalR connection info input binding in a *function.json* file and a function that uses the binding to return the connection information.

Here's binding data for the example in the *function.json* file:

```
{
"type": "signalRConnectionInfo",
"name": "connectionInfo",
"hubName": "hubName1",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "in"
}
```


Here's the JavaScript code:

```
const { app, input } = require('@azure/functions');
const inputSignalR = input.generic({
type: 'signalRConnectionInfo',
name: 'connectionInfo',
hubName: 'hubName1',
connectionStringSetting: 'AzureSignalRConnectionString',
});
app.post('negotiate', {
authLevel: 'function',
handler: (request, context) => {
return { body: JSON.stringify(context.extraInputs.get(inputSignalR)) }
},
route: 'negotiate',
extraInputs: [inputSignalR],
});
```


Complete PowerShell examples are pending.

The following example shows a SignalR connection info input binding in a *function.json* file and a [Python function](functions-reference-python) that uses the binding to return the connection information.

Here's the Python code:

```
def main(req: func.HttpRequest, connectionInfoJson: str) -> func.HttpResponse:
return func.HttpResponse(
connectionInfoJson,
status_code=200,
headers={
'Content-type': 'application/json'
}
)
```


The following example shows a [Java function](functions-reference-java) that acquires SignalR connection information using the input binding and returns it over HTTP.

```
@FunctionName("negotiate")
public SignalRConnectionInfo negotiate(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST },
authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> req,
@SignalRConnectionInfoInput(
name = "connectionInfo",
HubName = "hubName1") SignalRConnectionInfo connectionInfo) {
return connectionInfo;
}
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attribute to define the function. C# script instead uses a function.json configuration file.

The following table explains the properties of the `SignalRConnectionInfoInput`

attribute:

| Attribute property | Description |
|---|---|
HubName |
Required. The hub name. |
ConnectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |
UserId |
Optional. The user identifier of a SignalR connection. You can use a
|

**IdToken****ClaimTypeList**. You can use a[binding expression](#binding-expressions-for-http-trigger)to bind the value to an HTTP request header or query.**ClaimTypeList****IdToken**.## Annotations

The following table explains the supported settings for the `SignalRConnectionInfoInput`

annotation.

| Setting | Description |
|---|---|
name |
Variable name used in function code for connection info object. |
hubName |
Required. The hub name. |
connectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |
userId |
Optional. The user identifier of a SignalR connection. You can use a
|

**idToken****claimTypeList**. You can use a[binding expression](#binding-expressions-for-http-trigger)to bind the value to an HTTP request header or query.**claimTypeList****idToken**.## Annotations

The following table explains the supported settings for the `SignalRConnectionInfoInput`

annotation.

| Setting | Description |
|---|---|
name |
Variable name used in function code for connection info object. |
hubName |
Required. The hub name. |
connectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |
userId |
Optional. The user identifier of a SignalR connection. You can use a
|

**idToken****claimTypeList**. You can use a[binding expression](#binding-expressions-for-http-trigger)to bind the value to an HTTP request header or query.**claimTypeList****idToken**.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `signalRConnectionInfo` . |
direction |
Must be set to `in` . |
hubName |
Required. The hub name. |
connectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |
userId |
Optional. The user identifier of a SignalR connection. You can use a
|

**idToken****claimTypeList**. You can use a[binding expression](#binding-expressions-for-http-trigger)to bind the value to an HTTP request header or query.**claimTypeList****idToken**.Warning

For the simplicity, we omit the authentication and authorization parts in this sample. As a result, this endpoint is publicly accessible without any restrictions. To ensure the security of your negotiation endpoint, you should implement appropriate authentication and authorization mechanisms based on your specific requirements. For guidance on protecting your HTTP endpoints, see the following articles:

## Usage

### Managed identity-based connections

For optimal security, your function app should use managed identities when connecting to the Azure SignalR service instead of using a connection string, which contains a shared secret key. For more information, see [Authorize requests to Azure SignalR Service resources with Microsoft Entra managed identities](../azure-signalr/signalr-howto-authorize-managed-identity#azure-signalr-service-bindings-in-azure-functions).

### Authenticated tokens

When an authenticated client triggers the function, you can add a user ID claim to the generated token. You can easily add authentication to a function app using [App Service Authentication](../app-service/overview-authentication-authorization).

App Service authentication sets HTTP headers named `x-ms-client-principal-id`

and `x-ms-client-principal-name`

that contain the authenticated user's client principal ID and name, respectively.

You can set the `UserId`

property of the binding to the value from either header using a [binding expression](#binding-expressions-for-http-trigger): `{headers.x-ms-client-principal-id}`

or `{headers.x-ms-client-principal-name}`

.

```
[Function("Negotiate")]
public static string Negotiate([HttpTrigger(AuthorizationLevel.Anonymous)] HttpRequestData req,
[SignalRConnectionInfoInput(HubName = "hubName1", UserId = "{headers.x-ms-client-principal-id}")] string connectionInfo)
{
// The serialization of the connection info object is done by the framework. It should be camel case. The SignalR client respects the camel case response only.
return connectionInfo;
}
```


```
@FunctionName("negotiate")
public SignalRConnectionInfo negotiate(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST, HttpMethod.GET },
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> req,
@SignalRConnectionInfoInput(name = "connectionInfo", hubName = "hubName1", userId = "{headers.x-ms-signalr-userid}") SignalRConnectionInfo connectionInfo) {
return connectionInfo;
}
```


Here's binding data in the *function.json* file:

```
{
"type": "signalRConnectionInfo",
"name": "connectionInfo",
"hubName": "hubName1",
"userId": "{headers.x-ms-client-principal-id}",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "in"
}
```


Here's the JavaScript code:

```
const { app, input } = require('@azure/functions');
const inputSignalR = input.generic({
type: 'signalRConnectionInfo',
name: 'connectionInfo',
hubName: 'hubName1',
connectionStringSetting: 'AzureSignalRConnectionString',
userId: '{headers.x-ms-client-principal-id}',
});
app.post('negotiate', {
authLevel: 'function',
handler: (request, context) => {
return { body: JSON.stringify(context.extraInputs.get(inputSignalR)) }
},
route: 'negotiate',
extraInputs: [inputSignalR],
});
```


Complete PowerShell examples are pending.

Here's the Python code:

```
def main(req: func.HttpRequest, connectionInfo: str) -> func.HttpResponse:
# connectionInfo contains an access key token with a name identifier
# claim set to the authenticated user
return func.HttpResponse(
connectionInfo,
status_code=200,
headers={
'Content-type': 'application/json'
}
)
```


```
@FunctionName("negotiate")
public SignalRConnectionInfo negotiate(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST },
authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> req,
@SignalRConnectionInfoInput(
name = "connectionInfo",
HubName = "hubName1",
userId = "{headers.x-ms-client-principal-id}") SignalRConnectionInfo connectionInfo) {
return connectionInfo;
}
```


### Binding expressions for HTTP trigger

[
It's a common scenario that the values of some attributes of SignalR input binding come from HTTP requests. Therefore, we show how to bind values from HTTP requests to SignalR input binding attributes via ][binding expression](functions-bindings-expressions-patterns#trigger-metadata).

| HTTP metadata type | Binding expression format | Description | Example |
|---|---|---|---|
| HTTP request query | `{query.QUERY_PARAMETER_NAME}` |
Binds the value of corresponding query parameter to an attribute | `{query.userName}` |
| HTTP request header | `{headers.HEADER_NAME}` |
Binds the value of a header to an attribute | `{headers.token}` |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/storage-considerations -->

# Storage considerations for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create a function app instance in Azure, you must provide access to a default Azure Storage account. The following diagram and table detail how Azure Functions uses services in the default storage account:


| Storage service | Functions usage |
|---|---|
|

1.Deployment source for apps that run in a

[Flex Consumption plan](flex-consumption-plan).Used by default for

[task hubs in Durable Functions](durable/durable-functions-task-hubs).Can be used to store function app code for

[Linux Consumption remote build](functions-deployment-technologies#remote-build)or as part of[external package URL deployments](functions-deployment-technologies#external-package-url).[Azure Files](../storage/files/storage-files-introduction)2[Consumption Plan](consumption-plan)and[Premium Plan](functions-premium-plan).Maintain

[extension bundles](extension-bundles).Store deployment logs.

Supports

[Managed dependencies in PowerShell](functions-reference-powershell#managed-dependencies-feature).[Azure Queue storage](../storage/queues/storage-queues-introduction)[task hubs in Durable Functions](durable/durable-functions-task-hubs). Used for failure and retry handling in[specific Azure Functions triggers](functions-bindings-storage-blob-trigger). Used for object tracking by the[Blob storage trigger](functions-bindings-storage-blob-trigger).[Azure Table storage](../storage/tables/table-storage-overview)[task hubs in Durable Functions](durable/durable-functions-task-hubs).Used for tracking

[diagnostic events](functions-diagnostics).- Blob storage is the default store for function keys, but you can
[configure an alternate store](function-keys-how-to#manage-key-storage). - Azure Files is set up by default, but you can
[create an app without Azure Files](#create-an-app-without-azure-files)under certain conditions.

## Important considerations

You must strongly consider the following facts regarding the storage accounts used by your function apps:

When your function app is hosted on the Consumption plan or Premium plan, your function code and configuration files are stored in Azure Files in the linked storage account. When you delete this storage account, the content is deleted and can't be recovered. For more information, see

[Storage account was deleted](functions-recover-storage-account#storage-account-was-deleted).Important data, such as function code,

[access keys](function-keys-how-to), and other important service-related data, persist in the storage account. You must carefully manage access to the storage accounts used by function apps in the following ways:Audit and limit the access of apps and users to the storage account based on a least-privilege model. Permissions to the storage account can come from

[data actions in the assigned role](../role-based-access-control/role-definitions#control-and-data-actions)or through permission to perform the[listKeys operation](/en-us/rest/api/storagerp/storage-accounts/list-keys).Monitor both control plane activity (such as retrieving keys) and data plane operations (such as writing to a blob) in your storage account. Consider maintaining storage logs in a location other than Azure Storage. For more information, see

[Storage logs](#storage-logs).


## Storage account requirements

Storage accounts that you create during the function app creation process in the Azure portal work with the new function app. When you choose to use an existing storage account, the list provided doesn't include certain unsupported storage accounts. The following restrictions apply to storage accounts used by your function app. Make sure an existing storage account meets these requirements:

The account type must support Blob, Queue, and Table storage. Some storage accounts don't support queues and tables. These accounts include blob-only storage accounts and Azure Premium Storage. To learn more about storage account types, see

[Storage account overview](../storage/common/storage-account-overview).You can't use a network-secured storage account when your function app is hosted in the

[Consumption plan](consumption-plan).When you create your function app in the Azure portal, you can only choose an existing storage account in the same region as the function app that you create. This requirement is a performance optimization and not a strict limitation. To learn more, see

[Storage account location](#storage-account-location).When you create your function app on a plan with

[availability zone support](/en-us/azure/reliability/reliability-functions#availability-zone-support)enabled, only[zone-redundant storage accounts](../storage/common/storage-redundancy#zone-redundant-storage)are supported.

When you use deployment automation to create your function app with a network-secured storage account, you must include specific networking configurations in your ARM template or Bicep file. If you don't include these settings and resources, your automated deployment might fail in validation. For ARM template and Bicep guidance, see [Secured deployments](functions-infrastructure-as-code#secured-deployments). For an overview on configuring storage accounts with networking, see [How to use a secured storage account with Azure Functions](configure-networking-how-to).

## Storage account guidance

Every function app requires a storage account to operate. When you delete that account, your function app stops running. To troubleshoot storage-related issues, see [How to troubleshoot storage-related issues](functions-recover-storage-account). The following considerations apply to the storage account used by function apps.

### Storage account location

For best performance, your function app should use a storage account in the same region, which reduces latency. The Azure portal enforces this best practice. If you need to use a storage account in a region different from your function app, you must create your function app outside of the Azure portal.

The storage account must be accessible to the function app. If you need to use a secured storage account, consider [restricting your storage account to a virtual network](functions-networking-options#restrict-your-storage-account-to-a-virtual-network).

### Storage account connection setting

By default, function apps configure the `AzureWebJobsStorage`

connection as a connection string stored in the [AzureWebJobsStorage application setting](functions-app-settings#azurewebjobsstorage). You can also [configure AzureWebJobsStorage to use an identity-based connection](functions-reference#connecting-to-host-storage-with-an-identity) without a secret.

Function apps running in a Consumption plan (Windows only) or an Elastic Premium plan (Windows or Linux) can use Azure Files to store the images required to enable dynamic scaling. For these plans, set the connection string for the storage account in the [WEBSITE_CONTENTAZUREFILECONNECTIONSTRING](functions-app-settings#website_contentazurefileconnectionstring) setting and the name of the file share in the [WEBSITE_CONTENTSHARE](functions-app-settings#website_contentshare) setting. This value is usually the same account used for `AzureWebJobsStorage`

. You can also [create a function app that doesn't use Azure Files](#create-an-app-without-azure-files), but scaling might be limited.

Note

You must update a storage account connection string when you regenerate storage keys. For more information, see [Create an Azure storage account](../storage/common/storage-account-create).

### Shared storage accounts

Multiple function apps can share the same storage account without any problems. For example, in Visual Studio, you can develop multiple apps by using the [Azurite storage emulator](functions-develop-local#local-storage-emulator). In this case, the emulator acts like a single storage account. The same storage account that your function app uses can also store your application data. However, this approach isn't always a good idea in a production environment.

You might need to use separate storage accounts to [avoid host ID collisions](#avoiding-host-id-collisions).

### Lifecycle management policy considerations

Don't apply [lifecycle management policies](../storage/blobs/lifecycle-management-overview) to your Blob Storage account used by your function app. Functions uses Blob storage to persist important information, such as [function access keys](function-keys-how-to). Policies could remove blobs, such as keys, needed by the Functions host. If you must use policies, exclude containers used by Functions, which are prefixed with `azure-webjobs`

or `scm`

.

### Storage logs

Because function code and keys might be persisted in the storage account, logging of activity against the storage account is a good way to monitor for unauthorized access. Azure Monitor resource logs can be used to track events against the storage data plane. See [Monitoring Azure Storage](../storage/blobs/monitor-blob-storage) for details on how to configure and examine these logs.

The [Azure Monitor activity log](/en-us/azure/azure-monitor/essentials/activity-log) shows control plane events, including the [listKeys operation](/en-us/rest/api/storagerp/storage-accounts/list-keys). However, you should also configure resource logs for the storage account to track subsequent use of keys or other identity-based data plane operations. You should have at least the [StorageWrite log category](../storage/blobs/monitor-blob-storage#collection-and-routing) enabled to be able to identify modifications to the data outside of normal Functions operations.

To limit the potential impact of any broadly scoped storage permissions, consider using a nonstorage destination for these logs, such as Log Analytics. For more information, see [Monitoring Azure Blob Storage](../storage/blobs/monitor-blob-storage).

### Optimize storage performance

To maximize performance, use a separate storage account for each function app. This approach is particularly important when you have Durable Functions or Event Hubs triggered functions, which both generate a high volume of storage transactions. When your application logic interacts with Azure Storage, either directly (using the Storage SDK) or through one of the storage bindings, you should use a dedicated storage account. For example, if you have an event hub-triggered function writing some data to blob storage, use two storage accounts: one for the function app and another for the blobs that the function stores.

### Consistent routing through virtual networks

Multiple function apps hosted in the same plan can also use the same storage account for the Azure Files content share, defined by `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

. When you secure this storage account by using a virtual network, all of these apps (including slots) should use the same value for `vnetContentShareEnabled`

(formerly `WEBSITE_CONTENTOVERVNET`

) and the same virtual network integration configuration to ensure that traffic routes consistently through the intended virtual network. A mismatch in this setting between apps that use the same Azure Files storage account might result in traffic routing through public networks. In this configuration, storage account network rules block access.

## Working with blobs

A key scenario for Functions is file processing of files in a blob container, such as for image processing or sentiment analysis. To learn more, see [Process file uploads](functions-scenarios#process-file-uploads).

### Trigger on a blob container

There are several ways to run your function code based on changes to blobs in a storage container, as indicated by this diagram:


Use the following table to determine which function trigger best fits your needs for processing added or updated blobs in a container:

| Strategy | Blob trigger (polling) | Blob trigger (event-driven) | Queue trigger | Event Grid trigger |
|---|---|---|---|---|
| Latency | High (up to 10 min) | Low | Medium | Low |
|

[Blob storage](functions-bindings-storage-blob-trigger)[Blob storage](functions-bindings-storage-blob-trigger)[Queue storage](functions-bindings-storage-queue-trigger)[Event Grid](functions-bindings-event-grid-trigger)[Blob name pattern](functions-bindings-storage-blob-trigger#blob-name-patterns)[Event filters](../storage/blobs/storage-blob-event-overview#filtering-events)[Event filters](../storage/blobs/storage-blob-event-overview#filtering-events)[event subscription](../event-grid/concepts#event-subscriptions)[Flex Consumption plan](flex-consumption-plan)[inbound access restrictions](functions-networking-options#inbound-access-restrictions)3[Blob storage trigger reference](functions-bindings-storage-blob-trigger#example).`Source`

parameter value of `EventGrid`

. For more information, see [Tutorial: Trigger Azure Functions on blob containers using an event subscription](functions-event-grid-blob-trigger).[How to work with Event Grid triggers and bindings in Azure Functions](event-grid-how-tos).- Blob storage input and output bindings support blob-only accounts.
- High scale can be loosely defined as containers that have more than 100,000 blobs in them or storage accounts that have more than 100 blob updates per second.
- You can work around inbound access restrictions by having the event subscription deliver events over an encrypted channel in public IP space using a known user identity. For more information, see
[Deliver events securely using managed identities](../event-grid/deliver-events-using-managed-identity).

## Storage data encryption

Azure Storage encrypts all data in a storage account at rest. For more information, see [Azure Storage encryption for data at rest](../storage/common/storage-service-encryption).

By default, data is encrypted with Microsoft-managed keys. For more control over encryption keys, you can supply customer-managed keys to use for encryption of blob and file data. These keys must be present in Azure Key Vault for Functions to be able to access the storage account. To learn more, see [Encrypt your application data at rest using customer-managed keys](configure-encrypt-at-rest-using-cmk).

### In-region data residency

When all customer data must remain within a single region, the storage account associated with the function app must be one with [in-region redundancy](../storage/common/storage-redundancy). An in-region redundant storage account also must be used with [Azure Durable Functions](durable/durable-functions-azure-storage-provider#storage-account-selection).

Other platform-managed customer data is only stored within the region when hosting in an internally load-balanced App Service Environment (ASE). To learn more, see [ASE zone redundancy](../app-service/environment/zone-redundancy#in-region-data-residency).

## Host ID considerations

Note

The Host ID considerations in this section don't apply when your app runs in a [Flex Consumption plan](flex-consumption-plan). In this hosting plan, the Host ID value is created in a way that avoids these potential issues.

Functions uses a host ID value as a way to uniquely identify a particular function app in stored artifacts. By default, this ID is autogenerated from the name of the function app, truncated to the first 32 characters. This ID is then used when storing per-app correlation and tracking information in the linked storage account. When you have function apps with names longer than 32 characters and when the first 32 characters are identical, this truncation can result in duplicate host ID values. When two function apps with identical host IDs use the same storage account, you get a host ID collision because stored data can't be uniquely linked to the correct function app.

Note

This same kind of host ID collision can occur between a function app in a production slot and the same function app in a staging slot, when both slots use the same storage account.

In version 4.x of the Functions runtime, an error is logged and the host is stopped, resulting in a hard failure. For more information, see [HostID Truncation can cause collisions](https://github.com/Azure/azure-functions-host/issues/2015).

### Avoiding host ID collisions

You can use the following strategies to avoid host ID collisions:

- Use a separate storage account for each function app or slot involved in the collision.
- Rename one of your function apps to a value fewer than 32 characters in length, which changes the computed host ID for the app and removes the collision.
- Set an explicit host ID for one or more of the colliding apps. To learn more, see
[Override the host ID](#override-the-host-id).

Important

Changing the storage account associated with an existing function app or changing the app's host ID can affect the behavior of existing functions. For example, a Blob storage trigger tracks whether it's processed individual blobs by writing receipts under a specific host ID path in storage. When the host ID changes or you point to a new storage account, previously processed blobs could be reprocessed.

### Override the host ID

You can explicitly set a specific host ID for your function app in the application settings by using the `AzureFunctionsWebHost__hostid`

setting. For more information, see [AzureFunctionsWebHost__hostid](functions-app-settings#azurefunctionswebhost__hostid).

When the collision occurs between slots, you must set a specific host ID for each slot, including the production slot. You must also mark these settings as [deployment settings](functions-deployment-slots#create-a-deployment-setting) so they don't get swapped. To learn how to create app settings, see [Work with application settings](functions-how-to-use-azure-function-app-settings#settings).

## Azure Arc-enabled clusters

When your function app is deployed to an Azure Arc-enabled Kubernetes cluster, your function app might not require a storage account. In this case, functions only require a storage account when your function app uses a trigger that requires storage. The following table indicates which triggers might require a storage account and which don't.

| Not required | might require storage |
|---|---|
| •
•
•
•
•
|

[Azure SQL](functions-bindings-azure-sql)•

[Blob storage](functions-bindings-storage-blob)•

[Event Grid](functions-bindings-event-grid)•

[Event Hubs](functions-bindings-event-hubs)•

[IoT Hub](functions-bindings-event-iot)•

[Queue storage](functions-bindings-storage-queue)•

[SendGrid](functions-bindings-sendgrid)•

[SignalR](functions-bindings-signalr-service)•

[Table storage](functions-bindings-storage-table)•

[Timer](functions-bindings-timer)•

[Twilio](functions-bindings-twilio)To create a function app on an Azure Arc-enabled Kubernetes cluster without storage, you must use the Azure CLI command [az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create). The version of the Azure CLI must include version 0.1.7 or a later version of the [appservice-kube extension](/en-us/cli/azure/appservice/kube). Use the `az --version`

command to verify that the extension is installed and is the correct version.

Creating your function app resources using methods other than the Azure CLI requires an existing storage account. If you plan to use any triggers that require a storage account, you should create the account before you create the function app.

## Create an app without Azure Files

The Azure Files service provides a shared file system that supports high-scale scenarios. When your function app runs in an Elastic Premium plan or on Windows in a Consumption plan, an Azure Files share is created by default in your storage account. This share is used by Functions to enable certain features, like log streaming. It's also used as a shared package deployment location, which guarantees the consistency of your deployed function code across all instances.

By default, function apps hosted in Premium and Consumption plans use [zip deployment](deployment-zip-push), with deployment packages stored in this Azure file share. This section is only relevant to these hosting plans.

Using Azure Files requires the use of a connection string, which is stored in your app settings as [ WEBSITE_CONTENTAZUREFILECONNECTIONSTRING](functions-app-settings#website_contentazurefileconnectionstring). Azure Files doesn't currently support identity-based connections. If your scenario requires you to not store any secrets in app settings, you must remove your app's dependency on Azure Files. You can avoid this dependency by creating your app without the default Azure Files dependency.

Note

You should also consider running your function app in the Flex Consumption plan, which provides greater control over the deployment package, including the ability use managed identity connections. For more information, see [Configure deployment settings](flex-consumption-how-to#configure-deployment-settings).

To run your app without the Azure file share, you must meet the following requirements:

- You must
[deploy your package to a remote Azure Blob storage container](run-functions-from-deployment-package)and then set the URL that provides access to that package as theapp setting. This approach lets you store your app content in Blob storage instead of Azure Files, which does support`WEBSITE_RUN_FROM_PACKAGE`

[managed identities](run-functions-from-deployment-package#fetch-a-package-from-azure-blob-storage-using-a-managed-identity).

You must manually update the deployment package and maintain the deployment package URL, which likely contains a shared access signature (SAS).

You should also note the following considerations:

- The app can't use version 1.x of the Functions runtime.
- Your app can't rely on a shared writeable file system.
- Portal editing isn't supported.
- Log streaming experiences in clients such as the Azure portal default to file system logs. You should instead rely on Application Insights logs.

If the preceding requirements suit your scenario, you can proceed to create a function app without Azure Files. Create an app without the `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

and `WEBSITE_CONTENTSHARE`

app settings in one of these ways:

- Bicep/ARM templates: remove the two app settings from the ARM template or Bicep file and then deploy the app using the modified template.
- The Azure portal: unselect
**Add an Azure Files connection**in the**Storage**tab when you create the app in the Azure portal.

Azure Files is used to enable dynamic scale-out for Functions. Scaling could be limited when you run your app without Azure Files in the Elastic Premium plan and Consumption plans running on Windows.

## Mount file shares

*This functionality is current only available when running on Linux.*

You can mount existing Azure Files shares to your Linux function apps. By mounting a share to your Linux function app, you can use existing machine learning models or other data in your functions.

Important

After 30 September 2028, the option to host your function app on Linux in a Consumption plan is retired. To avoid disruptions, migrate your existing Consumption plan apps that run on Linux to the [Flex Consumption plan](flex-consumption-plan) before that date. Apps running on Windows in a Consumption plan aren't affected by this change.
For more information, see the [Linux Consumption plan retirement notice](https://go.microsoft.com/fwlink/?linkid=2335809).

You can use the following command to mount an existing share to your Linux function app.

[az webapp config storage-account add](/en-us/cli/azure/webapp/config/storage-account#az-webapp-config-storage-account-add)

In this command, `share-name`

is the name of the existing Azure Files share. `custom-id`

can be any string that uniquely defines the share when mounted to the function app. Also, `mount-path`

is the path from which the share is accessed in your function app. `mount-path`

must be in the format `/dir-name`

, and it can't start with `/home`

.

For a complete example, see [Create a Python function app and mount an Azure Files share](scripts/functions-cli-mount-files-storage-linux).

Currently, only a `storage-type`

of `AzureFiles`

is supported. You can only mount five shares to a given function app. Mounting a file share can increase the cold start time by at least 200-300 ms, or even more when the storage account is in a different region.

The mounted share is available to your function code at the `mount-path`

specified. For example, when `mount-path`

is `/path/to/mount`

, you can access the target directory by file system APIs, as in the following Python example:

```
import os
...
files_in_share = os.listdir("/path/to/mount")
```


## Related article

Learn more about Azure Functions hosting options.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2-output -->

# Azure Cosmos DB output binding for Azure Functions 2.x and higher

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Cosmos DB output binding lets you write a new document to an Azure Cosmos DB database using the SQL API.

For information on setup and configuration details, see the [overview](functions-bindings-cosmosdb-v2).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

## Example

Unless otherwise noted, examples in this article target version 3.x of the [Azure Cosmos DB extension](functions-bindings-cosmosdb-v2). For use with extension version 4.x, you need to replace the string `collection`

in property and attribute names with `container`

and `connection_string_setting`

with `connection`

.

The following code defines a `MyDocument`

type:

```
public class MyDocument
{
public string? Id { get; set; }
public string? Text { get; set; }
public int Number { get; set; }
public bool Boolean { get; set; }
}
```


In the following example, the return type is an [ IReadOnlyList<T>](/en-us/dotnet/api/system.collections.generic.ireadonlylist-1), which is a modified list of documents from trigger binding parameter:

```
using System.Collections.Generic;
using System.Linq;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.Logging;
namespace SampleApp
{
public class CosmosDBFunction
{
private readonly ILogger<CosmosDBFunction> _logger;
public CosmosDBFunction(ILogger<CosmosDBFunction> logger)
{
_logger = logger;
}
//<docsnippet_exponential_backoff_retry_example>
[Function(nameof(CosmosDBFunction))]
[ExponentialBackoffRetry(5, "00:00:04", "00:15:00")]
[CosmosDBOutput("%CosmosDb%", "%CosmosContainerOut%", Connection = "CosmosDBConnection", CreateIfNotExists = true)]
public object? Run(
[CosmosDBTrigger(
"%CosmosDb%",
"%CosmosContainerIn%",
Connection = "CosmosDBConnection",
LeaseContainerName = "leases",
CreateLeaseContainerIfNotExists = true)] IReadOnlyList<MyDocument> input,
FunctionContext context)
{
if (input != null && input.Any())
{
foreach (var doc in input)
{
_logger.LogInformation("Doc Id: {id}", doc.Id);
}
// Cosmos Output
return input.Select(p => new { id = p.Id });
}
return null;
}
//</docsnippet_exponential_backoff_retry_example>
}
```


[Queue trigger, save message to database via return value](#queue-trigger-save-message-to-database-via-return-value-java)[HTTP trigger, save one document to database via return value](#http-trigger-save-one-document-to-database-via-return-value-java)[HTTP trigger, save one document to database via OutputBinding](#http-trigger-save-one-document-to-database-via-outputbinding-java)[HTTP trigger, save multiple documents to database via OutputBinding](#http-trigger-save-multiple-documents-to-database-via-outputbinding-java)

### Queue trigger, save message to database via return value

The following example shows a Java function that adds a document to a database with data from a message in Queue storage.

```
@FunctionName("getItem")
@CosmosDBOutput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
connectionStringSetting = "AzureCosmosDBConnection")
public String cosmosDbQueryById(
@QueueTrigger(name = "msg",
queueName = "myqueue-items",
connection = "AzureWebJobsStorage")
String message,
final ExecutionContext context) {
return "{ id: \"" + System.currentTimeMillis() + "\", Description: " + message + " }";
}
```


#### HTTP trigger, save one document to database via return value

The following example shows a Java function whose signature is annotated with `@CosmosDBOutput`

and has return value of type `String`

. The JSON document returned by the function is automatically written to the corresponding Azure Cosmos DB collection.

```
@FunctionName("WriteOneDoc")
@CosmosDBOutput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
connectionStringSetting = "Cosmos_DB_Connection_String")
public String run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
final ExecutionContext context) {
// Item list
context.getLogger().info("Parameters are: " + request.getQueryParameters());
// Parse query parameter
String query = request.getQueryParameters().get("desc");
String name = request.getBody().orElse(query);
// Generate random ID
final int id = Math.abs(new Random().nextInt());
// Generate document
final String jsonDocument = "{\"id\":\"" + id + "\", " +
"\"description\": \"" + name + "\"}";
context.getLogger().info("Document to be saved: " + jsonDocument);
return jsonDocument;
}
```


### HTTP trigger, save one document to database via OutputBinding

The following example shows a Java function that writes a document to Azure Cosmos DB via an `OutputBinding<T>`

output parameter. In this example, the `outputItem`

parameter needs to be annotated with `@CosmosDBOutput`

, not the function signature. Using `OutputBinding<T>`

lets your function take advantage of the binding to write the document to Azure Cosmos DB while also allowing returning a different value to the function caller, such as a JSON or XML document.

```
@FunctionName("WriteOneDocOutputBinding")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@CosmosDBOutput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
connectionStringSetting = "Cosmos_DB_Connection_String")
OutputBinding<String> outputItem,
final ExecutionContext context) {
// Parse query parameter
String query = request.getQueryParameters().get("desc");
String name = request.getBody().orElse(query);
// Item list
context.getLogger().info("Parameters are: " + request.getQueryParameters());
// Generate random ID
final int id = Math.abs(new Random().nextInt());
// Generate document
final String jsonDocument = "{\"id\":\"" + id + "\", " +
"\"description\": \"" + name + "\"}";
context.getLogger().info("Document to be saved: " + jsonDocument);
// Set outputItem's value to the JSON document to be saved
outputItem.setValue(jsonDocument);
// return a different document to the browser or calling client.
return request.createResponseBuilder(HttpStatus.OK)
.body("Document created successfully.")
.build();
}
```


### HTTP trigger, save multiple documents to database via OutputBinding

The following example shows a Java function that writes multiple documents to Azure Cosmos DB via an `OutputBinding<T>`

output parameter. In this example, the `outputItem`

parameter is annotated with `@CosmosDBOutput`

, not the function signature. The output parameter, `outputItem`

has a list of `ToDoItem`

objects as its template parameter type. Using `OutputBinding<T>`

lets your function take advantage of the binding to write the documents to Azure Cosmos DB while also allowing returning a different value to the function caller, such as a JSON or XML document.

```
@FunctionName("WriteMultipleDocsOutputBinding")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@CosmosDBOutput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
connectionStringSetting = "Cosmos_DB_Connection_String")
OutputBinding<List<ToDoItem>> outputItem,
final ExecutionContext context) {
// Parse query parameter
String query = request.getQueryParameters().get("desc");
String name = request.getBody().orElse(query);
// Item list
context.getLogger().info("Parameters are: " + request.getQueryParameters());
// Generate documents
List<ToDoItem> items = new ArrayList<>();
for (int i = 0; i < 5; i ++) {
// Generate random ID
final int id = Math.abs(new Random().nextInt());
// Create ToDoItem
ToDoItem item = new ToDoItem(String.valueOf(id), name);
items.add(item);
}
// Set outputItem's value to the list of POJOs to be saved
outputItem.setValue(items);
context.getLogger().info("Document to be saved: " + items);
// return a different document to the browser or calling client.
return request.createResponseBuilder(HttpStatus.OK)
.body("Documents created successfully.")
.build();
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@CosmosDBOutput`

annotation on parameters that is written to Azure Cosmos DB. The annotation parameter type should be `OutputBinding<T>`

, where `T`

is either a native Java type or a POJO.

The following example shows a storage queue triggered [TypeScript function](functions-reference-node?tabs=typescript) for a queue that receives JSON in the following format:

```
{
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


The function creates Azure Cosmos DB documents in the following format for each record:

```
{
"id": "John Henry-123456",
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


Here's the TypeScript code:

```
import { app, InvocationContext, output } from '@azure/functions';
interface MyQueueItem {
name: string;
employeeId: string;
address: string;
}
interface MyCosmosItem {
id: string;
name: string;
employeeId: string;
address: string;
}
export async function storageQueueTrigger1(queueItem: MyQueueItem, context: InvocationContext): Promise<MyCosmosItem> {
return {
id: `${queueItem.name}-${queueItem.employeeId}`,
name: queueItem.name,
employeeId: queueItem.employeeId,
address: queueItem.address,
};
}
app.storageQueue('storageQueueTrigger1', {
queueName: 'inputqueue',
connection: 'MyStorageConnectionAppSetting',
return: output.cosmosDB({
databaseName: 'MyDatabase',
collectionName: 'MyCollection',
createIfNotExists: true,
connectionStringSetting: 'MyAccount_COSMOSDB',
}),
handler: storageQueueTrigger1,
});
```


To output multiple documents, return an array instead of a single object. For example:

```
return [
{
id: 'John Henry-123456',
name: 'John Henry',
employeeId: '123456',
address: 'A town nearby',
},
{
id: 'John Doe-123457',
name: 'John Doe',
employeeId: '123457',
address: 'A town far away',
},
];
```


The following example shows a storage queue triggered [JavaScript function](functions-reference-node) for a queue that receives JSON in the following format:

```
{
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


The function creates Azure Cosmos DB documents in the following format for each record:

```
{
"id": "John Henry-123456",
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


Here's the JavaScript code:

```
const { app, output } = require('@azure/functions');
const cosmosOutput = output.cosmosDB({
databaseName: 'MyDatabase',
collectionName: 'MyCollection',
createIfNotExists: true,
connectionStringSetting: 'MyAccount_COSMOSDB',
});
app.storageQueue('storageQueueTrigger1', {
queueName: 'inputqueue',
connection: 'MyStorageConnectionAppSetting',
return: cosmosOutput,
handler: (queueItem, context) => {
return {
id: `${queueItem.name}-${queueItem.employeeId}`,
name: queueItem.name,
employeeId: queueItem.employeeId,
address: queueItem.address,
};
},
});
```


To output multiple documents, return an array instead of a single object. For example:

```
return [
{
id: 'John Henry-123456',
name: 'John Henry',
employeeId: '123456',
address: 'A town nearby',
},
{
id: 'John Doe-123457',
name: 'John Doe',
employeeId: '123457',
address: 'A town far away',
},
];
```


The following example shows how to write data to Azure Cosmos DB using an output binding. The binding is declared in the function's configuration file (*functions.json*), and takes data from a queue message and writes out to an Azure Cosmos DB document.

```
{
"name": "EmployeeDocument",
"type": "cosmosDB",
"databaseName": "MyDatabase",
"collectionName": "MyCollection",
"createIfNotExists": true,
"connectionStringSetting": "MyStorageConnectionAppSetting",
"direction": "out"
}
```


In the *run.ps1* file, the object returned from the function is mapped to an `EmployeeDocument`

object, which is persisted in the database.

```
param($QueueItem, $TriggerMetadata)
Push-OutputBinding -Name EmployeeDocument -Value @{
id = $QueueItem.name + '-' + $QueueItem.employeeId
name = $QueueItem.name
employeeId = $QueueItem.employeeId
address = $QueueItem.address
}
```


The following example demonstrates how to write a document to an Azure Cosmos DB database as the output of a function. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.route()
@app.cosmos_db_output(arg_name="documents",
database_name="DB_NAME",
collection_name="COLLECTION_NAME",
create_if_not_exists=True,
connection_string_setting="CONNECTION_SETTING")
def main(req: func.HttpRequest, documents: func.Out[func.Document]) -> func.HttpResponse:
request_body = req.get_body()
documents.set(func.Document.from_json(request_body))
return 'OK'
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#azure-cosmos-db-v2-output).

| Attribute property | Description |
|---|---|
Connection |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see
|

**DatabaseName****ContainerName****CreateIfNotExists***false*because new containers are created with reserved throughput, which has cost implications. For more information, see the[pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).**PartitionKey**`CreateIfNotExists`

is true, it defines the partition key path for the created container. May include binding parameters.**ContainerThroughput**`CreateIfNotExists`

is true, it defines the [throughput](/en-us/azure/cosmos-db/set-throughput)of the created container.**PreferredLocations**`East US,South Central US,North Europe`

.## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, the following properties on the `cosmos_db_output`

:

| Property | Description |
|---|---|
`arg_name` |
The variable name used in function code that represents the list of documents with changes. |
`database_name` |
The name of the Azure Cosmos DB database with the container being monitored. |
`container_name` |
The name of the Azure Cosmos DB container being monitored. |
`create_if_not_exists` |
A Boolean value that indicates whether the database and collection should be created if they do not exist. |
`connection_string_setting` |
The connection string of the Azure Cosmos DB being monitored. |

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

From the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@CosmosDBOutput`

annotation on parameters that write to Azure Cosmos DB. The annotation supports the following properties:

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the binding configuration properties that you set in the *function.json* file, where properties differ by extension version:

| function.json property | Description |
|---|---|
connection |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see
|

**databaseName****containerName****createIfNotExists***false*because new containers are created with reserved throughput, which has cost implications. For more information, see the[pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).**partitionKey**`createIfNotExists`

is true, it defines the partition key path for the created container. May include binding parameters.**containerThroughput**`createIfNotExists`

is true, it defines the [throughput](/en-us/azure/cosmos-db/set-throughput)of the created container.**preferredLocations**`East US,South Central US,North Europe`

.See the [Example section](#example) for complete examples.

## Usage

By default, when you write to the output parameter in your function, a document is created in your database. You should specify the document ID of the output document by specifying the `id`

property in the JSON object passed to the output parameter.

Note

When you specify the ID of an existing document, it gets overwritten by the new output document.

The output function parameter must be defined as `func.Out[func.Document]`

. Refer to the [output example](#example) for details.

The parameter type supported by the Cosmos DB output binding depends on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to write to a single document, the Cosmos DB output binding can bind to the following types:

| Type | Description |
|---|---|
| JSON serializable types | An object representing the JSON content of a document. Functions attempts to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write to multiple documents, the Cosmos DB output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is JSON serializable type |
An array containing multiple documents. Each entry represents one document. |

For other output scenarios, create and use a [CosmosClient](/en-us/dotnet/api/microsoft.azure.cosmos.cosmosclient) with other types from [Microsoft.Azure.Cosmos](/en-us/dotnet/api/microsoft.azure.cosmos) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

## Connections

The `connectionStringSetting`

/`connection`

and `leaseConnectionStringSetting`

/`leaseConnection`

properties are references to environment configuration which specifies how the app should connect to Azure Cosmos DB. They may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections). This option is only available for the`connection`

and`leaseConnection`

versions from[version 4.x or higher of the extension](functions-bindings-cosmosdb-v2?tabs=extensionv4).

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

The connection string for your database account should be stored in an application setting with a name matching the value specified by the connection property of the binding configuration.

### Identity-based connections

If you are using [version 4.x or higher of the extension](functions-bindings-cosmosdb-v2?tabs=extensionv4), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). To do this, you would define settings under a common prefix which maps to the connection property in the trigger and binding configuration.

In this mode, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Account Endpoint | `<CONNECTION_NAME_PREFIX>__accountEndpoint` |
The Azure Cosmos DB account endpoint URI. | https://<database_account_name>.documents.azure.com:443/ |

Additional properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

Cosmos DB does not use Azure RBAC for data operations. Instead, it uses a [Cosmos DB built-in RBAC system](/en-us/azure/cosmos-db/how-to-setup-rbac) which is built on similar concepts. You will need to create a role assignment that provides access to your database account at runtime. Azure RBAC Management roles like [Owner](../role-based-access-control/built-in-roles#owner) are not sufficient. The following table shows built-in roles that are recommended when using the Azure Cosmos DB extension in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles1 |
|---|---|
Trigger2 |
|

[Cosmos DB Built-in Data Reader](/en-us/azure/cosmos-db/how-to-setup-rbac#built-in-role-definitions)[Cosmos DB Built-in Data Contributor](/en-us/azure/cosmos-db/how-to-setup-rbac#built-in-role-definitions)1 These roles cannot be used in an Azure RBAC role assignment. See the [Cosmos DB built-in RBAC system](/en-us/azure/cosmos-db/how-to-setup-rbac) documentation for details on how to assign these roles.

2 When using identity, Cosmos DB treats container creation as a management operation. It is not available as a data-plane operation for the trigger. You will need to ensure that you create the containers needed by the trigger (including the lease container) before setting up your function.

## Exceptions and return codes

| Binding | Reference |
|---|---|
| Azure Cosmos DB |
|

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-first-java-gradle -->

# Use Java and Gradle to create and publish a function to Azure

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to build and publish a Java function project to Azure Functions with the Gradle command-line tool. When you're done, your function code runs in Azure in a [serverless hosting plan](consumption-plan) and is triggered by an HTTP request.

Note

If Gradle is not your preferred development tool, check out our similar tutorials for Java developers using [Maven](how-to-create-function-azure-cli?pivots=programming-language-java), [IntelliJ IDEA](/en-us/azure/developer/java/toolkit-for-intellij/quickstart-functions) and [VS Code](how-to-create-function-vs-code?pivot=programming-language-java).

## Prerequisites

To develop functions using Java, you must have the following installed:

[Java Developer Kit](/en-us/azure/developer/java/fundamentals/java-support-on-azure), version 8, 11, 17 or 21. (Java 21 is currently supported on Linux only)[Azure CLI](/en-us/cli/azure)[Azure Functions Core Tools](functions-run-local#v2)version 2.6.666 or above[Gradle](https://gradle.org/), version 6.8 and above

You also need an active Azure subscription. If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

Important

The JAVA_HOME environment variable must be set to the install location of the JDK to complete this quickstart.

## Prepare a Functions project

Use the following command to clone the sample project:

```
git clone https://github.com/Azure-Samples/azure-functions-samples-java.git
cd azure-functions-samples-java/triggers-bindings
```


Open `build.gradle`

and change the `appName`

in the following section to a unique name to avoid domain name conflict when deploying to Azure.

```
azurefunctions {
resourceGroup = 'java-functions-group'
appName = 'azure-functions-sample-demo'
pricingTier = 'Consumption'
region = 'westus'
runtime {
os = 'windows'
}
localDebug = "transport=dt_socket,server=y,suspend=n,address=5005"
}
```


Open the new Function.java file from the *src/main/java* path in a text editor and review the generated code. This code is an [HTTP triggered](functions-bindings-http-webhook) function that echoes the body of the request.

## Run the function locally

Run the following command to build then run the function project:

```
gradle jar --info
gradle azureFunctionsRun
```


You see output like the following from Azure Functions Core Tools when you run the project locally:

... Now listening on: http://0.0.0.0:7071 Application started. Press Ctrl+C to shut down. Http Functions: HttpExample: [GET,POST] http://localhost:7071/api/HttpExample ...

Trigger the function from the command line using the following cURL command in a new terminal window:

```
curl -w "\n" http://localhost:7071/api/HttpExample --data AzureFunctions
```


The expected output is the following:

Hello, AzureFunctions

Note

If you set authLevel to `FUNCTION`

or `ADMIN`

, the [access key](function-keys-how-to) isn't required when running locally.

Use `Ctrl+C`

in the terminal to stop the function code.

## Deploy the function to Azure

A function app and related resources are created in Azure when you first deploy your function app. Before you can deploy, use the [az login](/en-us/cli/azure/authenticate-azure-cli) Azure CLI command to sign in to your Azure subscription.

```
az login
```


Tip

If your account can access multiple subscriptions, use [az account set](/en-us/cli/azure/account#az-account-set) to set the default subscription for this session.

Use the following command to deploy your project to a new function app.

```
gradle azureFunctionsDeploy
```


This creates the following resources in Azure, based on the values in the build.gradle file:

- Resource group. Named with the
*resourceGroup*you supplied. - Storage account. Required by Functions. The name is generated randomly based on Storage account name requirements.
- App Service plan. Serverless Consumption plan hosting for your function app in the specified
*region*. The name is generated randomly. - Function app. A function app is the deployment and execution unit for your functions. The name is your
*appName*, appended with a randomly generated number.

The deployment also packages the project files and deploys them to the new function app using [zip deployment](functions-deployment-technologies#zip-deploy), with run-from-package mode enabled.

The authLevel for HTTP Trigger in sample project is `ANONYMOUS`

, which will skip the authentication. However, if you use other authLevel like `FUNCTION`

or `ADMIN`

, you need to get the function key to call the function endpoint over HTTP. The easiest way to get the function key is from the [Azure portal](https://portal.azure.com).

## Get the HTTP trigger URL

You can get the URL required to trigger your function, with the function key, from the Azure portal.

Browse to the

[Azure portal](https://portal.azure.com), sign in, type the*appName*of your function app into**Search**at the top of the page, and press enter.In your function app, select

**Functions**, choose your function, then click**Get Function Url**at the top right.Choose

**default (Function key)**and select**Copy**.

You can now use the copied URL to access your function.

## Verify the function in Azure

To verify the function app running on Azure using `cURL`

, replace the URL from the sample below with the URL that you copied from the portal.

```
curl -w "\n" http://azure-functions-sample-demo.azurewebsites.net/api/HttpExample --data AzureFunctions
```


This sends a POST request to the function endpoint with `AzureFunctions`

in the body of the request. You see the following response.

Hello, AzureFunctions

## Next steps

You've created a Java functions project with an HTTP triggered function, run it on your local machine, and deployed it to Azure. Now, extend your function by...

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-web-pubsub -->

# Web PubSub bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This set of articles explains how to authenticate, send real-time messages to clients connected to [Azure Web PubSub](https://azure.microsoft.com/products/web-pubsub/) by using Azure Web PubSub bindings in Azure Functions.

| Action | Type |
|---|---|
| Handle client events from Web PubSub |
|

[Input binding](functions-bindings-web-pubsub-input)[Output binding](functions-bindings-web-pubsub-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

Add the extension to your project by installing this [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.WebPubSub/).

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

Note

The Web PubSub extensions for Java is not supported yet.

## Key concepts

(1)-(2) `WebPubSubConnection`

input binding with HttpTrigger to generate client connection.

(3)-(4) `WebPubSubTrigger`

trigger binding or `WebPubSubContext`

input binding with HttpTrigger to handle service request.

(5)-(6) `WebPubSub`

output binding to request service do something.

## Connection

You can use [connection string](#connection-string) or [Microsoft Entra identity](#identity-based-connections) to connect to Azure Web PubSub service.

### Connection String

By default, an application setting named `WebPubSubConnectionString`

is used to store your Web PubSub connection string. When you choose to use a different setting name for your connection, you must explicitly set that as the key name in your binding definitions. During local development, you must also add this setting to the `Values`

collection in the [ local.settings.json file](functions-develop-local#local-settings-file).

Important

A connection string includes the authorization information required for your application to access Azure Web PubSub service. The access key inside the connection string is similar to a root password for your service. For optimal security, your function app should use [managed identities](#identity-based-connections) when connecting to the Web PubSub service instead of using a connection string.

For details on how to configure and use Web PubSub and Azure Functions together, refer to [Tutorial: Create a serverless notification app with Azure Functions and Azure Web PubSub service](../azure-web-pubsub/tutorial-serverless-notification).

### Identity-based connections

If you're using Azure Web PubSub Functions Extensions v1.10.0 or higher, instead of using a connection string with an access key, you can configure your function app to authenticate to Azure Web PubSub using a Microsoft Entra identity.

This approach removes the need to manage secrets and is recommended for production workloads.

#### Prerequisites

Make sure the Microsoft Entra identity used by your function app has been granted an appropriate Azure RBAC role on the target Web PubSub resource:

#### Configuration

Identity-based connections in Azure Functions use a set of settings that share a common prefix. By default, Azure Web PubSub Functions extensions look for settings with the prefix `WebPubSubConnectionString`

. You can customize this prefix by setting the `connection`

property in your trigger or binding.

For Azure Web PubSub, the service-specific setting you must provide is the service endpoint URI:

| Property | Environment variable template | Description | Required |
|---|---|---|---|
| Service URI | `WebPubSubConnectionString__serviceUri` |
The URI of your Web PubSub service endpoint. | Yes |

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified. For more information on how to customize the identity, [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Example configuration

The following example shows how to configure identity-based with default settings:

```
{
"WebPubSubConnectionString__serviceUri": "https://your-webpubsub.webpubsub.azure.com"
}
```


Note

When using `local.settings.json`

file at local, [Azure App Configuration](../azure-app-configuration/quickstart-azure-functions-csharp), or [Key Vault](/en-us/azure/key-vault/general/overview) to provide settings for identity-based connections, replace `__`

with `:`

in the setting name to ensure names are resolved correctly.

For example, `WebPubSubConnectionString:serviceUri`

.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-your-first-function-visual-studio -->

# Quickstart: Create your first C# function in Azure using Visual Studio

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions lets you use Visual Studio to create local C# function projects and then easily publish this project to run in a scalable serverless environment in Azure. If you prefer to develop your C# apps locally using Visual Studio Code, you should instead consider the [Visual Studio Code-based version](how-to-create-function-vs-code?pivot=programming-language-csharp) of this article.

By default, this article shows you how to create C# functions that run on .NET 8 in an [isolated worker process](dotnet-isolated-process-guide). Function apps that run in an isolated worker process are supported on all versions of .NET that are supported by Functions. For more information, see [Supported versions](dotnet-isolated-process-guide#supported-versions).

In this article, you learn how to:

- Use Visual Studio to create a C# class library project.
- Create a function that responds to HTTP requests.
- Run your code locally to verify function behavior.
- Deploy your code project to Azure Functions.

Completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

This video shows you how to create a C# function in Azure.

The steps in the video are also described in the following sections.

## Prerequisites

[Visual Studio 2022](https://visualstudio.microsoft.com/vs/). Make sure to select the**Azure development**workload during installation.[Azure subscription](../guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing). If you don't already have an account,[create a free one](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

## Create a function app project

The Azure Functions project template in Visual Studio creates a C# class library project that you can publish to a function app in Azure. You can use a function app to group functions as a logical unit for easier management, deployment, scaling, and sharing of resources.

From the Visual Studio menu, select

**File**>**New**>**Project**.In

**Create a new project**, enter*functions*in the search box, choose the**Azure Functions**template, and then select**Next**.In

**Configure your new project**, enter a**Project name**for your project, and then select**Next**. The function app name must be valid as a C# namespace, so don't use underscores, hyphens, or any other nonalphanumeric characters.For the remaining

**Additional information**settings,Setting Value Description **Functions worker****.NET 8.0 Isolated (Long Term Support)**Your functions run on .NET 8 in an isolated worker process. **Function****HTTP trigger**This value creates a function triggered by an HTTP request. **Use Azurite for runtime storage account (AzureWebJobsStorage)**Enable Because a function app in Azure requires a storage account, one is assigned or created when you publish your project to Azure. An HTTP trigger doesn't use an Azure Storage account connection string; all other trigger types require a valid Azure Storage account connection string. When you select this option, the [Azurite emulator](../storage/common/storage-use-azurite?tabs=visual-studio)is used.**Authorization level****Anonymous**The created function can be triggered by any client without providing a key. This authorization setting makes it easy to test your new function. For more information, see [Authorization level](functions-bindings-http-webhook-trigger#http-auth).Make sure you set the

**Authorization level**to**Anonymous**. If you choose the default level of**Function**, you're required to present the[function key](function-keys-how-to)in requests to access your function endpoint in Azure.Select

**Create**to create the function project and HTTP trigger function.

Visual Studio creates a project and class that contains boilerplate code for the HTTP trigger function type. The boilerplate code sends an HTTP response that includes a value from the request body or query string. The `HttpTrigger`

attribute specifies that the function is triggered by an HTTP request.

## Rename the function

The `Function`

method attribute sets the name of the function, which by default is generated as `Function1`

. Since the tooling doesn't let you override the default function name when you create your project, take a minute to create a better name for the function class, file, and metadata.

In

**File Explorer**, right-click the Function1.cs file and rename it to`HttpExample.cs`

.In the code, rename the Function1 class to

`HttpExample`

.In the method named

`Run`

, rename the`Function`

method attribute to`HttpExample`

.

Your function definition should now look like the following code:

```
[Function("HttpExample")]
public IActionResult Run([HttpTrigger(AuthorizationLevel.Anonymous, "get", "post")] HttpRequest req)
{
_logger. LogInformation("C# HTTP trigger function processed a request.");
return new OkObjectResult("Hello, functions");
}
```


Now that you've renamed the function, you can test it on your local computer.

## Run the function locally

Visual Studio integrates with Azure Functions Core Tools so that you can test your functions locally using the full Azure Functions runtime.

To run your function, press

`F5`in Visual Studio. You might need to enable a firewall exception so that the tools can handle HTTP requests. Authorization levels are never enforced when you run a function locally.Copy the URL of your function from the Azure Functions runtime output.

Paste the URL for the HTTP request into your browser's address bar and run the request. The following image shows the response in the browser to the local GET request returned by the function:

To stop debugging, press

`Shift`+`F5`in Visual Studio.

After you've verified that the function runs correctly on your local computer, it's time to publish the project to Azure.

## Publish the project to Azure

Visual Studio can publish your local project to Azure. Before you can publish your project, you must have a function app in your Azure subscription. If you don't already have a function app in Azure, Visual Studio can help you create one before you publish your project. In this article, you create a function app that runs on Linux in a Flex Consumption plan, which is the recommended plan for event-driven and secure serverless functions.

In

**Solution Explorer**, right-click the project and then select**Publish**.On the

**Publish**page, make the following selections:- On
**Target**, select**Azure**, and then select**Next**. - On
**Specific target**, select**Azure Function App**, and then select**Next**. - On
**Functions instance**, select**Create new**.

- On
Create a new instance by using the values specified in the following table:

Setting Value Description **Name**A globally unique name The name must uniquely identify your new function app. Accept the suggested name or enter a new name. The following characters are valid: `a-z`

,`0-9`

, and`-`

.**Subscription name**The name of your subscription The function app is created in an Azure subscription. Accept the default subscription or select a different one from the list. [Resource group](../azure-resource-manager/management/overview)The name of your resource group The function app is created in a resource group. Select **New**to create a new resource group. You can also select an existing resource group from the list.[Plan Type](functions-scale)**Flex Consumption**When you publish your project to a function app that runs in a [Flex Consumption plan](flex-consumption-plan), you might pay only for executions of your functions app. Other hosting plans can incur higher costs.**IMPORTANT:**

When creating a Flex Consumption plan, you must first select**App service plan**and then reselect**Flex Consumption**to clear an issue with the dialog.**Operating system****Linux**The Flex Consumption plan currently requires Linux. **Location**The location of the app service Select a location in an [Azure region supported by the Flex Consumption plan](flex-consumption-how-to#view-currently-supported-regions). When an unsupported region is selected, the**Create**button is grayed-out.**Instance memory size****2048**The [memory size of the virtual machine instances](flex-consumption-plan#instance-sizes)in which the app runs is unique to the Flex Consumption plan.[Azure Storage](storage-considerations)A general-purpose storage account The Functions runtime requires a Storage account. Select **New**to configure a general-purpose storage account. You can also use an existing account that meets the[storage account requirements](storage-considerations#storage-account-requirements).[Application Insights](functions-monitoring)An Application Insights instance You should turn on Application Insights integration for your function app. Select **New**to create a new instance, either in a new or in an existing Log Analytics workspace. You can also use an existing instance.Select

**Create**to create a function app and its related resources in Azure. The status of resource creation is shown in the lower-left corner of the window.Select

**Finish**. The**Publish profile creation progress**window appears. When the profile is created, select**Close**.On the publish profile page, select

**Publish**to deploy the package that contains your project files to your new function app in Azure.When deployment is complete, the root URL of the function app in Azure is shown on the publish profile page.

On the publish profile page, go to the

**Hosting**section. Select the ellipsis (**...**), and then select**Open in Azure portal**. The new function app Azure resource opens in the Azure portal.

## Verify your function in Azure

In the Azure portal, you should be in the

**Overview**page for your new functions app.Under

**Functions**, select your new function named**HttpExample**, then in the function page select**Get function URL**and then the**Copy to clipboard icon**.In the address bar in your browser, paste the URL you copied and run the request.

The URL that calls your HTTP trigger function is in the following format:

`https://<APP_NAME>.azurewebsites.net/api/HttpExample?name=Functions`

Go to this URL and you see a response in the browser to the remote GET request returned by the function, which looks like the following example:


## Clean up resources

*Resources* in Azure refer to function apps, functions, storage accounts, and so forth. They're grouped into *resource groups*, and you can delete everything in a group by deleting the group.

You created Azure resources to complete this quickstart. You could be billed for these resources, depending on your [account status](https://azure.microsoft.com/account/) and [service pricing](https://azure.microsoft.com/pricing/). Other quickstarts in this collection build upon this quickstart. If you plan to work with subsequent quickstarts, tutorials, or with any of the services you've created in this quickstart, don't clean up the resources.

Use the following steps to delete the function app and its related resources to avoid incurring any further costs.

In the Visual Studio Publish dialogue, in the Hosting section, select

**Open in Azure portal**.In the function app page, select the

**Overview**tab and then select the link under**Resource group**.In the

**Resource group**page, review the list of included resources, and verify that they're the ones you want to delete.Select

**Delete resource group**, and follow the instructions.Deletion may take a couple of minutes. When it's done, a notification appears for a few seconds. You can also select the bell icon at the top of the page to view the notification.


## Next steps

In this quickstart, you used Visual Studio to create and publish a C# function app in Azure with a simple HTTP trigger function.

To learn more about working with C# functions that run in an isolated worker process, see the [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide). Check out [.NET supported versions](functions-dotnet-class-library#supported-versions) to see other versions of supported .NET versions in an isolated worker process.

Advance to the next article to learn how to add an Azure Storage queue binding to your function:
