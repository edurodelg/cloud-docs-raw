---
merged_at: 2026-01-26T21:02:36.339646
merged_files: 2
---


---
<!-- Source: N/A -->

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
<!-- Source: N/A -->

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
