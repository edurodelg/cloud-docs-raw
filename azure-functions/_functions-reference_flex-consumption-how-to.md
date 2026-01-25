---
merged_at: 2026-01-25T15:41:11.631498
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-reference.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-reference -->

# Azure Functions developer guide

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure Functions, all functions share some core technical concepts and components, regardless of your preferred language or development environment. This article is language-specific. Choose your preferred language at the top of the article.

This article assumes that you've already read the [Azure Functions overview](functions-overview).

If you prefer to jump right in, you can complete a quickstart tutorial using [Visual Studio](functions-create-your-first-function-visual-studio), [Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-csharp), or from the [command prompt](how-to-create-function-azure-cli?pivots=programming-language-csharp).

If you prefer to jump right in, you can complete a quickstart tutorial using [Maven](how-to-create-function-azure-cli?pivots=programming-language-java) (command line), [Eclipse](functions-create-maven-eclipse), [IntelliJ IDEA](functions-create-maven-intellij), [Gradle](functions-create-first-java-gradle), [Quarkus](functions-create-first-quarkus), [Spring Cloud](/en-us/azure/developer/java/spring-framework/getting-started-with-spring-cloud-function-in-azure?toc=/azure/azure-functions/toc.json), or [Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-java).

If you prefer to jump right in, you can complete a quickstart tutorial using [Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-javascript) or from the [command prompt](how-to-create-function-azure-cli?pivots=programming-language-javascript).

If you prefer to jump right in, you can complete a quickstart tutorial using [Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-typescript) or from the [command prompt](how-to-create-function-azure-cli?pivots=programming-language-typescript).

If you prefer to jump right in, you can complete a quickstart tutorial using [Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-powershell) or from the [command prompt](how-to-create-function-azure-cli?pivots=programming-language-powershell).

If you prefer to jump right in, you can complete a quickstart tutorial using [Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-python) or from the [command prompt](how-to-create-function-azure-cli?pivots=programming-language-python).

## Code project

At the core of Azure Functions is a language-specific code project that implements one or more units of code execution called *functions*. Functions are simply methods that run in the Azure cloud based on events, in response to HTTP requests, or on a schedule. Think of your Azure Functions code project as a mechanism for organizing, deploying, and collectively managing your individual functions in the project when they're running in Azure. For more information, see [Organize your functions](functions-best-practices#organize-your-functions).

The way that you lay out your code project and how you indicate which methods in your project are functions depends on the development language of your project. For detailed language-specific guidance, see the [C# developers guide](dotnet-isolated-process-guide).

The way that you lay out your code project and how you indicate which methods in your project are functions depends on the development language of your project. For language-specific guidance, see the [Java developers guide](functions-reference-java).

The way that you lay out your code project and how you indicate which methods in your project are functions depends on the development language of your project. For language-specific guidance, see the [Node.js developers guide](functions-reference-node).

The way that you lay out your code project and how you indicate which methods in your project are functions depends on the development language of your project. For language-specific guidance, see the [PowerShell developers guide](functions-reference-powershell).

The way that you lay out your code project and how you indicate which methods in your project are functions depends on the development language of your project. For language-specific guidance, see the [Python developers guide](functions-reference-python).

All functions must have a trigger, which defines how the function starts and can provide input to the function. Your functions can optionally define input and output bindings. These bindings simplify connections to other services without you having to work with client SDKs. For more information, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings).

Azure Functions provides a set of language-specific project and function templates that make it easy to create new code projects and add functions to your project. You can use any of the tools that support Azure Functions development to generate new apps and functions using these templates.

## Development tools

The following tools provide an integrated development and publishing experience for Azure Functions in your preferred language:

[Azure Functions Core Tools](functions-develop-local)(command prompt)

These tools integrate with [Azure Functions Core Tools](functions-develop-local) so that you can run and debug on your local computer using the Functions runtime. For more information, see [Code and test Azure Functions locally](functions-develop-local).

[ There's also an editor in the Azure portal that lets you update your code and your ]*function.json* definition file directly in the portal. You should only use this editor for small changes or creating proof-of-concept functions. You should always develop your functions locally, when possible. For more information, see [Create your first function in the Azure portal](functions-create-function-app-portal).

Portal editing is only supported for [Node.js version 3](functions-reference-node?pivots=nodejs-model-v3), which uses the function.json file.

## Deployment

When you publish your code project to Azure, you're essentially deploying your project to an existing function app resource. A function app provides an execution context in Azure in which your functions run. As such, it's the unit of deployment and management for your functions. From an Azure Resource perspective, a function app is equivalent to a site resource (`Microsoft.Web/sites`

) in Azure App Service, which is equivalent to a web app.

A function app is composed of one or more individual functions that are managed, deployed, and scaled together. All of the functions in a function app share the same [pricing plan](functions-scale), [deployment method](functions-deployment-technologies), and [runtime version](functions-versions). For more information, see [How to manage a function app](functions-how-to-use-azure-function-app-settings).

When the function app and any other required resources don't already exist in Azure, you first need to create these resources before you can deploy your project files. You can create these resources in one of these ways:

- During
[Visual Studio](functions-develop-vs#publish-to-azure)publishing

Using

[Visual Studio Code](functions-develop-vs-code#publish-to-azure)Programmatically using

[Azure CLI](scripts/functions-cli-create-serverless),[Azure PowerShell](create-resources-azure-powershell#create-a-serverless-function-app-for-c),[ARM templates](functions-create-first-function-resource-manager), or[Bicep files](functions-create-first-function-bicep)In the

[Azure portal](functions-create-function-app-portal)

In addition to tool-based publishing, Functions supports other technologies for deploying source code to an existing function app. For more information, see [Deployment technologies in Azure Functions](functions-deployment-technologies).

## Connect to services

A major requirement of any cloud-based compute service is reading data from and writing data to other cloud services. Functions provides an extensive set of bindings that makes it easier for you to connect to services without having to work with client SDKs.

Whether you use the binding extensions provided by Functions or you work with client SDKs directly, you securely store connection data and do not include it in your code. For more information, see [Connections](#connections).

### Bindings

Functions provides bindings for many Azure services and a few third-party services, which are implemented as extensions. For more information, see the [complete list of supported bindings](functions-triggers-bindings#supported-bindings).

Binding extensions can support both inputs and outputs, and many triggers also act as input bindings. Bindings let you configure the connection to services so that the Functions host can handle the data access for you. For more information, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings).

If you're having issues with errors coming from bindings, see the [Azure Functions Binding Error Codes](functions-bindings-error-pages) documentation.

### Client SDKs

While Functions provides bindings to simplify data access in your function code, you're still able to use a client SDK in your project to directly access a given service, if you prefer. You might need to use client SDKs directly should your functions require a functionality of the underlying SDK that's not supported by the binding extension.

When using client SDKs, you should use the same process for [storing and accessing connection strings](#connections) used by binding extensions.

When you create a client SDK instance in your functions, you should get the connection info required by the client from [Environment variables](functions-dotnet-class-library#environment-variables).

When you create a client SDK instance in your functions, you should get the connection info required by the client from [Environment variables](functions-reference-java#environment-variables).

When you create a client SDK instance in your functions, you should get the connection info required by the client from [Environment variables](functions-reference-node#environment-variables).

When you create a client SDK instance in your functions, you should get the connection info required by the client from [Environment variables](functions-reference-powershell#environment-variables).

When you create a client SDK instance in your functions, you should get the connection info required by the client from [Environment variables](functions-reference-python#environment-variables).

## Connections

As a security best practice, Azure Functions takes advantage of the application settings functionality of Azure App Service to help you more securely store strings, keys, and other tokens required to connect to other services. Application settings in Azure are stored encrypted and can be accessed at runtime by your app as environment variable `name`

`value`

pairs. For triggers and bindings that require a connection property, you set the application setting name instead of the actual connection string. You can't configure a binding directly with a connection string or key.

For example, consider a trigger definition that has a `connection`

property. Instead of the connection string, you set `connection`

to the name of an environment variable that contains the connection string. Using this secrets access strategy both makes your apps more secure and makes it easier for you to change connections across environments. For even more security, you can use identity-based connections.

The default configuration provider uses environment variables. These variables are defined in [application settings](functions-how-to-use-azure-function-app-settings?tabs=portal#settings) when running in the Azure and in the [local settings file](functions-develop-local#local-settings-file) when developing locally.

### Connection values

When the connection name resolves to a single exact value, the runtime identifies the value as a *connection string*, which typically includes a secret. The details of a connection string depend on the service to which you connect.

However, a connection name can also refer to a collection of multiple configuration items, useful for configuring [identity-based connections](#configure-an-identity-based-connection). Environment variables can be treated as a collection by using a shared prefix that ends in double underscores `__`

. The group can then be referenced by setting the connection name to this prefix.

For example, the `connection`

property for an Azure Blob trigger definition might be `Storage1`

. As long as there's no single string value configured by an environment variable named `Storage1`

, an environment variable named `Storage1__blobServiceUri`

could be used to inform the `blobServiceUri`

property of the connection. The connection properties are different for each service. Refer to the documentation for the component that uses the connection.

Note

When using [Azure App Configuration](../azure-app-configuration/quickstart-azure-functions-csharp) or [Key Vault](/en-us/azure/key-vault/general/overview) to provide settings for Managed Identity connections, setting names should use a valid key separator such as `:`

or `/`

in place of the `__`

to ensure names are resolved correctly.

For example, `Storage1:blobServiceUri`

.

### Configure an identity-based connection

Some connections in Azure Functions can be configured to use an identity instead of a secret. Support depends on the runtime version and the extension using the connection. In some cases, a connection string may still be required in Functions even though the service to which you're connecting supports identity-based connections. For a tutorial on configuring your function apps with managed identities, see the [creating a function app with identity-based connections tutorial](functions-identity-based-connections-tutorial).

Note

When running in a Consumption or Elastic Premium plan, your app uses the [ WEBSITE_AZUREFILESCONNECTIONSTRING](functions-app-settings#website_contentazurefileconnectionstring) and

[settings when connecting to Azure Files on the storage account used by your function app. Azure Files doesn't support using managed identity when accessing the file share. For more information, see](functions-app-settings#website_contentshare)

`WEBSITE_CONTENTSHARE`

[Azure Files supported authentication scenarios](../storage/files/storage-files-active-directory-overview#supported-authentication-scenarios)

Identity-based connections are only supported on Functions 4.x, If you are using version 1.x, you must first [migrate to version 4.x](migrate-version-1-version-4).

The following components support identity-based connections:

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

Choose one of these tabs to learn about permissions for each component:

-
[Azure Blobs extension](#tabpanel_1_blob) -
[Azure Queues extension](#tabpanel_1_queue) -
[Azure Tables extension](#tabpanel_1_table) -
[Event Hubs extension](#tabpanel_1_eventhubs) -
[Service Bus extension](#tabpanel_1_servicebus) -
[Event Grid extension](#tabpanel_1_eventgrid) -
[Azure Cosmos DB extension](#tabpanel_1_cosmos) -
[Azure SignalR extension](#tabpanel_1_signalr) -
[Azure Web PubSub extension](#tabpanel_1_web-pubsub) -
[Durable Functions storage provider](#tabpanel_1_durable) -
[Functions host storage](#tabpanel_1_azurewebjobsstorage)

You need to create a role assignment that provides access to your blob container at runtime. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) aren't sufficient. The following table shows built-in roles that are recommended when using the Blob Storage extension in normal operation. Your application may require further permissions based on the code you write.

| Binding type | Example built-in roles |
|---|---|
| Trigger |
and
1Extra permissions must also be granted to the AzureWebJobsStorage connection. 2 |

[Storage Blob Data Reader](../role-based-access-control/built-in-roles#storage-blob-data-reader)[Storage Blob Data Owner](../role-based-access-control/built-in-roles#storage-blob-data-owner)1 The blob trigger handles failure across multiple retries by writing [poison blobs](functions-bindings-storage-blob-trigger#poison-blobs) to a queue on the storage account specified by the connection.

2 The AzureWebJobsStorage connection is used internally for blobs and queues that enable the trigger. If it's configured to use an identity-based connection, it needs extra permissions beyond the default requirement. The required permissions are covered by the [Storage Blob Data Owner](../role-based-access-control/built-in-roles#storage-blob-data-owner), [Storage Queue Data Contributor](../role-based-access-control/built-in-roles#storage-queue-data-contributor), and [Storage Account Contributor](../role-based-access-control/built-in-roles#storage-account-contributor) roles. To learn more, see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity).

#### Common properties for identity-based connections

An identity-based connection for an Azure service accepts the following common properties, where `<CONNECTION_NAME_PREFIX>`

is the value of your `connection`

property in the trigger or binding definition:

| Property | Environment variable template | Description |
|---|---|---|
| Token Credential | `<CONNECTION_NAME_PREFIX>__credential` |
This property determines how a token should be obtained for the connection. The property shouldn't be set in
`managedidentity` . When you intend to
`managedidentityasfederatedidentity` . |

`<CONNECTION_NAME_PREFIX>__clientId`

`credential`

is set to `managedidentity`

, this property can be set to specify the user-assigned identity to be used when obtaining a token. The property accepts a client ID corresponding to a user-assigned identity assigned to the application. It's invalid to specify both a resource ID and a client ID. If neither are specified, the system-assigned identity is used.This property is used differently in cross-tenant scenarios. See the

[cross-tenant scenarios](#connecting-to-a-resource-in-another-tenant)section.This property is used differently in

[local development scenarios](#local-development-with-identity-based-connections), when`credential`

shouldn't be set.`<CONNECTION_NAME_PREFIX>__managedIdentityResourceId`

`credential`

is set to `managedidentity`

, this property can be set to specify the user-assigned identity to be used when obtaining a token. The property accepts a resource identifier corresponding to a user-assigned identity assigned to the application. It's invalid to specify both a resource ID and a client ID. If neither are specified, the system-assigned identity is used.Other options may be supported for a given connection type. Refer to the documentation for the component making the connection.

##### Azure SDK Environment Variables

Caution

Use of the Azure SDK's [ EnvironmentCredential](/en-us/dotnet/api/azure.identity.environmentcredential) environment variables is not recommended due to the potentially unintentional impact on other connections. They also are not fully supported when deployed to Azure Functions.

The environment variables associated with the Azure SDK's [ EnvironmentCredential](/en-us/dotnet/api/azure.identity.environmentcredential) can also be set, but these are not processed by the Functions service for scaling in Consumption plans. These environment variables are not specific to any one connection and will apply as a default unless a corresponding property is not set for a given connection. For example, if

`AZURE_CLIENT_ID`

is set, this would be used as if `<CONNECTION_NAME_PREFIX>__clientId`

had been configured. Explicitly setting `<CONNECTION_NAME_PREFIX>__clientId`

would override this default.##### Local development with identity-based connections

Note

Local development with identity-based connections requires version `4.0.3904`

of [Azure Functions Core Tools](functions-run-local), or a later version.

When you're running your function project locally, the above configuration tells the runtime to use your local developer identity. The connection attempts to get a token from the following locations, in order:

- A local cache shared between Microsoft applications
- The current user context in Visual Studio
- The current user context in Visual Studio Code
- The current user context in the Azure CLI

If none of these options are successful, an error occurs.

Your identity may already have some role assignments against Azure resources used for development, but those roles may not provide the necessary data access. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) aren't sufficient. Double-check what permissions are required for connections for each component, and make sure that you have them assigned to yourself.

In some cases, you may wish to specify use of a different identity. You can add configuration properties for the connection that point to the alternate identity based on a client ID and client Secret for a Microsoft Entra service principal. **This configuration option is not supported when hosted in the Azure Functions service.** To use an ID and secret on your local machine, define the connection with the following extra properties:

| Property | Environment variable template | Description |
|---|---|---|
| Tenant ID | `<CONNECTION_NAME_PREFIX>__tenantId` |
The Microsoft Entra tenant (directory) ID. |
| Client ID | `<CONNECTION_NAME_PREFIX>__clientId` |
The client (application) ID of an app registration in the tenant. |
| Client secret | `<CONNECTION_NAME_PREFIX>__clientSecret` |
A client secret that was generated for the app registration. |

Here's an example of `local.settings.json`

properties required for identity-based connection to Azure Blobs:

```
{
"IsEncrypted": false,
"Values": {
"<CONNECTION_NAME_PREFIX>__blobServiceUri": "<blobServiceUri>",
"<CONNECTION_NAME_PREFIX>__queueServiceUri": "<queueServiceUri>",
"<CONNECTION_NAME_PREFIX>__tenantId": "<tenantId>",
"<CONNECTION_NAME_PREFIX>__clientId": "<clientId>",
"<CONNECTION_NAME_PREFIX>__clientSecret": "<clientSecret>"
}
}
```


#### Connecting to host storage with an identity

The Azure Functions host uses the storage connection set in [ AzureWebJobsStorage](functions-app-settings#azurewebjobsstorage) to enable core behaviors such as coordinating singleton execution of timer triggers and default app key storage. This connection can also be configured to use an identity.

Caution

Other components in Functions rely on `AzureWebJobsStorage`

for default behaviors. You should not move it to an identity-based connection if you are using older versions of extensions that do not support this type of connection, including triggers and bindings for Azure Blobs, Event Hubs, and Durable Functions. Similarly, `AzureWebJobsStorage`

is used for deployment artifacts when using server-side build in Linux Consumption, and if you enable this, you will need to deploy via [an external deployment package](run-functions-from-deployment-package).

In addition, your function app might be reusing `AzureWebJobsStorage`

for other storage connections in their triggers, bindings, and/or function code. Make sure that all uses of `AzureWebJobsStorage`

are able to use the identity-based connection format before changing this connection from a connection string.

To use an identity-based connection for `AzureWebJobsStorage`

, configure the following app settings:

| Setting | Description | Example value |
|---|---|---|
`AzureWebJobsStorage__blobServiceUri` |
The data plane URI of the blob service of the storage account, using the HTTPS scheme. | https://<storage_account_name>.blob.core.windows.net |
`AzureWebJobsStorage__queueServiceUri` |
The data plane URI of the queue service of the storage account, using the HTTPS scheme. | https://<storage_account_name>.queue.core.windows.net |
`AzureWebJobsStorage__tableServiceUri` |
The data plane URI of a table service of the storage account, using the HTTPS scheme. | https://<storage_account_name>.table.core.windows.net |

[Common properties for identity-based connections](#common-properties-for-identity-based-connections) may also be set as well.

If you're configuring `AzureWebJobsStorage`

using a storage account that uses the default DNS suffix and service name for global Azure, following the `https://<accountName>.[blob|queue|file|table].core.windows.net`

format, you can instead set `AzureWebJobsStorage__accountName`

to the name of your storage account. The endpoints for each storage service are inferred for this account. This doesn't work when the storage account is in a sovereign cloud or has a custom DNS.

| Setting | Description | Example value |
|---|---|---|
`AzureWebJobsStorage__accountName` |
The account name of a storage account, valid only if the account isn't in a sovereign cloud and doesn't have a custom DNS. This syntax is unique to `AzureWebJobsStorage` and can't be used for other identity-based connections. |
<storage_account_name> |

You need to create a role assignment that provides access to the storage account for "AzureWebJobsStorage" at runtime. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) aren't sufficient. The [Storage Blob Data Owner](../role-based-access-control/built-in-roles#storage-blob-data-owner) role covers the basic needs of Functions host storage - the runtime needs both read and write access to blobs and the ability to create containers. Several extensions use this connection as a default location for blobs, queues, and tables, and these uses may add requirements as noted in the table below. You may also need other permissions if you use "AzureWebJobsStorage" for any other purposes.

| Extension | Roles required | Explanation |
|---|---|---|
No extension (host only) |
|

This scenario represents the minimum set of permissions for normal operation, but it doesn't include support for diagnostic events

1.*No extension (host only), with support for diagnostic events*1[Storage Blob Data Owner](../role-based-access-control/built-in-roles#storage-blob-data-owner),[Storage Table Data Contributor](../role-based-access-control/built-in-roles#storage-table-data-contributor)[Storage Account Contributor](../role-based-access-control/built-in-roles#storage-account-contributor),[Storage Blob Data Owner](../role-based-access-control/built-in-roles#storage-blob-data-owner),[Storage Queue Data Contributor](../role-based-access-control/built-in-roles#storage-queue-data-contributor)[blob receipts](functions-bindings-storage-blob-trigger#blob-receipts). It uses the AzureWebJobsStorage connection for these purposes, regardless of the connection configured for the trigger.[Storage Blob Data Owner](../role-based-access-control/built-in-roles#storage-blob-data-owner)[Storage Blob Data Owner](../role-based-access-control/built-in-roles#storage-blob-data-owner)[Storage Blob Data Contributor](../role-based-access-control/built-in-roles#storage-blob-data-contributor),[Storage Queue Data Contributor](../role-based-access-control/built-in-roles#storage-queue-data-contributor),[Storage Table Data Contributor](../role-based-access-control/built-in-roles#storage-table-data-contributor)[Durable Functions extension configuration](durable/durable-functions-bindings#host-json).1 For some types of issues, Azure Functions can raise a diagnostic event that can assist with troubleshooting, even when the issue prevents the function app from starting. If [Storage Table Data Contributor](../role-based-access-control/built-in-roles#storage-table-data-contributor) isn't assigned, you might see warnings in your logs about the inability to write these events.

#### Connecting to a resource in another tenant

If your function needs to connect to a resource in a different Microsoft Entra tenant, your connection needs to use a *federated identity credential*. This requires a user-assigned managed identity and a multi-tenant Entra ID app registration. You cannot use a system-assigned managed identity for cross-tenant connections.

Important

When you configure a trigger for a cross-tenant connection in the Consumption or Flex Consumption plan types, the platform no longer scales the function app based on that trigger.

To configure a cross-tenant identity-based connection, you first need to set up your infrastructure using the following steps:

- In the tenant where your function app is deployed,
[create a new user-assigned managed identity](/en-us/entra/identity/managed-identities-azure-resources/how-manage-user-assigned-managed-identities#create-a-user-assigned-managed-identity). [Assign that identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json#add-a-user-assigned-identity)to the function app.- In the same tenant,
[create a multi-tenant Entra app registration](/en-us/entra/workload-id/workload-identity-federation-config-app-trust-managed-identity#configure-a-multi-tenant-app-registration)that represents the cross-tenant resource you want to access. [Add the managed identity as a federated identity credential for the app registration.](/en-us/entra/workload-id/workload-identity-federation-config-app-trust-managed-identity)- In the tenant where the resource is deployed,
[create an enterprise application for the app registration](/en-us/entra/identity/enterprise-apps/create-service-principal-cross-tenant). - Assign permissions for the enterprise application to access the resource.

A cross-tenant identity-based connection uses the following properties, where `<CONNECTION_NAME_PREFIX>`

is the value of your `connection`

property in the trigger or binding definition:

| Property | Environment variable template | Description |
|---|---|---|
| Token Credential | `<CONNECTION_NAME_PREFIX>__credential` |
Required. When connecting to a resource in another tenant, set this property to `managedidentityasfederatedidentity` . |
| Azure Cloud | `<CONNECTION_NAME_PREFIX>__azureCloud` |
Required. This property determines the Azure cloud environment. Allowed values are "public" for Azure Public Cloud, "usgov" for Azure US Government Cloud, and "china" for Azure operated by 21Vianet. |
| Client ID | `<CONNECTION_NAME_PREFIX>__clientId` |
Required. When `credential` is set to `managedidentityasfederatedidentity` , set this property to the client ID (app ID) of the app registration.This property is used differently in single-tenant identity-based connections. See the
This property is used differently in
`credential` shouldn't be set. |
| Tenant ID | `<CONNECTION_NAME_PREFIX>__tenantId` |
Required. When `credential` is set to `managedidentityasfederatedidentity` , set this property to the tenant ID of the resource tenant.This property is used differently in
`credential` shouldn't be set. |
| Managed Identity Client ID | `<CONNECTION_NAME_PREFIX>__managedIdentityClientId` |
When `credential` is set to `managedidentityasfederatedidentity` , this property specifies the user-assigned identity that you configured as a federated identity credential and assigned to the application.1 The property accepts a client ID corresponding to that user-assigned identity. |
| Managed Identity Object ID | `<CONNECTION_NAME_PREFIX>__managedIdentityObjectId` |
When `credential` is set to `managedidentityasfederatedidentity` , this property specifies the user-assigned identity that you configured as a federated identity credential and assigned to the application.1 The property accepts an object ID (principal ID) corresponding to that user-assigned identity. |
| Managed Identity Resource ID | `<CONNECTION_NAME_PREFIX>__managedIdentityResourceId` |
When `credential` is set to `managedidentityasfederatedidentity` , this property specifies the user-assigned identity that you configured as a federated identity credential and assigned to the application.1 The property accepts a resource identifier corresponding to that user-assigned identity. |

1 When `credential`

is set to `managedidentityasfederatedidentity`

, your connection must specify exactly one of `managedIdentityClientId`

, `managedIdentityObjectId`

, or `managedIdentityResourceId`

.

This is also [documented by the Azure SDK](/en-us/dotnet/azure/sdk/authentication/create-token-credentials-from-configuration?tabs=client-id#managed-identity-as-a-federated-identity-credential) in a JSON format.

## Reporting Issues

| Item | Description | Link |
|---|---|---|
| Runtime | Script Host, Triggers & Bindings, Language Support |
|

[File an Issue](https://github.com/Azure/azure-webjobs-sdk-templates/issues)## Open source repositories

The code for Azure Functions is open source, and you can find key components in these GitHub repositories:

## Next steps

For more information, see the following resources:


---

<!-- DOCUMENTO FUSIONADO: flex-consumption-how-to.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/flex-consumption-how-to -->

# Create and manage function apps in the Flex Consumption plan

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to create function apps hosted in the [Flex Consumption plan](flex-consumption-plan) in Azure Functions. It also shows you how to manage certain features of a Flex Consumption plan hosted app.

Function app resources are langauge-specific. Make sure to choose your preferred code development language at the beginning of the article.

## Prerequisites

An Azure account with an active subscription. If you don't already have one, you can

[create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).: used to create and manage resources in Azure. When using the Azure CLI on your local computer, make sure to use version 2.60.0, or a later version. You can also use[Azure CLI](/en-us/cli/azure/install-azure-cli)[Azure Cloud Shell](../cloud-shell/overview), which has the correct Azure CLI version.: used to create and develop apps, create Azure resources, and deploy code projects to Azure. When using Visual Studio Code, make sure to also install the latest[Visual Studio Code](functions-develop-vs-code)[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions). You can also install the[Azure Tools extension pack](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack).While not required to create a Flex Consumption plan app, you need a code project to be able to deploy to and validate a new function app. Complete the first part of one of these quickstart articles, where you create a code project with an HTTP triggered function:

[Create an Azure Functions project from the command line](how-to-create-function-azure-cli)[Create an Azure Functions project using Visual Studio Code](how-to-create-function-vs-code)

To create an app in a new Flex Consumption plan during a Maven deployment, you must create your local app project and then update the project's pom.xml file. For more information, see

[Create a Java Flex Consumption app using Maven](#create-and-deploy-your-app-using-maven)Return to this article after you create and run the local project, but before you're asked to create Azure resources. You create the function app and other Azure resources in the next section.


## Create a Flex Consumption app

This section shows you how to create a function app in the Flex Consumption plan by using either the Azure CLI, Azure portal, or Visual Studio Code. For an example of creating an app in a Flex Consumption plan using Bicep/ARM templates, see the [Flex Consumption repository](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/README.md#iac-samples-overview).

You can skip this section if you choose to instead [create and deploy your app using Maven](#create-and-deploy-your-app-using-maven).

To support your function code, you need to create three resources:

- A
[resource group](../azure-resource-manager/management/overview), which is a logical container for related resources. - A
[Storage account](../storage/common/storage-account-create), which is used to maintain state and other information about your functions. - A function app in the Flex Consumption plan, which provides the environment for executing your function code. A function app maps to your local function project and lets you group functions as a logical unit for easier management, deployment, and sharing of resources in the Flex Consumption plan.

If you haven't done so already, sign in to Azure:

`az login`

The

command signs you into your Azure account.`az login`

Use the

`az functionapp list-flexconsumption-locations`

command to review the list of regions that currently support Flex Consumption in alphabetical order.`az functionapp list-flexconsumption-locations --query "sort_by(@, &name)[].{Region:name}" -o table`


Create a resource group in one of the currently supported regions listed by the command in the previous step.

`az group create --name <RESOURCE_GROUP> --location <REGION>`

In the previous command, replace

`<RESOURCE_GROUP>`

with a value that's unique in your subscription and`<REGION>`

with one of the currently supported regions. The[az group create](/en-us/cli/azure/group#az-group-create)command creates a resource group.Create a general-purpose storage account in your resource group and region:

`az storage account create --name <STORAGE_NAME> --location <REGION> --resource-group <RESOURCE_GROUP> --sku Standard_LRS --allow-blob-public-access false`

In the previous example, replace

`<STORAGE_NAME>`

with a name that's appropriate to you and unique in Azure Storage. Names must contain three to 24 characters consisting of numbers and lowercase letters only.`Standard_LRS`

specifies a general-purpose account that Azure Functions supports according to[storage account requirements](storage-considerations#storage-account-requirements). The[az storage account create](/en-us/cli/azure/storage/account#az-storage-account-create)command creates the storage account.Important

The storage account is used to store important app data, sometimes including the application code itself. You should limit access from other apps and users to the storage account.

Create the function app in Azure:

`az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage-account <STORAGE_NAME> --flexconsumption-location <REGION> --runtime dotnet-isolated --runtime-version 8.0`

[C# apps that run in-process](functions-dotnet-class-library)aren't currently supported when running in a Flex Consumption plan.`az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage-account <STORAGE_NAME> --flexconsumption-location <REGION> --runtime java --runtime-version 17`

For Java apps, Java 11 is also currently supported.

`az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage-account <STORAGE_NAME> --flexconsumption-location <REGION> --runtime node --runtime-version 20`

`az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage-account <STORAGE_NAME> --flexconsumption-location <REGION> --runtime python --runtime-version 3.11`

For Python apps, Python 3.10 is also currently supported.

`az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage-account <STORAGE_NAME> --flexconsumption-location <REGION> --runtime powershell --runtime-version 7.4`

In this example, replace both

`<RESOURCE_GROUP>`

and`<STORAGE_NAME>`

with the resource group and the name of the account you used in the previous step, respectively. Also replace`<APP_NAME>`

with a globally unique name appropriate to you. The`<APP_NAME>`

is also the default domain name server (DNS) domain for the function app. Thecommand creates the function app in Azure.`az functionapp create`

This command creates a function app running in the Flex Consumption plan.

Because you created the app without specifying

[always ready instances](#set-always-ready-instance-counts), your app only incurs costs when actively executing functions. The command also creates an associated Azure Application Insights instance in the same resource group, with which you can monitor your function app and view logs. For more information, see[Monitor Azure Functions](functions-monitoring).

## Deploy your code project

For deployment, Flex Consumption plan apps use a Blob storage container to host .zip package files that contain your project code and all libraries that are required for your app to run. For more information, see [Deployment](flex-consumption-plan#deployment).

You can skip this section if you choose to instead [create and deploy your app using Maven](#create-and-deploy-your-app-using-maven).

You can choose to deploy your project code to an existing function app using various tools:

You can use the Azure CLI to upload a deployment package file to the deployment share for a function app in Azure. To make this deployment, you must produce a .zip package file that can run when the package is mounted to your app.

This package file must contain all of the build output files and referenced libraries required for your project to run.

For projects with a large number of libraries, you should package the root of your project file and request a [remote build](functions-deployment-technologies#remote-build).

For Python projects, you should package the root of your project file and always request a [remote build](functions-deployment-technologies#remote-build). Using a remote build prevents potential issues that can occur when you build a project on Windows to be deployed on Linux.

Using your preferred development tool, build the code project.

Create a .zip file that contains the output of the build directory. For more information, see

[Project structure](dotnet-isolated-process-guide#project-structure).When required, sign in to your Azure account and select the active subscription using the

command.`az login`

`az login`

Run the

command to deploy the application package located in the relative`az functionapp deployment source config-zip`

`<FILE_PATH>`

.`az functionapp deployment source config-zip --src <FILE_PATH> --name <APP_NAME> --resource-group <RESOURCE_GROUP>`


Using your preferred development tool, build the code project.

Create a .zip file that contains the output of the build directory. For more information, see

[Folder structure](functions-reference-java#folder-structure).When required, sign in to your Azure account and select the active subscription using the

command.`az login`

`az login`

Run the

command to deploy the application package located in the relative`az functionapp deployment source config-zip`

`<FILE_PATH>`

.`az functionapp deployment source config-zip --src <FILE_PATH> --name <APP_NAME> --resource-group <RESOURCE_GROUP>`


Create a .zip file that contains the root directory of your code project. For more information, see

[Folder structure](functions-reference-powershell#folder-structure).When required, sign in to your Azure account and select the active subscription using the

command.`az login`

`az login`

Run the

command to deploy the application package located in the relative`az functionapp deployment source config-zip`

`<FILE_PATH>`

.`az functionapp deployment source config-zip --src <FILE_PATH> --name <APP_NAME> --resource-group <RESOURCE_GROUP>`


Create a .zip file that contains the root directory of your code project. For more information, see

[Folder structure](functions-reference-node#folder-structure).When required, sign in to your Azure account and select the active subscription using the

command.`az login`

`az login`

Run the

command to deploy the application package located in the relative`az functionapp deployment source config-zip`

`<FILE_PATH>`

.`az functionapp deployment source config-zip --src <FILE_PATH> --name <APP_NAME> --resource-group <RESOURCE_GROUP> --build-remote true`

Make sure to set

`--build-remote true`

to perform a[remote build](functions-deployment-technologies#remote-build).

Create a .zip file that contains the root directory of your code project. For more information, see

[Folder structure](functions-reference-python#folder-structure).When required, sign in to your Azure account and select the active subscription using the

command.`az login`

`az login`

Run the

command to deploy the application package located in the relative`az functionapp deployment source config-zip`

`<FILE_PATH>`

.`az functionapp deployment source config-zip --src <FILE_PATH> --name <APP_NAME> --resource-group <RESOURCE_GROUP> --build-remote true`

Make sure to set

`--build-remote true`

to perform a[remote build](functions-deployment-technologies#remote-build).

## Create and deploy your app using Maven

You can use Maven to create a Flex Consumption hosted function app and required resources during deployment by modifying the pom.xml file.

Create a Java code project by completing the first part of one of these quickstart articles:

In your Java code project, open the pom.xml file and make these changes to create your function app in the Flex Consumption plan:

Change the value of

`<properties>.<azure.functions.maven.plugin.version>`

to`1.34.0`

.In the

`<plugin>.<configuration>`

section for the`azure-functions-maven-plugin`

, add or uncomment the`<pricingTier>`

element as follows:`<pricingTier>Flex Consumption</pricingTier>`


(Optional) Customize the Flex Consumption plan in your Maven deployment by also including these elements in the

`<plugin>.<configuration>`

section: .`<instanceSize>`

- sets the[instance memory](flex-consumption-plan#instance-sizes)size for the function app. The default value is`2048`

.`<maximumInstances>`

- sets the highest value for the maximum instances count of the function app.`<alwaysReadyInstances>`

- sets the[always ready instance counts](flex-consumption-plan#always-ready-instances)with child elements for HTTP trigger groups (`<http>`

), Durable Functions groups (`<durable>`

), and other specific triggers (`<my_function>`

). When you set any instance count greater than zero, you're charged for these instances whether your functions execute or not. For more information, see[Billing](flex-consumption-plan#billing).

Before you can deploy, sign in to your Azure subscription using the Azure CLI.

`az login`

The

command signs you into your Azure account.`az login`

Use the following command to deploy your code project to a new function app in Flex Consumption.

`mvn azure-functions:deploy`

Maven uses settings in the pom.xml template to create your function app in a Flex Consumption plan in Azure, along with the other required resources. Should these resources already exist, the code is deployed to your function app, overwriting any existing code.


## Enable virtual network integration

You can enable [virtual network integration](functions-networking-options#virtual-network-integration) for your app in a Flex Consumption plan. The examples in this section assume that your account already contains a [virtual network and subnet](../virtual-network/quick-create-cli#create-a-virtual-network-and-subnet). You can enable virtual network integration when you create your app or at a later time.

Important

The Flex Consumption plan currently doesn't support subnets with names that contain underscore (`_`

) characters.

To enable virtual networking when you create your app:

You can enable virtual network integration by running the [ az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create) command and including the

`--vnet`

and `--subnet`

parameters.[Create the virtual network and subnet](../virtual-network/quick-create-cli#create-a-virtual-network-and-subnet), if you don't have one already.Complete steps 1-4 in

[Create a Flex Consumption app](#create-a-flex-consumption-app)to create the resources required by your app.Run the

command, including the`az functionapp create`

`--vnet`

and`--subnet`

parameters, as in this example:`az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage-account <STORAGE_NAME> --flexconsumption-location <REGION> --runtime <RUNTIME_NAME> --runtime-version <RUNTIME_VERSION> --vnet <VNET_RESOURCE_ID> --subnet <SUBNET_NAME>`

The

`<VNET_RESOURCE_ID>`

value is the resource ID for the virtual network, which is in the format:`/subscriptions/<SUBSCRIPTION_ID>/resourceGroups/<RESOURCE_GROUP>/providers/Microsoft.Network/virtualNetworks/<VNET_NAME>`

. You can use this command to get a list of virtual network IDs, filtered by`<RESOURCE_GROUP>`

:`az network vnet list --resource-group <RESOURCE_GROUP> --output tsv --query "[]".id`

.

For end-to-end examples of how to create apps in Flex Consumption with virtual network integration see these resources:

[Flex Consumption: HTTP to Event Hubs using virtual network integration](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/README.md)[Flex Consumption: triggered from Service Bus using virtual network integration](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/blob/main/README.md)

To modify or delete virtual network integration in an existing app:

Use the [ az functionapp vnet-integration add](/en-us/cli/azure/functionapp/vnet-integration#az-functionapp-vnet-integration-add) command to enable virtual network integration to an existing function app:

```
az functionapp vnet-integration add --resource-group <RESOURCE_GROUP> --name <APP_NAME> --vnet <VNET_RESOURCE_ID> --subnet <SUBNET_NAME>
```


Use the [ az functionapp vnet-integration remove](/en-us/cli/azure/functionapp/vnet-integration#az-functionapp-vnet-integration-remove) command to disable virtual network integration in your app:

```
az functionapp vnet-integration remove --resource-group <RESOURCE_GROUP> --name <APP_NAME>
```


Use the [ az functionapp vnet-integration list](/en-us/cli/azure/functionapp/vnet-integration#az-functionapp-vnet-integration-list) command to list the current virtual network integrations for your app:

```
az functionapp vnet-integration list --resource-group <RESOURCE_GROUP> --name <APP_NAME>
```


When you're choosing a subnet, these considerations apply:

- The subnet you choose can't already be used for other purposes, such as with private endpoints or service endpoints, or be delegated to any other hosting plan or service.
- You can't share the same subnet between a Container Apps environment and a Flex Consumption app.
- You can share the same subnet with more than one app running in a Flex Consumption plan. Because the networking resources are shared across all apps, one function app might affect the performance of others on the same subnet.
- In a Flex Consumption plan, a single function app might use up to 40 IP addresses, even when the app scales beyond 40 instances. While this rule of thumb is helpful when estimating the subnet size you need, it isn't strictly enforced.

## Configure deployment settings

In the Flex Consumption plan, the deployment package that contains your app's code is maintained in an Azure Blob Storage container. By default, deployments use the same storage account (`AzureWebJobsStorage`

) and connection string value used by the Functions runtime to maintain your app. The connection string is stored in the `DEPLOYMENT_STORAGE_CONNECTION_STRING`

application setting. However, you can instead designate a blob container in a separate storage account as the deployment source for your code. You can also change the authentication method used to access the container.

A customized deployment source should meet this criteria:

- The storage account must already exist.
- The container to use for deployments must also exist.
- When more than one app uses the same storage account, each should have its own deployment container. Using a unique container for each app prevents the deployment packages from being overwritten, which would happen if apps shared the same container.

When configuring deployment storage authentication, keep these considerations in mind:

- As a security best practice, you should use managed identities when connecting to Azure Storage from your apps. For more information, see
[Connections](functions-reference#connections). - When you use a connection string to connect to the deployment storage account, the application setting that contains the connection string must already exist.
- When you use a user-assigned managed identity, the provided identity gets linked to the function app. The
`Storage Blob Data Contributor`

role scoped to the deployment storage account also gets assigned to the identity. - When you use a system-assigned managed identity, an identity gets created when a valid system-assigned identity doesn't already exist in your app. When a system-assigned identity does exists, the
`Storage Blob Data Contributor`

role scoped to the deployment storage account also gets assigned to the identity.

To configure deployment settings when you create your function app in the Flex Consumption plan:

Use the [ az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create) command and supply these extra options that customize deployment storage:

| Parameter | Description |
|---|---|
`--deployment-storage-name` |
The name of the deployment storage account. |
`--deployment-storage-container-name` |
The name of the container in the account to contain your app's deployment package. |
`--deployment-storage-auth-type` |
The authentication type to use for connecting to the deployment storage account. Accepted values include `StorageAccountConnectionString` , `UserAssignedIdentity` , and `SystemAssignedIdentity` . |
`--deployment-storage-auth-value` |
When using `StorageAccountConnectionString` , this parameter is set to the name of the application setting that contains the connection string to the deployment storage account. When you set `UserAssignedIdentity` , this parameter is set to the name of the resource ID of the identity you want to use. |

This example creates a function app in the Flex Consumption plan with a separate deployment storage account and user assigned identity:

```
az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage <STORAGE_NAME> --runtime dotnet-isolated --runtime-version 8.0 --flexconsumption-location "<REGION>" --deployment-storage-name <DEPLOYMENT_ACCOUNT_NAME> --deployment-storage-container-name <DEPLOYMENT_CONTAINER_NAME> --deployment-storage-auth-type UserAssignedIdentity --deployment-storage-auth-value <MI_RESOURCE_ID>
```


You can also modify the deployment storage configuration for an existing app.

Use the [ az functionapp deployment config set](/en-us/cli/azure/functionapp/deployment/config#az-functionapp-deployment-config-set) command to modify the deployment storage configuration:

```
az functionapp deployment config set --resource-group <RESOURCE_GROUP> --name <APP_NAME> --deployment-storage-name <DEPLOYMENT_ACCOUNT_NAME> --deployment-storage-container-name <DEPLOYMENT_CONTAINER_NAME>
```


## Configure instance memory

The instance memory size used by your Flex Consumption plan can be explicitly set when you create your app. For more information about supported sizes, see [Instance sizes](flex-consumption-plan#instance-sizes).

To set an instance memory size that's different from the default when creating your app:

Specify the `--instance-memory`

parameter in your [ az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create) command. This example creates a C# app with an instance size of

`4096`

:```
az functionapp create --instance-memory 4096 --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage-account <STORAGE_NAME> --flexconsumption-location <REGION> --runtime dotnet-isolated --runtime-version 8.0
```


At any point, you can change the instance memory size setting used by your app.

This example uses the [ az functionapp scale config set](/en-us/cli/azure/functionapp/scale/config#az-functionapp-scale-config-set) command to change the instance memory size setting to 512 MB:

```
az functionapp scale config set --resource-group <resourceGroup> --name <APP_NAME> --instance-memory 512
```


## Set always ready instance counts

You can set a specific number of always ready instances for the [Per-function scaling](flex-consumption-plan#per-function-scaling) groups or individual functions, to keep your functions loaded and ready to execute. There are three special groups, as in per-function scaling:

`http`

- All of the HTTP triggered functions in the app scale together into their own instances.`durable`

- All of the Durable triggered functions (Orchestration, Activity, Entity) in the app scale together into their own instances.`blob`

- All of the blob (Event Grid) triggered functions in the app scale together into their own instances.

Use `http`

, `durable`

, or `blob`

as the name for the name value pair setting to configure always ready counts for these groups. For all other functions in the app you need to configure always ready for each individual function using the format `function:<FUNCTION_NAME>=n`

.

To define one or more always ready instance designations, use the `--always-ready-instances`

parameter with the [ az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create) command. This example sets the always ready instance count for all HTTP triggered functions to

`10`

:```
az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage <STORAGE_NAME> --runtime <LANGUAGE_RUNTIME> --runtime-version <RUNTIME_VERSION> --flexconsumption-location <REGION> --always-ready-instances http=10
```


This example sets the always ready instance count for all Durable trigger functions to `3`

and sets the always ready instance count to `2`

for a service bus triggered function named `function5`

:

```
az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage <STORAGE_NAME> --runtime <LANGUAGE_RUNTIME> --runtime-version <RUNTIME_VERSION> --flexconsumption-location <REGION> --always-ready-instances durable=3 function:function5=2
```


You can also modify always ready instances on an existing app by adding or removing instance designations or by changing existing instance designation counts.

This example uses the [ az functionapp scale config always-ready set](/en-us/cli/azure/functionapp/scale/config/always-ready#az-functionapp-scale-config-always-ready-set) command to change the always ready instance count for the HTTP triggers group to

`10`

:```
az functionapp scale config always-ready set --resource-group <RESOURCE_GROUP> --name <APP_NAME> --settings http=10
```


To remove always ready instances, use the [ az functionapp scale config always-ready delete](/en-us/cli/azure/functionapp/scale/config/always-ready#az-functionapp-scale-config-always-ready-delete) command, as in this example that removes all always ready instances from both the HTTP triggers group and also a function named

`hello_world`

:```
az functionapp scale config always-ready delete --resource-group <RESOURCE_GROUP> --name <APP_NAME> --setting-names http function:hello_world
```


## Set HTTP concurrency limits

Unless you set specific limits, HTTP concurrency defaults for Flex Consumption plan apps are determined based on your instance size setting. For more information, see [HTTP trigger concurrency](functions-concurrency#http-trigger-concurrency).

Here's how you can set HTTP concurrency limits for an existing app:

Use the [ az functionapp scale config set](/en-us/cli/azure/functionapp/scale/config#az-functionapp-scale-config-set) command to set specific HTTP concurrency limits for your app, regardless of instance size.

```
az functionapp scale config set --resource-group <RESOURCE_GROUP> --name <APP_NAME> --trigger-type http --trigger-settings perInstanceConcurrency=10
```


This example sets the HTTP trigger concurrency level to `10`

. After you specifically set an HTTP concurrency value, that value is maintained despite any changes in your app's instance size setting.

## Set site update strategy

The Flex Consumption plan uniquely supports two different site update strategies that control how your function app handles code deployments and configuration changes. By default, Flex Consumption plan apps use the `Recreate`

strategy, which terminates currently executing functions during deployments. To enable zero-downtime deployments, you can configure the `RollingUpdate`

strategy instead. For more information, see [Site update strategies in Flex Consumption](flex-consumption-site-updates).

Note

Site update strategy configuration is currently in public preview and is only available through Bicep or ARM templates. You can't configure this setting using the Azure CLI, Azure portal, or Visual Studio Code.

Site update strategy configuration isn't currently supported in the Azure CLI. Use Bicep or ARM templates as described in [Configure site update strategy](flex-consumption-site-updates#configure-your-update-strategy).

## View currently supported regions

To view the list of regions that currently support Flex Consumption plans:

If you haven't done so already, sign in to Azure:

`az login`

The

command signs you into your Azure account.`az login`

Use the

`az functionapp list-flexconsumption-locations`

command to review the list of regions that currently support Flex Consumption in alphabetical order.`az functionapp list-flexconsumption-locations --query "sort_by(@, &name)[].{Region:name}" -o table`


When you create an app in the [Azure portal](flex-consumption-how-to?tabs=azure-portal#create-a-flex-consumption-app) or by using [Visual Studio Code](flex-consumption-how-to?tabs=vs-code#create-a-flex-consumption-app), currently unsupported regions are filtered out of the region list.

## Monitor your app in Azure

Azure Monitor provides these distinct sets of metrics to help you better understand how your function app runs in Azure:

- Platform metrics: provides infrastructure-level insights
- Application Insights: provides code-level insights, including traces and errors logs.

If you [enable Application Insights in your app](configure-monitoring#enable-application-insights-integration), you're able to:

- Track detailed execution times and dependencies
- Monitor individual function performance
- Analyze failures and exceptions
- Correlate platform metrics with application behavior with custom queries

For more information, see [Monitor Azure Functions](monitor-functions).

### Supported metrics

Run this script to view all of the platform metrics that are currently available your app:

```
appId=$(az functionapp show --name <APP_NAME> --resource-group <RESOURCE_GROUP> --query id -o tsv)
az monitor metrics list-definitions --resource $appId --query "[].{Name:name.localizedValue,Value:name.value}" -o table
```


In this example, replace `<RESOURCE_GROUP>`

and `<APP_NAME>`

with your resource group and function app names, respectively. This script gets the fully qualified app ID and returns the available platform metrics in a table.

### View metrics

You can review current metrics either in the Azure portal or by using the Azure CLI.

In the Azure portal, you can also create metrics alerts and pin charts and other reports to dashboards in the portal.

Use this script to generate a report of the current metrics for your app:

```
appId=$(az functionapp show --name <APP_NAME> --resource-group <RESOURCE_GROUP> --query id -o tsv)
appId=$(az functionapp show --name func-fuxigh6c255de --resource-group exampleRG --query id -o tsv)
echo -e "\nAlways-ready and on-emand execution counts..."
az monitor metrics list --resource $appId --metric "AlwaysReadyFunctionExecutionCount" --interval PT1H --output table
az monitor metrics list --resource $appId --metric "OnDemandFunctionExecutionCount" --interval PT1H --output table
echo -e "\nExecution units (MB-ms) in always-ready and on-emand execution counts..."
az monitor metrics list --resource $appId --metric "AlwaysReadyFunctionExecutionUnits" --interval PT1H --output table
az monitor metrics list --resource $appId --metric "OnDemandFunctionExecutionUnits" --interval PT1H --output table
echo -e "\nAlways-ready resource utilization..."
az monitor metrics list --resource $appId --metric "AlwaysReadyUnits" --interval PT1H --output table
echo -e "\nMemory utilization..."
az monitor metrics list --resource $appId --metric "AverageMemoryWorkingSet" --interval PT1H --output table
az monitor metrics list --resource $appId --metric "MemoryWorkingSet" --interval PT1H --output table
echo -e "\nInstance count and CPU utilization..."
az monitor metrics list --resource $appId --metric "InstanceCount" --interval PT1H --output table
az monitor metrics list --resource $appId --metric "CpuPercentage" --interval PT1H --output table
```


To learn more about metrics for Azure Functions, see [Monitor Azure Functions](monitor-functions).

### View logs

When your app is connected to Application Insights, you can better analyze your app performance and troubleshoot problems during execution.

- Use "Performance" to analyze response times and dependencies
- Use "Failures" to identify any errors occurring after migration
- Create custom queries in "Logs" to analyze function behavior. For example:

Use this query to compare success rates by instance:

```
requests
| where timestamp > ago(7d)
| summarize successCount=countif(success == true), failureCount=countif(success == false) by bin(timestamp, 1h), cloud_RoleName
| render timechart
```


Use this query to analyze the number of instances that were actively processing your function:

```
let _startTime = ago(20m); //Adjust start time as needed
let _endTime = now(); //Adjust end time as needed
let bins = 1s; //Adjust bin as needed - this will give per second results
requests
| where operation_Name == 'EventHubsTrigger' //Replace with the name of the function in the function app that you are analyzing
| where timestamp between(_startTime .. _endTime)
| make-series dcount(cloud_RoleInstance) default=0 on timestamp from _startTime to _endTime step bins
| render columnchart
```


### View costs

Because you can tune your app to adjust performance versus operating costs, it's important to track the costs associated with running your app in the Flex Consumption plan.

To view the current costs:

In your function app page in the

[Azure portal](https://portal.azure.com), select the resource group link.In the resource group page, select

**Cost Management**>**Cost analysis**.Review the current costs and cost trajectory of the app itself.

Optionally, select

**Cost Management**>**Alerts**and then**+ Add**to create a new alert for the app.

## Fine-tune your app

The Flex Consumption plan provides several settings that you can tune to refine the performance of your app. Actual performance and costs can vary based on your app-specific workload patterns and configuration. For example, higher [memory instance sizes](flex-consumption-plan#instance-sizes) can improve performance for memory-intensive operations but at a higher cost per active period.

Here are some adjustments you can make to fine-tune performance versus cost:

[Adjust concurrency settings](functions-concurrency)to maximize throughput per instance.[Choose the appropriate memory size](#configure-instance-memory)for your workload. Higher memory sizes cost more but can improve performance.
