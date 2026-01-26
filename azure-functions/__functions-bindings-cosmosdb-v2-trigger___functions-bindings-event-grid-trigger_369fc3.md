---
merged_at: 2026-01-26T21:02:36.355614
merged_files: 2
---


---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

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
<!-- Source: N/A -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/scenario-database-changes-azure-sqldb -->

# Quickstart: Respond to Azure SQL Database changes using Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this Quickstart, you use Visual Studio Code to build an app that responds to changes in an Azure SQL Database table. After testing the code locally, you deploy it to a new serverless function app running in a Flex Consumption plan in Azure Functions.

The project source uses the Azure Developer CLI (azd) extension with Visual Studio Code to simplify initializing and verifying your project code locally, and deploying your code to Azure. This deployment follows current best practices for secure and scalable Azure Functions deployments.

Important

While responding to [changes in an Azure SQL database](functions-bindings-azure-mysql-trigger) is supported for all languages, this quickstart scenario currently only has examples for C#, Python, and TypeScript. To complete this quickstart, select one of these supported languages at the top of the article.

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

- The
[SQL Server (mssql) extension](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)for Visual Studio Code.

## Initialize the project

You can use the `azd init`

command from the command palette to create a local Azure Functions code project from a template.

In Visual Studio Code, open a folder or workspace in which you want to create your project.

Press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Initialize App (init)`

, and then choose**Select a template**.When prompted, search for and select

`Azure Functions with SQL Triggers and Bindings`

.When prompted, enter a unique environment name, such as

`sqldbchanges`

.

This command pulls the project files from the [template repository](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-sql) and initializes the project in the current folder or workspace. In `azd`

, the environment is used to maintain a unique deployment context for your app, and you can define more than one. It's also part of the name of the resource group you create in Azure.

This command pulls the project files from the [template repository](https://github.com/Azure-Samples/functions-quickstart-python-azd-sql) and initializes the project in the current folder or workspace. In `azd`

, the environment is used to maintain a unique deployment context for your app, and you can define more than one. It's also part of the name of the resource group you create in Azure.

This command pulls the project files from the [template repository](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-sql) and initializes the project in the current folder or workspace. In `azd`

, the environment is used to maintain a unique deployment context for your app, and you can define more than one. It's also part of the name of the resource group you create in Azure.

Before you can run your app locally, you must create the resources in Azure.

## Create Azure resources

This project is configured to use the `azd provision`

command to create a function app in a Flex Consumption plan, along with other required Azure resources that follow current best practices.

In Visual Studio Code, press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Sign In with Azure Developer CLI`

, and then sign in using your Azure account.Press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Provision Azure resources (provision)`

to create the required Azure resources.When prompted in the Terminal window, provide these required deployment parameters:

Prompt Description Select an Azure Subscription to use Select the subscription in which you want your resources to be created. *location*deployment parameterAzure region in which to create the resource group that contains the new Azure resources. Only regions that currently support the Flex Consumption plan are shown. *vnetEnabled*deployment parameterWhile the template supports creating resources inside a virtual network, to simplify deployment and testing, choose `False`

.

The `azd provision`

command uses your response to these prompts with the Bicep configuration files to create and configure these required Azure resources, following the latest best practices:

- Flex Consumption plan and function app
- Azure SQL Database (default name: ToDo)
- Azure Storage (required) and Application Insights (recommended)
- Access policies and roles for your account
- Service-to-service connections using managed identities (instead of stored connection strings)

Post-provision hooks also generate the *local.settings.json* file, which is required to run locally. This file contains the settings required to connect to your database in Azure.

## Review the code (optional)

The sample defines two functions:

| Function name | Code file | Trigger type | Description |
|---|---|---|---|
`httptrigger-sql-output` |
|

`ToDo`

table.`ToDoTrigger`

[sql_trigger.cs](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-sql/blob/main/sql_trigger.cs)`ToDo`

table for row-level changes and returns an object that represents the changed row.The `ToDoItem`

type is defined in [ToDoItem.cs](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-sql/blob/main/ToDoItem.cs).

| Function name | Code file | Trigger type | Description |
|---|---|---|---|
`http_trigger_sql_output` |
|

`ToDo`

table.`httptrigger-sql-output`

[sql_trigger_todo](https://github.com/Azure-Samples/functions-quickstart-python-azd-sql/blob/main/function_app.py#L15C5-L15C21)`ToDo`

table for row-level changes and returns an object that represents the changed row.The `ToDoItem`

type is defined in [todo_item.py](https://github.com/Azure-Samples/functions-quickstart-python-azd-sql/blob/main/todo_item.py).

| Function name | Code file | Trigger type | Description |
|---|---|---|---|
`httpTriggerSqlOutput` |
|

`ToDo`

table.`sqlTriggerToDo`

[sql_trigger.ts](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-sql/blob/main/src/functions/sql_trigger.ts)`ToDo`

table for row-level changes and returns an object that represents the changed row.The `ToDoItem`

type is defined in [ToDoItem.ts](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-sql/blob/main/src/models/ToDoItem.ts).

Both functions use the app-level `AZURE_SQL_CONNECTION_STRING_KEY_*`

environment variables that define an identity-based connection to the Azure SQL Database instance using Microsoft Entra ID authentication. These environment variables are created for you both in Azure (function app settings) and locally (local.settings.json) during the `azd provision`

operation.

## Connect to the SQL database

You can use the SQL Server (mssql) extension for Visual Studio Code to connect to the new database. This extension helps you make updates in the `ToDo`

table to run the SQL trigger function.

Press

`F1`and in the command palette search for and run the command`MS SQL: Add Connection`

.In the

**Connection dialog**, change**Input type**to**Browse Azure**and then set these remaining options:Option Choose Description **Server**Your SQL Server instance By default, all servers accessible to your Azure account are displayed. Use **Subscription**,**Resource group**, and**Location**to help filter the servers list.**Database**`ToDo`

The database created during the provisioning process. **Authentication type****Microsoft Entra ID**If you aren't already signed-in, select **Sign in**and sign in to your Azure account.**Tenant ID**The specific account tenant. If your account has more than one tenant, choose the correct tenant for your subscription. Select

**Connect**to connect to your database. The connection uses your local user account, which is granted admin permissions in the hosting server and mapped to`dbo`

in the database.In the

**SQL Server**view, locate and expand**Connections**and then your new server in SQL Server explorer. Expand**Tables**and verify that the`ToDo`

table exists. If it doesn't exist, you might need run`azd provision`

again and check for errors.

## Run the function locally

Visual Studio Code integrates with [Azure Functions Core tools](functions-run-local) to let you run this project on your local development computer before you publish to your new function app in Azure.

Press

`F1`and in the command palette search for and run the command`Azurite: Start`

.To start the function locally, press

`F5`or the**Run and Debug**icon in the left-hand side Activity bar.The

**Terminal**panel displays the output from Core Tools. Your app starts in the**Terminal**panel, and you can see the name of the function that's running locally.

With the app running, you can verify and debug both function triggers.

To verify the HTTP trigger function that writes to a SQL output binding:

Copy this JSON object, which you can also find in the

`test.http`

project file:`{ "id": "11111111-1111-1111-1111-111111111111", "order": 1, "title": "Test Todo Item", "url": "https://example.com", "completed": false }`

This data represents a row that you insert in your SQL database when you call the HTTP endpoint. The output binding translates the data object into an

`INSERT`

operation in the database.With the app running, in the

**Azure**view under**Workspace**expand**Local project**>**Functions**.Right-select your HTTP function (or

`Ctrl`+click on macOS), select**Execute function now**, paste the copied JSON data, and press`Enter`.The function handles the HTTP request and writes the item to the connected SQL database and returns the created object.

Back in the SQL Server explorer, right-select the

`ToDo`

table (or`Ctrl`+click on macOS), and choose**Select Top 1000**. When the query executes, it returns the inserted or updated row.Repeat Step 3 and resend the same data object with the same ID. This time, the output binding performs an

`UPDATE`

operation instead of an`INSERT`

and modifies the existing row in the database.

When you're done, type `Ctrl`+`C` in the terminal to stop the Core Tools process.

## Deploy to Azure

You can run the `azd deploy`

command from Visual Studio Code to deploy the project code to your already provisioned resources in Azure.

Press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Deploy to Azure (deploy)`

.The

`azd deploy`

command packages and deploys your code to the deployment container. The app is then started and runs in the deployed package.After the command completes successfully, your app is running in Azure. Make a note of the

`Endpoint`

value, which is the URL of your function app running in Azure.

## Invoke the function on Azure

In Visual Studio Code, press

`F1`and in the command palette search for and run the command`Azure: Open in portal`

, select`Function app`

, and choose your new app. Sign in with your Azure account, if necessary.Select

**Log stream**in the left pane, which connects to the Application Insights logs for your app.Return to Visual Studio Code to run both the functions in Azure.


Press

`F1`to open the command palette, search for and run the command`Azure Functions: Execute Function Now...`

.Search for and select your remote function app from the list, then select the HTTP trigger function.

As before, paste your JSON object data in

**Enter payload body**and press`Enter`.`{ "id": "11111111-1111-1111-1111-111111111111", "order": 1, "title": "Test Todo Item", "url": "https://example.com", "completed": false }`

To perform an

`INSERT`

instead of an`UPDATE`

, replace the`id`

with a new GUID value.Return to the portal and view the execution output in the log window.


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
