---
merged_at: 2026-01-25T15:41:11.656496
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-cosmosdb-v2-trigger.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2-trigger -->

# Azure Cosmos DB trigger for Azure Functions 2.x and higher

The Azure Cosmos DB Trigger uses the [Azure Cosmos DB change feed](/en-us/azure/cosmos-db/change-feed) to listen for inserts and updates across partitions. The change feed publishes new and updated items, not including updates from deletions. For an end-to-end scenario that uses the Azure Cosmos DB trigger, see [Quickstart: Respond to database changes in Azure Cosmos DB using Azure Functions](scenario-database-changes-azure-cosmosdb).

For information on setup and configuration details, see the [overview](functions-bindings-cosmosdb-v2).

Cosmos DB scaling decisions for the Consumption and Premium plans are done via target-based scaling. For more information, see [Target-based scaling](functions-target-based-scaling).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

The Python v1 programming model requires you to define bindings in a separate *function.json* file in the function folder. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-configuration#programming-model).

This article supports both programming models.

## Example

The usage of the trigger depends on the extension package version and the C# modality used in your function app, which can be one of the following:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

An in-process class library is a compiled C# function runs in the same process as the Functions runtime.

The following examples depend on the extension version for the given C# mode.

Apps using [Azure Cosmos DB extension version 4.x](functions-bindings-cosmosdb-v2?tabs=extensionv4) or higher have different attribute properties, which are shown here. This example refers to a simple `ToDoItem`

type.

```
namespace CosmosDBSamplesV2
{
// Customize the model with your own desired properties
public class ToDoItem
{
public string id { get; set; }
public string Description { get; set; }
}
}
```


```
using System.Collections.Generic;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using Microsoft.Extensions.Logging;
namespace CosmosDBSamplesV2
{
public static class CosmosTrigger
{
[FunctionName("CosmosTrigger")]
public static void Run([CosmosDBTrigger(
databaseName: "databaseName",
containerName: "containerName",
Connection = "CosmosDBConnectionSetting",
LeaseContainerName = "leases",
CreateLeaseContainerIfNotExists = true)]IReadOnlyList<ToDoItem> input, ILogger log)
{
if (input != null && input.Count > 0)
{
log.LogInformation("Documents modified " + input.Count);
log.LogInformation("First document Id " + input[0].id);
}
}
}
}
```


The following example shows a [C# function](functions-dotnet-class-library) that is invoked when there are inserts or updates in the specified database and collection.

```
using Microsoft.Azure.Documents;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using System.Collections.Generic;
using Microsoft.Extensions.Logging;
namespace CosmosDBSamplesV2
{
public static class CosmosTrigger
{
[FunctionName("CosmosTrigger")]
public static void Run([CosmosDBTrigger(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection",
LeaseCollectionName = "leases",
CreateLeaseCollectionIfNotExists = true)]IReadOnlyList<Document> documents,
ILogger log)
{
if (documents != null && documents.Count > 0)
{
log.LogInformation($"Documents modified: {documents.Count}");
log.LogInformation($"First document Id: {documents[0].Id}");
}
}
}
}
```


This example refers to a simple `ToDoItem`

type:

```
public class ToDoItem
{
public string? Id { get; set; }
public string? Description { get; set; }
}
```


The following function is invoked when there are inserts or updates in the specified database and collection.

```
[Function("CosmosTrigger")]
public void Run([CosmosDBTrigger(
databaseName: "ToDoItems",
containerName:"TriggerItems",
Connection = "CosmosDBConnection",
LeaseContainerName = "leases",
CreateLeaseContainerIfNotExists = true)] IReadOnlyList<ToDoItem> todoItems,
FunctionContext context)
{
if (todoItems is not null && todoItems.Any())
{
foreach (var doc in todoItems)
{
_logger.LogInformation("ToDoItem: {desc}", doc.Description);
}
}
}
```


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


An `IReadOnlyList<T>`

is used as the Azure Cosmos DB trigger binding parameter in the following example:

```
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
```


This example requires the following `using`

statements:

```
using System.Collections.Generic;
using System.Linq;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.Logging;
```


This function is invoked when there are inserts or updates in the specified database and container.

Because of schema changes in the Azure Cosmos DB SDK, version 4.x of the Azure Cosmos DB extension requires [azure-functions-java-library V3.0.0](https://central.sonatype.com/artifact/com.microsoft.azure.functions/azure-functions-java-library/3.0.0) for Java functions.

```
@FunctionName("CosmosDBTriggerFunction")
public void run(
@CosmosDBTrigger(
name = "items",
databaseName = "ToDoList",
containerName = "Items",
leaseContainerName="leases",
connection = "AzureCosmosDBConnection",
createLeaseContainerIfNotExists = true
)
Object inputItem,
final ExecutionContext context
) {
context.getLogger().info("Items modified: " + inputItems.size());
}
```


```
@FunctionName("cosmosDBMonitor")
public void cosmosDbProcessor(
@CosmosDBTrigger(name = "items",
databaseName = "ToDoList",
collectionName = "Items",
leaseCollectionName = "leases",
createLeaseCollectionIfNotExists = true,
connectionStringSetting = "AzureCosmosDBConnection") String[] items,
final ExecutionContext context ) {
context.getLogger().info(items.length + "item(s) is/are changed.");
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@CosmosDBTrigger`

annotation on parameters whose value would come from Azure Cosmos DB. This annotation can be used with native Java types, plain-old Java objects (POJOs), or nullable values using `Optional<T>`

.

The following example shows an Azure Cosmos DB trigger [TypeScript function](functions-reference-node?tabs=typescript). The function writes log messages when Azure Cosmos DB records are added or modified.

```
import { app, InvocationContext } from '@azure/functions';
export async function cosmosDBTrigger1(documents: unknown[], context: InvocationContext): Promise<void> {
context.log(`Cosmos DB function processed ${documents.length} documents`);
}
app.cosmosDB('cosmosDBTrigger1', {
connection: '<connection-app-setting>',
databaseName: 'Tasks',
containerName: 'Items',
createLeaseContainerIfNotExists: true,
handler: cosmosDBTrigger1,
});
```


TypeScript samples aren't documented for model v3.

The following example shows an Azure Cosmos DB trigger [JavaScript function](functions-reference-node). The function writes log messages when Azure Cosmos DB records are added or modified.

```
const { app } = require('@azure/functions');
app.cosmosDB('cosmosDBTrigger1', {
connection: '<connection-app-setting>',
databaseName: 'Tasks',
containerName: 'Items',
createLeaseContainerIfNotExists: true,
handler: (documents, context) => {
context.log(`Cosmos DB function processed ${documents.length} documents`);
},
});
```


The following example shows an Azure Cosmos DB trigger binding in a *function.json* file and a [JavaScript function](functions-reference-node) that uses the binding. The function writes log messages when Azure Cosmos DB records are added or modified.

Here's the binding data in the *function.json* file:

```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseCollectionName": "leases",
"connectionStringSetting": "<connection-app-setting>",
"databaseName": "Tasks",
"collectionName": "Items",
"createLeaseCollectionIfNotExists": true
}
```


```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseContainerName": "leases",
"connection": "<connection-app-setting>",
"databaseName": "Tasks",
"containerName": "Items",
"createLeaseContainerIfNotExists": true
}
```


Note that some of the binding attribute names changed in version 4.x of the Azure Cosmos DB extension.

Here's the JavaScript code:

```
module.exports = async function (context, documents) {
context.log('First document Id modified : ', documents[0].id);
}
```


The following example shows how to run a function as data changes in Azure Cosmos DB.

```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseCollectionName": "leases",
"connectionStringSetting": "<connection-app-setting>",
"databaseName": "Tasks",
"collectionName": "Items",
"createLeaseCollectionIfNotExists": true
}
```


```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseContainerName": "leases",
"connection": "<connection-app-setting>",
"databaseName": "Tasks",
"containerName": "Items",
"createLeaseContainerIfNotExists": true
}
```


Note that some of the binding attribute names changed in version 4.x of the Azure Cosmos DB extension.

In the *run.ps1* file, you have access to the document that triggers the function via the `$Documents`

parameter.

```
param($Documents, $TriggerMetadata)
Write-Host "First document Id modified : $($Documents[0].id)"
```


The following example shows an Azure Cosmos DB trigger binding. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="CosmosDBTrigger")
@app.cosmos_db_trigger(arg_name="documents",
connection="CONNECTION_SETTING",
database_name="DB_NAME",
container_name="CONTAINER_NAME",
lease_container_name="leases",
create_lease_container_if_not_exists="true")
def test_function(documents: func.DocumentList) -> str:
if documents:
logging.info('Document id: %s', documents[0]['id'])
```


The function writes log messages when Azure Cosmos DB records are modified. Here's the binding data in the *function.json* file:

```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseCollectionName": "leases",
"connectionStringSetting": "<connection-app-setting>",
"databaseName": "Tasks",
"collectionName": "Items",
"createLeaseCollectionIfNotExists": true
}
```


```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseContainerName": "leases",
"connection": "<connection-app-setting>",
"databaseName": "Tasks",
"containerName": "Items",
"createLeaseContainerIfNotExists": true
}
```


Note that some of the binding attribute names changed in version 4.x of the Azure Cosmos DB extension.

Here's the Python code:

```
import logging
import azure.functions as func
def main(documents: func.DocumentList) -> str:
if documents:
logging.info('First document Id modified: %s', documents[0]['id'])
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated process](dotnet-isolated-process-guide) C# libraries use `CosmosDBTriggerAttribute`

to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#azure-cosmos-db-v2-trigger).

The specific properties depends both on the process model and the extension version:

In-process libraries use [CosmosDBTriggerAttribute](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.CosmosDB/Trigger/CosmosDBTriggerAttribute.cs) from the `Microsoft.Azure.WebJobs`

namespace, which defines these properties:

| Attribute property |
Description |
**Connection** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**DatabaseName** |
The name of the Azure Cosmos DB database with the container being monitored. |
**ContainerName** |
The name of the container being monitored. |
**LeaseConnection** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease container.
When not set, the `Connection` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases container must have write permissions. |
**LeaseDatabaseName** |
(Optional) The name of the database that holds the container used to store leases. When not set, the value of the `databaseName` setting is used. |
**LeaseContainerName** |
(Optional) The name of the container used to store leases. When not set, the value `leases` is used. |
**CreateLeaseContainerIfNotExists** |
(Optional) When set to `true` , the leases container is automatically created when it doesn't already exist. The default value is `false` . When using Microsoft Entra identities if you set the value to `true` , creating containers is not [an allowed operation](/en-us/azure/cosmos-db/troubleshoot-forbidden#non-data-operations-are-not-allowed) and your Function won't be able to start. |
**LeasesContainerThroughput** |
(Optional) Defines the number of Request Units to assign when the leases container is created. This setting is only used when `CreateLeaseContainerIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**LeaseContainerPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease container for this function. Using a prefix allows two separate Azure Functions to share the same Lease container by using different prefixes. |
**FeedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**LeaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**LeaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**LeaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**MaxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored container are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**StartFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the container's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**StartFromTime** |
(Optional) Gets or sets the date and time from which to initialize the change feed read operation. The recommended format is ISO 8601 with the UTC designator, such as `2021-02-16T14:19:29Z` . This is only used to set the initial trigger state. After the trigger has a lease state, changing this value has no effect. |
**PreferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |

In-process libraries use [CosmosDBTriggerAttribute](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.CosmosDB/Trigger/CosmosDBTriggerAttribute.cs) from the `Microsoft.Azure.WebJobs`

namespace, which defines these properties:

| Attribute property |
Description |
**ConnectionStringSetting** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**DatabaseName** |
The name of the Azure Cosmos DB database with the collection being monitored. |
**CollectionName** |
The name of the collection being monitored. |
**LeaseConnectionStringSetting** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease collection.
When not set, the `ConnectionStringSetting` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases collection must have write permissions. |
**LeaseDatabaseName** |
(Optional) The name of the database that holds the collection used to store leases. When not set, the value of the `databaseName` setting is used. |
**LeaseCollectionName** |
(Optional) The name of the collection used to store leases. When not set, the value `leases` is used. |
**CreateLeaseCollectionIfNotExists** |
(Optional) When set to `true` , the leases collection is automatically created when it doesn't already exist. The default value is `false` . |
**LeasesCollectionThroughput** |
(Optional) Defines the number of Request Units to assign when the leases collection is created. This setting is only used when `CreateLeaseCollectionIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**LeaseCollectionPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease collection for this function. Using a prefix allows two separate Azure Functions to share the same Lease collection by using different prefixes. |
**FeedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**LeaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**LeaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**LeaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**CheckpointInterval** |
(Optional) When set, it defines, in milliseconds, the interval between lease checkpoints. Default is always after each Function call. |
**CheckpointDocumentCount** |
(Optional) Customizes the amount of documents between lease checkpoints. Default is after every function call. |
**MaxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored collection are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**StartFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the collection's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**PreferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |
**UseMultipleWriteLocations** |
(Optional) Enables multi-region accounts for writing to the leases collection. |
**UseDefaultJsonSerialization** |
(Optional) Lets you use `JsonConvert.DefaultSettings` in the monitored collection. This setting only applies to the monitored collection and the consumer to setup the serialization used in the monitored collection. The `JsonConvert.DefaultSettings` must be set in a class derived from `CosmosDBWebJobsStartup` . |

Isolated worker process libraries use [CosmosDBTriggerAttribute](https://github.com/Azure/azure-functions-dotnet-worker/blob/main/extensions/Worker.Extensions.CosmosDB/src/CosmosDBTriggerAttribute.cs) from the `Microsoft.Azure.Functions.Worker`

namespace, which defines these properties:

| Attribute property |
Description |
**Connection** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**DatabaseName** |
The name of the Azure Cosmos DB database with the container being monitored. |
**ContainerName** |
The name of the container being monitored. |
**LeaseConnection** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease container.
When not set, the `Connection` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases container must have write permissions. |
**LeaseDatabaseName** |
(Optional) The name of the database that holds the container used to store leases. When not set, the value of the `databaseName` setting is used. |
**LeaseContainerName** |
(Optional) The name of the container used to store leases. When not set, the value `leases` is used. |
**CreateLeaseContainerIfNotExists** |
(Optional) When set to `true` , the leases container is automatically created when it doesn't already exist. The default value is `false` . When using Microsoft Entra identities if you set the value to `true` , creating containers is not [an allowed operation](/en-us/azure/cosmos-db/troubleshoot-forbidden#non-data-operations-are-not-allowed) and your Function won't be able to start. |
**LeasesContainerThroughput** |
(Optional) Defines the number of Request Units to assign when the leases container is created. This setting is only used when `CreateLeaseContainerIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**LeaseContainerPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease container for this function. Using a prefix allows two separate Azure Functions to share the same Lease container by using different prefixes. |
**FeedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**LeaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**LeaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**LeaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**MaxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored container are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**StartFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the container's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**StartFromTime** |
(Optional) Gets or sets the date and time from which to initialize the change feed read operation. The recommended format is ISO 8601 with the UTC designator, such as `2021-02-16T14:19:29Z` . This is only used to set the initial trigger state. After the trigger has a lease state, changing this value has no effect. |
**PreferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |

Isolated worker process libraries use [CosmosDBTriggerAttribute](https://github.com/Azure/azure-functions-dotnet-worker/blob/main/extensions/Worker.Extensions.CosmosDB/src/CosmosDBTriggerAttribute.cs) from the `Microsoft.Azure.Functions.Worker`

namespace, which defines these properties:.

| Attribute property |
Description |
**ConnectionStringSetting** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**DatabaseName** |
The name of the Azure Cosmos DB database with the collection being monitored. |
**CollectionName** |
The name of the collection being monitored. |
**LeaseConnectionStringSetting** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease collection.
When not set, the `ConnectionStringSetting` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases collection must have write permissions. |
**LeaseDatabaseName** |
(Optional) The name of the database that holds the collection used to store leases. When not set, the value of the `databaseName` setting is used. |
**LeaseCollectionName** |
(Optional) The name of the collection used to store leases. When not set, the value `leases` is used. |
**CreateLeaseCollectionIfNotExists** |
(Optional) When set to `true` , the leases collection is automatically created when it doesn't already exist. The default value is `false` . |
**LeasesCollectionThroughput** |
(Optional) Defines the number of Request Units to assign when the leases collection is created. This setting is only used when `CreateLeaseCollectionIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**LeaseCollectionPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease collection for this function. Using a prefix allows two separate Azure Functions to share the same Lease collection by using different prefixes. |
**FeedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**LeaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**LeaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**LeaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**CheckpointInterval** |
(Optional) When set, it defines, in milliseconds, the interval between lease checkpoints. Default is always after each Function call. |
**CheckpointDocumentCount** |
(Optional) Customizes the amount of documents between lease checkpoints. Default is after every function call. |
**MaxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored collection are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**StartFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the collection's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**PreferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |
**UseMultipleWriteLocations** |
(Optional) Enables multi-region accounts for writing to the leases collection. |
**UseDefaultJsonSerialization** |
(Optional) Lets you use `JsonConvert.DefaultSettings` in the monitored collection. This setting only applies to the monitored collection and the consumer to setup the serialization used in the monitored collection. The `JsonConvert.DefaultSettings` must be set in a class derived from `CosmosDBWebJobsStartup` . |

## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, the following properties on the `cosmos_db_trigger`

:

| Property |
Description |
`arg_name` |
The variable name used in function code that represents the list of documents with changes. |
`database_name` |
The name of the Azure Cosmos DB database with the container being monitored. |
`container_name` |
The name of the Azure Cosmos DB container being monitored. |
`connection` |
The connection string of the Azure Cosmos DB being monitored. |

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

Because of schema changes in the Azure Cosmos DB SDK, version 4.x of the Azure Cosmos DB extension requires [azure-functions-java-library V3.0.0](https://central.sonatype.com/artifact/com.microsoft.azure.functions/azure-functions-java-library/3.0.0) for Java functions.

Use the `@CosmosDBTrigger`

annotation on parameters that read data from Azure Cosmos DB. The annotation supports the following properties:

| Attribute property |
Description |
**connection** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**name** |
The name of the function. |
**databaseName** |
The name of the Azure Cosmos DB database with the container being monitored. |
**containerName** |
The name of the container being monitored. |
**leaseConnectionStringSetting** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease container.
When not set, the `Connection` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases container must have write permissions. |
**leaseDatabaseName** |
(Optional) The name of the database that holds the container used to store leases. When not set, the value of the `databaseName` setting is used. |
**leaseContainerName** |
(Optional) The name of the container used to store leases. When not set, the value `leases` is used. |
**createLeaseContainerIfNotExists** |
(Optional) When set to `true` , the leases container is automatically created when it doesn't already exist. The default value is `false` . When using Microsoft Entra identities if you set the value to `true` , creating containers isn't [an allowed operation](/en-us/azure/cosmos-db/troubleshoot-forbidden#nondata-operations-arent-allowed) and your function app isn't allowed to start. |
**leasesContainerThroughput** |
(Optional) Defines the number of Request Units to assign when the leases container is created. This setting is only used when `CreateLeaseContainerIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**leaseContainerPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease container for this function. Using a prefix allows two separate Azure Functions to share the same Lease container by using different prefixes. |
**feedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**leaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**leaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease isn't renewed within this interval, it expires and ownership of the partition moves to another instance. Default is 60000 (60 seconds). |
**leaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renewal interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**maxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored container are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**startFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the container's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**preferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, `East US,South Central US,North Europe` . |

From the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@CosmosDBTrigger`

annotation on parameters that read data from Azure Cosmos DB. The annotation supports the following properties:


## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `app.cosmosDB()`

method. The `type`

, `direction`

, and `name`

properties don't apply to the v4 model.

The following table explains the binding configuration properties that you set in the *function.json* file, where properties differ by extension version:

The following table explains the binding configuration properties that you set in the *function.json* file, where properties differ by extension version:

| function.json property |
Description |
**type** |
Must be set to `cosmosDBTrigger` . |
**direction** |
Must be set to `in` . This parameter is set automatically when you create the trigger in the Azure portal. |
**name** |
The variable name used in function code that represents the list of documents with changes. |
**connection** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](functions-bindings-cosmosdb-v2-trigger#connections). |
**databaseName** |
The name of the Azure Cosmos DB database with the container being monitored. |
**containerName** |
The name of the container being monitored. |
**leaseConnection** |
(Optional) The name of an app setting or setting container that specifies how to connect to the Azure Cosmos DB account that holds the lease container.
When not set, the `connection` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases container must have write permissions. |
**leaseDatabaseName** |
(Optional) The name of the database that holds the container used to store leases. When not set, the value of the `databaseName` setting is used. |
**leaseContainerName** |
(Optional) The name of the container used to store leases. When not set, the value `leases` is used. |
**createLeaseContainerIfNotExists** |
(Optional) When set to `true` , the leases container is automatically created when it doesn't already exist. The default value is `false` . When using Microsoft Entra identities if you set the value to `true` , creating containers is not [an allowed operation](/en-us/azure/cosmos-db/troubleshoot-forbidden#non-data-operations-are-not-allowed) and your Function won't be able to start. |
**leasesContainerThroughput** |
(Optional) Defines the number of Request Units to assign when the leases container is created. This setting is only used when `createLeaseContainerIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**leaseContainerPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease container for this function. Using a prefix allows two separate Azure Functions to share the same Lease container by using different prefixes. |
**feedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**leaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**leaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**leaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**maxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored container are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**startFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the container's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**startFromTime** |
(Optional) Gets or sets the date and time from which to initialize the change feed read operation. The recommended format is ISO 8601 with the UTC designator, such as `2021-02-16T14:19:29Z` . This is only used to set the initial trigger state. After the trigger has a lease state, changing this value has no effect. |
**preferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |

| function.json property |
Description |
**type** |
Must be set to `cosmosDBTrigger` . |
**direction** |
Must be set to `in` . This parameter is set automatically when you create the trigger in the Azure portal. |
**name** |
The variable name used in function code that represents the list of documents with changes. |
**connectionStringSetting** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**databaseName** |
The name of the Azure Cosmos DB database with the collection being monitored. |
**collectionName** |
The name of the collection being monitored. |
**leaseConnectionStringSetting** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease collection.
When not set, the `connectionStringSetting` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases collection must have write permissions. |
**leaseDatabaseName** |
(Optional) The name of the database that holds the collection used to store leases. When not set, the value of the `databaseName` setting is used. |
**leaseCollectionName** |
(Optional) The name of the collection used to store leases. When not set, the value `leases` is used. |
**createLeaseCollectionIfNotExists** |
(Optional) When set to `true` , the leases collection is automatically created when it doesn't already exist. The default value is `false` . |
**leasesCollectionThroughput** |
(Optional) Defines the number of Request Units to assign when the leases collection is created. This setting is only used when `createLeaseCollectionIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**leaseCollectionPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease collection for this function. Using a prefix allows two separate Azure Functions to share the same Lease collection by using different prefixes. |
**feedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**leaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**leaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**leaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**checkpointInterval** |
(Optional) When set, it defines, in milliseconds, the interval between lease checkpoints. Default is always after each Function call. |
**checkpointDocumentCount** |
(Optional) Customizes the amount of documents between lease checkpoints. Default is after every function call. |
**maxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored collection are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**startFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the collection's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**preferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |
**useMultipleWriteLocations** |
(Optional) Enables multi-region accounts for writing to the leases collection. |

See the [Example section](#example) for complete examples.

## Usage

The trigger requires a second collection that it uses to store *leases* over the partitions. Both the collection being monitored and the collection that contains the leases must be available for the trigger to work.

Important

If multiple functions are configured to use an Azure Cosmos DB trigger for the same collection, each of the functions should use a dedicated lease collection or specify a different `LeaseCollectionPrefix`

for each function. Otherwise, only one of the functions is triggered. For information about the prefix, see the [Attributes section](#attributes).

Important

If multiple functions are configured to use an Azure Cosmos DB trigger for the same collection, each of the functions should use a dedicated lease collection or specify a different `leaseCollectionPrefix`

for each function. Otherwise, only one of the functions is triggered. For information about the prefix, see the [Annotations section](#annotations).

Important

If multiple functions are configured to use an Azure Cosmos DB trigger for the same collection, each of the functions should use a dedicated lease collection or specify a different `leaseCollectionPrefix`

for each function. Otherwise, only one of the functions is triggered. For information about the prefix, see the [Configuration section](#configuration).

The trigger doesn't indicate whether a document was updated or inserted, it just provides the document itself. If you need to handle updates and inserts differently, you could do that by implementing timestamp fields for insertion or update.

The parameter type supported by the Azure Cosmos DB trigger depends on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to process a single document, the Cosmos DB trigger can bind to the following types:

| Type |
Description |
| JSON serializable types |
Functions tries to deserialize the JSON data of the document from the Cosmos DB change feed into a plain-old CLR object (POCO) type. |

When you want the function to process a batch of documents, the Cosmos DB trigger can bind to the following types:

| Type |
Description |
`IEnumerable<T>` where `T` is a JSON serializable type |
An enumeration of entities included in the batch. Each entry represents one document from the Cosmos DB change feed. |

## Connections

The `connectionStringSetting`

/`connection`

and `leaseConnectionStringSetting`

/`leaseConnection`

properties are references to environment configuration which specifies how the app should connect to Azure Cosmos DB. They may specify:

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

The connection string for your database account should be stored in an application setting with a name matching the value specified by the connection property of the binding configuration.

### Identity-based connections

If you are using [version 4.x or higher of the extension](functions-bindings-cosmosdb-v2?tabs=extensionv4), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). To do this, you would define settings under a common prefix which maps to the connection property in the trigger and binding configuration.

In this mode, the extension requires the following properties:

| Property |
Environment variable template |
Description |
Example value |
| Account Endpoint |
`<CONNECTION_NAME_PREFIX>__accountEndpoint` |
The Azure Cosmos DB account endpoint URI. |
https://<database_account_name>.documents.azure.com:443/ |

Additional properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

Cosmos DB does not use Azure RBAC for data operations. Instead, it uses a [Cosmos DB built-in RBAC system](/en-us/azure/cosmos-db/how-to-setup-rbac) which is built on similar concepts. You will need to create a role assignment that provides access to your database account at runtime. Azure RBAC Management roles like [Owner](../role-based-access-control/built-in-roles#owner) are not sufficient. The following table shows built-in roles that are recommended when using the Azure Cosmos DB extension in normal operation. Your application may require additional permissions based on the code you write.

1 These roles cannot be used in an Azure RBAC role assignment. See the [Cosmos DB built-in RBAC system](/en-us/azure/cosmos-db/how-to-setup-rbac) documentation for details on how to assign these roles.

2 When using identity, Cosmos DB treats container creation as a management operation. It is not available as a data-plane operation for the trigger. You will need to ensure that you create the containers needed by the trigger (including the lease container) before setting up your function.

## Next steps


---

<!-- DOCUMENTO FUSIONADO: __functions-bindings-event-grid-trigger_deployment-zip-push_functions-bindings-s_770438.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-event-grid-trigger_deployment-zip-push.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-event-grid-trigger.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-grid-trigger -->

# Azure Event Grid trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the function trigger to respond to an event sent by an [Event Grid source](../event-grid/overview). You must have an event subscription to the source to receive events. To learn how to create an event subscription, see [Create a subscription](event-grid-how-tos#create-a-subscription). For information on binding setup and configuration, see the [overview](functions-bindings-event-grid).

Note

Event Grid triggers aren't natively supported in an internal load balancer App Service Environment (ASE). The trigger uses an HTTP request that can't reach the function app without a gateway into the virtual network.

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

## Example

For an HTTP trigger example, see [Receive events to an HTTP endpoint](../event-grid/receive-events).

The type of the input parameter used with an Event Grid trigger depends on these three factors:

- Functions runtime version
- Binding extension version
- Modality of the C# function.

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

When running your C# function in an isolated worker process, you need to define a custom type for event properties. The following example defines a `MyEventType`

class.

```
{
public string? Id { get; set; }
public string? Topic { get; set; }
public string? Subject { get; set; }
public string? EventType { get; set; }
public DateTime EventTime { get; set; }
public IDictionary<string, object>? Data { get; set; }
}
```


The following example shows how the custom type is used in both the trigger and an Event Grid output binding:

```
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
```


This section contains the following examples:

The following examples show trigger binding in [Java](functions-reference-java) that use the binding and generate an event, first receiving the event as `String`

and second as a POJO.

### Event Grid trigger, String parameter

```
@FunctionName("eventGridMonitorString")
public void logEvent(
@EventGridTrigger(
name = "event"
)
String content,
final ExecutionContext context) {
context.getLogger().info("Event content: " + content);
}
```


### Event Grid trigger, POJO parameter

This example uses the following POJO, representing the top-level properties of an Event Grid event:

```
import java.util.Date;
import java.util.Map;
public class EventSchema {
public String topic;
public String subject;
public String eventType;
public Date eventTime;
public String id;
public String dataVersion;
public String metadataVersion;
public Map<String, Object> data;
}
```


Upon arrival, the event's JSON payload is de-serialized into the `EventSchema`

POJO for use by the function. This process allows the function to access the event's properties in an object-oriented way.

```
@FunctionName("eventGridMonitor")
public void logEvent(
@EventGridTrigger(
name = "event"
)
EventSchema event,
final ExecutionContext context) {
context.getLogger().info("Event content: ");
context.getLogger().info("Subject: " + event.subject);
context.getLogger().info("Time: " + event.eventTime); // automatically converted to Date by the runtime
context.getLogger().info("Id: " + event.id);
context.getLogger().info("Data: " + event.data);
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `EventGridTrigger`

annotation on parameters whose value would come from Event Grid. Parameters with these annotations cause the function to run when an event arrives. This annotation can be used with native Java types, POJOs, or nullable values using `Optional<T>`

.

The following example shows an event grid trigger [TypeScript function](functions-reference-node?tabs=typescript).

```
import { app, EventGridEvent, InvocationContext } from '@azure/functions';
export async function eventGridTrigger1(event: EventGridEvent, context: InvocationContext): Promise<void> {
context.log('Event grid function processed event:', event);
}
app.eventGrid('eventGridTrigger1', {
handler: eventGridTrigger1,
});
```


The following example shows an event grid trigger [JavaScript function](functions-reference-node).

```
const { app } = require('@azure/functions');
app.eventGrid('eventGridTrigger1', {
handler: (event, context) => {
context.log('Event grid function processed event:', event);
},
});
```


The following example shows how to configure an Event Grid trigger binding in the *function.json* file.

```
{
"bindings": [
{
"type": "eventGridTrigger",
"name": "eventGridEvent",
"direction": "in"
}
]
}
```


The Event Grid event is made available to the function via a parameter named `eventGridEvent`

, as shown in the following PowerShell example.

```
param($eventGridEvent, $TriggerMetadata)
# Make sure to pass hashtables to Out-String so they're logged correctly
$eventGridEvent | Out-String | Write-Host
```


The following example shows an Event Grid trigger binding and a Python function that uses the binding. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="eventGridTrigger")
@app.event_grid_trigger(arg_name="event")
def eventGridTest(event: func.EventGridEvent):
result = json.dumps({
'id': event.id,
'data': event.get_json(),
'topic': event.topic,
'subject': event.subject,
'event_type': event.event_type,
})
logging.info('Python EventGrid trigger processed an event: %s', result)
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the [EventGridTrigger](https://github.com/Azure/azure-functions-eventgrid-extension/blob/master/src/EventGridExtension/TriggerBinding/EventGridTriggerAttribute.cs) attribute. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#event-grid-trigger).

Here's an `EventGridTrigger`

attribute in a method signature:

```
[Function(nameof(EventGridFunction))]
[EventGridOutput(TopicEndpointUri = "MyEventGridTopicUriSetting", TopicKeySetting = "MyEventGridTopicKeySetting")]
public static MyEventType Run([EventGridTrigger] MyEventType input, FunctionContext context)
{
```


## Annotations

The [EventGridTrigger](/en-us/java/api/com.microsoft.azure.functions.annotation.eventgridtrigger) annotation allows you to declaratively configure an Event Grid binding by providing configuration values. See the [example](#example) and [configuration](#configuration) sections for more detail.

## Configuration

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file. There are no constructor parameters or properties to set in the `EventGridTrigger`

attribute.

| function.json property | Description |
|---|---|
type |
Required - must be set to `eventGridTrigger` . |
direction |
Required - must be set to `in` . |
name |
Required - the variable name used in function code for the parameter that receives the event data. |

See the [Example section](#example) for complete examples.

## Usage

The Event Grid trigger uses a webhook HTTP request, which can be configured using the same [ host.json settings as the HTTP Trigger](functions-bindings-http-webhook#hostjson-settings).

The parameter type supported by the Event Grid trigger depends on the Functions runtime version, the extension package version, and the C# modality used.

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

The Event Grid event instance is available via the parameter associated to the `EventGridTrigger`

attribute, typed as an `EventSchema`

.

The Event Grid instance is available via the parameter configured in the *function.json* file's `name`

property.

The Event Grid instance is available via the parameter configured in the *function.json* file's `name`

property, typed as `func.EventGridEvent`

.

## Event schema

Data for an Event Grid event is received as a JSON object in the body of an HTTP request. The JSON looks similar to the following example:

```
[{
"topic": "/subscriptions/{subscriptionid}/resourceGroups/eg0122/providers/Microsoft.Storage/storageAccounts/egblobstore",
"subject": "/blobServices/default/containers/{containername}/blobs/blobname.jpg",
"eventType": "Microsoft.Storage.BlobCreated",
"eventTime": "2018-01-23T17:02:19.6069787Z",
"id": "{guid}",
"data": {
"api": "PutBlockList",
"clientRequestId": "{guid}",
"requestId": "{guid}",
"eTag": "0x8D562831044DDD0",
"contentType": "application/octet-stream",
"contentLength": 2248,
"blobType": "BlockBlob",
"url": "https://egblobstore.blob.core.windows.net/{containername}/blobname.jpg",
"sequencer": "000000000000272D000000000003D60F",
"storageDiagnostics": {
"batchId": "{guid}"
}
},
"dataVersion": "",
"metadataVersion": "1"
}]
```


The example shown is an array of one element. Event Grid always sends an array and may send more than one event in the array. The runtime invokes your function once for each array element.

The top-level properties in the event JSON data are the same among all event types, while the contents of the `data`

property are specific to each event type. The example shown is for a blob storage event.

For explanations of the common and event-specific properties, see [Event properties](../event-grid/event-schema#event-properties) in the Event Grid documentation.

## Next steps

- If you have questions, submit an issue to the team
[here](https://github.com/Azure/azure-sdk-for-net/issues) [Dispatch an Event Grid event](functions-bindings-event-grid-output)


---

<!-- DOCUMENTO FUSIONADO: deployment-zip-push.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/deployment-zip-push -->

# Zip deployment for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to deploy your function app project files to Azure from a .zip (compressed) file. You learn how to do a push deployment, both by using Azure CLI and by using the REST APIs. [Azure Functions Core Tools](functions-run-local) also uses these deployment APIs when publishing a local project to Azure.

Zip deployment is also an easy way to [run your functions from a package file in Azure](run-functions-from-deployment-package). It's the default deployment technology in the [Consumption](consumption-plan), [Elastic Premium](functions-premium-plan), and [Dedicated (App Service)](dedicated-plan) hosting plans. The [Flex Consumption](flex-consumption-plan) plan doesn't support zip deployment.

Azure Functions has the full range of continuous deployment and integration options that are provided by Azure App Service. For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment).

To speed up development, you might find it easier to deploy your function app project files directly from a .zip file. The .zip deployment API takes the contents of a .zip file and extracts the contents into the `wwwroot`

folder of your function app. This .zip file deployment uses the same Kudu service that powers continuous integration-based deployments, including:

- Deletion of files that were left over from earlier deployments.
- Deployment customization, including running deployment scripts.
- Deployment logs.
- Syncing function triggers in a
[Consumption plan](functions-scale)function app.

For more information, see the [.zip deployment reference](https://github.com/projectkudu/kudu/wiki/Deploying-from-a-zip-file-or-url).

Important

When you use .zip deployment, any files from the previous deployment are either deleted or updated during a subsequent deployment to your function app. Other files and directories in your function app that weren't part of the previous deployment are maintained.

## Deployment .zip file requirements

The zip archive you deploy must contain all of the files needed to run your function app. You can manually create a zip archive from the contents of a Functions project folder using built-in .zip compression functionality or non-Microsoft tools.

The archive must include the [host.json](functions-host-json) file at the root of the extracted folder. The selected language stack for the function app creates other requirements:

Important

For languages that generate compiled output for deployment, make sure to compress the contents of the output folder you plan to publish and not the entire project folder. When Functions extracts the contents of the zip archive, the `host.json`

file must exist in the root of the package.

A zip deployment process extracts the zip archive's files and folders in the `wwwroot`

directory. If you include the parent directory when creating the archive, the system won't find the files it expects to see in `wwwroot`

.

## Deploy by using Azure CLI

You can use Azure CLI to trigger a push deployment. Push deploy a .zip file to your function app by using the [az functionapp deployment source config-zip](/en-us/cli/azure/functionapp/deployment/source#az-functionapp-deployment-source-config-zip) command. To use this command, you must use Azure CLI version 2.0.21 or later. To see what Azure CLI version you're using, use the `az --version`

command.

In the following command, replace the `<zip_file_path>`

placeholder with the path to the location of your .zip file. Also, replace `<app_name>`

with the unique name of your function app and replace `<resource_group>`

with the name of your resource group.

```
az functionapp deployment source config-zip -g <resource_group> -n \
<app_name> --src <zip_file_path>
```


This command deploys project files from the downloaded .zip file to your function app in Azure. It then restarts the app. To view the list of deployments for this function app, you must use the REST APIs.

When you're using Azure CLI on your local computer, `<zip_file_path>`

is the path to the .zip file on your computer. You can also run Azure CLI in [Azure Cloud Shell](../cloud-shell/overview). When you use Cloud Shell, you must first upload your deployment .zip file to the Azure Files account that's associated with your Cloud Shell. In that case, `<zip_file_path>`

is the storage location that your Cloud Shell account uses. For more information, see [Persist files in Azure Cloud Shell](../cloud-shell/persisting-shell-storage).

## Deploy ZIP file with REST APIs

You can use the [deployment service REST APIs](https://github.com/projectkudu/kudu/wiki/REST-API) to deploy the .zip file to your app in Azure. To deploy, send a POST request to `https://<app_name>.scm.azurewebsites.net/api/zipdeploy`

. The POST request must contain the .zip file in the message body. The deployment credentials for your app are provided in the request by using HTTP BASIC authentication. For more information, see the [.zip push deployment reference](https://github.com/projectkudu/kudu/wiki/Deploying-from-a-zip-file).

For the HTTP BASIC authentication, you need your App Service deployment credentials. To see how to set your deployment credentials, see [Set and reset user-level credentials](../app-service/deploy-configure-credentials#userscope).

### With cURL

The following example uses the cURL tool to deploy a .zip file. Replace the placeholders `<deployment_user>`

, `<zip_file_path>`

, and `<app_name>`

. When prompted by cURL, type in the password.

```
curl -X POST -u <deployment_user> --data-binary "@<zip_file_path>" https://<app_name>.scm.azurewebsites.net/api/zipdeploy
```


This request triggers push deployment from the uploaded .zip file. You can review the current and past deployments by using the `https://<app_name>.scm.azurewebsites.net/api/deployments`

endpoint, as shown in the following cURL example. Again, replace `<app_name>`

with the name of your app and `<deployment_user>`

with the username of your deployment credentials.

```
curl -u <deployment_user> https://<app_name>.scm.azurewebsites.net/api/deployments
```


#### Asynchronous zip deployment

While deploying synchronously, you might receive errors related to connection timeouts. Add `?isAsync=true`

to the URL to deploy asynchronously. You receive a response as soon as the zip file is uploaded with a `Location`

header pointing to the pollable deployment status URL. When polling the URL provided in the `Location`

header, you receive an HTTP 202 (Accepted) response while the process is ongoing and an HTTP 200 (OK) response once the archive has been expanded and the deployment completes successfully.

#### Microsoft Entra authentication

An alternative to using HTTP BASIC authentication for the zip deployment is to use a Microsoft Entra identity. Microsoft Entra identity might be needed if [HTTP BASIC authentication is disabled for the SCM site](../app-service/deploy-configure-credentials#disable-basic-authentication).

A valid Microsoft Entra access token for the user or service principal performing the deployment is required. An access token can be retrieved using the Azure CLI's `az account get-access-token`

command. The access token is used in the Authentication header of the HTTP POST request.

```
curl -X POST \
--data-binary "@<zip_file_path>" \
-H "Authorization: Bearer <access_token>" \
"https://<app_name>.scm.azurewebsites.net/api/zipdeploy"
```


### With PowerShell

The following example uses [Publish-AzWebapp](/en-us/powershell/module/az.websites/publish-azwebapp) upload the .zip file. Replace the placeholders `<group-name>`

, `<app-name>`

, and `<zip-file-path>`

.

```
Publish-AzWebapp -ResourceGroupName <group-name> -Name <app-name> -ArchivePath <zip-file-path>
```


This request triggers push deployment from the uploaded .zip file.

To review the current and past deployments, run the following commands. Again, replace the `<deployment-user>`

, `<deployment-password>`

, and `<app-name>`

placeholders.

```
$username = "<deployment-user>"
$password = "<deployment-password>"
$apiUrl = "https://<app-name>.scm.azurewebsites.net/api/deployments"
$base64AuthInfo = [Convert]::ToBase64String([Text.Encoding]::ASCII.GetBytes(("{0}:{1}" -f $username, $password)))
$userAgent = "powershell/1.0"
Invoke-RestMethod -Uri $apiUrl -Headers @{Authorization=("Basic {0}" -f $base64AuthInfo)} -UserAgent $userAgent -Method GET
```


## Deploy by using ARM Template

You can use [ZipDeploy ARM template extension](https://github.com/projectkudu/kudu/wiki/MSDeploy-VS.-ZipDeploy#zipdeploy) to push your .zip file to your function app.

### Example ZipDeploy ARM Template

This template includes both a production and staging slot and deploys to one or the other. Typically, you would use this template to deploy to the staging slot and then swap to get your new zip package running on the production slot.

```
{
"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
"appServiceName": {
"type": "string"
},
"deployToProduction": {
"type": "bool",
"defaultValue": false
},
"slot": {
"type": "string",
"defaultValue": "staging"
},
"packageUri": {
"type": "secureString"
}
},
"resources": [
{
"condition": "[parameters('deployToProduction')]",
"type": "Microsoft.Web/sites/extensions",
"apiVersion": "2021-02-01",
"name": "[format('{0}/ZipDeploy', parameters('appServiceName'))]",
"properties": {
"packageUri": "[parameters('packageUri')]",
"appOffline": true
}
},
{
"condition": "[not(parameters('deployToProduction'))]",
"type": "Microsoft.Web/sites/slots/extensions",
"apiVersion": "2021-02-01",
"name": "[format('{0}/{1}/ZipDeploy', parameters('appServiceName'), parameters('slot'))]",
"properties": {
"packageUri": "[parameters('packageUri')]",
"appOffline": true
}
}
]
}
```


For the initial deployment, you would deploy directly to the production slot. For more information, see [Slot deployments](functions-infrastructure-as-code#slot-deployments).

## Run functions from the deployment package

You can also choose to run your functions directly from the deployment package file. This method skips the deployment step of copying files from the package to the `wwwroot`

directory of your function app. Instead, the Functions runtime mounts the package file, and the contents of the `wwwroot`

directory become read-only.

Zip deployment integrates with this feature, which you can enable by setting the function app setting `WEBSITE_RUN_FROM_PACKAGE`

to a value of `1`

. For more information, see [Run your functions from a deployment package file](run-functions-from-deployment-package).

## Deployment customization

The deployment process assumes that the .zip file that you push contains a ready-to-run app. By default, no customizations are run. To enable the same build processes that you get with continuous integration, add the following to your application settings:

`SCM_DO_BUILD_DURING_DEPLOYMENT=true`


When you use .zip push deployment, this setting is **false** by default. The default is **true** for continuous integration deployments. When set to **true**, your deployment-related settings are used during deployment. You can configure these settings either as app settings or in a .deployment configuration file that's located in the root of your .zip file. For more information, see [Repository and deployment-related settings](https://github.com/projectkudu/kudu/wiki/Configurable-settings#repository-and-deployment-related-settings) in the deployment reference.

## Download your function app files

If you created your functions by using the editor in the Azure portal, you can download your existing function app project as a .zip file in one of these ways:

**From the Azure portal:**Sign in to the

[Azure portal](https://portal.azure.com), and then go to your function app.On the

**Overview**tab, select**Download app content**. Select your download options, and then select**Download**.

The downloaded .zip file is in the correct format to be republished to your function app by using .zip push deployment. The portal download can also add the files needed to open your function app directly in Visual Studio.

**Using REST APIs:**Use the following deployment GET API to download the files from your

`<function_app>`

project:`https://<function_app>.scm.azurewebsites.net/api/zip/site/wwwroot/`

Including

`/site/wwwroot/`

makes sure your zip file includes only the function app project files and not the entire site. If you aren't already signed in to Azure, you are asked to do so.

You can also download a .zip file from a GitHub repository. When you download a GitHub repository as a .zip file, GitHub adds an extra folder level for the branch. This extra folder level means that you can't deploy the .zip file directly as you downloaded it from GitHub. If you're using a GitHub repository to maintain your function app, you should use [continuous integration](functions-continuous-deployment) to deploy your app.


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-storage-blob-input.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-blob-input -->

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
