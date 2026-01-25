---
merged_at: 2026-01-25T15:41:11.645084
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __configure-networking-how-to_functions-scenarios_functions-create-first-functio_433d42.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _configure-networking-how-to_functions-scenarios.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: configure-networking-how-to.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/configure-networking-how-to -->

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

<!-- DOCUMENTO FUSIONADO: functions-scenarios.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-scenarios -->

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

<!-- DOCUMENTO FUSIONADO: functions-create-first-function-resource-manager.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-first-function-resource-manager -->

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

<!-- DOCUMENTO FUSIONADO: _functions-bindings-storage-queue-output_functions-how-to-custom-container.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-storage-queue-output.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-queue-output -->

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

<!-- DOCUMENTO FUSIONADO: functions-how-to-custom-container.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-how-to-custom-container -->

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
